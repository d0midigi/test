# Running Table of Contents

## PART I - Reader Orientation, Identity, and The Federal Mission

### <mark style="color:pink;">**Chapter 1 - The Reader's Guide to the Identity Battlefield**</mark>

* **1.1 Why This Book Exists**
  * 1.1.1 One Environment, Several Professional Views
  * 1.1.2 Why Offensive and Defensive Security Belong Together
  * 1.1.3 Why the Federal Context Changes the Problem
* **1.2 Who This Book Is For**
  * 1.2.1 New Federal and DoD Cybersecurity Practitioners
  * 1.2.2 Systems and Active Directory Administrators
  * 1.2.3 Identity and ICAM Engineers
  * 1.2.4 ISSOs, ISSMs, ISSEs, and Assessors
  * 1.2.5 SOC/NOC Analysts, and Threat Hunters
  * 1.2.6 Ethical Hackers, Penetration Testers, Red, and Purple Teams
  * 1.2.7 Incident Responders and Recovery + Triage Engineers
* **1.3 What the Reader Is Expected to Know**
  * 1.3.1 General Information and Technology Foundations
  * 1.3.2 Basic Windows and Linux OS Familiarity
  * 1.3.3 Basic Active Directory Infrastructure Familiarity
  * 1.3.4 Basic Cybersecurity Concepts
  * 1.3.5 Command-Line Interface (CLI) and Scripting Familiarity
  * 1.3.6 Basic Security Assessment Concepts
* **1.4 What The Reader Does Not Need to Know Yet**
  * 1.4.1 You Do Not Need to Know Kerberos Internals
  * 1.4.2 You Do Not Need to Know LDAP Internals
  * 1.4.3 You Do Not Need to Understand Windows Authorization Internals
  * 1.4.4 You Do Not Need to Know Active Directory Certificate Services (AD CS)
  * 1.4.5 You Do Not Need to Know FICAM or DoD ICAM
  * 1.4.6 You Do Not Need Prior Offensive or Defensive Active Directory Experience
  * 1.4.7 You Do Not Need Prior Federal or Military Experience
* **1.5 How This Book Teaches Identity Security**
  * 1.5.1 Architecture Before Exploitation
  * 1.5.2 Protocol Mechanics Before Protocol Abuse
  * 1.5.3 Assessment Before Offensive Validation
  * 1.5.4 Offensive Tradecraft Paired with Defensive Engineering
  * 1.5.5 Detection Before Response
  * 1.5.6 Recovery Before Trust Restoration
  * 1.5.7 Technical Findings Must Be Translated Into Mission Meaning
* **1.6 How to Use This Book**
  * 1.6.1 Figures and Architecture Diagrams
  * 1.6.2 Tables and Technical Reference Material
  * 1.6.3 Labs and Exercises
  * 1.6.4 Case Studies
  * 1.6.5 Attacker and Defender Journal Entries
  * 1.6.6 Field Notes and Operational Lessons
  * 1.6.7 MITRE ATT\&CK Framework Mappings
  * 1.6.8 Offensive and Defensive Tooling
* **1.7 The Reader Contract**
  * 1.7.1 What This Book Is
  * 1.7.2 What This Book Is Not
  * 1.7.3 Ethical Use and Authorization
  * 1.7.4 Authorization and Rules of Engagement
  * 1.7.5 Production-System Safety
* **1.8 The Book's Progression**
* **1.9 Preparing for Chapter 2**

### <mark style="color:pink;">**Chapter 2 - Identity Infrastructure Networking**</mark>

* **2.1 Why Identity Depends on the Network**
  * 2.1.1 Network Transport Dynamics: Kerberos, NTLM, RADIUS, and LDAP/S as Network Payloads
  * 2.1.2 Threat Model: On-Path and Man-in-the-Middle (MitM) Adversary Capabilities
  * 2.1.3 FICAM Alignment: Impact of Transport Interception on Credential Assurance Levels (CAL)
* **2.2 TCP/IP Foundations for Identity Services**
  * 2.2.1 Transport Dynamics: TCP Versus UDP Behavior for Kerberos, DNS, and LDAP
  * 2.2.2 Kerberos MTU and Packet Fragmentation: Handling `KRB_ERR_RESPONSE_TOO_BIG`
  * 2.2.3 Defensive Configuration: Enforcing Kerberos Over TCP via Registry (`MaxPacketSize`)
* **2.3 Routing and Segmentation**
  * 2.3.1 Directory Routing Topologies: Traffic Shaping Between Domain Controllers, NPS, and Clients
  * 2.3.2 Zero Trust Microsegmentation: Tier 0, Tier 1, and Tier 2 Network Isolation (NIST SP 800-207)
  * 2.3.3 Host-Based Access Control: Restricting Lateral Movement with Windows Defender Firewall Rules
* **2.4 Ports and Transport Dependencies**
  * 2.4.1 Core Port Matrix: Kerberos (88), RPC (135), LDAP/S (389/636), SMB (445), GC (3268/3269), NTP (123), RADIUS (1812/1813)
  * 2.4.2 Traffic Reconnaissance: Passive Sniffing and Active Service Scanning
  * 2.4.3 Defensive RPC Hardening: Restricting Dynamic RPC High-Port Ranges via Registry
* **2.5 Domain Name System (DNS)**
  * **2.5.1 AD-Integrated DNS**
    * 2.5.1.1 Multi-Master Replication, Partition Architecture (`DomainDnsZones`, `ForestDnsZones`), and ACL Delegation
  * **2.5.2 Service (SRV) Records**
    * 2.5.2.1 Active Directory Resource Locator Mechanics and Query Paths
  * **2.5.3 Dynamic Updates**
    * 2.5.3.1 Offensive Vector: Non-Secure DNS Record Overwriting (`adidnsdump`, `dnstool`)
    * 2.5.3.2 Defensive Configuration: Enforcing Secure Dynamic Updates Exclusively
* **2.6 Domain Name Resolution**
  * 2.6.1 Multicast/Broadcast Protocol Mechanics: LLMNR (5355), NBT-NS (137), mDNS (5353), and Dynamic Host Configuration Protocol Version 6 (DHCPv6)
  * 2.6.2 Offensive Vector: Broadcast Poisoning and Rogue IPv6 Delegation (`Responder`, `mitm6`, `Inveigh`)
  * 2.6.3 Defensive Hardening: Disabling Multicast Name Resolution and NetBIOS via GPO and Registry
* **2.7 Time Synchronization and the Network Time Protocol (NTP)**
  * 2.7.1 Kerberos Clock Skew Constraints: ± 5-Minute Tolerance windows (`MaxToleranceInMinutes`)
  * 2.7.2 Offensive Vector: Time Skew Injection, Replay Attacks, and Protocol Downgrades
  * 2.7.3  Defensive Configuration: Authoritative PDC Hierarchy NTP Sync Configuration
* **2.8 SMB and RPC**
  * 2.8.1 Transport Protocols: SMB v1/v2/v3 Security States and Dynamic RPC Interfaces
  * 2.8.2 Offensive Vector: Coerced Authentication and Authentication Relaying (`PetitPotam`, `ntlmrelayx`)
  * 2.8.3 Defensive Hardening: Mandatory SMB/LDAP Signing, SMB Encryption, and Channel Binding Tokens (CBT)
* **2.9 Network Access Authentication**
  * **2.9.1 RADIUS**
    * 2.9.1.1 Protocol Architecture (UDP 1812/1813), Shared Secrets, and Packet Header Structures
  * **2.9.2 Microsoft Network Policy Server (NPS)**
    * 2.9.2.1 RADIUS Policy Engine, Active Directory User Mapping, and Audit Logging
  * **2.9.3 TACACS+**
    * 2.9.3.1 Protocol Mechanics (TCP 49), Full-Payload Encryption, and Command Authorization
  * **2.9.4 IEEE 802.1X**
    * 2.9.4.1 Port-Based Network Access Control: Supplicant, Authenticator, and Authentication Server Interaction
* **2.10 Legacy Authentication Protocols**
  * **2.10.1 PAP**
    * 2.10.1.1 Plaintext Credentials and Packet Sniffing Risks
  * **2.10.2 CHAP**
    * 2.10.2.1 MD5 Challenge-Response Weaknesses and Offline Cracking
  * **2.10.3 MS-CHAP and MS-CHAPv2**
    * 2.10.3.1 Single DES Key Derivation Weaknesses (56-Bit Cipher Strength) and Challenge Cracking (`asleap`)
* **2.11 Extensible Authentication Protocols**
  * **2.11.1 EAP-MD5**
    * 2.11.1.1 Cleartext Hash Transport and Lack of Mutual Authentication
  * **2.11.2 LEAP**
    * 2.11.2.1 MS-CHAP Challenge Interception and Dictionary Attacks (`asleap`)
  * **2.11.3 EAP-TLS**
    * 2.11.3.1 High-Assurance Mutual Certificate Authentication (FICAM CAL-3 / FIPS 201 / PIV Integration)
    * 2.11.3.2 Certificate Validation: SAN, Client Auth EKU, and CRL/OCSP Checking
  * **2.11.4 PEAP**
    * 2.11.4.1 Protected EAP Outer TLS Tunneling
    * 2.11.4.2 Offensive Vector: Rogue Access Point / Evil Twin Deployment (`eaphammer`)
  * **2.11.5 EAP-TTLS**
    * 2.11.5.1 Outer TLS Tunnel with Legacy Inner Authentication (PAP, CHAP, MS-CHAPv2)
  * **2.11.6 EAP-FAST**
    * 2.11.6.1 Protected Access Credentials (PAC) Provisioning and Secure Tunneling
  * **2.11.7 EAP-GTC**
    * 2.11.7.1 Hardware/Software Token and One-Time Password (OTP) Integration
  * **2.11.8 EAP-SIM and EAP-AKA**
    * 2.11.8.1 Cellular-Based Identity Authentication in Hybrid Networks
  * **2.11.9 TEAP**
    * 2.11.9.1 Dual-Credential Tunnel Chaining (RFC 7170): Machine Certificate and User Credential Validation
* **2.12 User Versus Machine Authentication**
  * 2.12.1 Boot-Time Identity: Domain Computer Account Mechanics (`COMPUTER$`)
  * 2.12.2 Interactive Handoff: Single Sign-On (SSO) Transition to User Context
  * 2.12.3 Network Enforcement: Pre-Logon Access Control (PLAP) and Dynamic VLAN Assignment
* **2.13 Network Identity Trust Boundaries**
  * 2.13.1 Architecture: Tiered Subnet Enforcement (Tier 0 / Tier 1 / Tier 2 Isolation)
  * 2.13.2 FICAM and NIST Control Mapping: `IA-2`, `IA-5`, `SC-8`, `SC-13`
  * 2.13.3 Telemetry and Event Auditing: Log Analysis for Event ID 4624 (Logon Type 8), Event IDs 6272/6278 (NPS), and Event IDs 4768/4769 (Kerberos)
* **2.14 Preparing for Chapter 3**

\=/=/=/=/=/=/=/=/=/=/=/=/=/=/=/=/=

### <mark style="color:pink;">**Chapter 2 - Identity as the Battlefield**</mark>

* **2.1 From the Network Perimeter to the Identity Perimeter**
  * 2.1.1 Why the Internal Network Was Never a Complete Trust Boundary
  * 2.1.2 Authentication Became Portable
  * 2.1.3 Authorization Became More Important Than Simple Entry
  * 2.1.4 Identity Expanded Beyond the Human User
* **2.2 How Enterprise Identity Reached This Current Point**
  * 2.2.1 The Early Days of Windows NT Domains
  * 2.2.2 Novell NetWare and NDS/eDirectory
  * 2.2.3 X.500 and Directory-Service Concepts
  * 2.2.4 Windows 2000 and Active Directory
  * 2.2.5 Enterprise Adoption and Microsoft Integration Strategy
  * 2.2.6 Backward Compatibility and Identity Debt
* **2.3 Identity as the Federal Enterprise Control Plane**
  * 2.3.1 Authority Is Distributed Even When Administration Is Centralized
  * 2.3.2 Active Directory Does Not Need to Own a Resource to Control Access To It
  * 2.3.3 Administrative Control Exists Beyond Domain Admins
  * 2.3.4 Group Policy Extends Identity Authority Into System Configuration and Security Enforcement
  * 2.3.5 How Certificate and Federation Infrastructure Extend the Control Plane
* **2.4 Identity as an Attack Surface**
  * 2.4.1 Vulnerabilities and Identity Weaknesses Are Not The Same Thing
  * 2.4.2 Credentials Are Only One Part of the Identity Attack Surface
  * 2.4.3 Administrative Convenience Produces Security Reachability
  * 2.4.4 Legacy Compatibility Preserves Attack Surface
* **2.5 Trust Rather Than Network Location**
  * 2.5.1 Trust Can Cross Boundaries Without Removing Them
  * 2.5.2 Transitive Trust Extends Security Consequences
  * 2.5.3 Federation Separates Authentication From the Resource Boundary
  * 2.5.4 Certificates Move Trust Into Cryptographic Infrastructure
  * 2.5.5 Identity Trust Is Only as Strong as Its Upstream Authorities
* **2.6 Assume Breach as an Engineering Model**
  * 2.6.1 Compromise Should Not Automatically Become Trust
  * 2.6.2 Privileged Administration Changes Under Assume Breach
  * 2.6.3 Assume Breach Applies to Identity Systems Themselves
  * 2.6.4 Prevention Will Always Matter
* **2.7 Attack Pathways Rather Than Isolated Vulnerabilities**
  * 2.7.1 Identity Relationships Create Pathways
  * 2.7.2 Low-Severity Conditions Can Produce High-Impact Pathways
  * 2.7.3 Attack Pathways Often Cross Technology Boundaries
  * 2.7.4 Pathway Removal Is More Important Than Cosmetic Remediation
* **2.8 Authentication Is Not Authority**
  * 2.8.1 Strong Authentication Can Protect Excessive Privilege
  * 2.8.2 Authority Can Exist Without Obvious Privilege
  * 2.8.3 Authority Can Be Manufactured
  * 2.8.4 Authority as the More Durable Adversary Objective
* **2.9 The Identity Attack Chain Lifecycle**
  * 2.9.1 Why Real-World Intrusions Are Nonlinear
  * 2.9.2 Passive Reconnaissance
  * 2.9.3 Active Enumeration
  * 2.9.4 Initial Identity Acquisition
  * 2.9.5 Credential Acquisition
  * 2.9.6 Authority Expansion
  * 2.9.7 Enterprise Identity Mobility
  * 2.9.8 Persistence and Domain Dominance
* **2.10 Why Real Intrusions Are Nonlinear**

### <mark style="color:pink;">**Chapter 3 - The Federal Identity Trust System**</mark>

* **3.1 Active Directory as Mission Infrastructure**
  * 3.1.1 Authentication Availability Becomes Service Availability
  * 3.1.2 Directory Integrity Is Mission-Relevant Integrity
  * 3.1.3 Active Directory Supports Both Mission Users and Mission Administrators
  * 3.1.4 Identity Infrastructure Is Part of the Mission Dependency Map
* **3.2 The Domain Versus the Identity Trust System**
  * 3.2.1 Product Boundaries Are Not Security Boundaries
  * 3.2.2 Administrative Boundaries Can Differ From Trust Boundaries
  * 3.2.3 Authentication Boundaries Can Be Broader Than Directory Boundaries
  * 3.2.4 The Trusted Core Extends Beyond Domain Controllers
* **3.3 Components of the Federal Identity Trust System**
  * 3.3.1 Active Directory Domain Services (AD DS)
  * 3.3.2 Certificate and Public Key Infrastructure (PKI)
  * 3.3.3 Active Directory Federation Services (AD FS)
  * 3.3.4 Cloud Identity
  * 3.3.5 Identity Synchronization
  * 3.3.6 Privileged Identity Systems
  * 3.3.7 Authoritative Attribute Sources
* **3.4 Commercial Versus Federal Identity Active Directory Environments**
  * 3.4.1 Identity Is Often Governed Outside the Local System
  * 3.4.2 Formal Authorization Changes the Meaning of Evidence
  * 3.4.3 Mission Requirements Can Constrain Security Changes
  * 3.4.4 Federal Identity Security Requires Traceability
* **3.5 Federal and Military Enclaves**
  * 3.5.1 NIPRNet
  * 3.5.2 SIPRNet
  * 3.5.3 JWICS and National Security Systems (NSS)
  * 3.5.4 Tactical and Disconnected Environments
* **3.6 Cross-Domain Solutions and Identity**
  * 3.6.1 Cross-Domain Identity Is Not Considered Ordinary Domain Trust
  * 3.6.2 Attribute Integrity Becomes a Critical Component of Active Directory Infrastructure
  * 3.6.3 Identity Compromise Can Have Asymmetric Consequences
* **3.7 Mission-Partner and Coalition Identity**
  * 3.7.1 Federation Preserves Administrative Independence
  * 3.7.2 Partner Access Must Have a Lifecycle
  * 3.7.3 Mission-Partner Compromise Is a Shared Incident
* **3.8 Contractor-Operated and Shared Infrastructure**
  * 3.8.1 Administrative Authority Can Cross Contractual Boundaries
  * 3.8.2 Shared Services Concentrate Both Value and Dependency
* **3.9 Identity Dependencies and Mission Assurance**
  * 3.9.1 Hidden Dependencies Complicate Hardening
  * 3.9.2 Recovery Dependencies Must Be Identified Separately
* **3.10 Translating Identity Failure Into Operational Consequence**
  * 3.10.1 Technical Impact Is Not Yet Mission Impact
  * 3.10.2 Loss of Trust Can Exceed Loss of Availability
  * 3.10.3 Identity Security Is Mission Security When Mission Depends on Identity
* **3.11 Preparing for Chapter 4**

### <mark style="color:pink;">**Chapter 4 - Federal Cybersecurity Governance**</mark>

