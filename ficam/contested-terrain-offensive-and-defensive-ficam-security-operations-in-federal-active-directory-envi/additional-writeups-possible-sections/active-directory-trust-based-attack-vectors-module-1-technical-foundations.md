# Active Directory Trust-Based Attack Vectors Module 1 – Technical Foundations

Active Directory Trust-Based Attack Vectors\
Module 1 – Technical Foundations

Active Directory remains the authoritative identity plane in the Fortune 500, mid-market, and every regulated vertical that still keeps a mainframe on life-support. Even where the corporate slide-deck promises “cloud-first,” the on-prem footprint continues to sign 90 % of privileged tickets, enforce GPO baselines, and anchor certificate templates whose retirement date is measured in decades. Inside that footprint, trust objects—stored as nTTrustedDomain entities and animated at runtime by the MS-ADTS and MS-KILE protocol stacks—form the cryptographic ligaments between every domain and forest. A single over-permissioned attribute in one of those objects is enough to convert a modest domain-level breach into cross-forest, Tier 0 compromise.

The security community’s systematic study of this projection began in 2015 with harmj0y’s “Trustpocalypse,” the first public proof that forest trusts do not filter the Enterprise Admins or built-in Administrator (500) SIDs. By wrapping those identifiers in an inter-realm TGT, an attacker could jump from a compromised resource forest into the root of an otherwise well-defended corporate forest. A 2017 follow-up operationalized intra-forest referral-ticket delegation, skeleton-key injection across shortcut trusts, and showed that selective authentication is silently bypassed whenever the ms-DS-Allowed-To-Authenticate attribute is absent. Since then the canon has grown to include SIDHistory injection, cross-forest resource-based constrained delegation, and quarantine-disabled external trusts—once exotic curios, now standard red-team fare mapped to MITRE ATT\&CK T1484.001, T1558.003, and T1558.001.

The default topology is an implicit mesh: every child domain automatically trusts its parent, every tree root automatically trusts every sibling, and transitive forest trusts extend that mesh across boundaries the risk register swears are air-gapped. Compromise one child and you can harvest the inter-realm krbtgt hash, mint a forged referral ticket, and replay it in the parent—or in any peer domain—without ever touching a DC in the target. Shortcut trusts introduced years ago to shave logon latency shorten the path even further, letting you circumvent Protected-Users lifetime restrictions and audit policies that fire only on forest-crossing tickets. Where cross-forest trusts exist, importing historical SIDs into sIDHistory and clearing TRUST\_ATTRIBUTE\_QUARANTINED\_DOMAIN lets you impersonate any principal in the foreign forest while appearing to originate from a legitimate, trusted DC.

Penetration testers must therefore be able to map the trust graph with LDAP filters and DsEnumerateDomainTrusts, interpret the TRUST\_ATTRIBUTE\_\* bit field that governs SID filtering, and weaponize the extracted trust key—whether RC4 or AES-256—to forge inter-realm TGTs that survive the tightest EDR baselines. Defenders must reciprocate by enabling SID filtering, enforcing selective authentication, purging stale sIDHistory, rotating trust keys every thirty days, and isolating Tier 0 inside an Enhanced Security Administrative Environment whose forests maintain no inbound trusts beyond a single, heavily monitored outbound gateway. Treat trust relationships as first-class security primitives, not invisible plumbing, or the modest compromise of one domain will cascade into enterprise-wide defeat.

Enter S4U2Self, the Microsoft Kerberos extension that allows any service equipped with an SPN to obtain a ticket to itself on behalf of an arbitrary security principal—no password, no TGT, no delegation bit required. The request is a vanilla TGS-REQ whose PA-FOR-USER field names the victim and whose sname points back to the caller; the KDC responds with a PAC-bearing ticket encrypted in the service’s long-term key. The returned ticket is forwardable only if the service is trusted for constrained delegation, but even a non-forwardable grant is still valid for local authorization decisions.

