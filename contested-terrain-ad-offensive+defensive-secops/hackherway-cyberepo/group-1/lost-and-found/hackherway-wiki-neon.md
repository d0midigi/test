# hackherway wiki neon

## Fundamentals

* Introduction to Ethical Hacking
* Hacking Methodology
* Cyber Kill Chain
* MITRE ATT\&CK Framework
* Legal & Ethical Considerations
* Scope & Rules of Engagement
* Authorization & Contracts
* Reporting & Disclosure

## Network Fundamentals

* OSI Model
* TCP/IP Stack
* Network Topologies
* Network Protocols
* TCP vs UDP
* HTTP/HTTPS
* DNS Protocol
* Email Protocols (SMTP / POP / IMAP)
* Network Devices
* Routers & Switches
* Firewalls & IDS/IPS
* IP Addressing & Subnetting
* IPv4 & IPv6
* CIDR Notation
* Network Hardening

## Reconnaissance & Enumeration

* Passive Reconnaissance (OSINT)
* OSINT Tools & Techniques
* Google Dorking
* Social Media Intelligence
* Domain & IP Research
* Active Reconnaissance
* Network Scanning (Nmap)
* Port Scanning Techniques
* Service & Version Detection
* Vulnerability Scanning
* Service Enumeration
* DNS Enumeration
* SNMP Enumeration
* SMB/NetBIOS Enumeration
* LDAP Enumeration
* FTP Enumeration
* SSH Enumeration
* Web Application Enumeration
* Technology Stack Identification
* Directory & File Discovery
* Subdomain Enumeration
* API Endpoint Discovery

## Web Application Security

* OWASP Top 10
* Injection Attacks
* SQL Injection (SQLi)
  * Manual SQLi Exploitation
  * Automated SQLi (SQLMap)
* NoSQL Injection
* OS Command Injection
* LDAP Injection
* XML/XXE Injection
* Cross-Site Scripting (XSS)
  * Reflected XSS
  * Stored XSS
  * DOM-Based XSS
* CSRF Attacks
* Server-Side Request Forgery (SSRF)
* Server-Side Template Injection (SSTI)
* File Inclusion Attacks
  * Local File Inclusion (LFI)
  * Remote File Inclusion (RFI)
  * Path Traversal
* File Upload Vulnerabilities
* Authentication & Authorization
  * Broken Authentication
  * Session Management Flaws
  * Password Attacks
* API Security
  * REST API Testing
  * GraphQL Security
  * JWT Token Attacks
  * OAuth/OIDC Security
  * WebSocket Security
* Business Logic Vulnerabilities
* Race Conditions
* Insecure Deserialization

## Network Exploitation

* Man-in-the-Middle (MITM) Attacks
* ARP Spoofing/Poisoning
* DNS Spoofing
* DHCP Attacks
* Session Hijacking
  * TCP Session Hijacking
  * HTTP Session Hijacking
* Network Sniffing & Analysis
  * Packet Capture (Wireshark)
  * Traffic Analysis
* DoS & DDoS Attacks
  * SYN Flood
  * UDP Flood
  * Amplification Attacks
* Wireless Network Attacks
  * WiFi Cracking (WPA/WPA2/WPA3)
  * Rogue Access Points
  * Evil Twin Attacks
  * Bluetooth Attacks
* VLAN Hopping
* VPN Exploitation

## System Exploitation

* Metasploit Framework
  * MSF Basics & Usage
  * Exploit Development
  * Post-Exploitation Modules
* Buffer Overflow Attacks
  * Stack-Based Overflow
  * Heap-Based Overflow
* Return-Oriented Programming (ROP)
* Format String Vulnerabilities
* Shellcode Development
* Kernel Exploitation
* Exploit Mitigation Bypass
  * ASLR Bypass
  * DEP/NX Bypass
  * Stack Canary Bypass
* Remote Code Execution (RCE)
* Service Exploitation
  * SMB Exploitation (EternalBlue)
  * RPC Exploitation
  * Database Exploitation

## Active Directory Security

* AD Enumeration & Reconnaissance
  * BloodHound Analysis
  * LDAP Queries
  * PowerView Enumeration
  * User & Computer Enumeration
  * Domain Trust Enumeration

