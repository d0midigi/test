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

#### 42.1 Identity Infrastructure Vulnerability Classes

* 42.1.1 Architectural Vulnerability Vectors: Protocol Downgrades, Cryptographic Implementation Flaws, and Memory Corruption in Domain Services
* 42.1.2 Unauthenticated Remote Code Execution: Impact of High-Severity Flaws in Core AD RPC Interfaces
* 42.1.3 Exposure Surface Minimization: Isolating DC Interfaces and Hardening Network-Level Authentication (NLA)

#### 42.2 Domain Controller Vulnerabilities

* 42.2.1 Remote Code Execution Flaws: Exploiting Unpatched Memory Errors and Serialization Vulnerabilities in DC Services
* 42.2.2 Service Coercion Protocols: Abusing MS-RPRN (PrinterBug), MS-EFSR (PetitPotam), and MS-DFSNM (DFSCoerce) to Force DC Authentication
* 42.2.3 Host Isolation & Hardening: Enforcing Strict Protocol Whitelisting, Disabling Unused RPC Interfaces, and Enforcing RPC Packet Privacy

#### 42.3 Netlogon Vulnerabilities

* 42.3.1 Cryptographic Flaws in Netlogon (Zerologon / CVE-2020-1472): Abusing Insecure AES-CFB8 Initialization Vectors to Zero Out DC Machine Passwords
* 42.3.2 Channel Binding & Secure RPC: Exploiting Unenforced `Netlogon` Secure Channel Bindings
* 42.3.3 Mitigation & Enforcement Modes: Monitoring Event ID 5829 and Enforcing Strict Netlogon Secure Channel Requirements Enterprise-Wide

#### 42.4 KDC and Kerberos Vulnerabilities

* 42.4.1 PAC Validation Bypasses (MS14-068 / CVE-2021-42287): Forging Privilege Attribute Certificates to Claim Immediate Domain Admin Rights
* 42.4.2 Cryptographic Downgrade Attacks: Forcing KDCs to Negotiate Weak RC4-HMAC Encryption for Ticket Granting Service (TGS) Requests
* 42.4.3 KDC Patching & Hardening: Disabling Weak Ciphers (DES/RC4), Enforcing AES128/256, and Monitoring KDC Anomaly Events

#### 42.5 LDAP Vulnerabilities

* 42.5.1 Unauthenticated Bindings and LDAP Injection: Exploiting Weak Search Filters and Insecure Anonymous Binds
* 42.5.2 LDAP Signing and Channel Binding Enforcement: Relaying NTLM Authentication over Plaintext LDAP (TCP 389) Services
* 42.5.3 Enforcing LDAPS & Channel Binding: Requiring Signed LDAP (LDAPS / TCP 636) and Enforcing Extended Protection for Authentication (EPA)

#### 42.6 AD CS Vulnerabilities

* 42.6.1 Certificate Engine Exploitation: Leveraging Template Misconfigurations and Unauthenticated Web Enrollment Points
* 42.6.2 Relaying to AD CS Endpoints: Coercing DC Authentication and Relaying to HTTP/RPC Certificate Services (ESC8/ESC11)
* 42.6.3 Hardening PKI Infrastructure: Disabling NTLM on Web Enrollment, Enforcing EPA, and Enforcing KB5014754 Strong Certificate Binding

#### 42.7 Federation-Service Vulnerabilities

* 42.7.1 AD FS Software & Endpoint Exploitation: Targetting Authentication Protocols and Endpoints on Federated Identity Servers
* 42.7.2 SAML Token Signing Key Extraction: Stealing Cryptographic Keys to Sign Forged SAML Assertions Off-Host
* 42.7.3 Federation Security Baselines: Segmenting AD FS Proxy Servers (WAP), Enforcing MFA for SAML Endpoints, and Migrating to Native Entra ID Auth

#### 42.8 Cloud and Synchronization Vulnerabilities

* 42.8.1 Entra Connect Server Compromise: Extracting `MSOL_` Passwords and SQL Encryption Keys to Intercept Sync Pipelines
* 42.8.2 Password Hash Sync (PHS) Exploitation: Injecting Modified Password Hashes Directly into Cloud Tenants via Compromised Sync Agents
* 42.8.3 Securing Hybrid Pipelines: Treating Sync Servers as Tier 0 Assets, Enforcing Cloud Sync Architecture, and Isolating Sync Service Credentials

#### 42.9 Authentication Denial

* 42.9.1 Distributed Account Lockout Attacks: Exploiting Publicly Accessible Authentication Endpoints to Lock Out Privileged Enterprise Accounts
* 42.9.2 KDC Resource Exhaustion: Flooding Domain Controllers with Malformed Kerberos Requests to Trigger Denial of Service (DoS)
* 42.9.3 Mitigating Auth DoS: Implementing Smart Lockout Policies, Rate-Limiting Authentication Requests, and Isolating Internal KDCs

#### 42.10 Directory Sabotage

* 42.10.1 Mass Schema and Attribute Corruption: Executing Destructive Scripting to Delete or Overwrite Critical Directory Objects (`CN=Configuration`)
* 42.10.2 Disruption of Replication Topology: Overwriting USN Vectors and Modifying Partition Metadata to Cause Directory Replication Collapses
* 42.10.3 **Restoring Directory Integrity**: Deploying Active Directory Authoritative Restores and Enforcing Immutable Directory Snapshots

#### 42.11 GPO Destruction

* 42.11.1 **Mass GPO Overwriting**: Injecting Malicious or Blank `SYSVOL` Scripts to Wipe Local Computer Security Configurations
* 42.11.2 **Unlinking Core Group Policy Objects (GPO)**: Detaching Default Domain and Domain Controller Policies to Neutralize Enterprise-Wide Security Controls
* 42.11.3 **`SYSVOL` Protection and Auditing:** Restricting `Write` Access to `SYSVOL` Policies, Monitoring Event ID 5136 and GPO Modification Logs

#### 42.12 Domain Trust Corruption

* 42.12.1 **Severing Inter-Realm Trust Passwords**: Overwriting Shared Trust Secrets to Induce Cross-Forest Authentication Outages
* 42.12.2 **Routing Table Modification**: Manipulating Name Suffix Routing Tables to Route Inter-Forest Authentication Requests to Attacker Infrastructure
* 42.12.3 **Trust Resilience**: Automating Trust Key Health Checks and Enforcing Selective Authentication Protocols

#### 42.13 Ransomware and Wipers That Target Active Directory Domain Components

* 42.13.1 **Group Policy Object (GPO)-Driven Ransomware Deployment**: Abusing Active Directory Group Policy to Simultaneously Push Ransomware Payloads to All Domain-Joined Systems
* 42.13.2 **Domain Controller Wipe Attacks**: Executing Low-Level Disk Wipers to Destroy the `NTDS.dit` Database and System State Files
* 42.13.3 **Rapid Isolation and Backup Recovery**: Implementing Offline Air-Gapped Backups, Immutable Storage, and Isolated Forest Recovery Playbooks

#### 42.14 Loss of Administrative Control

* 42.14.1 Complete Tier 0 Lockout: Modifying All Domain Admin / Enterprise Admin Credentials and Revoking Emergency Access Handles
* 42.14.2 Active Directory Database Encryption: Encrypting `NTDS.dit` In-Place to Prevent KDC and Directory Service Initialization
* 42.14.3 Break-Glass Recovery Mechanisms: Maintaining Out-of-Band Physical Break-Glass Accounts and Isolated Standalone Recovery Controllers

#### 42.15 Mission Degradation and Operational Impact

* 42.15.1 Cascading Enterprise System Failures: How Loss of Identity Halts Network Access, Email, PKI, and Operational Technology (OT) Systems
* 42.15.2 Critical Infrastructure Impact: Quantifying Operational Stoppage in SCADA, Defense Enclaves, and Government Operations
* 42.15.3 Continuity of Operations (COOP) Execution: Executing Forest Recovery Procedures to Re-establish Minimum Operational Identity Capabilities

## <mark style="color:cyan;">**PART V - Defensive Identity Engineering**</mark>

### <mark style="color:cyan;">**Chapter 43 - Enterprise Access Model and Privileged Administration**</mark>

#### 43.1 From Legacy Tiering to the Enterprise Access Model

* 43.1.1 Evolution of Administrative Isolation: Transitioning from the Traditional 3-Tier Model (Tier 0/1/2) to the Enterprise Access Model (EAM)
* 43.1.2 Plane Segmentation Overview: Mapping Control Planes, Management Planes, and User Access Planes
* 43.1.3 Alignment with Zero Trust Architecture: Enforcing Explicit Verification and Least Privilege Access Across Administrative Boundaries (NIST SP 800-207)

#### 43.2 Tier 0, Tier 1, and Tier 2

* 43.2.1 Control Plane (Tier 0): Securing Identity Store Assets (Domain Controllers, PKI, AD FS, Entra ID, Key Management Systems)
* 43.2.2 Management Plane (Tier 1): Enterprise Servers, Hypervisors, Database Engines, SCCM/MCM, and Line-of-Business Applications
* 43.2.3 User Access Plane (Tier 2): End-User Workstations, Mobile Devices, Peripheral Assets, and User Identity Contexts

#### 43.3 Clean Source Principle and Control Plane Isolation

* 43.3.1 Clean Source Mechanics: Ensuring Administrative Dependencies Meet or Exceed the Trust Level of the Target Managed System
* 43.3.2 Identifying Dependency Violations: Auditing Cross-Plane Jump Hosts, Shared Storage, Management Agents, and Dual-Homed Devices
* 43.3.3 Technical Boundary Enforcement: Applying Network Microsegmentation, Firewall Enclaves, and Strict IP Whitelisting for Control Plane Interfaces

#### 43.4 Privileged Access Workstations (PAWs) and SAWs

* 43.4.1 PAW Architecture & Hardware-Enforced Isolation: Deploying Hardened Workstations with Virtualization-Based Security (VBS) and Device Guard
* 43.4.2 PAW Deployment Models: Comparing Dedicated Physical PAWs, Dual-Device Strategies, and Virtualized Administrative Desktops
* 43.4.3 Securing PAW Lifecycle: Restricting Web Browsing, Email Clients, Local Admin Access, and Unapproved Software Ingestion on PAWs

#### 43.5 Administrative Identity Segregation and Credential Isolation

* 43.5.1 Account Naming Conventions & Segregation: Provisioning Distinct Accounts for Control Plane (`admin_user_t0`), Server Admin (`admin_user_t1`), and Daily Use
* 43.5.2 Blocking Cross-Plane Authentication: Applying `Deny Logon Through Remote Desktop Services` and `Deny Logon Locally` User Rights via GPOs
* 43.5.3 Restricted Admin Mode & Remote Credential Guard: Securing RDP Sessions to Prevent Credential Caching in LSASS on Target Systems

#### 43.6 Just-In-Time (JIT) and Just-Enough-Administration (JEA)

* 43.6.1 Eliminating Standing Privileges: Implementing Ephemeral Group Memberships and Time-Bound Role Assignment
* 43.6.2 PowerShell Just-Enough-Administration (JEA): Creating Constrained Endpoint Configurations, Role Capability Definitions, and Command Whitelisting
* 43.6.3 Operationalizing JEA Endpoints: Delegating Helpdesk and System Admin Tasks Without Granting Native Domain Admin Access

#### 43.7 Privileged Access Management (PAM) and Break-Glass Architecture

* 43.7.1 PAM Infrastructure & Session Vaulting: Deploying Privileged Access Management Bastions for Password Auto-Rotation and Session Recording
* 43.7.2 Cloud & On-Premises Break-Glass Accounts: Configuring Out-of-Band Emergency Accounts Excluded from Conditional Access and MFA Dependencies
* 43.7.3 Auditing Emergency Access: Real-Time Alerting and Automated Incident Workflows Triggered Upon Any Break-Glass Account Authentication Event

#### 43.8 Hybrid Identity Governance and Privileged Cloud Roles

* 43.8.1 Entra ID Privileged Identity Management (PIM): Configuring Time-Bound Activation, Approval Workflows, and Justification Rules for Cloud Roles
* 43.8.2 High-Privilege Role Isolation: Securing Global Administrator, Privileged Role Administrator, and Hybrid Identity Administrator Accounts
* 43.8.3 Aligning On-Premises Tier 0 with Entra ID: Establishing Unified Control Plane Boundaries Across Hybrid Directory Environments

#### 43.9 Hardening, Auditing, and Administrative Telemetry

* 43.9.1 User Rights Assignment Baselines: Configuring `Enable Admin Approval Mode`, Disabling Local Account Use of Blank Passwords, and Restricting Network Logons
* 43.9.2 Telemetry Event Monitoring: Auditing Event ID 4672 (Special Privileges Assigned), Event ID 4624 (Logon Types 2/3/10), and Event ID 4104 (Script Block Logging)
* 43.9.3 Microsoft Defender for Identity (MDI) Integration: Tracking Sensitive Account Lateral Movement Paths and Administrative Anomaly Alerts

***

### <mark style="color:cyan;">**Chapter 44 - Identity Lifecycle Hardening**</mark>

#### 44.1 Human Identity Hygiene

* 44.1.1 Enterprise Naming & Provisioning Baselines: Standardizing Identity Identifiers, UPN Mappings, and Immutable Object GUIDs
* 44.1.2 Least Privilege Identity Onboarding: Minimizing Initial Entitlements and Default Group Assignments During Account Provisioning
* 44.1.3 Continuous Identity Auditing: Enforcing Periodic Access Certification Cycles and Account Telemetry Reviews

#### 44.2 Joiner-Mover-Leaver Controls

* 44.2.1 Joiner Automated Workflows: Integrating HR Systems with Active Directory / Entra ID via SCIM and Automated Identity Pipelines
* 44.2.2 Mover Entitlement Hygiene: Clearing Residual Group Memberships and Delegated Permissions During Intra-Organizational Transfers
* 44.2.3 Leaver Offboarding Enforcement: Immediate Deprovisioning, Session Termination, Kerberos Ticket Invalidation, and Token Revocation Protocols

#### 44.3 Stale and Orphaned Accounts

* 44.3.1 Identifying Dormant Identities: Querying `lastLogonTimestamp`, `pwdLastSet`, and Interactive Sign-In Logs via PowerShell and LDAP
* 44.3.2 Automated Lifecycle Quarantine: Moving Inactive Accounts to Isolated OUs, Stripping Privileges, and Disabling Account Objects
* 44.3.3 Orphaned Account Decommissioning: Deleting Abandoned Test Accounts, Former Vendor Access, and Legacy Administrative Handles

#### 44.4 Privileged Group Governance

* 44.4.1 Tier 0 Group Auditing: Restricting Standing Memberships in `Domain Admins`, `Enterprise Admins`, `Schema Admins`, and `Account Operators`
* 44.4.2 Shadow Admin Identification: Scanning Direct and Transitive DACL Assignments Granting Administrative Control Over Directory Objects
* 44.4.3 Access Certification & Recertification: Implementing Automated Approval Workflows for Privileged Group Inclusion

#### 44.5 Windows LAPS

* 44.5.1 Windows LAPS Architecture: Schema Extensions, Centralized Encryption, and Automated Local Admin Password Rotation
* 44.5.2 Delegating LAPS Read Permissions: Auditing DACLs over `msLAPS-Password` Attributes to Prevent Insecure Secret Exposure
* 44.5.3 Hybrid LAPS Integration: Synchronizing Local Administrator Passwords to Entra ID and Enforcing Access Auditing

#### 44.6 Service Account Hardening

* 44.6.1 Service Account Discovery: Cataloging Interactive Service Accounts, Scheduled Tasks, and Application Pool Identities
* 44.6.2 Enforcing Non-Interactive Logons: Assigning `Deny Logon Locally` and `Deny Logon Through Remote Desktop Services` Rights
* 44.6.3 Hardening Passwords and Encryption: Enforcing 128-Character Passwords and AES128/256-Only Kerberos Encryption Flags

#### 44.7 MSA, gMSA, and dMSA

* 44.7.1 Standalone Managed Service Accounts (sMSA): Architecture, Automatic Password Management, and Host Binding Limits
* 44.7.2 Group Managed Service Accounts (gMSA): Key Distribution Service (KDS) Root Keys, `msDS-GroupMSAMembership` Security Descriptors, and Deployment
* 44.7.3 Delegated Managed Service Accounts (dMSA): Windows Server 2025 dMSA Architecture, Binding Service Accounts to Machine Identifiers, and Eliminating Stored Hashes

#### 44.8 SPN Governance

* 44.8.1 Service Principal Name Auditing: Cataloging Duplicate, Orphaned, and Weakly Authenticated SPNs Across the Directory
* 44.8.2 Kerberoasting Surface Reduction: Identifying High-Privilege Accounts with Registered SPNs and Migrating Services to gMSAs
* 44.8.3 SPN Lifecycle Automation: Binding SPN Registration Rights to Automated Service Deployment Pipelines

#### 44.9 Non-Person Identity Governance

* 44.9.1 Non-Person Identity (NPI) Classification: Categorizing API Keys, Service Principals, Automated Test Drivers, and Network Device Credentials
* 44.9.2 Ownership & Custody Assignment: Binding Every NPI to an Active Human Custodian and Business Unit
* 44.9.3 Cryptographic Key Binding: Replacing Plaintext Secrets with Mutual TLS (mTLS) and Hardware-Backed Private Keys

#### 44.10 Workload Identity Security

* 44.10.1 Cloud & Hybrid Workload Identities: Securing Entra ID Service Principals, Managed Identities, and App Registrations
* 44.10.2 Conditional Access for Workload Identities: Enforcing Location, IP, and Risk-Based Policies for Service Account Interactions
* 44.10.3 Credential Hygiene & Expiration: Blocking Long-Lived Client Secrets and Enforcing Federated Identity Credentials (OIDC)

#### 44.11 Device Identity Hardening

* 44.11.1 Domain-Joined Device Hygiene: Auditing Machine Account Creation, Password Rotation, and Stale Computer Objects
* 44.11.2 Hybrid Joined & Workplace Joined Devices: Securing Primary Refresh Tokens (PRTs) and TPM-Backed Device Certificates
* 44.11.3 Device Health Attestation: Integrating TPM-Based Health Certificates into Network Access Control (NAC) and Conditional Access

#### 44.12 Password and Fine-Grained Password Policies

* 44.12.1 Domain Password Policy Limitations: Evaluating Legacy Single-Policy Restrictions in Active Directory Domains
* 44.12.2 Fine-Grained Password Policies (FGPP): Configuring Password Settings Objects (PSOs) and `msDS-PSOAppliesTo` Attributes for Sensitive Accounts
* 44.12.3 Password Protection & Banned Words: Integrating Entra Password Protection On-Premises to Block Common Passwords and Dict Patterns

#### 44.13 Account Lockout

* 44.13.1 Lockout Threshold Mechanics: Balancing Denial-of-Service (DoS) Risks against Password Guessing Mitigation
* 44.13.2 Smart Lockout Policies: Differentiating Between Authorized User Locations and Malicious Authentication Floods
* 44.13.3 Investigating Lockout Sources: Tracing Persistent Lockout Causes via Netlogon Logs and Event ID 4740 Telemetry