Attackers abuse the primitive in three recurring scenarios. First, local privilege escalation: a web shell or SQLi running as NT AUTHORITY\NETWORK SERVICE (i.e., the computer account) can mint a ticket for a domain admin and pass-the-ticket to Service Manager, instantly promoting the compromised context to BUILTIN\Administrators. Second, a stealthy alternative to silver tickets: because the PAC is signed by the KDC itself, the ticket is cryptographically genuine and never triggers “forged ticket” alerts; with the computer account hash harvested via DCSync or LSASS, the attacker can repeatedly impersonate high-value users without burning the golden krbtgt. Third, double-hop fuel: when constrained or resource-based delegation is configured, the forwardable ticket obtained through S4U2Self is immediately usable as evidence in an S4U2Proxy request, letting the attacker hop from the first service to any second service listed in msDS-AllowedToDelegateTo or msDS-AllowedToActOnBehalfOfOtherIdentity—often ending on a domain controller’s CIFS or LDAP SPN.

In short, S4U2Self turns any principal that knows a service’s Kerberos key—be it a compromised IIS AppPool, SQL Server, or print spooler—into a universal impersonation engine capable of manufacturing valid, high-privilege tickets without ever touching the victim’s credentials or TGT. Couple that with the trust-mapping techniques described earlier and you have a repeatable path from a single foothold to cross-forest, Tier 0 sovereignty: Kerberoast across the trust, S4U2Self for privilege escalation, forge an inter-realm TGT, and loop back through SIDHistory injection or RBCD until the entire estate answers to your command.

### **Active Directory Trust-Based Attack Vectors: Technical Foundations & Modern Threat Landscape**

### **Enumerating Domain & Forest Trusts**

When the red-team shell lands on a foreign domain-joined host, the first order of business is not to spray credentials or spin up Mimikatz—it is to map the **trust graph**.\
Every `trustedDomain` object in `CN=System,DC=corp,DC=local` is a **cryptographic treaty**: it lists who will accept whose tickets, under what encryption types, with which SID filters (if any), and whether the gate swings both ways.\
Mis-read that treaty and you waste hours on a forest you can never reach; read it correctly and you can convert a single-domain foothold into a **transitive, cross-forest skeleton key**.

Below we keep the original cmdlet & PowerView output **byte-for-byte**, but we **annotate each bit-field with the forensic meaning** and **add real-world attacker tradecraft** that the naked cmdlets never tell you.

***

#### 1. Built-in Enumeration – `Get-ADTrust` – What the Flags _Really_ Say

```powershell
PS C:\htb> Import-Module ActiveDirectory
PS C:\htb> Get-ADTrust -Filter *
```



| Original Field                                                                    | Hex Mask | ATT\&CK-mapped Interpretation (why you care)                                                                                                            |
| --------------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `TrustAttributes : 8`                                                             | `0x0008` | <p><code>TRUST_ATTRIBUTE_FOREST_TRANSITIVE</code><br>→ <strong>SIDHistory poison will flow</strong> unless you manually enable SID filtering.</p>       |
| `TrustAttributes : 32`                                                            | `0x0020` | <p><code>TRUST_ATTRIBUTE_WITHIN_FOREST</code><br>→ <strong>krbtgt hash is shared</strong>; Golden ticket minted in child works in parent instantly.</p> |
| `SelectiveAuthentication : False`                                                 | —        | **Every user from the other side** can authenticate to _any_ resource once they present a valid TGT.                                                    |
| `SIDFilteringQuarantined : False`                                                 | —        | **Quarantine is OFF**; attacker can inject SIDs such as `S-1-5-21-<Root>-500` and become EA in the target.                                              |
| <p><code>UsesAESKeys : False</code><br><code>UsesRC4Encryption : False</code></p> | —        | **Trust still negotiates RC4** (type 23) for inter-realm TGTs; attacker downgrades to `krbtgt` NTLM hash and forges tickets without ever touching AES.  |
| `TGTDelegation : False`                                                           | —        | **Looks safe**, but _only_ blocks _user_ TGT delegation; **does NOT block S4U2Self → S4U2Proxy** if constrained delegation is enabled elsewhere.        |