* **4.1 How Federal Cybersecurity Authority Flows**
  * 4.1.1 Authority Becomes More Specific as It Approaches the Technology
  * 4.1.2 The Same Technical Control May Serve Multiple Governance Purposes
  * 4.1.3 Governance Should Remain Traceable to Real Configuration
* **4.2 Legislative Authorities**
  * 4.2.1 FISMA
  * 4.2.2 National Security System Authorities
  * 4.2.3 Privacy and Information Protection Requirements
* **4.3 Executive Authorities**
  * 4.3.1 The White House and Executive Cybersecurity Direction
  * 4.3.2 Executive Orders as Leading Cybersecurity Catalysts
  * 4.3.3 Office of Management and Budget (OMB)
  * 4.3.4 Federal Zero Trust Direction
* **4.4 National Institute of Standards and Technology (NIST)**
  * 4.4.1 FIPS - Federal Information Processing Standard
  * 4.4.2 NIST Special Publications (SP)
  * 4.4.3 NIST Cybersecurity Framework (CSF)
  * 4.4.4 NIST SP 800-63: Digital Identity Guidance
* **4.5 Cybersecurity and Infrastructure Security Agency (CISA)**
  * 4.5.1 Binding Operational Directives
  * 4.5.2 Known Exploited Vulnerabilities
  * 4.5.3 Federal Civilian Identity Security
* **4.6 Department of Defense Governance**
  * 4.6.1 DoD Chief Information Officer
  * 4.6.2 Defense Information Systems Agency
  * 4.6.3 National Security Agency
  * 4.6.4 United States Cyber Command
  * 4.6.5 JFHQ-DoDIN
  * 4.6.6 Military Departments and Service Components
* **4.7 Federal Cloud and Contractor Governance**
  * 4.7.1 FedRAMP
  * 4.7.2 Defense Industrial Base
  * 4.7.3 Controlled Unclassified Information
  * 4.7.4 Contractor Identity Responsibilities
* **4.8 From Law to Technical Configuration**
  * 4.8.1 Law
  * 4.8.2 Policy
  * 4.8.3 Standards
  * 4.8.4 Security Controls
  * 4.8.5 Technical Security Baselines
  * 4.8.6 Active Directory Implementation
* **4.9 Preparing for Chapter 5**

### <mark style="color:pink;">**Chapter 5 - FICAM and DoD ICAM**</mark>

* **5.1  Introduction to Federal Identity, Credential, and Access Management (FICAM)**
  * 5.1.1 Identity Exists Before the Account
  * 5.1.2 Credentialing Is Not Authentication
  * 5.1.3 Access Management Begins After Authentication but Does Not Depend on Authentication Alone
  * 5.1.4 Federation Extends Trust Without Transferring Ownership
  * 5.1.5 Governance Determines Which Identity Facts Matter
* **5.2 Department of Defense ICAM (DoD ICAM)**
  * 5.2.1 Enterprise ICAM Does Not Eliminate Local Identity Engineering
  * 5.2.2 DoD ICAM Must Support Mission Partners
  * 5.2.3 Person Entities and Non-Person Entities (NPE)
  * 5.2.4 Local and Disconnected ICAM Are Deliberate Architectural Cases
* **5.3 The Identity Lifecycle**
  * 5.3.1 Sponsorship
  * 5.3.2 Identity Proofing
  * 5.3.3 Enrollment
  * 5.3.4 Credential Issuance
  * 5.3.5 Credential Binding
  * 5.3.6 Authentication
  * 5.3.7 Authorization
  * 5.3.8 Recertification
  * 5.3.9 Revocation and Deprovisioning
* **5.4 Digital Identity Assurance**
  * **5.4.1 Identity Assurance Levels**
    * 5.4.1.1 IAL1
    * 5.4.1.2 IAL2
    * 5.4.1.3 IAL3
  * **5.4.2 Authenticator Assurance Levels (AAL)**
    * 5.4.2.1 AAL1
    * 5.4.2.2 AAL2
    * 5.4.2.3 AAL3
  * **5.4.3 Federation Assurance Levels (FAL)**
    * 5.4.3.1 FAL1
    * 5.4.3.2 FAL2
    * 5.4.3.3 FAL3
  * 5.4.4 Legacy Levels of Assurance
* **5.5 Federal Credentials**
  * 5.5.1 Personal Identity Verification (PIV)
  * 5.5.2 Common Access Card (CAC)
  * 5.5.3 EDIPI and the DoD Identification Number
  * 5.5.4 Biometrics
  * 5.5.5 Derived Credentials
* **5.6 Identity Governance**
  * 5.6.1 Identity Governance Is the Control Against Identity Debt
  * 5.6.2 Identity State Must Follow the Authoritative Relationship
  * 5.6.3 Privileged Identity Requires Stronger Governance
* **5.7 Credential Governance**
  * 5.7.1 Strong Credentials Require Strong Enrollment
  * 5.7.2 Recovery Is Part of the Credential Security Model
  * 5.7.3 Credential Revocation Must Match Credential Diversity
* **5.8 Access Governance**
  * 5.8.1 Entitlement Should Express a Defensible Relationship
  * 5.8.2 Role-Based Access Is Useful but Not Automatically Least Privilege
  * 5.8.3 Effective Access Must Be Governed, Not Governed By Direct Access
  * 5.8.4 Separation of Duties Must Survive Indirect Control
* **5.9 Federation Governance**
  * 5.9.1 Federation Transfers an Identity Decision, Not Unlimited Authority
  * 5.9.2 Trust Agreements = Security Architecture
  * 5.9.3 Federation Expands the Consequence of Signing-Key Compromise
  * 5.9.4 Federation Governance Must Include Failure
* **5.10 Authoritative Attributes**
  * 5.10.1 Authoritative Does Not Mean Universally Authoritative
  * 5.10.2 Attribute Provenance Is a Security Property
  * 5.10.3 Synchronization Creates Copies but Should Not Create Ambiguity
  * 5.10.4 Attribute Manipulation Can Become Privilege Escalation
* **5.11 Person Entities and Non-Person Entities (NPE)**
  * 5.11.1 Person Identity Has a Natural Authoritative Relationship
  * 5.11.2 Every NPE Needs an Accountable Human or Mission Owner
  * 5.11.3 NPE Credentials Behave Differently From Human Credentials
  * 5.11.4 NPE Privilege Can Be Difficult to See
  * 5.11.5 Machine Identity Is More Than a Computer Object
  * 5.11.6 Workload Identity Changes the Scale of Identity Governance
* **5.12 Mission-Partner Identity Governance**
  * 5.12.1 Mission Trust Should Be Narrower Than Identity Trust
  * 5.12.2 Identity Translation Can Become a Security Boundary
  * 5.12.3 Sponsorship Provides Local Accountability for External Identity
  * 5.12.4 Partner Trust Requires an Incident Path
  * 5.12.5 Federation Failure Must Not Become Mission Paralysis
* **5.13 FICAM, DoD ICAM, and Zero Trust**
  * 5.13.1 Zero Trust Depends on Authoritative Identity
  * 5.13.2 Strong Authentication Is Necessary but Not Sufficient
  * 5.13.3 Device Identity Becomes Part of Access Trust
  * 5.13.4 Continuous Evaluation Changes the Meaning of a Session
  * 5.13.5 Zero Trust Does Not Eliminate the Trusted Core
  * 5.13.6 FICAM Provides the Identity Discipline Zero Trust Requires
* **5.14 Prepar-ing for Chapter 6**

### <mark style="color:pink;">**Chapter 6 - Risk Management Framework (RMF), Security Baselines, and Authorization Evidence**</mark>

* **6.1 Risk Management Framework**
  * 6.1.1 Step 1 - Prepare
  * 6.1.2 Step 2 - Categorize
  * 6.1.3 Step 3 - Select
  * 6.1.4 Step 4 - Implement
  * 6.1.5 Step 5 - Assess
  * 6.1.6 Step 6 - Authorize
  * 6.1.7 Step 7 - Monitor
* **6.2 Identity as a Common Control Provider**
  * 6.2.1 Common Identity Services Concentrate Assurance
  * 6.2.2 Common Control Does Not Mean Complete Control
  * 6.2.3 Common Control Failure Is a Shared-Risk Event
* **6.3 Control Inheritance and Shared Services**
  * 6.3.1 Inheritance Should Follow Technical Responsibility
  * 6.3.2 Shared Services Create Boundary Interfaces
  * 6.3.3 Inherited Risk Must Reach the Authorizing Official
* **6.4 Identity Risk Within RMF**
  * 6.4.1 Authentiation Risk
  * 6.4.2 Authorization Risk
  * 6.4.3 Credential Risk
  * 6.4.4 Federation Risk
  * 6.4.5 Privileged Access Risk
* **6.5 DISA STIGs and SRGs**
  * 6.5.1 Baselines Establish the Expected State
  * 6.5.2 Baselines Must Distinguish Requirement From Implementation
  * 6.5.3 Baseline Deviations Are Risk Decisions
  * 6.5.4 Identity Baselines Must Include Relationships
  * 6.5.5 STIG Findings Must Be Interpreted Through Identity Criticality
  * 6.5.6 Applicability Must Be Defensible
  * 6.5.7 Automation Does Not Eliminate Engineering Judgment
  * 6.5.8 STIG Evidence Should Support RMF Rather Than Become a Separate Compliance Universe
* **6.6 Microsoft Security Baselines**
  * 6.6.1 Microsoft Baselines Represent Vendor-Recommended Secure Configuration
  * 6.6.2 The Security Compliance Toolkit
  * 6.6.3 Baseline Comparison Should Precede Deployment
  * 6.6.4 Windows Server 2025 Introduces Role-Aware Baseline Management Through OSConfig
  * 6.6.5 Microsoft Baselines and DISA STIGs Should Be Compared, Not Blended Blindly
  * 6.6.6 Baseline Versioning Importance
  * 6.6.7 Baseline Drift Is an Identity Security Problem
  * 6.6.8 Domain Controller Baselines Protect the Platform, Not the Entire Domain
  * 6.6.9 Baselines Should Become Layered Engineering Artifacts
* **6.7 Vulnerability Management, IAVAs, and Identity Risk**
  * **6.7.1 Information Assurance Vulnerability Alerts (IAVAs)**
    * 6.7.1.1 Identity-Centric IAVAs Can Affect More Than Domain Controllers
    * 6.7.1.2 IAVA Prioritization Must Follow the Control Plane
    * 6.7.1.3 Patching Does Not Automatically Close the Identity Exposure
    * 6.7.1.4 Verification Must Include Service Health and Security State
  * **6.7.2 Operational Vulnerability Response**
    * 6.7.2.1 Triage Begins With Exploitability and Reach
    * 6.7.2.2 Identity Systems Require Dependency-Aware Remediation
    * 6.7.2.3 Emergency Change Control Must Move Faster Without Becoming Sloppy
    * 6.7.2.4 Compensating Controls Need to Reduce a Real Attack Opportunity
    * 6.7.2.5 SOC and Engineering Operations Need a Shared Picture
    * 6.7.2.6 Suspected Exploitation Changes the Mission
    * 6.7.2.7 Containment Must Preserve Evidence and Mission Capability
    * 6.7.2.8 Recovery Means More Than Returning the Server to Service
    * 6.7.2.9 Post-Remediation Validation Must Test the Mission Path
    * 6.7.2.10 Vulnerability Closure Should Leave an Evidence Trail
    * 6.7.2.11 Lessons Learned Should Modify the Environment
* **6.8 eMASS and Authorization Evidence**
  * **6.8.1 Control Implementation Evidence**
    * 6.8.1.1 Evidence Must Describe the Environment That Actually Exists
  * **6.8.2 Assessment Evidence**
    * 6.8.2.1 Control Implementation Statements Should Be Technically Testable
  * **6.8.3 Authorization Artifacts**
* 6.9 Plans of Action and Milestones (POA\&Ms)
* 6.10 Continuous Monitoring
* 6.11 Continuous Diagnostics and Mitigation
* 6.12 Vulnerability and Patch Management
* 6.13 CCRI and CORA Readiness
* 6.14 Inspector General (IG) and Assessment Findings
* 6.15 Configuration Drift
* 6.16 Strategic Security Testing and Evaluation (ST\&E)
* 6.17 Mission-Aware Change Control (MACC)
* **6.18 Preparing for Chapter 7**

## PART II - Identity Infrastructure and Active Directory Architecture

### Chapter 7 - Identity Infrastructure Networking

* **7.1 Why Identity Depends on the Network**
  * 7.1.1 Network Transport Dynamics: Kerberos, NTLM, RADIUS, and LDAP/S as Network Payloads
  * 7.1.2 Threat Modeling: On-Path and Man-in-the-Middle (MitM) Adversary Capabilities
  * 7.1.3 FICAM Alignment: Impact of Transport Interception on Credential Assurance Levels (CAL)
* **7.2 TCP/IP Foundations for Identity Services**
  * 7.2.1 Transport Dynamics: TCP Versus UDP Behaviors for Kerberos, DNS, and LDAP
  * 7.2.2 Kerberos MTU and Packet Fragmentation: Handling `KRB_ERR_RESPONSE_TOO_BIG`
  * 7.2.3 **Defensive Configuration**: Enforcing Kerberos Over TCP via Registry (`MaxPacketSize`)
* **7.3 Routing and Segmentation**
  * 7.3.1 **Directory Routing Topologies**: Traffic Shaping Between Domain Controllers, NPS, and Clients
  * 7.3.2 **Zero Trust Microsegmentation**: Tier 0, Tier1, and Tier 2 Network Isolation (NIST SP 800-207)
  * 7.3.3 **Host-Based Access Control**: Restricting Lateral Movement with Windows Defender Firewall Rules
* **7.4 Network Ports and Transport Dependencies**
  * 7.4.1 **Core Port Matrix**: Kerberos (88), RPC (135), LDAP/S (389/636), SMB (445), GC (3268/3269), NTP (123), RADIUS (1812/1813)
  * 7.4.2 **Network Traffic Reconnaissance**: Passive Sniffing and Active Service Scanning
  * 7.4.3 **Defensive RPC Hardening**: Restricting Dynamic RPC High-Port Ranges via Registry
* **7.5 Domain Name System**
  * **7.5.1 AD-Integrated DNS**
    * 7.5.1.1 Multi-Master Replication, Partition Architecture (`DomainDnsZones`, `ForestDnsZones`), and ACL Delegation
  * **7.5.2 DNS Service Locator (SRV) Records**
    * 7.5.2.1 Active Directory Resource Locator Mechanics and Query Paths
  * **7.5.3 Dynamic Updates**
    * 7.5.3.1 Offensive Vector: Non-Secure DNS Record Overwriting (`adidnsdump`, `dnstool`)
    * 7.5.3.2 Defensive Configuration: Enforcing Secure Dynamic Updates Exclusively
  * **7.5.4 Name Resolution**
    * 7.5.4.1 Multicast/Broadcast Protocol Mechanics: LLMNR (5355), NBT-NS (127), mDNS (5353), and DHCPv6
    * 7.5.4.2 Offensive Vector: Broadcast Poisoning and Rogue IPv6 Delegation (`Responder`, `mitm6`, `Inveigh`)
    * 7.5.4.3 Defensive Hardening: Disabling Multicast Resolution and NetBIOS via GPO and Registry
* **7.6 Time Synchronization and the Network Time Protocol (NTP)**
  * 7.6.1 Kerberos Clock Skew Constraints: ±5-Minute Tolerance Window (`MaxToleranceInMinutes`)
  * 7.6.2 Offensive Vector: Time Skew Injection, Replay Attacks, and Protocol Downgrades
  * 7.6.3 Defensive Configuration: Authoritative PDC Hierarchy NTP Sync Configuration
* **7.7 SMB and RPC**
  * 7.7.1 Network Transport Protocols: SMB v1/v2/v3 Security States and Dynamic RPC Interfaces
  * 7.7.2 Offensive Vector: Coerced Authentication and Authentication Relaying (PetitPotam, `ntlmrelayx`)
  * 7.7.3 Defensive Hardening: Mandatory SMB/LDAP Signing, SMB Encryption, and Channel Binding Tokens (CBT)
* **7.8 Network Access Authentication**
  * **7.8.1 RADIUS**
    * 7.8.1.1 Protocol Architecture (UDP 1812/1813), Shared Secrets, and Packet Header Structures
  * **7.8.2 Microsoft Network Policy Server (NPS)**
    * 7.8.2.1 RADIUS Policy Engine, Active Directory User Mapping, and Audit Logging
  * **7.8.3 TACACS+**
    * 7.8.3.1 Protocol Mechanics (TCP 49), Full-Payload Encryption, and Command Authorization
  * **7.8.4 IEEE 802.1X**
    * 7.8.4.1 Port-Based Network Access Control (NAC): Supplicant, Authenticator, and Authentication Server Interaction
* **7.9 Legacy Authentication Protocols**
  * **7.9.1 PAP**
    * 7.9.1.1 Plaintext Credentials and Packet Sniffing Risks
* **7.9.2 CHAP**
  * 7.9.2.1 MD5 Challenge-Response Weaknesses and Offline Cracking
* **7.9.3 MS-CHAP and MS-CHAPv2**
  * 7.9.3.1 Single DES Key Derivation Weaknesses (56-Bit Cipher Strength) and Challenge Cracking (`asleap`)
* **7.10 Extensible Authentication Protocols (EAP)**
  * **7.10.1 EAP-MD5**
    * 7.10.1.1 Cleartext Hash Transport and Lack of Mutual Authentication
* **7.10.2 LEAP**
  * 7.10.2.1 MS-CHAP Challenge Inspection and Dictionary Attacks (`asleap`)
    * 7.10.2.1.1 `asleap -r leap_capture.pcap -f /usr/share/wordlists/rockyou.txt`