#### 44.14 Credential Rotation

* 44.14.1 Automated Rotation Intervals: Establishing Rotation Cycles for Service Accounts, Computer Accounts, and High-Privilege Users
* 44.14.2 Dual-Key Rotation Protocols: Managing Overlapping Rotation Windows for High-Availability Services to Prevent Downtime
* 44.14.3 Emergency Credential Invalidation: Rapid-Reset Playbooks for Compromised Cryptographic Keys and Enterprise Accounts

#### 44.15 Authenticator Recovery

* 44.15.1 Lost Authenticators: Provisions for Temporary Access Passes (TAP), FIDO2 Key Replacement, and Hardware Token Revocation
* 44.15.2 MFA Reset: Securing Helpdesk Support Workflows Against Social Engineering Attacks Targetting Phone/App MFA Resets
* 44.15.3 Reproofing: High-Assurance In-Person or Remote Identity Proofing (NIST SP 800-63A IAL2/IAL3) Before Issuing Replacement Credentials
* 44.15.4 Credential Replacement: Secure Out-of-Band Delivery Channels for Initial Passwords, TAP Tokens, and Security Keys
* 44.15.5 Revocation: Invalidating Active Refresh Tokens, Clearing Kerberos Ticket Caches, and Terminating Active Sessions Enterprise-Wide

#### 45.1 Domain Controller Isolation

* 45.1.1 Tier 0 Network Microsegmentation: Placing Domain Controllers in Isolated VLAN Enclaves with Strict Stateful Firewall Rules
* 45.1.2 Restricting Inbound RPC and Management Traffic: Whitelisting Only Necessary RPC Dynamic Ports, Kerberos (88), LDAPS (636), and SMB (445)
* 45.1.3 Host-Based Firewalls and IPsec Policies: Enforcing Windows Defender Firewall with Advanced Security to Block Lateral Movement from Lower-Tier Servers

#### 45.2 RODC Security

* 45.2.1 Read-Only Domain Controller Deployment Architecture: Isolating Branch Office and Low Physical Security Environments
* 45.2.2 Unidirectional Replication Mechanics: Preventing Inbound Directory Changes from RODCs to Writable DCs
* 45.2.3 Delegated Administrator Accounts: Granting Limited Local Administrative Privileges Without Delegating Domain-Wide Rights

#### 45.3 Password Replication Policy

* 45.3.1 PRP Mechanics & Credential Caching: Filtering Which User and Computer Password Hashes Are Stored on RODCs
* 45.3.2 Default Denied and Allowed Groups: Enforcing Implicit Deny Rules for `Domain Admins`, `Enterprise Admins`, and Sensitive Service Accounts
* 45.3.3 Auditing Cached Credentials: Utilizing `Get-ADDomainControllerPasswordReplicationPolicy` to Verify PRP Compliance and Identify High-Risk Accounts

#### 45.4 Replication Rights

* 45.4.1 Directory Replication Service (DRS) Permissions: Auditing `Replicating Directory Changes` and `Replicating Directory Changes All`
* 45.4.2 Restricting Non-DC Replication Grants: Eliminating Unwanted Extended Rights that Enable DCSync Attacks
* 45.4.3 Monitoring Replication Access: Tracking Event ID 4662 (Operation Performed on Object) for Replication Right Usage

#### 45.5 FSMO Protection

* 45.5.1 Flexible Single Master Operation (FSMO) Roles: Hardening PDC Emulator, RID Master, Infrastructure Master, Schema Master, and Domain Naming Master
* 45.5.2 Placement Strategy & Network Isolation: Distributing FSMO Roles Across Dedicated, Highly Available Tier 0 Domain Controllers
* 45.5.3 Seizure & Transfer Protocols: Establishing Emergency FSMO Role Seizure Playbooks in Response to Offline DC Events

#### 45.6 Global Catalog Security

* 45.6.1 Global Catalog (GC) Infrastructure: Managing Universal Group Membership Caching and Cross-Domain Query Performance
* 45.6.2 Partial Attribute Set (PAS) Hardening: Securing Replicated Attributes Across Forest Domain Boundaries
* 45.6.3 Restricting GC Exposure: Disabling Unnecessary GC Roles on Non-Essential Domain Controllers to Reduce Attack Surface

#### 45.7 Directory Service Permissions

* 45.7.1 Active Directory DACL Auditing: Enforcing Strict Access Control Lists Over `CN=System`, `CN=Configuration`, and Domain Root
* 45.7.2 Object Inheritance Control: Blocking Unintended DACL Inheritance Across Organizational Units (OUs)
* 45.7.3 Protecting System Containers: Restricting Modification Rights Over `Program Data`, `PKI Services`, and `GPO Policies`

#### 45.8 Virtualization Security

* 45.8.1 Virtualized DC (vDC) Security Risks: Mitigating Memory Dumps, Host-Level File Snapshot Access, and Unauthenticated Disk Mounting
* 45.8.2 Hypervisor Host Isolation: Shielding Hypervisor Hosts Managing Tier 0 vDCs Using Clean Source Principles
* 45.8.3 BitLocker Enclave Protection: Enforcing BitLocker Drive Encryption on Virtual Hard Disks (`.vhdx`) with TPM-Backed Keys

#### 45.9 VM-Generation ID

* 45.9.1 VM-Generation ID Mechanics: Hypervisor-Exposed Identifiers (`vmgenid`) for Detecting Snapshot Restores and VM Cloning
* 45.9.2 Active Directory Response Logic: Triggering Invocation ID Resets and RID Pool Invalidation Upon Snapshot Detection
* 45.9.3 Monitoring VMGenID Events: Auditing Event ID 2168, 2170, and 2172 Logs to Verify Hypervisor Safety Controls

#### 45.10 USN Rollback Prevention

* 45.10.1 Update Sequence Number (USN) Mechanics: Monotonic Counter Tracking Database Changes Across Replication Partners
* 45.10.2 Causes and Impact of USN Rollback: Database Divergence, Re-introduced Deleted Objects (Lingering Objects), and Replication Stoppage
* 45.10.3 Quarantine & Isolation Actions: Automatic Execution of Event ID 2095, Disabling Netlogon, and Quarantine Recovery Procedures

#### 45.11 Backup Protection

* 45.11.1 Active Directory Backup Mechanisms: System-State Backups, Volume Shadow Copy Service (VSS), and Bare-Metal Recovery Images
* 45.11.2 Immutable Backup Architecture: Cryptographically Locking Backups Against Ransomware Deletion or Alteration
* 45.11.3 Encryption of Backups: Utilizing AES-256 BitLocker or Application-Level Encryption for Offline System-State Files

#### 45.12 Recovery-System Isolation

* 45.12.1 Out-of-Band Isolated Recovery Environment (IRE): Establishing Air-Gapped Networks for Disaster Restoration
* 45.12.2 Clean-Room Jumpbox Deployment: Provisioning Uncompromised Administrative Workstations for Forest Recovery Operations
* 45.12.3 Automated Forest Recovery Playbooks: Validating Active Directory Forest Recovery (ADFR) Procedures Under Isolated Test Conditions

#### 45.13 Administrative Dependencies

* 45.13.1 Eliminating Downward Dependencies: Securing DNS, Hypervisors, Storage Arrays, and Backup Agents Managing Tier 0 Systems
* 45.13.2 Isolating Storage Networks: Protecting iSCSI and SAN Interfaces Connecting Domain Controller Virtual Hard Disks
* 45.13.3 Third-Party Agent Auditing: Stripping Unnecessary System-Level Management Agents from Domain Controller Operating Systems

### Capter 46 - Authenticationm and Network Access Hardening

#### 46.1 Kerberos Hardening

* 46.1.1 Disabling Weak Encryption Ciphers: Purging DES and RC4-HMAC Ciphers to Enforce AES-128 and AES-256 Bit Encryption Enterprise-Wide
* 46.1.2 Pre-Authentication Requirements: Auditing and Remediating Accounts Set with `Do not require Kerberos preauthentication` Flags
* 46.1.3 Ticket Lifetime & Renewal Controls: Restricting Maximum TGT and Service Ticket Validity Windows via KDC Group Policies

#### 46.2 Kerberos Armoring

* 46.2.1 Flexible Authentication Secure Tunneling (FAST): Enforcing RFC 6113 Armoring to Encapsulate `AS-REQ` Pre-Authentication Trajectories
* 46.2.2 Compound Authentication Mechanics: Binding User Authorization Contexts with Computer Account Cryptographic Keys
* 46.2.3 Armoring Deployment Strategies: Enforcing KDC and Client-Side Support for Kerberos Armoring Across Enterprise Domains

#### 46.3 NTLM Reduction

* 46.3.1 Auditing NTLM Footprints: Utilizing Event ID 8001/8004 Telemetry and Windows Server Enhanced Auditing Policies
* 46.3.2 Restricting Inbound and Outbound NTLM: Configuring `Restrict NTLM` Group Policies and Mapping Fallback Triggers
* 46.3.3 Executing NTLM Deprecation: Transitioning Environments to Local KDC, IAKerb, and Modern Kerberos-Only Endpoints

#### 46.4 LDAP Signing

* 46.4.1 Plaintext LDAP Risks: Identifying Credential Exposure and Session Hijacking Risks Across Unencrypted TCP 389 Queries
* 46.4.2 Enforcing LDAP Server Signing: Configuring Domain Controller Policies to Reject Unsigned SASL LDAP Binds
* 46.4.3 Client-Side LDAP Hardening: Requiring Signed LDAP Binds Across Member Servers, Workstations, and Third-Party Applications

#### 46.5 LDAP Channel Binding

* 46.5.1 Channel Binding Token (CBT) Mechanics: Binding Outer TLS Cryptographic Tunnels to Inner SASL Authentication Contexts
* 46.5.2 Domain Controller Enforcement Levels: Configuring `LdapEnforceChannelBinding` to Level 2 (Always Enforce)
* 46.5.3 Diagnosing Compatibility Issues: Correlating Event ID 2886, 2887, and 2889 Logs to Remediate Non-Compliant LDAP Clients

#### 46.6 SMB Signing

* 46.6.1 Message Integrity Protections: Defeating SMB Relay and Session Hijacking via Cryptographic Signatures
* 46.6.2 SMB Signing Enforcement: Requiring SMB Signing Across All Domain Controllers, Member Servers, and Workstations
* 46.6.3 Transitioning to SMB3 Encryption: Enforcing End-to-End SMB Encryption for High-Value Storage Shares and SYSVOL Data

#### 46.7 Extended Protection for Authentication

* 46.7.1 Service Binding & Channel Binding Tokens: Protecting Web and RPC Authentication Protocols Against Relay Attacks
* 46.7.2 EPA Implementation Across IIS and Web Services: Enforcing Hardened EPA Settings for AD CS, AD FS, and Enterprise Portals
* 46.7.3 Remediating Relay Vulnerabilities: Eliminating Credential Relay Exposure Points Across HTTP, RPC, and Enterprise Application Gateways

#### 46.8 Secure Channel Protection

* 46.8.1 Netlogon Secure Channel Hardening: Enforcing Strict RPC Secure Channel Sign and Seal Operations
* 46.8.2 Machine Account Password Rotation: Automating Computer Account Secret Updates and Purging Stale Machine Accounts
* 46.8.3 Blocking Vulnerable Channel Bindings: Monitoring Event ID 5829 and Enforcing Strict Netlogon Enforcement Mode

#### 46.9 LLMNR and NBT-NS Reduction

* 46.9.1 Multicast Name Resolution Exposure: Mitigating LLMNR/NBT-NS Poisoning and Poisoning-Based Credential Theft
* 46.9.2 Disabling LLMNR via Group Policy: Configuring `Turn off Link-Local Multicast Name Resolution` Policies Domain-Wide
* 46.9.3 Decommissioning NetBIOS over TCP/IP: Disabling NBT-NS Across Network Adapters and DHCP Scope Options

#### 46.10 WPAD Controls

* 46.10.1 Web Proxy Auto-Discovery Exploitation: Mitigating Rogue WPAD Server Spoofing and Unauthenticated Traffic Hijacking
* 46.10.2 Disabling Automatic Proxy Detection: Enforcing GPO and Registry Controls to Block WPAD Auto-Lookup Mechanisms
* 46.10.3 Restricting DNS WPAD Records: Configuring DNS Global Query Blocklists and Disabling Dynamic Registration for WPAD

#### 46.11 Secure DNS

* 46.11.1 DNS Security Extensions (DNSSEC): Cryptographically Signing DNS Zones to Prevent Cache Poisoning and Record Spoofing
* 46.11.2 Secure Dynamic Update Protections: Restricting Active Directory-Integrated Zone Updates to Authenticated Clients Only
* 46.11.3 DNS Transport Encryption: Implementing DNS over HTTPS (DoH) and DNS over TLS (DoT) for Enterprise Name Resolution

#### 46.12 RADIUS and NPS Hardening

* 46.12.1 Network Policy Server (NPS) Architecture: Securing Centralized RADIUS Infrastructure for Remote Access and 802.1X
* 46.12.2 Protecting RADIUS Shared Secrets: Deploying Complex Shared Secrets and Restricting RADIUS Client IP Enclaves
* 46.12.3 Hardening RADIUS Transport: Implementing RadSec (RADIUS over TLS) to Prevent Secret Sniffing Across Network Segments

#### 46.13 802.1X

* 46.13.1 Port-Based Network Access Control: Establishing Hardware-Enforced Layer 2 Network Perimeter Controls
* 46.13.2 Infrastructure Integration: Configuring Enterprise Switches, Wireless Access Points, and NPS Access Policies
* 46.13.3 Dynamic Access Assignment: Routing Devices to Quarantined or Restricted Network Segments Based on Health State

#### 46.14 EAP-TLS

* 46.14.1 High-Assurance EAP-TLS 1.3 Deployment: Utilizing RFC 9190 Standards for Mutual Certificate-Based Authentication
* 46.14.2 Certificate Validation Controls: Enforcing SAN/UPN Mappings, Extended Key Usages (EKUs), and Strict Revocation Checking (CRL/OCSP)
* 46.14.3 TPM-Backed Certificate Enrollment: Issuing Keys Secured by Hardware Trusted Platform Modules via Auto-Enrollment

#### 46.15 Legacy EAP Reduction

* 46.15.1 Weak EAP Protocol Risks: Deprecating Vulnerable Protocols (EAP-MD5, LEAP, EAP-FAST, and PEAP-MSCHAPv2)
* 46.15.2 Mitigating Password Exposure: Eliminating Challenge-Response Protocols Subject to Offline Dictionary Attacks
* 46.15.3 Migrating to Pure Certificate Authentication: Transitioning Enterprise Wireless and Wired Networks Exclusively to EAP-TLS

#### 46.16 VPN and Remote Access Authentication

* 46.16.1 Securing Remote Access Gateways: Integrating Multi-Factor Authentication (MFA) and Device Health Attestation
* 46.16.2 Always On VPN & Zero Trust Architecture: Deploying Machine and User Certificate Binds with Device Tunneling
* 46.16.3 Conditional Access Integration: Enforcing Location, Device Compliance, and Risk-Based Controls for Remote Connections

#### 46.17 Coercion and Relay Resistance

* 46.17.1 Protocol Coercion Vectors: Neutralizing Unauthenticated RPC Call Coercion (PetitPotam, ShadowCoerce, DFSCoerce)
* 46.17.2 Cross-Protocol Relay Defense Strategy: Binding Authentication to Transport Protection Across All Protocol Boundaries
* 46.17.3 Comprehensive System Hardening: Enforcing RPC Packet Privacy, Disabling Unused Services, and Auditing Relay Telemetry

### Chapter 47 - Policy, Trust, and Domain Post-Migration Hardening

#### 47.1 GPO Delegation

* 47.1.1 Restricting Group Policy Creation & Modification: Restricting `Group Policy Creator Owners` Group Memberships and Delegated Edit Rights
* 47.1.2 Auditing GPO Access Control Lists: Identifying Insecure `WriteDACL`, `WriteProperty`, or `GenericAll` Permissions Over GPO Objects
* 47.1.3 Enforcing Least Privilege Delegation: Assigning Role-Based Access Controls for OU-Level Policy Linking and Management

#### 47.2 GPO Change Control

* 47.2.1 Advanced Group Policy Management (AGPM): Deploying AGPM for Version Control, Check-in/Check-out Workflows, and Approval Pipelines
* 47.2.2 Policy Rollback and Auditing: Maintaining GPO Revision History and Automating Rollback Configurations Upon Unauthorized Changes
* 47.2.3 Monitoring Policy Modifications: Correlating Event ID 5136 and AGPM Audit Logs to Track GPO Attribute and Policy State Alterations

#### 47.3 SYSVOL Permissions

* 47.3.1 SYSVOL ACL Security Baselines: Securing Default NTFS and Share Permissions Over `\\<Domain>\SYSVOL`
* 47.3.2 Restricting Write Access: Blocking Non-Administrative Accounts from Modifying SYSVOL Scripts, Executables, and Policy Templates
* 47.3.3 Auditing SYSVOL Integrity: Deploying File Integrity Monitoring (FIM) and Auditing Event ID 4663 to Detect SYSVOL File Modifications

#### 47.4 Script Integrity

* 47.4.1 Cryptographic Script Signing: Enforcing Digital Signatures Over PowerShell, VBScript, and Batch Startup/Logon Scripts
* 47.4.2 Execution Policy Enforcement: Configuring `AllSigned` or `RemoteSigned` Execution Policies via Group Policy
* 47.4.3 Application Control in SYSVOL: Applying WDAC / AppLocker Rules to Prevent Unapproved Script Execution from SYSVOL Paths

#### 47.5 DFSR Health

* 47.5.1 Distributed File System Replication Mechanics: Managing Multi-DC SYSVOL Synchronization and Replication Topologies
* 47.5.2 DFSR Health Monitoring: Detecting Replication Stoppages, Backlogs, and Database Corruption via `dfsrdiag` and PowerShell
* 47.5.3 Remediating SYSVOL Desynchronization: Executing Authoritative (`D4`) and Non-Authoritative (`D2`) SYSVOL Restores safely

#### 47.6 Security Filtering

* 47.6.1 Security Filtering Mechanics: Utilizing Read and Apply Group Policy ACLs to Scope GPO Application
* 47.6.2 Enforcing Authenticated Users Read Rights: Maintaining `Authenticated Users` Read Access (MS16-072) to Prevent GPO Processing Failures
* 47.6.3 Security Group Architecture: Structuring Targeted Security Groups to Preempt Policy Overreach Across Enclaves

#### 47.7 WMI Filtering

* 47.7.1 WMI Filter Architecture: Evaluating Query Performance and Targeting Logic for OS, Hardware, and Registry Criteria
* 47.7.2 Mitigating Performance Impact: Preventing Logon Delays and CPU Spikes Caused by Inefficient WMI Query Constructs
* 47.7.3 WMI Filter Security: Auditing DACLs on WMI Filter Containers (`CN=SOM,CN=WMIP,CN=System`) to Prevent Unauthorized Targeting

