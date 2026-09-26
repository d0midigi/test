# Chapter 4 - The Federal Identity Trust System - Boundaries, Dependencies, and Mission Authority

### Abstract&#xD;

Federal identity trust extends far beyond the Active Directory domain. Authentication, authorization, credential issuance, federation, synchronization, privileged administration, device identity, cloud services, virtualization, backup, recovery, and authoritative data sources collectively determine which systems and principals can establish or effectively alter trusting and trusted entities. Chapter 4 develops the federal identity trust system as a security model for understanding those dependencies. Rather than relying on product boundaries, network diagrams, or administrative titles, readers learn to identify effective authority: which components can create identities, issue credentials, modify trusted attributes, impersonate principals, administer Tier 0 systems, restore compromised infrastructure, or cause another system to accept an assertion as valid. Particular attention is given to trusted-core infrastructure, clean0source administration, certificate and federation trust, synchronization, mission-partner and cross-domain identity, contractor-operated services, hidden administrative dependencies, and recovery systems. The chapter concludes by showing how trust relationships become attack pathways and how defenders can map, tier, monitor, constrain, and ultimately reestablish trust following identity control-plane compromise.

### <mark style="color:$warning;">4.1 From Active Directory Domain to Identity Trust System</mark>&#xD;

* 4.1.1 The Domain Is Not the Entire Identity Boundary
* 4.1.2 Product Boundaries and Security Boundaries Are Different
* 4.1.3 Authentication Boundaries Can Extend Beyond Directory Boundaries
* 4.1.4 Administrative Boundaries Can Differ From Authentication Boundaries
* 4.1.5 Authorization Boundaries Can Differ From Both
* 4.1.6 Trust Can Cross Cloud, On-Premises, and Mission-Partner Environments
* 4.1.7 Effective Authority Defines the Real Security Boundary
* 4.1.8 The Identity Trust System Is the Effective Control Plane

### <mark style="color:$warning;">4.2 Why Identity Infrastructure Is Mission Infrastructure</mark>&#xD;

* 4.2.1 Authentication Availability Becomes Service Availability
* 4.2.2 Directory Integrity Becomes Mission-Relevant Integrity
* 4.2.3 Authorization Integrity Determines Who or What Can Act
* 4.2.4 Credential Issuance Determines Who or What Can Authenticate
* 4.2.5 Identity Supports Both Mission Users and Mission Administrators
* 4.2.6 Compromise of Identity Can Bypass an Otherwise Secure Application
* 4.2.7 Identity Recovery Determines Whether Mission Trust Can Be Restored
* 4.2.8 Identity Belongs in the Mission Dependency Map

### <mark style="color:$warning;">4.3 Trust Must Be Evaluated by Function Rather Than by Product Name</mark>&#xD;

* 4.3.1 Identity Authority
* 4.3.2 Authentication Authority
* 4.3.3 Credential Authority
* 4.3.4 Authorization Authority
* 4.3.5 Administrative Authority
* 4.3.6 Configuration Authority
* 4.3.7 Recovery Authority
* 4.3.8 Any System Exercising These Functions Can Become Security-Critical

### <mark style="color:$warning;">4.4 Components of the Federal Identity Trust System</mark>&#xD;

* 4.4.1 Active Directory Domain Services (AD DS)
* 4.4.2 Public Key Infrastructure (PKI) and Active Directory Certificate Services (AD CS)
* 4.4.3 Federation Infrastructure and Identity Providers (IdP)
* 4.4.4 Microsoft Entra ID and Cloud Identity
* 4.4.5 Identity Synchronization and Provisioning Platforms
* 4.4.6 Privileged Access Infrastructure
* 4.4.7 Authoritative Identity Sources
* 4.4.8 Device, Application, Service, and Workload Identity
* 4.4.9 Identity Governance Platforms
* 4.4.10 Backup, Recovery, Virtualization, and Administrative Management Infrastructure

### <mark style="color:$warning;">4.5 Authority Flows Through Dependencies</mark>&#xD;

