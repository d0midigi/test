Technical Rationale for the Table of Contents Structure
The structure follows a deliberate pedagogical progression tailored for defensive training curricula:

Part I establishes immutable protocol-level understanding so defenders can recognize why the misconfiguration exists;

Part II dedicates focused chapters to the offensive mechanics and tooling (including explicit BloodHound and PowerView enumeration logic) to enable "know thy adversary" competency without prescribing real-world execution;

Part III maps each offensive element to layered preventive, detective, and responsive controls with concrete technical rationales grounded in Microsoft event schemas, RFC behaviors, and gMSA architecture;

Part IV operationalizes the knowledge through labs and case studies with emphasis on reproducible, academically rigorous content. Subtopics were selected to cover the complete A-Z lifecycle:

Protocol → Discovery → Exploitation Mechanics → Tooling → Advanced Variants → Full Defensive Stack → Training Delivery → Futures

While remaining convertible to LaTeX via direct mapping of numbered sections to \\chapter, \\section, and \\subsection commands. All terminology adheres to neutral professional standards (e.g., "exploiting the misconfiguration," "vulnerable service principal," "target environment") to satisfy publishing guidelines. This ensures the book delivers immediately actionable and meaningful defensive value while maintaining technical depth and balance for all readers.

================================================================================================================



\*\*Introduction\*\*

Understanding Active Directory

\*\*Detecting and Mitigating Active Directory Compromises\*\*

&#x09;Kerberoasting

&#x09; Authentication Server Response (AS-REP) Roasting

&#x09; Password Spraying

&#x09; MachineAccountQuota Compromise

&#x09; Unconstrained Delegation

&#x09; Password in Group Policy Preferences (GPP) Compromise

&#x09; Active Directory Certificate Services (AD CS) Compromise

&#x09; Golden Certificate

&#x09; DCSync

&#x09; Dumping ntds.dit

&#x09; Golden Ticket

&#x09; Silver Ticket

&#x09; Golden Security Assertion Markup Language (SAML)

&#x09; Microsoft Entra Connect Compromise

&#x09; One-Way Domain Trust Bypass

&#x09; Security Identifier (SID) History Compromise

&#x09; Skeleton Key

&#x09; \*\*Detecting Active Directory Compromise with Canaries

&#x09;

&#x09;Appendix A-Active Directory Security Controls

&#x09;Appendix B-Active Directory Events



Domain Controller Events

Active Directory Certificate Services Certificate Authority (AD CS CA) Events

Active Directory Federation Services (AD FS) Events

Microsoft Entra Connect Server Events

Computer Objects Configured for Unconstrained Delegation Events

Computer Objects Compromised by a Silver Ticket



Detecting and Mitigating Active Directory Compromises



There are many known and observed techniques used to compromise AD DS, AD CS, and AD FS. Malicious actors target these services to escalate their privileges and move laterally across enterprise IT networks. This guidance addresses the most common AD DS, AD CS and AD FS techniques, providing an overview of each technique, as well as how to mitigate it. This guidance organizes the outlined compromises in the sequence they are typically executed against Active Directory, beginning with those sued to escalate privileges and move laterally and concluding with compromises aimed at establishing persistence.

===============================================================================================================



\### PART I: FOUNDATIONS

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 1: Active Directory in the Modern Enterprise

&#x20; </summary>



<ul>

<li><b>1.1.</b> The Evolution of Active Directory (2000-2026)</li>

<li><b>1.2.</b> Why Active Directory Remains a Prime Target for Cyberattacks</li>

<li><b>1.3. Active Directory vs. Novell NetWare (NDS e-Directory):</b> Coexistence and Different Realities</li>

<li><b>1.4.</b> The Expanding Attack Surface</li>

<li><b>1.5.</b> Regulatory and Compliance Landscape (NIS2, DORA, Zero Trust Mandates)</li>

<li><b>1.6. Threat Landscape Overview:</b> Nation-State, Ransomware, and Insider Threats</li></ul>

</details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 2: Active Directory Architectural Deep Dive

&#x20; </summary>



<ul>

<li><b>2.1. Logical Architecture:</b> Forests, Domains, Trees, and Trusts</li>

<li><b>2.2. Physical Architecture:</b> Domain Controllers (DCs), Sites and Services, and Domain Replication</li>

<li><b>2.3. Naming Conventions:</b> DNS, NetBIOS, and LDAP Naming Contexts</li>

<li><b>2.4.</b> The Global Catalog and Its Role</li>

<li><b>2.5.</b> Schema and Configuration Partitions</li>

<li><b>2.6.</b> Flexible Single Master Operations (FSMO) Roles</li>

<li><b>2.7.</b> Group Policy Architecture and Processing Order</li>

<li><b>2.8.</b> Active Directory Certificate Services (AD CS) Architecture

<li><b>2.9.</b> Active Directory Federation Services (AD FS) Architecture</li>

<li><b>2.10.</b> Read-Only Domain Controllers (RODCs)</li></ul>

</details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 3: Authentication and Authorization Internals

&#x20; </summary>



<ul>

<li><b>3.1. NTLM Authentication:</b> Protocol Internals and Weaknesses</li>

<li><b>3.2. Kerberos Authentication:</b> Deep Protocol Analysis</li><ul>

<li><b>3.2.1.</b> AS-REQ / AS-REP</li>

<li><b>3.2.2.</b> TGS-REQ / TGS-REP</li>

<li><b>3.2.3.</b> PAC Validation and Signature Mechanisms</li>

<li><b>3.2.4. Kerberos Delegation:</b> Unconstrained, Constrained, and RBCD</li></ul>

<li><b>3.3.</b> LDAP Bind and Channel Binding</li>

<li><b>3.4.</b> Claims-Based Authentication and Dynamic Access Control (DAC)</li>

<li><b>3.5. NTLM vs. Kerberos:</b> When Each Is Used</li>

<li><b>3.6.</b> Security Access Tokens and Access Control Lists (DACLs, SACLs)</li>

<li><b>3.7.</b> Managed Service Accounts (MSA) and Group Managed Service Accounts (gMSA)</li>

<li><b>3.8.</b> Windows Hello for Business and FIDO2 Integration</li>

<li><b>3.9.</b> Certificate-Based Authentication (PKINIT / Smart Cards)</li></ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 4: Setting Up Your Lab Environment

&#x20; </summary>



&#x20;<ul>

<li><strong>4.1.</strong> Lab Architecture Design (Multi-Forest, Hybrid)</li>

<li><strong>4.2.</strong> Virtualization Platforms: Proxmox, VMware, Hyper-V, Cloud Labs</li>

<li><strong>4.3.</strong> Automated Lab Deployment with Terraform and Ansible</li>

<li><strong>4.4.</strong> Deploying Vulnerable AD Environments (DVAD, GOAD, PurpleCloud)</li>

<li><strong>4.5.</strong> Integrating Entra ID / Azure for Hybrid Labs</li>

<li><strong>4.6.</strong> Installing and Configuring Monitoring and Logging</li>

<li><strong>4.7.</strong> Snapshotting and Reverting: Lab Hygiene Best Practices</li>

<li><strong>4.8.</strong> Simulating Real-World Enterprise Complexity</li>

</ul></details>



\---



\### PART II: RECONNAISSANCE AND ENUMERATION



<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 5: Passive Reconnaissance

&#x20; </summary>



&#x20; <ul>

<li><strong>5.1.</strong> OSINT for Active Directory Targets</li>

<li><strong>5.2.</strong> DNS Reconnaissance: External and Internal</li>

<li><strong>5.3.</strong> Harvesting Credentials from Public Breaches</li>

<li><strong>5.4.</strong> LinkedIn and Social Engineering Intelligence</li>

<li><strong>5.5.</strong> Identifying VPN, RDP, and Exposed Services</li>

<li><strong>5.6.</strong> Metadata Extraction from Public Documents</li>

&#x20; <li><strong>5.7.</strong> Identifying Hybrid and Cloud Footprints</li></ul>

</details>



<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 6: Active Directory Enumeration

&#x20; </summary>



<ul>

<li><strong>6.1.</strong> Initial Enumeration Without Credentials

<ul>

<li><strong>6.1.1.</strong> Null Session Enumeration</li>

<li><strong>6.1.2.</strong> LDAP Anonymous Binds</li>

<li><strong>6.1.3.</strong> DNS Zone Transfer Attempts</li>

<li><strong>6.1.4.</strong> SMB Enumeration and Signing Detection</li>

<li><strong>6.1.5.</strong> MSRPC Enumeration (RID Cycling, User Enumeration)</li>

</ul>

</li>

<li><strong>6.2.</strong> Authenticated Enumeration

<ul>

<li><strong>6.2.1.</strong> BloodHound / SharpHound / AzureHound Collection</li>

<li><strong>6.2.2.</strong> LDAP Queries with ldapsearch, PowerView, and ADExplorer</li>

<li><strong>6.2.3.</strong> Enumerating Users, Groups, OUs, and Computers</li>

<li><strong>6.2.4.</strong> Enumerating Group Policy Objects (GPOs)</li>

<li><strong>6.2.5.</strong> Enumerating ACLs and DACLs</li>

<li><strong>6.2.6.</strong> Enumerating Trusts and Cross-Forest Relationships</li>

<li><strong>6.2.7.</strong> Enumerating AD CS: Certificate Templates and CAs</li>

<li><strong>6.2.8.</strong>\\\&nbsp;Enumerating Service Principal Names (SPNs)</li>

<li><strong>6.2.9.</strong> Enumerating LAPS, BitLocker, and Credential Vaults</li>

<li><strong>6.2.10.</strong> Enumerating gMSA Passwords and Permissions</li>

</ul>

</li>

<li><strong>6.3.</strong> Automated Enumeration Frameworks

<ul>

<li><strong>6.3.1.</strong> BloodHound CE and Custom Cypher Queries</li>

<li><strong>6.3.2.</strong> PingCastle and Purple Knight for Posture Assessment</li>

<li><strong>6.3.3.</strong> ADRecon and SOAPHound</li>

<li><strong>6.3.4.</strong> Adalanche and Other Graph-Based Tools</li>

</ul>

</li>

<li><strong>6.4.</strong> Defensive Detection of Enumeration Activity</li>

&#x20; </ul></details>



\## PART III: ACCESS AND CREDENTIAL ATTACKS



\---

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 7: Gaining Initial Access

&#x20; </summary>



&#x20; <ul>

<li><strong>7.1. Password Spraying:</strong> Techniques and Evasion</li>

<li><strong>7.2.</strong> Brute-Force Attacks Against Exposed Services</li>

<li><strong>7.3.</strong> Exploiting Publicly Facing Services (Exchange, ADFS, RDWeb)</li>

<li><strong>7.4.</strong> Phishing for Credentials and Initial Footholds</li>

<li><strong>7.5.</strong> Exploiting VPN and Remote Access Gateways</li>

<li><strong>7.6.</strong> Abusing Default and Weak Configurations</li>

<li><strong>7.7.</strong> Supply Chain and Trusted Relationship Abuse</li>

<li><strong>7.8.</strong> Physical Access Vectors (Rogue Devices, Network Implants)</li>

<li><strong>7.9.</strong> Exploiting Misconfigured Network Access Control (NAC Bypass)</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 8: Credential Theft and Harvesting

&#x20; </summary>



&#x20; <ul>

<li><strong>8.1.</strong> SAM Database Extraction</li>

<li><strong>8.2.</strong> LSASS Memory Dumping

<ul>

<li><strong>8.2.1.</strong> Mimikatz, pypykatz, and Alternatives</li>

<li><strong>8.2.2.</strong> Covert Dump Techniques (<code>MiniDumpWriteDump</code>, <code>Comsvcs.dll</code>)</li>

<li><strong>8.2.3.</strong> Bypass Credential Guard and PPL</li>

</ul>

</li>

<li><strong>8.3.</strong> <code>NTDS.dit</code> Extraction

<ul>

<li><strong>8.3.1.</strong> VSS Shadow Copy</li>

<li><strong>8.3.2.</strong> <code>ntdsutil</code> and DCSYNC Comparison</li>

</ul>

</li>

<li><strong>8.4.</strong> Cached Credentials and DPAPI Secrets</li>

<li><strong>8.5.</strong> Credential Harvesting from Network Traffic</li>

<li><strong>8.6.</strong> Keylogging and Screen Capture</li>

<li><strong>8.7.</strong> Credential Theft from Browsers, Vaults, and Password Managers</li>

<li><strong>8.8.</strong> Extracting Credentials from Group Policy Preferences (<code>cpassword</code>)</li>

<li><strong>8.9.</strong> Harvesting Credentials from SCCM/MECM</li>

<li><strong>8.10.</strong> LAPS Password Retrieval</li>

<li><strong>8.11.</strong> gMSA Password Extraction and Abuse</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 9: NTLM Relay and Coercion Attacks

&#x20; </summary>



&#x20; <ul>

<li><strong>9.1.</strong> Understanding NTLM Relay Attack Theory</li>

<li><strong>9.2. Responder and Inveigh:</strong> LLMNR/NBNS/mDNS Poisoning</li>

<li><strong>9.3.</strong> NTLM Relay to SMB, LDAP, LDAPS, HTTP, MSSQL</li>

<li><strong>9.4.</strong> Coercion Techniques

<ul>

<li><strong>9.4.1.</strong> PetitPotam and MS-EFSRPC Abuse</li>

<li><strong>9.4.2.</strong> PrinterBug / SpoolSample (MS-RPRN)</li>

<li><strong>9.4.3.</strong> DFSCoerce (MS-DFSNM)</li>

<li><strong>9.4.4.</strong> ShadowCoerce and Other Coercion Vectors</li>

</ul>

</li>

<li><strong>9.5.</strong> Relay to AD CS (ESC8 and HTTP Enrollment)</li>

<li><strong>9.6.</strong> NTLM Relay in IPv6 Environments (<code>mitm6</code>)</li>

<li><strong>9.7.</strong> WebDAV-Based Relay Attacks</li>

<li><strong>9.8.</strong> Cross-Protocol Relay Scenarios</li>

<li><strong>9.9.</strong> Defenses: EPA, LDAP Signing, Channel Binding, SMB Signing</li>

</ul></details>



\---



\## PART IV: PRIVILEGE ESCALATION



<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 10: Local Privilege Escalation on Domain-Joined Hosts</summary>



&#x20; <ul>

<li><strong>10.1.</strong> Token Impersonation and Potato Attacks (<code>GodPotato</code>, <code>PrintSpoofer</code>)</li>

<li><strong>10.2.</strong> Unquoted Service Paths and DLL Hijacking</li>

<li><strong>10.3.</strong> <code>AlwaysInstallElevated</code> Exploitation</li>

<li><strong>10.4.</strong> Scheduled Task and Service Misconfigurations</li>

<li><strong>10.5.</strong> Abusing <code>SeImpersonate, SeAssignPrimaryToken</code>, and Other Privileges</li>

<li><strong>10.6.</strong> Credential Harvesting from Local Hosts for Domain Escalation</li>

<li><strong>10.7.</strong> Exploiting Vulnerable Drivers (BYOVD)</li>

<li><strong>10.8.</strong> UAC (User Access Control) Bypass Techniques</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 11: Domain Privilege Escalation

&#x20; </summary>



&#x20; <ul>

<li><strong>11.1.</strong> Kerberoasting

<ul>

<li><strong>11.1.1.</strong> Traditional Kerberoasting</li>

<li><strong>11.1.2.</strong> Targeted Kerberoasting (Setting SPNs)</li>

<li><strong>11.1.3.</strong> AS-REP Roasting</li>

<li><strong>11.1.4.</strong> Cracking Strategies (Hashcat, John, Rules, Wordlists)</li>

</ul>

</li>

<li><strong>11.2.</strong> ACL/DACL Abuse Paths

<ul>

<li><strong>11.2.1.</strong> <code>WriteDACL, GenericAll, GenericWrite</code></li>

<li><code></code><strong>11.2.2.</strong> Ownership Abuse (<code>WriteOwner</code>)</li>

<li><strong>11.2.3.</strong> <code>AddMember, ForceChangePassword</code></li>

<li><strong>11.2.4.</strong> Shadow Credentials (<code>msDS-KeyCredentialLink</code>)</li>

<li><strong>11.2.5.</strong> Targeted ACL Chains via BloodHound</li>

</ul>

</li>

<li><strong>11.3.</strong> Group Policy Abuse

<ul>

<li><strong>11.3.1.</strong> GPO Delegation Exploitation</li>

<li><strong>11.3.2.</strong> Creating Malicious GPOs</li>

<li><strong>11.3.3.</strong> Immediate Task Abuse</li>

</ul>

</li>

<li><strong>11.4.</strong> Kerberos Delegation Abuse

<ul>

<li><strong>11.4.1.</strong> Unconstrained Delegation Exploitation</li>

<li><strong>11.4.2.</strong> Constrained Delegation Abuse (<code>S4U2Self, S4U2Proxy</code>)</li>

<li><strong>11.4.3.</strong> Resource-Based Constrained Delegation (RBCD) Attacks</li>

</ul>

</li>

<li><strong>11.5.</strong> AD CS Exploitation (ESC1\\\&ndash;ESC15+)

<ul>

<li><strong>11.5.1.</strong> Misconfigured Certificate Templates (ESC1, ESC2, ESC3)</li>

<li><strong>11.5.2.</strong> Vulnerable CA Configuration (ESC6, ESC7)</li>

<li><strong>11.5.3.</strong> NTLM Relay to HTTP Enrollment (ESC8)</li>

<li><strong>11.5.4.</strong> Newer ESC Vectors (ESC9\\\&ndash;ESC15 and Beyond)</li>

<li><strong>11.5.5.</strong> Certipy, Certify, and ForgeCert Usage</li>

</ul>

</li>

<li><strong>11.6.</strong> MSSQL Server Linked Server Abuse</li>

<li><strong>11.7.</strong> Exchange Server Privilege Escalation</li>

<li><strong>11.8.</strong> SCCM/MECM Abuse for Privilege Escalation</li>

<li><strong>11.9.</strong> WSUS Exploitation</li>

<li><strong>11.10.</strong> <code>DNSAdmins</code> Abuse</li>

<li><strong>11.11.</strong> Backup Operator Privilege Abuse</li>

<li><strong>11.12.</strong> Schema and Configuration Partition Abuse</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 12: Cross-Trust and Cross-Forest Attacks

&#x20; </summary>



&#x20; <ul>

<li><strong>12.1.</strong> Trust Types and Security Boundaries Revisited</li>

<li><strong>12.2.</strong> SID History Injection</li>

<li><strong>12.3.</strong> SID Filtering Bypass Techniques</li>

<li><strong>12.4.</strong> Cross-Forest Kerberoasting</li>

<li><strong>12.5.</strong> Foreign Group Membership Exploitation</li>

<li><strong>12.6.</strong> Trust Key Extraction and Golden Ticket Across Trusts</li>

<li><strong>12.7.</strong> PAM (Privilege Access Management) Trust Abuse</li>

<li><strong>12.8.</strong> Selective Authentication Bypass</li>

<li><strong>12.9.</strong> PrinterBug Across Trusts</li>

</ul></details>

\---

\### PART V: LATERAL MOVEMENT AND PERSISTENCE



<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 13: Lateral Movement Techniques

&#x20; </summary>



&#x20; <ul>

<li><strong>13.1.</strong> Pass-the-Hash (PtH)</li>

<li><strong>13.2.</strong> Pass-the-Ticket (PtT)</li>

<li><strong>13.3.</strong> Overpass-the-Hash (OtPH) / Pass-the-Key (PtK)</li>

<li><strong>13.4.</strong> Pass-the-Certificate</li>

<li><strong>13.5.</strong> Remote Code Execution (RCE) Methods</li>

<li><strong>13.5.1.</strong> PsExec and SMBExec</li>