### Advanced AD Security Topics

* Advanced AD Enumeration
* Kerberoasting + AS-REP Roasting
* Golden | Silver Ticket Attacks
* AD Delegation Attacks
* AD CS (Certificate Services)
* Advanced BloodHound Analysis
* LDAP Injection Attack
* NTLM Relay Attack
* Advanced Kerberoasting
* Kerberos Attacks
  * Kerberoasting (T1558.003)
  * AS-REP Roasting (T1558.004)
  * Golden Ticket Attack
  * Silver Ticket Attack
  * Diamond Ticket Attack
  * Sapphire Ticket Attack
  * Kerberos Reflection Attack
  * Delegation Attacks
    * Unconstrained Delegation
    * Constrained Delegation
    * Resource-Based Constrained Delegation
  * Certificate Services (AD CS) Attacks
    * ESC1–ESC15 (various AD CS abuse techniques)
* Credential Access Attacks
  * DCSync Attack (T1003.006)
  * NTLM Relay Attack
  * Pass-the-Hash (PtH)
  * Pass-the-Ticket (PtT)
  * Overpass-the-Hash
  * Password Spraying
  * DPAPI Credential Extraction
* AD Persistence Mechanisms
  * Golden Ticket Persistence
  * DCShadow (T1207)
  * Skeleton Key (T1556.001)
  * AdminSDHolder Abuse
  * DSRM Password Abuse
  * ACL & Permission Abuse (WriteDACL, GenericAll)
  * ForceChangePassword
* Domain Trust Attacks
  * SID History Injection
  * Cross-Forest Attacks

## Post-Exploitation

* Privilege Escalation
  * Windows Privilege Escalation
  * Linux Privilege Escalation
  * Kernel Exploits
  * SUID/SGID Exploitation
  * Sudo Misconfigurations
  * Token Impersonation (T1134)
  * UAC Bypass Techniques
* Credential Harvesting
  * Mimikatz Usage
  * LSASS Memory Dumping
  * SAM Database Extraction
  * Credential Manager/Vault
  * Browser Credential Extraction
* Persistence Techniques
  * Registry Persistence
  * Scheduled Tasks / Cron Jobs
  * Service Creation
  * Startup Folder
  * DLL Hijacking
  * Backdoor Accounts
  * Web Shells
* Lateral Movement
  * PSExec
  * WMI (Windows Management Instrumentation)
  * RDP Hijacking
  * WinRM
  * DCOM Lateral Movement
  * SSH Lateral Movement
* Data Exfiltration
  * Exfiltration Techniques
  * DNS Exfiltration
  * ICMP Exfiltration
  * Steganography
* Covering Tracks
  * Log File Manipulation
  * Timestomping
  * Artifact Removal

## Red Team Operations

* Red Team Methodology
* Threat Emulation
* Adversary Simulation
* Operational Security (OPSEC)
  * OPSEC Principles
  * Attribution Avoidance
* Command & Control (C2)
  * C2 Framework Development
  * Cobalt Strike
  * Covenant
  * Sliver
  * Havoc Framework
  * C2 Infrastructure Setup
* EDR/AV Evasion
  * Signature Evasion
  * Code Obfuscation
  * AMSI Bypass
  * ETW Bypass
  * Process Injection
  * Living-Off-The-Land (LOLBins)
    * Windows LOLBins
    * Linux GTFOBins
  * Advanced Bypass Techniques
    * Sandbox Evasion
    * DLL Sideloading
    * Process Hollowing
* Covert Channels
  * DNS Tunneling
  * ICMP Tunneling
  * HTTP/S Tunneling
* Social Engineering
  * Phishing Campaigns
  * Pretexting
  * Vishing & Smishing
* Physical Security Assessment
  * Tailgating
  * Physical Access Controls
  * Lockpicking

## Mobile & IoT Security

* Android Security Testing
  * APK Analysis
  * Android Reverse Engineering
  * Root Detection Bypass
* iOS Security Testing
  * IPA Analysis
  * Jailbreak Detection Bypass
* Mobile API Security
* IoT Device Exploitation
  * Firmware Analysis
  * IoT Protocol Testing (MQTT, CoAP)
  * Hardware Hacking (UART, JTAG)

## Cloud Security

