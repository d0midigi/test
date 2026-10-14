# hackherway wiki cyberpunk princess

### Reconnaissance

Reconnaissance is the first phase of ethical hacking where information about the target system is gathered. This phase is crucial for understanding the attack surface and planning subsequent exploitation attempts.

{% hint style="warning" %}
Always ensure you have proper authorization before conducting any reconnaissance activities on systems you don't own.
{% endhint %}

#### Passive Reconnaissance

Passive reconnaissance involves gathering information without directly interacting with the target system. This approach is stealthy and less likely to trigger security alerts.

**OSINT Techniques**

Open Source Intelligence (OSINT) leverages publicly available information to gather intelligence about targets. This includes social media, public records, and online databases.

Example: Using theHarvester for OSINT

{% code title="theharvester" %}
```bash
theharvester -d target.com -b google,bing,linkedin
theharvester -d target.com -b all -f output.html
```
{% endcode %}

**DNS Enumeration**

DNS enumeration reveals valuable information about a target's infrastructure including subdomains, mail servers, and name servers.

DNS Enumeration Commands

{% code title="dns-enum" %}
```bash
dnsrecon -d target.com
dnsenum target.com
fierce --domain target.com
```
{% endcode %}

**Social Engineering**

Social engineering exploits human psychology to gather information or gain unauthorized access. Common techniques include phishing, pretexting, and baiting.

#### Active Reconnaissance

Active reconnaissance involves direct interaction with target systems to gather information. While more invasive, it provides detailed technical information.

**Port Scanning**

Port scanning identifies open ports and services running on target systems, providing crucial information for exploitation attempts.

Nmap scanning techniques

{% code title="nmap-scans" %}
```bash
nmap -sS -sV -O target.com        # SYN scan with version and OS detection
nmap -p- -T4 target.com           # Scan all ports
nmap -sU --top-ports 1000 target.com  # UDP scan top 1000 ports
```
{% endcode %}

**Service Detection**

Identifying specific services and their versions helps determine potential vulnerabilities and attack vectors.

**Vulnerability Scanning**

Automated vulnerability scanners identify known security weaknesses in target systems.

### Exploitation

The exploitation phase involves leveraging discovered vulnerabilities to gain unauthorized access to target systems.

#### Web Application Attacks

Web applications are common targets due to their accessibility and often poor security implementations.

**SQL Injection**

SQL injection attacks exploit improperly sanitized user input to execute malicious SQL queries against backend databases.

Basic SQL Injection payloads

{% code title="sql-payloads" %}
```sql
' OR '1'='1
' UNION SELECT NULL,NULL,NULL--
' AND 1=2 UNION SELECT table_name,NULL FROM information_schema.tables--
```
{% endcode %}

**Cross-Site Scripting (XSS)**

XSS attacks inject malicious scripts into web pages viewed by other users, potentially stealing sessions or credentials.

{% hint style="danger" %}
XSS can lead to account takeover, data theft, and malware distribution.
{% endhint %}

**CSRF Attacks**

Cross-Site Request Forgery tricks authenticated users into performing unintended actions on web applications.

#### Network Attacks

Network-level attacks target communication protocols and infrastructure components.

**Man-in-the-Middle Attacks**

MITM attacks intercept and potentially modify communications between two parties without their knowledge.

**Session Hijacking**

Session hijacking involves stealing or predicting valid session tokens to gain unauthorized access to web applications.

**ARP Spoofing**

ARP spoofing redirects network traffic through an attacker's machine by poisoning ARP tables.

### Active Directory Attacks

Active Directory is a prime target in enterprise environments, offering extensive control over Windows domains.

#### AD Enumeration

Enumeration gathers information about AD structure, users, groups, and trusts.

**BloodHound Analysis**

BloodHound uses graph theory to reveal hidden relationships and attack paths in Active Directory environments.

BloodHound collection examples

{% code title="bloodhound-collection" %}
```bash
SharpHound.exe -c All -d domain.local
bloodhound-python -u user -p password -ns dc.domain.local -d domain.local
```
{% endcode %}