* **7.10.3 EAP-TLS**
  * 7.10.3.1 High-Assurance Mutual Certificate Authentication (FICAM CAL-3 / FIPS 201 / PIV Integration)
  * 7.10.3.2 Certificate Validation: SAN, Client Auth EKU, and CRL/OCSP Checking
* **7.10.4 PEAP**
  * 7.10.4.1 Protected EAP Outer TLS Tunneling
  * 7.10.4.2 Offensive Vector: Rogue Access Point / Evil Twin Deployment via `eaphammer`
* **7.10.5 EAP-TTLS**
  * 7.10.5.1 Outer TLS Tunnel with Legacy Inner Authentication (PAP, CHAP, MS-CHAPv2)
* **7.10.6 EAP-FAST**
  * 7.10.6.1 Protected Access Credentials (PAC) Provisioning and Secure Tunneling
* **7.10.7 EAP-GTC**
  * 7.10.7.1 Hardware/Software Token and One-Time Password (OTP) Integration
* **7.10.8 EAP-SIM and EAP-AKA**
  * 7.10.8.1 Cellular-Based Identity Authentication in Hybrid Networks
* **7.10.9 TEAP**
  * 7.10.9.1 Dual-Credential Tunnel Chaining (RFC 7170): Machine Certificate and User Credential Validation
* **7.10.10 User Versus Machine Authentication**
  * 7.10.10.1 Boot-Time Identity: Domain Computer Account Mechanics (`COMPUTER$`)
  * 7.10.10.2 Interactive Handoff: Single Sign-On (SSO) Transition to User Context
  * 7.10.10.3 Network Enforcement: Pre-Logon Access Control (PLAP) and Dynamic VLAN Assignment
* **7.11 Network Identity Trust Boundaries**
  * 7.11.1 Architecture: Tiered Subnet Enforcement (Tier 0 / Tier 1 / Tier 2 Isolation)
  * 7.11.2 FICAM and NIST Control Mapping: `IA-2`, `IA-5`, `SC-8`, `SC-13`
* 7.11.3 Telemetry and Event Auditing: Log Analysis for Event ID 4624 (Logon Type 8), Event IDs 6272/6278 (NPS), and Event IDs 4768/4769 (Kerberos)

### Chapter 8 - The Architecture of Authority

* **8.1 Active Directory Forests**
  * 8.1.1 Root Authority and Schema Control: The Forest as the True Security and Cryptographic Boundary
  * 8.1.2 Forest Root Domain: Criticality of the Primary Domain Controller Emulator (ePDC) and Schema Master
  * 8.1.3 Forest-Wide Scope: Global Catalog (GC) Replication, Enterprise Admins (EA), and Schema Admins
  * 8.1.4 Reconnaissance and Hardening: Mapping Forest Topologies (BloodHound) and Tier 0 Group Membership Restrictions
  * 8.1.5 Defensive Configuration: Tier 0 Forest Hardening and Restricting EA Group Membership
* **8.2 Active Directory Trees**
  * 8.2.1 Disjoint and Contiguous Namespaces: Structural Tree Hierarchies Within a Single Forest
  * 8.2.2 Kerberos Transit Paths: Automatic Two-Way Transitive Parent-Child Kerberos Trust Chains
  * 8.2.3 Offensive Vector: Intra-Forest Child-to-Parent Escalation via SID History and Enterprise Key Extraction via `mimikatz`
  * 8.2.4 Defensive Configuration: Enforcing SID Filtering and Selective Authentication on Internal Trust Paths
* **8.3 Active Directory Domains**
  * 8.3.1 Administrative Partitioning: Replication, Policy, and Database (`NTDS.dit`) Isolation Limits
  * 8.3.2 Domain Controllers: FSMO Roles (RID Master, Infrastructure Master, PDC Emulator), and KDC Architecture
  * 8.3.3 Offensive Vector: Domain Controller Takeover via Coerced Authentication and DCSync
  * 8.3.4 Defensive Configuration: Domain Isolation Policy and Tier 0 Domain Controller Hardening
* **8.4 Active Directory Organizational Units (OU)**
* 8.4.1 Logical Structuring: Administrative Delegation, Group Policy Object (GPO) Application, and Asset Grouping
* 8.4.2 ACL Delegation & Inheritance: Explicit vs. Inherited Access Control Entries (ACEs) on OU Containers
* 8.4.3 Offensive Vector: Abusing Delegated OU Permissions (`GenericAll`, `WriteDACL`) Over User/Computer Objects
* 8.4.3.1 `Get-DomainOU | Get-DomainAcl -ResolveGUIDs | ? {$_.IdentityReference - match "TargetUser"}`
* 8.4.3.2 `bloodyAD --host dc01.domain.local -u user -p pass add genericAll --tar -get "OU=Workstations,DC=domain,DC=local"`
* 8.4.4 Defensive Hardening: Auditing OU DACLs, Enforcing Block GPO Inheritance, and Applying Least Privilege Delegation
* 8.5 Active Directory Sites and Administrative Topology
* 8.5.1 Physical Network Mapping: IP Subnet Associations, Site Objects, and Site Links
* 8.5.2 Replication Topology: Knowledge Consistency Checker (KCC) and Inter-Site Topology Generator (ISTG)
* 8.5.3 Offensive Vector: Rogue Site Association and Client Subnet Hijacking for Credential Interception
* 8.5.4 Defensive Configuration: Audit and Clean Up Unassigned Subnets via Active Directory Sites and Services (`dssite.msc`)
* 8.6 Active Directory Naming Boundaries
* 8.6.1 Namespace Architecture: Fully Qualified Domain Name (FQDN), NetBIOS, and User Principal Names (UPNs)
* 8.6.2 X.500 and LDAP Pathing: Distinguished Names (DN), Relative Distinguished Names (RDN), and Canonical Names (CN)
* 8.6.3 Offensive Vector: UPN Spoofing and Kerberos Service Principal Names (SPN) Aliasing Attacks
* 8.6.4 Defensive Configuration: Restricting UPN Suffix Routing and Enforcing Unique SPN Validation
* 8.7 Active Directory Authentication Boundaries
* 8.7.1 Kerberos and NTLM Scope: Authentication Realm Issuance and Ticket Granting Ticket (TGT) Boundaries
* 8.7.2 Cross-Boundary Authentication: Referral Tickets (`KRB_TGT_REP`) Across Domain Trees
* 8.7.3 Offensive Vector: Cross-Domain Kerberoasting and AS-REP Roasting via Impacket
* 8.7.4 Defensive Configuration: Disabling NTLM Across Domain Boundaries and Enforcing AES-256 Kerberos Encryption Only
* **8.8 Active Directory Administrative Boundaries**
* 8.8.1 **Delegation Models**: Task Delegation Wizard, Built-In Administrative Groups, and Custom Roles
* 8.8.2 **AdminSDHolder and SDProp**: Protection Mechanics for High-Privilege Domain Accounts
* 8.8.3 **Offensive Vector**: Abusing ACL Inheritance Flaws and Persistence via AdminSDHolder DACL Modification
* 8.8.4 **Defensive Hardening**: Protecting AdminSDHolder, Clearing Unauthorized ACEs, and Monitoring SDProp Execution
* **8.9 Active Directory Security Boundaries**
  * 8.9.1 **The Forest Boundary Law**: Why the Forest is the Only True Security Boundary in Active Directory
  * 8.9.2 **Domain Boundary Fallacy**: Mechanics of Transitive Trust Exploitation and Cross-Domain Admin Escalation
  * 8.9.3 **FICAM Alignment**: Mapping Forest Security Boundaries to FICAM CAL-3 and FIPS 201 Control Standards
  * 8.9.4 **Defensive Architecture**: Deploying Isolated Red Forests (ESAE / Privileged Access Forests) or Zero Trust Workload Enclaves
* **8.10 Why Logical Structure Does Not Equal Effective Control**
  * 8.10.1 **Structural Pitfalls**: Conflating OU Hierarchies with Security Isolation
  * 8.10.2 **Implicit Trust Relationships**: GPO Link Overrides, Cross-OU Service Account Usage, and Shared Local Admin Credentials
  * 8.10.3 **Offensive Vector**: Mapping Implicit Control Paths and Indirect Privilege Escalation with BloodHound Cypher Queries
  * 8.10.4 **Defensive Blueprint**: Transitioning from Logical Hierarchies to Strict Administrative Tiering (Tier 0 / Tier 1 / Tier 2)
  * 8.10.5 **FICAM and NIST Control Mapping**: `AC-2` (Account Management), `AC-3` (Access Enforcement), `AC-6` (Least Privilege), `SC-7` (Boundary Protection)
  * 8.10.6 **Telemetry and Event Auditing**: Log Analysis for Event ID 4670 (Permissions Changed), Event ID 4738 (User Account Modified), and Event ID 5136 (Directory Object Modified)

### Chapter 9 - The Active Directory Object Model and Schema

* **9.1 Directory Objects**
  * 9.1.1 **Object-Oriented Architecture**: Representation of Physical and Logical Entities in LDAP
  * 9.1.2 **Directory Instances**: Object Instantiation from Schema Definitions Inside `NTDS.dit`
  * 9.1.3 **Object Class Categorization**: Structural, Abstract, and Auxiliary Object Classes
* **9.2 Object Classes**
  * 9.2.1 **Class Hierarchy**: Inheritance Tree Rooted at Top
  * 9.2.2 **Class Schemas**: `classSchema` Definition Objects and Structural Rules
  * 9.2.3 **Class Types**: Structural Classes (Users, Computers), Auxiliary Classes (Security Enhancements), and Abstract Classes
* **9.3 Attributes**
  * 9.3.1 **Attribute Definitions**: `attributeSchema` Objects and Attribute Properties
  * 9.3.2 **Data Syntaxes and Constraints**: Single-Valued Versus Multi-Valued Attributes, Unicode Strings, Octet Strings, and Integer Types
  * 9.3.3 **Specialized Attribute Types**: Indexed Attributes, Confidential Attributes (`SEARCH_FLAGS = 128`), and RODC-Filtered Attribute Sets (FAS)
  * 9.3.4 **Global Catalog Scope**: Partial Attribute Set (PAS) Marking (`IsMemberOfPartialAttributeSet`)
* **9.4 Distinguished Names**
  * 9.4.1 **X.500 LDAP Pathing**: Fully Qualified Directory Paths (`CN=User,OU=Execs,DC=domain,DC=local`)
  * 9.4.2 **Object Binding**: Uniquely Identifying Objects Across Naming Contexts
  * 9.4.3 **Directory Operations**: Relocation and Rename Impacts on Distinguished Name (DN) Paths
* **9.5 Relative Distinguished Names (RDN)**
  * 9.5.1 **Leaf Node Naming**: RDN Structure (`CN=JohnDoe`) Within Parent Containers
  * 9.5.2 **Naming Constraints**: Character Escaping and Length Limits
  * 9.5.3 **Collision Handling**: Disambiguation Mechanics During Directory Object Creation and Multi-Master Replication
* **9.6 GUIDs and ObjectGUID**
  * 9.6.1 **Immutable Identification**: 128-Bit Universally Unique Identifiers (`objectGUID`)
  * 9.6.2 **Persistence Across Operations**: Tracking Objects Independent of Renames, Domain Moves, or Container Transfers
  * 9.6.3 **Offensive and Defensive Utility**: Binding BloodHound Telemetry and Access Control Entries (ACEs) to `objectGUID` Identifiers
* **9.7 Security Identifiers (SID)**
  * 9.7.1 **SID Structure**: Revision Level, Identifier Authority, Sub-Authorities, and Relative Identifier (RID)
  * 9.7.2 **Identity Mapping**: Resolving `sAMAccountName` to Security Identifiers for Access Control Checks
  * 9.7.3 **Well-Known SIDs**: Universal SIDs (`S-1-5-32-544` - Administrators, `S-1-5-18` - Local System)
  * 9.7.4 **Offensive Vector**: SID History (`sAMAccountType / sIDHistory`) Injection for Cross-Domain Privilege Escalation via `mimikatz`
  * 9.7.5 **Defensive Hardening**: Auditing `sIDHistory` Attributes and Enforcing SID Filtering Across Trust Boundaries
* **9.8 User Principal Names (UPN)**
  * 9.8.1 **Identity Formatting**: Enterprise User Identity Naming (`user@domain.local`)
  * 9.8.2 **UPN Types**: Implicit UPNs (Default `sAMAccountName@FQDN`)Versus Explicit UPNs
  * 9.8.3 **Routing Boundaries**: Alternative UPN Suffixes for Federated Identity and Multi-Forest Alignment (FICAM CAL Alignment)
* **9.9 Service Principal Names (SPN)**
  * 9.9.1 **Kerberos Service Binding**: Associating Unique Services with Active Directory Accounts (`service/host:port`)
  * 9.9.2 **SPN Syntax and Mechanics**: Host-Based SPNs, Service Accounts, and Unique SPN Enforcements
  * 9.9.3 **Offensive Vector**: SPN Enumeration and Kerberoasting Target Acquisition (`Impacket`, `Rubeus`)
  * 9.9.4 **Defensive Hardening**: Enforcing Group Managed Service Accounts (gMSA) and Long/Complex Passwords on SPN Accounts
* **9.10 Naming Contexts**
  * 9.10.1 **Directory Partitioning**: Logical Division of `NTDS.dit` for Targeted Replication
  * 9.10.2 **Cross-Reference Objects**: Cross-Domain and Cross-Partition Routing (`crossRef` Objects)
* **9.11 Domain Partition**
  * 9.11.1 **Directory Contents**: Users, Computers, Groups, OUs, and Domain-Specific GPOs
  * 9.11.2 **Replication Boundary**: Scope and Transport Dynamics Across Domain Controllers
* **9.12 Schema Partition**
  * 9.12.1 **Directory Contents**: Forest-Wide Object Class and Attribute Definitions
  * 9.12.2 **Control Scope**: Schema Master FSMO Role Authorization and Single-Master Replication
* **9.13 Application Partitions**
  * 9.13.1 **Custom Storage**: Non-Domain Data Partitioning and Selective Replication Topologies
  * 9.13.2 **DNS Partitions**: `DomainDnsZones` and `ForestDnsZones` Integration
  * 9.13.3 **Offensive Vector**: Storage of Rogue Objects or Data Staging Inside Custom Application Partitions
* **9.14 Schema Architecture**
  * 9.14.1 **Structural Blueprint**: Rules Governing Database Record Creation and Validation
  * 9.14.2 **Class Dependencies**: Mandatory Attributes (`mustContain`) and Optional Attributes (`mayContain`)
  * 9.14.3 **Object Identifiers (OIDs)**: Standardized ISO/ITU Naming Structure for Custom Schema Elements
* **9.15 Schema Extensions**
  * 9.15.1 **Modifying Directory Physics**: Adding Custom Classes, Attributes, or Extending Existing Objects
  * 9.15.2 **Enterprise Extensions**: Microsoft Exchange, LAPS (`ms-MCSF-SASUClearTextPassword`), and PKI Schema Modifications
  * 9.15.3 **Offensive Vector**: Schema Poisoning, Backdoor Attribute Creation, and Covert Data Storage
  * 9.15.4 **Defensive Hardening**: Restricting Schema Admins Group Membership, Enforcing Change Control, and Auditing Schema Modifications
* **9.16 Directory Metadata**
  * 9.16.1 **Attribute Tracking**: Attribute-Level Change Tracking via `msDS-ReplAttributeMetaData`
  * 9.16.2 **Sequence Numbers**: Update Sequence Numbers (USN) and Vector State Tracking
  * 9.16.3 **Originating Versus Replicated Updates**: Tracking Source Domain Controllers via `invocationDI` and Version Counters
* **9.17 Authoritative Directory State**
  * 9.17.1 Object Deletion Lifecycle: Active State, Tombstone State, and Recycled State (AD Recycle Bin)
  * 9.17.2 Replication Synchronization: High-Water Marks and Up-To-Dateness Vector Tables
  * 9.17.3 Restoration Mechanics: Authoritative Versus Non-Authoritative Restores
  * 9.17.4 Threat Mitigation: Detecting USN Rollback, Database Corruption, and Covert Object Restoration
  * 9.17.5 FICAM and NIST Control Mapping: `IA-2` (Identification), `AC-2` (Account Management), `SI-7` (Software, Firmware, and Information Integrity)
  * 9.17.6 Telemetry and Event Auditing: Audit Logging for Event ID 5136 (Directory Service Object Modified), Event ID 5137 (Directory Object Created), and Event ID 5141 (Directory Object Deleted)

### Chapter 10 - Domain Controllers, Replication, and Directory State