<li><strong>13.5.2.</strong> WMI (Windows Management Instrumentation and and WinRM (Windows Remote) Execution</li>

<li><strong>13.5.3.</strong> Distributed Component Object Model (DCOM) Lateral Movement</li>

<li><strong>13.5.4.</strong> SSH (Secure Shell) on Windows</li>

<li><strong>13.5.5.</strong> RDP (Remote Desktop Protocol) Hijacking and Shadowing</li>

<li><strong>13.6.</strong> Lateral Movement via Scheduled Tasks and Services</li>

<li><strong>13.7.</strong> Abusing Windows Administrative Shares (<code>C$</code>, <code>ADMIN$</code>)</li>

<li><strong>13.8.</strong> Lateral Movement Through MSSQL (Microsoft SQL)</li>

<li><strong>13.9.</strong> Lateral Movement via SCCM (System Center Configuration Manager)</li>

<li><strong>13.10.</strong> Living-Off-The-Land Binaries (LOLBins) for Lateral Movement</li>

<li><strong>13.11.</strong> Command \\\&amp; Control (C2) Frameworks and Active Directory</li>

<li><strong>13.11.1.</strong> Cobalt Strike</li>

<li><strong>13.11.2.</strong> Sliver</li>

<li><strong>13.11.3.</strong> Mythic</li>

<li><strong>13.11.4.</strong> Havoc</li>

<li><strong>13.11.5.</strong> Nighthawk</li>

<li><strong>13.12.</strong> Pivoting Through Segmented Networks</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 14: Domain Dominance

&#x20; </summary>



&#x20; <ul>

<li><strong>14.1.</strong> DCSync Attack (Replicating Directory Changes)</li>

<li><strong>14.2.</strong> DCShadow Attack (Rogue Domain Controller)</li>

<li><strong>14.3.</strong> AdminSDHolder and SDProp Abuse</li>

<li><strong>14.4.</strong> Skeleton Key Attack</li>

<li><strong>14.5.</strong> Custom SSP Injection</li>

<li><strong>14.6.</strong> Directory Service Restore Mode (DSRM) Backdoor</li>

<li><strong>14.7.</strong> Primary Group ID Manipulation</li>

<li><strong>14.8.</strong> SID History Backdoor</li>

<li><strong>14.9.</strong> Machine Account Quota Abuse</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 15: Persistence Mechanisms

&#x20; </summary>



&#x20; <ul>

<li><strong>15.1.</strong> Golden Ticket Attacks

<ul>

<li><strong>15.1.1.</strong> Traditional Golden Tickets (<code>KRBTGT</code>)</li>

<li><strong>15.1.2.</strong> Diamond Tickets</li>

<li><strong>15.1.3.</strong> Sapphire Tickets</li></ul>

</li>

<li><strong>15.2.</strong> Silver Ticket Attacks</li>

<li><strong>15.3.</strong> Golden Certificate (Stolen CA Private Key)</li>

<li><strong>15.4.</strong> Rogue Certificate Authority Persistence</li>

<li><strong>15.5.\\\&nbsp;</strong>Certificate-Based Persistence (User and Machine Certificates)</li>

<li><strong>15.6.</strong> Kerberos Delegation Backdoors</li>

<li><strong>15.7.</strong> GPO-Based Persistence</li>

<li><strong>15.8.</strong> Scheduled Tasks and Registry Run Keys via Domain Resources</li>

<li><strong>15.9.</strong> WMI Event Subscriptions</li>

<li><strong>15.10.</strong> DLL (Dynamic Link Library) Search Order Hijacking on Domain Controllers</li>

<li><strong>15.11.</strong> Modifying <code>ntds.dit</code> Schema for Hidden Attributes</li>

<li><strong>15.12.</strong> Trustworthy Domain Controller Certificates</li>

<li><strong>15.13.</strong> Shadow Credentials for Persistent Access</li>

<li><strong>15.14.</strong> Account Manipulation (Hidden Admin Accounts, Service Accounts)</li>

<li><strong>15.15.</strong> Persistence via AD FS Token Signing Certificate (Golden SAML)</li>

</ul></details>

\---

\### PART VI: HYBRID AND CLOUD ATTACK PATHS

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 16: Entra ID (Azure AD) Fundamentals for AD Practitioners

&#x20; </summary>



&#x20; <ul>

<li><strong>16.1.</strong> Entra ID Architecture and Terminology</li>

<li><strong>16.2. Azure AD Connect / Cloud Sync:</strong> How Identities Synchronize</li>

<li><strong>16.3. Authentication Methods:</strong> PHS, PTA, Federation</li>

<li><strong>16.4.</strong> Conditional Access Policies</li>

<li><strong>16.5.</strong> Managed Identities and Service Principals</li>

<li><strong>16.6.</strong> Microsoft Graph API and Permissions Model</li>

<li><strong>16.7.</strong> Entra ID Roles and Privileged Identity Management (PIM)</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 17: Attacking Hybrid AD Environments

&#x20; </summary>



&#x20; <ul>

<li><strong>17.1.</strong> Compromising Azure AD Connect Servers

<ul>

<li><strong>17.1.1.</strong> Extracting Sync Credentials (DPAPI, AADInternals)</li>

<li><strong>17.1.2.</strong> Password Hash Sync (PHS) Exploitation</li>

<li><strong>17.1.3.</strong> Pass-Through Authentication (PTA) Agent Backdoors</li>

</ul>

</li>

<li><strong>17.2.</strong> On-Prem to Cloud Escalation Paths

<ul>

<li><strong>17.2.1.</strong> Seamless SSO and <code>AZUREADSSOACC$</code> Abuse</li>

<li><strong>17.2.2.</strong> Cloud Kerberos Trust Exploitation</li>

<li><strong>17.2.3.</strong> Abusing Hybrid Joined Devices</li>

</ul>

</li>

<li><strong>17.3.</strong> Cloud to On-Prem Escalation Paths</li>

<li><strong>17.4.</strong> Abusing Entra ID Service Principals and App Registrations</li>

<li><strong>17.5.</strong> Consent Grant Attacks (Illicit Consent)</li>

<li><strong>17.6.</strong> Token Theft and Replay in Entra ID</li>

<li><strong>17.7.</strong> Device Code Phishing</li>

<li><strong>17.8.</strong> Entra ID Certificate-Based Authentication Abuse</li>

<li><strong>17.9.</strong> Attacking Federated Environments (AD FS, Golden SAML)</li>

<li><strong>17.10.</strong> Tools

<ul>

<li><strong>17.10.1.</strong> AADInternals</li>

<li><strong>17.10.2.</strong> ROADtools</li>

<li><strong>17.10.3.</strong> GraphRunner</li>

<li><strong>17.10.4.</strong> AzureHound</li>

</ul>

</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 18: Defending Hybrid Environments

&#x20; </summary>



&#x20; <ul>

<li><strong>18.1.</strong> Securing Azure AD Connect and Sync Accounts</li>

<li><strong>18.2.</strong> Conditional Access Policy Design and Hardening</li>

<li><strong>18.3.</strong> Monitoring Entra ID Sign-In and Audit Logs</li>

<li><strong>18.4.</strong> Protecting Service Principals and App Registrations</li>

<li><strong>18.5.</strong> Entra ID Identity Protection and Risk Signals</li>

<li><strong>18.6.</strong> Workload Identity Federation Security</li>

<li><strong>18.7.</strong> Cross-Environment Detection Strategies</li>

</ul></details>



\---

\### PART VII: DEFENSE, DETECTION, AND HARDENING



<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 19: Active Directory Hardening

&#x20; </summary>



&#x20; <ul>

<li><strong>19.1.</strong> Tiered Administration Model (Enterprise Access Model)

<ul>

<li><strong>19.1.1.</strong> Tier 0: Identity Plane Protection</li>

<li><strong>19.1.2.</strong> Tier 1: Server and Application Protection</li>

<li><strong>19.1.3.</strong> Tier 2: Workstation and User Protection</li>

</ul>

</li>

<li><strong>19.2.</strong> Privileged Access Workstations (PAWs)</li>

<li><strong>19.3.</strong> Privileged Access Management (PAM) and Just-in-Time (JIT) Access</li>

<li><strong>19.4.</strong> Hardening Domain Controllers (DCs)

<ul>

<li><strong>19.4.1.</strong> OS (Operating System) Hardening and Attack Surface Reduction</li>

<li><strong>19.4.2.</strong> Firewall and Network Segmentation for DCs</li>

<li><strong>19.4.3.</strong> Virtualization Security for DC VMs</li>

</ul>

</li>

<li><strong>19.5.</strong><code> KRBTGT</code> Account Rotation Strategy</li>

<li><strong>19.6.</strong> Securing Active Directory Certificate Services (AD CS)

<ul>

<li><strong>19.6.1.</strong> Auditing and Hardening Certificate Templates</li>

<li><strong>19.6.2.</strong> Certificate Authority (CA) Tiering and Network Isolation</li>

<li><strong>19.6.3.</strong> Certificate Lifecycle Management</li>

</ul>

</li>

<li><strong>19.7.</strong> Hardening Authentication

<ul>

<li><strong>19.7.1.</strong> Disabling NTLM (NewTechnology LAN Manager) or Enforcing Restrictions</li>

<li><strong>19.7.2.</strong> Enforcing Kerberos Armoring (FAST)</li>

<li><strong>19.7.3.</strong> Enforcing Advanced Encryption Standard (AES)-Only Kerberos Encryption</li>

<li><strong>19.7.4.</strong>\\\&nbsp;Lightweight Directory Access Protocol (LDAP) Signing and Channel Binding Enforcement</li>

<li><strong>19.7.5.</strong>\\\&nbsp;Server Message Block (SMB) Signing Enforcement</li>

</ul>

</li>

<li><strong>19.8.</strong> Group Policy Object (GPO) Hardening</li>

<li><strong>19.9.</strong>\\\&nbsp;Access Control List (ACL) Hygiene and Least-Privilege Enforcement</li>

<li><strong>19.10.</strong> Securing Service Accounts</li>

<li><strong>19.11.</strong> LAPS (Local Administrator Password Solution) Deployment (Windows LAPS and Legacy LAPS)</li>

<li><strong>19.12.</strong> Disabling Legacy Protocols

<ul>

<li><strong>19.12.1.</strong> LLMNR -\\\&nbsp;Link-Local Multicast Name Resolution</li>

<li><strong>19.12.2.</strong> NBNS - NetBIOS Name Service</li>

<li><strong>19.12.3.</strong> WPAD - Web-Proxy Auto-Discovery</li>

<li><strong>19.12.4.</strong> NetBIOS - Network Basic Input/Output System</li>

</ul>

</li>

<li><strong>19.13.</strong> AdminSDHolder Lockdown</li>

<li><strong>19.14.</strong> DNS Security

<ul>

<li><strong>19.14.1.</strong> DNSSEC - Domain Name Service Security</li>

<li><strong>19.14.2.</strong> DNS Filtering</li>

<li><strong>19.14.3.</strong> DNS Logging</li>

</ul>

</li>

<li><strong>19.15.</strong> Patch Management Strategy for AD Infrastructure</li>

<li><strong>19.16.</strong> Secure Backup and Recovery of Active Directory</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 20: Monitoring and Detection

&#x20; </summary>



&#x20; <ul>

<li><strong>20.1.</strong> Critical Event IDs for Active Directory Security</li>

<li><strong>20.2.</strong> Configuring Advanced Audit Policies</li>

<li><strong>20.3.</strong> Windows Event Forwarding (WEF) at Scale</li>

<li><strong>20.4.</strong> Sysmon Configuration for AD Threat Detection</li>

<li><strong>20.5.</strong> Detecting Credential Theft</li>

<li><strong>20.6.</strong> Detecting Lateral Movement

<ul>

<li><strong>20.6.1.</strong> Anomalous Logon Patterns</li>

<li><strong>20.6.2.</strong> Pass-the-Hash (PtH) and Pass-the-Ticket (PtT) Indicators of Compromise (IOCs)</li>

<li><strong>20.6.3.</strong> Remote Execution Tool Artifacts</li>

</ul>

</li>

<li><strong>20.7.</strong> Detecting Persistence

<ul>

<li><strong>20.7.1.</strong> Golden Ticket and Silver Ticket Anomalies</li>

<li><strong>20.7.2.</strong> Certificate Abuse Detection</li>

<li><strong>20.7.3.</strong> Unexpected AD Object Modifications</li>

</ul>

</li>

<li><strong>20.8.</strong> Detecting Enumeration

<ul>

<li><strong>20.8.1.</strong> LDAP Query Anomalies</li>

<li><strong>20.8.2.</strong> BloodHound Collection Detection</li>

</ul>

</li>

<li><strong>20.9.</strong> Honeypots, Honeytokens, Honey-Canaries, and Deception in Active Directory Security

<ul>

<li><strong>20.9.1.</strong> Honey Users, Computers, and SPNs</li>

<li><strong>20.9.2.</strong> Deploying Decoy Credentials</li>

<li><strong>20.9.3.</strong> Canary Files and Shares</li>

</ul>

</li>

<li><strong>20.10.</strong> System Information and Event Management (SIEM) Integration and Correlation Rules</li>

<li><strong>20.11.</strong> Leveraging Microsoft Defender for Identity (MDI)</li>

<li><strong>20.12.</strong> Leveraging Microsoft Sentinel for AD Detection Capabilities</li>

<li><strong>20.13.</strong> Endpoint Detection Response (EDR) / Extended Detection and Response (XDR) Integration for AD-Centric Threats</li>

<li><strong>20.14.</strong> Network Detection and Response (NDR) for AD Protocols</li>

<li><strong>20.15.</strong> User and Entity Behavior Analysis (UEBA)</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 21: Incident Response for Active Directory Compromises

&#x20; </summary>



&#x20; <ul>

<li><strong>21.1.</strong> AD-Specific Incident Response Framework</li>

<li><strong>21.2.</strong> Indicators of Compromise (IOCs) for AD Attacks</li>

<li><strong>21.3.</strong> Triage and Scoping an AD Breach</li>

<li><strong>21.4.</strong> Forensic Analysis of Domain Controllers</li>

&#x20; <li><strong>21.5.</strong> Analyzing <code>NTDS.dit</code> and Registry Hives Post-Breach</li>

<li><strong>21.6.</strong> Identifying and Revoking Compromised Credentials</li>

<li><strong>21.7.</strong> <code>KRBTGT</code> Reset Procedures (Double Reset Strategy)</li>

<li><strong>21.8.</strong> Revoking and Re-Issuing Certificates Post-Compromise</li>

<li><strong>21.9.</strong> Trust Recovery After Cross-Forest Compromise</li>

<li><strong>21.10.</strong> Recovering from Ransomware Targeting AD</li>

<li><strong>21.11.</strong> Full Forest Recovery Procedures</li>

<li><strong>21.12.</strong> Post-Incident Hardening and Lessons Learned + Areas for Improvement</li>

<li><strong>21.13.</strong> Legal and Regulatory Notification Requirements</li>

</ul></details>



\---

\### PART VIII: OFFENIVE OPERATIONS AND RED TEAM TRADECRAFT

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 22: Red Team Methodology for Active Directory

&#x20; </summary>



&#x20; <ul>

<li><strong>22.1.</strong> Engagement Scoping and Rules of Engagement</li>

<li><strong>22.2.</strong> AD Attack Kill Chain Mapping (MITRE ATT\\\&amp;CK)</li>

<li><strong>22.3.</strong> Operational Security (OPSEC) Considerations</li>

<li><strong>22.4.</strong> Choosing and Customizing C2 Frameworks</li>

<li><strong>22.5.</strong> Evasion Techniques

<ul>

<li><strong>22.5.1.</strong> AMSI Bypass Techniques</li>

<li><strong>22.5.2.</strong> ETW Patching and Evasion</li>

<li><strong>22.5.3.</strong> Credential Guard and PPL Bypass</li>

<li><strong>22.5.4.</strong> EDR Evasion and Unhooking</li>

<li><strong>22.5.5.</strong> Payload Obfuscation and Encryption</li>

<li><strong>22.5.6.</strong> Living-off-the-Land and Reflective Loading</li>

</ul>

</li>

<li><strong>22.6.</strong> Linux-Based AD Attacks

<ul>

<li><strong>22.6.1.</strong> Impacket</li>

<li><strong>22.6.2.</strong> NetExec</li>

<li><strong>22.6.3.</strong> Certipy</li>

&#x20; <li><strong>22.6.4.</strong> <code>krbrelayx</code></li>

</ul>

</li>

<li><strong>22.7.</strong> Automation and Tooling Pipelines</li>

<li><strong>22.8.</strong> Reporting and Communication for Stakeholders</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 23: Purple Team Exercises for Active Directory

&#x20; </summary>



&#x20; <ul>

<li><strong>23.1.</strong> Purple Team Philosophy and Methodology</li>

<li><strong>23.2.</strong> Designing AD-Specific Purple Team Scenarios</li>

<li><strong>23.3.</strong> MITRE ATT\\\&amp;CK Mapping and Coverage Analysis</li>

<li><strong>23.4.</strong> Atomic Red Team and Adversary Emulation Plans</li>

<li><strong>23.5.</strong> Measuring Detection Efficacy and Gaps</li>

<li><strong>23.6.</strong> Tuning Detections Based on Exercise Results</li>

<li><strong>23.7.</strong> Continuous Validation Platforms (BAS for AD)</li>

<li><strong>23.8.</strong> Building a Purple Team Program Around AD</li>

</ul></details>



\---

\### PART IX: ADVANCED AND EMERGING TOPICS

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 24: Active Directory and Zero Trust Architecture

&#x20; </summary>



&#x20; <ul>

<li><strong>24.1.</strong> Zero Trust Principles Applied to Active Directory</li>

<li><strong>24.2.</strong> Identity as the New Perimeter</li>

<li><strong>24.3.</strong> Microsegmentation for AD Infrastructure</li>

<li><strong>24.4.</strong> Continuous Verification and Adaptive Access</li>

<li><strong>24.5.</strong> Reducing Reliance on Domain Trust Boundaries</li>

<li><strong>24.6.</strong> Integration with Modern Identity Providers</li>

<li><strong>24.7. Transitioning from Legacy AD to Zero Trust:</strong> Practical Roadmap</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 25: AI and Machine Learning in AD Security

&#x20; </summary>



&#x20; <ul>

<li><strong>25.1.</strong> AI-Powered Attack Path Analysis</li>

<li><strong>25.2.</strong> Machine Learning for Anomaly Detection in AD</li>

<li><strong>25.3.</strong> LLM-Assisted Offensive Tooling and Prompt-Based Attacks</li>

<li><strong>25.4.</strong> AD-Driven Phishing and Social Engineering Against AD Users</li>

<li><strong>25.5. Defensive AI:</strong> Automated Response and Threat Hunting</li>

<li><strong>25.6.</strong> Adversarial Machine Learning Evading AI-Based Defenses</li>

<li><strong>25.7.</strong> Ethical Considerations and Limitations</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Chapter 26: Emerging Threats and Future Attack Vectors

&#x20; </summary>



&#x20; <ul>

<li><strong>26.1.</strong> Post-Quantum Cryptography Implications for Kerberos and NTLM</li>

<li><strong>26.2. New Windows and AD Features:</strong> Security Implications</li>

<li><strong>26.3. Identity Fabric Attacks:</strong> Bridging On-Prem and Multi-Cloud</li>

<li><strong>26.4.</strong> Supply Chain Attacks Targeting A Infrastructure</li>

<li><strong>26.5.</strong> Attacking AD-Integrated DevOps Pipelines</li>

<li><strong>26.6. IoT and OT Device Integration with AD:</strong> New Attack Surface</li>

<li><strong>26.7.</strong> Passwordless Authentication Attack Vectors</li>

<li><strong>26.8. The Future of Active Directory:</strong> Deprecation, Migration, or Evolution?</li>

</ul></details>



\---

\### PART X: APPENDICES

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix A: Tool Reference Guide

&#x20; </summary>



&#x20; <ul>

<li><strong>A.1.</strong> Enumeration Tools

<ul>

<li><strong>A.1.1.</strong> BloodHound</li>

<li><strong>A.1.2.</strong> PowerView</li>

<li><strong>A.1.3.</strong> ADRecon</li>

<li><strong>A.1.4.</strong> ldapdomaindump</li>

</ul>

</li>

<li><strong>A.2.</strong> Attack Tools

<ul>

<li><strong>A.2.1.</strong> Mimikatz</li>

<li><strong>A.2.2.</strong> Impacket Suite</li>

<li><strong>A.2.3.</strong> Rubeus</li>

<li><strong>A.2.4.</strong> Certipy \\\&amp; Certify</li>

<li><strong>A.2.5.</strong> NetExec</li>

<li><strong>A.2.6.</strong> CrackMapExec (CME)</li>

</ul>

</li>

<li><strong>A.3.</strong> Defense and Assessment Tools

<ul>

<li><strong>A.3.1.</strong> PingCastle</li>

<li><strong>A.3.2.</strong> Purple Knight</li>

<li><strong>A.3.3.</strong> Semperis DSP</li>

</ul>

</li>

<li><strong>A.4.</strong> C2 Frameworks Comparison Table</li>

<li><strong>A.5.</strong> Lab Automation Tools and Scripts</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix B: Critical Event Log IDs Quick Reference

&#x20; </summary>



&#x20; <ul>

<li><strong>B.1.</strong> Authentication Events</li>

<li><strong>B.2.</strong> Privilege Escalation Events</li>

<li><strong>B.3.</strong> Object Modification Events</li>

<li><strong>B.4.</strong> Replication and DC Events</li>

<li><strong>B.5.</strong> Certificate Services Events</li>

<li><strong>B.6.</strong> Anomalous Activity Events</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix C: MITRE ATT\&CK Mapping for Active Directory

&#x20; </summary>



&#x20; <li>**C.1.** Technique-to-Chapter Cross-Reference</li>

&#x20; <li>**C.2.** Detection Coverage Matrix</li>

&#x20; <li>**C.3.** Recommended Data Sources per Technique</li></ul>

</details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix D: Active Directory Security Checklist

&#x20; </summary>



&#x20; <ul>

<li><strong>D.1.</strong> Pre-Deployment Security Checklist</li>

<li><strong>D.2.</strong> Ongoing Operations Security Checklist</li>

<li><strong>D.3.</strong> Incident Readiness Checklist</li>

<li><strong>D.4.</strong> Hybrid Environment Security Checklist</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix E: PowerShell and Python Scripts Library

&#x20; </summary>



&#x20; <ul>

<li><strong>E.1.</strong> Enumeration Scripts</li>

<li><strong>E.2.</strong> Hardening Automation Scripts</li>

<li><strong>E.3.</strong> Detection and Monitoring Scripts</li>

<li><strong>E.4.</strong> Incident Response (IR) Scripts</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix F: Glossary of Terms

&#x20; </summary>



&#x20; <ul>

<li><strong>F.1.</strong> Glossary of Terms</li>

</ul></details>

<details class="hw-acc">

&#x20; <summary>

&#x20;   <span class="acc-icon">▸</span>

&#x20;   Appendix G: References and Further Reading Recommendations

&#x20; </summary>



&#x20; <ul>

<li><strong>G.1.</strong> Whitepapers and Research</li>

<li><strong>G.2.</strong> CVEs and Microsoft Security Advisories</li>

<li><strong>G.3.</strong> Community Resources, Blogs, and Conferences</li>

<li><strong>G.4.</strong> Training and Certification Paths</li>

</ul></details>

===============================================================================================================



# **Master of Your Domain: Hacking and Defending Active Directory in 7 Days for Ethical Hackers**

## **Complete Table of Contents**

## **Foreword: The Ethical Hacker's Responsibility**

## **Preface: How to Use This Book**

* Prerequisites and Required Knowledge
* Lab Environment Setup Requirements
* Learning Path Recommendations
* Companion Resources and Tools

## **Part I: Foundations (Day 1)**

### **Chapter 1: Understanding the Active Directory Ecosystem**

#### **1.1 What is Active Directory and Why It Matters**

* 1.1.1 The Business Case for Active Directory
* 1.1.2 AD in Modern Enterprise Infrastructure
* 1.1.3 Cloud Integration: Azure AD and Hybrid Environments

#### **1.2 Core Components and Architecture**

* 1.2.1 Domain Controllers and Their Role
* 1.2.2 Forests, Trees, and Domains Explained
* 1.2.3 Organizational Units (OUs) Structure
* 1.2.4 Sites and Replication Topology
* 1.2.5 Global Catalog and FSMO Roles

#### **1.3 Active Directory Objects and Schema**

* 1.3.1 Users, Computers, and Groups
* 1.3.2 Service Accounts and Managed Service Accounts
* 1.3.3 Group Policy Objects (GPOs)
* 1.3.4 Schema Extensions and Custom Attributes

### **Chapter 2: Essential Information Security Concepts for AD**

#### **2.1 The CIA Triad in Active Directory Context**

* 2.1.1 Confidentiality: Protecting Sensitive Directory Data
* 2.1.2 Integrity: Ensuring Trust in Authentication
* 2.1.3 Availability: Maintaining Directory Services

#### **2.2 Authentication vs. Authorization**

* 2.2.1 Kerberos Protocol Deep Dive
* 2.2.2 NTLM: Legacy but Persistent
* 2.2.3 LDAP Authentication Mechanisms
* 2.2.4 Modern Authentication: SAML, OAuth, and AD FS

#### **2.3 Defense in Depth Strategy**

* 2.3.1 Network Segmentation for AD Protection
* 2.3.2 Principle of Least Privilege
* 2.3.3 Zero Trust and Active Directory
* 2.3.4 Monitoring and Detection Layers

### **Chapter 3: Network Security Fundamentals for AD Environments**

#### **3.1 Critical Network Protocols in AD**

* 3.1.1 DNS and Its Crucial Role in AD
* 3.1.2 LDAP and LDAPS Communication
* 3.1.3 SMB/CIFS for File Sharing
* 3.1.4 RPC and Dynamic Port Allocation
* 3.1.5 Kerberos Network Traffic Analysis

#### **3.2 Network Security Controls**

* 3.2.1 Firewall Rules for Domain Controllers
* 3.2.2 Network Access Control (NAC) Integration
* 3.2.3 VLANs and AD Traffic Isolation
* 3.2.4 IPSec for Domain Controller Communication

#### **3.3 Common Network Attack Vectors**

* 3.3.1 Man-in-the-Middle Attacks on AD Traffic
* 3.3.2 DNS Poisoning and Hijacking
* 3.3.3 Broadcast Protocol Exploitation
* 3.3.4 IPv6 Attack Vectors in AD

## **Part II: Reconnaissance and Enumeration (Day 2)**

### **Chapter 4: Passive and Active Information Gathering**

#### **4.1 OSINT for Active Directory**

* 4.1.1 LinkedIn and Organizational Mapping
* 4.1.2 Email Harvesting and Username Formats
* 4.1.3 DNS Reconnaissance Techniques
* 4.1.4 Certificate Transparency Logs

#### **4.2 Network Scanning and Discovery**

* 4.2.1 Using Nmap for AD Infrastructure Mapping
* 4.2.2 Identifying Domain Controllers
* 4.2.3 Service Discovery and Fingerprinting
* 4.2.4 Avoiding Detection During Scanning

#### **4.3 Initial Access Techniques**

* 4.3.1 Password Spraying Strategies
* 4.3.2 Username Enumeration Methods
* 4.3.3 Null Session Enumeration
* 4.3.4 LDAP Anonymous Binds

### **Chapter 5: Advanced AD Enumeration**

#### **5.1 Authenticated Enumeration Tools**

* 5.1.1 BloodHound: Mapping Attack Paths
* 5.1.2 PowerView and PowerShell Empire
* 5.1.3 ADExplorer and Native Tools
* 5.1.4 SharpHound Collection Methods

#### **5.2 Enumerating Critical Information**

* 5.2.1 User and Computer Object Properties
* 5.2.2 Group Memberships and Nested Groups
* 5.2.3 Trust Relationships Mapping
* 5.2.4 GPO Settings and Misconfigurations
* 5.2.5 Service Principal Names (SPNs)

#### **5.3 Defensive Enumeration Detection**

* 5.3.1 Honeypot Accounts and Honeytoken
* 5.3.2 Monitoring LDAP Queries
* 5.3.3 Detecting BloodHound Activity
* 5.3.4 Advanced Audit Policies

## **Part III: Initial Compromise and Lateral Movement (Day 3-4)**

### **Chapter 6: Common Attack Vectors and Initial Compromise**

#### **6.1 Credential-Based Attacks**

* 6.1.1 Password Spraying Implementation
* 6.1.2 Credential Stuffing Techniques
* 6.1.3 Kerberoasting: From SPN to Credentials
* 6.1.4 AS-REP Roasting Vulnerable Accounts

#### **6.2 Relay Attacks**

* 6.2.1 LLMNR/NBT-NS Poisoning
* 6.2.2 SMB Relay Attack Chains
* 6.2.3 LDAP Relay and Resource-Based Constrained Delegation
* 6.2.4 WebDAV and HTTP to LDAP Relay

#### **6.3 Exploiting Misconfigurations**

* 6.3.1 Weak GPO Permissions
* 6.3.2 Unconstrained Delegation Abuse
* 6.3.3 Print Spooler Service Exploitation
* 6.3.4 SYSVOL and GPP Password Exposure

### **Chapter 7: Lateral Movement Techniques**

#### **7.1 Traditional Lateral Movement**

* 7.1.1 Pass-the-Hash (PtH) Attacks
* 7.1.2 Pass-the-Ticket (PtT) Techniques
* 7.1.3 Overpass-the-Hash/Pass-the-Key
* 7.1.4 Token Impersonation Methods

#### **7.2 Living Off the Land**

* 7.2.1 WMI for Remote Execution
* 7.2.2 PowerShell Remoting Techniques
* 7.2.3 Scheduled Tasks and At Jobs
* 7.2.4 Service Creation and Modification

#### **7.3 Advanced Persistence Mechanisms**

* 7.3.1 Golden Ticket Creation and Usage
* 7.3.2 Silver Ticket Attacks
* 7.3.3 Skeleton Key Implants
* 7.3.4 AdminSDHolder Modification
* 7.3.5 SID History Injection

### **Chapter 8: Defensive Strategies Against Lateral Movement**

#### **8.1 Credential Protection**

* 8.1.1 Credential Guard Implementation
* 8.1.2 Protected Users Security Group
* 8.1.3 LAPS Deployment and Management
* 8.1.4 Kerberos Armoring (FAST)

#### **8.2 Network Segmentation Strategies**

* 8.2.1 Tiered Administrative Model
* 8.2.2 Privileged Access Workstations (PAWs)
* 8.2.3 Authentication Silos and Policies
* 8.2.4 Selective Authentication in Trusts

#### **8.3 Detection and Response**

* 8.3.1 Honey Credentials and Deception
* 8.3.2 Advanced Threat Analytics (ATA)
* 8.3.3 Windows Event Log Analysis
* 8.3.4 Network Traffic Analysis for Anomalies

## **Part IV: Privilege Escalation and Persistence (Day 5)**

### **Chapter 9: Privilege Escalation in Active Directory**

#### **9.1 Local Privilege Escalation**

* 9.1.1 Unquoted Service Paths
* 9.1.2 DLL Hijacking Opportunities
* 9.1.3 Registry Autoruns Abuse
* 9.1.4 Scheduled Task Manipulation

#### **9.2 Domain Privilege Escalation**

* 9.2.1 ACL Abuse and Privilege Chains
* 9.2.2 DNSAdmins Group Exploitation
* 9.2.3 Exchange Privilege Escalation
* 9.2.4 Certificate Template Misconfigurations

#### **9.3 Forest and Trust Escalation**

* 9.3.1 Foreign Security Principal Abuse
* 9.3.2 Trust Ticket Attacks
* 9.3.3 PAM Trust Exploitation
* 9.3.4 Azure AD Connect Abuse

### **Chapter 10: Advanced Persistence Techniques**

#### **10.1 Backdoor Accounts and Groups**

* 10.1.1 Hidden Administrative Accounts
* 10.1.2 Shadow Security Principals
* 10.1.3 Nested Group Backdoors
* 10.1.4 Computer Account Takeover

#### **10.2 System-Level Persistence**

* 10.2.1 DCShadow Attacks
* 10.2.2 Custom SSP Installation
* 10.2.3 Malicious Domain Controller
* 10.2.4 Forest Trust Abuse

#### **10.3 Application-Level Persistence**

* 10.3.1 Outlook Rules and Forms
* 10.3.2 Office 365 Application Consent
* 10.3.3 Federation Trust Manipulation
* 10.3.4 ADFS Backdoors

## **Part V: Defense, Detection, and Response (Day 6)**

### **Chapter 11: Hardening Active Directory**

#### **11.1 Baseline Security Configuration**

* 11.1.1 Security Baselines and Benchmarks
* 11.1.2 Group Policy Hardening
* 11.1.3 Administrative Template Settings
* 11.1.4 Security Options Configuration

#### **11.2 Advanced Hardening Techniques**

* 11.2.1 RID Randomization
* 11.2.2 SID Filtering Configuration
* 11.2.3 Selective Authentication
* 11.2.4 Authentication Policy Silos

#### **11.3 Patch Management and Updates**

* 11.3.1 Critical AD Security Updates
* 11.3.2 WSUS Integration
* 11.3.3 Emergency Patching Procedures
* 11.3.4 Testing and Rollback Strategies

### **Chapter 12: Monitoring and Threat Detection**

#### **12.1 Log Collection and Analysis**

* 12.1.1 Essential Windows Event IDs
* 12.1.2 Sysmon for Enhanced Visibility
* 12.1.3 PowerShell Logging Configuration
* 12.1.4 Centralized Log Management

#### **12.2 SIEM Integration and Correlation**

* 12.2.1 Detection Use Cases for AD
* 12.2.2 Correlation Rules Development
* 12.2.3 Threat Intelligence Integration
* 12.2.4 Automated Response Playbooks

#### **12.3 Threat Hunting in AD**

* 12.3.1 Hunting for Golden Tickets
* 12.3.2 Detecting Kerberoasting Activity
* 12.3.3 Anomalous Authentication Patterns
* 12.3.4 Behavioral Analytics Implementation

### **Chapter 13: Incident Response and Recovery**

#### **13.1 Incident Response Planning**

* 13.1.1 AD-Specific IR Procedures
* 13.1.2 Evidence Collection Methods
* 13.1.3 Containment Strategies
* 13.1.4 Communication Protocols

#### **13.2 Compromise Recovery**

* 13.2.1 Determining Compromise Scope
* 13.2.2 Evicting Advanced Attackers
* 13.2.3 Credential Reset Procedures
* 13.2.4 Trust Relationship Recovery

#### **13.3 Forest Recovery Operations**

* 13.3.1 Forest Recovery Planning
* 13.3.2 Backup and Restore Strategies
* 13.3.3 Authoritative Restore Procedures
* 13.3.4 Post-Recovery Validation

## **Part VI: Advanced Topics and Real-World Scenarios (Day 7)**

### **Chapter 14: Cloud and Hybrid Environments**

#### **14.1 Azure AD Integration Security**

* 14.1.1 Azure AD Connect Security
* 14.1.2 Pass-through Authentication Risks
* 14.1.3 Password Hash Sync Considerations
* 14.1.4 Federation Security Best Practices

#### **14.2 Cloud-Specific Attack Vectors**

* 14.2.1 Token Theft and Replay
* 14.2.2 Consent Phishing Attacks
* 14.2.3 Cloud Privilege Escalation
* 14.2.4 Multi-Factor Authentication Bypass

#### **14.3 Securing Hybrid Deployments**

* 14.3.1 Conditional Access Policies
* 14.3.2 Identity Protection Features
* 14.3.3 Privileged Identity Management
* 14.3.4 Cloud App Security Integration

### **Chapter 15: Real-World Attack Simulations**

#### **15.1 Purple Team Exercises**

* 15.1.1 Exercise Planning and Scoping
* 15.1.2 Attack Scenario Development
* 15.1.3 Detection Capability Testing
* 15.1.4 Metrics and Improvement Tracking

#### **15.2 Complete Attack Chain Walkthroughs**

* 15.2.1 APT-Style Long-Term Compromise
* 15.2.2 Ransomware Attack Simulation
* 15.2.3 Insider Threat Scenarios
* 15.2.4 Supply Chain Compromise

#### **15.3 Defensive Scenario Exercises**

* 15.3.1 Incident Detection Challenge
* 15.3.2 Forensics and Attribution
* 15.3.3 Recovery Time Objectives
* 15.3.4 Lessons Learned Documentation

### **Chapter 16: Compliance and Best Practices**

#### **16.1 Regulatory Requirements**

* 16.1.1 GDPR and Data Protection
* 16.1.2 HIPAA Compliance for Healthcare
* 16.1.3 PCI-DSS for Payment Systems
* 16.1.4 SOX Compliance Requirements

#### **16.2 Security Frameworks**

* 16.2.1 NIST Cybersecurity Framework
* 16.2.2 CIS Controls for AD
* 16.2.3 MITRE ATT\&CK Mapping
* 16.2.4 Zero Trust Architecture

#### **16.3 Continuous Improvement**

* 16.3.1 Security Metrics and KPIs
* 16.3.2 Vulnerability Management Programs
* 16.3.3 Security Awareness Training
* 16.3.4 Third-Party Security Assessments

## **Appendices**

### **Appendix A: Lab Environment Setup**

* A.1 Virtual Machine Requirements
* A.2 Building a Test Domain
* A.3 Vulnerable Configuration Setup
* A.4 Tool Installation Guide

### **Appendix B: Essential Tools Reference**

* B.1 Offensive Security Tools
* B.2 Defensive and Monitoring Tools
* B.3 PowerShell Scripts and Modules
* B.4 Open Source vs. Commercial Tools

### **Appendix C: Quick Reference Guides**

* C.1 Common Port Numbers
* C.2 Critical Event IDs
* C.3 PowerShell Commands Cheat Sheet
* C.4 Mimikatz Command Reference

### **Appendix D: Security Checklist Templates**

* D.1 Domain Controller Security Checklist
* D.2 Post-Compromise Checklist
* D.3 Audit and Compliance Checklist
* D.4 Incident Response Checklist

### **Appendix E: Additional Resources**

* E.1 Recommended Reading
* E.2 Online Training Platforms
* E.3 Community Forums and Support
* E.4 Security Research Papers

## **Glossary of Terms**

## **Index**

## **About the Author**

===============================================================================================================



This table of contents (outline) balances offensive techniques, defensive strategies, and modern-day threats while ensuring practical relevance for red teamers, blue teamers, security professionals, and everyone else in-between.

TABLE OF CONTENTS

Foreword

The Evolving Threat Landscape of Active Directory (2020-2026)

Who This Book Is For (Red Team, Blue Team, Architects, CISOs)

# How To Use This Book (Hands-On Labs, Real-World Scenarios)

PART I: FOUNDATION OF ACTIVE DIRECTORY SECURITY

Chapter A - Active Directory Architecture in the Modern Enterprise

A.1 Core Components of Active Directory
A.1.1 Domains
A.1.2 Forests
A.1.3 Trusts
A.1.4 Sites

A.2. Modern AD: Hybrid Cloud
A.2.1 Hybrid Cloud
A.2.1.1 Azure AD
A.2.1.2 Entra ID
A.2.1.3 NTLM Deprecation

A.3. AD Protocols and Authentication
A.3.1 Kerberos
A.3.2 NTLM
A.3.3 LDAP

Chapter B - Authentication Protocol Attacks and Abuse

B.1. Kerberos Attacks
B.1.1 Golden and Silver Tickets
B.1.2 S4U2Self/Proxy
B.1.3 PAC Validation

B.2. NTLM Attacks
B.2.1 Relay Attacks
B.2.2 NetNTLMv2
B.2.3 Session Signing

B.3. LDAP Attacks
B.3.1 LDAP Injection
B.3.2 Channel Binding
B.3.3 Signing Requirements

PART II - ATTACKING ACTIVE DIRECTORY (RED TEAM PERSPECTIVE)

Chapter C - Reconnaissance and Enumeration
C.1 Reconnaissance Fundamentals

C.2 Passive vs. Active Recon
C.2.1 BloodHound
C.2.2 SharpHound
C.2.3 ADExplorer

C.3 LDAP Queries and PowerShell Enumeration

C.4 Hybrid Cloud Reconnaissance
C.4.1 Azure AD Connect
C.4.2 Entra ID Sync

Chapter D - Initial Access and Exploitation
D.1 Phishing and Social Engineering
D.1.1 OAuth Abuse
D.1.2 Device Code Flow

D.2 Exploiting Misconfigurations
D.2.1 Unconstrained Delegation
D.2.2 ACL Abuse

PART III - Defending Active Directory (Blue Team Perspective)

Chapter E - Monitoring, Detection, and Response
E.1 Logging and Telemetry

E.2 SIEM Architecture
E.2.1 Splunk
E.2.2 Microsoft Sentinel
E.2.3 Elastic

E.3 Behavioral Analysis

E.4 Incident Response for AD Compromise

PART IV - FUTURE-PROOFING ACTIVE DIRECTORY

Chapter F - Emerging Threats and Defensive Evolution
F.1 AI and Machine Learning in Active Directory

F.2 Quantum Threats and Post-Quantum Cryptography

F.3 Automating AD Defense
F.3.1 PowerShell
F.3.2 Python

1. Attacks on OAuth and Modern Authentication Models
8.1 Pass-the-PRT
8.2 Device Code Phishing
2. AD Data Stores and Critical Objects
9.1 NTDS.dit and the Active Directory Database
9.2 Group Policy Objects (GPOs) and SYSVOL
9.3 Security Principals
9.3.1 Users \& Groups
9.3.2 Computers \& Service Accounts
3. PAWs/SAWs, and Tiered Administration
====================

PART X: ATTACKING ACTIVE DIRECTORY (RED TEAM PERSPECTIVE)

1. Reconnaissance and Enumeration
2. Passive vs. Active Recon
2.1 BloodHound
2.2 SharpHound
2.3 ADExplorer
3. LDAP Queries and PowerShell Enumeration
4. Cloud Hybrid Recon
4.1 Azure AD Connect
4.2 Entra ID Sync
5. Initial Access Techniques
5.1 Phishing
5.1.1 Modern OAuth Attacks
5.1.2 Device Code Flow
6. Exploiting Misconfigurations
6.1 Unconstrained Delegation
6.2 ACL Abuse
7. Password Spraying and Credential Stuffing
7.1 Defenses Against MFA Bypass
8. Supply Chain Attacks
8.1 Third-Party Integrations
8.2 AD CS Abuse
9. Lateral Movement and Privilege Escalation
9.1 Pass-the-Hash (PtH)
9.2 Overpass-the-Hash / Pass-the-Ticket (PtT)
10. Kerberos Attacks
10.1 AS-REP Roasting
10.2 Kerberoasting
10.3 Unconstrained Delegation
11. Abusing Group Policy
11.1 GPO Abuse
11.2 Startup \& Logon Scripts
12. Privilege Escalation via Service Accounts and Managed Service Accounts (gMSAs)
13. Persistence Mechanisms
14. Golden Ticket Attacks
14.1 Forging Kerberos TGTs
15. Silver Ticket Attacks
15.1 Service Tickets
16. Skeleton Key and Custom SSPs
17. DSRM Abuse and Directory Services Restore Mode
18. Backdooring AD
18.1 Malicious GPOs
18.2 Scheduled Tasks
18.3 WMI Event Subscriptions
19. Defense Evasion and Bypasses
20. Living-Off-The-Land Binaries (LOLBins) in AD Attacks
21. AMSI and EDR Bypass Techniques
21.1 PowerShell Constrained Language Model
22. Disabling Logging and Tampering with Event Logs
23. Abusing Trusts
23.1 Forest Trust Abuse
23.2 External Trust Abuse
23.3 SID Filtering Bypass
24. Exfiltration and Impact
24.1 Data Exfiltration via AD
24.1.1 LDAP, DNS, SMB
25. Ransomware and AD
25.1 Group Policy Ransomware
25.2 DC Encryption
26. Destructive Attacks
26.1 DC Wiping
26.2 AD Database Corruption
====================

PART X: DEFENDING ACTIVE DIRECTORY (BLUE TEAM PERSPECTIVE)

1. Hardening Active Directory
2. Secure AD Design
2.1 Tiered Administration
2.2 PAWs \& SAWs
2.3 Just-Enough-Administration (JEA)
3. Disabling Legacy Protocols
3.1 NTLM
3.2 LM Hashes
3.3 Weak Ciphers
4. Enforcing LDAP Signing and Channel Binding
5. Securing Service Accounts
5.1 gMSAs, Group Managed Service Accounts
6. Monitoring and Detection Strategies
6.1 Windows Event Logs
6.1.1 Key Event Identifiers for AD-Specific Attacks
7. SIEM Rules for AD Attacks
7.1 Splunk
7.2 Microsoft Sentinel
7.3 ELK (Elastic, Logstash, Kibana)
8. Behavioral Analytics
8.1 Unusual Logon Patterns
8.2 Identifying Privilege Escalation Attempts and Attacks
9. Incident Response (IR) for AD Attacks
9.1 Containment Strategies
9.1.1 Isolating Domain Controllers
9.1.2 Disabling Compromised Accounts
10. Forensic Analysis
10.1 NTDS.dit Extraction
10.2 Memory Forensics
11.Recovering from AD Compromise
11.1 Authoritative Restore
11.2 DC Promotion
11. Post-Incident Review
12.1 Lessons Learned
12.2 Hardening Improvements
12. Advanced Defenses and Zero Trust Network Architecture (ZTNA)
13. Privileged Access Workstations (PAWs) and Secure Admin Workstations (SAWs)
14. Just-in-Time (JIT) and Just-Enough-Administration (JEA)
15. Microsoft Defender for Identity (MDI) and Advanced Threat Protection
16. Zero Trust for AD
17.1 Conditional Access
17.2 Identity Protection
17.3 MFA Enforcement
17. Securing Hybrid AD Environments
18.1 Azure AD Connect Security
18.1.1 Password Hash Sync
18.1.2 Pass-Through Auth
18. Securing Entra ID
19.1 Conditional Access
19.2 Identity Protection
19. Detecting and Preventing Cloud-Based AD Attacks
20.1 Pass-the-PRT
20.2 Device Code Phishing
20. Synchronization Risks
21.1 On-Prem-to-Cloud
21.2 Cloud-to-On-prem
===================

PART X: FUTURE-PROOFING ACTIVE DIRECTORY

1. Emerging Threats and Trends (2026 and Beyond)
2. AI and Machine Learning in AD Attacks and Defenses
3. Quantum Computing and Cryptographic Threats to AD
4. Post-Quantum Cryptography for AD (Preparing for the Future)
5. The Role of AD in Zero Trust Network Architectures
6. Automating AD Security
6.1 PowerShell and Python for AD Security
6.1.1 Scripting Defenses \& Attacks
7. Infrastructure as Code (IaC) for Secure AD Deployment
8. Continuous Security Validation (Red Team Automation, Purple Teaming)
9. Case Studies and Real-World Scenarios
9.1 High-Profile AD Breaches
9.1.1 Lessons Learned
9.1.2 Ransomware Attacks on AD
9.1.1.1 Conti
9.1.1.2 LockBit
9.1.1.3 Supply Chain Attacks
====================

PART X: FOUNDATIONAL CYBERSECURITY CONCEPTS

1. Introduction to Cybersecurity and Information Security
1.1 Cybersecurity Landscape
1.2 Threat Modeling
1.3 Risk Management Principles
1.4 Ethical Hacking Methodology \& Framework
2. Security Fundamentals \& Frameworks
2.1 CIA Triad
2.2 DAD Triad
2.3 NIST Cybersecurity Framework (NIST CSF)
2.4 ISO 27001/27002 Standards
2.5 MITRE ATT\&CK Framework
2.6 Cyber Kill Chain (CKC)
2.7 Compliance and Regulatory Requirements
3. Networking Fundamentals
3.1 TCP/IP Architecture
3.2 Network Protocols
3.3 Open Systems Interconnection (OSI) Reference Model
3.4 Network Communication Principles
3.5 Network Topologies
4. Windows and Active Directory Architecture
4.1 Active Directory Design
4.2 Domain Controller Roles
4.3 Authentication Mechanisms
4.4 Group Policy Fundamentals
====================

PART X: ACTIVE DIRECTORY INFRASTRUCTURE

1. Active Directory Components
2. Domain Structure
3. Organizational Units (OUs)
4. User and Computer Objects
5. Trust Relationships
6. Identity and Access Management (IAM)
6.1 Authentication Protocols
6.1.1 Kerberos Internals
6.1.2 NTLM Authentication
6.1.3 Credential Management
6.1.4 Privileged Access Control (PAC)
7. Network Security Fundamentals
7.1 Firewall Configurations
7.2 Network Segmentation
7.3 Intrusion Detection \& Prevention
7.4 Security Monitoring
7.5 Log Analysis Techniques
8. Active Directory Security Configuration
8.1 Hardening Windows Servers
8.2 Secure Group Policy Implementations
8.3 Least Privilege Principles
8.4 Monitoring \& Auditing
8.5 Secure Administrative Practices
====================

PART X: OFFENSIVE TECHNIQUES

1. Reconnaissance and Information Gathering
2. OSINT Techniques
3. Active Directory Enumeration
4. Vulnerability Scanning
5. Asset \& Network Host Discovery
6. Initial Access and Exploitation
6.1 Social Engineering
6.2 Phishing Techniques
6.3 Credential Harvesting
6.4 Initial Foothold Strategies
7. Privilege Escalation
7.1 Windows Privilege Models
7.2 Kernel Exploitation
7.3 Pass-the-Hash
7.4 Golden Ticket Attacks
7.5 DCSync and DCShadow Techniques
8. Advanced Persistent Threats (APTs) in Active Directory
8.1 APT Methodology
8.2 Lateral Movement
8.3 Living-Off-The-Land (LOTL) Techniques
8.4 Advanced Evasion Strategies
9. Web Application and Database Attacks
9.1 SQL Injection (SQLi) in Active Directory
9.2 Web Service Exploitation
9.3 LDAP Injection
9.4 NoSQL Attack Vectors
9.5 Authentication Bypass Techniques
10. Advanced Exploitation Techniques
10.1 Memory Exploitation
10.2 Kernel-level Attacks
10.3 Rootkit Development
10.4 Bypassing Security Controls
10.5 Advanced Malware Techniques
====================

PART X: DEFENSIVE STRATEGIES

CHAPTER X: Threat Detection and Monitoring

SUBPART 1:  
1.0 Security Information and Event Management (SIEM)
2.0 Anomaly Detection
3.0 Threat Hunting Techniques
4.0 Behavioral Analysis
5.0 Incident Response (IR) and Forensics
5.1 Incident Response Framework
5.2 Digital Forensics Principles
5.3 Evidence Collection
5.4 Malware Analysis \& Reverse Engineering
5.5 Forensic Toolkits

SUBPART 2. Active Directory Hardening
6.0 Secure Configuration Guidelines
6.1 Advanced Group Policy
6.2 Credential Guard
6.3 Just-Enough-Administration (JEA)
6.4 AD Secure Technical Infrastructure Guideline (STIG) Configurations \& Security Controls

SUBPART 3: Advanced Defensive Controls
7.0 Multi-Factor Authentication (MFA)
7.1 Zero Trust Architecture
7.2 Network Segmentation
7.3 Micro-segmentation Strategies
7.4 Advanced Endpoint Protection

SUBPART 4: Threat Hunting and Proactive Defense
8.0 Threat Intelligence
8.1 Continuous Monitoring
8.2 Threat Hunting Methodologies
8.3 Red \& Blue Team Exercises
8.4 Breach Access Simulation (BAS) Training

SUBPART 5. Legal and Ethical Considerations
9.0 Ethical Hacking Guidelines
9.1 Ethical Hacking Code of Conduct
9.2 Legal Implications
9.3 Responsible Disclosure
9.4 Professional Conduct
9.5 Cybersecurity Ethics
===

PART X: FOUNDATIONS OF CYBERSECURITY AND INFORMATION SECURITY

CHAPTER X. The Cybersecurity Landscape and Information Security

SUBPART 1:
1.0 Evolution of Cyber Threats and Common AD Attack Vectors
2.0 The Role of Ethical Hackers in Modern Security
3.0 Cyber Kill Chain and MITRE ATT\&CK Framework Integration
4.0 Risk Management and Threat Modeling Methodologies
5.0 Building an Ethical Hacking Lab Environment
6.0 Legal Boundaries and Responsible Disclosure

SUBPART 2: Security Frameworks, Standards, and Compliance
7.0 NIST Cybersecurity Framework (NIST CSF)
8.0 ISO/IEC 27001/27002 Implementation
9.0 CIS Controls and Benchmarks for Active Directory
10.0 MITRE ATT\&CK for Enterprise: Mapping AD Attacks
10.1 PCI DSS, HIPAA, and SOX Compliance in AD Environments
10.2 Zero Trust Architecture Principles

SUBPART 3: Networking Fundamentals for Security Professionals
11.0 TCP/IP Protocol Suite Deep Dive
11.1 Open Systems Interconnection (OSI) Reference Model and Protocol Analysis
11.2 Subnetting, VLANs, and Network Segmentation
11.3 DNS, DHCP, and Their Security Implications
11.4 Wireshark and Network Traffic Analysis
11.5 IPv6 Security Considerations
11.6 Network Device Security (Switches, Routers, Firewalls)

SUBPART 4: Windows Internals and Active Directory Architecture
12.0 Windows Security Subsystem Architecture
4.2 Active Directory Domain Services (AD DS) Components
4.3 Domain Controllers: Roles and Responsibilities
4.4 Forests, Trees, and Trust Relationships
4.5 Schema and Global Catalog Service (GCS)
4.6 Replication Technology and SYSVOL
4.7 Authentication Protocols: NTLM, Kerberos, and LDAP
===

PART X: ACTIVE DIRECTORY IDENTITY AND ACCESS MANAGEMENT (IAM)

CHAPTER X: Kerberos Authentication Protocol Deep Dive
1.1 Kerberos Protocol Flow and Message Types
1.2 Ticket Granting Tickets (TGTs) and Service Tickets (TGSs)
1.3 Delegation: Constrained, Unconstrained, and Resource-Based Constrained Delegation (RBCD)
1.4 Kerberos Armoring and FAST
1.5 Common Kerberos Attack Vectors
1.6 Kerberos Logging and Monitoring
2. Cre

====================

APPENDICES

Appendix X: AD Security Checklist (2026 Edition)

Appendix X: PowerShell and Command Reference for AD Attacks \& Defenses

Appendix X: Common Vulnerabilities and Exploits

Appendix X: Reference Architectures

Appendix X: Certification Pathways \& Resources

Appendix X: Tools and Toolkit

Appendix X: Recommended Tools
BloodHound
Mimikatz
Rubeus

# Appendix X: Further Reading and Resources

INDEX

Comprehensive index for quick reference.

Glossary of Terms

===============================================================================================================



\*\*1 Active Directory Exploitation and Defense
Master Attack Vectors and Build Unbreakable Domain Security

Imagine a domain environment where every attack vector is understood, every privilege escalation pathway is secured, and every lateral movement attempt is detected in near-real-time on the fly. This technically in-depth guide aims to bridge the gap between offensive and defensive security by providing you with deep technical knowledge of Active Directory exploitation techniques and the defensive strategies to counter them effectively. You'll master Kerberos ticketing attacks, credential theft methodologies, privilege escalation paths and attack vectors, and lateral movement tactics, among more, while simultaneously learning how to detect, prevent, and respond in an efficient manner to these critical and devastating domain threats. From conducting security and risk assessments and audits, to hardening domain infrastructure while combating attacks like Kerberoasting, DCShadow, DCSync, Password Spraying and Golden SAML abuse to responding to incidents, this book equips you with the practical knowledge and defensive frameworks needed to secure your organization's most critical assets. Through detailed attack flow and chain analysis, real-world use cases and scenarios, and defensive implementation strategies, you'll develop the expertise to identify vulnerabilities before attackers do and build resilient security controls that withstand sophisticated cyber threats.

Educational Content Disclaimer: This book provides comprehensive information and educational content on security, but does not replace professional advice. Always consult qualified professionals for important decisions.

Table of Contents

Introduction
Why Active Directory Security Matters
Aligning Offensive and Defensive Perspectives
How to Use This Book
Chapter 1: Kerberos Authentication and Exploitation Fundamentals
Kerberos Protocol Architecture and Components
Understanding Ticket Structure and Encryption
Identifying the Kerberos Attack Surface
Chapter 2: Kerberos Ticket Exploitation Techniques
Golden Ticket Attack Methods and Implementation
Silver Ticket Forgery and Service Impersonation
AS-REP Roasting and Pre-Authentication Bypass
Kerberoasting Attacks and Service Principal Name (SPN) Exploitation
Chapter 3: Credential Theft and Pass-the-Hash (PtH) Attacks
Credential Dumping Tactics and Memory Extraction
Pass-the-Hash Techniques and NTLM Exploitation
NTLM Relay Attacks and Authentication Interception
Chapter 4: Privilege Escalation Pathways and Domain Abuse
Identifying Privilege Escalation Vectors
Constrained Delegation Abuse and Impersonation
Unconstrained Delegation Exploitation
Domain Privilege Abuse and Administrative Exploitation
Chapter 5: Lateral Movement Detection and Evasion
Lateral Movement Techniques and Attack Chains
Detecting Lateral Movement Activities
Evasion Strategies and Stealth Techniques
Chapter 6: Group Policy Exploitation and Domain Infrastructure Hardening
Group Policy as an Attack Vector
Group Policy Exploitation Methods
Group Policy Hardening and Secure Configuration
Chapter 7: Domain Controller Compromise and Protection
Domain Controller Attack Scenarios and Objectives
Identifying Domain Controller Compromise Indicators
Domain Controller Hardening and Protection Controls
Chapter 8: Trust Relationship Attacks and Forest Security
Trust Types and Exploitation Methods
Forest Trust Exploitation and Cross-Domain Attacks
Securing Trust Relationships and Forest Architecture
Chapter 9: Authentication Hardening and Policy Enforcement
Password Policy Enforcement and Account Lockout Controls
Service Principal Name Management and Security
Multi-Factor Authentication (MFA) and Advanced Authentication Controls
Chapter 10: Security Monitoring and Anomaly Detection
Security Group Monitoring and Access Control Auditing
Anomaly Detection Methods and Behavioral Analysis
Forensic Analysis Techniques and Evidence Collection
Chapter 11: Incident Response and Threat Remediation
Incident Response Procedures and Playbooks
Threat Containment and Remediation Strategies
Post-Incident Hardening and Prevention
Chapter 12: Zero-Trust Architecture and Advanced Defense
Zero-Trust Architecture Principles and Implementation
Privileged Access Management and Just-In-Time (JIT) Access
Continuous Verification and Adaptive Security Controls
Chapter 13: Red Team Methodology and Assessment Execution
Attack Chain Analysis and Methodology
Assessment Planning and Scope Definition
Reporting Findings and Remediation Recommendations
Conclusion
Key Takeaways and Strategic Priorities
Continuous Improvements and Staying Current
===

1. Active Directory Exploitation and Defense
Mastering Attack Vectors, Detecting Threats, and Securing Your Domain Infrastructure Like a Boss

Imagine your Active Directory infrastructure operating with complete visibility into every attack vector, every privilege escalation pathway, and every lateral movement technique. You understand not just how attackers compromise real-world domains, but exactly how to detect, prevent, and respond to these threats in real-time. This fundamental guide on Active Directory offensive and defensive security tactics and techniques aims to bridge attacker and defender security gaps by teaching you the actual attack methodologies used by adversaries while simultaneously providing the defensive controls and detection strategies to effectively stop them. You'll master Kerberos exploitation techniques, credential theft tactics, privilege escalation pathways, and lateral movement evasion - then immediately learn how to harden each infrastructure component. From Golden Ticket attacks to Zero-Trust Architectural implementations, from forensic analysis to incident response procedures, you'll develop a dual perspective that separates elite security professionals from the rest. From conducting red team security assessments or building blue team defenses, this book will equip you with actionable and meaningful techniques, detection signatures, and hardening strategies that directly apply to your organization's overall security posture.

Educational Content Disclaimer: This book provides in-depth information and educational content on security, but does not replace professional advice. Always consult qualified professionals for important decisions.

Table of Contents

Introduction
Why Active Directory Security Matters Today
The Offensive-Defensive Security Balance
How to Use This Book Effectively
Chapter 1: Active Directory Fundamentals and Attack Surfaces
Active Directory Architecture and Components
Understanding Trust Relationships and Domain Boundaries
Mapping Your Attack Surfaces
Chapter 2: Kerberos Authentication and Exploitation
Kerberos Authentication Protocol Deep Dive
Kerberos Ticket Exploitation Techniques
Kerberoasting ad AS-REP Roasting Attacks
Chapter 3: Golden and Silver Ticket Attacks
Golden Ticket Attack Methods and Execution
Silver Ticket Forgery and Service Impersonation
Detecting and Preventing Forged Tickets
Chapter 4: Credential Theft and Pass-the-Hash (PtH) Attacks
Credential Dumping Tactics and Tools
Pass-the-Hash (PtH) Techniques and Lateral Movement
NTLM Relay Attacks and Mitigation
Chapter 5: Privilege Escalation and Domain Abuse
Identifying Privilege Escalation Pathways
Domain Privilege Abuse Techniques
Constrained, Unconstrained, and Role-Based Constrained Delegation (RBCD) Abuse
Chapter 6: Lateral Movement: Attack and Detection
Lateral Movement Evasion Techniques
Detecting Lateral Movement in Your Domain Environment
Preventing Lateral Movement Through Network Segmentation
Chapter 7: Group Policy Object (GPO) Exploitation and Hardening
Group Policy Object (GPO) Exploitation Methods
Group Policy Object (GPO) Hardening and Best Practices
Monitoring and Auditing Group Policy Object Changes
Chapter 8: Domain Controller (DC) Compromise and Trust Attacks
Domain Controller Compromise Scenarios
Trust Relationship Attacks and Forest Exploitation
Protecting Domain Controllers from Compromise
Chapter 9: Authentication Hardening and Account Protection
Password Policy Enforcement and Account Lockout Thresholds
Service Principal Names (SPNs) and Kerberos Hardening
Protecting Privileged Accounts and Service Accounts
Chapter 10: Monitoring, Detecting, and Forensic Analysis
Anomaly Detection Methods and Security Baselines
Forensic Analysis Techniques for Active Directory
Security Group Monitoring and Privileged Access Management (PAM)
Chapter 11: Incident Response and Zero-Trust Architecture
Incident Response Procedures for Domain Compromise
Implementing Zero-Trust Architecture in Active Directory Domain Environments
Blue Team Defense Strategies and Continuous Improvements
Chapter 12: Red Team Methodology and Attack Chain Analysis
Red Team Methodology and Tactics
Analyzing Complete Attack Chains
Conducting Effective Security Assessments
Conclusion
Building an Integrated Offensive-Defensive Security Program
Continuous Learning and Staying Current
Appendix X: Quick Reference Guides
Attack Techniques Quick Reference
Detection Signatures and Indicators
Active Directory Hardening Checklist
===

3. Active Directory Exploitation and Defense
Mastering Attack Vectors and Building Unbreakable Domain Security

Imagine your organization's Active Directory environment as a fortress - secure, resilient, and impenetrable to attackers. This comprehensive guide will equip you with the knowledge to build that fortress while understanding every tool an adversary might use to breach it. Whether you're defending against sophisticated attacks or conducting authorized security assessments, you'll find yourself mastering the art of offensive and defensive security to better defend and understand the attack vectors that threaten your very domain while implementing defensive security controls that actually work. From Kerberos ticket exploitation to Zero-Trust Architecture, from credential dumping tactics to forensic analysis techniques, this book aims to bridge the critical gap between offensive and defensive security. You'll learn how attackers chain together vulnerabilities and exploits to conduct privilege escalation and lateral movement, how to detect these techniques in near-real-time, and how to architect defenses that eliminate entire attack chains and categories. With practical methodologies, real-world use cases and scenarios, and actionable hardening strategies, you'll transform your Active Directory security posture from reactive to proactive, protecting your organization's most critical assets.

Educational Content Disclaimer: This book provides comprehensive information and educational content on security, but does not replace professional advice. Always consult qualified professionals for important decisions.

Table of Contents

Introduction
Why Active Directory Security Matters
The Convergence of Offensive and Defensive Perspectives
How to Use This Book
Chapter 1: Active Directory Fundamentals and Attack Surfaces
Active Directory Architecture and Components
Understanding Trust Relationships and Domain Boundaries
Mapping Your Attack Surfaces
Chapter 2: Kerberos Authentication: Exploitation and Hardening
Kerberos Authentication Protocol Deep Dive
Kerberos Ticket Exploitation Techniques
Golden Ticket Attack Methods and Detection
Kerberos Authentication Hardening Strategies
Chapter 3: Advanced Kerberos Attacks: Roasting and Delegation
AS-REP Roasting Attacks and Mitigation
Kerberoasting: Extracting Service Credentials
Constrained Delegation Abuse and Defense
Unconstrained Delegation Risks and Remediation
Chapter 4: Credential Theft and Pass-the-Hash (PtH) Attacks
Credential Dumping Tactics and Detection
Pass-the-Hash Techniques and Prevention
NTLM Relay Attacks and Mitigation Strategies
Silver Ticket Forgery and Detection Methods
Chapter 5: Privilege Escalation and Domain Privilege Abuse
Identifying Privilege Escalation Pathways
Domain Privilege Abuse Techniques
Service Principal Names (SPNs) and Exploitation
Detecting Privilege Escalation Attempts
Chapter 6: Lateral Movement: Techniques and Detection
Lateral Movement Attack Methodologies
Detecting Lateral Movement in Near-Real-Time
Evasion Techniques and Counter-Evasion Strategies
Chapter 7: Group Policy: Exploitation and Hardening
Group Policy Exploitation Techniques
Group Policy Hardening and Secure Configurations
Monitoring and Auditing Group Policy Changes
Chapter 8: Domain Controller Compromise and Trust Attacks
Domain Controller Compromise Indicators and Prevention
Forest Trust Exploitation and Network Segmentation
Trust Relationship Attack Vectors and Defenses
Chapter 9: Authentication Hardening and Account Protection
Account Lockout Policies and Brute Force Prevention
Password Policy Enforcement and Complexity Requirements
Strengthening User Account Protections
Chapter 10: Monitoring, Detection, and Incident Response
Security Group Monitoring and Auditing
Anomaly Detection Methods and Implementation
Forensic Analysis Techniques for Active Directory
Incident Response Procedures and Playbooks
Chapter 11: Zero-Trust Architecture and Privileged Access Management
Zero-Trust Architecture Principles for Active Directory
Privileged Access Management Implementation
Continuous Verification and Adaptive Security
Chapter 12: Red Team Methodology and Security Assessment
Red Team Methodology and Attack Chain Analysis
Conducting Effective Security Assessments
Active Directory Vulnerability Auditing and Remediation
Conclusion
Building an Integrated Defense Strategy
Continuous Improvement and Staying Current
Glossary
Further Reading and Resources
===

\*\*4. Active Directory Exploitation and Defense
Mastering Attack Vectors, Detecting Threats, and Securing Your Domain Infrastructure Like a Boss

Imagine a domain infrastructure where every attack vector is understood, every privilege escalation path is blocked, and every threat is detected before it has a chance to spread and infect. This book bridges the gap between offensive and defensive security by teaching you how attackers think and act within IVE Directory domain environments. You'll master the most dangerous attack methodologies - from Kerberos delegation abuse and credential theft to GPO exploitation and replication attacks - while simultaneously learning how to detect, prevent, and respond to each threat. Whether you're conducting security assessments, hunting for compromises, or hardening your domain infrastructure, this comprehensive guide will provide you the tactical knowledge and strategic frameworks you need to be the best defender you can be. Combining real-world attack scenarios with defensive countermeasures, you'll develop the ability to think like an attacker and defend like an expert. Learn to analyze attack chains, implement Zero-Trust principles, configure advanced audit policies, and build monitoring systems that catch sophisticated threats. By the end, you'll possess the dual perspective necessary to secure modern Active Directory environments against the some of the most advanced threats

Table of Contents

Introduction
Why Active Directory Security Matters Today
The Attacker-Defender Mindset
How to Use This Book
Chapter 1: Active Directory Fundamentals and Attack Surfaces
Understanding Active Directory Architecture and Trust Relationships
Mapping Your Attack Surfaces: Objects, Permissions, and Delegation
Reconnaissance Framework: Domain Enumeration Techniques
Chapter 2: Kerberos Authentication Exploitation
Kerberos Protocol Weaknesses and Attack Vectors
Kerberos Delegation Abuse: Constrained, Unconstrained and Resource-Based
Preauth Disabling and S4U2Self/S4U2Proxy Exploitation
Defending Kerberos: Authentication Hardening and Delegation Controls
Chapter 3: Credential Theft and Extraction Attacks
LSASS Memory and Secrets Dumping: Techniques and Detection
DCSync Attack Methodology and Replication Exploitation
NTDS.dit Extraction Methods and Offline Cracking
Defending Against Credential Theft: Credential Guard and Continuous Monitoring
Chapter 4: Group Policy and Object Exploitation
GPO Abuse and Exploitation: Logon Scripts, Scheduled Tasks, and Startup Scripts
Computer Object Exploitation and Privilege Escalation
Security Group Policy: Hardening, Auditing, and Monitoring
Chapter 5: Advanced Replication and Domain Controller (DC) Attacks
DCShadow Attacks: Rogue Domain Controller Exploitation
Netlogon Exploitation and PetitPotam Attacks
Defending Domain Controllers: Replication Security and Monitoring
Chapter 6: Certificate and Trust Relationship Attacks
AD CS Certificate Abuse and Exploitation Techniques
Shadow Credentials Attacks and Alternate Credential Pathways
AD FS Golden SAML 2.0 Abuse: Federation and Assertion Statement Attacks
Defending Certificate Authorities (CAs), Certificates, and Trust Relationships
Chapter 7: Injection Attacks and Lateral Movement
LDAP Injection Attack Vectors and Exploitation
Detecting Lateral Movement and Attack Chains
Preventing Injection Attacks and Lateral Movement
Chapter 8: Persistence, Backdoors, and Skeleton Key Attacks
Persistence Mechanisms Detection and Prevention
Backdoor Detection Methods and Indicators of Compromise (IOCs)
Skeleton Key and Malware-Based Persistence
Chapter 9: Defensive Monitoring and Domain Threat Hunting
Audit Policy Configurations and Event Log Analysis Framework
Threat Hunting in Active Directory: Methodologies and TTPs
BloodHound Graph Analysis for Attack Path Identification
Building Comprehensive Defensive Monitoring Strategies
Chapter 10: Security Assessment and Domain Hardening
Compromise Assessment Framework and Incident Response (IR)
Security Descriptor Auditing and Privilege Boundary Enforcement
Password Policy Enforcement and User Account Protection
Implementing Zero-Trust Architecture in Active Directory Domain Environments
Chapter 11: Social Engineering and Human-Hacking
Social Engineering Attack Vectors and Methodologies
Social Engineering Defense and User Security Awareness Programs
Conclusion
Building an Integrated Offense-Defense Strategy
Continuous Improvements and Staying Ahead of Threats
Glossary
Further Reading and Resources
===



========================================================================

6. Active Directory Exploitation and Defense
Master Attack Vectors and Build Unbreakable Domain Security

Imagine your domain infrastructure operating with complete visibility into every attack vector, every privilege escalation path, and every lateral movement technique. You understand exactly how attackers think, what they target, and how they move through your environment—because you've learned to think like them. This comprehensive guide bridges the gap between offensive and defensive security by teaching you both sides of Active Directory exploitation. You'll master attack methodologies including Kerberos delegation abuse, credential theft, and domain controller compromise while simultaneously building defensive controls that detect and prevent these exact techniques. Through practical frameworks for threat hunting, incident response, and security assessment, you'll develop the expertise to identify vulnerabilities before attackers do. Whether you're conducting red team operations or hardening your blue team defenses, this book provides the tactical knowledge and strategic insights needed to secure your domain infrastructure against sophisticated, multi-stage attacks.

Table of Contents

Introduction
Why Active Directory Security Matters
The Dual Perspective: Offense and Defense
How to Use This Book
Chapter 1: Active Directory Fundamentals and Attack Surface
Active Directory Architecture and Components
Domain and Forest Trust Relationships
Identifying the Attack Surface
Chapter 2: Domain Enumeration and Reconnaissance
LDAP Enumeration Techniques and Injection Attacks
BloodHound Graph Analysis and Path Discovery
Mapping Privilege Escalation Paths
Chapter 3: Kerberos Authentication Exploitation
Kerberos Protocol Fundamentals
Kerberos Delegation Abuse and Constrained Delegation
Preauth Disabling and Ticket Forgery
S4U2Self and S4U2Proxy Attack Methodologies
Chapter 4: Credential Theft and Extraction
LSASS Memory Dumping and Credential Guard Bypass
DCSync Attack Methodology and Domain Replication
NTDS.dit Extraction and Offline Cracking
Chapter 5: Group Policy and Security Descriptor Exploitation
Group Policy Object Abuse and Exploitation
Security Descriptor Auditing and Misconfiguration
Logon Script Exploitation and Hardening
Chapter 6: Certificate and PKI Exploitation
Active Directory Certificate Services Abuse
Shadow Credentials and Certificate Injection
AD FS Golden SAML 2.0 Abuse
Chapter 7: Advanced Persistence and Lateral Movement
Persistence Mechanisms: Skeleton Keys and Backdoors
DCShadow Attacks and Rogue Domain Controllers
Netlogon Exploitation and PetitPotam
Chapter 8: Defensive Monitoring and Detection
Audit Policy Configuration and Event Log Analysis
Threat Hunting Framework for Active Directory
Detecting Persistence, Lateral Movement, and Privilege Escalation
Chapter 9: Incident Response and Compromise Assessment
Incident Response Procedures for Domain Compromise
Compromise Assessment Framework and Forensics
Recovery and Post-Incident Hardening
Chapter 10: Building Resilient Defenses and Zero-Trust Architecture
Implementing Layered Defensive Controls
Zero-Trust Architecture Principles for Active Directory
Password Policy Enforcement and Account Protection
Conclusion
Integrating Offense and Defense
Continuous Security Assessment and Improvement
Appendix: Tools, Commands, and Resources
Offensive Security Tools and Techniques
Defensive Monitoring and Analysis Tools
Reference Materials and Further Learning
===

\*\* 7. Active Directory Exploitation and Defense
Master Attack Vectors and Build Unbreakable Domain Security

Imagine your domain infrastructure operating with complete visibility into every attack vector, every privilege escalation path, and every lateral movement technique. You understand exactly how attackers think, what they target, and how they move through your environment—because you've learned to think like them. This comprehensive guide bridges the gap between offensive and defensive security by teaching you both sides of Active Directory exploitation. You'll master attack methodologies including Kerberos delegation abuse, credential theft, and domain controller compromise while simultaneously building defensive controls that detect and prevent these exact techniques. Through practical frameworks for threat hunting, incident response, and security assessment, you'll develop the expertise to identify vulnerabilities before attackers do. Whether you're conducting red team operations or hardening your blue team defenses, this book provides the tactical knowledge and strategic insights needed to secure your domain infrastructure against sophisticated, multi-stage attacks.

Table of Contents

========================================================================

8. Active Directory Exploitation and Defense
Mastering Kerberos, LDAP, AD CS, and Advanced Persistence Techniques for Offensive and Defensive Security

Imagine confidently navigating the complex arena of Active Directory security - understanding exactly how attackers are able to successfully exploit Kerberos delegations, perform injection attacks via LDAP or SQL, and exploit certificate and ticket issuing systems while simultaneously implementing resilient detection mechanisms that catch these cyberattacks in near-real-time. This in-depth guide aims to bridge the gap between offensive and defensive security, providing you with the technical depth needed to both exploit and defend against the most sophisticated attacks against the vast infrastructure that comprises AD. You'll master Kerberos ticket forgeries and detections, AD CS web enrollment and certificate template abuses, constrained delegation exploitation, and credential extraction defense, plus more. Learn to perform advanced domain and subdomain enumeration while evading detection, analyze GPO abuse patterns, and implement DCSync attack defenses. Discover how to conduct threat hunting using event log analysis frameworks, configure advanced auditing policies, create, deploy, and enforce stringent security policies via GPO, and build monitoring strategies that identify persistence mechanisms and hidden backdoors. Whether you're looking to execute shadow credentialed attacks, or defend against them, this book will quip you with the practical knowledge to secure enterprise AD environments against the full spectrum of available Active Directory threats.

Table of Contents

Introduction
Why Active Directory Security Matters
The Offensive-Defensive Balance
How to Use This Book
Chapter 1: Kerberos Fundamentals and Attack Surfaces
Kerberos Authentication Protocol Overview and Components
Ticket Structure, the Key Distribution Center (KDC), and Cryptographic Analysis
Identifying Kerberos Attack Vectors
Chapter 2: Kerberos Ticket Forgery and Detection
Golden Ticket Attacks and Execution
Silver Ticket Attacks and Execution
Sapphire Ticket Attacks and Execution
Diamond Ticket Attacks and Execution
Detecting Ticket Forgery Through Event Log Analysis and Correlation
Implementing Kerberos Armor and "Kerberos-Only" Protections
Chapter 3: Kerberos Delegation Exploitation and Defense
Constrained Delegation Abuse Techniques
Unconstrained Delegation Attack Chains
Resource-Based Constrained Delegation (RBCD) Exploitation
Kerberos Delegation Auditing and Defense Mechanisms
Chapter 4: Kerberoasting and AS-REP Roasting Prevention
Kerberoasting Attack Mechanics and Execution
AS-REP Roasting and Preauthentication Bypass
Detection Strategies and Mitigation Security Controls
Chapter 5: LDAP Injection and Channel Security
LDAP Query Injection Attack Vectors
LDAP Signing and Channel Binding Enforcement
LDAP Defense Strategies and Validation
Chapter 6: Credential Extraction and Defense
LSASS Memory Dumping and Credential Extraction
DCSync Attacks and Replication Abuse
NTDS.dit Extraction and Database Security
Credential Guar and LSA Protection Defense
Chapter 7: AD CS Exploitation and Hardening
AC DS Architecture and Certificate Issuance
Web Enrollment Agent Abuse and Certificate Forgery
AD CS Template Misconfiguration Exploitation
Chapter 8: Advanced Reconnaissance and Evasion
Advanced Domain and Subdomain Enumeration Techniques
BloodHound and SharpHound Graph Analysis and Attack Pathway Mapping
Active Directory Reconnaissance Evasion
Chapter 9: Group Policy Abuse and Persistence
Group Policy Poisoning and Abuse Techniques
Group Policy Preferences (GPP) Abuse
Logon Script Abuse and Persistence
GPO Auditing and Defense Strategies
Chapter 10: NTLM Relay and Zerologon Attacks
NTLM Relay Attack Mechanics and Execution
Zerologon Vulnerability Exploitation
NTLM Relay Detection and Mitigation
Chapter 11: Threat Hunting and Continuous Monitoring (ConMon)
Sysmon AD Monitoring Rules and Configuration
Event Log Analysis Frameworks and Forensics
Advanced Audit Policy Configuration
Threat Hunting Framework for Active Directory
Chapter 12: Lateral Movement and Privilege Escalation
Lateral Movement Detection and Prevention
Privilege Escalation Chains and Exploitation
Malware Persistence in Active Directory
Conclusion
Building an Integrated Defense Strategy
ConMon and Improvement
Appendix
Detection Rules and Queries
Active Directory Hardening Checklist
Further Reading and Resources
===

9 Active Directory Exploitation and Defense
Mastering Kerberos, LDAP, and AD CS Attacks While Building Enterprise-Grade Defenses

Imagine your Active Directory environment fully hardened against sophisticated attacks, with every exploitation technique detected in real-time and every attacker's movement tracked and blocked. This comprehensive guide equips you with both the offensive knowledge to identify vulnerabilities and the defensive expertise to eliminate them. You'll master the complete attack lifecycle—from advanced domain enumeration and Kerberos delegation abuse to LDAP injection, ADCS exploitation, and credential extraction. Simultaneously, you'll learn to implement detection rules, configure advanced audit policies, and build threat hunting frameworks that catch attackers before they escalate privileges. Whether you're conducting red team assessments or defending enterprise infrastructure, this book provides the technical depth needed to understand how attackers compromise Active Directory and the practical strategies to stop them. Each attack technique is paired with corresponding defensive controls, enabling you to think like both attacker and defender. By the end, you'll possess the knowledge to secure your organization's most critical asset—the directory service that controls access to everything.

Introduction
Why Active Directory Security Matters
The Attack-Defense Duality
How to Use This Book
Chapter 1: Active Directory Fundamentals and Attack Surface
Active Directory Architecture and Trust Relationships
Kerberos Protocol Mechanics and Ticket Flow
LDAP Authentication and Directory Queries
Mapping Your Attack Surface
Chapter 2: Advanced Domain Enumeration and Reconnaissance Evasion
Advanced Enumeration Techniques and Tools
BloodHound Graph Analysis and Path Discovery
Evading Detection During Reconnaissance
Detecting Reconnaissance Activities
Chapter 3: Kerberos Delegation Exploitation and Defense
Constrained Delegation Exploitation Techniques
Unconstrained Delegation Attacks and Mitigation
Resource-Based Delegation and Exploitation Chains
Auditing and Monitoring Delegation Abuse
Chapter 4: Credential Extraction and Kerberos Attacks
Kerberoasting Attacks and Prevention Strategies
AS-REP Roasting and Preauthentication Enforcement
LSASS Memory Dumping and Credential Guard Defense
Kerberos Ticket Forgery Detection and Kerberos Armor
Chapter 5: LDAP Injection and Channel Binding Security
LDAP Injection Attack Vectors and Exploitation
LDAP Channel Binding and Signing Enforcement
Query Validation and Input Sanitization
Detecting LDAP-Based Attacks
Chapter 6: Active Directory Certificate Services Exploitation
ADCS Architecture and Certificate Issuance
Enrollment Agent Abuse and Rogue Certificate Issuance
ADCS Template Hardening and Misconfiguration Detection
Enrollment Auditing and Certificate Monitoring
Chapter 7: Advanced Credential and Replication Attacks
DCSync Attacks and Replication Permission Defense
DCShadow Attacks and Replication Forensics
PetitPotam and Netlogon Vulnerability Exploitation
Monitoring and Detecting Replication Attacks
Chapter 8: Lateral Movement and Privilege Escalation Chains
Mapping Lateral Movement Paths and Trust Chains
Privilege Escalation Chain Exploitation
Shadow Credentials and Alternate Authentication Methods
Detecting Lateral Movement and Escalation Attempts
Chapter 9: Persistence, Backdoors, and Malware in Active Directory
Group Policy Poisoning and Logon Script Abuse
Malware Persistence Mechanisms in Active Directory
Golden SAML Attacks and Federation Abuse
Detecting Persistence and Backdoor Mechanisms
Chapter 10: Monitoring, Detection, and Threat Hunting
Sysmon Rules for Active Directory Monitoring
Advanced Audit Policies and Event Log Analysis
Threat Hunting Frameworks and Behavioral Analysis
Detecting Zerologon and PrintNightmare Exploitation
Chapter 11: Comprehensive Defense Strategy and Hardening
Building a Comprehensive Defense Framework
Active Directory Backup Security and Recovery
Managing Credential Caching Risks
Active Directory Hardening Checklist
Conclusion
Your Ongoing Security Journey
Staying Current with Emerging Threats
Glossary
Further Reading and Resources
===

\*\* 10. Active Directory Exploitation and Defense
Master Kerberos, LDAP, and ADCS Attacks While Building Enterprise-Grade Defenses

Imagine your Active Directory environment fully hardened against sophisticated attacks, with every exploitation technique detected in real-time and every attacker's movement tracked and blocked. This comprehensive guide equips you with both the offensive knowledge to identify vulnerabilities and the defensive expertise to eliminate them. You'll master the complete attack lifecycle—from advanced domain enumeration and Kerberos delegation abuse to LDAP injection, ADCS exploitation, and credential extraction. Simultaneously, you'll learn to implement detection rules, configure advanced audit policies, and build threat hunting frameworks that catch attackers before they escalate privileges. Whether you're conducting red team assessments or defending enterprise infrastructure, this book provides the technical depth needed to understand how attackers compromise Active Directory and the practical strategies to stop them. Each attack technique is paired with corresponding defensive controls, enabling you to think like both attacker and defender. By the end, you'll possess the knowledge to secure your organization's most critical asset—the directory service that controls access to everything.

# Table of Contents

11. Active Directory Attack and Defense
Master Kerberos Exploitation, ADCS Abuse, and Enterprise Security Hardening

Imagine confidently defending your enterprise against sophisticated Active Directory attacks while understanding exactly how attackers exploit Kerberos, ADCS, and delegation mechanisms. This comprehensive guide equips you with both offensive and defensive expertise to secure your critical infrastructure. You'll master the attack techniques that threaten your environment—from Golden Ticket forgery and ADCS certificate abuse to constrained delegation chains—while learning proven detection and prevention strategies. Discover how to implement Credential Guard, enforce LDAP signing, deploy Kerberos armor, and build Sysmon monitoring rules that catch attackers in action. Whether you're conducting security assessments, responding to incidents, or hardening your infrastructure, this book provides the technical depth and practical guidance needed to stay ahead of threats. Learn to audit delegation configurations, detect lateral movement, prevent credential extraction, and build resilient Active Directory baselines that withstand both known exploits and emerging attack vectors. Transform your security posture from reactive to proactive.

Table of Contents
Introduction
Why Active Directory Security Matters
The Dual Perspective: Offense and Defense
How to Use This Book
Chapter 1: Kerberos Protocol Fundamentals and Attack Surface
Kerberos Authentication Flow and Components
Ticket Structure and Cryptographic Validation
Kerberos Authentication Protocol Vulnerabilities and Weaknesses
Chapter 2: Golden and Silver Ticket Attacks
Golden Ticket Creation and Exploitation Techniques
Golden Ticket Detection Methods and Events Analysis
Silver Ticket Attacks and Forensics Analysis
Chapter 3: Credential Extraction and Kerberoasting Attacks
LSASS Memory Dump Techniques and Prevention
Kerberoasting Attacks and Mitigation Strategies
AS-REP Roasting and Preauthentication Bypass Defense
Chapter 4: Delegation Chain Exploitation and Defense
Constrained Delegation Chains and Exploitation
Unconstrained Delegation Attacks and Detection
Resource-Based Delegation Attacks and Auditing
Chapter 5: Active Directory Certificate Services (AD CS) Exploitation
AD CS Misconfiguration Scanning and Identification
Certificate Template Abuse and Privilege Escalation
Web Enrollment Agent Abuse and Restriction Enforcement
Chapter 6: NTLM Relay and Downgrade Attack Prevention
NTLM Relay Attack Techniques and Detection
NTLM Downgrade Attack Defense and Mitigation
LDAP Signing Configuration and Channel Binding Enforcement
Chapter 7: Lateral Movement Detection and Prevention
Lateral Movement Forensics and Attack Chain Analysis
Active Directory Reconnaissance Evasion and Detection
Malware Persistence Detection in Active Directory
Chapter 8: Credential Protection and Memory Security
Credential Guard Implementation and Configuration
Credential Caching Mitigation and Risk Assessment
Kerberos Armor Deployment and Fast Armor Protections
Chapter 9: Monitoring, Auditing, and Forensic Capabilities
Sysmon Event log tuning for Active Directory Monitoring
AD Audit Policy Hardening and Event Log Configuration
AD Replication Security Monitoring and Integrity Validation
Chapter 10: Active Directory Hardening and Baseline Implementation
Active Directory Hardening Baselines and Best Practices
Group Policy Enforcement Auditing and Poisoning Defense
PrintSpooler Service Lockdown and Service Hardening
Chapter 11: LDAP Security and Query Injection Prevention
LDAP Query Injection Prevention and Detection
LDAP Enumeration Attacks and Monitoring
Directory Service Hardening and Access Controls
Chapter 12: Incident Response and Forensic Analysis
Privilege Escalation Chain Analysis and Investigation
AD Backup Integrity Verification and Recovery
Forensic Investigation Techniques and Evidence Collection
Conclusion
Building Your Comprehensive Defense Strategy
Continuous Improvement and Threat Adaptation
===

\*\*12. Active Directory Attack and Defense Mastery
Complete Offensive and Defensive Strategies for Securing Enterprise Identity, Credential, and Access Management (ICAM) Infrastructure

Imagine your organization's Active Directory environment is completely hardened against cyberattacks, with critical vulnerabilities identified and remediated, and your security team can detect and respond to threats in near-real-time all thanks to your defensive inputs, security implementations and strategies. This security-rich guide will equip you with the knowledge to achieve that reality. Whether you are conducing penetration tests, defending enterprise networks, or validating security controls, you will master the complete spectrum of Active Directory attack techniques and defensive strategies. From Kerberos exploitation and credential extraction to lateral movement detection and incident response, this book provides you practical, hands-on guidance grounded in real-world cyberattack scenarios. You will learn how to map attacks to the MITRE ATT\&CK Framework, understand the Cyber Kill Chain, and implement detection strategies that actually work. With detailed coverage of both offensive security methodologies and defensive countermeasures, you will develop the necessary expertise to secure your organization's most critical asset: its identity infrastructure.

Table of Contents
Introduction
Why Active Directory Security Matters
The Duality of Offensive and Defensive Security
How to Use This Book
Frameworks: MITRE ATT\&CK and Cyber Kill Chain
Chapter 1: Active Directory Fundamentals and Attack Surfaces
Active Directory Architecture and Components
Authentication and Identity Security Foundations
Identifying the Privileged Attack Surface
Active Directory Security Assessment Frameworks
Chapter 2: Reconnaissance and Enumeration Techniques
Active Directory Reconnaissance Tools and Methods
LDAP Enumeration and Domain Mapping
BloodHound and SharpHound Path Analysis
PowerShell Active Directory Enumeration Techniques
Chapter 3: Kerberos Authentication Protocol Attacks
Kerberoasting Attack Techniques and Detection
AS-REP Roasting Exploitation and Mitigation
Kerberos Ticket Analysis and Forensics
Defending Against Kerberos-Based Attacks
Chapter 4: Credential Extraction and Abuse
Mimikatz Credential Extraction Methodology
DCSync Attack Methodology and Detection
Attacking NTDS.dit and Password Hash Extraction
Defending Against Credential Extraction Attacks
Chapter 5: Lateral Movement and Privilege Escalation
Pass-the-Hash and Pass-the-Ticket Attack Chains
Detecting Lateral Movement Across Domains
Privilege Escalation Detection and Prevention
Defensive Strategies for Movement and Escalation
Chapter 6: NTLM Relay and Network-Based Attacks
NTLM Relay Attach Chains and Exploitation
LDAP Relay Exploitation Techniques
Responder Framework Usage and Detection
Defending Against Relay-Based Attacks
Chapter 7: Trust Relationships and Cross-Domain Attacks
Exploiting Active Directory Domain Trusts
Forest Trust Exploitation and Cross-Forest Attacks
Child-to-Parent Domain Escalation Techniques
Monitoring and Defending Trust Relationships
Chapter 8: Persistence and Advanced Exploitation
Skeleton Key Persistence and Detection
Active Directory Access Control List (ACL) and Access Control Entry (ACE) Abuse Techniques
AdminSDHolder Abuse and SID History Injection
AD CS Privilege Escalation and LAPS Exploitation
Chapter 9: Advanced Defensive Monitoring and Detection
Event Log Forensics and Analysis Techniques
Threat Hunting in Active Directory Environments
Defensive Monitoring Strategies and Implementation
Blue Team Detection Methods and Indicators
Chapter 10: Incident Response and Attack Chain Analysis
Understanding Attack Chain Workflows
Mapping Attacks to the MITRE ATT\&CK Framework
Incident Response Procedures for Active Directory
Applying the Cyber Kill Chain to AD Incidents
Chapter 11: Red Team, Blue Team, and Purple Team Operations
Red Team Engagement Planning and Execution
Blue Team and Defensive Security Goals
Purple Team Simulation and Validation
Conclusion
Building an Integrated Offense-Defense Strategy
Continuous Improvements and Staying Current
Glossary
Further Reading and Resources
===

\*\* 13. Active Directory Exploitation and Defense
A Comprehensive Guide to Attacking, Defending, and Securing Enterprise Identity Infrastructure

Imagine confidently navigating the complex landscape of Active Directory security—knowing exactly how attackers exploit vulnerabilities and precisely how to defend against them. This comprehensive guide bridges the gap between offensive and defensive security by providing practical, real-world techniques used by ethical hackers and security teams. You'll master attack methodologies including Kerberoasting, credential extraction, pass-the-hash chains, and NTLM relay attacks while simultaneously learning how to detect, prevent, and respond to these threats. The book maps every attack to the MITRE ATT\&CK framework and cyber kill chain, ensuring you understand the strategic context behind each technique. Whether you're conducting red team engagements, implementing blue team defenses, or orchestrating purple team simulations, you'll gain actionable insights into Active Directory's relational concepts, authentication vulnerabilities, and privilege escalation paths. From domain controller attacks to forest trust exploitation, from BloodHound enumeration to incident response procedures, this guide equips you with the knowledge to secure enterprise identity infrastructure against sophisticated threats.

Table of Contents
Introduction
Why Active Directory Security Matters
Red Team, Blue Team, and Purple Team Perspectives
How to Use This Book
Chapter 1: Active Directory Fundamentals and Attack Surface
Active Directory Architecture and Components
Authentication and Identity Security Concepts
Identifying the Privileged Attack Surface
Active Directory Security Assessment Frameworks
Chapter 2: Reconnaissance and Enumeration Techniques
Active Directory Recon Tools and Frameworks
LDAP Enumeration and PowerShell Reconnaissance
BloodHound and SharpHound for Path Analysis
Malicious Enumeration and Domain Mapping
Chapter 3: Kerberos Authentication Attacks
Kerberoasting Attack Techniques and Exploitation
AS-REP Roasting and Exploitation Methodology
Kerberos Ticket Analysis and Abuse
Pass-the-Ticket Exploitation and Lateral Movement
Chapter 4: Credential Extraction and Abuse
Mimikatz Credential Extraction Techniques
DCSync Attack Methodology and Domain Controller Compromise
Attacking NTDS.dit and Password Database Extraction
Pass-the-Hash Attack Chains and Lateral Movement
Chapter 5: NTLM Relay and Network-Based Attacks
NTLM Relay Attack Chains and Exploitation
LDAP Relay Exploitation and Domain Controller Attacks
Responder Framework Usage and Network Poisoning
Authentication Vulnerabilities and Relay Prevention
Chapter 6: Privilege Escalation and Persistence Mechanisms
AD ACL and ACE Abuse for Privilege Escalation
ADCS Privilege Escalation Techniques
Skeleton Key Persistence and Domain Controller Backdoors
AdminSDHolder Abuse and Privilege Persistence
Chapter 7: Advanced Persistence and Lateral Movement
SID History Injection and Privilege Escalation
Abusing Microsoft LAPS and ms-DS-MachineAccountQuota
GPOddity and Group Policy Object Exploitation
DPAPI Attacks and Credential Decryption
Chapter 8: Cross-Forest and Trust-Based Attacks
Forest Trust Exploitation and Cross-Forest Attacks
Child-to-Parent Domain Escalation
Exploiting AD Domain Trusts for Enterprise Compromise
ExtraSIDS Attack and SID History Manipulation
Chapter 9: Red Team Operations and Attack Planning
Attack Chain Workflow and MITRE ATT\&CK Mapping
Cyber Kill Chain and Attack Phases
Red Team and Offensive Security Goals for AD
Red Team Engagement Planning and Execution
Chapter 10: Blue Team Defense and Detection
Blue Team and Defensive Security Goals for AD
Defensive Monitoring Strategies and Event Log Forensics
Privilege Escalation and Lateral Movement Detection
Incident Response Procedures and Threat Hunting
Chapter 11: Purple Team Simulation and Validation
Purple Team Security Goals and Objectives
Purple Team Simulation Exercises and Methodology
Validating Detection Methods and Control Effectiveness
Administrative Tiering Model and Best Practices
Chapter 12: Defensive Architecture and Resilience
Offensive and Defensive Architecture for Enterprise Security
Security Identifier Architecture and Cryptographic Foundations
Best Practices for Surviving a Cyberattack
Critical Security Risk: Native Administrator Account Exploitation
Conclusion
Key Takeaways and Strategic Insights
Continuous Learning and Professional Development
Glossary
Further Reading and Resources
===

14. Active Directory Attack and Defense Mastery
Complete Guide to Offensive and Defensive Security in Active Directory Enterprise Environments

Imagine confidently navigating the complex landscape of Active Directory security, knowing exactly how attackers exploit vulnerabilities and precisely how to detect and stop them. This comprehensive guide equips you with the knowledge and practical skills to master both sides of the Active Directory security equation. You'll discover the complete attack chain from initial reconnaissance through persistence, learning how real-world attacks unfold and where defenders can intervene. Explore offensive techniques including Kerberoasting, credential extraction, and privilege escalation while simultaneously understanding the defensive monitoring strategies, detection methods, and incident response procedures that stop these attacks. This book bridges the gap between theory and practice, mapping attacks to the MITRE ATT\&CK framework and Cyber Kill Chain while providing hands-on guidance for enumeration, exploitation, and defense. Whether you're conducting red team engagements, building blue team detection capabilities, or validating security controls through purple team exercises, you'll gain the architectural understanding and practical expertise needed to protect enterprise environments effectively.

Table of Contents
Introduction
Why Active Directory Security Matters
Red Team, Blue Team, and Purple Team Perspectives
How to Use This Book
MITRE ATT\&CK and Cyber Kill Chain Overview
Chapter 1: Active Directory Fundamentals and Architecture
Understanding Active Directory Structure and Components
Domain Trusts and Forest Architecture
Security Identifiers and Cryptographic Foundations
Administrative Tiering Models and Privilege Boundaries
Chapter 2: Reconnaissance and Enumeration Techniques
Passive Reconnaissance and Footprinting
LDAP Enumeration and Active Directory Recon Tools
BloodHound and SharpHound Path Analysis
PowerShell Active Directory Enumeration for Network Reconnaissance
Chapter 3: Kerberos Authentication Attacks
Kerberoasting Attack Techniques and Detection
AS-REP Roasting Exploitation and Mitigation
Pass-the-Ticket Exploitation and Kerberos Ticket Analysis
Kerberos Ticket Analysis for Incident Response
Chapter 4: Credential Extraction and Lateral Movement
Mimikatz Credential Extraction Techniques
DCSync Attack Methodology and Detection
Pass-the-Hash Attack Chains and Lateral Movement
Attacking NTDS.dit and Database Extraction
Chapter 5: NTLM and LDAP Relay Attacks
NTLM Relay Attack Chains and Exploitation
LDAP Relay Exploitation and Responder Framework
Detecting and Preventing Relay Attacks
Chapter 6: Privilege Escalation and Domain Escalation
Active Directory ACL and ACE Abuse for Privilege Escalation
ADCS Privilege Escalation Techniques
Child-to-Parent Domain Escalation Attacks
Forest Trust Exploitation and Cross-Forest Attacks
Chapter 7: Persistence and Backdoor Mechanisms
Skeleton Key Persistence and Domain Controller Attacks
AdminSDHolder Abuse and Privilege Persistence
SID History Injection and Persistence Techniques
GPOddity and Group Policy Object Exploitation
Chapter 8: Advanced Attack Techniques and Evasion
Abusing Microsoft LAPS via ms-DS-MachineAccountQuota
Active Directory DPAPI Attacks and Data Protection
Active Directory AMSI Bypass and Evasion Techniques
ExtraSIDS Attack and Advanced Persistence
Chapter 9: Defensive Monitoring and Detection Strategies
Event Log Forensics and Active Directory Auditing
Lateral Movement Detection and Behavioral Analysis
Privilege Escalation Detection Methods
Threat Hunting in Active Directory Environments
Chapter 10: Incident Response and Forensic Analysis
Incident Response Procedures for Active Directory Breaches
Forensic Analysis and Malware Identification
Recovery and Remediation Strategies
Chapter 11: Red Team, Blue Team, and Purple Team Operations
Red Team Engagement Planning and Execution
Blue Team Detection Methods and Defense Architecture
Purple Team Simulation and Control Validation
Attack Chain Workflow and Cyber Kill Chain Mapping
Chapter 12: Security Assessment Frameworks and Best Practices
Active Directory Security Assessment Frameworks
Authentication and Identity Security Best Practices
Best Practices for Surviving a Cyberattack
Managing the Privileged Attack Surface
Conclusion
Key Takeaways and Continuous Learning
The Future of Active Directory Security
===

\*\* 15. Active Directory Reconnaissance Mastery
Complete Guide to AD Enumeration, Footprinting, and Trust Mapping for Security Professionals

Imagine having complete visibility into your organization's Active Directory infrastructure—understanding every domain controller, trust relationship, and potential attack pathway before adversaries do. This comprehensive guide equips you with the knowledge and techniques to conduct thorough Active Directory reconnaissance, whether you're defending against attacks or testing security posture. You'll master passive information gathering through OSINT and public sources, execute network footprinting to identify AD services, and perform both unauthenticated and authenticated enumeration. Learn to leverage industry-standard tools like PowerView, BloodHound, and PowerUpSQL to automate complex reconnaissance tasks. Discover how to map trust relationships, identify misconfigurations in SCCM, Exchange, and AD CS, and uncover delegation rights that create lateral movement opportunities. This book bridges offensive and defensive perspectives, ensuring you understand reconnaissance from both attack and protection angles. Whether you're conducting authorized penetration tests or hardening your infrastructure, you'll gain practical, hands-on expertise in AD reconnaissance techniques that separate skilled security professionals from the rest.

Table of Contents
Introduction
Why Active Directory Reconnaissance Matters
How to Use This Book
Prerequisites and Assumptions
Chapter 1: Foundations of Active Directory Architecture
Understanding Domains, Trees, and Forests
Domain Controllers and Global Catalog Servers (GCS)
Trust Relationships and Domain Boundaries
Chapter 2: Passive Information Gathering and OSINT
Leveraging Public Sources and OSINT Tools
Analyzing Employee Data for Username Generation
DNS, WHOIS, and External Intelligence Gathering
Using Shodan and Public Repositories for Service Discovery
Chapter 3: Network Footprinting and Service Discovery
IPv6 Abuse and mitm6 DNS Spoofing
LLMNR, NBT-NS, and mDNS Poisoning Opportunities
Scanning for AD Services: LDAP, SMB, Kerberos, and DNS
SPN Scanning for Service Discovery Without Port Scanning
Chapter 4: Unauthenticated Enumeration Techniques
Anonymous LDAP Binds and Null Sessions
Enum4linux and RPClient User Enumeration
DNS Zone Transfer Enumeration
Identifying Password Policies and Account Lockout Thresholds
Chapter 5: Authenticated Enumeration with User Credentials
PowerView Fundamentals and Tips and Tricks
Mapping Users, Groups, and Nested Group Memberships
Enumerating Organizational Units (OUs) and User Attributes
Identifying Insecure ACLs and Object Ownership
Chapter 6: Advanced Enumeration and Kerberoasting
Querying LDAP for SPNs and Kerberoasting Targets
Enumeration Using Meterpreter ADSI Extended API Commands
Dumping AD Domain Information with PowerUpSQL
Enumeration Without Admin Rights and Privilege Escalation Paths
Chapter 7: AD Component Footprinting
Footprinting SCCM and Exchange Infrastructure
Enumerating AD CS Templates and Certificate Services
Mapping MSSQL Integrated Security and Trusted Links
Enumerating Domain Shares and SYSVOL
Chapter 8: Group Policy and Delegation Analysis
GPO Analysis and Misconfigurations
Analyzing AD Delegation Rights and Permissions
Identifying LAPS Usage and Local Admin Password Solutions
Identifying Read-Only Domain Controllers (RODCs) and Their Implications
Chapter 9: Trust Relationships and Multi-Domain Reconnaissance
Enumerating Inter-Domain and Forest Trust Relationships
Mapping Forests, Trees, and Domain Hierarchies
Domain Trust Discovery for Lateral Movement
Locating Active Directory Sites and Subnets
Chapter 10: BloodHound and Attack Pathway Visualization
BloodHound Fundamentals and Data Collection
Mapping AD Attack Pathways and Privilege Escalation Routes
Advanced BloodHound Queries and Analysis Techniques
Chapter 11: Evasion and OPSEC (Operational Security)
Avoiding Detection During Reconnaissance
Operational Security Best Practices
Understanding AD Logging and Monitoring Evasion
Detecting Reconnaissance Activities as a Defender
Chapter 12: Defensive Reconnaissance and Hardening
Applying Reconnaissance knowledge to Defense
Remediating Common Enumeration Vectors
Building Effective AD Monitoring and Detection Strategies
Conclusion
Key Takeaways and Next Steps
Continuing Your AD Security Journey
Appendix: Tools and Resources
Quick Reference Guide to AD Reconnaissance Tools
Common Commands and Syntax Reference
Further Reading and Additional Resources
===

Recon

Active Directory LDAP Reconnaissance Techniques
AD Domain Trust Discovery - Information Trust Gathering to Achieve Lateral Movement
AD Recon - Beyond Domain Admins - Domain Controller \& AD Administration
Active Directory Recon Without Admin Rights
AD Reconnaissance - Dumping AD Domain Infor with PowerUpSQL
AD Recon: Enumeration Using the Meterpreter ADSI Extended API Commands
AD Recon: PowerView Tips and Tricks
AD Recon: SPN Scanning: Service Discovery Without Network Port Scanning
AD Internal and Passive Reconnaissance Techniques and Evasion
Footprinting Foundational AD Structure \& Architecture
AD Recon: Mapping Forests, Trees, and Domains
AD Recon \& Footprinting: Identifying Domain Controllers (DCs) and Global Catalog Servers
AD Recon: Locating Active Directory Sites and Subnets
AD Recon: Identifying Read-Only Domain Controller (RODCs)
Passive Information Gathering: Gathering Information via External Sources (DNS/WHOIS)
Passive Information Gathering: Analyzing Publicly Available Employee Data for username Generation
Passive Information Gathering: Using OSINT and Shodan/Public Repositories/IoT for AD Service Endpoints (LDAP. SMB, RPC)
Active Directory Enumeration (No Creds/No Session): Checking for Anonymous LDAP Binds and Null Sessions
Active Directory Enumeration (No Creds/No Session): Enum4linux and RPClient User Enumeration
Active Directory Enumeration (No Creds/No Session): DNS Zone Transfer Enumeration
Active Directory Enumeration (No Creds/No Session): Identifying Password policies and Account Lockout Thresholds
Active Directory Enumeration (With User Credentials): Using PowerView for Dep Domain Object Enumeration
Active Directory Enumeration (With User Credentials): Mapping users, Groups, and Nested Group Memberships
Active Directory Enumeration (With User Credentials): Enumerating organizational Units (OUs) and User Attributes
Active Directory Enumeration (With User Credentials): Querying LDAP for SPNs for Kerberoasting
Active Directory Enumeration (With User Credentials): Identifying Insecure ACLs and Object Ownership
Active Directory Component Footprinting: GPO Analysis and Misconfigurations
Active Directory Component Footprinting: Enumerating Domain Shares and SYSVOL
Active Directory Component Footprinting: Mapping Microsoft SQL Server (MSSQL) Integrated Security and Trusted Links
Active Directory Component Footprinting: Enumerating AD CS Templates
Active Directory Component Footprinting: Footprinting SCCM and Exchange Infrastructure
AD Trust and Advanced Mapping Techniques: Enumerating inter-Domain and Forest Trust Relationships
AD Trust and Advanced Mapping Techniques: Mapping AD Attack pathways with BloodHound
AD Trust and Advanced Mapping Techniques: Identifying LAPS Usage
AD Trust and Advanced Mapping Techniques: Analyzing AD Delegation Rights
AD Network and Service Footprinting: Scanning for AD Services (LDAP/389, SMB/445, Kerberos/88. DNS/53)
AD Network and Service Footprinting: Detecting LLMNR/NBT-NS/mDNS Poisoning Opportunities
AD Network and Service Footprinting: IPv6 and mitm6 DNS Spoofing Recognition
===

AD CS Attacks

ESC1 (Misconfigured Template-SAN)
ESC2 (Weak Template EKU)
ESC3 (Enrollment Agent Misuse)
ESC4 (Vulnerable Template ACLs)
ESC5 (Vulnerable PKI Object Access)
ESC7 (Vulnerable CA ACLs)
ESC8 (NTLM Relay to AD CS)
PetitPotam (NTLM Relay)
Certipy/Certify Exploitation
Golden CA Certificate Forgery
Pass-the-Certificate
DPAPI Certificate Theft
APT29
===

\*\* Chapter x; Pass-the-Hash (PtH) Mastery
The Complete Guide to NTLM Exploitation, Defense, and Lateral Movement in Active Directory

Imagine having complete mastery over NTLM authentication vulnerabilities - understanding not just how Pass-the-Hash (PtH) attacks work, but why they succeed where traditional security controls fail. This tactical guide will equip you with the technical depth needed to exploit, defend, and ultimately secure Active Directory (AD) environments against one of the most persistent threats that plague modern-day enterprise networks. You will progress from foundational NTLM mechanics and credential storage principles through advanced lateral movement techniques, learning how attackers acquire hashes from memory, disk, and network sources. Discover how to leverage BloodHound and permission auditing to identify high-value targets, then master the technical implementation of Pass-the-Hash across SMB, WinRM, RPC, and other protocols. The book aims to bridge offensive and defensive perspectives, covering exploitation frameworks like Mimikatz and Impacket alongside detection strategies and EDR evasion techniques. You will explore constrained delegation abuse, multi-forest pivoting, and custom automation workflows while understanding the defensive countermeasures that actually work. Whether you are conducting penetration tests or hardening infrastructure, this guide provides the technical rationale and practical tools to stay ahead of evolving threats.



Introduction
Why Pass-the-Hash (PtH) Remains Critical in Modern Security Architecture
How This Book Is Organized
Balancing Offensive Understanding with Defensive Strategy
Chapter 1: NTLM Authentication Fundamentals
Historical Context and Protocol Evolution from NTLMv1 to NTLMv2
Challenge-Response Mechanics and Cryptographic Principles
Credential Storage Mechanisms and Hash Generation
Chapter 2: Pass-the-Hash Principles and Attack Surface
Core Pass-the-Hash Concepts and Why It Bypasses Password Policies
Service and User Account Behaviors That Enable Hash Persistence
Common Misconfigurations That Amplify Risk
Chapter 3 - Reconnaissance and Target Identification
Using BloodHound for hash Reuse Enumeration
Permissions Auditing and Account Identification
Identifying Prerequisite Permissions for Exploitation
Chapter 4: Hash Acquisition Techniques
LSASS Memory Dumping and Extraction Methods
Disk-Based Credential Artifacts and Recovery
DPAPI Interaction and Decryption Workflows
Chapter 5: Pass-the-Hash Exploitation Mechanics
Injecting NTLM Hashes Into Authentication Contexts
Remote Execution Vectors: SMB, WinRM, RPC, and WMI
Impact of LMCompatibilityLevel and NTLM Restrictions
Chapter 6: Offensive Tools and Frameworks
Mimikatz and In-Memory Hash Injection
PowerShell-Based Modules and Invoke-PassTheHash
Cross-Platform Impacket Tools: wmiexec.py and psexec.py
Chapter 7: Advanced Exploitation Frameworks
Empire, Cobalt Strike, and PowerSploit Integration
Custom Script Development and Automated Workflows
BloodHound and PowerView Integration for Targeting
Chapter 8: Lateral Movement and Pivoting
Lateral Movement Across Multi-Domain Environments
Pivoting Across Forest Boundaries and Trust Relationships
Pass-the-Hash in Hybrid and Cloud-Connected AD
Chapter 9: Advanced Evasion and Detection Bypass
Evasion of Native Logging and EDR Detection
Mitigation Controls and Configuration Hardening
Building a Comprehensive Monitoring Framework
Conclusion
The Evolving Threat Landscape





Introduction to NTLM and Pass-the-Hash (PtH) Principles
Historical Context and Protocol Specifications in NTLMv1/v2
Challenge-Response Mechanics
Credential Storage Mechanisms
Service and User Account Behaviors That Enable Hash Persistence
Common Misconfiguration
Technical Rationale for Balancing Offensive Security Understanding
Enumeration Opportunities for Hash Reuse in the Target Environment
Identification of Accounts
Prerequisite Permissions Required
Using BloodHound
Permissions Auditing
Offensive Perspective - Exploiting Pass-the-hash Techniques
Technical Mechanics of Pass-the-Hash
Hash Acquisition From Memory, Disk, or Network - LSASS Dumping and DPAPI Interaction
Injection NTLM Hashes Into Authentication Contexts Without Password Knowledge
Remote Execution Vectors - SMB, SMI, WinRM, and RPC with Passed Hashes
Impact of Legacy Compatibility Settings - LMCompatibilityLevel, NTLM Restrictions- on Technique Visibility
Technical Rationale for Why Pass-the-Hash Bypasses Password-Policy Controls Entirely
Tools and Techniques for PtH Misconfigurations
In-Memory Frameworks - Mimikatz and Overpass-the-Hash
PowerShell-Based Modules - Invoke-PassTheHash, PowerSploit - Empire and Cobalt Strike Integration
Cross-Platform Implementations Using the Impacket Tool Suite - wmiexec.py and psexec.py with Hashes
Custom Script Development - PowerShell and Python Snippets for Automated Pass-the-Hash Workflows
Integration with BloodHound and PowerView for Prioritizing Vulnerable Objects with Confirmed Local Admin Rights
Advanced Exploitation Scenarios and Evasion Techniques
Pass-the-Hash in Constrained or Resource-Based Delegation Chains
Lateral Movement and Pivoting Across Multi-Domain, Multi-Forest, and Hybrid AD Environments
Evasion of Native Logging and Modern EDR During Hash Injections
Combining Pass-the-Hash with Complementary Credential Techniques
Technical Rational for Why These Variant Remain

===============================================================================================================



\# Master of Your Domain: Hacking and Defending Active Directory



\## Complete Table of Contents



\---



\## \*\*Foreword: The Ethical Hacker's Responsibility\*\*



\## \*\*Preface: How to Use This Book\*\*



\- Prerequisites and Required Knowledge

\- Lab Environment Setup Requirements

\- Learning Path Recommendations

\- Companion Resources and Tools



\---



\## \*\*Part I: Foundations (Day 1)\*\*



\### \*\*Chapter 1: Understanding the Active Directory Ecosystem\*\*



\#### 1.1 What is Active Directory and Why It Matters



\- 1.1.1 The Business Case for Active Directory - Active Directory (AD) provides a compelling business case by centralizing identity management, enhancing security through controlled access, and reducing IT operational costs. It streamlines administration for users, devices, and applications while enabling compliance, making it critical for efficient network security, user management, and employment productivity.

\- Key Business Benefits of Active Directory

&#x09;- Centralized Administration \& Reduced Costs: IT teams can manage users, computers, and security policies from a single, central location, significantly reducing manual administration time and associated costs.

&#x09;- Enhanced Security \& Compliance: AD allows for the enforcement of strict security policies, such as password requirements and access controls, protecting sensitive data and aiding in compliance with regulatory standards like HIPAA or PCI DSS.

&#x09;- Improved User Productivity (SSO): Users benefit from Single Sign-On (SSO) allowing them to access multiple, authorized network resources with one set of credentials, minimizing issues.

&#x09;- Scalability \& Flexibility: As businesses grow, AD easily adapts, allowing for the quick addition or removal of users, devices, and resources, providing a scalable IT infrastructure.

&#x09;- Secure Resource Management: Administrators can easily manage access to shared drives, printers, and applications based on user roles and groups.

\- Active Directory acts as the foundation for identity and access control, ensuring only authorized users have access to critical data and preventing unauthorized access.

\- 1.1.2 AD in Modern Enterprise Infrastructure - In modern enterprise infrastructure, Active Directory (AD) functions as the foundational identity and access management (IAM) service, acting as a centralized "phone book" and security authority for managing users, computers, and resources. While its traditional, on-premises form persists in over 90% of enterprises, the modern iteration is heavily integrated with cloud-based solutions - namely Microsoft Entra ID (formerly Azure AD) - to support hybrid workforces and modern security standards like Zero Trust.

\- Key Aspects of AD in Modern Infrastructure:

&#x09;- Hybrid Identity Center: Modern AD rarely operates in isolation. Through tools like Azure AD Connect, on-premises AD synchronizes with Entra ID, creating a hybrid environment where on-prem systems (legacy apps, servers), and cloud resources (Microsoft 365, SaaS apps) share the same identity credentials.

&#x09;- Core Authentication/Authorization: It manages authentication (verifying who you are via Kerberos/NTLM) and authorization (what you can access) for Windows-based networks.

&#x09;- Group Policy Object (GPO) Management: AD allows administrators to configure security policies, software updates, and user configurations centrally across the entire organization

&#x09;- High-Value Security Target: Because it holds the "keys to the kingdom," AD is a primary target for cyberattacks. Consequently, modern AD management prioritizes hardening, such as implementing the "Tier 0" model to isolate domain controllers, using Privileged Access Workstations (PAWs) and enforcing Multi-Factor Authentication (MFA).

&#x09;- \*\*Evolution Toward "Zero Trust:\*\* While legacy AD was built for a secure, perimeter-based network, modern AD is being adapted to support Zero Trust principles, where no user or device is trusted implicitly, regardless of location.

\- \*\*Key Components in a Modern AD Infrastructure\*\*

&#x09;- \*\*Active Directory Domain Services (AD DS):\*\* The core database storing network objects.

&#x09;- \*\*Domain Controllers (DCs):\*\* Servers that handle authentication and policy enforcement.

&#x09;- \*\*Microsoft Entra ID (Cloud):\*\* Manages cloud-based authentication and SaaS operations.

&#x09;- \*\*AD Certificate Services (AD CS):\*\* Manages Public Key Infrastructure (PKI) for security.

\- Despite the rise of cloud-only solutions, traditional AD remains deeply entrenched due to its reliance on legacy applications, making its modernization and security a critical component of modern IT and ethical hacking strategy.

\- 1.1.3 Cloud Integration: Azure AD and Hybrid Environments - Azure AD and Hybrid Environments (now referred to as Microsoft Entra ID) refers to the strategic, technical and architectural process of connecting on-premises IT infrastructure (Active Directory Domain Services) with Microsoft's cloud services (Entra ID/Azure AD). This approach enables organizations to transition to the cloud while leveraging existing, on-premises investments.

\- This integration creates a hybrid identity model, allowing users to sign in to both local and cloud resources using a single, consistent set of credentials.

\- Key Components of Cloud Integration

&#x09;- Hybrid Identity: Unifying on-premises Active Direcotry and cloud-based Entra ID for a seamless auhentication experience.

&#x09;- Microsoft Entra Connect (formerly Azure AD Connect): The essential tool used to synchronize users, groups and identities from on-premises AD to the cloud.

&#x09;- Hybrid Azure AD Join: A method where devices are joined to on-premises AD and registered with Entra ID, enabling Group Policy enforcement while allowing access to cloud-based resources.

&#x09;- Single Sign-On (SSO): Enables users to use one set of credentials for both on-premises applications and SaaS apps in the cloud, increasing productivity and security.



\#### 1.2 Core Components and Architecture



\- 1.2.1 Domain Controllers and Their Role

\- 1.2.2 Forests, Trees, and Domains Explained

\- 1.2.3 Organizational Units (OUs) Structure

\- 1.2.4 Sites and Replication Topology

\- 1.2.5 Global Catalog and FSMO Roles



\#### 1.3 Active Directory Objects and Schema



\- 1.3.1 Users, Computers, and Groups

\- 1.3.2 Service Accounts and Managed Service Accounts

\- 1.3.3 Group Policy Objects (GPOs)

\- 1.3.4 Schema Extensions and Custom Attributes



\### \*\*Chapter 2: Essential Information Security Concepts for AD\*\*



\#### 2.1 The CIA Triad in Active Directory Context



\- 2.1.1 Confidentiality: Protecting Sensitive Directory Data

\- 2.1.2 Integrity: Ensuring Trust in Authentication

\- 2.1.3 Availability: Maintaining Directory Services



\#### 2.2 Authentication vs. Authorization



\- 2.2.1 Kerberos Protocol Deep Dive

\- 2.2.2 NTLM: Legacy but Persistent

\- 2.2.3 LDAP Authentication Mechanisms

\- 2.2.4 Modern Authentication: SAML, OAuth, and AD FS



\#### 2.3 Defense in Depth Strategy



\- 2.3.1 Network Segmentation for AD Protection

\- 2.3.2 Principle of Least Privilege

\- 2.3.3 Zero Trust and Active Directory

\- 2.3.4 Monitoring and Detection Layers



\### \*\*Chapter 3: Network Security Fundamentals for AD Environments\*\*



\#### 3.1 Critical Network Protocols in AD



\- 3.1.1 DNS and Its Crucial Role in AD

\- 3.1.2 LDAP and LDAPS Communication

\- 3.1.3 SMB/CIFS for File Sharing

\- 3.1.4 RPC and Dynamic Port Allocation

\- 3.1.5 Kerberos Network Traffic Analysis



\#### 3.2 Network Security Controls



\- 3.2.1 Firewall Rules for Domain Controllers

\- 3.2.2 Network Access Control (NAC) Integration

\- 3.2.3 VLANs and AD Traffic Isolation

\- 3.2.4 IPSec for Domain Controller Communication



\#### 3.3 Common Network Attack Vectors



\- 3.3.1 Man-in-the-Middle Attacks on AD Traffic

\- 3.3.2 DNS Poisoning and Hijacking

\- 3.3.3 Broadcast Protocol Exploitation

\- 3.3.4 IPv6 Attack Vectors in AD



\---



\## \*\*Part II: Reconnaissance and Enumeration (Day 2)\*\*



\### \*\*Chapter 4: Passive and Active Information Gathering\*\*



\#### 4.1 OSINT for Active Directory



\- 4.1.1 LinkedIn and Organizational Mapping

\- 4.1.2 Email Harvesting and Username Formats

\- 4.1.3 DNS Reconnaissance Techniques

\- 4.1.4 Certificate Transparency Logs



\#### 4.2 Network Scanning and Discovery



\- 4.2.1 Using Nmap for AD Infrastructure Mapping

\- 4.2.2 Identifying Domain Controllers

\- 4.2.3 Service Discovery and Fingerprinting

\- 4.2.4 Avoiding Detection During Scanning



\#### 4.3 Initial Access Techniques



\- 4.3.1 Password Spraying Strategies

\- 4.3.2 Username Enumeration Methods

\- 4.3.3 Null Session Enumeration

\- 4.3.4 LDAP Anonymous Binds



\### \*\*Chapter 5: Advanced AD Enumeration\*\*



\#### 5.1 Authenticated Enumeration Tools



\- 5.1.1 BloodHound: Mapping Attack Paths

\- 5.1.2 PowerView and PowerShell Empire

\- 5.1.3 ADExplorer and Native Tools

\- 5.1.4 SharpHound Collection Methods



\#### 5.2 Enumerating Critical Information



\- 5.2.1 User and Computer Object Properties

\- 5.2.2 Group Memberships and Nested Groups

\- 5.2.3 Trust Relationships Mapping

\- 5.2.4 GPO Settings and Misconfigurations

\- 5.2.5 Service Principal Names (SPNs)



\#### 5.3 Defensive Enumeration Detection



\- 5.3.1 Honeypot Accounts and Honeytoken

\- 5.3.2 Monitoring LDAP Queries

\- 5.3.3 Detecting BloodHound Activity

\- 5.3.4 Advanced Audit Policies



\---



\## \*\*Part III: Initial Compromise and Lateral Movement (Day 3-4)\*\*



\### \*\*Chapter 6: Common Attack Vectors and Initial Compromise\*\*



\#### 6.1 Credential-Based Attacks



\- 6.1.1 Password Spraying Implementation

\- 6.1.2 Credential Stuffing Techniques

\- 6.1.3 Kerberoasting: From SPN to Credentials

\- 6.1.4 AS-REP Roasting Vulnerable Accounts



\#### 6.2 Relay Attacks



\- 6.2.1 LLMNR/NBT-NS Poisoning

\- 6.2.2 SMB Relay Attack Chains

\- 6.2.3 LDAP Relay and Resource-Based Constrained Delegation

\- 6.2.4 WebDAV and HTTP to LDAP Relay



\#### 6.3 Exploiting Misconfigurations



\- 6.3.1 Weak GPO Permissions

\- 6.3.2 Unconstrained Delegation Abuse

\- 6.3.3 Print Spooler Service Exploitation

\- 6.3.4 SYSVOL and GPP Password Exposure



\### \*\*Chapter 7: Lateral Movement Techniques\*\*



\#### 7.1 Traditional Lateral Movement



\- 7.1.1 Pass-the-Hash (PtH) Attacks

\- 7.1.2 Pass-the-Ticket (PtT) Techniques

\- 7.1.3 Overpass-the-Hash/Pass-the-Key

\- 7.1.4 Token Impersonation Methods



\#### 7.2 Living Off the Land



\- 7.2.1 WMI for Remote Execution

\- 7.2.2 PowerShell Remoting Techniques

\- 7.2.3 Scheduled Tasks and At Jobs

\- 7.2.4 Service Creation and Modification



\#### 7.3 Advanced Persistence Mechanisms



\- 7.3.1 Golden Ticket Creation and Usage

\- 7.3.2 Silver Ticket Attacks

\- 7.3.3 Skeleton Key Implants

\- 7.3.4 AdminSDHolder Modification

\- 7.3.5 SID History Injection



\### \*\*Chapter 8: Defensive Strategies Against Lateral Movement\*\*



\#### 8.1 Credential Protection



\- 8.1.1 Credential Guard Implementation

\- 8.1.2 Protected Users Security Group

\- 8.1.3 LAPS Deployment and Management

\- 8.1.4 Kerberos Armoring (FAST)



\#### 8.2 Network Segmentation Strategies



\- 8.2.1 Tiered Administrative Model

\- 8.2.2 Privileged Access Workstations (PAWs)

\- 8.2.3 Authentication Silos and Policies

\- 8.2.4 Selective Authentication in Trusts



\#### 8.3 Detection and Response



\- 8.3.1 Honey Credentials and Deception

\- 8.3.2 Advanced Threat Analytics (ATA)

\- 8.3.3 Windows Event Log Analysis

\- 8.3.4 Network Traffic Analysis for Anomalies



\---



\## \*\*Part IV: Privilege Escalation and Persistence (Day 5)\*\*



\### \*\*Chapter 9: Privilege Escalation in Active Directory\*\*



\#### 9.1 Local Privilege Escalation



\- 9.1.1 Unquoted Service Paths - Unquoted service paths constitute a well-known Local Privilege Escalation (LPE) vulnerablity on Windows systems, often relevant in Active Directory environments when a low=privileged user gains a foothold on a workstation or server. The vulnerability arises hen a service's executable path contains spaces and is not enclosed in quotation marks, allowing Windows to incorrectly interpret the path and execute a malicious binary instead of the intended service.

\- The Technical Mechanism

&#x09;- When the Widows Service Control Manager (SCM) attempts to run a service with a path like `C:\\\\Program Files\\\\Vendor App\\\\Service.exe`

&#x09;	- 1. `C:\\\\Program.exe`

&#x09;	- 2. `C:\\\\Program Files\\\\Vendor.exe`

&#x09;	- 3. `C:\\\\Program Files\\\\Vendor App\\\\Service.exe`

&#x09;- If an attacker has write permissions to any of the intermediate directories (e.g., `C:\\\\`), they can place a malicious executable named `Program.exe` there. When the service starts (typically at boot or upon a service restart), Windows will execute the malicious file instead, usually with `NT AUTHRORITY\\\\SYSTEM` privileges.

\- Exploitation Flow in Active Directory

&#x09;- In an AD environment, this attack is typically executed after gaining initial access via phishing or other means:

&#x09;	1. Enumeration: Attacker use tools like `PowerUp.ps1` (`Invoke-AllChecks`) or `wmic` to find services with unquoted paths.

&#x09;	2. Permission Check: The attacker verifies they have write access to the directory where the malicious executable will be dropped (e.g., using `icacls`).

&#x09;	3. Payload Generation \& Delivery: A malicious `.exe` is generated (e.g., using `msfvenom`) and moved to the vulnerable path.

&#x09;	4. Execution: The attacker forces a service restart, or waits for a system reboot, to trigger the payload.

\* Mitigation and Prevention

&#x09;\* The primary fix is to ensure all service paths containing spaces are wrapped in quotes within the Windows Registry.

&#x09;	\* Fixing via Registry: Navigate to `HKLM\\\\SYSTEM\\\\CurrentControlSet\\\\Services`, locate the service, and modify the `ImagePath` key to add quotes (e.g., `"C:\\\\Program Files\\\\Vendo App\\\\Service.exe"`).

&#x09;	\* Securing Permissions: Ensure that standard user accounts do not have write permissions to directories under `C:\\\\Program Files` or the root of `C:\\\\`.

&#x09;	\* Audit and Monitor: Use Group Policy Objects (GPOs) to push configurations that correct these paths or deploy scripts to monitor for new, insecure service installations.

\- 9.1.2 DLL Hijacking Opportunities

\- 9.1.3 Registry Autoruns Abuse

\- 9.1.4 Scheduled Task Manipulation



\#### 9.2 Domain Privilege Escalation



\- 9.2.1 ACL Abuse and Privilege Chains

\- 9.2.2 DNSAdmins Group Exploitation

\- 9.2.3 Exchange Privilege Escalation

\- 9.2.4 Certificate Template Misconfigurations



\#### 9.3 Forest and Trust Escalation



\- 9.3.1 Foreign Security Principal Abuse

\- 9.3.2 Trust Ticket Attacks

\- 9.3.3 PAM Trust Exploitation

\- 9.3.4 Azure AD Connect Abuse



\### \*\*Chapter 10: Advanced Persistence Techniques\*\*



\#### 10.1 Backdoor Accounts and Groups



\- 10.1.1 Hidden Administrative Accounts

\- 10.1.2 Shadow Security Principals

\- 10.1.3 Nested Group Backdoors

\- 10.1.4 Computer Account Takeover



\#### 10.2 System-Level Persistence



\- 10.2.1 DCShadow Attacks

\- 10.2.2 Custom SSP Installation

\- 10.2.3 Malicious Domain Controller

\- 10.2.4 Forest Trust Abuse



\#### 10.3 Application-Level Persistence



\- 10.3.1 Outlook Rules and Forms

\- 10.3.2 Office 365 Application Consent

\- 10.3.3 Federation Trust Manipulation

\- 10.3.4 ADFS Backdoors



\---



\## \*\*Part V: Defense, Detection, and Response (Day 6)\*\*



\### \*\*Chapter 11: Hardening Active Directory\*\*



\#### 11.1 Baseline Security Configuration



\- 11.1.1 Security Baselines and Benchmarks

\- 11.1.2 Group Policy Hardening

\- 11.1.3 Administrative Template Settings

\- 11.1.4 Security Options Configuration



\#### 11.2 Advanced Hardening Techniques



\- 11.2.1 RID Randomization

\- 11.2.2 SID Filtering Configuration

\- 11.2.3 Selective Authentication

\- 11.2.4 Authentication Policy Silos



\#### 11.3 Patch Management and Updates



\- 11.3.1 Critical AD Security Updates

\- 11.3.2 WSUS Integration

\- 11.3.3 Emergency Patching Procedures

\- 11.3.4 Testing and Rollback Strategies



\### \*\*Chapter 12: Monitoring and Threat Detection\*\*



\#### 12.1 Log Collection and Analysis



\- 12.1.1 Essential Windows Event IDs

\- 12.1.2 Sysmon for Enhanced Visibility

\- 12.1.3 PowerShell Logging Configuration

\- 12.1.4 Centralized Log Management



\#### 12.2 SIEM Integration and Correlation



\- 12.2.1 Detection Use Cases for AD

\- 12.2.2 Correlation Rules Development

\- 12.2.3 Threat Intelligence Integration

\- 12.2.4 Automated Response Playbooks



\#### 12.3 Threat Hunting in AD



\- 12.3.1 Hunting for Golden Tickets

\- 12.3.2 Detecting Kerberoasting Activity

\- 12.3.3 Anomalous Authentication Patterns

\- 12.3.4 Behavioral Analytics Implementation



\### \*\*Chapter 13: Incident Response and Recovery\*\*



\#### 13.1 Incident Response Planning



\- 13.1.1 AD-Specific IR Procedures

\- 13.1.2 Evidence Collection Methods

\- 13.1.3 Containment Strategies

\- 13.1.4 Communication Protocols



\#### 13.2 Compromise Recovery



\- 13.2.1 Determining Compromise Scope

\- 13.2.2 Evicting Advanced Attackers

\- 13.2.3 Credential Reset Procedures

\- 13.2.4 Trust Relationship Recovery



\#### 13.3 Forest Recovery Operations



\- 13.3.1 Forest Recovery Planning

\- 13.3.2 Backup and Restore Strategies

\- 13.3.3 Authoritative Restore Procedures

\- 13.3.4 Post-Recovery Validation



\---



\## \*\*Part VI: Advanced Topics and Real-World Scenarios (Day 7)\*\*



\### \*\*Chapter 14: Cloud and Hybrid Environments\*\*



\#### 14.1 Azure AD Integration Security



\- 14.1.1 Azure AD Connect Security

\- 14.1.2 Pass-through Authentication Risks

\- 14.1.3 Password Hash Sync Considerations

\- 14.1.4 Federation Security Best Practices



\#### 14.2 Cloud-Specific Attack Vectors



\- 14.2.1 Token Theft and Replay

\- 14.2.2 Consent Phishing Attacks

\- 14.2.3 Cloud Privilege Escalation

\- 14.2.4 Multi-Factor Authentication Bypass



\#### 14.3 Securing Hybrid Deployments



\- 14.3.1 Conditional Access Policies

\- 14.3.2 Identity Protection Features

\- 14.3.3 Privileged Identity Management

\- 14.3.4 Cloud App Security Integration



\### \*\*Chapter 15: Real-World Attack Simulations\*\*



\#### 15.1 Purple Team Exercises



\- 15.1.1 Exercise Planning and Scoping

\- 15.1.2 Attack Scenario Development

\- 15.1.3 Detection Capability Testing

\- 15.1.4 Metrics and Improvement Tracking



\#### 15.2 Complete Attack Chain Walkthroughs



\- 15.2.1 APT-Style Long-Term Compromise

\- 15.2.2 Ransomware Attack Simulation

\- 15.2.3 Insider Threat Scenarios

\- 15.2.4 Supply Chain Compromise



\#### 15.3 Defensive Scenario Exercises



\- 15.3.1 Incident Detection Challenge

\- 15.3.2 Forensics and Attribution

\- 15.3.3 Recovery Time Objectives

\- 15.3.4 Lessons Learned Documentation



\### \*\*Chapter 16: Compliance and Best Practices\*\*



\#### 16.1 Regulatory Requirements



\- 16.1.1 GDPR and Data Protection

\- 16.1.2 HIPAA Compliance for Healthcare

\- 16.1.3 PCI-DSS for Payment Systems

\- 16.1.4 SOX Compliance Requirements



\#### 16.2 Security Frameworks



\- 16.2.1 NIST Cybersecurity Framework

\- 16.2.2 CIS Controls for AD

\- 16.2.3 MITRE ATT\&CK Mapping

\- 16.2.4 Zero Trust Architecture



\#### 16.3 Continuous Improvement



\- 16.3.1 Security Metrics and KPIs

\- 16.3.2 Vulnerability Management Programs

\- 16.3.3 Security Awareness Training

\- 16.3.4 Third-Party Security Assessments



\---



\## \*\*Appendices\*\*



\### \*\*Appendix A: Lab Environment Setup\*\*



\- A.1 Virtual Machine Requirements

\- A.2 Building a Test Domain

\- A.3 Vulnerable Configuration Setup

\- A.4 Tool Installation Guide



\### \*\*Appendix B: Essential Tools Reference\*\*



\- B.1 Offensive Security Tools

\- B.2 Defensive and Monitoring Tools

\- B.3 PowerShell Scripts and Modules

\- B.4 Open Source vs. Commercial Tools



\### \*\*Appendix C: Quick Reference Guides\*\*



\- C.1 Common Port Numbers

\- C.2 Critical Event IDs

\- C.3 PowerShell Commands Cheat Sheet

\- C.4 Mimikatz Command Reference



\### \*\*Appendix D: Security Checklist Templates\*\*



\- D.1 Domain Controller Security Checklist

\- D.2 Post-Compromise Checklist

\- D.3 Audit and Compliance Checklist

\- D.4 Incident Response Checklist



\### \*\*Appendix E: Additional Resources\*\*



\- E.1 Recommended Reading

\- E.2 Online Training Platforms

\- E.3 Community Forums and Support

\- E.4 Security Research Papers



\---



\## \*\*Glossary of Terms\*\*



\## \*\*Index\*\*



\## \*\*About the Author\*\*

===============================================================================================================



Master of Your Domain: Book Table of Contents



\## Part I: The Foundation \& The Author's Journey



Preface: The Identity Battlefield

\* \*\*Philosophy\*\*: "To defend it, you must first know how to destroy it.

\* \*\*Identity as the New Perimeter:\*\* Why the Firewall is no longer enough.

\* \*\*The Author's Voice:\*\* From the 17 years in the DoD NetSecOps trenches.



```table-of-contents

```

```table-of-contents

title: 

style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)

minLevel: h1 # Include headings from the specified level

maxLevel: h5 # Include headings up to the specified level

include: 

exclude: 

includeLinks: true # Make headings clickable

hideWhenEmpty: false # Hide TOC if no headings are found

debugInConsole: false # Print debug info in Obsidian console

```

<h4>Chapter 1: The Architecture of Trust</h4>





/table



&#x20;<h5>1.1 The Identity Evolution: From Novell NDS to Active Directory</h5>

&#x20;<h5>1.2 The Forest, The Tree, and The Domain: Understanding the True Security Boundaries</h5>

&#x20;<h5>1.3 The Language of Identity: Kerberos (Tickets) vs. NTLM (Challenge-Response).</h5>

&#x20;<h5>1.4 The Crown Jewel: The <code>ntds.dit</code> and the JET Database Engine</h5>

<h5> 1.5 FSMO Roles: Identifying the "Boss" Domain Controllers.</h5>

===============================================================================================================



\\documentclass{article}

\\usepackage{blindtext}

\\usepackage{titlesec}

\\title{Sections and Chapters}

\\author{Gubert Farnsworth}

\\date{ }

\\begin{document}



\\maketitle



\\tableofcontents



\\section{Part I-Foundations of Active Directory (AD) Security}



What This Book Will Teach You (and What It Will Not)

Offensive vs. Defensive Lenses in AD Security

Why AD Continues to Remain Vulnerable

AD Crown Jewels-An Attractive Target for Attackers

Ethical and Legal Considerations for Hacking Active Directory Environments



\\subsection{Core Networking and Security Concepts for AD Environments}

Networking 101: How Data Moves

TCP/IP: IP Addressing, Subnets, and Routing Basics

Common Network and AD-Related Protocols: SMB, LDAP, Kerberos, DNS, RPC, RDP

Packet Flow in AD Authentication



\\subsection{Active Directory Architecture}

Domains, Trees, and Forests

Organizational Units (OUs) and Group Policy Objects (GPOs)

Security Principles: Users, Groups, Computers, Service Accounts

AD Relationships and Trusts: Internal and External Attack Surfaces



\\subsection{Identity, Authentication, and Authorization in Active Directory}

Kerberos Authentication Deep Dive

NTLM and Legacy Protocols

Access Control Lists (ACLs) and Security Descriptors

Privilege Models and AD Tiers (Tier 0, 1, 2)



\\subsection{Regulatory and Compliance Drivers in AD Security}

NIST, CIS, ISO, and Microsoft Baselines

Common Enterprise AD Compliance Requirements

How Compliance Affects Offensive and Defensive Operations



\\section{Part II-Offensive Security: Attacking Active Directory}



\\subsection{The AD Attack Surface}

Mapping Attack Entry Points

Common Misconfigurations

The Role of Shadow IT in AD Risk



\\subsection{Reconnaissance and Enumeration}

Passive Recon with OSINT

Internal AD Enumeration:

LDAP, PowerView, BloodHound

Mapping Trusts and Privilege Escalation Pathways



\\subsection{Credential Access and Abuse}

Credential Dumping

LSASS

SAM

\\subsubsection{\\texttt{NTDS.dit}}

Pass-the-Hash (PtH)

Pass-the-Ticket (PtT)

Overpass-the-Hash

Harvesting and Reusing Kerberos Tickets



\\subsection{Privilege Escalation in AD}

Exploiting Delegation

Unconstrained Delegation

Constrained Delegation

Resource-based Constrained Delegation (RBCD)

Abusing Service Principal Names (SPNs)

Kerberoasting

Exploiting Weak ACLs and GPO Permissions



\\subsection{Persistence Techniques}

Golden and Silver Tickets

Skeleton Keys and Security Support Provider (SSP) Injection

DCShadow Attack

Abusing \\texttt{AdminSDHolder}

SIDHistory Abuse



\\subsection{Lateral Movement}

Pass-the-Hash / Ticket Techniques

Remote Service Exploitation

\\subsubsection{WMI: (Windows Management Instrumentation}

\\subsubsection{Sysinternals \\texttt{PsExec}}

WRM: (Windows Remote Management)

Credential Relay Attacks

NTLM Relay Attack



\\subsection{AD Attacks in Hybrid Environments}

Azure AD and On-Prem Sync Abuse

OAuth Token Theft and Cloud-Based Persistence

Cross-Tenant and Cross-Forest Exploitation



\\section{Part III-Defensive Security: Protecting Active Directory}

\\subsection{Building an AD Defense Strategy}



Adopting and Establishing Zero Trust in Active Directory

The Tiered Administration Model

The Principle of Least Privilege (PoLP) and Just-in-Time (JIT) Access



\\subsection{Hardening Authentication}

Enforcing Kerberos Pre-Auth and Disabling NTLM

MFA for AD Accounts

Securing Service Accounts and SPNs



\\subsection{Group Policy and OU Security}

Locking Down GPO Permissions

GPO Attack Detection and Prevention

Securing OU Structure Against Misuse



\\subsection{Monitoring and Detection}

Event Logging for Defenders

SIEM Integration and Use Cases



\\subsection{Detecting Common AD Attacks}

DCSync

DCShadow

AS-REP Roasting

LLMNR and NBT-NS



\\subsection{Incident Response (IR) in AD Breaches}

Containment and Eradication Procedures

Putting Out Forest Fires: DC Reinstallation and Forest Recovery

Post-Incident Hardening



\\subsection{Threat Hunting in AD}

Threat Hunting Methodologies

Using BloodHound for Defensive Strategies

Canary Objects and Decoy Accounts



\\subsection{Defending Against Hybrid AD Attacks}

Azure AD Conditional Access Policies

Securing Azure AD Connect

Cloud and On-Prem Identity Threat Detection



\\section{Part IV-Advanced Scenarios and Case Studies}

\\subsection{Full Kill Chain Walkthrough: From Initial Toehold to Domain Admin (DA)}



Step-by-Step Red Team Attack Simulation

Blue Team Detection and Mitigation at Each Stage



\\subsection{Case Study: Real-World AD Breach Analysis}

How the Attack Unfolded

Missed Defensive Opportunities

Lessons Learned and Preventative Measures



\\subsection{Designing and Secure AD From the Ground Up}

Defender Security Best Practices

Secure Build Standards and Templates

Long-Term Maintenance Strategy



\\subsection{Initial Access and Active Directory Exploitation}

\\begin{itemize}

    \\item Exploit unpatched, uncovered vulnerabilities to gain initial access

    \\item Perform application allowlisting attack for executing malicious scripts inside the domain structure

    \\item Set up an in-house Active Directory simulated environment and gain offensive and defensive learning by simulating APT TTPs and mapping attacker TTPs to their respective security framework

    \\item Other Topics to be Covered:

        \\begin{itemize}

            \\item Lab Setup

        \\end{itemize}

        \\begin{itemize}

            \\item     Abusing Server Message Block (SMB)

        \\end{itemize}

        \\begin{itemize}

            \\item SMB DLL Delivery

        \\end{itemize}

        \\begin{itemize}

            \\item LLMNR Poisoning Attack

        \\end{itemize}

        \\begin{itemize}

            \\item Capturing NTLMv2 Hashes

        \\end{itemize}

\\end{itemize}



\\subsection{Active Directory Enumeration}

Perform domain reconnaissance on domain entities such as domains, users, groups, ACLs, OYs. Forests, Trust Relationships, GPOs and GPPs using Microsoft built-in utilities

Hunt and map Active Directory resources using PowerShell enumeration scripts, and the tools BloodHound, and RPCClient

Seek out hidden Domain Admin and Administrator accounts to use for privilege escalation, lateral movement, and persistence.



\\subsection{Post-Enumeration Activities in Active Directory}

RPCClient

BloodHound

PowerView



\\subsection{Abusing Kerberos}

Discover Service Principal Names (SPNs) that are associated with normal user accounts

Use Kerberoasting attacks to steal service tickets or RC4 HMAC hashes tied to service accounts

Perform AS-REP Roasting to retrieve an encrypted AS-REP with a user's RC4 HMAC password

Kerberos Authentication Protocol and Delegation

AS-REP Roasting Attack

Kerberoasting

Kerberos Brute-Force Attacks



\\subsection{Credential Dumping}

Domain Cache Credential

Local Administrator Password Solution (LAPS)

DCSync Attack

NTDS.dit

Golden Ticket

Silver Ticket



\\subsection{Privilege Escalation}

Unconstrained Delegation

Resource-based Constrained Delegation (RBCD)

HiveNightmare

sAMAccountName Spoofing

SeBackupPrivilege

PrintNightmare



\\subsection{Establishing and Maintaining Persistence in Active Directory}

Golden Certificate Attack

DSRM

AdminSDHolder

DC Shadow Attack

Skeleton Key



\\subsection{Lateral Movement}

Pass-the-Ticket (PtT)

Pass-the-Cache

Overpass-the-Hash

Pass-the-Hash (PtH)



\\subsection{Tools}

PowerShell-Empire

CrackMapExec

Impacket Suite

A to Z Mimikat \& Rubeus









\\section{Part ?-References and Tools}

\\section{AD Security Tools Catalog}

\\subsection{Offensive Tools}

\\subsubsection{PowerView}

\\subsubsection{Mimikatz}

\\subsubsection{Rubeus}

\\subsubsection{Impacket Suite}

\\subsection{Defensive Tools}

\\subsubsection{ATA}

\\subsubsection{Defender for Identity}

\\subsubsection{PingCastle}

\\subsubsection{\\texttt{SYSMON}}



\\section{Command and Script Reference}

\\subsection{Common PowerShell, CMD, and Bash Scripts for AD Operations}

\\subsection{Tool Syntax and Usage Examples}



\\section{Glossary of Active Directory Security Terms}



\\section{Appendices}

\\subsection{A: AD Security Checklist}

\\subsection{B: Detection Rule Samples}

\\subsubsection{Sigma}

\\subsubsection{Splunk Queries}

\\subsubsection{KQL}

\\subsection{C: AD Hardening GPO Examples}



\\section{Part VI-Active Directory Enumeration and Local Privilege Escalation}

\\subsection{Enumerating Useful Active Domain-Related Information}

\\subsection{AD Local Privilege Escalation Techniques}

\\subsection{Hunting for Domain Local Admin Privileges Using Multiple Methods}

\\subsection{Abusing Enterprise AD Applications to Discover Attack Pathways}

\\subsection{Security Defense Evasion}

\\subsubsection{Techniques for Bypassing Security Control Mechanisms}

\\subsubsection{Bypassing Signature-Based Antivirus}

\\subsubsection{Pivoting and Obfuscation Methods}

\\section{Part VII-Lateral Movement, Domain Privilege Escalation, and Persistence}

\\subsection{Hunting for Domain Administrator Accounts}

\\subsection{Hijacking High-Privileged Sessions}

\\subsection{AD Credential Extraction}

\\subsubsection{Credential Theft and Replay Attacks}

\\subsubsection{Exfiltrating Credentials from Restricted Environments}

\\subsubsection{Bypassing Allowlists}

\\subsection{Leveraging Built-In Protocols to Escalate Privileges}

\\subsection{Abusing Derivative Domain Local Admin Privileges}

\\subsection{Understanding the Classic Kerberoast}

\\subsubsection{Variants to Escalate Privileges}

\\subsection{Exploiting Delegation Issues}

\\subsection{Protected Groups Privilege Abuse}

\\subsection{Kerberos}

\\subsubsection{Abusing Kerberos Functionality to Persist Using DA Privileges}

\\subsection{Golden and Silver Tickets}

\\subsection{Abusing DC Safe Mode for Persistence}

\\subsection{AdminSDHolder Manipulation}

\\section{Part IIIX-Domain Persistence and Escalation to Enterprise Admins}

\\subsection{ACL Modification for DCSync Attack}

\\subsection{Security Host Descriptor Modification}

\\subsection{Methods for Domain Controller Persistence}

\\subsection{Abusing Trust Keys and \\texttt{krbtgt}}

\\subsection{Executing Intra-Forest Trust Attacks}

\\subsection{AD Database Abuse to Achieve RCE}

\\section{Part IX-Advanced Threat Analytics and Deception}

\\subsubsection{Temporal Group Memberships}

\\subsubsection{ACL and ACE Auditing}

\\subsubsection{LAPS-Local Administrator Password Solution}

\\subsubsection{Hardening SIDs}

\\subsubsection{Kerberos Pre-Auth}

\\subsubsection{SID Filtering}

\\subsubsection{Selective Authentication}

\\subsubsection{Credential Guard and Device Guard}

\\subsubsection{PAWs and SAWs}

\\subsection{Tiered Administration}

\\subsubsection{Tier 0}

\\subsubsection{Tier 1}

\\subsubsection{Tier 2}

\\subsection{EASE and Red Forests}

\\subsection{Defensive Deception Tactics}

\\subsubsection{Lures and Decoys}

\\subsubsection{Canaries and Canary Tokens}

\\subsubsection{Honeypots, Honeynets, and Honey Tokens}



\\section{Introduction to Red Teaming}

\\subsection{Defining Red Team}

\\subsection{Red Team vs. Pentesting}

\\subsectiob{Objectives and Benefits}

\\subsection{Rules of Engagement (ROE) and Legal Aspects}

\\subsection{Tools and Red Team Methodologies}

\\section{Infrastructure and Command \& Control (C2)}

\\subsection{Acquisition of Domains for Operations}

\\subsection{Infrastructure Requirements}

\\subsection{Setting Up and Securing C2 Infrastructure}

\\subsection{Domain Fronting}

\\subsection{HTTPS and DNS Redirectors}

\\section{Initial Recognition}

\\subsection{Passive Recognition: WHOIS, DNS, and Social Networks}

\\subsection{Active Recognitiion: Network Scanning and Service Discovery}

\\subsection{Identity by Email}

\\subsection{Organizational Data Analysis}

\\subsection{Best Practices for Keeping a Low Profile}

\\section{Initial Compromise}

\\subsection{Compromise Techniques}

\\subsubsection{Web Shells}

\\subsubsection{SQL Injection (SQLi)}

\\subsubsection{Password Spraying}

\\subsection{Preparation and Use of Social Engineering Attacks}

\\subsection{Creation of Malicious Payloads}

\\subsection{Payload Distribution}

\\subsection{Attack Vector Customization}

\\subsection{Cyberattack Simulation}

\\section{Establishing a Bridgehead}

\\subsection{Obfuscation Techniques}

\\subsection{Bypassing and Evading Traditional Security Detection Mechanisms}

\\subsection{Executing Malicious Code with .NET and PowerShell}

\\subsection{Command Execution}

\\subsection{Coded Scripts to Evade Detection}

\\subsection{Post-Attack and Intelligence Gathering}

\\subsectiob{Access and Detection Avoidance Strategies}

\\section{Attacking Active Directory Red Team Style}

\\subsection{Lateral Movement}

\\subsection{Enumeration and Privilege Escalation in Active Directory}

\\subsection{Mapping AD Relationships}

\\subsection{Lateral Movement Propagation}

\\subsectiob{The Importance of Situational Awareness and Personal OPSEC}

\\section{Goal Attainment and Reporting}

\\subsection{Database Attack Strategies}

\\subsection{Sensitive Data Exfiltration Techniques}

\\subsection{Preparing Detailed Vulnerability Identification and Remediation Reports}

\\subsection{Verifying and Validating Corrective Measures: Re-Verification and Re-Validation Testing Procedures}

\\subsection{Analyzing Post-Attack Effectiveness of Attack Methodologies}

\\subsection{Measuring Impact of Attack and TTP Strategies}

\\section{Frameworks and Methodologies}

\\subsection{Introduction to Cyber Security Frameworks}

\\subsubsection{MITRE ATT\&CK Framework}

\\subsubsection{Lockheed Martin Cyber Kill Chain (CKC)}

\\subsection{Understanding and Using Threat Intelligence}

\\subsection{Planning and Executing Opponent Emulations}

\\subsection{Analysis of Indicators of Compromise (IoC)}

\\subsection{Technology Watch and Strategy Adaptation}

\\section{Attack Infrastructure and Operational Security}

\\subsection{Configuring and Managing Red Team Tools}

\\subsection{Securing Attack Infrastructure}

\\subsection{Setting Up Beacons and Redirectors}

\\subsection{Maintaining Access and Continued Persistence}

\\subsection{Risk Management}

\\subsection{Reducing Your Attack Footprint}

\\section{Malware Analysis and Reverse Engineering}

\\subsection{Malware Analysis Tools}

\\subsubsection{Ghidra}

\\subsubsection{IDA Pro}

\\subsubsection{OllyDBG}

\\subsection{Malware Reverse Engineering}

\\subsection{Portable Execution (PE) File Formats and Internal Structure}

\\subsection{Malware Tactics}

\\subsection{Importance of Malware Analysis}

\\section{Capture the Red Team Flag}





















\\subsection{}



This is the first section.



\\blindtext



\\addcontentsline{toc}{section}{Unnumbered Section}

\\section\*{Unnumbered Section}



\\blindtext



\\section{Second Section}



\\blindtext

\\end{document}

===============================================================================================================



* Reconnaissance \& Information Gathering

  * Passive Reconnaissance Overview
  * Identifying Our Target
  * Discovering Email Addresses
  * Gathering Credentials with Breach-Parse
  * Gathering Credentials with DeHashed
  * Hunting Subdomains, Part I
  * Hunting Subdomains, Part II
  * Identifying Website Technologies
  * Information Gathering with Burp Suite
  * Google Fu
  * Utilizing Social Media Platforms for Reconnaissance
  * OSINT Fundamentals

===============================================================================================================



* Active Directory Lab Build

  * Lab Overview and Requirements
  * Downloading Necessary ISOs
  * Setting Up Domain Controllers
  * Setting Up User Machines
  * Setting Up Users, Groups, and Policies
  * Joining Machines to Domain



===============================================================================================================



* Active Directory Overview

  * Physical Active Directory Components
  * Logical Active Directory Components

===============================================================================================================



* Active Directory Pentesting Playbook

  * Introduction
  * Objectives of an External Pentest
  * Checklists, FW
  * Rules of Engagement
  * Scope Verification
  * Client Communications
* Kicking Off

  * Attack Strategies
  * Vulnerability Scanning
  * Reviewing and Extracting Information
* Information Gathering Activities via OSINT

  * Overview
  * Hunting for Breached Credentials
  * Identifying Target Employees and Emails
  * Enumerating Valid Active Directory Accounts (Pre-Attack)
  * Other Useful Information
* Attacking Login Portals

  * Overview and Strategy
  * Attacking O365
  * Attacking OWA
  * Attacking Other Portals
  * Bypassing MFA
* Escalating Access

  * Strategy and Walkthrough
* Report Writing

  * Report Writing
* Common Pentest Findings

  * Overview
  * Insufficient Authentication Controls
  * Weak Password Policies
  * Insufficient Patch Management
  * Default Credentials
  * Insufficient Encryption
  * Information Disclosure
  * Username Enumeration
  * Default Web Pages
  * Open Mail Relays
  * IKE Aggressive Mode
  * Unexpected Perimeter Services
  * Insufficient Traffic Blocking
  * Undetected Malicious Activities
  * Historical Account Compromise
* Wrapping Up

  * Client Debriefs
  * Attestation Letters
  * Client Retests

===============================================================================================================



* **Attacking Active Directory - Post-Compromise Attacks**

  * Introduction

    * Pass-the-Hash / Password Overview
    * Installing CrackMapExec
    * Pass-the-Password Attacks
    * Dumping Hashes with `secretsdump.py`
    * Cracking NTLM Hashes with Hashcat
    * Pass-the-Hash (PtH) Attacks
    * Pass Attack Mitigations
  * Token Impersonation Overview

    * Token Impersonation with Incognito
  * Token Impersonation Mitigation
  * Kerberoasting Overview

    * Kerberoasting Walkthrough
    * Kerberoasting Mitigation
  * GPP/cPassword Attacks Overview

    * Abusing GPP, Part I
    * Abusing GPP, Part II
* URL File Attacks
* PrintNightmare (CVE)-2012-1675) Walkthrough
* Mimikatz Overview
* Credential Dumping with Mimikatz
* **Additional Active Directory Attacks**

  * Abusing ZeroLogon

===============================================================================================================



* **Attacking Active Directory - Post-Compromise Enumeration**

&#x09;\* Introduction

&#x09;\* PowerView Overview

&#x09;\* Domain Enumeration with PowerView

&#x09;\* BloodHound Overview and Setup

&#x09;\* Grabbing Data with `Invoke-Bloodhound`

&#x09;\* Enumerating Domain Data with BloodHound

===============================================================================================================



* **Exploitation**

  * Reverse Shells vs. Bind Shells
  * Staged vs. Non-Staged Payloads
  * Gaining Root with Metasploit
  * Manual Exploitation
  * Brute-Force Attacks
  * Credential Stuffing and Password Spraying

===============================================================================================================



* Initial Active Directory Attack Vectors

  * Introduction
  * LLMNR Poisoning Overview
  * Capturing NTLMv2 Hashes with Responder
  * Password Cracking with Hashcat
  * LLMNR Poisoning Defenses
  * SMB Relay Attacks Overview
  * Discovering Hosts with SMB Signing Disabled
  * SMB Relay Attack Demonstration, Part I
  * SMB Relay Attack Demonstration, Part II
  * SMB Relay Attack Defenses
  * Gaining Shell Access
  * IPv6 Attacks Overview
  * Installing mitm6
  * Setting Up LDAPS
  * IPv6 DNS Takeover via mitm6
  * IPv6 Attack Defenses
  * Passback Attacks
  * Other Attack Vectors and Strategies

===============================================================================================================



* **Linux Privilege Escalation for Beginners**

&#x09;\* Introduction

* **Initial Access and Enumeration**

&#x09;\* System Enumeration

&#x09;\* User Enumeration

&#x09;\* Network Enumeration

&#x09;\* Password Hunting

* **Exploring Automated Tools**

&#x09;\* Introduction

&#x09;\* Exploring Automated Tools

* **Escalation Path: Kernel Exploits**

&#x09;\* Kernel Exploits Overview

&#x09;\* Escalation via Kernel Exploitation

* **Escalation Path: Passwords and File Permissions**

&#x09;\* Overview

&#x09;\* Escalation via Stored Passwords

&#x09;\* Escalation via Weak File Permissions

&#x09;\* Escalation via SSH Keys

* **Escalation Path: Sudo**

&#x09;\* Sudo Overview

&#x09;\* Escalation via Sudo Shell Escaping

&#x09;\* Escalation via Intended Functionality

&#x09;\* Escalation via `LD\\\_PRELOAD`

&#x09;\* Challenge Overview

&#x09;\* Challenge Walkthrough

&#x09;\* CVE-2019-14287 Overview

&#x09;\* Escalation via CVE-2019-14267

&#x09;\* Overview and Escalation via CVE-2019-18634

* **Escalation Path: SUID**

&#x09;\* SUID Overview

&#x09;\* Gaining a Foothold

&#x09;\* Escalation via SUID

* **Escalation Path: Other SUID Escalation**

&#x09;\* Escalation via Shared Object Injection

&#x09;\* Escalation via Binary Symlinks

&#x09;\* Escalation via Environmental Variables

* **Escalation Path: Capabilities**

&#x09;\* Capabilities Overview

&#x09;\* Escalation via Capabilities

* **Escalation Path: Scheduled Tasks**

&#x09;\* Cron and Timers Overview

&#x09;\* Escalation via Cron Paths

&#x09;\* Escalation via Cron Wildcards

&#x09;\* Escalation via Cron File Overwrites

&#x09;\* Challenge Overview

&#x09;\* Challenge Walkthrough

* **Escalation Path: NFS Root Squashing**

&#x09;\* Overview and Escalation via NFS Root Squashing

* **Escalation Path: Docker**

&#x09;\* Overview

&#x09;\* Gaining a Foothold

&#x09;\* Escalation via Docker

===============================================================================================================



* **Understanding the SAM Database**
* **Attack Methodology**

  * Prerequisites and Privilege Escalation
  * Legal and Compliance Implications
  * Summary
* **Historical Evolution of SAM Security Mechanisms**
* **Common SAM Extraction Tools and Techniques**

  * Registry-Based Extraction Methods
  * Volume Shadow Copy Service Exploitation
  * Specialized Credential Extraction Tools
  * Remote SAM Extraction Techniques
* **Hash Cracking Methodology**

  * NTLM Hash Algorithm Characteristics
  * Dictionary and Rule-Based Attacks
  * Brute-Force and Mask Attacks
  * Rainbow Tables and Precomputation Attacks
  * Cracking Tool Ecosystem
* **Defensive Strategies and SAM Hardening**

  * Access Control Hardening
  * Group Policy-Based Hardening at Scale
  * Detection and Response Procedures
  * Credential Guard and Virtualization-Based Security
* **Real-World Case Studies and Impact Analysis**

  * Case Study Target Corporation Breach (2013)
  * Case Study NotPetya Ransomware Campaign (2017)
  * Case Study: SolarWinds Supply Chain Compromise (2020)
  * Impact on Active Directory Infrastructure)