> **Pro-tip**: Pipe to `| Select-Object Name,TrustAttributes,@{N='Flags';E={$_.TrustAttributes -band 0x3F}}` to decode on the fly.

***

#### 2. PowerView – `Get-DomainTrust` & `Get-DomainTrustMapping` – Adding the Neighbours’ Neighbours

```powershell
PS C:\htb> Get-DomainTrustMapping
```

The extra rows you see (`logistics.ad → megacorp.ad`) are **NOT** returned by the native cmdlet; PowerView recursively queries every discovered DC via DsEnumerateDomainTrusts **with the DS\_DIRECTORY\_SERVICE\_REQUIRED flag**, giving you the **three-level trust diamond**:

```
INLANEFREIGHT.AD
├─ intra-forest  ➜ child.inlanefreight.ad
└─ inter-forest  ➜ logistics.ad
                 └─ outbound ➜ megacorp.ad
```

**Attacker translation**

* **Outbound** from logistics → megacorp means **you cannot walk that edge** unless you first compromise a principal _inside_ `logistics.ad`.
* But any **user or machine** already in `logistics.ad` can be **phished, kerberoasted, or relayed** to pivot into `megacorp.ad`.
* Keep the edge in your notes—later, when you pull the `logistics.ad` krbtgt hash, you can **forge a referral TGT** that impersonates `admin@megacorp.ad` and presents it **back to logistics DCs**; they will happily forward you to `megacorp.ad` DCs because the **outbound trust** is transitive.

***

#### 3. Visualising the Graph – One-liner That Generates DOT & SVG

```powershell
# On your C2 beacon
Get-DomainTrustMapping | %{
    '"{0}" -> "{1}" [label="{2}/{3}"]; ' -f $_.SourceName,$_.TargetName,$_.TrustDirection,$_.TrustType
} | Set-Content trusts.dot
# Copy locally & render
dot -Tsvg trusts.dot -o trusts.svg
```

Open the SVG in BloodHound’s graph view or drop it into your report—**blue teams instantly see why the “isolated” OT forest is only two hops from the enterprise root**.

***

#### 4. Extra Intel You Can Only Get with LDAP Filters

```powershell
# Find every trust that disabled SID filtering (quarantine = 0)
(Get-ADObject -LDAPFilter "(&(objectClass=trustedDomain)(!(trustAttributes:1.2.840.113556.1.4.803:=8)))" -Properties trustAttributes,trustPartner)
```



| trustPartner     | Risk Score | Justification                                                                                                                           |
| ---------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `vendor.local`   | **10/10**  | External non-quarantined trust created for M\&A in 2019; SIDHistory injection from `vendor.local` → `EA` in your forest is **trivial**. |
| `dev.corp.local` | **7/10**   | Intra-forest, but **SelectiveAuth = False**; any compromised dev account can **DCSync** the parent.                                     |



***

#### 5. Operational Checklist

1. **Run both built-in and PowerView enumerations**—they return **different trust flags** (MS-ADTS vs. NetLogon RPC).
2. **Document directionality**: outbound trusts are **egress edges** for you, **ingress edges** for the adversary once they own the other side.
3. **Highlight non-quarantined, non-selective-authentication trusts**—these are **golden bridges** for SIDHistory & RBCD abuse.
4. **Log creation & last-change timestamps**: a trust whose `WhenChanged` is **newer than the last change-control ticket** is a **rogue trust**—tear it down.
5. **Export the graph**, render it, and **attach it to the risk register**—trust relationships **must** be treated as \*\*Tier 0 attack paths.

Keep the cmdlet output you already copied, but **never again stare at raw text** without decoding the bit masks. The moment you see `TrustAttributes : 8` and `SelectiveAuthentication : False`, you know you are **one forged ticket away** from owning the next forest—**act accordingly**.