*

    #### 10.1 Domain Controller Roles

    * Core Identity Services: Active Directory Domain Services (AD DS), Key Distribution Center (KDC), and Local Security Authority (LSA) Interaction
    * Identity Infrastructure Anchor: Authenticating Users, Computers, and Services Across Enterprise Boundaries

    #### 10.2 Writable Domain Controllers

    * Full Database Authority: Multi-Master Replication and Write-Capable Directory Operations
    * High-Value Target Profile: Tier 0 Security Boundary Requirements and Administrative Isolation Models

    #### 10.3 Read-Only Domain Controllers

    * Edge & Branch Deployment: Unidirectional Replication Architecture and Read-Only Database Isolation
    * Password Replication Policy (PRP): Deny/Allow Lists for Credential Caching
    * Offensive Vector: RODC Credential Cache Dumping and Abusing Weak PRP Rules (`Impacket`)
    * Defensive Hardening: Restricting Administrative Account Caching and Enforcing Strict PRP Auditing

    #### 10.4 Global Catalogs

    * Forest-Wide Directory Indexing: Universal Group Membership Resolution and Partial Attribute Set (PAS)
    * Authentication Dependencies: Inter-Domain User Principal Name (UPN) Resolution and Global Directory Searches

    #### 10.5 FSMO Roles

    * Single-Master Operations: Flexible Single Master Operation Role Distributing (Schema Master, Domain Naming Master, RID Master, PDC Emulator, Infrastructure Master)
    * System Criticality: Impact of FSMO Role Availability on Domain Stability and Authentication Mechanics
    * Offensive Vector: FSMO Role Hijacking and PDC Emulator Exploitation

    #### 10.6 Knowledge Consistency Checker (KCC)

    * Automated Topology Generation: Dynamic Intra-Site and Inter-Site Replication Link Calculation
    * Spanning Tree Architecture: Dual-Ring Topology and Route Optimization for Directory Updates

    #### 10.7 Replication Topology

    * Directory Synchronization Routes: Intersite Topology Generator (ISTG), Site Links, and Bridgehead Server Design
    * Transport Protocols: RPC over IP (`TCP 135/49152+`) vs. Asynchronous SMTP Transport
    * Offensive Vector: DCSync Operations via Directory Replication Service (DRS) RPC Protocol (`DSGetNCChanges`) (`Mimikatz`)
    * Defensive Hardening: Auditing Directory Service Access Control Entries (ACEs) for Replication Rights (`DS-Replication-Get-Changes-All`)

    #### 10.8 Update Sequence Numbers

    * Monotonic Counter Mechanics: Attribute-Level Tracking of Database Modifications per DC
    * State Synchronization: Local USN vs. High-Watermark Vectors Across Replication Partners
    * Offensive & Defensive Vector: USN Rollback Detection and Virtualization Snapshot Recovery Hazards

    #### 10.9 Invocation IDs

    * Database Identity Tracking: Uniquely Identifying Database Instances Independent of Domain Controller GUIDs
    * State Reset Mechanics: Invocation ID Reset Operations Following Authoritative Restores or Virtual Machine Rollbacks

    #### 10.10 Replication Metadata

    * Attribute-Level Vector Tracking: Originating Change Time, Version Counters, and Originating DC Invocation ID
    * Conflict Resolution: Last-Writer-Wins Algorithms and Deterministic Attribute Value Conflict Handling

    #### 10.11 Tombstones and Deleted Objects

    * Deletion Lifecycle: Soft Deletes, Tombstone Lifetime (`tombstoneLifetime`), and Recycled Object States
    * Deleted Objects Container: Object Stripping and Preservation of Core Identification Attributes

    #### 10.12 Lingering Objects

    * Replication Inconsistency: Obsolete Objects Retained on DCs Disconnected Beyond Tombstone Lifetimes
    * Security Exposure: Re-animation Risks and Unauthorized Access via Out-of-Sync Objects
    * Defensive Configuration: Enforcing Strict Replication Consistency Across All Domain Controllers

    #### 10.13 Replication Consistency

    * Directory State Uniformity: Monitoring Convergence and Attribute Synchronization Health
    * Auditing Tools: Validating Replication Health (`repadmin`, `Get-ADReplicationPartnerMetadata`)

    #### 10.14 NTDS.dit

    * Database Anatomy: Structural Layout of the Active Directory JET Database Engine
    * Core Database Tables: Data Table, Link Table, Security Descriptor Table, and SD Prop Table
    * Offensive Vector: Offline Database Extraction via Volume Shadow Copy Service (VSS) or Disk Parsing (`ntdsutil`, `vssadmin`, `secretsdump`)
    * Defensive Hardening: BitLocker Drive Encryption, VSS Access Restrictions, and Credential Guard Implementation

    #### 10.15 Extensible Storage Engine

    * JET Blue Engine Physics: Page Allocation, B-Trees, Record Layouts, and Indexing Algorithms
    * Database Performance: Caching Mechanics in System RAM (LSASS Memory Pressure)

    #### 10.16 Transaction Logs

    * ACID Compliance: Write-Ahead Logging (`edb.log`), Checkpoint Files (`edb.chk`), and Reserve Logs
    * Database Integrity: Crash Recovery Mechanics and Transaction Roll-Forward Operations

    #### 10.17 Registry Hives

    * System Secret Anchors: Role of the `SYSTEM`, `SECURITY`, and `SOFTWARE` Hives on DCs
    * LSA Secrets Storage: Local Security Authority Storage of Service Credentials, DPAPI Master Keys, and Machine Account Secrets

    #### 10.18 BootKey and Password Encryption Key (PEK)

    * Cryptographic Architecture: SYSKEY/BootKey Extraction from the `SYSTEM` Registry Hive
    * PEK Decryption Physics: Utilizing BootKey to Decrypt the PEK, Unlocking Encrypted NTLM Hashes and Kerberos Keys in `NTDS.dit`
    * Offensive Vector: Offline PEK Decryption and Full-Forest Hash Extraction
    * Defensive Hardening: Tier 0 Physical and Hypervisor-Level Access Protections

    #### 10.19 Directory Backup and Recovery Metadata

    * System State Backup Architecture: Cryptographic Binding of Database, Registry Hives, SYSVOL, and Certificate Data
    * DSRM Security: Directory Services Restore Mode Account Hardening and Local Account Passwords (`NTDSettings`)
    * Offensive Vector: Abusing DSRM Accounts for Persistent Administrative Access (`DSRMAdminLogonBehavior`)
    * FICAM & NIST Control Mapping: `CP-9` (Information System Backup), `CP-10` (Information System Recovery), `IA-2` (Identification and Authentication), `SC-12` (Cryptographic Key Establishment and Management)
    * Telemetry & Event Auditing: Log Analysis for Event ID 4662 (Directory Service Access), Event ID 4932/4933 (Replication Synchronization Success/Failure), and Event ID 1658/1659 (DRS Replication Events)

### Chapter 11 - Lightweight Directory Access Protocol (LDAP) and Windows Directory Protocols

*

    #### 11.1 LDAP Architecture

    * Core Protocol Specification: RFC 4511 Standards and the Active Directory LDAP Implementation
    * Directory Server Listeners: Port Bindings for Standard LDAP (`TCP 389`), Secure LDAP (`TCP 636`), Global Catalog (`TCP 3268`), and Global Catalog SSL (`TCP 3269`)
    * Message Structure & BER Encoding: Basic Encoding Rules (BER) Binary Data Marshaling for Requests and Responses

    #### 11.2 RootDSE

    * Directory Entry Zero: Querying the Operational Attribute Container (`RootDSE`)
    * Discovery Mechanics: Enumerating Supported SASL Mechanisms, Naming Contexts, Server Functionality Levels, and Capabilities
    * Offensive Vector: Anonymous and Authenticated Pre-Domain Reconnaissance for Forest Topography and Policy State

    #### 11.3 LDAP Searches

    * Search Execution Parameters: Base DN, Search Scope (`Base`, `OneLevel`, `Subtree`), and Attribute Selection
    * Result Paging Controls: Simple Paged Results Control (`1.2.840.113556.14.319`) and Virtual List View (VLV) for Bypassing `MaxPageSize` Server Limits
    * Offensive Vector: Automated Directory Harvesting and Enumeration Tools (`BloodHound`, `ldapsearch`)

    #### 11.4 Search Filters

    * Filter Construction: Boolean Operators (`&`, `|`, `!`) and Attribute-Value Match Assertions
    * Bitwise Match Rules: Matching Bitmasks via `LDAP_MATCHING_RULE_BIT_AND` (`1.2.840.113556.14.803`)
    * Extensible Match Rules: Transitive Group Membership Expansion via `LDAP_MATCHING_RULE_IN_CHAIN` (`1.2.840.113556.14.1841`)
    * Offensive Vector: Querying Sensitive Accounts, Unconstrained Delegation Targets, and Privileged Group Memberships

    #### 11.5 LDAP Binding

    * Authentication States: Anonymous Bind, Simple Bind (Cleartext Credentials), and SASL Bind
    * Security Exposure: Cleartext Credential Interception on Unencrypted Simple Binds over Port 389
    * Defensive Hardening: Disabling Anonymous Binds and Enforcing Strong Authentication Protocols

    #### 11.6 SASL and SPNEGO

    * Simple Authentication and Security Layer: RFC 4422 Abstraction Layer for Delegated Authentication
    * SPNEGO Negotiation: Simple and Protected GSSAPI Negotiation Mechanism for Kerberos and NTLM Negotiation Over LDAP
    * Session Cryptography: Establishing Integrity and Confidentiality Contexts Post-Authentication

    #### 11.7 LDAP Signing and Sealing

    * Data Integrity vs. Privacy: Digital Signatures (Signing) vs. Payload Encryption (Sealing/GSS-API)
    * Offensive Vector: LDAP Relay Attacks via Unsigned Binds to Elevate Privileges or Modify Directory Objects
    * Defensive Hardening: Enforcing LDAP Server Signing Requirements (`LdapServerIntegrity = 2`) via Group Policy

    #### 11.8 LDAPS and StartTLS

    * Transport Layer Encryption: SSL/TLS Tunneling (`TCP 636`) vs. In-Band TLS Upgrade via StartTLS Extension (`TCP 389`)
    * Certificate Validation: PKI Trust Anchor Requirements, Subject Alternative Names (SAN), and Certificate Revocation Checking
    * Channel Binding Tokens: Mitigating NTLM Relay with Extended Protection for Authentication (EPA / CBT) (`LdapEnforceChannelBinding`)

    #### 11.9 Global Catalog Queries

    * Forest-Wide Lookups: Querying the Partial Attribute Set (PAS) Across All Forest Domains via Ports 3268/3269
    * Cross-Domain Referrals: Handling Referral Responses (`LDAP_REFERRAL`) for Out-of-Partition Objects
    * Performance & Security: Balancing Global Catalog Replication Traffic Against Cross-Domain Query Scope

    #### 11.10 Netlogon

    * MS-NRPC Architecture: Netlogon Remote Protocol for Member Workstation and Domain Controller Secure Channels
    * Credential Validation: Pass-Through Authentication and Domain Trust Maintenance
    * Offensive Vector: ZeroLogon (`CVE-2020-1472`) Exploitation of Weak Cryptographic Initialization Vectors (AES-CFB8)
    * Defensive Hardening: Enforcing Secure Channel Encryption and Applying Netlogon Vulnerability Patches

    #### 11.11 MS-RPC

    * Remote Procedure Call Framework: Client-Server Abstraction for Distributed Windows Services
    * Data Marshaling: Network Data Representation (NDR) Serialization and Transfer Syntax
    * RPC Transport Bindings: RPC over Connection-Oriented TCP/IP, Named Pipes (`ncacn_np` over SMB), and RPC over HTTP

    #### 11.12 RPC Endpoint Mapper

    * Service Resolution: RPC Endpoint Mapper (EPMAP) Listener on `TCP 135`
    * Dynamic Port Assignment: Mapping Interface UUIDs to Dynamic Server High-Port Ranges (`TCP 49152-65535`)
    * Offensive Vector: RPC Interface Enumeration to Map Active Services and Unpatched Interfaces (`rpcdump`)
    * Defensive Hardening: Restricting Dynamic RPC Port Ranges and Enforcing Network Segmentation Rules

    #### 11.13 SAMR

    * Security Account Manager Remote Protocol: `[MS-SAMR]` Interface for Managing Accounts, Groups, and Passwords
    * Domain & Local Reconnaissance: Querying User Lists, Group Memberships, and Password Policies
    * Offensive Vector: Anonymous and Low-Privilege User/Group Enumeration over SAMR
    * Defensive Hardening: Configuring `RestrictRemoteSAM` Registry Policies to Limit Remote SAMR Access

    #### 11.14 LSARPC

    * Local Security Authority Remote Protocol: `[MS-LSAD]` Interface for Local Security Policy Management
    * Privilege & Identity Resolution: SID-to-Name Mapping, LSA Secrets Querying, and Privilege Right Assignments
    * Offensive Vector: SID Lookup Reconnaissance and LSA Policy Enumeration
    * Defensive Hardening: Restricting Anonymous LSA Access (`NullSessionPipes` and `RestrictNullSessAccess`)

    #### 11.15 DRSR and DRSUAPI

    * Directory Replication Service Remote Protocol: `[MS-DRSR]` Interface for Active Directory Multi-Master Replication
    * DRSUAPI RPC Interface: Core Replication Binding for Schema, Topology, and Object Updates
    * Offensive Vector: DCSync Attack Vector via RPC Interface (`DSGetNCChanges`) to Extract Domain Hashes
    * Defensive Hardening: Auditing Extended Directory Rights (`DS-Replication-Get-Changes-All`) and Restricting Replication Privileges

    #### 11.16 EFSRPC

    * Encrypting File System Remote Protocol: `[MS-EFSR]` Interface for Remote EFS Maintenance Operations
    * Offensive Vector: Authentication Coercion via PetitPotam (`EfsRpcOpenFileRaw`) Forcing Unauthenticated DC NTLM Authentication
    * Defensive Hardening: Disabling EFS Services, Applying Endpoint Patches, and Blocking Unauthenticated EFSRPC Calls

    #### 11.17 MS-RPRN

    * Print System Remote Protocol: `[MS-RPRN]` Interface for Remote Print Client-Server Communication
    * Offensive Vector: PrinterBug Authentication Coercion (`RpcRemoteFindFirstPrinterChangeNotificationEx`)
    * Defensive Hardening: Disabling the Print Spooler Service (`Spooler`) on Domain Controllers and Tier 0 Assets

    #### 11.18 DFSR

    * Distributed File System Replication: `[MS-DFSR]` Engine for Multi-Master SYSVOL and Shared Folder Replication
    * Staging & Conflict Resolution: Staging Directory Mechanics, RDC (Remote Differential Compression), and Conflict Resolution Folders
    * FICAM & NIST Control Mapping: `AC-4` (Information Flow Enforcement), `SC-8` (Transmission Confidentiality and Integrity), `SC-13` (Cryptographic Protection), `AU-12` (Audit Generation)
    * Telemetry & Event Auditing: Log Analysis for Event ID 2887/2889 (Unsigned LDAP Binds), Event ID 3039/3074 (LDAP Channel Binding Failures), Event ID 4624/4625 (Logon Events over Protocols), Event ID 4742 (Computer Account Modification - Netlogon), and Event ID 5136 (Directory Service Object Modification)

#### 26.1 Identity Identity Graph Theory

* 26.1.1 Applied Graph Theory in Identity Security: Nodes (Principals), Edges (Permissions/Trusts), and Directed Acyclic Graphs (DAGs)
* 26.1.2 Shortest Path Algorithms: Utilizing Dijkstra’s and Breadth-First Search (BFS) to Calculate Operational Attack Paths
* 26.1.3 Transitive Trust & Privilege Cascades: Modeling Implicit Access Inheritance across Directory Boundaries

#### 26.2 BloodHound

* 26.2.1 Core Architecture: Neo4j Graph Database Mechanics, Cypher Query Language (CQL), and User Interface Layouts
* 26.2.2 Enterprise vs. Open-Source Deployments: BloodHound Enterprise Attack-Path Management (APM) vs. Community Collector Workflows
* 26.2.3 Custom Cypher Queries: Writing CQL to Uncover Complex Non-Standard Control Paths and Specific Federal Role Escalations

#### 26.3 SharpHound

* 26.3.1 Collection Engines: SharpHound (.NET/PowerShell) Ingestion Workflows and Session/LAPS/DACL Collection Flags
* 26.3.2 Operational Security (OPSEC) & Stealth: Tuning Collection Threads, LDAP Page Sizes, and Loop Duration to Evade MDI and EDR Detection
* 26.3.3 Offline & Containerized Ingestion: Processing Ingested JSON Data in Isolated Security Enclaves

#### 26.4 Nodes, Edges, and Relationships

* 26.4.1 Standard DACL/ACE Edges: Analyzing `GenericAll`, `WriteDacl`, `WriteOwner`, `GenericWrite`, and `AddMember`
* 26.4.2 Session and Execution Edges: Mapping `HasSession`, `AdminTo`, `ExecuteDCOM`, `CanPSRemote`, and `CanRD`
* 26.4.3 Credential Abuse Edges: Evaluating `ForceChangePassword`, `DCSync`, `ReadLAPSPassword`, and `ReadGMSAPassword`

#### 26.5 Effective Control Paths

* 26.5.1 Indirect Object Control: Identifying Multi-Hop Administrative Control over Intermediate Groups and Users
* 26.5.2 Overlapped & Nested Group Inheritance: Resolving Complex Cross-OU Group Memberships and Delegated Rights
* 26.5.3 Object Ownership Exploitation: Leveraging Owner Rights (`WriteDacl`) to Modify Security Descriptors on Target Objects

#### 26.6 Hidden Delegation Paths

* 26.6.1 Kerberos Unconstrained Delegation Chains: Reconstructing Computer Account Control Paths Leading to TGT Theft
* 26.6.2 Constrained Delegation & S4U Abuses: Mapping Protocol Transition (`S4U2Self` / `S4U2Proxy`) Paths to Target SPNs
* 26.6.3 Resource-Based Constrained Delegation (RBCD): Graphing `msDS-AllowedToActOnBehalfOfOtherIdentity` Control Edges Across Host Assets

#### 26.7 Tier 0 Reachability

* 26.7.1 Asset Grouping & Control Plane Definition: Tagging Tier 0 Nodes (DCs, AD CS CAs, Entra Sync, High-Privilege Users)
* 26.7.2 Measuring Exposure Metrics: Calculating Percentage of Directory Principals with Paths to Tier 0 Assets
* 26.7.3 Structural Choke Point Identification: Locating High-Value Intermediary Nodes Whose Remediation Severs Multiple Attack Paths

#### 26.8 Certificate and PKI Enumeration

* 26.8.1 AD CS Graph Integration: Mapping Certificate Authority (CA) Nodes, Enrollment Rights, and Certificate Template Objects
* 26.8.2 ESC Edge Analysis: Visualizing `ADCSESC1`, `ADCSESC3`, `ADCSESC4`, `ADCSESC6`, and `ADCSESC9` Exploit Paths
* 26.8.3 PKI-Based Identity Hijacking: Identifying Paths Exposing Domain Controller Certificates and Golden Certificate Generation