* **Windows Operating System (OS) Version and Configuration Comparison**

  * **Legacy Windows Versions**

    * Windows XP
    * Windows Server 2003
    * Windows Vista
    * Windows Server 2008
  * **Modern Windows Versions**

    * Windows 8.1
    * Windows Server 2016
    * Windows Server 2019
    * Windows 11
    * Windows Server 2022
    * Configuration Impact on SAM Security
* **Integration with Incident Response (IR) Frameworks**

  * Detection Integration with SIEM and SOAR Platforms
  * Incident Classification and Escalation
  * Forensic Investigation Procedures
* **Advanced SAM Extraction Techniques**

  * Memory-Resident SAM Extraction
  * Remote SAM Extraction via SMB and RPC
  * Registry Shadow Copy Exploitation
  * Lateral Movement and Credential Reuse
  * NTLM Relay Attacks with Extracted Hashes
  * Supply Chain and Persistence Mechanisms
* Conclusion

===============================================================================================================



\* Windows Privilege Escalation for Beginners

&#x09;\* Introduction

&#x09;	\* Resources and Tips for Success

&#x09;\* Gaining a Foothold

&#x09;	\* Introduction

&#x09;	\* Gaining a Foothold Methodology

&#x09;\* Initial Enumeration

&#x09;	\* System Enumeration