* 4.5.1 Direct Authority
* 4.5.2 Indirect Authority
* 4.5.3 Transitive Authority
* 4.5.4 Authority Through Credential Access
* 4.5.5 Authority Through Configuration
* 4.5.6 Authority Through Software Deployment
* 4.5.7 Authority Through Backup and Recovery
* 4.5.8 Authority Must Be Evaluated by Maximum Reach

### <mark style="color:$warning;">4.6 Effective Authority Matters More Than Administrative Labels</mark>&#xD;

* 4.6.1 Formal Administrators
* 4.6.2 Delegated Administrators
* 4.6.3 Hidden Administrators
* 4.6.4 Service and Automation Principals
* 4.6.5 Certificate-Issuance Authority
* 4.6.6 Password-Reset and Recovery Authority
* 4.6.7 Management-Plane Authority
* 4.6.8 What a Principal Can Cause to Happen Is the Relevant Security Question

### <mark style="color:$warning;">4.7 The Trusted Core Extends Beyond Domain Controllers</mark>&#xD;

* 4.7.1 Domain Controllers (DC)
* 4.7.2 Certification Authorities (CA)
* 4.7.3 Federation Signing Infrastructure
* 4.7.4 Identity Synchronization Systems
* 4.7.5 Privileged Access Platforms
* 4.7.6 Hypervisors and Virtualization Management
* 4.7.7 Backup and Recovery Systems
* 4.7.8 Endpoint and Configuration Management
* 4.7.9 Security Management Infrastructure
* 4.7.10 Automation and Orchestration Platforms

### <mark style="color:$warning;">4.8 Tier 0 Is a Relationship, Not a List of Servers</mark>&#xD;

* 4.8.1 Direct Tier 0 Assets
* 4.8.2 Systems That Administer Tier 0
* 4.8.3 Systems That Can Execute Code on Tier 0
* 4.8.4 Systems That Store Tier 0 Credentials
* 4.8.5 Systems That Can Restore Tier 0
* 4.8.6 Systems That Can Issue Tier 0 Authentication Material
* 4.8.7 Systems That Can Change Tier 0 Authorization
* 4.8.8 Hidden Tier 0 Must Be Discovered Through Dependency Analysis

### <mark style="color:$warning;">4.9 The Clean Source Principal</mark>&#xD;

* 4.9.1 A System Cannot Be Safely Administered From a Less-Trusted System
* 4.9.2 Administrative Dependencies Inherit the Target's Security Tier
* 4.9.3 Credential Entry Creates a Trust Relationship
* 4.9.4 Management Sessions Create a Trust Relationship
* 4.9.5 Software Supply and Deployment Pathways That Matter
* 4.9.6 Administrative Tooling Must Also Be Trusted
* 4.9.7 Recovery Sources Must Be and Remain Clean
* 4.9.8 Trust Reconstitution Requires a Known-Good Administrative Origin

### <mark style="color:$warning;">4.10 Identity Trust Versus Network Trust</mark>&#xD;

* 4.10.1 Network Location Is Not Proof of Identity
* 4.10.2 Internal Does Not Mean Trusted
* 4.10.3 Authentication Is Not Proof of Device Integrity 4.10.4 Device Trust Is Not User Trust
* 4.10.5 User Trust Is Not Application Trust
* 4.10.6 Network Segmentation Does Not Replace Identity Segmentation
* 4.10.7 Identity Trust Is Contextual
* 4.10.8 Trust Must Be Evaluated Per Access Decision

### <mark style="color:$warning;">4.11 Identity Trust Versus Administrative Trust</mark>&#xD;

* 4.11.1 Recognizing an Identity Does Not Grant Administrative Authority
* 4.11.2 Administration Can Exist Without Interactive Logon
* 4.11.3 Application Programming Interfaces (API) Permissions Can Represent Administrative Authority
* 4.11.4 Service Principals Can Hold Administrative Authority
* 4.11.5 Certificates Can Convey Administrative Authority
* 4.11.6 Delegation Can Convey Administrative Authority
* 4.11.7 Ownership and Access Control Lists (ACL) Can Create Hidden Administration
* 4.11.8 Administrative Trust Must Be Mapped Separately From Authentication Trust