#### 26.9 Federation Enumeration

* 26.9.1 Federation Server Control Edges: Graphing Administrative Rights Over AD FS Servers, Web Application Proxies (WAP), and Service Accounts
* 26.9.2 Relying Party Trust Vulnerabilities: Visualizing Over-Permissive Relying Party DACLs and Claims Transformation Vulnerabilities
* 26.9.3 Cross-Domain Federation Links: Mapping Federation Trust Nodes Connecting On-Premises AD to External Agency Identity Providers

#### 26.10 Entra ID Enumeration

* 26.10.1 AzureHound Mechanics: Collecting Cloud Tenant Data via Microsoft Graph API and Azure Resource Manager (ARM)
* 26.10.2 Cloud Node & Edge Mapping: Visualizing `AZGlobalAdmin`, `AZAppAdmin`, `AZOwner`, `AZKeyVaultContributor`, and `AZAddMembers`
* 26.10.3 Service Principal & Managed Identity Paths: Uncovering Secret/Credential Injection Edges Across Enterprise Applications

#### 26.11 Hybrid Identity Enumeration

* 26.11.1 On-Premises to Cloud Escalation Edges: Graphing `ADSync` Service Account (`MSOL_`) Privileges and Hybrid Sync Agents
* 26.11.2 Pass-Through Auth (PTA) & Seamless SSO Paths: Visualizing `AZUREADSSOACC` Kerberos Ticket Abuse Vectors
* 26.11.3 Cloud-to-On-Premises Escalation: Graphing Password/Device Writeback Connectors and Cloud Admin Impersonation Paths

#### 26.12 AI-Assisted Attack-Path Analysis

* 26.12.1 Machine Learning Graph Traversal: Utilizing Algorithmic Pattern Recognition to Predict Unindexed Identity Paths
* 26.12.2 Automated Path Contextualization: Summarizing Multi-Hop Attack Vectors into Natural Language Threat Intelligence Briefs
* 26.12.3 Predictive Anomaly Detection: Identifying Sudden Identity Graph Structure Changes Indicating Adversary Persistence Insertion

#### 26.13 Path Prioritization and Validation

* 26.13.1 Operational Risk Scoring: Ranking Attack Paths Based on Complexity, Required Privileges, and Detection Risk
* 26.13.2 Technical Path Validation: Verifying Graph-Predicted Attack Paths via Safe Active Probing Protocols
* 26.13.3 Remediation Engineering & Telemetry: Severing Dangerous Edges, Implementing Least-Privilege DACLs, and Auditing via Event ID 4662, 5136, and MDI Graph Telemetry

#### 27.1 Initial Access Strategy and Identity Focus

* 27.1.1 The Identity-Centric Perimeter: Shifting Focus from Network Exploitation to Valid Credential Acquisition
* 27.1.2 FICAM Authenticator Assurance Levels (AAL): Evaluating AAL1–AAL3 Controls and Identifying Fallback Vulnerabilities
* 27.1.3 Operational Security (OPSEC) for Initial Access: Managing Source IP Reputation, User-Agent Spoofing, and Request Velocity

#### 27.2 Password Spraying Techniques

* 27.2.1 External Portal Spraying: Targeting OWA, VPN Gateways, Remote Desktop Gateways, and Entra ID Endpoints
* 27.2.2 Lockout Policy Evasion: Analyzing Account Lockout Thresholds, Observation Windows, and Smart Lockout Mechanics
* 27.2.3 Targeted Wordlist Generation: Creating Season/Year, Agency-Specific, and Behavioral Password Lists Based on OSINT

#### 27.3 Kerberos Unauthenticated Vectors

* 27.3.1 AS-REP Roasting Mechanics: Querying Accounts Set with `DONT_REQUIRE_PREAUTH` without Prior Domain Access
* 27.3.2 Offline Hash Extraction & Cracking: Extracting `krb5asrep` Hashes and Executing GPU-Accelerated Attacks via Hashcat
* 27.3.3 Mitigating AS-REP Roasting: Identifying and Enforcing Pre-Authentication Across All Domain Objects

#### 27.4 Credential Coercion and Relay

* 27.4.1 Unauthenticated RPC Coercion: Abusing MS-EFSR (PetitPotam), MS-RPRN (PrinterBug), and ShadowCoerce Protocols
* 27.4.2 LLMNR/NBT-NS Poisoning: Capturing NetNTLMv2 Hashes on Local Segments via Responder and Inveigh
* 27.4.3 NTLM Relay to AD CS: Relaying Coerced Machine/User Authentication to PKI Web Enrollment (ESC8) for Instant Certificate Issuance

#### 27.5 Phishing and MFA Bypass Techniques

* 27.5.1 Adversary-in-the-Middle (AiTM) Proxies: Deploying Evilginx/Muraena to Intercept Session Cookies and Primary Refresh Tokens (PRTs)
* 27.5.2 Phishing-Resistant Control Evasion: Targeting Legacy Protocol Endpoints (WS-Trust / Basic Auth) and Alternate Auth Methods
* 27.5.3 Push Fatigue & MFA Prompt Bombarding: Exploiting Interactive Push Notification Workflows to Force User Approval

#### 27.6 External Identity Portal Exploitation

* 27.6.1 Vulnerable Extranet Gateways: Exploiting Misconfigured Single Sign-On (SSO) Portals and Keycloak/Shibboleth Endpoints
* 27.6.2 SAML/OAuth Exchange Abuse: Intercepting and Manipulating Insecure Authentication Tokens in Hybrid Portals
* 27.6.3 Partner & Contractor Portal Targeting: Exploiting B2B Trust Flows and Over-Permissive Guest Account Registrations

#### 27.7 Credential Stuffing and Darknet Breach Reuse

* 27.7.1 Breach Data Aggregation: Mining Historical Breaches for Enterprise Email Addresses and Plaintext Passwords
* 27.7.2 Automated Credential Validation: Testing Recycled Passwords Against Public-Facing Active Directory and O365 Endpoints
* 27.7.3 Pattern-Based Password Mutation: Applying Transformation Rules to Historical Passwords to Predict Current Credentials

#### 27.8 Initial Access Validation and Telemetry Auditing

* 27.8.1 Credential Testing & Validation: Validating Acquired Credentials via Non-Interactive LDAP and SMB Binds
* 27.8.2 Canary Accounts and Honeypots: Deploying Decoy Accounts and Lure Credentials to Trigger Immediate Intrusion Alerts
* 27.8.3 Event Logging & Telemetry Analysis: Auditing Event ID 4625 (An Account Failed to Log On), Event ID 4624 (Successful Logon), Event ID 4768 (Kerberos TGT Request - AS-REP), and Entra ID Risk Detections

#### 28.1 Multicast and Broadcast Name Resolution Exploitation

* 28.1.1 Fallback Name Resolution Protocols: Protocol Mechanics of LLMNR (UDP 5355), NBT-NS (UDP 137), and mDNS (UDP 5353)
* 28.1.2 Trust Assumptions in Local Subnets: Exploiting Unauthenticated Race Conditions in Link-Local Broadcast Domains
* 28.1.3 Federal & Military Enclave Risks: Evaluating Legacy Protocol Exposure across Tactical, OT, and Enclave Subnets

#### 28.2 LLMNR, NBT-NS, and mDNS Poisoning Mechanics

* 28.2.1 Inbound Query Interception: Utilizing Tools (Responder, Inveigh) to Listen and Forge Poisoned Responses
* 28.2.2 NetNTLMv1/v2 Hash Capture: Forcing Inbound NTLM Challenge-Response Authentication Workflows
* 28.2.3 Passive vs. Active Poisoning OPSEC: Throttling Poisoning Responses to Avoid Network Disruptions and Detection Thresholds

#### 28.3 Web Proxy Auto-Discovery (WPAD) Spoofing

* 28.3.1 WPAD Protocol Architecture: Automatic Proxy Discovery via DNS, DHCP Option 252, and Link-Local Multicast Fallbacks
* 28.3.2 Serving Malicious `wpad.dat` Files: Injecting Rogue Proxy Configurations to Intercept HTTP/HTTPS Traffic
* 28.3.3 Forcing Proxy Authentication: Prompting Background Windows Services and Browsers for NTLM Credentials

#### 28.4 Rogue IPv6 SLAAC and DHCPv6 DNS Takeover

* 28.4.1 Windows Dual-Stack Behavior: Capitalizing on Default Windows IPv6 Activation and IPv6 DNS Preference
* 28.4.2 Executing `mitm6` Takeover Attacks: Assigning Rogue Link-Local IPv6 Addresses and Spoofing Primary DNS Servers
* 28.4.3 Intercepting WPAD over IPv6: Forcing Enterprise Workstations to Authenticate to Attacker-Controlled IPv6 Endpoints

#### 28.5 NTLM Relaying Architecture and Constraints

* 28.5.1 Relaying vs. Cracking Mechanics: Forwarding Intercepted NTLM Challenge-Responses directly to Target Protocols
* 28.5.2 SMB Signing Barriers: Understanding Same-Protocol Relaying Restrictions and Cross-Protocol Relaying Vectors
* 28.5.3 MIC (Message Integrity Code) Bypass Vectors: Bypassing NTLM MIC Validation and Session Cryptographic Bindings

#### 28.6 Credential Coercion Protocols

* 28.6.1 RPC/MS-EFSR Coercion (PetitPotam): Forcing Unauthenticated Computer Account Authentication via Encrypting File System RPC
* 28.6.2 Spoolss Coercion (PrinterBug / MS-RPRN): Triggering Remote Domain Controller Authentication via Print System Remote Protocol
* 28.6.3 Advanced Coercion Vectors: Abusing ShadowCoerce (MS-FSRVP), DFSCoerce (MS-DFSNM), and WebDAV Remote Paths

#### 28.7 Relay Destinations and Exploitation Outcomes

* 28.7.1 Relaying to LDAP/LDAPS: Injecting Resource-Based Constrained Delegation (RBCD) and Creating Rogue Computer Accounts
* 28.7.2 Relaying to AD CS PKI Web Enrollment (ESC8): Relaying Coerced Machine NTLM Authentication to Obtain Client Authentication Certificates
* 28.7.3 Relaying to HTTP/SMB Management Interfaces: Executing Remote Code via Administrative Web Endpoints and Unsigned SMB Services

#### 28.8 DNS Spoofing and Dynamic DNS Update Abuse

* 28.8.1 Dynamic DNS (DDNS) Insecurity: Injecting Unauthorized A/AAAA Records via Unauthenticated Dynamic Updates
* 28.8.2 Active Directory Integrated DNS (ADIDNS) Attacks: Abusing Default Authenticated User Record Creation Permissions (`AdidnsDump`)
* 28.8.3 DNS Cache Poisoning: Intercepting and Redirecting Enterprise Identity and SSO Hostname Resolution

#### 28.9 SMB Signing, EPA, and LDAP Channel Binding Enforcement

* 28.9.1 Enforcing SMB Signing: Deploying GPOs for Required SMB Client/Server Signing across Domain Controllers and Member Servers
* 28.9.2 Enforcing LDAP Signing & Channel Binding: Hardening Directory Services Against Insecure NTLM Relay Submissions
* 28.9.3 Implementing Extended Protection for Authentication (EPA): Binding TLS Credentials to NTLM Authentication Tokens on Web/RPC Services

#### 28.10 Defensive Hardening, GPO Controls, and Telemetry

* 28.10.1 Disabling LLMNR & NBT-NS via GPO: Configuring `Turn off multicast name resolution` and Disabling NetBIOS over TCP/IP
* 28.10.2 IPv6 Guard Controls: Deploying Network Switch RA Guard, DHCPv6 Guard, and Windows Firewall Block Rules
* 28.10.3 Event Logging & Intrusion Auditing: Monitoring Event ID 4624 (NTLM Logon Types), Event ID 3020/3021 (SMB Signing Audits), Event ID 2886/2887/2889 (Unsigned LDAP Binds), and MDI Network Poisoning Alerts

#### 29.1 Fundamental Mechanics of Authentication Coercion

* 29.1.1 The Coercion Primitive: Forcing Remote Computer Accounts (`SYSTEM` Context) to Initiate Outbound Authentication
* 29.1.2 Transport & Protocol Vectors: Triggering Authentication via SMB, HTTP/WebDAV, RPC, and MS-RPC Bindings
* 29.1.3 Identity Context Harvesting: Capturing Machine Account Hashes (`HOSTNAME$`) vs. Interactive User Security Contexts

#### 29.2 Coercion RPC Interfaces and Execution

* 29.2.1 MS-RPRN (PrinterBug): Abusing `RpcRemoteFindFirstPrinterChangeNotificationEx` to Trigger Inbound SMB Binds
* 29.2.2 MS-EFSR (PetitPotam): Exploiting Encrypting File System RPC Calls (`EfsRpcOpenFileRaw`) to Force Unauthenticated Authentication
* 29.2.3 Advanced Coercion Triggers: Executing ShadowCoerce (MS-FSRVP), DFSCoerce (MS-DFSNM), and WebCoerce Protocols

#### 29.3 WebDAV and UNC Path Manipulation

* 29.3.1 WebDAV Mini-Redirector Mechanics: Forcing Workstations/DCs to Connect via HTTP/WebDAV (`\\attacker@80\share`)
* 29.3.2 Bypassing SMB Relaying Restrictions: Converting SMB-Based Coercion into HTTP NetNTLM Auth to Bypass Same-Protocol SMB Signing
* 29.3.3 UNC Path Injection in Directory Attributes: Injecting Malicious File Paths into User/Computer Attributes (`telephonenumber`, `scriptPath`)

#### 29.4 NTLM Relaying Fundamentals and Constraints

* 29.4.1 The NTLM Challenge-Response Protocol: Intercepting Type 1, Type 2, and Type 3 NTLM Messages in Transit
* 29.4.2 Cross-Protocol Relaying Mechanics: Relaying Intercepted HTTP/SMB Authentication to LDAP, LDAPS, HTTP, and IMAP Services
* 29.4.3 Security Barriers: Evaluating SMB Signing Restrictions, MIC (Message Integrity Code) Validation, and Session Key Cryptography

#### 29.5 Advanced Kerberos Relaying and Reflection

* 29.5.1 Kerberos Relay Mechanics (KrbRelay / KrbRelayx): Relaying `KRB_AP_REQ` Tokens Across Local and Remote RPC/SMB Interfaces
* 29.5.2 SPN Manipulation & DNS Spoofing: Altering Host Target Names and Arbitrary Port Binds to Force Relayed Kerberos Authentication
* 29.5.3 Kerberos Reflection Vulnerabilities: Reflecting System Authentication Back to the Originating Host to Gain Administrative Access

#### 29.6 Relay Target: LDAP / LDAPS Directory Injection

* 29.6.1 Machine Account Quota (`ms-DS-MachineAccountQuota`) Abuse: Utilizing Low-Privilege Access or Relayed Binds to Create Rogue Computer Objects
* 29.6.2 Resource-Based Constrained Delegation (RBCD) Injection: Writing `msDS-AllowedToActOnBehalfOfOtherIdentity` Attributes via Relayed LDAP Sessions
* 29.6.3 Shadow Admin Creation: Adding Attacker-Controlled Accounts to Delegated Groups via Relayed Directory Binds

#### 29.7 Relay Target: Active Directory Certificate Services (AD CS - ESC8)

* 29.7.1 HTTP NTLM Relaying to AD CS Web Enrollment: Relaying Coerced DC/Server Authentication to `/certsrv` Interfaces
* 29.7.2 Instant Computer Certificate Generation: Requesting Domain Controller/Machine Authentication Certificates via Relayed NTLM
* 29.7.3 Domain Takeover via Certificate Authentication: Exchanging Certificates for TGTs via PKINIT to Obtain Full Domain Privileges

#### 29.8 Cross-Domain and Cross-Forest Coercion

* 29.8.1 Trust-Crossing Coercion Vectors: Triggering Coercion Across Domain/Forest Trust Boundaries
* 29.8.2 SID Filtering & Foreign Security Principals (FSP): Impact of Trust Security Rules on Relayed Identity Assertions
* 29.8.3 Hybrid Cloud Coercion: Relaying Authentication across Hybrid Sync Connectors (Entra Connect / PTA Agents)

#### 29.9 Technical Defenses and Mitigation Engineering

* 29.9.1 Enforcing SMB Signing & LDAP Signing: Mandating Cryptographic Signatures across All Domain Controllers and Member Servers
* 29.9.2 Deploying Extended Protection for Authentication (EPA): Cryptographically Binding TLS Pass-Through Credentials to Neutralize NTLM Relay Attempts
* 29.9.3 Enforcing LDAP Channel Binding Tokens (CBT): Mandating CBT on LDAPS Port 636/3269 to Block Relayed Credentials
* 29.9.4 Disabling WebDAV & Unused RPC Services: Hardening Tier 0 Systems by Removing WebDAV Client Services and Disabling Print Spooler (`spoolsv`)

#### 29.10 Telemetry, Auditing, and Intrusion Detection

* 29.10.1 Monitoring RPC Coercion Events: Auditing RPC Pipe Binds and Machine Account Logons (Event ID 4624 - Logon Type 3)
* 29.10.2 Detecting Unsigned LDAP Binds: Tracking Event ID 2886, 2887, and 2889 in Directory Service Logs
* 29.10.3 Microsoft Defender for Identity (MDI) Alerts: Analyzing Suspicious RPC/Spooler Activity and NTLM Relay Attack Detections

#### 30.1 PKINIT Protocol Architecture and Federal Mandates

