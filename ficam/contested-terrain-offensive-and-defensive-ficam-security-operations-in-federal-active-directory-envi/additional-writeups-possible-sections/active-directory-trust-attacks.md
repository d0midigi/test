# Active Directory Trust Attacks

Active Directory’s trust subsystem remains one of the most under-scrutinized segments of the modern identity attack surface. Even organizations that have publicly committed to a “cloud-first” strategy still maintain on-premise forests that authenticate the majority of privileged accounts, enforce GPO-based security baselines, and house certificate authorities whose templates are nowhere near retirement. Within these forests, trust objects—stored as nTTrustedDomain entities and materialized at run-time through the MS-ADTS and MS-KILE protocol stacks—govern every cross-domain or cross-forest authentication request. If even one of these objects is configured with overly permissive attributes, an adversary who has already obtained administrative control of a single domain can project that privilege across every trusting domain, and ultimately into foreign forests that were presumed isolated.

The security community’s systematic study of this projection began in 2015 with harmj0y’s “Trustpocalypse” article, which demonstrated that forest trusts do not filter the Enterprise Admins or built-in Administrator SIDs. By forging an inter-realm ticket-granting ticket that contained these high-privilege identifiers, an attacker could parachute from a compromised resource forest into the root of an otherwise well-defended corporate forest. Two years later, a follow-up guide expanded the playbook to include intra-forest referral-ticket delegation, skeleton-key injection across shortcut trusts, and the discovery that selective-authentication enforcement is silently disabled for S4U proxy requests when the ms-DS-Allowed-To-Authenticate attribute is absent. Since then, researchers have added SIDHistory injection, cross-forest resource-based constrained delegation, and the abuse of quarantine-disabled external trusts to the canon, turning what was once an exotic corner case into a staple of red-team methodology.

These techniques matter because the default trust topology found in most enterprises is an implicit mesh: every child domain automatically trusts its parent, every tree root automatically trusts every other tree root, and transitive forest trusts extend that mesh across security boundaries that finance or regulatory teams assume are air-gapped. An operator who compromises a single child domain can therefore harvest the inter-realm krbtgt hash, mint a forged referral ticket, and replay it in the parent—or in any peer domain—without ever touching a domain controller in the target. If the environment also contains shortcut trusts introduced years ago to reduce logon latency, the attacker can further shorten the trust path, circumvent lifetime restrictions imposed by the Protected Users group, and evade audit policies that fire only when a ticket crosses a forest boundary. Where cross-forest trusts are involved, the same operator can import historical SIDs into sIDHistory, disable SID filtering by setting TRUST\_ATTRIBUTE\_QUARANTINED\_DOMAIN to zero, and then use resource-based constrained delegation to impersonate any principal in the foreign forest—all while appearing to originate from a legitimate, trusted domain controller.

Understanding these mechanics is no longer optional for either offensive or defensive teams. Penetration testers must be able to map the trust graph with LDAP queries and DsEnumerateDomainTrusts, interpret the bitmask values that govern SID filtering and quarantine behavior, and weaponize the extracted trust keys to forge inter-realm TGTs that survive scrutiny by enterprise detection stacks. Conversely, defenders must harden every trust object by enabling SID filtering, enforcing selective authentication, purging stale sIDHistory entries, rotating trust keys on a thirty-day cadence, and isolating tier-zero assets inside an Enhanced Security Administrative Environment whose forests maintain no inbound trusts beyond a single, heavily monitored outbound gateway. Only by treating trust relationships as first-class security primitives—rather than invisible plumbing—can an organization prevent the modest compromise of one domain from cascading into enterprise-wide, tier-zero defeat.

### Active Directory Trust-Based Attack Vectors

#### Module 1 – Technical Foundations

1. Problem Scope\
   Active Directory (AD) remains the dominant identity plane in the Fortune 500, mid-market, and regulated verticals, even where Azure AD or Entra ID is present. The residual on-prem footprint—still authoritative for Kerberos, LDAP, certificate templates, GPOs, and NTLM—creates a hybrid attack surface whose trust boundaries are frequently overlooked during cloud-migration risk models. Trust objects, represented internally as nTTrustedDomain entities and exposed through MS-ADTS and MS-KILE protocols, form the cryptographic and authorization backbone between domains and forests. Misconfiguration or over-permissioning of these objects allows an adversary to convert compromise of a single domain into cross-forest, tier-zero privilege.
2. Historical Context\
   In 2015, harmj0y’s “Trustpocalypse” post first weaponized the fact that forest trusts do not enforce SID filtering on the Enterprise Admins (EA) and Administrators (500) SIDs, enabling skeleton-key injection across forest boundaries. Subsequent 2017 research operationalized intra-forest TGT delegation, forged trust tickets, and discovered that ms-DS-Allowed-To-Authenticate and ms-DS-TrustForest-Trust-Info attributes are not validated during S4U proxy requests. The corpus has since expanded to include abuse of selective authentication, SIDHistory injection, and cross-forest RBCD. The module synthesizes these findings into a repeatable attack chain mapped to MITRE ATT\&CK (T1484.001, T1558.003, T1558.001).