#### 47.8 Trust Minimization

* 47.8.1 Trust Architecture Review: Evaluating Forest, External, Realm, and Shortcut Trust Necessity Across Infrastructure Boundaries
* 47.8.2 Transitivity Controls: Restricting Unnecessary Non-Transitive vs. Transitive Trust Relationships
* 47.8.3 Enforcing One-Way Trust Topologies: Transitioning High-Assurance Enclaves to One-Way Incoming/Outgoing Trust Relationships

#### 47.9 Selective Authentication

* 47.9.1 Selective Authentication Mechanics: Restricting Inter-Forest Authentication to Explicitly Authorized Resource Accounts
* 47.9.2 Provisioning Allowed-to-Authenticate Rights: Granting `Allowed to Authenticate` Permissions Over Specific Target Computer Objects
* 47.9.3 Auditing Cross-Forest Logons: Tracking Event ID 4624 (Logon Type 3) and Selective Authentication Failures Across Trust Boundaries

#### 47.10 SID Filtering

* 47.10.1 SID Filtering Mechanics: Enforcing SID History Quarantine to Block Extra SIDs in Inter-Forest Kerberos Tickets
* 47.10.2 Enabling Forest Trust Quarantine: Configuring `netdom trust /quarantine:yes` to Neutralize Golden Ticket SID Injection Vectors
* 47.10.3 Identifying SID Filtering Exceptions: Auditing forest trust SID filtering rules for legitimate migration scenarios

#### 47.11 Name-Suffix Routing

* 47.11.1 Routing Table Governance: Managing User Principal Name (UPN) and Service Principal Name (SPN) Routing Across Forest Trusts
* 47.11.2 Disabling Untrusted Name Suffixes: Blocking Conflicting or Malicious Name Suffix Requests Across Inter-Forest Interfaces
* 47.11.3 Preventing Identity Spoofing: Restricting Routing Collisions and Spoofed Domain Names via Name-Suffix Routing Validation

#### 47.12 Foreign Security Principal Governance

* 47.12.1 Foreign Security Principal (FSP) Containers: Mechanics of `CN=ForeignSecurityPrincipals` in Cross-Domain Group Membership
* 47.12.2 Auditing Legacy FSP Objects: Identifying Orphaned FSPs Pointing to Decommissioned or Untrusted Domains
* 47.12.3 Purging Stale FSPs: Automating FSP Cleanup to Prevent Unintended Access Paths Across Merged Identity Topology

#### 47.13 SIDHistory Governance

* 47.13.1 Post-Migration `sIDHistory` Exposure: Mitigating Privilege Escalation Risks Caused by Residual Injected SIDs
* 47.13.2 Auditing `sIDHistory` Attributes: Scanning All User and Group Objects for Non-Standard SIDs via PowerShell
* 47.13.3 Purging Legacy SIDs: Executing Systematic `sIDHistory` Removal Operations Post-Migration Validation

#### 47.14 Migration Cleanup

* 47.14.1 Post-Migration Identity Decommissioning: Disabling and Deleting Source Domain Accounts and Trust Relationships
* 47.14.2 Active Directory Migration Tool (ADMT) Cleanup: Purging Migration Service Accounts, Database Logs, and Temporary Delegation Rules
* 47.14.3 Forest Decommissioning Protocols: Systematically Retiring Legacy Child Domains and Forest Trust Infrastructure

#### 47.15 Cross-Forest Segmentation

* 47.15.1 Zero Trust Cross-Forest Design: Treating Connected Forests as External, Untrusted Boundaries
* 47.15.2 Isolating Control Planes: Preventing Administrative Escalation Across Forest Boundaries via Hardened Authentication Policies
* 47.15.3 Continuous Trust Telemetry: Monitoring Event ID 4706, 4707, and Cross-Domain Authentication Anomaly Alerts

### Chapter 48 - PKI, Smart Card, and Passwordless Hardening

#### 48.1 CA Tiering

* 48.1.1 PKI Architecture Hierarchy: Structuring Offline Root CAs, Policy CAs, and Online Enterprise Subordinate Issuing CAs
* 48.1.2 Control Plane Classification: Isolating Issuing Certificate Authorities as Tier 0 Assets Within the Enterprise Access Model
* 48.1.3 Segregation of Duties: Restricting `CA Administrator`, `Certificate Manager`, and `Auditor` Roles to Dedicated Accounts

#### 48.2 Offline Root Protection

* 48.2.1 Physical & Air-Gapped Security: Securing Standalone Offline Root CAs in Vault Enclaves with Hardware Access Control
* 48.2.2 Key Generation & Storage: Utilizing Hardware Security Modules (HSMs) for Offline Root Master Private Key Pair Generation
* 48.2.3 Root CA Lifecycle Operations: Establishing Secure Protocols for Subordinate CA Certificate Signing and Root CRL Publishing

#### 48.3 Certificate Template Governance

* 48.3.1 Template DACL Security Baselines: Auditing `WriteDACL`, `WriteProperty`, and `Enroll` Permissions Across Certificate Templates
* 48.3.2 Neutralizing ESC Vulnerability Classes: Preventing Misconfigured Client Authentication Templates (ESC1, ESC2, ESC3, ESC4, ESC9)
* 48.3.3 Enterprise Template Auditing: Enforcing Manager Approval and Authorized Signature Requirements for Sensitive Templates

#### 48.4 Enrollment Security

* 48.4.1 Securing Enrollment Endpoints: Hardening Network Device Enrollment Service (NDES), CES, and CEP Services
* 48.4.2 EPA and NTLM Blocking on Enrollment Interfaces: Enforcing Extended Protection for Authentication and TLS on Web Enrollment (ESC8)
* 48.4.3 Restricted Auto-Enrollment Policies: Scope-Limiting Auto-Enrollment Group Policies via Strict Security Filtering

#### 48.5 Strong Certificate Mapping

* 48.5.1 Mechanics of KB5014754 Enforcement: Understanding Explicit Certificate Mapping Requirements on Windows Domain Controllers
* 48.5.2 Mapping Methods Comparison: Transitioning from Weak SAN/UPN Mappings to Strong `altSecurityIdentities` (X509IssuerSubject / SKI)
* 48.5.3 Remediating Mapping Bypasses: Auditing Event ID 39, 40, and 41 Telemetry to Eliminate Unmapped Authentications

#### 48.6 Private-Key Protection

* 48.6.1 Exportability Controls: Marking Private Keys as Non-Exportable and Enforcing Software Key Protection (CryptoAPI / CNG)
* 48.6.2 Key Archival & Recovery: Securing Key Recovery Agent (KRA) Certificates and DPAPI-Protected Archival Databases
* 48.6.3 Protecting Client Private Keys: Deploying TPM-Backed Key Storage Providers (KSPs) for Enterprise Workstations

#### 48.7 HSMs

* 48.7.1 Hardware Security Module Architecture: Deploying FIPS 140-2/3 Level 3 Network and PCIe HSMs for Enterprise CAs
* 48.7.2 PKCS#11 and CNG Provider Integration: Configuring Cryptographic Next Generation Providers for CA Master Key Protection
* 48.7.3 HSM Key Backup & High Availability: Managing Cryptographic Partition Backups and Multi-Node HSM Clustering

#### 48.8 Certificate Revocation

* 48.8.1 Revocation Vector Triggers: Standardizing Revocation Playbooks for Compromised Keys, Terminated Users, and Retired Assets
* 48.8.2 Executing Immediate Revocation: Utilizing `certutil` and AD CS Administrative Interfaces for Rapid Invalidations
* 48.8.3 Revocation Delta Management: Optimizing Delta CRL Publishing Intervals and Emergency Revocation Distribution

#### 48.9 CRL and OCSP Resilience

* 48.9.1 High-Availability CRL Distribution Points (CDP): Deploying Redundant HTTP CDPs for High-Throughput Revocation Checks
* 48.9.2 Online Certificate Status Protocol (OCSP) Responding: Configuring OCSP Array Responders with Dedicated Signing Certificates
* 48.9.3 Preventing Revocation Outages: Mitigating Authentication Failures Caused by Expired CRLs or Unreachable Revocation Points

#### 48.10 FPKI Trust

* 48.10.1 Federal PKI Architecture: Cross-Certificate Bridges, Federal Bridge CA (FBCA), and Trust Anchor Management
* 48.10.2 External CA Trust Ingestion: Securing Enterprise Trust Stores Against Unauthorized External Intermediate Certificates
* 48.10.3 Path Validation & Policy Constraints: Enforcing Explicit Policy Mappings, Inhibit Policy Mapping, and Require Explicit Policy Flags

#### 48.11 PIV/CAC Hardening

* 48.11.1 Personal Identity Verification (PIV) Standards: Aligning Enterprise Smart Card Deployments with FIPS 201 Guidelines
* 48.11.2 Enforcement of Smart Card Logon: Setting `Smart card is required for interactive logon` for All High-Privilege Accounts
* 48.11.3 PIN Policy & Middleware Security: Hardening PIV Middleware, PIN Retries, and Physical Smart Card Reader Interfaces

#### 48.12 PKINIT Hardening

* 48.12.1 Kerberos PKINIT Protocols: Public Key Cryptography for Initial Authentication in Active Directory
* 48.12.2 Enforcing PKINIT Freshness Extension: Implementing RFC 8636 Freshness Tokens to Prevent Replay Attacks
* 48.12.3 Armoring PKINIT Trajectories: Enforcing FAST (Flexible Authentication Secure Tunneling) for All PKINIT Authentications

#### 48.13 Windows Hello for Business

* 48.13.1 WHfB Architecture: TPM-Backed Asymmetric Key Pair Generation and Two-Factor Strong Authentication
* 48.13.2 Key Trust vs. Certificate Trust Deployments: Evaluating Infrastructure Requirements and Domain Controller Certificates
* 48.13.3 WHfB Lifecycle Governance: Automating Enrollment, PIN Reset Services, and Revocation Upon Account Deprovisioning

#### 48.14 FIDO2 and Passkeys

* 48.14.1 WebAuthn and FIDO2 Architecture: Deploying Passwordless FIDO2 Hardware Security Keys (AAL3 Assurance)
* 48.14.2 Passkey Enterprise Controls: Distinguishing Between Device-Bound Passkeys and Synced Passkeys in High-Assurance Enclaves
* 48.14.3 Restricting Authenticator AAGUIDs: Whitelisting Approved Hardware FIDO2 Authenticator Models via Conditional Access

#### 48.15 Cloud Kerberos Trust

* 48.15.1 Cloud Kerberos Trust Mechanics: Hybrid Passwordless Access to On-Premises Resources via Entra ID Issued Read-Only TGTs
* 48.15.2 Eliminating On-Premises PKI Dependencies: Deploying Cloud Kerberos Objects in Active Directory Without Certificate Infrastructure
* 48.15.3 Hybrid Access Control: Securing On-Premises Active Directory Resources Accessed via Passwordless Cloud Authenticators

#### 48.16 Cryptographic Agility

* 48.16.1 Auditing Enterprise Cryptographic Suites: Inventorying RSA, ECC, Hash Functions, and Cipher Suites Across PKI Templates
* 48.16.2 Modernizing Cryptographic Providers: Migrating Legacy CryptoAPI (CAPI) Architecture to Cryptographic Next Generation (CNG)
* 48.16.3 Phasing Out Deprecated Algorithms: Deprecating SHA-1, RSA 1024/2048, and Weak ECC Curves Enterprise-Wide

#### 48.17 Post-Quantum Readiness

* 48.17.1 Post-Quantum Cryptography (PQC) Standards: Preparing for NIST PQC Algorithms (ML-KEM / FIPS 203, ML-DSA / FIPS 204)
* 48.17.2 Hybrid Cryptographic Certificates: Planning Dual-Key Classical/PQC Certificate Templates for AD CS Infrastructure
* 48.17.3 Quantum-Resistant Identity Roadmap: Transitioning Tier 0 Identity Infrastructure to PQC-Compliant Protocols

### Chapter 49 - Federation, Entra ID, and Hybrid Hardening

#### 49.1 AD FS Isolation

* 49.1.1 AD FS Tier 0 Enclave Classification: Isolating AD FS Servers and Web Application Proxies (WAP) within Tier 0 Control Planes
* 49.1.2 Web Application Proxy (WAP) Perimeter Hardening: Deploying WAPs in DMZ Segments to Prevent Direct External RPC/HTTPS Exposure to AD FS
* 49.1.3 Restricting Administrative Access: Enforcing Clean Source Principles and Blocking Non-Essential Inbound Ports (e.g., SMB, WinRM) to Federation Hosts

#### 49.2 Token-Signing Key Protection

* 49.2.1 Mitigating Golden SAML Attacks: Securing Private Token-Signing Keys Against Extraction and Unauthorized Certificate Generation
* 49.2.2 Hardware Security Module (HSM) Binding: Storing AD FS Token-Signing and Token-Decrypting Certificates in FIPS 140-2 Level 3 HSMs
* 49.2.3 Automating Certificate Auto-Rollover: Configuring Secure Key Rotation Cycles and Monitoring Event ID 335 Log Telemetry

#### 49.3 Claims Governance

* 49.3.1 Claims Xpath & Transformation Rules: Enforcing Custom Claims Issuance Rules to Filter Authorization Contexts
* 49.3.2 Restricting External Claims Trajectories: Blocking Untrusted SAML Attributes and Strip Unsanitized Active Directory Group SIDs
* 49.3.3 Issuance Authorization Policies: Configuring Device-Aware and Network-Aware Authorization Rules at the Federation Layer

#### 49.4 Relying-Party Governance

* 49.4.1 Auditing Relying Party Trusts (RPTs): Inventorying Active SAML 2.0 and WS-Federation Integrations Across Cloud and On-Premises
* 49.4.2 Enforcing Encrypted SAML Assertions: Requiring Encrypted Tokens for High-Assurance Third-Party Applications
* 49.4.3 Decommissioning Legacy Trusts: Removing Unused, Unmonitored, or Non-Compliant Relying Party Relationships

#### 49.5 Audience Restrictions

* 49.5.1 SAML Audience Restriction Verification: Enforcing Strict URI Matching to Prevent Assertion Replay Attacks Across Applications
* 49.5.2 Restricting Multi-Tenant Token Scope: Validating Target Resource Identifiers (`aud` claim) Within Web Applications
* 49.5.3 Detecting Token Misdirection: Monitoring Authentication Logs for Mismatched Audience Claims and Cross-App Replay Vectors

#### 49.6 Federation Trust Management

* 49.6.1 Federated vs. Managed Authentication: Evaluating Migration Paths from AD FS to Password Hash Sync (PHS) or Pass-Through Authentication (PTA)
* 49.6.2 Securing Immutable ID (`mS-DS-ConsistencyGuid`): Preventing Source Anchor Manipulation and User Account Hijacking
* 49.6.3 Federation Metadata Integrity: Enforcing HTTPS and Cryptographic Signature Verification for Automated Metadata Updates

#### 49.7 Entra Connect Security

* 49.7.1 Entra Connect Host Hardening: Classifying Synchronization Servers as Tier 0 Assets and Restricting Local Administrative Rights
* 49.7.2 Enforcing Server Build Hardening: Upgrading Entra Connect Sync Servers to Hardened Builds (v2.5.79.0+) or Transitioning to Cloud Sync
* 49.7.3 Staging Mode Deployment Architecture: Utilizing Isolated Staging Servers for High Availability, Audit Logs, and Safe Configuration Testing

#### 49.8 Synchronization Account Protection

* 49.8.1 On-Premises AD DS Connector Account: Restricting Privileges of the `MSOL_` Account (Limiting Password Hash Sync Rights)
* 49.8.2 Directory Synchronization Accounts in Entra ID: Auditing `Sync_*` Cloud Service Principals and Enforcing MFA/Conditional Access Exemptions
* 49.8.3 Mitigating Sync-Based Elevation Attacks: Monitoring for Unauthorized Writes Over Sensitive On-Premises Attributes (e.g., `sIDHistory`, `adminCount`)

#### 49.9 Conditional Access

* 49.9.1 Zero Trust Conditional Access Architecture: Designing Strict Access Policies Based on User, Device, Location, and Real-Time Risk
* 49.9.2 Requiring Compliant & Managed Devices: Enforcing Hybrid Entra Joined or Intune Compliant Device Checks for Sensitive Applications
* 49.9.3 Blocking Legacy Authentication: Creating Blanket Denial Rules for Basic Auth Protocols (POP3, IMAP4, SMTP) Lacking MFA Support

#### 49.10 Privileged Role Governance

* 49.10.1 Entra ID Privileged Identity Management (PIM): Enforcing Just-In-Time (JIT) Activation and Approval Workflows for Tier 0 Cloud Roles
* 49.10.2 Global Administrator Minimization: Restricting Standing Global Admin Roles to Fewer Than 5 Break-Glass Accounts
* 49.10.3 Access Reviews for Cloud Admins: Automating Recertification Cycles for High-Privilege Roles (`Privileged Role Administrator`, `Authentication Admin`)

#### 49.11 Service Principals

* 49.11.1 Service Principal Inventory & Auditing: Cataloging Enterprise Application Registrations and Secret Expiration Lifecycles
* 49.11.2 Eliminating Password Credentials: Replacing Plaintext Client Secrets with X.509 Certificates or Federated Identity Credentials (OIDC)
* 49.11.3 Least Privilege API Permissions: Restricting High-Risk Application Permissions (`Directory.ReadWrite.All`, `RoleManagement.ReadWrite.Directory`)

#### 49.12 Workload Identities

* 49.12.1 Entra Workload ID Governance: Deploying Workload Identity Premium Controls to Monitor Non-Human Access Trends
* 49.12.2 Managed Identities Deployment: Utilizing User-Assigned and System-Assigned Managed Identities for Azure Workloads to Eliminate Keys
* 49.12.3 Conditional Access for Workload Identities: Enforcing Location and Risk-Based Restrictions directly on Service Principals

#### 49.13 Application Consent

* 49.13.1 Neutralizing Consent Grant Attacks: Disabling User Consent for Unverified Third-Party OAuth Applications
* 49.13.2 Admin Consent Workflows: Establishing Automated Request and Security Review Pipelines for Multi-Tenant App Onboarding
* 49.13.3 Publisher Verification Controls: Requiring MPN-Verified Publisher Status for Applications Requested Within the Tenant

#### 49.14 Cross-Tenant Access

* 49.14.1 Cross-Tenant Access Settings: Managing Inbound and Outbound B2B Collaboration Settings in Entra External ID
* 49.14.2 Trusting External MFA & Device Claims: Selectively Trusting MFA, Compliant Device, and Hybrid Joined Claims from Trusted Partner Tenants
* 49.14.3 Restricting B2B Direct Connect: Configuring Cross-Tenant Boundaries for Teams Shared Channels and Extranet Resources

#### 49.15 External Collaboration