* 30.1.1 RFC 4556 Protocol Mechanics: PKINIT Extension Workflows, AS-REQ / AS-REP Cryptographic Exchange, and Diffie-Hellman (DH-SF) vs. RSA Key Exchanges
* 30.1.2 Federal PIV/CAC Integration: Aligning PKINIT with NIST SP 800-78-4, FIPS 201-3, and FICAM AAL3 Requirements
* 30.1.3 Smart Card Authentication Flow: Hardware TPM/Token Operations, PIN Verification, and KDC Certificate Validation Mechanics

#### 30.2 Certificate-to-Account Mapping Mechanics

* 30.2.1 Implicit SAN/UPN Mapping: Resolving User Principal Names (UPN) and Subject Alternative Names (SAN) in Domain Controller KDCs
* 30.2.2 Explicit Mapping via `altSecurityIdentities`: Mapping X509 Issuer/Subject Data, SHA-1 Key Identifiers, and AltSecIdentities Formatting
* 30.2.3 Weak Mapping Exploitation: Bypassing Certificate Identity Checks via Unenforced Strong Binding Rules and Arbitrary SAN Injection

#### 30.3 NTLM Hash Extraction via PKINIT

* 30.3.1 PAC Credential Structure Parsing: Deconstructing the `PAC_CREDENTIAL_INFO` Buffer Returned in PKINIT AS-REP Responses
* 30.3.2 Extracting NT Hashes (`Rubeus` / `pyPKINIT`): Decrypting PAC Buffers using Client Private Keys to Instantly Recover Plaintext NT Hashes
* 30.3.3 Mitigating NT Hash Exposure: Disabling NTLM Hash Invalidation, Enforcing Protected Users Group Membership, and Restricting PKINIT PAC Inclusions

#### 30.4 Shadow Credentials (`msDS-KeyCredentialLink`)

* 30.4.1 Key Credential Architecture: Windows Hello for Business (WHfB) Mechanics and Raw Public Key Attribute Binding
* 30.4.2 Injecting Key Credentials: Exploiting DACL Delegations (`GenericWrite`, `WriteProperty`) to Add Attacker Key Credentials to Target Accounts
* 30.4.3 PKINIT TGT Requests via Shadow Credentials: Requesting Kerberos TGTs using Injected RSA Keys without Active AD CS Infrastructure

#### 30.5 `SMARTCARD_REQUIRED` Enforcement and Bypasses

* 30.5.1 The `USER_SMARTCARD_REQUIRED` Flag: Architectural Limits of the Account Control Flag on Password Expiration and NTLM Authentication
* 30.5.2 NTLM Fallback Exploitation: Bypassing Smart Card Controls via Direct NTLM Binds, Network Relaying, and Explicit Service Authentication
* 30.5.3 Complete Smart Card Enforcement: Deploying Authentication Policies, Authentication Silos, and Disabling NTLM Enterprise-Wide

#### 30.6 Revocation Validation and PKI Infrastructure Attacks

* 30.6.1 CRL and OCSP Checking Mechanics: Domain Controller Revocation Verification Workflows during PKINIT Pre-Authentication
* 30.6.2 Soft-Fail vs. Hard-Fail Risks: Exploiting Soft-Fail Revocation Rules during OCSP Outages or Network Segregation
* 30.6.3 Tactical & Air-Gapped Network Challenges: Managing Offline Certificate Revocation Lists in Fragmented Defense Enclaves

#### 30.7 Hardening, Telemetry, and SIEM Auditing

* 30.7.1 Strong Certificate Binding (KB5014754 Compliance): Enforcing Full Enforcement Mode for SID-Bound Certificate Mappings
* 30.7.2 Auditing Shadow Credentials & Mapping Changes: Monitoring Attribute Modifications via Event ID 5136 (`msDS-KeyCredentialLink`, `altSecurityIdentities`)
* 30.7.3 PKINIT Event Telemetry Analysis: Tracking Event ID 4768 (Kerberos TGT Request - Certificate Pre-Auth), Event ID 4769 (Service Ticket Request), and Microsoft Defender for Identity (MDI) Smart Card Anomaly Alerts

#### 31.1 Protocol Mechanics of Kerberoasting and AS-REP Roasting

* 31.1.1 Kerberos Authentication Review: Comparing `AS-REQ`/`AS-REP` Pre-Authentication Workflows with `TGS-REQ`/`TGS-REP` Service Ticket Exchanges
* 31.1.2 AS-REP Roasting Mechanics: Exploiting Accounts Configured with `DONT_REQUIRE_PREAUTH` to Retrieve Encrypted TGT Data Unauthenticated
* 31.1.3 Kerberoasting Mechanics: Requesting Valid Service Tickets (`TGS-REP`) for Accounts Bound to Service Principal Names (SPNs)

#### 31.2 Service Principal Name (SPN) Cryptography and Encryption Fallbacks

* 31.2.1 SPN Attribute Architecture: Querying `servicePrincipalName` Attributes and Identifying High-Value Target Accounts
* 31.2.2 Encryption Type Negotiation: Analyzing `msDS-SupportedEncryptionTypes` and Requested Ticket Encryption Options
* 31.2.3 Cipher Downgrade Vectors: Forcing KDCs to Return RC4-HMAC (`0x4`) Encrypted Tickets Instead of AES-128/AES-256

#### 31.3 Offline Hash Extraction, Format Parsing, and GPU Cracking

* 31.3.1 Hash Extraction & Formatting: Parsing `$krb5asrep$` and `$krb5tgs$` Ticket Buffers for Off-Host Processing
* 31.3.2 GPU-Accelerated Cracking Strategy: Deploying Hashcat and John the Ripper using Custom Rule Sets, Mask Attacks, and Targeted Wordlists
* 31.3.3 Password Entropy Thresholds: Calculating Time-to-Crack Metrics Across Complex vs. Low-Entropy Service Passwords

#### 31.4 Deception Engineering: Honey-SPNs and Canary Accounts

* 31.4.1 Honey-SPN Deployment Mechanics: Creating Decoy Accounts with Arbitrary SPNs to Detect Unauthorized `TGS-REQ` Queries
* 31.4.2 AS-REP Canary Traps: Setting Up Monitored `DONT_REQUIRE_PREAUTH` Accounts to Flag Automated Enumeration Sweeps
* 31.4.3 Automated Response Workflows: Triggering Automated IP Isolation and Account Lockout Rules Upon Decoy Ticket Requests

#### 31.5 Architectural Remediation: gMSAs and High-Entropy Service Accounts

* 31.5.1 Migrating to Group Managed Service Accounts (gMSA): Eliminating Manual Password Management with 128-Character Automatic Rotation
* 31.5.2 Delegated Managed Service Accounts (dMSA): Implementing Next-Generation Windows Identity Controls for Service Objects
* 31.5.3 Enforcing AES-128/256 Cryptography: Disabling RC4-HMAC Globally via Group Policy and Restricting Service Account Password Policies

#### 31.6 Detection Engineering, Telemetry Correlation, and MDI Alerts

* 31.6.1 Event ID 4768 Auditing: Analyzing AS-REP Requests Lacking Pre-Authentication
* 31.6.2 Event ID 4769 Auditing: Monitoring Anomalous Service Ticket Request Volume, Rare SPN Access, and Ticket Encryption Types (`0x17` vs `0x12`)
* 31.6.3 Microsoft Defender for Identity (MDI) Integration: Configuring MDI Suspicious SPN Request Alerts and Behavior Anomaly Baselines

#### 32.1 LSASS Memory Extraction and Process Protection

* 32.1.1 LSASS Architecture and Memory Layout: How LSA Stores NTLM Hashes, Kerberos Tickets, and Primary Credentials in Memory
* 32.1.2 Memory Dumping Techniques: Executing LSASS Memory Dumps via Native Utilities (`comsvcs.dll`, `rundll32`), MiniDump APIs, and Custom Parsers
* 32.1.3 Eading Process Protections: Evaluating LSA Protection (`RunAsPPL`), Virtualization-Based Security (VBS), and Credential Guard Bypasses via BYOVD (Bring Your Own Vulnerable Driver)

#### 32.2 Registry Hive Secret Extraction

* 32.2.1 Local Account SAM Dumping: Extracting Local Administrator and User NTLM Hashes from the SAM Registry Hive
* 32.2.2 LSA Secrets and Cache Extraction: Parsing the `SECURITY` Hive to Recover Cached Domain Credentials (DCC2 / MSCash2) and Service Account Credentials
* 32.2.3 System Key Decryption Mechanics: Utilizing the `SYSTEM` Registry Hive to Obtain LSA Boot Keys required for Offline Registry Decryption

#### 32.3 Data Protection API (DPAPI) and Enterprise Secret Unlocking

* 32.3.1 DPAPI Cryptographic Architecture: User Master Keys, System Master Keys, and Credential Blob Encryption Structures
* 32.3.2 Domain-Wide DPAPI Decryption: Extracting the Domain Controller DPAPI Backup Key (`/protect /backupkey`) via RPC to Decrypt Any User Secret Offline
* 32.3.3 Target Secret Harvesting: Decrypting Chrome/Edge Credentials, Saved RDP Connections, Vaults, Wireless Profiles, and Task Scheduler Credentials

#### 32.4 Active Directory Database (`NTDS.dit`) Extraction

* 32.4.1 Harvesting `NTDS.dit` Snapshots: Utilizing Volume Shadow Copy Service (VSS), `ntdsutil`, and Install From Media (IFM) Workflows
* 32.4.2 Offline Database Parsing: Decrypting `NTDS.dit` using the Domain `SYSTEM` Hive to Extract All User Hashes, Supplemental Credentials, and Password History
* 32.4.3 Extracting Kerberos Keys: Parsing AES-128/256 Keys and `KRBTGT` Account Hashes for Persistent Ticket Forgery

#### 32.5 Local Administrator & Service Account Secret Harvesting

* 32.5.1 LAPS and Windows LAPS Attribute Extraction: Querying `ms-MCSF-LAPS-Password` and Encrypted `msLAPS-Password` Attributes via LDAP
* 32.5.2 gMSA Password Decryption: Reading `msDS-ManagedPassword` Blob Attributes and Converting Key Data into Plaintext Service Passwords
* 32.5.3 Group Policy Preferences (GPP) Residuals: Scanning SYSVOL for Legacy `Groups.xml` Files and Decrypting `cpassword` Attributes

#### 32.6 Kerberos Ticket Memory Management and Reuse

* 32.6.1 Extracting TGTs and TGSs from Memory: Dumping Kerberos Tickets from LSASS via `Rubeus` and `Mimikatz`
* 32.6.2 Pass-the-Hash (PtH) and Overpass-the-Hash (PtK): Executing NTLM Hash Injection and Exchanging NTLM/AES Hashes for Valid Kerberos TGTs
* 32.6.3 Pass-the-Ticket (PtT): Injecting Harvested Kerberos Tickets into Current Logon Sessions for Unauthenticated Lateral Movement

#### 32.7 Defensive Hardening, Endpoint Detection, and Telemetry

* 32.7.1 Enforcing Hardware and Kernel Protections: Deploying Credential Guard, Enforcing `RunAsPPL` via GPO, and Restricting Administrative Privileges
* 32.7.2 LSASS Access Auditing & EDR Telemetry: Monitoring Process Access Handle Requests to LSASS (Event ID 4656, Event ID 4663) and Detecting Suspicious Memory Reads
* 32.7.3 Microsoft Defender for Identity (MDI) Integration: Configuring Alerts for Pass-the-Hash, LSASS Memory Access Anomalies, and `NTDS.dit` Snapshot Creation

#### 33.1 Fundamentals of Token-Based Identity Execution

* 33.1.1 Authentication vs. Authorization Tokens: Distinguishing Between Credentials Used for Identity Proofing and Signed Tokens Used for Access Rights
* 33.1.2 Windows Access Token Mechanics: Primary Tokens, Impersonation Tokens, Security Contexts, and Token Impersonation Levels (`SecurityAnonymous`, `SecurityIdentification`, `SecurityImpersonation`, `SecurityDelegation`)
* 33.1.3 Token Theft Boundaries: Evaluating Process Privileges Required for Token Manipulation (`SeDebugPrivilege`, `SeImpersonatePrivilege`, `SeAssignPrimaryTokenPrivilege`)

#### 33.2 Pass-the-Hash (PtH) and Overpass-the-Hash (PtK)

* 33.2.1 Pass-the-Hash Mechanics: Replaying Raw NTLM Hashes Over SMB, RPC, and WMI Interfaces without Plaintext Decryption
* 33.2.2 Overpass-the-Hash (PtK) Mechanics: Exchanging NTLM or AES-128/256 Hashes for Kerberos TGTs via Pre-Authentication
* 33.2.3 Restricting NTLM Replay: Implementing Local Account Token Filter Policy (`LocalAccountTokenFilterPolicy`) and Disabling NTLM Fallback

#### 33.3 Pass-the-Ticket (PtT) and Kerberos Session Hijacking

* 33.3.1 Injected Kerberos Ticket Reuse: Importing Harvested TGTs and TGSs directly into Windows LSA Security Contexts via `Rubeus` or `Mimikatz`
* 33.3.2 Ticket Lifetime and Renewal Mechanics: Exploiting Ticket Renewal Windows (`ticket_max_renewable_age`) for Extended Domain Access
* 33.3.3 Service Principal Name (SPN) Mappings in Ticket Replay: Replaying TGS Tickets Against Alternative Host Interfaces and Non-Standard Ports

#### 33.4 Access Token Duplication and Impersonation

* 33.4.1 Enumerating Process Tokens: Querying Running Processes for High-Privilege Domain Contexts (`Domain Admin`, `SYSTEM`)
* 33.4.2 Token Duplication via OpenProcessToken: Executing `DuplicateTokenEx` to Create Primary Tokens for Process Launching
* 33.4.3 Bypassing User Account Control (UAC): Utilizing Privileged Tokens to Elevate Integrity Levels from Medium to High/System

#### 33.5 Cloud & Hybrid Token Theft: Entra ID Primary Refresh Tokens (PRTs)

* 33.5.1 Primary Refresh Token Architecture: Device-Bound Proof-of-Possession Tokens, TPM Bindings, and Local Cloud LSASS Storage
* 33.5.2 Extracting and Replaying PRTs: Harvesting PRTs via `ROADtools` or Native APIs to Bypass Multi-Factor Authentication (MFA)
* 33.5.3 Session Cookie Hijacking: Stealing Browser Authentication Cookies (`ESTSAUTH`, `ESTSAUTHPERSISTENT`) for Unauthenticated Cloud Portal Access

#### 33.6 Defensive Engineering, Isolation, and Telemetry

* 33.6.1 Deploying Windows Defender Credential Guard: Utilizing VBS to Isolate Kerberos Keys and NTLM Hashes in Virtual Containers
* 33.6.2 Restricting Token Privilege Abuse: Enforcing Least Privilege, Removing Dangerous User Rights Assignments, and Hardening PAWs
* 33.6.3 Telemetry Correlation & SIEM Auditing: Monitoring Event ID 4624 (Logon Type 9 - `NewCredentials`), Event ID 4672 (Special Privileges Assigned), Event ID 4768/4769 (Kerberos Anomaly Tracking), and MDI Replay Alerts

#### 34.1 Directory Access Control Architecture

* 34.1.1 Security Descriptors & ACL Structures: Parsing Discretionary Access Control Lists (DACLs), System Access Control Lists (SACLs), Object SIDs, and Inherited Flags
* 34.1.2 ACE Types and Evaluation Order: Evaluating Explicit Deny, Explicit Allow, Inherited Deny, and Inherited Allow Processing Sequence
* 34.1.3 Attribute-Scoped Permissions: Distinguishing Between Object-Level Rights and Specific Schema Property Set Rights

#### 34.2 Dangerous Directory Permissions and Exploitation

* 34.2.1 Full Control (`GenericAll`): Complete Object Manipulation, Password Resets, and Group Membership Modification
* 34.2.2 Permission Modification (`WriteDacl`): Modifying Target Object DACLs to Grant Explicit Full Control
* 34.2.3 Ownership Takeover (`WriteOwner` / `TakeOwnership`): Claiming Object Ownership to Reconfigure Discretionary Access Controls
* 34.2.4 Property Modification (`GenericWrite` / `WriteProperty`): Writing Targeted Attributes (`member`, `scriptPath`, `userAccountControl`) to Escalate Privileges

#### 34.3 AdminSDHolder and Protected Object Integrity

* 34.3.1 SDProp Process Mechanics: Understanding Automatic Permission Enforcement across Protected Groups and Users
* 34.3.2 AdminSDHolder Persistence: Injecting Backdoor ACEs into `CN=AdminSDHolder` for Automated Security Descriptor Propagation
* 34.3.3 Orphaned Protected Accounts: Identifying Accounts with `adminCount=1` Outside Protected Groups and Remediating Permission Drift

#### 34.4 Primary Group ID and Shadow Administrative Chains

* 34.4.1 PrimaryGroupID Manipulation: Altering the `primaryGroupID` Attribute to Gain Stealthy Access to Privileged Domain Groups
* 34.4.2 Nested Group Authorization Abuse: Exploiting Cross-OU and Transitive Group Memberships to Access Restricted Enterprise Resources
* 34.4.3 Foreign Security Principals (FSP) Abuse: Abusing Cross-Domain Group Memberships to Maintain High-Privilege Access Across Trust Boundaries

#### 34.5 Dynamic Access Control (DAC) and Claims-Based Access

* 34.5.1 Central Access Policies (CAP) Architecture: Evaluating Device Claims, User Claims, and Resource Attributes in Resource Authorization
* 34.5.2 Claim Spoofing & Kerberos Extension Abuse: Manipulating User and Device Claims in Kerberos PACs to Bypass ABAC Rules
* 34.5.3 Hardening Claims-Based Authorization: Validating Claim Issuance Rules and Restricting Dynamic Access Control Fallbacks

#### 34.6 Defensive Engineering, ACL Auditing, and Telemetry