### <mark style="color:$warning;">4.12 Authoritative Identity and Attribute Trust</mark>&#xD;

* 4.12.1 Every Identity Fact Has An Origin
* 4.12.2 Authoritative Does Not Mean Authoritative For Everything
* 4.12.3 Attribute Provenance Is a Security Property
* 4.12.4 Attribute Modification Rights are Security-Relevant
* 4.12.5 Attribute Manipulation Can Become Privilege Escalation
* 4.12.6 Synchronization Does Not Create Independent Authority
* 4.12.7 Conflicting Authorities Create Identity Ambiguity
* 4.12.8 Consumers Must Know Which Source They Actually Trust

### <mark style="color:$warning;">4.13 Identity Synchronization Is a Trust Boundary</mark>&#xD;

* 4.13.1 Synchronization Is More Than Just Data Movement
* 4.13.2 On-Premises-to-Cloud Authority
* 4.13.3 Cloud-to-On-Premises Authority
* 4.13.4 Writeback Creates Reverse Trust Pathways
* 4.13.5 Synchronization Account Are High-Value Principals
* 4.13.6 Scoping and Transformation Rules Affect Security
* 4.13.7 Staging and Recovery Systems Preserve Privileged Capability 4.13.8 Synchronization Failure Can Become Mission Failure

### <mark style="color:$warning;">4.14 Credential Trust</mark>&#xD;

* 4.14.1 Identity and Credential Are Different Concepts
* 4.14.2 Credential Strength Does Not Repair Excessive Authority
* 4.14.3 Credential Issuance Is a Trust Decision
* 4.14.4 Credential Binding Is a Trust Decision
* 4.14.5 Authentication Method Affects Trust Strength
* 4.14.6 Credential Recovery Is Part of the Trust Model
* 4.14.7 Credential Revocation Must Match Credential Diversity
* 4.14.8 Password Rotation Alone Does Not Revoke All Identity Authority

### <mark style="color:$warning;">4.15 Certificate Trust Within the Identity Trust System</mark>&#xD;

* 4.15.1 Certificates Can Represent Users, Devices, Services, and Applications
* 4.15.2 Certification Authorities Determine Which Credentials Can Exist
* 4.15.3 Certificate Templates and Enrollment Policy Shape Identity Authority
* 4.15.4 Trust Stores Become Security Boundaries
* 4.15.5 NTAuth and Certificate Mappings Affect Authentication
* 4.15.6 Private Keys Represent Persistent Authority
* 4.15.7 Revocation Infrastructure Is an Operational Dependency
* 4.15.8 PKI Compromise Can Become Identity Control-Plane Compromise

### <mark style="color:$warning;">4.16 Federation Is Distributed Identity Authority</mark>&#xD;

* 4.16.1 Federation Separates Authentication From the Resource
* 4.16.2 Identity Providers Become Upstream Authorities
* 4.16.3 Relying Parties (RP) Delegate Authentication Decisions
* 4.16.4 Signing Keys Become Identity Authority
* 4.16.5 Claims Carry Security-Relevant Meaning
* 4.16.6 Federation Trust Must Be Scoped
* 4.16.7 Authentication Assurance Must Survive Federation
* 4.16.8 Federation Failure and Compromise Have Multi-System Consequence

### <mark style="color:$warning;">4.17 Cloud and Hybrid Identity Exposure and the Trust Graph</mark>&#xD;

* 4.17.1 Cloud Roles
* 4.17.2 Service Principals
* 4.17.3 Managed Identities
* 4.17.4 Device Registrations
* 4.17.5 Conditional Access
* 4.17.6 Cloud Applications
* 4.17.7 Hybrid Identity Bridges
* 4.17.8 Compromise Can Propagate in Either Direction (Upstream/Downstream)

### <mark style="color:$warning;">4.18 Person and Non-Person Entities (NPE) Require Different Trust Models</mark>&#xD;

* 4.18.1 Human Users (Person Entities)
* 4.18.2 Privileged Person Entities
* 4.18.3 Devices
* 4.18.4 Service Accounts
* 4.18.5 Applications and Service Principals