3. Trust Taxonomy\
   3.1 Intra-forest\
   – Parent-child (automatic two-way transitive).\
   – Tree-root (automatic two-way transitive).\
   – Shortcut (manual, transitive, can collapse trust path length).\
   Attack primitive: TGT delegation across Kerberos referral tickets; krbtgt hash is shared only within the forest, enabling Golden-Ticket replay in any child domain.

3.2 Cross-forest\
– External (non-transitive, NTLM or Kerberos, selective auth optional).\
– Forest (transitive, Kerberos only, SID filtering enabled by default but bypassable).\
Attack primitive: SIDHistory filtration gaps, forged inter-realm TGTs, and RBCD across forest boundary when selective auth is disabled.

4. Module Objectives\
   Upon completion the operator will be able to:\
   a. Enumerate trust topology via LDAP queries, DsEnumerateDomainTrusts, and MS-LSAD RPC.\
   b. Identify trust attributes (TRUST\_ATTRIBUTE\_\* flags) that disable SID filtering or enable quarantine bypass.\
   c. Forge inter-realm TGTs using the target trust key (RC4 or AES-256) obtained through DCSync or KRBTGT hash extraction.\
   d. Exploit intra-forest shortcut trusts to reduce ticket lifetime and evade PAS-aligned audit controls.\
   e. Weaponize RBCD across forests by chaining sIDHistory injection with S4U2Self/S4U2Proxy.\
   f. Recommend hardening artifacts: enable SID filtering, enforce selective authentication, remove sIDHistory, rotate trust keys ≥ 30 days, and implement tier-zero ESAE / Red-Forest isolation.

### Why Devote Cycles to Trust Abuse?

Because the moment a penetration test stalls at the edge of a well-hardened domain, trusts become the covert bridge back to privilege. A foothold that offers no local path to DA can still export Kerberos roasting across an intra-forest trust, cough up the hash of a service account in a child domain, and let that child’s krbtgt carry us uphill into the parent we started in. Pivot once more and a transitive forest trust—often inherited from a forgotten merger—can welcome the same forged TGT into a partner forest whose admins have never heard of your red-team badge. From there, SID-history injection, cross-forest RBCD, or a simple relay through their Certificate Authority loops the attack right back into the originally assessed forest, this time at tier-zero.

Throughout the module we will dissect both the pedestrian and the arcane vectors that make this hop possible: referral-ticket forgery across shortcut links, selective-authentication bypasses stitched together with Linux Impacket suites, and Windows-native Rubeus chains that turn a compromised jump host into a multi-forest skeleton key. Real incident artifacts—packet captures of inter-realm TGT exchanges, DCSync logs that betray trust-key rotation schedules, and firewall flows that accidentally expose 464/3268 between forests—will be replayed in lab form so you can trigger, observe, and silence each primitive. Whether you wear red or blue, the outcome is the same: an intuitive, protocol-level grasp of why a trust relationship is never just a line in a Visio diagram, but a living authentication channel that can either extend your reach or collapse your entire estate.

### S4U2Self Active Directory Attacks

Service-for-User-to-Self (S4U2Self) is a Microsoft Kerberos extension that allows a service to obtain a service ticket **to itself** on behalf of any arbitrary security principal **without needing that principal’s password or TGT**.\
The request is nothing more than a normal TGS-REQ whose `PA-FOR-USER` field names the victim account and whose `sname` points back to the requesting service.\
If the service account (or the machine account it runs under) has an SPN and holds valid Kerberos keys, the KDC will issue a ticket that contains the victim’s PAC—groups, SID history, and all—encrypted in the service’s long-term key.

Because **no delegation bit needs to be set**, the primitive works even when:

* constrained delegation is absent,
* the target user is marked “Account is sensitive and cannot be delegated”, or
* the user is in the Protected Users group.

The returned ticket is **forwardable only if the service is also trusted for constrained delegation (protocol transition)**, but even a non-forwardable ticket is still valid for local authorization decisions.

Attackers abuse this behavior in three recurring scenarios:

1. **Local privilege escalation**\
   A web shell or SQLi running as `NT AUTHORITY\NETWORK SERVICE` (which acts as the computer account on the wire) can call S4U2Self to mint a ticket for a domain admin, then pass-the-ticket to a local privileged service such as Service Manager, instantly promoting the compromised context to `BUILTIN\Administrators` .
2. **Stealthy alternative to silver tickets**\
   Because the PAC is signed by the KDC itself, the resulting ticket is cryptographically genuine and never triggers “forged ticket” detections. With the computer account hash in hand (harvested via DCSync, LSASS dump, or NetNTLMv1 downgrade) an attacker can repeatedly impersonate high-value users without burning the krbtgt golden key .
3. **Feeding S4U2Proxy (double-hop)**\
   When constrained or resource-based delegation is configured, the forwardable ticket obtained through S4U2Self is immediately usable as evidence in an S4U2Proxy request, letting the attacker hop from the first service to any second service listed in the `msDS-AllowedToDelegateTo` or `msDS-AllowedToActOnBehalfOfOtherIdentity` attributes—often ending on a domain controller’s CIFS or LDAP SPN .

In short, S4U2Self turns any principal that knows a service’s Kerberos key—be it a compromised IIS AppPool, SQL Server, or print spooler—into a universal impersonation engine, capable of manufacturing valid, high-privilege tickets without ever touching the victim user’s credentials or TGT.