* 49.15.1 Guest User Access Restrictions: Setting Restrictive Options for External Guest Enumeration of Tenant Users and Groups
* 49.15.2 One-Time Passcode (OTP) Authentication: Standardizing Guest User Authentication Protocols via Email OTP or Federated IdPs
* 49.15.3 Automated Guest Lifecycle Purging: Implementing Entra ID Governance Access Reviews to Automatically Deprovision Inactive Guest Accounts

#### 49.16 Token Revocation

* 49.16.1 Emergency Session Revocation: Executing Immediate Refresh Token Invalidation via `Revoke-MgUserSignInSession` and Graph API
* 49.16.2 Emergency Access (Break-Glass) Playbooks: Bypassing Standard MFA Pipelines During Outages via Hardened, Un-Federated Cloud Accounts
* 49.16.3 Token Lifetime Policies: Restricting Refresh Token Validity and Enforcing Short-Lived Access Tokens for Privileged Roles

#### 49.17 Continuous Access Evaluation

* 49.17.1 Continuous Access Evaluation (CAE) Architecture: Enabling Real-Time Claims Evaluation via RFC 8693 / Security Events 1.0 Protocols
* 49.17.2 Real-Time Event Triggers: Enforcing Automated Token Rejection Upon Account Disabling, Password Resets, or Elevated User Risk State
* 49.17.3 CAE for Workload Identities: Deploying Real-Time IP Location and Threat Revocation Across API Interactions for Service Principals

### Chapter 50 - Identity Governance and Authoritative Attributes

#### 50.1 Identity Governance and Administration

* 50.1.1 IGA Architecture & FICAM Integration: Aligning Centralized IGA Engines with Enterprise Directory Controls and NIST SP 800-53 (AC-2)
* 50.1.2 Unified Identity Warehousing: Aggregating Accounts, Groups, and Entitlements Across On-Premises AD, Entra ID, and SaaS Endpoints
* 50.1.3 Compliance & Audit Telemetry: Automating Continuous Policy Compliance Reporting and Evidentiary Collection for Audit Frameworks

#### 50.2 Authoritative Identity Sources

* 50.2.1 Primary System of Record (SoR) Binding: Integrating Enterprise HR Systems (e.g., Workday, SAP) as Immutable Identity Sources
* 50.2.2 Multi-SoR Priority Resolution: Structuring Precedence Rules when Ingesting Attributes from Overlapping HR and Vendor Databases
* 50.2.3 Source Ingestion Hardening: Securing HR-to-IGA Connectors Against Unauthenticated Payload Injection and Man-in-the-Middle Manipulation

#### 50.3 Attribute Provenance

* 50.3.1 Cryptographic Attribute Lineage: Verifying System-of-Origin Signing for Sensitive Attributes (`department`, `clearance`, `mail`)
* 50.3.2 System-of-Origin Tracking: Maintaining Detailed Audit Logs of System Writes to Identify Out-of-Band Directory Modification
* 50.3.3 Detecting Attribute Mutation Anomalies: Triggering Real-Time Security Alerts When Authoritative Attributes Change Outside Standard IGA Channels

#### 50.4 Attribute Integrity

* 50.4.1 Schema Normalization & Validation: Enforcing Strict Regex Validation, Case-Formatting, and Character Encoding on Ingested Data
* 50.4.2 Immutable Identifier Mapping: Assigning Non-Reusable Unique Identifiers (GUIDs/UUIDs) to Prevent Identity Collision and Re-use
* 50.4.3 Preventing Attribute Poisoning & Injection: Filtering Malicious LDAP Injection Characters and Scripting Payloads from HR Input Fields

#### 50.5 Provisioning and SCIM

* 50.5.1 SCIM v2.0 Protocol Implementation: Deploying Standardized RESTful JSON SCIM APIs (RFC 7643/7644) for Cross-Domain Synchronization
* 50.5.2 Automated Event-Driven Provisioning Pipelines: Executing Real-Time Account Creation and Attribute Propagation Upon HR Trigger
* 50.5.3 Securing SCIM API Gateways: Enforcing OAuth 2.0 Bearer Tokens, Mutual TLS (mTLS), and IP Whitelisting on SCIM Interfaces

#### 50.6 Entitlement Governance

* 50.6.1 Entitlement Catalog Architecture: Structuring Standardized Catalogs of Active Directory Groups, Application Roles, and Direct Permissions
* 50.6.2 Birthright Entitlement Baselines: Establishing Minimal Core Entitlement Sets Derived Automatically from Department and Job Function
* 50.6.3 Out-of-Band Entitlement Remediation: Automatically Detecting and Stripping Unmanaged Privileges Directly Assigned via Directory DACLs

#### 50.7 Role Engineering

* 50.7.1 Role-Based Access Control (RBAC) Mining: Analyzing Historical Group Memberships to Build Optimally Scoped Business Roles
* 50.7.2 Attribute-Based Access Control (ABAC) Integration: Dynamically Evaluating User and Environmental Attributes for Real-Time Access Decisions
* 50.7.3 Preventing Role Explosion: Implementing Role Hierarchy Limits and Periodic Consolidation Reviews to Eliminate Over-Customized Roles

#### 50.8 Segregation of Duties

* 50.8.1 Toxic Combination Matrix Design: Defining Explicit Conflicts Between Sensitive Business Functions and Privileged Roles (NIST SP 800-53 AC-5)
* 50.8.2 Preventive vs. Detective SoD Enforcement: Blocking Conflicting Entitlement Requests at Request Time vs. Scanning for Violations
* 50.8.3 Cross-Control Plane SoD Governance: Correlating On-Premises Administrative Rights with Cloud/SaaS High-Privilege Roles

#### 50.9 Access Certification

* 50.9.1 High-Assurance Certification Campaign Design: Establishing Scheduled and Targeted Access Review Cycles for Sensitive Enclaves
* 50.9.2 Manager vs. Resource Owner Attestation: Routing Certification Tasks to Direct Line Managers and Specific System/Data Owners
* 50.9.3 Mitigating Fatigue via Risk-Weighted Certification: Prioritizing Review Actions Based on Entitlement Risk Scores and Usage Analytics

#### 50.10 Recertification

* 50.10.1 Event-Driven Micro-Recertifications: Triggering Immediate Attestation Actions Upon User Transfer, Promotion, or Role Change
* 50.10.2 Privileged Role & Entitlement Recertification: Enforcing Shortened Review Cycles (e.g., Monthly/Quarterly) for Tier 0 and Tier 1 Access
* 50.10.3 Automated Revocation Mechanics Upon Attestation Failure: Deprovisioning Uncertified Entitlements Instantly When Reviews Time Out or Reject

#### 50.11 Sponsorship

* 50.11.1 Identity Sponsorship Frameworks: Mandating Active Full-Time Employee Custodians for All Contingent or Temporary Accounts
* 50.11.2 Custodial Responsibility Binding: Requiring Sponsors to Formally Verify Identity Validity, Scope of Access, and Business Justification
* 50.11.3 Sponsor Offboarding and Re-Sponsorship Protocols: Re-assigning or Disabling Sponsored Accounts Instantly When a Sponsor Departs

#### 50.12 Contractor Identity Governance

* 50.12.1 Third-Party Lifecycle Management: Managing Vendor, Partner, and Consultant Identities Separately from Core Employee Databases
* 50.12.2 Hard Expiration & Time-Bound Access Enforcement: Setting Mandatory Fixed Account Expiration Dates Not Exceeding 180 Days
* 50.12.3 Contractor Reproofing & Access Scope Isolation: Enforcing Remote Identity Re-Verification (NIST SP 800-63A IAL2) and Segmented Enclave Access

#### 50.13 Non-Person Identity Governance

* 50.13.1 Service & Workload Identity Attestation: Cataloging Service Accounts, API Keys, and Managed Identities Under Governed Lifecycles
* 50.13.2 Custodian Binding for NPI Objects: Enforcing Human Ownership and Accountability over Every Service Principal and Service Account
* 50.13.3 Automated NPI Deprovisioning Lifecycle: Decommissioning Unlinked, Unused, or Un-certified Non-Person Identities Automatically

#### 50.14 Deprovisioning

* 50.14.1 Rapid Deprovisioning Playbooks: Executing Immediate Multi-Stage Account Disabling Upon HR Termination Signal
* 50.14.2 Active Session Termination & Revocation: Revoking Kerberos Tickets, OAuth Tokens, and Active Web Sessions Instantly Enterprise-Wide
* 50.14.3 Post-Deprovisioning Residual Access Auditing: Verification Systems Confirming Full Removal Across Secondary Systems and On-Premises Shares

#### 50.15 Governance-to-Technical-Control Traceability

* 50.15.1 Mapping Policy to Directory DACLs and Scopes: Linking High-Level IGA Policies Directly to Active Directory ACLs, OUs, and Entra Roles
* 50.15.2 Automated Policy Compliance Verification: Continuous Scanning to Confirm On-Ground Directory State Matches Governed State
* 50.15.3 Continuous Telemetry and Audit Readiness: Maintaining Immutable Audit Trails Proving Complete Lineage from Policy Grant to Enforcement

#### 51.1 Identity Security Posture Assessment

* 51.1.1 Continuous Posture Assessment Architecture: Establishing Automated Frameworks to Audit Directory Configurations and Control Plane Integrity
* 51.1.2 Evaluating Configuration Drift: Tracking Unsanitized Object Changes, Stray Group Memberships, and Delegated Access Creep Over Time
* 51.1.3 Aligning Posture Metrics with Federal Baselines: Mapping Directory Telemetry to NIST SP 800-53, DISA STIGs, and CIS Benchmarks

#### 51.2 Attack-Path Exposure

* 51.2.1 Mechanics of Identity Attack Paths: Analyzing How Chained Misconfigurations (DACLs, SPNs, Session Leaks, Weak Passwords) Lead to Domain Compromise
* 51.2.2 Identity Blast Radius Modeling: Quantifying the Impact and Lateral Movement Reach of Compromised Non-Privileged Accounts
* 51.2.3 Graph-Based Structural Analysis: Utilizing Directed Graph Models to Map Hidden Access Choke Points and Transit Vectors Across Enclaves

#### 51.3 BloodHound for Defensive Analysis

* 51.3.1 BloodHound Infrastructure & Data Collection: Deploying SharpHound and AzureHound Data Collectors Safely in Production Systems
* 51.3.2 Querying High-Risk Graph Edges: Writing Cypher Queries to Identify `GenericAll`, `WriteDACL`, `ForceChangePassword`, and `AddMembers` Escalation Vectors
* 51.3.3 Enterprise Graph Analytics: Utilizing BloodHound Enterprise (BHE) for Continuous Tier 0 Exposure Tracking and Choke-Point Identification

#### 51.4 PingCastle

* 51.4.1 Health Check Engine Deployment: Executing Risk-Based Auditing of Domain Controllers, Trusts, Anomalies, and Stale Objects
* 51.4.2 PingCastle Score Modeling: Interpreting Risk Indicators Across Privileged Accounts, Forest Trusts, Stale Objects, and Protocol Security
* 51.4.3 Automating Posture Reporting: Integrating PingCastle Scans into Scheduled Pipeline Audits for Enterprise Risk Monitoring

#### 51.5 Purple Knight

* 51.5.1 Rapid Posture Assessment: Executing Community/Enterprise Scans to Detect Active Directory and Entra ID Security Gaps
* 51.5.2 Evaluating Indicators of Exposure (IoEs): Scrutinizing Findings Across Kerberos Configuration, PKI Templates, Group Policy, and Hybrid Sync
* 51.5.3 Prioritizing Technical Findings: Categorizing Remediation Tasks Based on Exploitation Likelihood and Severity Scores

#### 51.6 Effective Control Analysis

* 51.6.1 Paper Controls vs. Effective Controls: Validating Whether Documented Security Policies Are Cryptographically and Technical Enforced
* 51.6.2 DACL & ACE Evaluation: Calculating Effective Permissions Over Sensitive Directory Objects Considering Group Inheritance and Token Claims
* 51.6.3 Security Policy Audit Mechanics: Testing Local Security Authority (LSA) Policies and Group Policy Enforcement Across Member Endpoints

#### 51.7 Tier 0 Reachability

* 51.7.1 Defining Control Plane Boundaries: Classifying Domain Controllers, AD CS, AD FS, Entra Connect, and Hypervisors as Tier 0
* 51.7.2 Shortest-Path Tier 0 Transit Calculations: Executing Graph Algorithms to Measure the Minimum Hop Count from Any Compromised Account to Tier 0
* 51.7.3 Isolating Indirect Escalation Vectors: Identifying Shadow Admins and Non-Standard Permission Chains Leading to Control Plane Privilege

#### 51.8 Exposure Prioritization

* 51.8.1 Contextual Risk Scoring: Prioritizing Remediations Based on Path Transience, Asset Criticality, and Exposure to Internet Enclaves
* 51.8.2 High-Impact Choke Point Identification: Target Remediation Efforts on Single DACL or Policy Changes That Sever Hundreds of Potential Attack Paths
* 51.8.3 Cost-Benefit Analysis in Remediation: Balancing Threat Reduction Against Operational Impact and Business Interruption Risks

#### 51.9 Continuous Attack-Path Reduction

* 51.9.1 Automated Choke-Point Remediation: Deploying Scripted DACL Cleansing and Tiering Enforcements to Break Graph Chains
* 51.9.2 Continuous Graph Analytics Integration: Incorporating Real-Time BloodHound Graph Updates into Security Operations Center (SOC) Operations
* 51.9.3 Preventing Attack Path Re-Emergence: Enforcing GPO and IGA Governance Baseline Rules to Block Misconfiguration Resurgence

#### 51.10 Adversary Emulation

* 51.10.1 MITRE ATT\&CK Mapping for Identity: Designing Emulation Plans Scoped to Identity Tactics (T1003, T1558, T1098, T1484)
* 51.10.2 Executing Safe Offensive TTPs: Conducting Controlled Kerberoasting, AS-REP Roasting, DCSync, and ESC1 Exploitation Exercises
* 51.10.3 Threat Actor Playbook Reenactment: Simulating Known Threat Actor Methodologies (e.g., Solorigate, SCATTERED SPIDER) Against Hybrid Controls

#### 51.11 Breach and Attack Simulation

* 51.11.1 Automated BAS Platform Integration: Deploying Continuous Simulation Engines to Validate Network and Identity Boundary Defenses
* 51.11.2 Safe Payload Execution in Enclaves: Executing Synthetic Telemetry and Non-Destructive Exploitation Simulations in Live Production Scenarios
* 51.11.3 Measuring Telemetry Drift: Tracking Gaps Between Simulated Adversary Execution and Detection Generation in SIEM/EDR

#### 51.12 Purple-Team Validation

* 51.12.1 Purple-Team Exercise Frameworks: Aligning Offensive Execution (Red) with Defensive Telemetry Analysis (Blue) in Real-Time
* 51.12.2 Interactive Attack-Detection Cycles: Step-by-Step Step Execution of Identity Attack Vectors to Observe Live SIEM/EDR Event Generation
* 51.12.3 Cross-Functional Playbook Optimization: Refining Incident Response Runbooks Based on Real-Time Collaboration Between Red and Blue Teams

#### 51.13 Detection Validation

* 51.13.1 Auditing Detection Coverage: Mapping Event Logs (4624, 4662, 4768, 4769, 4776) Against SIEM Correlation Rules
* 51.13.2 Eliminating Blind Spots: Identifying Siloed Telemetry Sources Across Domain Controllers, Network Firewalls, and Cloud Identity Logs
* 51.13.3 Tuning Detection Precision: Minimizing False Positive Rates While Ensuring Zero Missed Alerts for High-Consequence Attacks (e.g., DCSync)

#### 51.14 Remediation Testing

* 51.14.1 Closed-Loop Remediation Workflows: Verifying That Technical Fixes Effectively Sever Intended Attack Paths Without Breaking Applications
* 51.14.2 Regression Testing Infrastructure: Executing Automated Health and Functional Audits Post-Remediation Application
* 51.14.3 DACL / Policy Rollback Safety: Establishing Reversion Protocols to Rapidly Restore Operational Baselines If Services Malfunction

#### 51.15 Demonstrating Attack-Path Closure

* 51.15.1 Quantitative Exposure Metrics: Tracking Tier 0 Exposure Indexes and Shortest-Path Transits Over Time
* 51.15.2 Executive and Board Reporting: Translating Complex Graph Analytics and Cyber Hygiene Scores into Executive-Level Risk Trends
* 51.15.3 Proving FICAM & Compliance Alignment: Producing Evidentiary Reporting Demonstrating Compliance with NIST SP 800-53 and CISA Zero Trust Baselines

#### 52.1 Identity Logging Strategy

* 52.1.1 Enterprise Audit Strategy Design: Defining Telemetry Scopes Across Tier 0 Assets, Member Servers, and Cloud Identity Workloads
* 52.1.2 Balancing Storage vs. Visibility: Sizing Local Log Buffers, Forwarding Bandwidth, and SIEM Ingestion Volumes Across Active Directory Enclaves
* 52.1.3 Regulatory Alignment: Mapping Audit Baselines to NIST SP 800-53 Rev. 5, DoD Security Technical Implementation Guides (STIGs), and CISA Guidelines

#### 52.2 Advanced Audit Policy

* 52.2.1 AAPC vs. Legacy Audit Policy: Enforcing Advanced Audit Policy Configuration (AAPC) to Eliminate Legacy Category Overwrites
* 52.2.2 Core AAPC Subcategory Baselines: Enabling High-Fidelity Subcategories Including _Directory Service Changes_, _Account Management_, and _Logon/Logoff_
* 52.2.3 Enforcing Policy Uniformity: Deploying AAPC Settings via Group Policy Objects (`GPO -> Advanced Audit Policy Configuration`) and Auditing via `auditpol.exe`

#### 52.3 SACL Strategy

* 52.3.1 Directory SACL Architecture: Defining Target Object SACLs to Generate Event ID 4662 (Operation Performed on Object) for High-Risk Actions
* 52.3.2 Scoping Attribute-Level SACLs: Applying Focused Auditing Over Critical Attributes (`servicePrincipalName`, `msDS-AllowedToDelegateTo`, `member`)
* 52.3.3 Mitigating SACL Performance Impact: Balancing SACL Granularity Against Domain Controller LSA and CPU Overhead

#### 52.4 Authentication Events

* 52.4.1 Kerberos Authentication Telemetry: Capturing TGT Requests (Event ID 4768), Service Ticket Requests (4769), and Renewal Events
* 52.4.2 Interactive & Network Logons: Analyzing Successful Logons (4624) and Failed Logons (4625) Across Logon Types (Type 2 Interactive, Type 3 Network, Type 10 RDP)
* 52.4.3 NTLM Authentication Monitoring: Tracking Event ID 8001–8004 Telemetry to Identify Fallback NTLM Authentications and Relay Attempts

#### 52.5 Authorization Events

* 52.5.1 Explicit Credential Usage: Monitoring Event ID 4648 (Logon with Explicit Credentials) to Detect Runas and Pass-the-Hash Executions
* 52.5.2 Privilege Assignment & Elevation: Tracking Special Privileges (Event ID 4672) Assigned to New Logons (e.g., `SeDebugPrivilege`, `SeEnableDelegationPrivilege`)
* 52.5.3 Kerberos Pre-Authentication & Ticket Anomaly Detection: Detecting AS-REP Roasting (Event ID 4768 with Pre-Auth Disabled) and Failed Kerberos Pre-Auth (4771)