### <mark style="color:$warning;">4.19 Privileged Access Infrastructure Becomes an Identity Broker</mark>&#xD;

* 4.19.1 Password Vaults
* 4.19.2 Privileged Session Brokers
* 4.19.3 Jump Hosts and Bastions
* 4.19.4 PAWS/SAWS - Privileged Access Workstations and Secure Administrative Workstations
* 4.19.5 Just-In-Time (JIT) Privilege
* 4.19.6 Credential Rotation
* 4.19.7 Break-Glass Accounts and Access
* 4.19.8 Compromise of the Broker Can Aggregate Otherwise Separated Authority

### <mark style="color:$warning;">4.20 Management, Virtualization, and Recovery Systems Extend the Trust Boundary</mark>&#xD;

* 4.20.1 Endpoint Management
* 4.20.2 Software Deployment
* 4.20.3 Configuration Management
* 4.20.4 Hypervisor Administration
* 4.20.5 Snapshot and Virtual Disk Access
* 4.20.6 Backup Administration
* 4.20.7 Recovery Orchestration
* 4.20.8 Infrastructure Beneath Identity Systems Can Be as Important as Identity Systems Themselves

### <mark style="color:$warning;">4.21 Federal and Department of Defense (DoD) Enclaves Change the Operating Context</mark>&#xD;

* 4.21.1 NIPRNet
* 4.21.2 SIPRNet
* 4.21.3 JWICS and Other National Security Systems (NSS)
* 4.21.4 Enterprise Versus Tactical Identity
* 4.21.5 Disconnected, Degraded, Intermittent, and Limited-Bandwidth Environments
* 4.21.6 Local Identity as an Operational Requirement
* 4.21.7 Delayed Revocation and Policy Convergence
* 4.21.8 Reconnection Creates Trust-Reconciliation Problems

### <mark style="color:$warning;">4.22 Cross-Domain Identity Is Controlled Trust Translation</mark>&#xD;

* 4.22.1 Cross-Domain Identity Is Not Ordinary Active Directory Trust
* 4.22.2 Identity Translation Creates a Security Decision Point
* 4.22.3 Attribute Integrity Becomes Critical
* 4.22.4 Identity Mapping Must Preserve Meaning
* 4.22.5 Classification Boundaries Change Consequence
* 4.22.6 Trust Must Be Explicit and Narrow
* 4.22.7 Cross-Domain Identity Must Be Auditable
* 4.22.8 Asymmetric Trust Can Create Asymmetric Mission Consequence

### <mark style="color:$warning;">4.23 Mission-Partner and Coalition Identity</mark>&#xD;

* 4.23.1 Collaboration Without Administrative Merger
* 4.23.2 Sponsorship Establishes Local Accountability
* 4.23.3 Partner Access Requires an Identity Lifecycle
* 4.23.4 Trust Should Be Narrower Than Connectivity
* 4.23.5 External Assurance Claims Require Deliberate Acceptance
* 4.23.6 Partner Identity Providers Become External Dependencies
* 4.23.7 Partner Compromise Becomes a Shared Identity Incident
* 4.23.8 Federation Failure Must Not Automatically Become Mission Paralysis

### <mark style="color:$warning;">4.24 Contractor-Operated and Shared Identity Infrastructure</mark>&#xD;

* 4.24.1 Contractual Boundaries Are Not Technical Security Boundaries
* 4.24.2 Administrative Authority Can Cross Employer Boundaries
* 4.24.3 Managed Service Providers Can Possess High-Impact Authority
* 4.24.4 Shared Services Concentrate Trust
* 4.24.5 Centralized Services Create Shared Risk
* 4.24.6 Contractor Service Accounts Require the Same Security Analysis as Government Accounts
* 4.24.7 Incident Responsibility Must Remain Traceable
* 4.24.8 Recovery Responsibility Must Be Defined Before Compromise

### <mark style="color:$warning;">4.25 Hidden Dependencies Create Hidden Identity Risk</mark>&#xD;