* 34.6.1 Automated DACL Auditing: Utilizing PowerShell, `BloodHound APM`, and `PingCastle` to Detect Dangerous Access Control Entries
* 34.6.2 Enforcing Least-Privilege Delegation: Implementing Role-Based Access Control (RBAC) and Restricting Delegated Administration Scopes
* 34.6.3 Telemetry & Event Auditing: Monitoring Directory Service Modifications via Event ID 5136 (Directory Service Object Modified), Event ID 4662 (Operation Performed on Object), and MDI Authorization Anomaly Alerts

#### 35.1 Group Policy Architecture and Replication

* 35.1.1 Dual-Component Structure of GPOs: Group Policy Container (GPC) in Active Directory LDAP vs. Group Policy Template (GPT) in SYSVOL
* 35.1.2 SYSVOL File Replication Mechanics: Distributed File System Replication (DFSR) Synchronization, Version Numbers, and Policy Consistency
* 35.1.3 Client-Side Extension (CSE) Processing: How Host Winlogon and Group Policy Services Evaluate GUIDs and Process Security Templates

#### 35.2 SYSVOL and GPO Permission Auditing

* 35.2.1 GPC Directory Permission Analysis: Auditing `WriteDacl`, `WriteOwner`, and `GenericWrite` Permissions on LDAP Policy Objects
* 35.2.2 SYSVOL File Share Security Descriptor Auditing: Inspecting DACLs on `\\domain\SYSVOL\domain\Policies\` Files and Folders
* 35.2.3 Delegation Abuses: Identifying Non-Standard Groups with Rights to Create, Link, or Edit GPOs Across Organizational Units (OUs)

#### 35.3 Policy Injection and Malicious GPO Execution

* 35.3.1 Immediate Scheduled Task Injection: Modifying `ScheduledTasks.xml` to Trigger Instant Command Execution as `SYSTEM` on Target Hosts
* 35.3.2 Startup/Shutdown and Logon/Logoff Script Manipulation: Injecting Malicious PowerShell or Batch Scripts into GPT Script Locations
* 35.3.3 User Rights Assignment (URA) Exploitation: Modifying Security Templates (`GptTmpl.inf`) to Grant Privileges Like `SeDebugPrivilege` or `SeRemoteInteractiveLogonRight`

#### 35.4 Group Policy Preferences (GPP) Password Recovery

* 35.4.1 GPP XML Password Encryption: Analysis of Microsoft's Historical AES-256 Key Usage for `cpassword` Strings
* 35.4.2 SYSVOL File Mining: Automated Scanning of XML Files (`Groups.xml`, `Services.xml`, `ScheduledTasks.xml`, `Printers.xml`) for Decryptable Credentials
* 35.4.3 Remediation of GPP Artifacts: Purging Legacy GPP Passwords and Deploying KB2962486 to Block Password Entry in Policy Consoles

#### 35.5 Defensive Hardening, GPO Governance, and Telemetry

* 35.5.1 Restricting GPO Creation and Linking: Enforcing Role-Based Access Control (RBAC) and Limiting `Group Policy Creator Owners` Membership
* 35.5.2 Automated GPO Drift and Integrity Monitoring: Implementing Version Tracking, Infrastructure as Code (IaC) Validation, and SYSVOL File Integrity Monitoring (FIM)
* 35.5.3 Telemetry Correlation & Event Auditing: Monitoring Event ID 5136 (GPC Modification), Event ID 5145 (SYSVOL Network Share Access), Event ID 4662 (GPO ACL Changes), and MDI Policy Abuse Detections

#### 36.1 Kerberos Delegation Architecture

* 36.1.1 Evolution of Kerberos Delegation: Comparing Unconstrained Delegation, Constrained Delegation, and Resource-Based Constrained Delegation (RBCD)
* 36.1.2 Service for User Extensions (S4U): Mechanics of `S4U2self` (Impersonation without Pre-Auth) and `S4U2proxy` (Constrained Forwarding)
* 36.1.3 Cryptographic Key Bindings: Ticket Granting Service (TGS) Requests, Service Principal Names (SPNs), and Forwardable TGT Caching

#### 36.2 Unconstrained Delegation Exploitation and Defense

* 36.2.1 Unconstrained Delegation Mechanics: Extracting Cached Domain Admin TGTs from LSASS on Compromised Delegated Hosts
* 36.2.2 Coercion Protocol Integration: Pairing Unconstrained Delegation Hosts with RPC Coercion (PetitPotam, PrinterBug) to Capture Domain Controller TGTs
* 36.2.3 Mitigating Unconstrained Risks: Disabling Unconstrained Delegation, Moving to RBCD, and Enforcing `ACCOUNT_NOT_DELEGATED` Flags

#### 36.3 Constrained Delegation and S4U Abuse

* 36.3.1 Constrained Delegation Configuration: Auditing `msDS-AllowedToDelegateTo` Attributes across User and Computer Objects
* 36.3.2 Protocol Transition Exploitation: Utilizing `S4U2self` to Forge Arbitrary User Identity Contexts to Delegated Target Services
* 36.3.3 Service Name (sname) Substitution: Replaying Constrained Delegation Service Tickets Against Unrelated Services (CIFS, LDAP, HOST) on Target Systems

#### 36.4 Resource-Based Constrained Delegation (RBCD)

* 36.4.1 RBCD Trust Architecture: Shifting Delegation Control from Frontend Services to Resource Owners (`msDS-AllowedToActOnBehalfOfOtherIdentity`)
* 36.4.2 Attack Path Execution: Creating Controlled Computer Objects (`ms-DS-MachineAccountQuota`) and Injecting Binary Security Descriptors
* 36.4.3 Escalation to Local SYSTEM: Executing `S4U` Interchanges to Obtain Administrative TGS Tokens for Target Machine Compromise

#### 36.5 Key Trust, WHfB, and Shadow Credentials

* 36.5.1 Key Trust Infrastructure: Windows Hello for Business (WHfB) Architecture, Asymmetric Key Pair Binding, and PKINIT Mechanics
* 36.5.2 Shadow Credential Injection: Writing RSA Public Key Attributes (`msDS-KeyCredentialLink`) via Delegated Permissions (`GenericWrite`, `WriteProperty`)
* 36.5.3 Requesting PKINIT TGTs: Authenticating to Domain Controller KDCs via Injected Key Credentials to Obtain Valid Kerberos TGTs and NT Hashes

#### 36.6 Passwordless Pre-Auth & Key Credential Edge Cases

* 36.6.1 WHfB Key Credential Coexistence: Managing Coexistence between Key Trust and Certificate Trust Deployment Models
* 36.6.2 Key Credential Lifecycle & Orphaned Keys: Identifying and Purging Stale RSA Keys Mapped to Decommissioned Workstations and Users

#### 36.7 Delegation Auditing, Hardening, and Telemetry

* 36.7.1 Protected Users Group Deployment: Blocking TGT Forwarding and Restricting Delegation Capabilities for Privileged Domain Accounts
* 36.7.2 Automated Delegation Auditing: Scanning Directory Objects for Delegation Flags, RBCD Security Descriptors, and Key Credential Attributes via PowerShell and BloodHound
* 36.7.3 Telemetry Correlation & SIEM Monitoring: Auditing Event ID 4768 (TGT Request), Event ID 4769 (Service Ticket Request - S4U2self/S4U2proxy), Event ID 5136 (`msDS-KeyCredentialLink` / `msDS-AllowedToActOnBehalfOfOtherIdentity` Modifications), and MDI Delegation Anomaly Detections

#### 36.8 Operational Playbook: Delegated Identity Incident Response

* 36.8.1 Containment & Key Invalidation: Revoking Compromised Delegation TGTs and Clearing `msDS-AllowedToActOnBehalfOfOtherIdentity` Attributes
* 36.8.2 Post-Remediation Validation: Re-baselining Identity Delegation Graphs and Verifying Ticket Cache Invalidation Across Enterprise DCs

#### 37.1 Active Directory Certificate Services (AD CS) Architecture

* 37.1.1 Enterprise CA vs. Standalone CA: Domain Integration, Directory Enrollment Objects, and PKI Trust Stores (`CN=Public Key Services,CN=Services,CN=Configuration`)
* 37.1.2 Certificate Template Mechanics: Schema Attributes, Extended Key Usages (EKUs), Authentication Flags, and Enrollment Rules
* 37.1.3 PKINIT Integration with AD CS: How KDCs Process Certificates for Initial Kerberos Authentication (RFC 4556)

#### 37.2 Misconfigured Certificate Templates (ESC1, ESC2, ESC3)

* 37.2.1 ESC1 - Enrollee Supplies SAN: Exploiting `ENROLLEE_SUPPLIES_SAN` Flags and Authentication EKUs to Request Certificates as Arbitrary Domain Admins
* 37.2.2 ESC2 - Any Purpose EKUs & SubCA Templates: Utilizing Any Purpose EKUs or No EKUs for Arbitrary Authentication and Certificate Chain Forgery
* 37.2.3 ESC3 - Certificate Request Agent EKUs: Chaining Enrollment Agent Templates to Request Authentication Certificates on Behalf of Other Users

#### 37.3 Access Control & Security Descriptor Abuse (ESC4, ESC5, ESC7)

* 37.3.1 ESC4 - Vulnerable Template Access Control: Exploiting `WriteDacl`, `WriteProperty`, or `GenericAll` Permissions over Template Objects to Inject Malicious Configurations
* 37.3.2 ESC5 - Vulnerable PKI Network Objects: Abusing Insecure Permissions over CA Computer Objects, PKI Containers, or AD CS File Shares
* 37.3.3 ESC7 - CA Administrator Privilege Abuse: Exploiting Delegated CA Manager Rights (`ManageCA`, `IssueAndManageCertificates`) to Approve Pending Requests and Enable SAN Modifications

#### 37.4 CA Server Configurations & Flag Abuse (ESC6, ESC8, ESC11)

* 37.4.1 ESC6 - `EDITF_ATTRIBUTESUBJECTALTNAME2` Flag: Forcing CAs to Accept Arbitrary SAN Extensions for All Issued Certificates
* 37.4.2 ESC8 - HTTP Enrollment Relaying: Coercing NTLM Authentication from Domain Controllers (via PetitPotam/PrinterBug) to `/certsrv/` Web Enrollment to Request Machine Certificates
* 37.4.3 ESC11 - Unauthenticated RPC Enrollment: Relaying NTLM Authentication over Uncached ICertPassage RPC Interfaces Lacking Packet Privacy (`RPC_C_AUTHN_LEVEL_PKT_PRIVACY`)

#### 37.5 Identity Mapping & Certificate Binding Attacks (ESC9, ESC10, ESC12, ESC13)

* 37.5.1 ESC9/ESC10 - Weak Certificate Identity Mapping: Exploiting `altSecurityIdentities` and No-UPN Mappings to Override Account Bindings
* 37.5.2 ESC12 - Shell Access on CA Hosts: Extracting Private Keys from Hardware Security Modules (HSMs) or Software Key Stores on CA Servers
* 37.5.3 ESC13 - OID Group Linkage Abuse: Abusing Issuance Policy OIDs Mapped to Privileged Active Directory Groups

#### 37.6 PKI Persistence: Golden Certificates

* 37.6.1 CA Private Key Extraction: Dumping CA Root/Subordinate Private Keys from Memory or Registry Hives via `Mimikatz` / `SharpDPAPI`
* 37.6.2 Offline Certificate Forgery: Fabricating Valid, Arbitrary Domain Authentication Certificates without Interacting with the Active CA
* 37.6.3 CA Certificate Renewal and Key Rotation: Invalidating Forged Certificates and Revoking Stolen Root Key Pairs

#### 37.7 Defensive Remediation, PKI Hardening, and Telemetry

* 37.7.1 Enforcing Strong Certificate Binding (KB5014754): Requiring Full Enforcement Mode for OID/SID Bindings across Domain Controllers
* 37.7.2 Hardening AD CS Enrollment Interfaces: Disabling NTLM on HTTP Web Enrollment, Enforcing Extended Protection for Authentication (EPA), and Requiring HTTPS
* 37.7.3 Automated PKI Auditing & SIEM Telemetry: Scanning AD CS Infrastructure with `Certify` / `Certipy`, Auditing Event ID 4886 (Certificate Request Received), Event ID 4887 (Certificate Issued), Event ID 4768 (PKINIT Kerberos Pre-Auth), and MDI PKI Anomaly Alerts

#### 38.1 Machine Account Architecture and Identity Security

* 38.1.1 Machine Account Quota (`ms-DS-MachineAccountQuota`): Default User Rights to Join Computer Objects to the Domain
* 38.1.2 Computer Account Credentials: Automatic LSA 30-Day Password Rotation, Password Entropy, and Local Secret Storage
* 38.1.3 Kerberos Names & Principal Mappings: `sAMAccountName`, `dNSHostName`, Service Principal Names (SPNs), and Account Type Flags (`UAC_WORKSTATION_TRUST_ACCOUNT`)

#### 38.2 On-Premises Machine Account Privilege Escalation

* 38.2.1 Name Collision & Spoofing Vectors: Exploiting `sAMAccountName` Trailing Dollar-Sign Mismatches (CVE-2021-42278 / CVE-2021-42287) to Request DC Service Tickets
* 38.2.2 RBCD & Machine Account Quota Coupling: Creating Controlled Computer Objects to Inject `msDS-AllowedToActOnBehalfOfOtherIdentity` Attributes
* 38.2.3 WebDAV and Coercion Vectors via Machine Accounts: Forcing Computer Account Authentication via WebDAV and NTLM Relay Workflows

#### 38.3 Entra Connect (Azure AD Connect) Architecture & Exploitation

* 38.3.1 Hybrid Identity Synchronization Models: Password Hash Sync (PHS), Pass-Through Authentication (PTA), and AD FS Federation Comparison
* 38.3.2 Extracting Sync Account Secrets: Recovering `MSOL_` Account Hashes and DPAPI Encryption Keys from Azure AD Connect LocalDB / SQL Instances
* 38.3.3 Replaying `MSOL_` Credentials: Utilizing Synchronization Account Privileges to Inject Hybrid Identities and Modify Cloud Password Hashes Directly in Entra ID

#### 38.4 Seamless SSO & Primary Refresh Token (PRT) Abuse

* 38.4.1 Seamless Single Sign-On Mechanics: The `AZUREADSSOACC` Computer Account and Kerberos Kerberized Identity Flow
* 38.4.2 Ticket Forgery via `AZUREADSSOACC` Key Extraction: Generating Kerberos Service Tickets to Bypass Cloud Multi-Factor Authentication (MFA)
* 38.4.3 Hybrid Joined Device Identity Hijacking: Extracting Device Certificates and Replaying Entra ID Primary Refresh Tokens (PRTs)

#### 38.5 Defensive Engineering, Hybrid Guardrails, and Telemetry

* 38.5.1 Machine Account Hardening: Enforcing `ms-DS-MachineAccountQuota = 0` and Deploying Windows LAPS Enterprise-Wide
* 38.5.2 Securing Hybrid Identity Servers: Treating Entra Connect Servers as Tier 0 Assets, Enforcing Conditional Access Policies, and Migrating to Entra Cloud Sync
* 38.5.3 Hybrid Threat Detection & SIEM Correlation: Monitoring Event ID 4741 (Computer Account Created), Event ID 4742 (Computer Account Modified), Entra ID Audit Logs, and Microsoft Defender for Identity (MDI) Hybrid Alerts

#### 39.1 Management Plane Architecture & Tiering Violations

* 39.1.1 Enterprise Access Model (EAM) Breakdown: Evaluating Tier 0 (Control Plane), Tier 1 (Management Plane / Servers), and Tier 2 (User Workstations / Devices)
* 39.1.2 Administrative Exposure Surfaces: Identifying Lateral Movement Pathways Created by Shared Administrative Credentials, Dual-Homed Jump Hosts, and Multi-Tier Management Agents
* 39.1.3 Privileged Access Workstation (PAW) Hardening: Implementing Hardware-Enforced Isolation, Clean Source Principles, and Strict Credential Isolation

#### 39.2 System Center Configuration Manager (SCCM / MCM) Exploitation

* 39.2.1 SCCM Site Hierarchy & Secret Discovery: Enumerating Primary Site Servers, Distribution Points, and Extracting Stored Database Credentials via `SharpSCCM`
* 39.2.2 Client Push Installation Relaying: Forcing NTLM Relays from Fallback Status Points (FSP) or Management Points to Harvest Local Admin and Domain Credentials
* 39.2.3 Arbitrary Application Deployment: Deploying High-Privilege Scripts and Software Packages to Enterprise Targets via Compromised Site Server Consoles

#### 39.3 Out-of-Band & Hypervisor Management Plane Attacks

* 39.3.1 Out-of-Band Interface Compromise: Exploiting Default Credentials, Flawed Web Consoles, and Weak Authentication in IPMI, iDRAC, and iLO Interfaces
* 39.3.2 Hypervisor Host Hijacking: Gaining Shell Access on ESXi / Hyper-V Hosts to Extract Active Directory `NTDS.dit` Databases directly from VM Disks (`.vmdk` / `.vhdx`)
* 39.3.3 Live Memory Snapshots: Extracting Active Domain Controller LSASS Memory and Cryptographic Keys via Virtual Machine Memory Dumps

#### 39.4 Remote Execution & Administrative Protocol Abuse

* 39.4.1 WinRM and PowerShell Remoting: Executing Stealthy In-Memory Payloads via WinRM, Session Hijacking, and Bypassing Constrained Language Mode (CLM)
* 39.4.2 WMI Event Persistence: Creating Permanent WMI Event Consumers and Class Modifications for Unattended System Execution
* 39.4.3 RDP Session Hijacking via `tscon`: Bypassing Authentication to Hijack Active or Disconnected High-Privilege User Sessions

#### 39.5 Hardening, Management Plane Isolation, and Auditing

* 39.5.1 Enforcing Just Enough Administration (JEA): Restricting PowerShell Remoting Endpoint Capabilities via Role Capabilities and Session Configurations
* 39.5.2 Securing Management Agents: Treating SCCM Site Servers, Hypervisors, and Out-of-Band Interfaces as Tier 0 Control Objects
* 39.5.3 Telemetry Correlation & Management Auditing: Monitoring Event ID 4688 (Process Creation with Command Line), Event ID 4104 (PowerShell Script Block Logging), Event ID 4776 (NTLM Validation), Event ID 4624 (Logon Type 10 - Remote Interactive), and MDI Management Anomaly Detections

#### 40.1 Active Directory Trust Architecture and Topologies

* 40.1.1 Trust Types and Directionality: Parent-Child, Cross-Link, Forest, External, and Shortcut Trusts (One-Way vs. Two-Way, Transitive vs. Non-Transitive)
* 40.1.2 The Trust Key Architecture: Cryptographic Shared Secrets (`[TRUST_NAME]$` Accounts), Trust Auth In/Out Attributes, and Password Rotation Mechanics
* 40.1.3 Kerberos Inter-Realm Referral Workflows: How KDCs Process Cross-Domain `TGS-REQ` and Issue Cross-Realm Ticket Granting Tickets (TGTs)

#### 40.2 Cross-Domain Escalation via SID History

* 40.2.1 Mechanics of `sIDHistory`: Historical Identifier Migration for Object Transfers and Active Directory Migrations
* 40.2.2 Injecting Privileged SIDs: Exploiting Domain Admin / Enterprise Admin Credentials in a Child Domain to Inject Tier 0 SIDs into User Attributes
* 40.2.3 Traversing Child-to-Parent Boundaries: Utilizing Injected Enterprise Admins SIDs (`-519`) in Cross-Realm Tickets to Gain Instant Control of the Forest Root Domain

#### 40.3 Trust Security Controls & Bypasses

* 40.3.1 SID Filtering Mechanics: How `Netlogon` and KDCs Filter Foreign SIDs at Trust Boundaries (`EnableSidFiltering` / Quarantine Mode)
* 40.3.2 Selective Authentication Exploitation: Navigating `Allowed-to-Authenticate` Explicit Delegations Across External and Forest Trusts
* 40.3.3 Name Canonicalization & Name Suffix Routing Abuse: Manipulating Name Suffix Routing Tables to Intercept or Spoof Cross-Forest Authentication Requests

#### 40.4 Trust Key Extraction and Ticket Forgery

* 40.4.1 Harvesting Inter-Realm Trust Keys: Extracting Trust Passwords from `NTDS.dit` or LSA Secrets via `Mimikatz` / `lsadump::trust`
* 40.4.2 Forging Inter-Realm TGTs: Constructing Custom Golden Tickets Enriched with Extracted Inter-Realm Keys and Modified PAC SIDs
* 40.4.3 Maintaining Cross-Forest Persistence: Establishing Hidden Cross-Domain Access via Persistent Trust Key Manipulation

#### 40.5 Hybrid & Cloud Trust Traversal

* 40.5.1 Entra ID Cross-Tenant Access Policies (CTAP): Evaluating Inbound/Outbound Trust Rules for Multi-Tenant B2B Workflows
* 40.5.2 B2B Guest Identity Abuse: Exploiting Over-Permissive Guest User Capabilities and Cross-Tenant Application Registrations
* 40.5.3 Federated Trust Exploitation (AD FS / SAML): Stealing Token Signing Certificates to Forge SAML Assertions Across Federated Trust Boundaries

#### 40.6 Hardening Trust Boundaries, Governance, and Telemetry

* 40.6.1 Enforcing Strict Trust Security Baselines: Mandating SID Filtering (Quarantine), Disabling Transitivity on External Trusts, and Enabling Selective Authentication
* 40.6.2 Trust Key Lifecycle Management: Implementing Automated Trust Password Rotation Protocols and Monitoring Trust Modifications
* 40.6.3 Cross-Forest SIEM Auditing & Telemetry: Monitoring Event ID 4706 (A Trust Relationship Was Created), Event ID 4707 (A Trust Relationship Was Removed), Event ID 4769 (Cross-Domain Service Ticket Requests), and MDI Cross-Forest Traversal Alerts

#### 41.1 Active Directory Replication Mechanics and Protocols

* 41.1.1 Directory Services Architecture: Partition Synchronization (Domain, Configuration, Schema, Application) and High-Water Marks / USN Vectoring
* 41.1.2 MS-DRSR and MS-ADDM RPC Protocols: Technical Mechanics of `DSGetNCChanges`, `DSAddEntry`, and Replication RPC Binding Handles
* 41.1.3 Security Descriptors on Domain Objects: Evaluating `Replicating Directory Changes`, `Replicating Directory Changes All`, and `Replicating Directory Changes In Filtered Set`

#### 41.2 Directory Replication Service Abuse (DCSync)

* 41.2.1 DCSync Execution Mechanics: Simulating Domain Controller Sync Requests via `lsadump::dcsync` and `impacket-dcsync`
* 41.2.2 Harvesting `krbtgt`, Machine Accounts, and Administrative Hashes: Pulling Current and Historical Password Hashes without Executing Code on DCs
* 41.2.3 Restricting and Auditing Replication Delegations: Identifying Non-DC Accounts Granted DRS Rights and Cleaning Misconfigured Directory DACLs

#### 41.3 Rogue Domain Controller Registration (DCShadow)

* 41.3.1 DCShadow Protocol Architecture: Registering Temporary Infrastructure Objects in `CN=Configuration` and `CN=Schema`
* 41.3.2 Pushing Unauthorized Replication Updates: Forcing Revisions to Object Attributes (`sIDHistory`, `primaryGroupID`, DACLs) via KCC and RPC Calls
* 41.3.3 Bypassing Event Log Auditing: Exploiting the Lack of Object Modification Log Generation (Event ID 5136) on Target DCs During Replication Ingestion

#### 41.4 Persistent Ticket Forgery: Golden and Silver Tickets

* 41.4.1 Golden Ticket Forgery Mechanics: Utilizing `krbtgt` AES Keys to Craft Fully Authorized TGTs with Custom Group SIDs and Non-Expiring Lifetimes
* 41.4.2 Silver Ticket Forgery Mechanics: Utilizing Service Account Keys (e.g., Computer `sAMAccountName`, Service Accounts) to Forge Targeted TGS Tickets
* 41.4.3 PAC Customization and PAC Validation Bypasses: Injecting Arbitrary PAC Claims, SIDs, and Exploiting Unenforced PAC Signature Validation Protocols

#### 41.5 Internal Schema, Object, and Memory Persistence

* 41.5.1 AdminSDHolder and SDProp Abuse: Maintaining Backdoors in `CN=AdminSDHolder` for Automated Privilege Re-Granting
* 41.5.2 DSRM Account Exploitation: Modifying `DsrmAdminLogonBehavior` to Enable Local Admin RDP/WinRM Access on DCs via the DSRM Account
* 41.5.3 LSASS Memory Patching (Skeleton Key): Injecting In-Memory Passwords into DC LSASS Threads to Grant Universal Password Access
* 41.5.4 Password Filter DLLs and Custom SSPs: Registering Malicious LSA Security Support Providers (`sspicli.dll`) for Plaintext Password Interception

#### 41.6 Dual-Rotation `krbtgt` Eviction and Remediation

* 41.6.1 The Dual-Rotation Lifecycle: Mechanics of Rotating the `krbtgt` Password Twice to Flush Historical Encryption Keys from KDC Caches
* 41.6.2 Scripted Rotation Playbooks: Automating Safe `krbtgt` Password Resets (`Reset-KrbTgtPassword`) Accounting for Replication Latency and Kerberos Ticket Lifetime Windows
* 41.6.3 Validating Enterprise Recovery: Ensuring Zero Residual Golden Ticket Activity Across Cross-Forest and Child Domain Enclaves

#### 41.7 Defensive Auditing, SIEM Telemetry, and Threat Hunting

* 41.7.1 Auditing Replication Events: Tracking Event ID 4662 (Operation Performed on Object) for Replication Extended Rights Access Requests
* 41.7.2 Detecting DCShadow and Rogue DCs: Monitoring Schema Modifications, `CN=Configuration` Class Changes, and Network RPC Binding Anomalies
* 41.7.3 Microsoft Defender for Identity (MDI) Alerts: Correlating DCSync Requests, Suspicious Ticket Renewal/PAC Anomalies, and Skeleton Key Detections

The Directory is a "collection of open systems cooperating to provide directory services" \[X.500]. A directory user, which may be a human or non-person entity (NPE), accesses the Directory through a client (or Directory User Agent (DUA)). The client, on behalf of the directory user's authorized and authenticated login, interacts with one or more servers (or Directory System Agents (DSA)). Clients therefore interact with servers using a directory access protocol.

This section details the protocol elements of the Lightweight Directory Access Protocol (LDAP), along with its semantics. Following the description of protocol elements, it describes the way in which the protocol elements are encoded and transferred across infrastructure.

Key Words

**Transport Connection.** Refers to the underlying transport services used to carry the protocol exchange over the network, as well as the associations established by these services.

**SASL Layer.** Refers to Simply Authentication and Security Layer (SASL) services used in providing security services, as well as the associations established by these services.

**LDAP Message Layer.** Refers to the LDAP Message Protocol Data Unit (PDU) services used in providing directory services, as well as the associations established by these services.

**LDAP Session.** Refers to combined services (transport connection, TLS layer, SASL layer, LDAP message layer) as well as their associations.

#### LDAP Protocol Model

The general model adopted by this protocol is one of clients performing protocol operations against network servers, both on-premises an, cloud, and hybrid environments. In this model, a client transmits a protocol request describing the operation to be performed to a server. The server is then responsible for performing the necessary operation(s) in the Directory. Upon completion of an operation, the server typically returns a response containing appropriate data to the requesting client.&#x20;

Protocol operations are generally independent of one another. Each operation is processed as an atomic action, leaving the directory in a consistent state.

Although servers are required to return responses whenever such responses are explicitly defined in the protocol to do so, there is no mandatory requirement for synchronous behavior on the part of either clients or servers. Requests and responses for multiple operations generally may be exchanged between a client and a server in any order. If required, synchronous behavior may be controlled by client applications.

#### Operation and LDAP Message Layer Relationship

Protocol operations are exchanged at the LDAP message layer. When the transport connection is closed, any uncompleted operations at the LDAP message layer are then abandoned (when possible) or are completed without transmission of the response (when abandoning them is not possible). Also, when the transport connection is closed, the client must not assume that any uncompleted update operations have either succeeded or failed.

### Mind Control and Cognitive Networking

* [**RFC 1097**](https://www.ietf.org/rfc/rfc1149.txt) **(1989) - TELNET Subliminal-Message Option**: A protocol allowing server administrators to inject subconscious visual frames directly into a user's terminal to subtly influence their behavior during a session.

### Classic Joke and Experimental RFCs

* [**RFC 1149**](https://www.ietf.org/rfc/rfc1149.txt): Standard for the Transmission of IP Datagrams on **Avian Carriers** (proposing data transfer via **carrier pigeon**, which was actually implemented as a real test in 1999).
* [**RFC 2324**](https://www.ietf.org/rfc/rfc2324.txt): Hyper Text Coffee Pot Control Protocol (**HTCPCP/1.0**) for controlling, monitoring, and diagnosing coffee pots.
* [**RFC 2795**](https://www.ietf.org/rfc/rfc2795.txt): The **Infinite Monkey Protocol Suite** (IMPS), outlining how to use an infinite number of monkeys at typewriters to reproduce the works of Shakespeare.
* [**RFC 3251**](https://www.ietf.org/rfc/rfc3251.txt): **Electricity over IP** (EoIP), detailing how to transmit electrical power straight through ethernet cables to run household appliances.
* [**RFC 3514**](https://www.ietf.org/rfc/rfc3514.txt): The **Evil Bit**, proposing a single 1-bit flag in IPv4 headers to let packets explicitly declare if they are sent with malicious intent.



### 🕊️ The Avian Carrier Trilogy (IP over Homing Pigeons)

* [**RFC 1149**](https://www.ietf.org/rfc/rfc1149.txt) **(1990) – IP on Avian Carriers**: Explains how to print a packet hex dump, roll it around a pigeon's leg, and unleash it into the air. _(Famously implemented in Norway in 2000; it successfully transferred 4 packets with 55% packet loss and a ping time of \~5,000,000 milliseconds)._
* [**RFC 2549**](https://www.ietf.org/rfc/rfc2549.txt) **(1999) – IP on Avian Carriers with Quality of Service**: An upgrade to the protocol adding QoS flags. It technically handles "multi-cast" (releasing multiple pigeons) and details a major bug: native predators (hawks), which act as a physical layer firewall.
* [**RFC 6214**](https://www.ietf.org/rfc/rfc6214.txt) **(2011) – Adaptation of RFC 1149 for IPv6**: Standardizes the pigeon protocol to accommodate the much larger IPv6 address headers, noting that the physical weight of printing a larger header may limit the pigeon's flight velocity.

### ☕ Smart Home & Kitchen Protocols

* [**RFC 2324**](https://www.ietf.org/rfc/rfc2324.txt) **(1998) – Hyper Text Coffee Pot Control Protocol (HTCPCP)**: Formally defines how to request coffee over the network. It gave birth to the internet’s favorite error message: `HTTP 418 I'm a teapot`, which states a teapot must refuse to brew coffee.
* [**RFC 7168**](https://www.ietf.org/rfc/rfc7168.txt) **(2014) – HTCPCP Extended for Tea**: An essential correction to the original coffee pot protocol, expanding the error structures to adequately handle loose-leaf tea, milk variants, and steeping times.

### 🎭 Hardware, Physics, and Sci-Fi Extensions

* [**RFC 1925**](https://datatracker.ietf.org/doc/html/rfc1925) **(1996) – The Twelve Networking Truths**: While humorous, this is actually a deeply respected list of fundamental computer truths. Fundamental Truth #1: _"It has to work."_ Fundamental Truth #4: _"With sufficient thrust, pigs fly just fine."_
* [**RFC 2795**](https://www.ietf.org/rfc/rfc2795.txt) **(2000) – The Infinite Monkey Protocol Suite**: A comprehensive framework for managing and routing traffic generated by an infinite array of monkeys typing at keyboards to create Shakespearean text.
* [**RFC 3251**](https://www.ietf.org/rfc/rfc3251.txt) **(2002) – Electricity over IP (EoIP)**: Explains how to break down high-voltage alternating current into discrete internet packets, allowing you to power your microwave through an Ethernet connection.
* [**RFC 9564**](https://datatracker.ietf.org/doc/rfc9564/) **(2024) – Faster-Than-Light (FTL) Encapsulation**: Addresses the issue of networking over warp drive, providing a framework for packets that arrive at their destination before they are sent.

### ⚖️ Human Behavior, Moods, and Social Media

* [**RFC 2482**](https://datatracker.ietf.org/doc/html/rfc2482) **(1999) – Language Tags in Data Transmission**: Standardizes how to transmit "sarcasm" over a network line so computers don't interpret it literally.
* [**RFC 4824**](https://www.ietf.org/rfc/rfc4824.txt) **(2007) – The Semaphore Flag Signaling System (SFSS)**: Adapts IP packets for transmission using maritime hand-held flags, tracking what happens when the flag-waver gets tired (packet degradation).
* [**RFC 5514**](https://datatracker.ietf.org/doc/html/rfc5514) **(2009) – IPv6 over Social Networks**: Proposes a way to map IPv6 architecture entirely into user profile structures on social networks, utilizing "pokes" and status updates as transport mechanics.
* [**RFC 5841**](https://www.ietf.org/rfc/rfc5841.txt) **(2010) – TCP Option to Denote Packet Mood**: Adds an emotional element to packets. Packet headers could be structurally flagged as `0x10` (Happy), `0x11` (Sad), or `0x14` (Anxious), allowing routers to prioritize "depressed" packets to cheer them up.

### 🛑 Security, Paranoia, and The "Evil Bit"

* [**RFC 3514**](https://www.ietf.org/rfc/rfc3514.txt) **(2003) – The Security Flag in the IPv4 Header (The Evil Bit)**: Solves all of cybersecurity by suggesting a 1-bit flag in every internet packet. If a packet is sent by a hacker with malicious intent, the bit is flipped to `1`. If it's a good packet, it's `0`. Firewalls would simply drop all packets with the "Evil Bit" enabled.
* [**RFC 3751**](https://datatracker.ietf.org/doc/html/rfc3751) **(2004) – Omniscience Protocol Requirements**: Explores the networking prerequisites required if the IETF were to build a standard for an all-knowing, telepathic network infrastructure.
* [**RFC 6592**](https://datatracker.ietf.org/doc/html/rfc6592) **(2012) – The Null Packet**: Standardizes a packet that contains absolutely nothing—no header, no payload, no footprint—and discusses how to properly handle a packet that doesn't exist.

### 📜 Pre-1990s Historical Anomalies

* [**RFC 527**](https://datatracker.ietf.org/doc/html/rfc527) **(1973) – ARPAWOCKY**: The oldest known joke RFC. Written by R. Merryman, it is a complete parody of Lewis Carroll’s nonsense poem _"Jabberwocky"_, rewritten to complain about the ARPANET host protocols.
* [**RFC 748**](https://datatracker.ietf.org/doc/html/rfc748) **(1978) – Telnet Randomly-Lose Option**: A proposal for a Telnet server option that randomly discards data during a session to keep user attention sharp.
* [**RFC 968**](https://datatracker.ietf.org/doc/html/rfc968) **(1985) – 'Twas the Night Before Start-up**: Written by Vint Cerf (one of the "fathers of the internet"), this is a complete rewrite of the classic Christmas poem about trying to get a network node online before morning.