#### 52.6 Directory Change Auditing

* 52.6.1 Object Creation & Deletion: Correlating Event ID 5137 (Directory Object Created) and 5141 (Directory Object Deleted)
* 52.6.2 Attribute Modification Tracking: Analyzing Event ID 5136 (Directory Service Object Modified) to Capture Old vs. New Attribute Values
* 52.6.3 DACL Modification Auditing: Detecting Permission Tampering Over OUs, Containers, and High-Value Administrative Accounts

#### 52.7 Group and Privilege Changes

* 52.7.1 Security Group Governance Logs: Monitoring Member Additions/Removals in Privileged Groups via Event IDs 4728, 4732, and 4756
* 52.7.2 AdminCount & SDProp Tracking: Auditing Background Propagations of Security Descriptors Over Protected Accounts
* 52.7.3 Account Status Alterations: Tracking Account Disabling (4725), Unlocking (4767), and Password Reset (4724) Actions

#### 52.8 GPO Changes

* 52.8.1 Group Policy Object Modification: Tracking Event ID 5136 Over `CN=Policies,CN=System` Containers and GPC Attributes
* 52.8.2 SYSVOL File Modifications: Correlating Directory Service Logs with File Integrity Monitoring (FIM) and VSS Shadow Copy Telemetry
* 52.8.3 Link and Enforcement Alterations: Auditing GPO Link Changes (Event ID 4932/4933) Over High-Assurance Enclave OUs

#### 52.9 Replication Telemetry

* 52.9.1 Directory Replication Service (DRS) Logs: Monitoring Inbound Replication Events and `DsGetNcChanges` API Calls
* 52.9.2 Detecting DCSync Attacks: Correlating Event ID 4662 (Directory Object Access with DRS Replication Guids) From Non-DC IP Addresses
* 52.9.3 Tracking Replication Errors: Monitoring Event IDs 2095 and 1388 to Detect USN Rollbacks and Lingering Objects

#### 52.10 PKI Logs

* 52.10.1 AD CS Certificate Authority Auditing: Enabling Extended CA Auditing to Track Certificate Requests, Issuances, and Denials
* 52.10.2 Template Modification Telemetry: Monitoring Event ID 4898 (Certificate Template Loaded) and Event 5136 Over Template ACLs
* 52.10.3 Enrollment Service Telemetry: Tracking NDES and Web Enrollment Request Logs for ESC Exploitation Patterns

#### 52.11 Federation Logs

* 52.11.1 AD FS Auditing Engine: Enabling Verbose Security Auditing in AD FS Properties to Track Issued Tokens and Auth Requests
* 52.11.2 SAML Assertion & Claim Telemetry: Analyzing Event ID 403, 410, and 501 Logs to Track Claims Transformations and Relying Party Issuance
* 52.11.3 WAP Perimeter Logs: Ingesting Web Application Proxy Event Logs to Correlate External Client IPs with On-Premises Auth Claims

#### 52.12 Entra and Cloud Logs

* 52.12.1 Entra ID Audit Logs: Ingesting Tenant Audit Logs for Role Assignments, Service Principal Credentials, and App Registrations
* 52.12.2 Entra ID Sign-In Logs: Correlating Interactive, Non-Interactive, Service Principal, and Managed Identity Sign-in Logs
* 52.12.3 Diagnostic Settings Pipelines: Streaming Cloud Audit Telemetry via Azure Monitor and Graph Streaming APIs to Security Data Lakes

#### 52.13 Network Authentication Logs

* 52.13.1 RADIUS and NPS Logging: Ingesting Network Policy Server Logs to Audit 802.1X Wired/Wireless and VPN Connection Attempts
* 52.13.2 DNS Security Telemetry: Tracking DNS Dynamic Updates (Event ID 2501), Zone Transfer Requests, and Query Resolution Logs
* 52.13.3 DHCP & IPAM Logs: Correlating IP Allocation Records with Domain Controller Logons to Track Transient Devices

#### 52.14 Microsoft Defender for Identity

* 52.14.1 MDI Sensor Telemetry Integration: Capturing Deep Network Packet Inspection (RPC, SMB, Kerberos, LDAP) and ETW Events
* 52.14.2 MDI Alert Schema: Mapping Defender for Identity Detections (e.g., Reconnaissance, Credential Access, Lateral Movement) into XDR
* 52.14.3 Sensor Health Monitoring: Tracking Sensor Offline Events, Performance Degradation, and Packet Dropping Telemetry

#### 52.15 SIEM Integration

* 52.15.1 Windows Event Forwarding (WEF): Deploying Standardized WEF Subscriptions with HTTPS/WinRM to Centralize Collector Topologies
* 52.15.2 Ingestion Architecture: Utilizing Azure Monitor Agent (AMA), Syslog, and Graph APIs to Transport Telemetry to Microsoft Sentinel/SIEM
* 52.15.3 Event Filtering & Parsing: Parsing Unstructured Event Data into Normalized Security Schemas (ASIM / CIM) for Real-Time Correlation

#### 52.16 Evidence Integrity

* 52.16.1 Immutable Storage Mechanisms: Forwarding Logs to Write-Once-Read-Many (WORM) Repositories and Cryptographically Sealed Storage
* 52.16.2 Log Hash Chaining: Utilizing Cryptographic Hashing and Digital Signatures on Exported Event Log Bundles
* 52.16.3 Segregation of Audit Administration: Restricting Access to Centralized Log Repositories Away from Domain Admins to Prevent Evidence Alteration

#### 52.17 Identity Anti-Forensics

* 52.17.1 Event Log Clearing: Detecting Event ID 1102 (Security Audit Log Cleared) and Event ID 104 (System Log Cleared) Across Domain Controllers
* 52.17.2 Audit Policy Modification: Monitoring Event ID 4719 (System Audit Policy Changed) to Spot Unauthorized Category Disabling
* 52.17.3 SACL Removal: Triggering High-Priority Alerts When SACL Entries are Removed from Sensitive Directory Containers
* 52.17.4 Sensor Tampering: Detecting MDI Sensor Service Stoppages, Driver Unloading, and Process Injection Attempts
* 52.17.5 Log Forwarder Interruption: Monitoring Heartbeat Failures and Buffer Overflows on Windows Event Forwarding (WEF) Agents
* 52.17.6 Cloud Audit Suppression: Tracking Disabling of Entra Diagnostic Settings, Graph API Log Exclusion Filters, and Defender Blinding

#### 53.1 Detection Engineering Methodology

* 53.1.1 Detection Development Lifecycle (DDL): Structuring Detection Requirements, Telemetry Scoping, Rule Authoring, Testing, and Continuous Tuning
* 53.1.2 Mapping to MITRE ATT\&CK & CAR: Aligning Detection Logic with Identity Attack Techniques (T1558, T1110, T1003, T1098, T1484)
* 53.1.3 Detection-as-Code (DaC) Architecture: Managing SIEM Detection Rules, KQL Queries, and Sigma Rules via Version-Controlled CI/CD Pipelines

#### 53.2 Baselines and Normal Behavior

* 53.2.1 Establishing Protocol & Authentication Baselines: Profiling Standard Operating Hours, Source Subnets, and Request Volumes per Principal
* 53.2.2 Filtering Administrative Baseline Noise: Whitelisting Legitimate System Accounts, Scheduled Tasks, and Authorized Security Scanners
* 53.2.3 Statistical Anomaly Thresholding: Utilizing Dynamic Standard Deviations and Time-Series Analytics to Reduce False Positive Rates

#### 53.3 Kerberos Detection

* 53.3.1 Anomalous Ticket-Granting Ticket (TGT) Requests: Detecting Anomalous Encryption Downgrades (RC4-HMAC Requests) via Event ID 4768
* 53.3.2 Ticket Renewal & Lifetime Anomalies: Tracking Suspicious Ticket Renewal Request Patterns and Out-of-Bounds Ticket Lifetimes
* 53.3.3 Kerberos Pre-Authentication Bypasses: Monitoring Failed Pre-Authentications (Event ID 4771) and Unexpected Pre-Auth Disabling Events

#### 53.4 NTLM Detection

* 53.4.1 Unexpected NTLM Usage: Monitoring Fallback to NTLM v1/v2 in Environments Enforcing Kerberos First Policies (Event ID 8001–8004)
* 53.4.2 Cross-Domain NTLM Anomaly Detection: Identifying Anomalous External NTLM Authentication Vectors Across Forest Trust Interfaces
* 53.4.3 Catching NTLM Relay Patterns: Correlating Rapid, Multi-Host NTLM Binds Originating from Singular Internal Machine Addresses

#### 53.5 LDAP Detection

* 53.5.1 Unencrypted & Anonymous LDAP Query Monitoring: Tracking Cleartext Binds (Port 389) and Unauthenticated Schema Enumeration via Event ID 2887/2889
* 53.5.2 LDAP Reconnaissance Detection: Identifying Heavy Mass-Object Enumeration Queries Targeted at High-Value Groups and Sensitive Attributes
* 53.5.3 Detecting Malformed & Excessive Filters: Catching Complex LDAP Injection Patterns and Reckless Graph Scans

#### 53.6 Password Spray Detection

* 53.6.1 Horizontal vs. Vertical Password Spray Mechanics: Distinguishing Low-and-Slow Password Sprays from Traditional Brute-Force Floods
* 53.6.2 Correlating Multi-Source Event ID 4625/4771 Logs: Aggregating Failed Logon Telemetry Across Multiple Accounts Targeted from Singular Source IPs/Hosts
* 53.6.3 Hybrid Password Spray Tracking: Correlating On-Premises Netlogon Failures with Entra ID Sign-In Risk Telemetry

#### 53.7 Kerberoasting Detection

* 53.7.1 Service Ticket Request Volumetrics: Detecting Spikes in TGS Requests (Event ID 4769) Requesting Weak RC4 Encryption Options
* 53.7.2 High-Value Account Monitoring: Alerting Instantly When TGS Requests Target Tier 0 Service Principal Names (SPNs)
* 53.7.3 Deception-Based Kerberoasting Alerts: Setting Up Lure/Honey SPN Accounts to Produce 100% High-Confidence Detections Upon TGS Request

#### 53.8 AS-REP Roasting Detection

* 53.8.1 Pre-Authentication Disabled Monitoring: Alerting When Event ID 4768 Is Generated for Accounts Configured with `DONT_REQUIRE_PREAUTH`
* 53.8.2 Bulk AS-REP Request Tracking: Detecting Mass Kerberos TGT Requests Lacking Pre-Authentication Across Short Time Intervals
* 53.8.3 Account Configuration Tracking: Correlating Event ID 5136 (Attribute Modification) When `userAccountControl` Flags Are Altered to Disable Pre-Auth

#### 53.9 Credential Access Detection

* 53.9.1 DCSync Attack Detection: Catching Non-DC Directory Replication Requests via Event ID 4662 (Matching DRS Guids: `1131f6aa-...` / `1131f6ad-...`)
* 53.9.2 NTDS.dit Extraction Telemetry: Monitoring VSS Service Creation (Event ID 7036), Volume Shadow Copy Access, and `esentutl.exe` Invocations
* 53.9.3 LSA Secrets & Memory Dumps: Catching Unauthorized LSASS Process Access (Event ID 10 in Sysmon) and Secrets Dump Execution

#### 53.10 Privileged Group Change Detection

* 53.10.1 Direct Tier 0 Membership Changes: High-Priority Real-Time Alerts for Additions to `Domain Admins`, `Enterprise Admins`, and `Schema Admins` (Event ID 4728/4756)
* 53.10.2 Transitive & Nested Group Modification: Detecting Indirect Privilege Escalation via Nested Sub-Group Membership Insertions
* 53.10.3 Out-of-Change-Window Group Modifications: Correlating Group Mod Events Against Scheduled Change Management Tickets

#### 53.11 ACL and ACE Change Detection

* 53.11.1 Directory DACL Modification Auditing: Capturing Write-DACL and Ownership Overrides Over Sensitive Containers via Event ID 5136
* 53.11.2 Detecting Shadow Admin Creation: Identifying Newly Assigned Dangerous Rights (`GenericAll`, `WriteProperty`, `ResetPassword`) Over High-Value Objects
* 53.11.3 AdminSDHolder Modification Alerts: Monitoring ACL Alterations on the `CN=AdminSDHolder` Container Before SDProp Execution

#### 53.12 GPO Change Detection

* 53.12.1 Unscheduled GPO Mod Monitoring: Capturing Object Modifications Within `CN=Policies,CN=System` Containers
* 53.12.2 High-Risk GPO Setting Alterations: Detecting Modification of Audit Policies, Security Options, Restricted Groups, or User Rights Assignments
* 53.12.3 SYSVOL Script & Executable Tampering: Alerting on New or Modified `.ps1`, `.bat`, or `.exe` Files Deposited Within SYSVOL Policies Paths

#### 53.13 Service Account Detection

* 53.13.1 Interactive Logon Alerts for Non-Human Accounts: Catching Service Accounts Executing Interactive Logons (Logon Type 2 / Type 10)
* 53.13.2 gMSA & dMSA Abuse Anomalies: Detecting Unauthorized Hosts Attempting Key Distribution Service (KDS) Secret Retrieval
* 53.13.3 Service Account Behavior Variance: Tracking Deviations in Source Machine, Target Machine, or API Query Patterns for Managed Identities

#### 53.14 Authentication Correlation

* 53.14.1 Multi-Log Event Chaining: Linking Source Network IP, Domain Controller Event ID 4624/4769, and Endpoint Process Creation Logs
* 53.14.2 Session Lifetime Correlation: Matching Ticket-Granting Services (TGS) to Active Network Connections to Identify Ticket Abuse/Pass-the-Ticket
* 53.14.3 Detecting Authentication Anomalies Across Tiers: Alerting When Lower-Tier Accounts Attempt Direct Authentication to Higher-Tier Systems

#### 53.15 Cross-Identity Correlation

* 53.15.1 On-Premises to Cloud Sign-In Correlation: Mapping Active Directory Logons to Upstream Microsoft Entra ID Interactive and Non-Interactive Sign-Ins
* 53.15.2 Tracking Identity Pivot Chains: Correlating Cloud Compromise Telemetry (e.g., Entra ID Risk Events) with On-Premises Kerberos Requests
* 53.15.3 B2B and Federated Identity Abuse: Auditing Federation Assertion Ingestion Against Downstream Local Resource Authorizations

#### 53.16 Alert Triage and Prioritization

* 53.16.1 Contextual Severity Scoring: Dynamic Alert Scoring Based on Target Principal Tier, System Criticality, and Asset Location
* 53.16.2 Automated Incident Triage Runbooks: Enforcing Automated SOC Workflows to Enrich Telemetry (e.g., Pulling BloodHound Paths, HR Status)
* 53.16.3 Measuring Detection Precision & Fatigue: Tracking False Positive Rates, Mean Time to Detect (MTTD), and Mean Time to Respond (MTTR) for Identity Alerts

#### 54.1 DCSync Detection

* 54.1.1 Mechanics of MS-DRSR Abuse: Analyzing How Adversaries Invoke `DsGetNcChanges` Requests to Pull Password Hashes Without Executing Code on DCs
* 54.1.2 Directory SACL & Event ID 4662 Correlation: Detecting Non-DC IP Addresses Requesting Directory Replication Extended Rights (`1131f6aa-9c0e-11d1-a7f3-00c04f79e7a0` and `1131f6ad-9c0e-11d1-a7f3-00c04f79e7a0`)
* 54.1.3 RPC Network Telemetry & MDI Integration: Utilizing Deep Packet Inspection (DPI) via Microsoft Defender for Identity to Flag Anomaly DRSUAPI Calls

#### 54.2 DCShadow Detection

* 54.2.1 Rogue Domain Controller Registration Mechanics: Analyzing How Threat Actors Inject Modifications via Temporary Configuration Partition Registration
* 54.2.2 Monitoring Configuration Partition Modifications: Alerting on Event ID 5136/5137 Over `CN=Sites,CN=Configuration` and SPN Registrations (`GC/` or KrbTgt GUIDs)
* 54.2.3 Detecting Push Replication Anomalies: Catching Unsolicited `DsReplicaAdd` or `DsReplicaSync` RPC Calls Initiated from Non-DC Workstations

#### 54.3 Replication Rights Monitoring

* 54.3.1 Auditing Domain Head DACLs: Scanning Root Domain Security Descriptors for Non-Standard `Replicating Directory Changes` Rights Assignments
* 54.3.2 SDProp & AdminSDHolder Replication Leakage: Tracking System Access Control Lists (SACLs) Over Protected Administrative Groups
* 54.3.3 Real-Time ACL Modification Telemetry: Generating High-Priority Alerts When `DS-Replication-Get-Changes` Rights Are Delegated to Non-DC Accounts

#### 54.4 Abnormal Replication

* 54.4.1 Baseline Replication Topologies: Profiling Standard DC-to-DC Replication Traffic Schedules, Partner Pairs, and Data Transfer Volumes
* 54.4.2 Inbound/Outbound Replication Drift: Detecting Unscheduled Inter-Site Transits and High-Frequency Partial Attribute Set (PAS) Updates
* 54.4.3 Tracking DRS Replication Error Event Logs: Correlating Event IDs 2095, 1388, and 1925 to Spot Out-of-Sequence Replication Activity

#### 54.5 SMB Movement

* 54.5.1 Admin Share Access Telemetry: Monitoring Authentication and File Access Over Administrative Shares (`C$`, `ADMIN$`, `IPC$`) via Event ID 5140/5145
* 54.5.2 SMB Named Pipe Inspection: Tracking Remote Named Pipe Operations (`\pipe\svcctl`, `\pipe\atsvc`, `\pipe\samr`) Used for Remote Execution
* 54.5.3 Detecting Lateral SMB File Transfers: Identifying Binary Drops, Script Transfers, and Staging Directories Across Internal Subnets

#### 54.6 WinRM Movement

* 54.6.1 PowerShell Remoting & WinRM Telemetry: Ingesting Event ID 4624 (Logon Type 3) Combined with `WSMan` Operational Log Tracing
* 54.6.2 Script Block & Transcribing Auditing: Enabling PowerShell Event ID 4104 (Script Block Logging) to Capture Obfuscated Commands Executed via WinRM
* 54.6.3 Restricting WinRM Administrative Paths: Profiling and Alerting on Non-Jump-Host Connections to Port 5985 (HTTP) and 5986 (HTTPS)

#### 54.7 WMI and DCOM Movement

* 54.7.1 WMI Remote Execution Telemetry: Correlating Event ID 4624 (Type 3) with WMI Operational Logs (`Microsoft-Windows-WMI-Activity/Operational` Event ID 5861)
* 54.7.2 DCOM Object Instantiation: Tracking Remote Creation of Sensitive COM Objects (e.g., `MMC20.Application`, `ShellWindows`, `ShellBrowserWindow`)
* 54.7.3 Detecting Persistent WMI Event Consumers: Alerting on Unauthorized Creation of `__EventFilter`, `__EventConsumer`, and `__FilterToConsumerBinding`