&#x09;	\* User Enumeration

&#x09;	\* Network Enumeration

&#x09;	\* Password Hunting

&#x09;	\* AV Enumeration

&#x09;\* Exploring Automated Tools

&#x09;	\* Automated Tools Overview

&#x09;	\* Exploring Automated Tools

&#x09;\* Escalation Path: Kernel Exploits

&#x09;	\* Kernel Exploits Overview

&#x09;	\* Escalation with Metasploit

&#x09;	\* Manual Kernel Exploitation Methods

&#x09;\* Escalation Path: Passwords and Port Forwarding

&#x09;	\* Overview

&#x09;	\* Gaining a Foothold

&#x09;	\* Escalation via Stored Passwords

&#x09;\* Escalation Path: Windows Subsystem for Linux (WSL)

&#x09;	\* Overview

&#x09;	\* Gaining a Foothold

&#x09;	\* Escalation via WSL

&#x09;\* Impersonation and Potato Attacks

&#x09;	\* Token Impersonation Overview

&#x09;	\* Impersonal Privileges Overview

&#x09;	\* Potato Attacks Overview

&#x09;\* Escalation Path: Potato Attacks

&#x09;	\* Alternate Data Streams

&#x09;\* Escalation Path: RunAs

&#x09;	\* Overview of RunAs