* 4.25.1 Architecture Diagrams Rarely Show Every Trust Relationship
* 4.25.2 Legacy Services
* 4.25.3 Hardcoded Credentials
* 4.25.4 Administrative Workloads
* 4.25.5 Old Trusts and integrations
* 4.25.6 Shared Privilege Accounts
* 4.25.7 Recovery Dependencies
* 4.25.8 Dependency Mapping Must Include Authority, Not Just Connectivity

### <mark style="color:$warning;">4.26 Trust Concentration Creates Strategic Choke Points</mark>&#xD;

* 4.26.1 Shared Identity Providers
* 4.26.2 Enterprise Certification Authorities
* 4.26.3 Central Synchronization Platforms
* 4.26.4 Enterprise Management Platforms
* 4.26.5 Privileged Access Platforms
* 4.26.6 Backup Systems
* 4.26.7 Automation Platforms
* 4.26.8 The Highest-Value Target May Be the System That Controls Other Attributes

### <mark style="color:$warning;">4.27 Compromise Propagates Through the Trust Graph</mark>&#xD;

* 4.27.1 Identity Compromise Is Often Nonlinear
* 4.27.2 Low Privilege Can Become High Consequence
* 4.27.3 Credentials Create Attack Edges
* 4.27.4 Administrative Relationships Create Attack Edges
* 4.27.5 Authentication Protocols Can Become Attack Pathways
* 4.27.6 Cross-Technology Attack Pathways That Matter
* 4.27.7 On-Premises Compromise Can Cross Into Cloud
* 4.27.8 Cloud or Partner Compromise Can Return Into Enterprise identity

### <mark style="color:$warning;">4.28 Translating Trust Failure Into Mission Consequence</mark>&#xD;

* 4.28.1 Technical Impact Is Not Yet Mission Impact
* 4.28.2 Authority Determines Potential Consequence
* 4.28.3 Confidentiality Failure
* 4.28.4 Integrity Failure
* 4.28.5 Availability Failure
* 4.28.6 Loss of Trust Can Be More Serious Than Loss of Service
* 4.28.7 Trust Failure Can Persist After Service Restoration 4.28.8 Recovery Cost Is Part of Mission Impact

### <mark style="color:$warning;">4.29 Assume Breach and Zero Trust Across the Identity Trust System</mark>&#xD;

* 4.29.1 Compromise of One Component Must Not Automatically Compromise All
* 4.29.2 Prevention Still Matters
* 4.29.3 Strong Authentication Is Necessary But Insufficient
* 4.29.4 Containment Must Follow Authority
* 4.29.5 Policy Enforcement Depends on Upstream Identity Integrity
* 4.29.6 Continuous Evaluation Requires Trustworthy Telemetry
* 4.29.7 Zero Trust Reduces Implicit Trust But Does Not Eliminate Trusted Authorities
* 4.29.8 Recovery Must Deliberately Reestablish Trust

### <mark style="color:$warning;">4.30 Mapping and Defending the Federal Identity Trust System</mark>&#xD;

* 4.30.1 Identify the Identity Authorities
* 4.30.2 Identify the Authentication Authorities
* 4.30.3 Identify the Credential Authorities
* 4.30.4 Identify the Attribute Authorities
* 4.30.5 Identify the Administrative Pathways
* 4.30.6 Identify the Credential Pathways
* 4.30.7 Identify the Federation and Synchronization Pathways
* 4.30.8 Identify the Recovery Pathways
* 4.30.9 Identify the Consumers of Each Authority
* 4.30.10 Find the Hidden Tier 0

### <mark style="color:$warning;">4.31 Locating Trust and Identity Components</mark>&#xD;

* 4.31.1 Locate Where Trust Crosses Agency, Command, Cloud, Contractor, or Mission-Partner Boundaries
* 4.31.2 Determine Which Components Can Impersonate or Speak on Behalf of Others
* 4.31.3 Determine Which Components Can Recreate Trust After Compromise
* 4.31.4 Prioritize Defense According to Maximum Effective Authority
* 4.31.5 Protect Every Component Allowed to Establish, Modify, Extend, Recover, or Speak on Behalf of Federal Identity Authority