* AWS Security Testing
  * AWS Enumeration
  * S3 Bucket Misconfiguration
  * IAM Privilege Escalation
  * Lambda Function Exploitation
* Azure Security Testing
  * Azure AD Enumeration
  * Azure Storage Attacks
  * Azure RBAC Exploitation
* Google Cloud Platform (GCP)
  * GCP Enumeration
  * GCS Bucket Attacks
* Container Security
  * Docker Security
  * Kubernetes Security
  * Container Escape Techniques

## Cryptography & Password Attacks

* Cryptography Fundamentals
  * Symmetric Encryption
  * Asymmetric Encryption
  * Hashing Algorithms
* Cryptographic Attacks
  * Padding Oracle Attack
  * Weak Cipher Exploitation
  * Downgrade Attacks
* Password Cracking
  * Hashcat
  * John the Ripper
  * Rainbow Tables
  * Brute Force Attacks
  * Dictionary Attacks
  * Hybrid Attacks

## Tools & Frameworks

* Scanning & Enumeration Tools
  * Nmap (see Nmap Deep Dive)
  * Masscan
  * Nuclei
* Exploitation Frameworks
  * Metasploit Framework
  * Exploit-DB
* Web Application Testing Tools
  * Burp Suite
  * OWASP ZAP
  * SQLMap
  * ffuf
* Post-Exploitation Tools
  * PowerShell Empire
  * Covenant
* Active Directory Tools
  * BloodHound
  * Impacket
  * CrackMapExec
  * Rubeus
* Defense & Monitoring Tools
  * SIEM Solutions
  * IDS/IPS (Snort, Suricata)
  * EDR Solutions

## Defensive Security

* Blue Team Operations
* Threat Hunting
* Incident Response
* Digital Forensics
* System Hardening
  * Windows Hardening
  * Linux Hardening
  * Active Directory Hardening
* Detection Engineering
  * Sigma Rules
  * YARA Rules
  * Log Analysis & SIEM
  * Windows Event Logs
  * Sysmon
  * Splunk
  * ELK Stack
* Vulnerability Management
  * Patch Management
  * Vulnerability Assessment
* Security Frameworks
  * NIST Cybersecurity Framework
  * CIS Controls
  * ISO 27001

## Certifications & Career

* Offensive Security Certifications
  * OSCP
  * OSEP
  * OSWE
  * CRTO
  * CRTP
* Defensive Security Certifications
  * CISSP
  * SANS GIAC Certifications
* General Security Certifications
  * CompTIA Security+
  * CEH (Certified Ethical Hacker)
* Career Paths
  * Penetration Tester
  * Red Team Operator
  * Bug Bounty Hunter
  * Security Researcher

## Resources & References

* Learning Platforms
  * HackTheBox
  * TryHackMe
  * PortSwigger Web Security Academy
  * PentesterLab
* Bug Bounty Platforms
  * HackerOne
  * Bugcrowd
  * Intigriti
* CTF Resources
  * CTFtime
  * picoCTF
* Books & Guides
  * OWASP Testing Guide
  * The Hacker's Playbook Series
  * RTFM: Red Team Field Manual
* Community & Forums
  * Discord Servers
  * Reddit Communities
  * InfoSec Twitter

***

## Reconnaissance

Reconnaissance is the first phase of ethical hacking where information about the target system is gathered. This phase is crucial for understanding the attack surface and planning subsequent exploitation attempts.

{% hint style="warning" %}
Always ensure you have proper authorization before conducting any reconnaissance activities on systems you don't own.
{% endhint %}

### Passive Reconnaissance

Passive reconnaissance involves gathering information without directly interacting with the target system. This approach is stealthy and less likely to trigger security alerts.

#### OSINT Techniques

Open Source Intelligence (OSINT) leverages publicly available information to gather intelligence about targets. This includes social media, public records, and online databases.

Example: Using theHarvester for OSINT

{% code title="theharvester" %}
```bash
theharvester -d target.com -b google,bing,linkedin
theharvester -d target.com -b all -f output.html
```
{% endcode %}

#### DNS Enumeration

DNS enumeration reveals valuable information about a target's infrastructure including subdomains, mail servers, and name servers.