&#x09;	\* Gaining a Foothold

&#x09;	\* Escalation via RunAs

&#x09;\* Escalation Path: Windows Registry

&#x09;	\* Overview of Autoruns

&#x09;	\* Escalation via Autoruns

&#x09;	\* `AlwaysInstallElevated` Overview and Escalation

&#x09;	\* Overview of `regsvc` ACL

&#x09;	\* `regsvc` Escalation

&#x09;\* Escalation Path: Executable Files

&#x09;	\* Executable Files Overview

&#x09;	\* Escalation via Executable Files

&#x09;\* Escalation Path: Startup Applications

&#x09;	\* Startup Applications Overview

&#x09;	\* Escalation via Startup Applications

&#x09;\* Escalation Path: DLL Hijacking

&#x09;	\* Overview and Escalation of DLL Hijacking

&#x09;\* Escalation Path: Service Permissions Pathways

&#x09;	\* Escalation via Binary Paths

&#x09;	\* Escalation via Unquoted Service Paths

&#x09;	\* Gaining a Foothold

&#x09;	\* Escalation via Unquoted Service Paths with Metasploit

===============================================================================================================



**Foundations of Domain Reconnaissance**

* **Introduction to Modern Cyber Reconnaissance**

  * Evolution From Port Scanning to OSINT Intelligence
  * MITRE ATT\&CK Reconnaissance Phase (TA0043)
  * Offensive vs. Defensive Reconnaissance Paradigms
  * Legal Frameworks for Authorized Penetration Testing