**LDAP Queries**

LDAP queries extract valuable information from Active Directory without requiring elevated privileges.

#### Kerberos Attacks

Kerberos authentication vulnerabilities enable various ticket-based attacks.

**Golden Ticket Attack**

Golden tickets provide domain-wide access by forging Kerberos TGTs using the krbtgt account hash.

Detection: Monitor krbtgt account usage and implement regular password rotation.

**Silver Ticket Attack**

Silver tickets forge service tickets for specific services without requiring domain admin privileges.

**Kerberoasting**

Kerberoasting extracts service account hashes for offline cracking.

Kerberoasting examples

{% code title="kerberoast" %}
```bash
GetUserSPNs.py domain.local/user:password -dc-ip 10.0.0.1 -request
Rubeus.exe kerberoast /outfile:hashes.txt
```
{% endcode %}

#### Delegation Attacks

Kerberos delegation misconfigurations allow privilege escalation and lateral movement.

**Unconstrained Delegation**

Unconstrained delegation allows a service to impersonate any user to any service.

**Constrained Delegation**

Constrained delegation limits impersonation to specific services but can still be abused.

**Resource-Based Constrained Delegation**

RBCD allows resources to configure which accounts can delegate to them.

### Post-Exploitation

Post-exploitation activities maintain access, escalate privileges, and move laterally through compromised networks.

#### Privilege Escalation

Privilege escalation exploits system misconfigurations or vulnerabilities to gain higher-level access.

**Windows Privilege Escalation**

Windows systems offer numerous privilege escalation vectors including service misconfigurations, unquoted paths, and token impersonation.

Windows PrivEsc enumeration

{% code title="windows-privesc" %}
```powershell
whoami /priv
net localgroup administrators
schtasks /query /fo LIST /v
wmic service get name,pathname,startmode
```
{% endcode %}

**Linux Privilege Escalation**

Linux privilege escalation often involves exploiting SUID binaries, cron jobs, or kernel vulnerabilities.

Linux PrivEsc enumeration

{% code title="linux-privesc" %}
```bash
find / -perm -u=s -type f 2>/dev/null
getcap -r / 2>/dev/null
cat /etc/crontab
sudo -l
```
{% endcode %}

#### Persistence Mechanisms

Persistence ensures continued access to compromised systems even after reboots or security updates.

**Registry Persistence**

Windows registry offers multiple locations for establishing persistence through auto-start entries.

**Scheduled Tasks**

Scheduled tasks provide reliable persistence with flexible execution triggers.

#### Lateral Movement

Lateral movement techniques spread access across networked systems.

**PSExec**

PSExec enables remote command execution on Windows systems using SMB.

**WMI**

Windows Management Instrumentation provides stealthy remote execution capabilities.

**RDP**

Remote Desktop Protocol offers interactive access to Windows systems.

### Tools & Resources

Essential tools for ethical hacking and penetration testing.

#### Scanning Tools

**Nmap**

Network discovery and security auditing tool for port scanning and service detection.

**Masscan**

High-speed TCP port scanner capable of scanning the entire Internet in under 6 minutes.

**Nikto**

Web server scanner that tests for dangerous files, outdated versions, and vulnerabilities.

#### Exploitation Frameworks

**Metasploit**

Comprehensive penetration testing framework with extensive exploit database.

**Empire**

PowerShell and Python post-exploitation framework for Windows and Linux.

**Cobalt Strike**

Advanced threat emulation software for red team operations.

#### Post-Exploitation Tools

**Mimikatz**

Credential extraction tool for Windows systems, capable of dumping passwords and hashes.

**BloodHound**

Active Directory attack path mapping tool using graph theory.

**PowerView**

PowerShell tool for Active Directory reconnaissance and exploitation.

#### Defense & Monitoring

**Sysmon**

Windows system monitoring tool that logs detailed system activity.

**OSSEC**

Open-source host intrusion detection system for log analysis and integrity checking.

**Suricata**

High-performance network threat detection engine with IDS/IPS capabilities.