{% code title="DNS enumeration examples" %}
```bash
dnsrecon -d target.com
dnsenum target.com
fierce --domain target.com
```
{% endcode %}

#### Social Engineering

Social engineering exploits human psychology to gather information or gain unauthorized access. Common techniques include phishing, pretexting, and baiting.

### Active Reconnaissance

Active reconnaissance involves direct interaction with target systems to gather information. While more invasive, it provides detailed technical information.

#### Port Scanning

Port scanning identifies open ports and services running on target systems, providing crucial information for exploitation attempts.

{% code title="Nmap scanning techniques" %}
```bash
nmap -sS -sV -O target.com        # SYN scan with version and OS detection
nmap -p- -T4 target.com           # Scan all ports
nmap -sU --top-ports 1000 target.com  # UDP scan top 1000 ports
```
{% endcode %}

#### Service Detection

Identifying specific services and their versions helps determine potential vulnerabilities and attack vectors.

#### Vulnerability Scanning

Automated vulnerability scanners identify known security weaknesses in target systems.

## Exploitation

The exploitation phase involves leveraging discovered vulnerabilities to gain unauthorized access to target systems.

### Web Application Attacks

Web applications are common targets due to their accessibility and often poor security implementations.

#### SQL Injection

SQL injection attacks exploit improperly sanitized user input to execute malicious SQL queries against backend databases.

Example: Basic SQL Injection payloads

{% code title="SQLi payloads" %}
```sql
' OR '1'='1
' UNION SELECT NULL,NULL,NULL--
' AND 1=2 UNION SELECT table_name,NULL FROM information_schema.tables--
```
{% endcode %}

#### Cross-Site Scripting (XSS)

XSS attacks inject malicious scripts into web pages viewed by other users, potentially stealing sessions or credentials.

{% hint style="danger" %}
XSS can lead to account takeover, data theft, and malware distribution.
{% endhint %}

#### CSRF Attacks

Cross-Site Request Forgery tricks authenticated users into performing unintended actions on web applications.

### Network Attacks

Network-level attacks target communication protocols and infrastructure components.

#### Man-in-the-Middle Attacks

MITM attacks intercept and potentially modify communications between two parties without their knowledge.

#### Session Hijacking

Session hijacking involves stealing or predicting valid session tokens to gain unauthorized access to web applications.

#### ARP Spoofing

ARP spoofing redirects network traffic through an attacker's machine by poisoning ARP tables.

## Active Directory Attacks

Active Directory is a prime target in enterprise environments, offering extensive control over Windows domains.

### AD Enumeration

Enumeration gathers information about AD structure, users, groups, and trusts.

#### BloodHound Analysis

BloodHound uses graph theory to reveal hidden relationships and attack paths in Active Directory environments.

{% code title="BloodHound collection" %}
```bash
SharpHound.exe -c All -d domain.local
bloodhound-python -u user -p password -ns dc.domain.local -d domain.local
```
{% endcode %}

#### LDAP Queries

LDAP queries extract valuable information from Active Directory without requiring elevated privileges.

### Kerberos Attacks

Kerberos authentication vulnerabilities enable various ticket-based attacks.

#### Golden Ticket Attack

Golden tickets provide domain-wide access by forging Kerberos TGTs using the krbtgt account hash.

Detection: Monitor krbtgt account usage and implement regular password rotation.

#### Silver Ticket Attack

Silver tickets forge service tickets for specific services without requiring domain admin privileges.

#### Kerberoasting

Kerberoasting extracts service account hashes for offline cracking.

{% code title="Kerberoasting examples" %}
```bash
GetUserSPNs.py domain.local/user:password -dc-ip 10.0.0.1 -request
Rubeus.exe kerberoast /outfile:hashes.txt
```
{% endcode %}

### Delegation Attacks

Kerberos delegation misconfigurations allow privilege escalation and lateral movement.

* Unconstrained Delegation: allows a service to impersonate any user to any service.
* Constrained Delegation: limits impersonation to specific services but can still be abused.
* Resource-Based Constrained Delegation (RBCD): allows resources to configure which accounts can delegate to them.

## Post-Exploitation

Post-exploitation activities maintain access, escalate privileges, and move laterally through compromised networks.

### Privilege Escalation