* **Reconnaissance Methodology Framework**

  * Passive vs. Active Reconnaissance Risk Models
  * The Reconnaissance Kill Chain
  * Target Profiling Lifecycle
  * Attribution and OPSEC Considerations

=====================================================



* **Introduction to Pass-the-Hash (PtH)**

  * Definition and Conceptual Overview
  * Evolution of NTLM and Authentication Protocols
  * The Anatomy of a Hash - LM vs. NTLM vs. NT
  * Why PtH Remains Prevalent - The Static Hash Weakness
  * Overview of the Attack Lifecycle (The A-Z Framework)
* **Foundations of NTLM Authentication and Credential Reuse in Active Directory Environments**

  * **Introduction to NTLM and Pass-the-Hash Principles**

    * Historical Context and Protocol Specifications in NTLMv1 and NLTMv2
    * Challenge-Response Mechanisms
    * Credential Storage Mechanisms
    * Service and User Account Behaviors That Enable Hash Persistence
    * Common Misconfigurations
    * Technical Rationale for Balancing Offensive Understanding
  * **Enumeration of Opportunities for Hash Reuse in Target Environments**

    * Identification of Accounts
    * Prerequisite Permissions
    * Using BloodHound
    * Permissions Auditing
    * Technical Rationale
* **Offensive Perspective - Exploiting Pass-the-Hash Techniques**

  * **Technical Mechanics of Pass-the-Hash**

    * Hash Acquisition From Memory, Disk, or Network - LSASS Dumping and DPAPI Interaction
    * Injection of NTLM Hashes Into Authentication Contexts Without Password Knowledge
    * Remote Execution Vectors - SMB, WMI, WinRM, and RPC with Passed Hashes
    * Impact of Legacy Compatibility Settings - LMCompatibilityLevel, NTLM Restrictions - on Technique Visibility
    * Technical Rationale for Why Pass-the-Hash Bypasses Password-Policy Controls Entirely
  * **Tools and Techniques for PtH Misconfigurations**

    * In-Memory Frameworks - Mimikatz and Overpass-the-Hash
    * PowerShell-Based Modules - Invoke-PassTheHash, PowerSploit - Empire and Cobalt Strike Integration
    * Cross-Platform Implementations Using the Impacket Tool Suite - wmiexec.py and psexec.py with Hashes
    * Custom Script Development - PowerShell and Python Snippets for Automated Pass-the-Hash Workflows
    * Integration with BloodHound and PowerView
  * **Advanced Exploitation Scenarios and Evasion Techniques**

    * Pass-the-Hash in Constrained or Resource-Based Delegation Chains
    * Lateral Movement and Pivoting
    * Evasion of Native Logging and Modern EDR During Hash Injection
    * Combining Pass-the-Hash with Complementary Credential Techniques
    * Technical Rationale for Why These Variants Remain