#### 54.8 RDP Movement

* 54.8.1 Remote Desktop Logon Telemetry: Monitoring Event ID 4624 (Logon Type 10) and `TerminalServices-LocalSessionManager` Event ID 21/22
* 54.8.2 Detecting Restricted Admin Mode & Pass-the-Hash for RDP: Tracking Network Logons (Type 3) Utilizing RDP Endpoints Without Interactive Credential Input
* 54.8.3 Anomalous RDP Source Tracking: Alerting on External, Non-PAW (Privileged Access Workstation) RDP Sessions Targeting Tier 0/1 Servers

#### 54.9 PsExec and Service Execution

* 54.9.1 Service Control Manager Telemetry: Detecting Remote Service Installations via Event ID 7045 (New Service Created) and Event ID 4697
* 54.9.2 PsExec Artifact Signatures: Matching Named Pipe Generations (`\pipe\psexec*`), Binary Drops (`PSEXESVC.exe`), and Custom Service Names
* 54.9.3 Catching Living-off-the-Land Services: Identifying Legitimate Utilities (e.g., `sc.exe`, `net.exe`) Executed via Remote Service Management Interfaces

#### 54.10 Scheduled Task Activity

* 54.10.1 Remote Task Scheduling Telemetry: Monitoring Event ID 4698 (Scheduled Task Created) and Event ID 4702 (Scheduled Task Updated)
* 54.10.2 Task Scheduler RPC Calls: Tracking `ITaskSchedulerService` Interfaces and Remote Modifications Over `C:\Windows\System32\Tasks`
* 54.10.3 Identifying Volatile/Immediate Tasks: Detecting Tasks Configured to Run Immediately and Delete Themselves Upon Completion to Evade Audits

#### 54.11 Lateral Authentication

* 54.11.1 Tracking Pass-the-Hash (PtH) & Pass-the-Ticket (PtT): Correlating NTLM Authentication (Event ID 4624 with NTLM Package) Without Prior TGT Requests
* 54.11.2 Detecting Kerberos Ticket Injections: Identifying Mismatched Kerberos Ticket Client Names and Workstation Identifiers Across Network Session Logs
* 54.11.3 Explicit Credential Telemetry (Runas): Tracking Event ID 4648 Across Member Servers to Detect Secondary Process Execution Under Alternate Principals

#### 54.12 Tier 0 Administrative Movement

* 54.12.1 Enforcing Control Plane Boundaries: Restricting Inbound Administrative Connections to Domain Controllers Exclusively from Dedicated PAWs
* 54.12.2 Catching Tier-Violation Movements: Triggering Instant Critical Alerts When Tier 2 Workstation Accounts or Sessions Attempt Direct Management of Tier 0 Hosts
* 54.12.3 Real-Time Network & Identity Correlation: Mapping Firewall Flow Logs and Identity Telemetry to Isolate and Neutralize Boundary-Crossing Movement

#### 55.1 Certificate Enrollment Monitoring

* 55.1.1 Event ID 4887 & CA Audit Ingestion: Monitoring Certificate Authority Issuance Events to Match Requestor Identity Against Subject Alt Name (SAN)
* 55.1.2 Detecting SAN Misalignments: Alerting on Certificate Requests Where UPN/DNS SAN Entries Mismatch the Requesting Principal's Security Context
* 55.1.3 Anomalous Auto-Enrollment & Volumetrics: Identifying Mass Certificate Requests Originating from Low-Privileged Accounts across Short Intervals

#### 55.2 Certificate Template Changes

* 55.2.1 Tracking Event ID 4898 & 5136 Over Templates: Monitoring Modulations in `CN=Certificate Templates,CN=Public Key Services` Containers
* 55.2.2 Detecting Dangerous EKU and Flag Insertions: Alerting on the Activation of `ENROLLEE_SUPPLIES_SUBJECT` or `Client Authentication` EKUs on Open Templates
* 55.2.3 DACL Tampering on Certificate Templates: Catching Permission Modifications Granting `Enroll` or `GenericAll` Rights to Unprivileged Groups

#### 55.3 CA Configuration Changes

* 55.3.1 Auditing Event ID 4885 & Registry Modulations: Monitoring Modifies to `HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration`
* 55.3.2 Catching Flag Modifications (`EDITF_ATTRIBUTESUBJECTALTNAME2`): Alerting on Dynamic Alterations to CA Flag Settings Enabling User-Defined SAN Extensions
* 55.3.3 Auditing CA Security Descriptors: Detecting Administrative Access Delegations and `WriteDACL` Overrides Over Certification Authority Objects

#### 55.4 Certificate Mapping Anomalies

* 55.4.1 KB5014754 Correlation & Event ID 39/40/41 Audit: Tracking Weak vs. Strong Certificate Binding Events on Domain Controllers
* 55.4.2 Detecting Explicit `altSecurityIdentities` Injections: Alerting on Manual User Account Attribute Modifications Adding Unrecognized X.509 Mappings
* 55.4.3 Identifying Computer Account Name Collisions: Catching CVE-2022-26923 Manipulation Involving `dNSHostName` Modifications Prior to Cert Enrollment

#### 55.5 PKINIT Anomalies

* 55.5.1 Kerberos Event ID 4768 Pre-Auth Analysis: Tracking TGT Requests Authenticated via Certificates (`PA-PK-AS-REQ`) Without Corresponding Interactive Sessions
* 55.5.2 Cross-Domain PKINIT Impersonation: Monitoring Mismatched Client Principal Names and Ticket Certificate Identifiers During Initial Authentication
* 55.5.3 Detecting PKINIT Encryption Downgrades: Catching Kerberos Pre-Authentication Requests Enforcing Legacy RC4 Encryption Keys Over Smart Cards

#### 55.6 AD CS Escalation Indicators

* 55.6.1 Monitoring ESC Vulnerability Chains (ESC1–ESC17): Correlating Certipy/Certify Tooling Signatures with High-Risk Template Enrollment Events
* 55.6.2 Detecting HTTP & RPC NTLM Relay Attempts (ESC8/ESC11): Tracking Unauthenticated NTLM Invocations Targeting AD CS Web Enrollment Endpoints
* 55.6.3 CA Private Key Extraction Telemetry (ESC5/ESC7): Alerting on Backup Key Requests, `CertUtil` Export Commands, and Unapproved KRA Access

#### 55.7 Token-Signing Activity

* 55.7.1 AD FS Token Issuance Logging: Ingesting Event ID 500 and 501 Telemetry to Track SAML Assertion Generation Contexts
* 55.7.2 Golden SAML Token Detection: Catching SAML Tokens Presented to Cloud Apps Lacking Corresponding On-Premises AD FS Authentication Logs
* 55.7.3 Token-Signing Certificate Export & Rollover Alerts: Monitoring Unscheduled Access to Private Key Storage Containers (`CN=ADFS,CN=Microsoft...`)

#### 55.8 Claims Manipulation

* 55.8.1 Tracking Federation Claims Engine Modifications: Auditing Configuration Changes to AD FS Claims Transformation Rules via Event ID 307
* 55.8.2 Detecting Administrative Claim Overrides: Alerting on Issuance Rules Modified to Force High-Privilege Group SIDs into SAML Assertions
* 55.8.3 Unsanitized Claims Processing: Identifying Injected Attributes Bypassing Perimeter WAP Validation Rules at the Federation Gateway

#### 55.9 Federation Trust Changes

* 55.9.1 Monitoring Relying Party Trust (RPT) Alterations: Tracking Event ID 303 & 304 Log Telemetry Flagging New or Modified SAML Integrations
* 55.9.2 Unapproved Cross-Tenant Federation Additions: Alerting on New External Identity Provider Registrations in Entra ID and On-Premises AD FS
* 55.9.3 Metadata Endpoint Tampering: Detecting Insecure HTTP Metadata Refresh Calls and Untrusted Issuer Certificate Binds

#### 55.10 Entra Connect Abuse

* 55.10.1 Monitoring Synchronization Account Telemetry: Tracking Anomalous Logons or API Calls Executed by the On-Premises `MSOL_` / `ADSync` Accounts
* 55.10.2 Detecting Sync Service Password Extraction: Alerting on Process Access (LSASS / DPAPI) Targeting Entra Connect Encryption Keys
* 55.10.3 Staging Mode Misconfiguration & Takeover: Identifying Unauthorized Promotion of Rogue Entra Connect Staging Servers into Active Sync Roles

#### 55.11 Synchronization Anomalies

* 55.11.1 Detecting Shadow Credential Injections (`msDS-KeyCredentialLink`): Monitoring Out-of-Band Additions of Public Keys to Synchronized Account Objects
* 55.11.2 Immutable ID (`mS-DS-ConsistencyGuid`) Hijacking: Alerting on Source Anchor Changes Used to Map On-Premises Accounts to Unlinked Cloud Users
* 55.11.3 Mass Attribute Mutation Auditing: Detecting Sudden Bulk Modifications to `mail`, `userPrincipalName`, or Group Membership Attributes During Sync

#### 55.12 Token Theft Indicators

* 55.12.1 Primary Refresh Token (PRT) Extraction: Catching LSASS Dumping or TPM Key Usage Targeting Entra ID PRT Credentials on Endpoints
* 55.12.2 Detecting Session Hijacking & Token Replay: Correlating Mismatched Device Identifiers, IP Ranges, and User-Agents across OAuth Access Tokens
* 55.12.3 Anomaly Alerts for Continuous Access Evaluation (CAE): Monitoring Real-Time Token Revocation Triggers and CAE Re-Authentication Requests

#### 55.13 Service Principal Changes

* 55.13.1 Auditing Entra ID Application Credential Addition: Alerting on New Client Secrets or Certificates Added to Privileged Enterprise Applications
* 55.13.2 Monitoring High-Risk API Permission Grants: Tracking App Registrations Assigned `Directory.ReadWrite.All` or `RoleManagement.ReadWrite.Directory`
* 55.13.3 Federated Identity Credential Abuse: Detecting Unapproved OIDC Trust Additions Binding External Workloads to Internal Service Principals

#### 55.14 Application Consent Abuse

* 55.14.1 Detecting Illicit OAuth Consent Grants: Tracking User or Admin Consent Events Granted to Unverified, Multi-Tenant Applications
* 55.14.2 High-Risk Permission Scope Alerts: Generating High-Severity Alerts When Apps Request `Offline_Access`, `Mail.Read`, or `Files.ReadWrite.All`
* 55.14.3 Monitoring Admin Consent Workflow Bypasses: Identifying Applications Granted Direct Tenant-Wide Privileges Without Security Review Approval

#### 55.15 Cloud Privilege Changes

* 55.15.1 Monitoring Entra ID Directory Role Assignments: Real-Time Telemetry for Assignment of `Global Administrator` or `Privileged Role Admin`
* 55.15.2 Tracking PIM Activation & Elevation Anomalies: Catching Out-of-Bounds Privileged Identity Management Activations Lacking Change Tickets
* 55.15.3 Cloud Break-Glass Account Activity Alerts: Immediate Security Alerts Triggered by Any Logon or Configuration Modification by Emergency Accounts

#### 56.1 Hunting the Directory

* 56.1.1 Hypothesis-Driven Directory Hunting: Formulating Threat Hypotheses Based on Adversary TTPs (MITRE ATT\&CK) and Directory Telemetry
* 56.1.2 LDAP Baseline Differencing: Executing Automated Directory Snapshots to Identify Stale, Modified, or Unexpectedly Created Objects
* 56.1.3 Hunting Schema & Container Anomalies: Auditing Schema Modifications, Non-Standard Object Classes, and Suspicious Structural Containers

#### 56.2 Hunting Effective Control

* 56.2.1 Graph Differential Analysis: Comparing Historical BloodHound/Cypher Snapshots to Identify Newly Emerged Attack Paths
* 56.2.2 Uncovering Shadow Admins: Searching for Indirect Control Over Tier 0 Accounts via Rights Like `WriteDACL`, `GenericAll`, and `WriteProperty`
* 56.2.3 Calculating Effective Permission Baselines: Evaluating Complex Token Access Rights across Nested Groups and OU Inheritance Trees

#### 56.3 Hunting Privileged Groups

* 56.3.1 AdminSDHolder & SDProp Auditing: Sweeping Protected Administrative Groups (`Domain Admins`, `Enterprise Admins`) for Unauthorized Additions
* 56.3.2 Hunting Nested & Transitive Group Memberships: Identifying Obfuscated Access Chains Created by Nesting Lower-Tier Groups into Higher-Tier Enclaves
* 56.3.3 Auditing Dynamic & Foreign Group Memberships: Sweeping Cross-Domain and Foreign Security Principal (FSP) Group Membership Links

#### 56.4 Hunting ACL Backdoors

* 56.4.1 Sweeping Directory Object DACLs: Writing PowerShell and LDAP Scripts to Identify Non-Standard ACE Grants Over Sensitive Containers
* 56.4.2 Hunting `ForceChangePassword` & Ownership Abuse: Identifying Accounts Granted Explicit Password Reset or Ownership Permissions Over Tier 0 Objects
* 56.4.3 Detecting Orphaned & Suspicious SIDs: Auditing Access Control Lists for Deleted SIDs or Unrecognized External Domain Identifiers

#### 56.5 Hunting Delegation

* 56.5.1 Hunting Unconstrained Delegation: Sweeping the Domain for Non-DC Computer Accounts Configured with `TRUSTED_FOR_DELEGATION`
* 56.5.2 Hunting Constrained Delegation Abuses: Auditing `msDS-AllowedToDelegateTo` Attributes for Sensitive Target Services (e.g., `cifs/`, `ldap/`, `host/`)
* 56.5.3 Hunting Resource-Based Constrained Delegation (RBCD): Sweeping `msDS-AllowedToActOnBehalfOfOtherIdentity` Attributes Over High-Value Computer Objects

#### 56.6 Hunting GPO Persistence

* 56.6.1 GPC/GPT Consistency Sweeps: Differencing Group Policy Container Attributes in AD Against SYSVOL Policy Template Files
* 56.6.2 Hunting Immediate Scheduled Task Injections: Sweeping `ScheduledTasks.xml` Files Within SYSVOL Policies for Malicious Binary Execution
* 56.6.3 Auditing Restrictive Group Policy Settings: Identifying Unauthorized Modulations to Local Security Options, User Rights, and Audit Configurations

#### 56.7 Hunting Replication Rights

* 56.7.1 Auditing `DS-Replication-Get-Changes` Access: Sweeping the Domain Head Security Descriptor for Non-DC Principals Granted Directory Replication Rights
* 56.7.2 Identifying Stealthy DCSync Persistence: Uncovering Accounts Possessing Both `DS-Replication-Get-Changes` and `DS-Replication-Get-Changes-All`
* 56.7.3 Tracking Extended Right Delegation Patterns: Auditing Delegated Operational Rights across Custom Partition Boundaries

#### 56.8 Hunting Certificate Abuse

* 56.8.1 Sweeping Certificate Templates for ESC Vulnerabilities: Auditing Template EKUs, DACLs, and `ENROLLEE_SUPPLIES_SUBJECT` Flags (ESC1–ESC17)
* 56.8.2 Hunting SAN/UPN Mapping Anomalies: Identifying Certificates Issued with Mismatched Subject Alternative Names or Alternate Mappings
* 56.8.3 Auditing CA Security Configurations: Sweeping Certificate Authority Registry Flags (`EDITF_ATTRIBUTESUBJECTALTNAME2`) and CA Permissions

#### 56.9 Hunting Federation Persistence

* 56.9.1 Auditing AD FS Claims Transformation Rules: Sweeping Issuance Claims Rules for Injected Custom Logic Adding Explicit Group Claims
* 56.9.2 Hunting Exported Token-Signing Certificates: Auditing Private Key Access Logs Over the `CN=ADFS,CN=Microsoft...` Active Directory Container
* 56.9.3 Relying Party Trust Sweeps: Identifying Secondary, Unregistered, or Insecure Relying Party Trusts Configured on Federation Gateways

#### 56.10 Hunting Hybrid Trust

* 56.10.1 Hunting Shadow Credentials (`msDS-KeyCredentialLink`): Sweeping User and Computer Objects for Out-of-Band Key Credentials Appended to Attributes
* 56.10.2 Sweeping Entra Connect & Cloud Sync Persistence: Auditing `MSOL_` / `ADSync` Accounts for Unauthorized Privilege Escalations and Writebacks
* 56.10.3 Hunting OIDC & Federated Identity Credentials: Auditing Service Principals in Entra ID for Unapproved External Federated Key Bindings

#### 56.11 Honeytokens

* 56.11.1 Designing High-Fidelity Honeytokens: Crafting Unused Accounts, Keys, and Tokens with Attractive Naming Schemes (e.g., `svc_backup_admin`)
* 56.11.2 Auditing SACLs Over Honeytokens: Applying Explicit Read and Operation SACLs Over Honeytoken Attributes to Generate Instant Alerts
* 56.11.3 Honeytoken Ingestion Pipelines: Routing Any Interaction with Honeytoken Accounts directly to Tier 1 Incident Response Playbooks

#### 56.12 Decoy Accounts

* 56.12.1 Deploying Deceptive Domain Accounts: Constructing Fully Provisioned Decoy Administrator and Service Accounts Integrated into the Directory
* 56.12.2 Enforcing Zero-Legitimate-Use Controls: Blocking All Legitimate Operations on Decoy Accounts to Guarantee 100% Signal-to-Noise Ratio
* 56.12.3 Monitoring Decoy Authentication Attempts: Alerting Instantly on Event ID 4625/4768 Logs Target Decoy User Principals

#### 56.13 Decoy Credentials

* 56.13.1 Injecting Lured Credentials in Memory: Depositing Synthetic Credentials into LSASS Memory on High-Exposure Workstations and Jump Hosts
* 56.13.2 LSASS Dumping Traps: Catching Credential Access Utilities (e.g., Mimikatz, LSASS memory readers) Triggering Alerts Upon Lure Access
* 56.13.3 DPAPI & Browser Decoy Artifacts: Depositing Decoy Credentials and Saved Passwords in Endpoint Credential Vaults to Catch Reconnaissance

#### 56.14 Decoy SPNs

* 56.14.1 Constructing Kerberoasting Traps: Assigning Decoy Service Principal Names (SPNs) Configured with Weak RC4 Encryption Keys to Lure Accounts
* 56.14.2 Monitoring TGS Ticket Requests: Generating High-Priority Real-Time Alerts via Event ID 4769 Whenever a Decoy SPN Is Requested
* 56.14.3 Deceptive SPN Placement: Placing Decoy SPNs Strategically in Directory Containers to Intercept Automated Kerberoasting Scanners

#### 56.15 Decoy Certificates

* 56.15.1 Deploying Vulnerable Decoy Templates: Publishing Seemingly Misconfigured AD CS Templates (Decoy ESC1/ESC2) Scoped with Tight SACLs
* 56.15.2 Trapping Automated PKI Scanners: Catching Tools (e.g., Certify, Certipy) Requesting Certificates Against Decoy Templates
* 56.15.3 Decoy Certificate Revocation Tracking: Alerting on Enrollment Attempts (Event ID 4887) Targeting Canary Certificate Infrastructure