Privilege escalation exploits system misconfigurations or vulnerabilities to gain higher-level access.

#### Windows Privilege Escalation

Windows systems offer numerous privilege escalation vectors including service misconfigurations, unquoted paths, and token impersonation.

{% code title="Windows PrivEsc enumeration" %}
```powershell
whoami /priv
net localgroup administrators
schtasks /query /fo LIST /v
wmic service get name,pathname,startmode
```
{% endcode %}

#### Linux Privilege Escalation

Linux privilege escalation often involves exploiting SUID binaries, cron jobs, or kernel vulnerabilities.

{% code title="Linux PrivEsc enumeration" %}
```bash
find / -perm -u=s -type f 2>/dev/null
getcap -r / 2>/dev/null
cat /etc/crontab
sudo -l
```
{% endcode %}

### Persistence Mechanisms

Persistence ensures continued access to compromised systems even after reboots or security updates.

#### Registry Persistence

Windows registry offers multiple locations for establishing persistence through auto-start entries.

#### Scheduled Tasks

Scheduled tasks provide reliable persistence with flexible execution triggers.

### Lateral Movement

Lateral movement techniques spread access across networked systems.

#### PSExec

PSExec enables remote command execution on Windows systems using SMB.

#### WMI

Windows Management Instrumentation provides stealthy remote execution capabilities.

#### RDP

Remote Desktop Protocol offers interactive access to Windows systems.

## Network Concepts

Understanding core networking concepts is essential for ethical hacking and penetration testing.

### Network Fundamentals

Core networking principles that form the foundation of modern computer networks.

#### OSI Model

The Open Systems Interconnection model describes seven layers of network communication:

{% code title="OSI Model Layers" %}
```
Layer 7 (L7) - Application (HTTP | FTP | SMTP)
Layer 6 (L6) - Presentation (SSL/TLS | Encryption)
Layer 5 (L5) - Session (NetBIOS | SQL)
Layer 4 (L4) - Transport (TCP | UDP)
Layer 3 (L3) - Network (IP | ICMP | Routers)
Layer 2 (L2) - Data Link (Ethernet Switches | MAC Addresses)
Layer 1 (L1) - Physical (Cables | Hubs | Signals)
```
{% endcode %}

#### TCP/IP Stack

The practical four-layer model used in modern networking.

#### Common Protocols

Essential protocols every ethical hacker should understand.

### Network Topologies

Different network architectures and their security implications.

### Network Devices

Routers, switches, firewalls, and other infrastructure components.

### Subnetting & VLANs

Network segmentation techniques for security and performance.

## Tools & Resources

Essential tools for ethical hacking and penetration testing.

### Scanning Tools

#### Nmap

Network discovery and security auditing tool for port scanning and service detection.

#### Masscan

High-speed TCP port scanner capable of scanning the entire Internet in under 6 minutes.

#### Nikto

Web server scanner that tests for dangerous files, outdated versions, and vulnerabilities.

### Exploitation Frameworks

#### Metasploit

Comprehensive penetration testing framework with extensive exploit database.

#### Empire

PowerShell and Python post-exploitation framework for Windows and Linux.

#### Cobalt Strike

Advanced threat emulation software for red team operations.

### Post-Exploitation Tools

#### Mimikatz

Credential extraction tool for Windows systems, capable of dumping passwords and hashes.

#### BloodHound

Active Directory attack path mapping tool using graph theory.

#### PowerView

PowerShell tool for Active Directory reconnaissance and exploitation.

### Defense & Monitoring

#### Sysmon

Windows system monitoring tool that logs detailed system activity.

#### OSSEC

Open-source host intrusion detection system for log analysis and integrity checking.

#### Suricata

High-performance network threat detection engine with IDS/IPS capabilities.

***

hackherway — Your comprehensive guide to ethical hacking and cybersecurity. Learn, practice, and defend with confidence.

🔒 Always hack ethically. Always get authorization.

## Resources

* Main Website: https://www.hackherway.com
* GitHub: https://github.com/calyxia
* Certifications
* Learning Paths
* Community

© 2025 hackherway | Ethical Hacking Wiki | Built with ♥ by Calyxia

This wiki is for educational purposes only. Unauthorized access to computer systems is illegal.