=====================================================



Notes about the following sections:

* Consistent parts, chapters, and sections structure suitable for academic publishing
* Balanced coverage (45% offensive, 45% defensive, 10% foundations and future)
* Technical depth signaled through specific subtopics (Event IDs, MITRE mappings)
* Comprehensive appendices for practitioner reference



* **Part I - Foundations of Kerberoasting**
* **Introduction to Kerberoasting in Active Directory Environments**

  * Historical Context, Evolution, Discovery, and Protocol Specifications
  * Core Components - Principals, Keys, Tickets (TGT \& TGS) and Encryption Types
  * Service Principal Names (SPNs) - Registration, Uniqueness, and Role in Service Authentication
  * Kerberoasting in the MITRE ATT\&CK Framework (T1558.003)
  * Common Misconfigurations in Service Accounts That Expand the Exploitation Surface
  * Offensive vs. Defensive Paradigms - A Comparative Overview
  * Scope and Methodology of This Book - Balancing Offensive Understanding with Defensive Training Objectives
* **Kerberos Authentication Protocol Fundamentals**

  * The Kerberos Architecture and Ticketing Lifecycle
  * Service Principal Names (SPNs) and Their Role in AD
  * Ticket Granting Tickets (TGTs) vs. Service Tickets (TGS)
  * Encryption Types and Key Derivation - RC4 and AES
  * Offensive Perspective - Identifying Weak Encryption Targets
  * Defensive Perspective - Protocol Hardening Opportunities