#### 56.16 Decoy Administrative Paths

* 56.16.1 Constructing Canary Jump Hosts & PAWs: Placing Seemingly Unlocked Administrative Workstations with Active Sessions in Low-Security Segments
* 56.16.2 Trapping Remote Management Trajectories: Monitoring Inbound RDP, WinRM, and SMB Binds Directed at Deceptive Management Endpoints
* 56.16.3 Severing Trapped Attack Paths: Isolate and Contain Adversaries Interacting with Deceptive Paths Before Control Plane Reachability Is Established

#### 57.1 Identity Forensic Methodology

* 57.1.1 Evidence Handling in Identity Enclaves: Establishing Chain of Custody Protocols for Volatile Memory, Domain Controller Disks, and Active Directory Database Artifacts
* 57.1.2 Scoping Identity Incidents: Defining Boundaries Between Host-Level Exploitation, Local Credential Theft, and Control Plane Domain Compromise
* 57.1.3 Forensic Workstation & Tooling Baselines: Deploying Isolated Forensic Enclaves Equipped with `NTDS.dit` Parsers, Volatility, and Log Correlation Pipelines

#### 57.2 LSASS and Memory

* 57.2.1 Volatile Memory Acquisition on DCs: Executing Crash Dumps and Live Memory Extractions on Domain Controllers and Privileged Access Workstations
* 57.2.2 Carving LSASS Process Memory: Analyzing LSASS Dumps for Injected DLLs, Unloaded Drivers, Process Hollowing, and Hooked LSA Authenticators
* 57.2.3 Extracting Memory-Resident Credentials: Recovering Plaintext Passwords, NTLM Hashes, Kerberos Encryption Keys, and PINs from In-Memory LSA Structures

#### 57.3 Tokens and Logon Sessions

* 57.3.1 Token Manipulation Forensics: Analyzing Primary, Impersonation, and Delegation Tokens Active in Endpoint Kernel Memory
* 57.3.2 Reconstructing Active Logon Sessions: Mapping Logon Session LUIDs Against Event ID 4624 Logs to Identify Pass-the-Hash and Token Theft Vectors
* 57.3.3 Detecting Access Token Injections: Identifying Mismatched Process Tokens and Privileged Security Identifiers (SIDs) Injected into User-Mode Processes

#### 57.4 Kerberos Tickets

* 57.4.1 Forensic Analysis of Kerberos Artifacts: Extracting and Parsing `.kirbi` Files, Cache Files (`krb5cc`), and LSASS Kerberos Ticket Stores
* 57.4.2 Detecting Golden and Silver Ticket Forgery: Analyzing Ticket Lifetime Anomalies, Non-Standard PAC Signatures, Mismatched SIDs, and Encryption Suite Downgrades
* 57.4.3 Pass-the-Ticket & Overpass-the-Hash Identification: Correlating Memory-Resident Tickets with Domain Controller Issue Logs to Identify Injected TGTs

#### 57.5 Credential Artifacts

* 57.5.1 Parsing the LSA Secrets Registry Hive: Forensic Extraction of Cached Domain Credentials (`MSCASH2`), Service Account Hashes, and Autologon Passwords
* 57.5.2 SAM & Vault Forensic Analysis: Recovering Local Administrator Account Hashes, Credential Manager Vaults, and Web Browser Stored Passwords
* 57.5.3 Offline `NTDS.dit` Database Parsing: Carving Active Directory Database Snapshots to Audit Historic Hash Values, `sIDHistory` Injections, and Tombstoned Objects

#### 57.6 DPAPI

* 57.6.1 Data Protection API (DPAPI) Architecture: Mechanics of Master Keys, Domain Backup Keys, and DPAPI-Protected Secret Encryption
* 57.6.2 Extracting DPAPI Domain Master Keys: Recovering LSA Domain DPAPI Backup Keys (`PREFERRED` / `masterkey`) to Decrypt Enterprise Secret Stores
* 57.6.3 Forensic Decryption of Protected User Data: Utilizing Extracted DPAPI Keys to Unveil Saved Certificates, Wi-Fi Passwords, RDP Credentials, and Browser Data

#### 57.7 Directory Change Analysis

* 57.7.1 Directory Service Database Reconstruction: Analyzing Metadata Attributes (`whenCreated`, `whenChanged`, `usnCreated`, `usnChanged`) Across Object Lifecycles
* 57.7.2 Uncovering Hidden Attribute Modifications: Identifying Historical Injections in `msDS-AllowedToDelegateTo`, `msDS-KeyCredentialLink`, and `adminCount`
* 57.7.3 Tombstone & Deleted Object Forensics: Restoring and Analyzing Deleted Directory Objects from the Active Directory Recycle Bin and Directory Database Stores

#### 57.8 Replication Artifacts

* 57.8.1 Analyzing Update Sequence Numbers (USNs): Tracking High-Water Mark and Vector Tables Across Domain Controllers to Identify Out-of-Sequence Writes
* 57.8.2 Detecting DCShadow Injections via Metadata: Uncovering Transient Objects, Schema Additions, and Replica Links Deposited During Rogue DC Operations
* 57.8.3 DRSUAPI Log & Packet Analysis: Reconstructing RPC-Level Replication Sessions to Audit Unauthorized Password Hash Pulls (DCSync)

#### 57.9 Group Policy Evidence

* 57.9.1 SYSVOL & GPT Differential Analysis: Comparing SYSVOL Filesystem Timestamps and Version Numbers Against Directory Container (`GPC`) Attributes
* 57.9.2 Forensic Parsing of Policy Artifacts: Extracting Malicious Scheduled Tasks, Immediate Tasks, Registry Settings, and Startup Scripts Deposited in GPOs
* 57.9.3 Tracking GPO Link Modification History: Reconstructing Historical Policy Application Paths Across OUs and Enclaves

#### 57.10 Certificate Evidence

* 57.10.1 AD CS Database (`edb.log` / `certsrv.msc`) Parsing: Carving CA Databases for Issued Certificates, Denied Requests, and Private Key Export Records
* 57.10.2 Forensic Analysis of Compromised Certificates: Extracting Serial Numbers, SAN Extensions, and Issuer Signatures to Track ESC Impersonation Campaigns
* 57.10.3 Tracking Certificate Revocation & KRA Access: Analyzing Audit Logs for Unauthorized Key Recovery Agent (KRA) Requests and Revocation List Disabling

#### 57.11 Federation Evidence

* 57.11.1 AD FS Operational & Tracing Log Analysis: Reconstructing Issued SAML Assertions, Relying Party Invocation, and Claims Transformations
* 57.11.2 Detecting Token-Signing Key Theft Artifacts: Analyzing Access to ADFS Private Keys in Active Directory and HSM Log Trajectories
* 57.11.3 Golden SAML Forensic Reconstruction: Correlating Cloud Application Sign-In Logs Against Missing On-Premises AD FS Issuance Events

#### 57.12 Entra and Cloud Evidence

* 57.12.1 Entra ID Unified Audit Log Parsing: Investigating Cloud Administrative Operations, Service Principal Modifications, and App Registration Key Additions
* 57.12.2 Primary Refresh Token (PRT) & Session Forensics: Analyzing Endpoint PRT Cache Artifacts, Device Claims, and Session Refresh Requests
* 57.12.3 Reconstructing Cross-Tenant Movement: Tracking B2B Guest Ingestion, Cross-Tenant Trust Modifications, and Multi-Tenant App Consent Events

#### 57.13 Authentication Timelines

* 57.13.1 Normalizing Multi-Source Time Structures: Aligning UTC Timestamps Across On-Premises Event Logs, Cloud Diagnostic Logs, and Endpoint Telemetry
* 57.13.2 Super-Timeline Generation for Identity Events: Building Unified Incident Timelines Merging Kerberos TGT/TGS Requests, NTLM Binds, and Web SSO Actions
* 57.13.3 Identifying Gaps & Log Tampering: Spotting Missing Event ID Sequences, Time-Stomping, Event Log Clearing (1102), and Audit Policy Disabling

#### 57.14 Reconstructing Identity Attack Paths

* 57.14.1 Graph-Based Post-Incident Mapping: Overlaying Forensic Discoveries onto BloodHound/Graph Topologies to Visualize Adversary Lateral Paths
* 57.14.2 Validating Initial Access to Domain Escalation: Proving the Step-by-Step Chain from Initial Compromise, Credential Theft, to Tier 0 Takeover
* 57.14.3 Formulating Evidence-Based Remediation Playbooks: Utilizing Confirmed Forensic Findings to Guarantee Elimination of All Persistence Backdoors

#### 58.1 Identity Incident Classification

* 58.1.1 Categorizing Identity Threat Severity: Defining Criteria for Low (Tier 2 User Compromise), Medium (Tier 1 Server/Service Account Compromise), and Critical (Tier 0 Domain/Forest Takeover) Incidents
* 58.1.2 Assessing Control Plane Blast Radius: Mapping Adversary Reach Across On-Premises Active Directory, AD CS, Federation Gateways, and Entra ID Cloud Tenants
* 58.1.3 Establishing Incident Thresholds: Automating Severity Escalations Based on TTP Indicators (e.g., DCSync, Golden SAML, Shadow Credential Creation)

#### 58.2 Initial Triage

* 58.2.1 Rapid Alert Verification & Telemetry Ingestion: Validating SIEM/MDI Alerts Against Domain Controller Event Logs, EDR Signals, and Cloud Sign-In Logs
* 58.2.2 Scoping Identity Blast Radius: Identifying Compromised Principals, Active Logon Sessions, Target Systems, and Exploited Network Segments
* 58.2.3 Preserving Volatile Context: Capturing Active Kerberos Tickets, In-Memory Session Tokens, and Network Socket States Prior to Executing Containment Playbooks

#### 58.3 Account Containment

* 58.3.1 Disabling Standard Compromised Accounts: Automating User Account Disablement (`ACCOUNTDISABLE` Flag) and Setting `userAccountControl` Security Locks
* 58.3.2 Force Password Reset Workflows: Invalidating User Credentials and Enforcing Immediate Password Change Flags Across On-Premises AD and Entra ID
* 58.3.3 Quarantine Group Placement: Dynamically Moving Compromised Accounts to Restricted Access Groups Enforced by Restrictive Network DACLs

#### 58.4 Privileged Account Containment

* 58.4.1 Tier 0 & Privileged Account Quarantine: Executing Emergency Privileged Disablement While Protecting Core Operational Break-Glass Accounts
* 58.4.2 Enforcing Smart Card / MFA Requirement Flags: Enabling `SMARTCARD_REQUIRED` Flags on Privileged Principals to Invalidate NTLM Hashes and Plaintext Passwords
* 58.4.3 Stripping Privileged Group Memberships: Dynamically Removing Compromised Accounts from `Domain Admins`, `Enterprise Admins`, and Custom Shadow Admin Groups

#### 58.5 Session Revocation

* 58.5.1 Active Interactive Session Disconnection: Initiating Remote Terminal Services / RDP Session Logoffs (`logoff.exe`) Across Affected Tier 0/1 Systems
* 58.5.2 SMB & Network Share Session Termination: Flushing Active SMB Connections (`net session /delete`) and Intercepting Open File Handles
* 58.5.3 Purging LSA Logon Sessions: Executing Local Security Authority Session Purges to Invalidated In-Memory Credentials and Impersonation Tokens

#### 58.6 Token Revocation

* 58.6.1 Flushing Kerberos Ticket Caches: Executing `klist purge` across Enclave Endpoints to Evict Stale TGTs and TGSs
* 58.6.2 Invalidating Cloud Refresh Tokens & PRTs: Invoking Entra ID `revokeSignInSessions` Graph APIs to Nullify Primary Refresh Tokens (PRTs) and OAuth Sessions
* 58.6.3 Intercepting Continuous Access Evaluation (CAE): Triggering Real-Time CAE Revocation Events to Terminate Cloud Resource Access Instantly

#### 58.7 Credential Rotation

* 58.7.1 Dual `krbtgt` Password Reset Procedure: Managing the Staged Double-Reset of the Domain `krbtgt` Account Password to Invalidate Golden Tickets
* 58.7.2 Service Account & gMSA Key Rotation: Automating Password and Key Resets for Service Accounts, Managed Service Accounts, and Application Pools
* 58.7.3 Domain Controller Machine Account Resets: Executing Controlled Machine Account Password Resets (`Reset-ComputerMachinePassword`) Over DC Infrastructure

#### 58.8 Certificate Revocation

* 58.8.1 Publishing High-Priority Certificate Revocation Lists (CRLs): Immediately Revoking Compromised Authentication Certificates and Forcing Immediate CRL Updates
* 58.8.2 Disabling Compromised Certificate Templates: Removing Enrollees' Ability to Request Certificates Against Potentially Exploited AD CS Templates
* 58.8.3 Certification Authority Private Key Protection: Securing CA Hardware Security Modules (HSMs) and Disabling Insecure Web Enrollment (CES/CES) Endpoints

#### 58.9 Tier 0 Isolation

* 58.9.1 Severing Domain Controller Network Access: Applying Automated Host-Based Firewall Rules to Isolate Compromised DCs to Essential Replication Ports Only
* 58.9.2 Locking Down Privileged Access Workstations (PAWs): Terminating Remote Administrative Access to PAWs and Re-enforcing Strict IPsec Tunneling
* 58.9.3 Segmenting Out-of-Band Management Interfaces: Isolating iLO/iDRAC and Virtualization Hypervisors from Compromised Corporate Network Segments

#### 58.10 Federation Containment

* 58.10.1 Breaking AD FS Relying Party Trusts: Temporarily Disabling Affected Federation Trusts to Prevent Cross-Boundary Impersonation into Cloud Systems
* 58.10.2 Emergency Token-Signing Certificate Rollover: Generating New AD FS Token-Signing Certificates to Render Forged SAML Tokens Ineffective
* 58.10.3 Restricting Web Application Proxy (WAP) Traffic: Blocking Inbound Federated Authentication Traffic at Perimeter WAP Gateways

#### 58.11 Hybrid Identity Containment

* 58.11.1 Pausing Entra Connect / Cloud Sync Synchronization: Stopping the Sync Engine (`Start-ADSyncSyncCycle -PolicyType Delta` Pause) to Prevent On-Premises Attack Persistence from Syncing to Cloud
* 58.11.2 Disabling Cloud Writeback Interfaces: Severing Password Writeback and Device Writeback Channels to Protect On-Premises AD from Cloud-Origin Attacks
* 58.11.3 Quarantining Staging & Sync Servers: Isolating Entra Connect Servers to Prevent LSASS Credential Harvesting and Key Theft

#### 58.12 Evidence Preservation

* 58.12.1 Capturing Forensic Images Before Disablement: Automating Memory and Disk Artifact Collection Prior to Executing Destructive Account/Session Resets
* 58.12.2 Offloading Directory Security Event Logs: Forwarding Active Directory Security Logs, CA Logs, and ADFS Operational Logs to WORM (Write-Once-Read-Many) Storage
* 58.12.3 Exporting Directory State Snapshots: Taking Offline Snapshots of `NTDS.dit` and Configuration Partitions to Support Post-Incident Forensic Reconstruction

#### 58.13 SOAR-Assisted Containment

* 58.13.1 Building Automated Identity Response Playbooks: Constructing Orchestrated Workflows Integrating SIEM, EDR, Active Directory, and Entra ID APIs
* 58.13.2 Implementing Operational Safety Guardrails: Injecting Human-in-the-Loop Approval Checks for Destructive Containment Actions (e.g., Domain-Wide `krbtgt` Reset)
* 58.13.3 API Rate Limiting & Fail-Safe Mechanisms: Ensuring Automated Containment Playbooks Do Not Trigger Self-Inflicted Denial-of-Service During Mass Incident Outbreaks

#### 58.14 Mission Coordination

* 58.14.1 Out-of-Band (OOB) Communications: Establishing Secure, Non-Federated Communication Channels (e.g., Out-of-Band Signal/Email) Unreachable by AD Adversaries
* 58.14.2 Operational Security (OpSec) During Remediation: Executing Containment Actions in Synchronized Waves to Prevent Adversaries from Detecting Countermeasures Early
* 58.14.3 Coordinating Cross-Functional Enclave Teams: Aligning Identity Engineers, SOC Analysts, Forensics Teams, and Executive Leadership During Crisis Operations

#### 58.15 Communications and Escalation

* 58.15.1 Regulatory & Federal Reporting Timelines: Fulfilling CISA, FedCIRC, DoD CIO, or HIPAA Mandatory Incident Reporting Deadlines Within Required Windows
* 58.15.2 Leadership & CISO Briefings: Translating Technical Identity Telemetry into Operational Impact Statements, Root Causes, and Remediation Roadmaps
* 58.15.3 Public & Partner Disclosure Protocols: Managing External Incident Notification Channels While Preserving Operational Security Integrity

#### 58.16 After-Action Review

* 58.16.1 Post-Incident Root-Cause Analysis (RCA): Conducting Formal Technical Reviews to Identify Initial Access Vectors, Control Plane Gaps, and Detection Latencies
* 58.16.2 Updating Detection & Response Baselines: Translating Discovered Adversary TTPs into New SIEM Rules, MDI Detections, and SOAR Playbooks
* 58.16.3 Refining FICAM Architecture & Control Plane Controls: Updating Security Architecture Baselines, GPO Configurations, and Zero Trust Policies Based on Lessons Learned

#### 59.1 Identity Service Resilience

* 59.1.1 Authentication Availability: Architecting High-Availability Active Directory and Entra ID Enclaves to Withstand Partial Domain Controller Loss
* 59.1.2 Degraded Operations: Defining Reduced-Functionality Operational Modes to Maintain Core Authentication During Identity Control Plane Stress
* 59.1.3 Disconnected Operations: Designing Tactical and Offline Authentication Capabilities Utilizing Local Caching and PKI Tokens During WAN Partitioning
* 59.1.4 COOP (Continuity of Operations): Aligning Identity Infrastructure Recovery Procedures with Federal COOP Directives and Critical Asset Priorities
* 59.1.5 Dependency Mapping: Documenting Inter-Service Dependencies (DNS, DHCP, PKI, KMS, Hypervisors) Required for Sequential Identity Service Bootstrapping
* 59.1.6 Protected Backups: Securing Bare-Metal, System State, and `NTDS.dit` Backups Using Immutable Storage, Cryptographic Signing, and Air-Gapping
* 59.1.7 Recovery Readiness: Conducting Periodic Active Directory Disaster Recovery (ADDR) Tabletop Exercises and Forest Recovery Simulations

#### 59.2 KRBTGT Recovery

* 59.2.1 Determining Whether KRBTGT Is Compromised: Establishing Indicators of Compromise (IoCs) Requiring Immediate Emergency `krbtgt` Account Key Rotation
* 59.2.2 First KRBTGT Reset: Executing the Initial Password Reset of the Domain `krbtgt` Account to Retain Historical Key Material for Valid Sessions
* 59.2.3 Replication Validation: Verifying Active Directory Replication Topology Across All Domain Controllers to Guarantee Complete First-Key Distribution
* 59.2.4 Second KRBTGT Reset: Initiating the Second `krbtgt` Reset After Ticket Lifetime Expiration (`MaxTicketAge`) to Completely Purge the Compromised Key
* 59.2.5 Ticket Invalidation: Monitoring Domain Logs to Confirm Mass Invalidation of Pre-Existing Kerberos Ticket Granting Tickets (TGTs)
* 59.2.6 Key-Version Transition: Tracking Key Version Number (`msDS-KeyVersionNumber` / `kvno`) Increments Across Domain Controllers

#### 59.3 Tier 0 Forest Recovery

* 59.3.1 Administrative Clean Room: Constructing an Isolated, Secure Enclave Network Free from Adversary Persistence to Rebuild Forest Operations
* 59.3.2 Domain Controller Rebuild: Provisioning Fresh Domain Controller Operating Systems from Verified, Hardened Media (STIG-Compliant)
* 59.3.3 Authoritative Restore: Performing Authoritative Database Restores over Specific Tier 0 Containers (`OU=Domain Controllers`, `CN=Configuration`)
* 59.3.4 Non-Authoritative Restore: Re-seeding Secondary Domain Controllers in the Clean Room Environment via Standard Inbound DRS Replication
* 59.3.5 Privileged Credential Renewal: Resetting Passwords and Keys for All Domain Admins, Enterprise Admins, Service Accounts, and Machine Accounts
* 59.3.6 Replication Revalidation: Auditing Metadata, USN Ranges, and Vector Tables to Ensure Replication Integrity across Rebuilt DCs
* 59.3.7 Trust Reconstitution: Re-establishing Inter-Forest, External, and Shortcut Trusts with Reset Passwords and Re-validated SID Filtering

#### 59.4 PKI Recovery

* 59.4.1 CA Recovery: Restoring Root and Subordinate Certification Authorities (AD CS) from Clean System State and HSM Key Backups
* 59.4.2 Key Renewal: Generating New Private Keys for Root and Issuing CAs Following Key Material Compromise or Exfiltration
* 59.4.3 Certificate Revocation: Issuing Immediate Emergency Revocation Commands for Compromised Domain Certificates and Publishing Updated CRLs
* 59.4.4 Certificate Reissuance: Systematically Re-issuing Authentication Certificates to Domain Controllers, Smart Cards, and Critical Infrastructure
* 59.4.5 Trust-Anchor Validation: Verifying and Redeploying Root CA Certificates and NTAuth Certificate Stores Across All Domain Endpoints

#### 59.5 Federation Recovery

* 59.5.1 AD FS Recovery: Rebuilding Active Directory Federation Services Farm Servers from Known-Good States in the Isolated Enclave
* 59.5.2 Token-Signing Key Replacement: Generating New Token-Signing and Token-Decrypting Certificates in AD FS to Invalidate Forged SAML Tokens
* 59.5.3 Relying-Party Revalidation: Re-exporting Federation Metadata and Re-establishing Trust Endpoints Across All Enterprise Relying Party Applications
* 59.5.4 Partner Trust Revalidation: Re-anchoring B2B External Identity Provider Trusts with Verified Cryptographic Key Material

#### 59.6 Hybrid and Cloud Recovery

* 59.6.1 Entra Session Revocation: Executing Tenant-Wide Revocation of Interactive Sign-In Sessions, Refresh Tokens, and Continuous Access Evaluation (CAE) Tokens
* 59.6.2 Synchronization Recovery: Re-installing and Hardening Microsoft Entra Connect / Cloud Sync Servers with Reset Service Account Credentials
* 59.6.3 Service Principal Credential Rotation: Purging and Rotating All Client Secrets, Certificates, and Federated Identity Credentials on Cloud Applications
* 59.6.4 Application Credential Rotation: Re-securing Managed Identities, OAuth Application Keys, and High-Privilege API Connections in Azure/Entra
* 59.6.5 Cross-Tenant Trust Validation: Auditing and Re-confirming B2B Collaboration Settings, Cross-Tenant Access Policies, and Inbound/Outbound Direct Trusts

#### 59.7 Proving That Identity Trust Has Been Restored

* 59.7.1 Post-Restoration Integrity Auditing: Running Comprehensive Graph Differential Sweeps, DACL Audits, and MDI Scans to Confirm Zero Persistence Left
* 59.7.2 Cryptographic Evidence Validation: Verifying CRL Publish Times, OCSP Responder Freshness, and `kvno` Uniformity Across All Forest Enclaves
* 59.7.3 Formal Attestation & Re-entry Sign-off: Compiling Forensic Verification Reports and Securing CISO/DAO Executive Approval to Reconnect Control Plane Operations

#### 60.1 Why Identity Programs Fail in Production

* 60.1.1 The Illusion of Deployment Completion: Examining Why Installing an Identity Management Product or Deploying MFA Does Not Equal Operational Security
* 60.1.2 Complexity vs. Maintainability: Analyzing How Over-Engineered Custom Integrations Outpace Internal Engineering Maintenance Capacity
* 60.1.3 Drift from Baseline: Mapping the Inevitable Degradation of Initial Security Deployments Under Day-to-Day Operational Pressure

#### 60.2 Configuration Drift

* 60.2.1 Unaudited Manual Overrides: Documenting How Emergency "Temporary" Changes Become Permanent Production Vulnerabilities
* 60.2.2 GPO and Policy Drift: Tracking Divergences Between Stated Security Baselines and Active Domain Controller Configurations
* 60.2.3 Automated Drift Detection & Enforcement: Implementing Continuous Compliance Guardrails Using Configuration-as-Code and Desired State Configuration (DSC)

#### 60.3 Documentation Failure

* 60.3.1 The Tribal Knowledge Trap: Risks Associated with Relying on Undocumented Active Directory Topologies and Custom Scripts
* 60.3.2 Architecture-to-Reality Gaps: Addressing Outdated Network Diagrams, Schema Extensions, and Unmapped Trust Relationships
* 60.3.3 Enforcing Documentation-as-Code: Mandating Version-Controlled Infrastructure Documentation Alongside Code Releases

#### 60.4 Contractor and Personnel Turnover

* 60.4.1 Offboarding Blind Spots: Managing Privileged Access Lifecycles and Shared Credentials Across External Contractors
* 60.4.2 Loss of Institutional Context: Mitigating the Impact of Senior Security Engineer Departure on Enclave Resilience
* 60.4.3 Automated Access Reviews: Implementing Rigorous Periodic Attestations to Prevent Privilege Creep

#### 60.5 Service Account Sprawl

* 60.5.1 Unmonitored Non-Human Identities: Auditing Proliferating Service Accounts Lacking Password Rotation and Expiration Policies
* 60.5.2 Legacy Account Dependencies: Untangling Hardcoded Passwords in Legacy Applications Tied to Tier 0 Service Principals
* 60.5.3 Transition to Group Managed Service Accounts (gMSA): Enforcing Native Automatic Password Management Across Enterprise Services

#### 60.6 PKI Ownership Failure

* 60.6.1 Orphaned Certificate Authorities: Identifying Unowned or Unpatched AD CS Environments Operating Without Security Oversight
* 60.6.2 Key Management Abandonment: Managing Expired Root Keys, Lost HSM Backups, and Unmonitored Enrollment Endpoints
* 60.6.3 Establishing PKI Governance: Defining Clear Operational Ownership Between Enterprise IT, Security, and Cryptographic Teams

#### 60.7 Federation Ownership Failure

* 60.7.1 The AD FS / IdP Blind Spot: Addressing Divided Responsibilities Between On-Premises Infrastructure and Cloud Identity Teams
* 60.7.2 Abandoned Relying Party Trusts: Auditing Legacy External Partner Integrations Left Active After Contract Termination
* 60.7.3 Unified Federation Governance: Consolidating Single Sign-On (SSO) Lifecycles Under a Singular Identity Security Authority

#### 60.8 Hybrid Identity Ownership Failure

* 60.8.1 The On-Premises vs. Cloud Divide: Resolving Security Ownership Ambiguities Across Hybrid Boundaries (AD to Entra ID)
* 60.8.2 Synchronization Boundary Failures: Managing Configuration Drift and Security Misalignments on Entra Connect / Cloud Sync Servers
* 60.8.3 Integrated Hybrid Operations: Unifying Incident Response and Change Management Across Both Control Planes

#### 60.9 SOC and Identity-Team Disconnect

* 60.9.1 Siloed Domain Knowledge: Bridging the Gap Between Enterprise AD Administrators Who Don't Do Detection and SOC Analysts Who Don't Understand AD Internals
* 60.9.2 Alert Relevance & Tuning Failures: Training SOC Personnel on High-Fidelity Identity TTPs Beyond Generic Event Log Alerts
* 60.9.3 Joint Response Protocols: Integrating Identity Engineers Directly into High-Severity Security Incident Response Cells

#### 60.10 Alert Fatigue

* 60.10.1 The Cost of High False-Positive Rates: Analyzing How Ignored Security Warnings Enable Dwell Time for Real Attackers
* 60.10.2 Noise Reduction Strategies: Tuning Thresholds, Leveraging Behavioral Baselines, and Enriching Telemetry Context
* 60.10.3 Prioritizing Actionable Signals: Shifting Focus from Volume-Based Detections to High-Confidence Identity Exploit Indicators

#### 60.11 Recovery Assumption Failures

* 60.11.1 Untested Disaster Recovery Plans: Exposing Flaws in Backup Restoration Strategies That Assume Clean Active Directory States
* 60.11.2 Reintroducing Backdoors via Restore: Examining How Restoring Compromised System States Rebuilds Adversary Persistence
* 60.11.3 Mandatory Clean-Room Validation: Enforcing Isolated Recovery and Air-Gapped Restoration Protocols

#### 60.12 Identity Ownership Ambiguity

* 60.12.1 The "Not My Job" Dilemma: Addressing Security Gaps Occurring When Identity Spans Multiple Organizational Silos
* 60.12.2 Defining Control Plane Accountability: Establishing Executive Sponsorship and Clear Operational Ownership for Tier 0 Assets
* 60.12.3 Cross-Functional Governance Frameworks: Aligning Identity Engineering, Compliance, and Defense Operations

#### 60.13 Lessons for the Engineer Inheriting an Existing Environment

* 60.13.1 Triage and Discovery First: Conducting Comprehensive BloodHound, LDAP, and PKI Sweeps Before Making Structural Changes
* 60.13.2 Mapping Hidden Technical Debt: Identifying Legacy Trusts, Unpatched Vulnerabilities, and Undocumented Admin SIDs
* 60.13.3 Stabilizing Before Hardening: Prioritizing Foundational Integrity and Logging Visibility Over Aggressive Policy Changes That Break Production

#### 60.14 Operational Judgment

* 60.14.1 Balancing Security vs. Mission Availability: Navigating the Tension Between Absolute Control Plane Lockdown and Operational Velocity
* 60.14.2 Risk-Based Decision Making: Applying Pragmatic Mitigations When Perfect Architectural Remediation is Impractical
* 60.14.3 Crisis Leadership in Identity: Maintaining Clear Communication and Methodical Execution During High-Pressure Domain Incidents

#### 60.15 Identity Threat Detection and Response

* 60.15.1 Evolution of ITDR: Moving Beyond Endpoint Detection to Monitor Identity Control Plane Native Protocols
* 60.15.2 Protocol-Level Visibility: Integrating Deep Packet Inspection, ETW, and Cloud Log Streams into Unified Detection Pipelines
* 60.15.3 Automated Response Integration: Connecting ITDR Insights Directly with SOAR Playbooks for Sub-Second Containment

#### 60.16 Identity Exposure Management

* 60.16.1 Continuous Attack Path Mapping: Proactively Identifying Vulnerable ACLs, Delegations, and Trust Misconfigurations Before Exploitation
* 60.16.2 Prioritizing Remediation Efforts: Focusing Engineering Resources on High-Value Tier 0 Exposure Nodes
* 60.16.3 Measuring Identity Posture: Establishing Quantitative Metrics for Enterprise Identity Risk and Attack Surface Reduction

#### 60.17 Machine-Identity Security

* 60.17.1 The Explosion of Non-Human Principals: Securing API Keys, Secrets, Certificates, and Managed Identities at Scale
* 60.17.2 Lifecycle Management for Machine Workloads: Automating Rotation and Revocation for Application-to-Application Credentials
* 60.17.3 Detecting Non-Human Compromise: Monitoring Anomalous API Usage and Lateral Movement by Automated Service Principals

#### 60.18 AI-Assisted Identity Attacks

* 60.18.1 AI-Assisted Reconnaissance: Leveraging LLMs to Automate OSINT, Map Attack Surfaces, and Parse Complex Directory Structures
* 60.18.2 Automated Attack-Path Discovery: Using Machine Learning to Dynamically Identify and Chain Novel Privilege Escalation Paths
* 60.18.3 AI-Assisted Phishing and Social Engineering: Countering Hyper-Realistic, Context-Aware Credential Harvesting Campaigns
* 60.18.4 Synthetic Identity and Impersonation Threats: Defending Against AI-Generated Deepfakes and Synthetic Biometrics in Remote Verification

#### 60.19 AI-Assisted Identity Defense

* 60.19.1 Detection Enrichment: Utilizing AI to Correlate Fragmented Identity Telemetry and Reduce Investigation Triage Times
* 60.19.2 Behavioral Analysis: Deploying Machine Learning Baselines to Detect Subtle, Low-and-Slow Anomalous Principal Behavior
* 60.19.3 Automated Exposure Prioritization: Using Intelligent Graph Modeling to Highlight Critical Attack Paths for Immediate Remediation
* 60.19.4 Response Orchestration: Leveraging Autonomous Agents to Execute Containment Workbooks Safely at Scale

#### 60.20 Passwordless Identity

* 60.20.1 Eliminating the Primary Human Weakness: Transitioning Away from Phishable Passwords and Shared Secrets
* 60.20.2 Enterprise Adoption Challenges: Balancing User Experience with High-Assurance Hardware Security Requirements
* 60.20.3 Fallback Mechanics: Securing Recovery Paths Without Reintroducing Vulnerable Legacy Authentication Channels

#### 60.21 Passkeys and FIDO2

* 60.21.1 Cryptographic Authentication Mechanics: Understanding Public-Key Credentials Bound to Hardware Authenticators
* 60.21.2 Phishing-Resistance Guarantees: Enforcing Origin-Bound Signatures That Render Man-in-the-Middle Relay Attacks Obsolete
* 60.21.3 Enterprise Deployment Strategies: Integrating FIDO2 Passkeys Across Hybrid Active Directory and Cloud Environments

#### 60.22 Adaptive Authentication

* 60.22.1 Context-Aware Access Policies: Dynamically Adjusting Authentication Requirements Based on Risk, Location, and Device Posture
* 60.22.2 Real-Time Risk Scoring: Integrating Threat Intelligence and Behavioral Telemetry Into Access Decision Gates
* 60.22.3 Balancing Friction and Security: Minimizing Authentication Prompts for Trusted Users While Challenging Anomalous Sessions

#### 60.23 Continuous Access Evaluation

* 60.23.1 Beyond Point-in-Time Authentication: Enforcing Real-Time Revocation of Access Tokens Based on Policy Changes
* 60.23.2 Instantaneous Session Termination: Utilizing CAE to Drop Compromised Sessions Within Seconds of Threat Detection
* 60.23.3 Hybrid Implementation Challenges: Extending Continuous Evaluation from Cloud Enclaves down to On-Premises Domain Controllers

#### 60.24 Cryptographic Agility

* 60.24.1 Designing for Algorithmic Transition: Building Identity Infrastructures Capable of Swapping Underlying Cryptographic Primitives
* 60.24.2 Inventorying Cryptographic Assets: Cataloging All Algorithms, Key Sizes, and X.509 Certificates Across Enterprise Enclaves
* 60.24.3 Avoiding Vendor Lock-In: Ensuring Software and Hardware Security Module (HSM) Interoperability Across Identity Platforms

#### 60.25 Post-Quantum Identity Infrastructure

* 60.25.1 The Quantum Threat Model: Understanding Shor's Algorithm and the "Harvest Now, Decrypt Later" Risk to Long-Lived Identity Secrets
* 60.25.2 NIST PQC Standardization: Implementing FIPS-approved post-quantum algorithms—including ML-KEM for key encapsulation and ML-DSA for digital signatures
* 60.25.3 Hardening Active Directory and PKI: Migrating Domain Controllers, Kerberos encryption types, and AD CS certificate templates to quantum-resistant standards before regulatory deadlines

#### 60.26 Zero Trust Modernization

* 60.26.1 Implementing CISA Zero Trust Pillars: Aligning Identity, Devices, Networks, Applications, and Data into a Cohesive Defense Architecture
* 60.26.2 Eradicating Implicit Trust: Replacing Perimeter-Based Security Models with Continuous Explicit Verification
* 60.26.3 Measuring Maturity Progress: Utilizing Maturity Models to Track Advancements from Traditional Enclaves to Optimal Zero Trust Operations

#### 60.27 Future Federal and DoD ICAM

* 60.27.1 FICAM Evolution: Adapting Federal Identity Mandates to Distributed, Multi-Cloud, and Edge Operational Environments
* 60.27.2 Tactical Identity Architecture: Securing Disconnected, Intermittent, and Low-Bandwidth Military Enclaves
* 60.27.3 Interoperability and Standards: Unifying Identity Credentials Across Coalition Partners and Joint Federal Agencies

#### 60.28 Identity-Centric Warfare

* 60.28.1 The Control Plane as Primary Battlefield: Recognizing That Modern Adversaries Target Identity Infrastructure Rather Than Forcing Network Perimeters
* 60.28.2 Contested Identity Environments: Operating and Defending Identity Services Under Active State-Sponsored Cyber Warfare
* 60.28.3 Offensive Identity Defense: Utilizing Deception, Active Hunting, and Rapid Reconstitution to Dominate the Control Plane

#### 60.29 Building Resilient Identity Infrastructure

* 60.29.1 Engineering Principles for Domain Survivability: Designing Fault-Tolerant, Highly Monitored, and Immutable Identity Silos
* 60.29.2 Redundancy and Air-Gapping: Protecting Core Tier 0 Backups and Recovery Assets Against Catastrophic Destruction
* 60.29.3 Continuous Validation: Institutionalizing Regular Disaster Recovery Drills, Red Teaming, and Automated Posture Assessments

#### 60.30 Final Operational Lessons

* 60.30.1 Identity is Security: Reaffirming That Protecting the Identity Control Plane is the Ultimate Determinant of Enterprise Survival
* 60.30.2 The Immutable Rule of Least Privilege: Enforcing Strict, Unyielding Access Controls Across Every User, Machine, and Cloud Workload
* 60.30.3 The Enduring Mandate: Maintaining Vigilance, Technical Depth, and Engineering Discipline in the Ever-Evolving Landscape of Identity Warfare

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