* **Service Account Management and Enumeration in the Target Environment**

  * Types of Service Accounts
  * Technical Mechanics of SPN Registration
* **The Kerberoasting Attack Vector**

  * Core Attack Mechanics - TGS Request and Response
  * Anatomy of a Roastable Service Ticket
  * Key Derivation and Password Cracking Mathematics
  * Success Factors - RC4 Prevalence and Password Policies



**Part II - Offensive Operations - The Attacker's Playbook**

* **Exploiting Misconfigurations Leading to Kerberoasting**

  * **Technical Mechanics of the Kerberoasting Misconfiguration**

    * Service Ticket Request Workflow
    * Extraction of the Encrypted Portion of the Service Ticket (TGS)
    * Offline Password Recovery Techniques
  * **Tools and Techniques for Demonstrating Exploitation of the Kerberoasting Misconfiguration**

    * PowerShell-Based Enumeration
    * C#-Based Frameworks (Rubeus)
    * Cross-Platform Implementations
    * Custom Script Development
    * Integration with BloodHound
  * **Advanced Exploitation Scenarios and Evasion Techniques**

    * Targeting High-Privilege or Long-Lived Service Principals
    * Kerberoasting in Multi-Domain, Multi-Forest, and Hybrid Cloud Environments
    * Evasion of Native Logging During Ticketing Requests
    * Combining Kerberoasting with Complementary Enumeration Techniques



* **Reconnaissance and Target Identification**

  * Active Directory Enumeration Techniques
  * PowerView, BloodHound, and LDAP Queries
  * SPN Discovery Using setspn and LDAP Filters
  * Credentialed vs. Uncredentialed Reconnaissance
  * Mapping High-Value Service Accounts in Active Directory
* **Weaponization and Execution**

  * Tool Arsenal - Rubeus, Impacket, Kekeo
  * Custom Payload Development
  * Request Forging and Evasion Techniques
  * AS-REP Roast Integration - Pre-Kerberoasting Abuse
* **Post-Exploitation and Cracking**

  * Offline Cracking Strategies Using Hashcat and John the Ripper (JtR)
  * GPU Acceleration and Distributed Cracking
  * Password Policy Analysis and Bypass
* **Lateral Movement and Privilege Escalation**

  * Service Account Takeover Workflows
  * Pivot Points - SQL Service Account and IIS AppPools
  * DCSync Rights Abuse Post-Compromise
  * Golden Ticket Forgery from Roasted Credentials
* **Advanced Offensive Techniques**

  * Kerberoasting over RPC and DCE
  * Cloud Hybrid Attacks - Azure AD Kerberoasting
  * Red Team OPSEC - Living-Off-The-Land (LoTL)
  * Automation Frameworks - Cobalt Strike and Empire



**Part III - Defensive Strategies - Blue Team Countermeasures**



* **Defensive Perspective - Mitigating, Detecting, and Responding to Kerberoasting Attacks**

  * **Preventive Hardening of Service Principals**

    * Enforcing Strong and Frequently Rotated Passwords
    * Deployment and Management of gMSAs
    * SPN Hygiene
    * Group Policy and Domain-Level Kerberos Policy Configurations
    * Technical Rationale for gMSA Adoption
  * **Detection and Monitoring Strategies**

    * Key Windows Security Events and IDs
    * Important Event IDs for Defenders - 4769, 4770, 4768) and Pattern Analysis
    * Building SIEM Correlation Rules
    * Behavioral Analytics - Machine-Learning
    * Technical Rationale for Event Logs
  * **Incident Response (IR) and Recovery Procedures**

    * Triage of Suspected Kerberoasting Activities
    * Forensics Collection and Analysis of Ticket-Related Attacks
    * Containment - Immediate Enterprise-Wide Password Resets and SPN Reconfiguration
    * Post-Incident Hardening and Root-Cause Analysis
    * Technical Rationale for Layered Response Playbooks
* **Defensive Detection Engineering**

  * Event Log Analysis - Event IDs 4769, 4624, 4672
  * SIEM Rules and Anomaly Detection
  * Network Traffic Signatures - Kerberos Over 88 and 445
  * Behavioral Analytics - TGS Request Volumes
* **Defensive Prevention Architecture**

  * Service Account Hardening Best Practices
  * SPN Management and Principle of Least Privilege
  * Group Managed Service Accounts (gMSAs) Deployment
* **Password and Credential Defense**

  * Policy Enforcement - Length, Complexity, and Rotation
  * Protected Users Group Implementation
  * LAPS and Just-In-Time (JIT) Administration
  * Tier 0 and PAWs/SAWs
  * Monitoring for Weak Encryption Usage
* **Defensive Response and Recovery**

  * Incident Response (IR) Playbooks
  * Compromised Account Reset Procedures
  * Forensic Analysis of Roasted Tickets
  * Threat Hunting Methodologies



**Part IV - Technical Deep Dive**

* **Cryptographic Analysis**

  * RC4-HMAC Weaknesses and Known Domain-Related Cyberattacks
  * AES Key Derivation Vulnerabilities
  * Ticket Signing and Integrity Validation
* **Implementation Details by Platform**

  * Windows Server 2008-2022 Behaviors
  * Linux and UNIX Kerberos - MIT vs. Heimdal
  * Hybrid Identity Considerations
* **Case Studies and Real-World Attacks**

  * Notable Breaches Involving Kerberoasting
  * Red Team Engagement - Lessons Learned
  * Blue Team Successful Strategies



**Part V - Tools, Code, and Resources**

* **Offensive Tool Compendium**

  * Open-Source Implementations
  * Commercial Tool Integration
  * Custom Script Repository
* **Defensive Tool Ecosystem**

  * Monitoring and Detection Tools
  * Hardening Scripts and GPO Templates
  * Testing and Validation Frameworks



**Part VI - Future and Emerging Trends**

* **Evolving Attack Landscape, Surfaces, and Thresholds**

  * Pass-the-Ticket (PtT) Execution
  * Quantum Computing Threats to Kerberos
  * Post-Quantum Cryptographic Migration
* **Research Directions and Open Problems**

  * Undiscovered Attack Vectors
  * Defensive Innovation Needs

=====================================================



**GPO Abuse, Lateral Movement, and Privilege Escalation (Initial Access)**

* **Foundational Concepts**

  * **Introduction to the Attack Surface**

    * GPO Abuse, Lateral Movement, and Initial Privesc Ecosystem
    * MITRE ATT\&CK Coverage (T1484, TA0008, TA0004)
    * Attack Chain Interdependencies
    * Scope - Domain vs. Local vs. Cloud Contexts
    * The Administrative Trust Model and Why It Fails
    * How Misconfigurations Accumulate Over Time in Enterprise Environments
    * Threat Actor Profiles - Who Uses These Techniques and Why
    * Real-World Intrusion Campaigns Featuring GPO-Based Lateral Movement
    * Chapter Roadmap - How the Attack Chain Maps to This Book
  * **Windows Security Architecture Foundations**

    * The Windows Security Reference Monitor and Access Token Model
    * Mandatory Integrity Control - Integrity Levels and UAC
    * Security Identifiers (SIDs) and Relative Identifiers (RIDs)
    * Access Control Lists - DACLs, SACLs, and ACE Evaluation Order
    * Windows Authentication Protocols - NTLM vs. Kerberos Side-by-Side
    * Local Security Authority (LSA) and the Credential Storage Model
    * Windows Token Impersonation and Delegation
    * Protected Processes and Credential Guard
    * How Windows Handles Privilege Separation at the Kernel Level
    * Security Architecture Gaps That GPO Abuse and Lateral Movement Exploit
  * **Active Directory Architecture for Attackers**

    * The AD Information Model - Forests, Domains, Trees, and Trust Boundaries
    * The LDAP Directory Service - How AD Stores and Exposes Object Data
    * Domain Controllers - Roles, Replication, and the FSMO Model
    * The Global Catalog and Its Role in Domain and Subdomain Enumeration
    * AD Object Classes and Attributes Relevant to Offensive Operations
    * Distinguished Names (DNs), Canonical Names (CNs), and Object Paths
    * AD Replication - USNs, Originating Updates, and Replication Conflicts
    * Trust Relationships - Transitive, External, Forest, and Shortcut Trusts
    * The AdminSDHOlder Mechanism and Protected Accounts
    * Read-Only Domain Controllers (RODCs) - Architecture and Attack Surface Differences
  * **Group Policy Architecture Deep Dive**

    * The Group Policy Processing Engine - Client-Side Extensions (CSEs)
    * Group Policy Container (GPC) vs. Group Policy Template (GPT) - The Two-Component Model
    * SYSVOL Architecture - DFS-R, FRS, and File Permission Implications
    * Enforced vs. Blocked Inheritance - Administrative Intent vs. Security Implications
    * Security Filtering and WMI Filtering - Scope Control Mechanisms
    * GPO Versioning - How Changes Are Tracked and Replicated
    * Computer Policy vs. User Policy - Processing Contexts and Timing Differences
    * Resultant Set of Policy (RSoP) - What Applies Where and Why
    * Group Policy Preferences vs. Group Policy Settings - The Security Distinction
  * **Organizational Unit (OU) Design and Delegation Models**

    * OU Design Philosophies - Geography, Function, Object Type, and Hybrid Models
    * How Delegation Works - The ACL Model Behind OU Administration
    * The `gpLink` and `gpoptions` Attributes - How GPOs Are Connected to OUs
    * The `managedBy` Attribute
    * Delegated Permissions That Create GPO Attack Paths
    * Nested OUs and Inherited Delegation - How Permissions Propagate Downward
    * OU Design Anti-Patterns That Create Privilege Escalation Opportunities
    * The Relationship Between OU Structure and Administrative Tier Models
    * Enumerating OU Delegation from a Low-Privilege Position
    * Mapping OUT Topology to Attack Paths
  * **Privilege Levels, Tiers, and Administrative Boundaries**

    * The Microsoft Tiering Model
    * Domain Admin, Enterprise Admin, and Schema Admin
    * Built-In Privileged Groups
    * Service Accounts
    * Local Admin
    * Privileged Access Workstations (PAWs) / Secured Administrative Workstations (SAWs)
    * How Tier Boundaries Break Down in Practice
    * Shadow Admins
    * The Relationship
    * Modeling Privilege Escalation
  * **Enumeration Methodology and Operational Security (OPSEC)**

    * Pre-Exploitation Enumeration Philosophy
    * LDAP Enumeration Techniques
    * PowerView
    * BloodHound
    * Native Windows Tools
    * Enumeration Artifacts
    * Operational Security (OPSEC)
    * Prioritizing Findings
    * Enumerating from Restricted Contexts
    * Building the Attack Graph



**Offensive Operations - The Attacker's Arsenal**

* **Initial Access and Foothold Establishment**

  * Defining Initial Access
  * Phishing and Credential Harvesting
  * Password Spraying
  * Exploiting Externally Facing Services
  * Gaining a Foothold via Misconfigured SMB
  * Default and Weak Credentials
  * Establishing a Beachhead
  * Situational Awareness from First Access
  * Avoiding Early Detection
  * Transitioning from Foothold to Enumeration
* **GPO Enumeration and Attack Surface Mapping**

  * Enumerating GPOs
  * Mapping GPO-to-OU Linkages
  * Identifying GPO Permissions Misconfigurations
  * BloodHound Queries for GPO
  * Enumerating SYSVOL
  * Identifying Unlinked GPOs
  * Enumerating WMI Filters
  * Mapping GPO Enforcements
  * Correlating GPO Permissions
  * Prioritizing GPO Attack Paths
* **Exploiting GPO Write Permissions**

  * Understanding `GenericWrite`
  * Abusing `GenericWrite`
  * SharpGPOAbuse
  * Deploying Malicious
  * Modifying GPOs
  * Abusing User Rights Assignments
  * Registry Modifications
* **GPO Linking Attacks and OU Targeting**

  * Understanding the `gpLink`
  * The `WriteProperty`
  * Identifying Principals with GPO
  * Creating a Malicious GPO
  * Enforced GPO Linking
  * Targeting Domain Controllers
  * Targeting Server OUs

===============================================================================



**Golden Ticket Attacks**



**Part I - Foundations**

1. **Introduction to Kerberos and Active Directory**
* The Kerberos Authentication Protocol - AS and TGS Exchange
* Key Distribution Center (KDC) Role
* Ticket Granting Tickets (TGTs) vs. Service Tickets (TGS)
* The Privilege Attribute Certificate (PAC)
* The Significance of the `krbtgt` Account

**2. The Anatomy of a Golden Ticket Attack**

* Defining Golden Ticket
* Post-Exploitation Nature - Why It Happens After Infiltration
* Key Components - Domain SID, User UID, `krbtgt` Hash
* The Goldmine - Impact of Total Domain Compromise

**3. Offensive Prerequisites and Setup**

* Initial Access Strategies (Phishing, Vulnerability Exploitation)
* Establishing Domain Admin (DA) Privileges
* Extracting the `krbtgt` Hash - LSASS Memory Dumps
* Advanced Extraction - DCSync and Replication Abuse



**Part II - The Offensive Perspective (Attack Techniques)**

**4. Creating the Golden Ticket (The Forgery Process)**

* Using Mimikatz for Ticket Generation
* Using Rubeus and Other Open-Source Tools
* Forging PAC Data for Elevated Privileges
* Setting Long-Term Persistence (10+ Year Lifetime)

**5. Advanced Exploitation and Evasion**

* Injecting Tickets Into Memory
* Bypassing Traditional EDR and Antivirus Systems
* Golden Ticket vs. Silver Ticket - Key Differences
* Lateral Movement Using Forged TGTs

**6. Covering Tracks**

* Tampering with Event Logs (Security and System)
* Timestamp Manipulation of Tickets
* Clearing Local Cache Memory



**Part III - The Defensive Perspective (Mitigation and Detection)**

**7. Preventive Measures - Reducing the Attack Surface**

* Enforcing Tiered Administration - Tiers 0, 1, and 2
* Restricting Domain Controller Access
* Implementing Local Administrator Password Solution (LAPS)
* Hardening LSASS - Credential Guard and Protections

**8. Detection and Behavioral Analysis**

* Monitoring for Abnormal `krbtgt` Account Access
* Identifying Unusual TGT Lifespans
* Analyzing Kerberos Event IDs - 4624, 4768, 4769
* Using SIEM and XDR to Detect Inconsistent PAC Data

9\. Incident Response and Remediation

* Identifying a Compromise - The Smoking Gun
* The Double `krbtgt` Reset Process
* Post-Reset Considerations - Disrupting Kerberos Traffic
* Forensic Analysis of Forged Tickets



Part IV - Future Landscape and Conclusion

10\. The Evolution of Kerberos Threats

* Cloud Hybrid Scenarios (Azure AD and Entra ID)
* Future of Identity-Based Attacks

11\. Summary of Best Practices

* Checklist for Active Directory Security
* Creating a Resilient Domain Architecture



Part V - Appendices

Appendix X - Mimikatz and Rubeus Command Examples

Appendix X - PowerShell Scripts for Security Auditing

Appendix X - Glossary of Terms

===============================================================================



AS-REP Roasting



Part I - Foundations of AS-REP Roasting

* **1. Introduction to AS-REP Roasting**

  * Discovery and Historical Context
  * MITRE ATT\&CK Mapping - T1558.004
  * AS-REP Roasting vs. Kerberoasting Key Distinctions
  * Attack Prerequisites and Scope Analysis
* **2. Kerberos Authentication Protocol**

  * AS-REP Request and Response Protocol Deep Dive
  * User Account Properties - DONT\_REQ\_PREAUTH Flag
  * Pre-Authentication Bypass Mechanics
  * Encryption Type Selection and Fallbacks
* **3. AS-REP Roast Attack Anatomy**

  * Core Exploitation Workflow
  * Hash Extraction and Structure Analysis
  * Key Derivation Attacks - RC4 - HMAC - MD5
  * Success Probability Factors by AD Environment



Part II - Offensive Operations - The Attacker's Arsenal

* **4. Execution and Harvesting**

  * Tool Ecosystem - Impacket Tool Suite and Impacket-GetNPUsers, and Rubeus
  * Multi-Threaded Enumeration Strategies
  * OPSEC Considerations - Query Rate Limiting
  * Hybrid Attack Combinations (AS-REP + Kerberoast)
* **5. Cracking and Analysis**

  * AS-REP Roast Hash Formats and Wordlists
  * GPU Cracking Optimization (Hashcat Mode 18200)
  * Password Policy Reverse Engineering
  * Batch Account Prioritization Models
* **6. Post-Exploitation Impact**

  * Direct Service Access with Compromised Credentials
  * Lateral Movement from Batch and Legacy Accounts
  * Privilege Escalation Pathways
  * DCSync and Delegation Abuse
* **7. Advanced Offensive Techniques**

  * Cloud AS-REP Roasting (Azure AD Legacy Apps)
  * Custom Payload Development
  * EDR Evasion Tactics
  * Automation in C2 Frameworks



**Part III - Reconnaissance and Enumeration**

* **8. Uncredentialed AD Enumeration Techniques**

  * LDAP Query Filters for DONT\_REQ\_PREAUTH
  * Netexec, CrackMapExec, and PowerView
* Anonymous Bind Exploitation
* Batch Account Identification Patterns



**Part IV - Defensive Strategies - Protection Framework**

* **9. Detection Capabilities**

  * Critical Event IDs - 4768, 4771, Failed AS-REQ
  * Anomaly Detection - Pre-Auth Bypass Patterns
  * Network Monitoring - Port 88 Anomalies
  * SIEM Correlation Rules
* **10. Prevention Engineering**

  * Account Configuration Hardening
  * Removing DONT\_REQ\_PREAUTH Flag
  * PowerShell Remediation Scripts
  * Legacy Account Cleanup Strategies
  * Service Account Segmentation Best Practices
* **11. Policy and Access Controls**

  * Pre-Authentication Domain-Wide Enforcement
  * Protected Users Group Membership
  * Fine-Grained Password Policies (FGPP)
  * Anonymous LDAP Bind Restrictions
* 12\. Response Procedures

  * Incident Response Timeline and Checklists
  * Compromised Account Isolation
  * Forensics Artifacts Collection
  * Reset and Remediation Protocols
* 13\. Advanced Defensive Architecture

  * Behavioral Analytics Platforms
  * Machine Learning Baselines
  * Zero Trust Identity Verification
  * Continuous Threat Hunting



Part IV - Technical Implementation

* **14. Cryptographic Weaknesses**

  * RC4 in AS-REP - Mathematical Vulnerabilities
  * Hash Format Evolution and Parsing
  * AES Transition Challenges
* 15\. Platform-Specific Behaviors

  * Windows Versions (2003-2022) Analysis
  * Samba and Linux Kerberos Behaviors
  * Hybrid Identity Implications
* 16\. Real-World Case Studies

  * Breach Post-Mortems Featuring AS-REP Roasting
  * Pentesting Engagements - Common Findings
  * Blue Team Mitigation Success Metrics



**Part V - Practitioner Resources**

* **17. Offensive Implementation Guide**

  * Complete Toolchain Walkthroughs
  * Bash and PowerShell Script Repository
  * Wordlist Optimization Strategies
* **18. Defensive Deployment Guide**

  * GPO Templates and Scripts
  * Detection Rule Libraries (Sigma, Splunk)
  * Validation Testing Frameworks



Part VI - Future Threat Landscape

* 19\. Attack Evolution Vectors

  * New Protocol Weaknesses
  * Cloud-Native AS-REP Variants
  * Quantum Resistance Requirements
* 20\. Research Frontiers

  * Detection Innovation Opportunities
  * Mitigation Tradeoff Analysis



Part VII - Appendices

Appendix X - AS-REP Event Log Reference

Appendix X - LDAP Query Templates

Appendix X - Hashcat and John Configuration Files

Appendix X - Remediation PowerShell Toolkit

Appendix X - AS-REP Roast Hash Format Specifications



