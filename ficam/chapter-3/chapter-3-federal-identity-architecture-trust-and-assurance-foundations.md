# Chapter 3 - Federal Identity Architecture, Trust, and Assurance Foundations

### Abstract

Federal identity security is implemented through an interconnected architecture of authoritative identity sources, proofing services, credentials, directories, public key infrastructure, federation services, cloud identity systems, administrative platforms, and authorization mechanisms. This chapter establishes the technical architecture underlying that ecosystem before later chapters address governance, assessment, and audit assurance. Readers examine Federal Identity, Credential, and Access Management (FICAM), Department of Defense Identity, Credential, and Access Management (DoD ICAM), Identity Assurance Level (IAL), Authenticator Assurance Level (AAL), Federation Assurance Level (FAL), Personal Identity Verification (PIV), Common Access Card (CAC), Electronic Data Interchange Personal Identifier (EDIPI), Federal Public Key Infrastructure (FPKI), Active Directory, Microsoft Entra ID, federation, and hybrid identity. Particular attention is given to assurance continuity, cryptographic trust, person and non-person identities, authoritative attributes, synchronization, and cross-system authority. The objective is architectural literacy: understanding how identity trust is established, represented, propagated, consumed, and technically weakened before evaluating the policies or controls intended to govern it.

### <mark style="color:$warning;">3.1 Trust System Dynamics in Federal Identity Architecture</mark>

* 3.1.1 Multi-System Identity Topography
* 3.1.2 Digital Credentials as Cryptographic Identity Claims
* 3.1.3 Establishing Operational Security Context Through Authentication
* 3.1.4 Mapping Identity to Effective Authority Through Authorization
* 3.1.5 Transitive Trust Expansion Through Identity Federation
* 3.1.6 Administrative Infrastructure Participation in the Trust Chain
* 3.1.7 Cascading Impact of Single-Point Trust Failures
* 3.1.8 Security Boundaries Beyond Directory Service Enclosures

### <mark style="color:$warning;">3.2 Topography of the Federal Identity Ecosystem</mark>

* 3.2.1 Government-Wide Identity Architecture
* 3.2.2 Department- and Agency-Level Identity Implementations
* 3.2.3 Department of Defense Enterprise Identity Infrastructure
* 3.2.4 Identity Architecture in National Security Systems
* 3.2.5 Civilian Agency Identity Control Planes
* 3.2.6 Cloud and Hybrid Identity Integration
* 3.2.7 Mission-Partner and Coalition Interoperability

### <mark style="color:$warning;">3.3 The FICAM Enterprise Architecture Framework</mark>

* 3.3.1 Federal ICAM Architectural Structure
* 3.3.2 Identity Lifecycle Architecture
* 3.3.3 Enterprise Credential Architecture
* 3.3.4 Access Management and Enforcement Systems
* 3.3.5 Cross-Domain and Cross-Agency Federation
* 3.3.6 Governance Interfaces and Lifecycle Coordination
* 3.3.7 Interoperability Across Federal Systems
* 3.3.8 FICAM as an Enterprise Architectural Model

### <mark style="color:$warning;">3.4 Operational Mechanics of DoD ICAM Architecture</mark>

* 3.4.1 Mission-Centric Design of DoD ICAM
* 3.4.2 Enterprise Identity Service Integration
* 3.4.3 Tactical and Mission-Level Identity Fabrics
* 3.4.4 Person Entity Architecture
* 3.4.5 Non-Person Entity Architecture
* 3.4.6 Attribute-Based Access Control Implementation
* 3.4.7 Mission-Partner Identity Integration
* 3.4.8 Mission Assurance Through ICAM Engineering

### <mark style="color:$warning;">3.5 Comparative Analysis: FICAM and DoD ICAM</mark>

* 3.5.1 Government-Wide Baseline Architecture
* 3.5.2 Department-Specific Implementation Constraints
* 3.5.3 Civilian Agency Operational Requirements
* 3.5.4 Defense Mission-Assurance Requirements
* 3.5.5 Classification-Boundary Architectural Divergence
* 3.5.6 Tactical and Coalition Interoperability
* 3.5.7 Disconnected, Intermittent, and Low-Bandwidth Operations
* 3.5.8 Common Identity Principles Under Divergent Constraints

### <mark style="color:$warning;">3.6 Authoritative Identity Sources and Attribute Provenance</mark>

* 3.6.1 Master Identity Record
* 3.6.2 Source-Authority Criteria and Boundaries
* 3.6.3 Human Resources and Personnel-System Integration
* 3.6.4 Sponsorship and Lifecycle Systems
* 3.6.5 DoD Personnel Sources and Defense Manpower Data Center Feeds
* 3.6.6 Attribute Provenance and Integrity
* 3.6.7 Cross-System Identity Correlation
* 3.6.8 Authoritative Records Versus Directory Account Objects

### <mark style="color:$warning;">3.7 Identity Proofing and Trust Foundation Establishment</mark>

* 3.7.1 Evaluating Claimed Identity
* 3.7.2 Identity Evidence Collection
* 3.7.3 Validation of Identity Evidence
* 3.7.4 Identity Resolution
* 3.7.5 Identity Verification
* 3.7.6 Remote and In-Person Proofing
* 3.7.7 Exceptions and Proofing Failure Modes
* 3.7.8 Exploitable Conditions Within Otherwise Compliant Proofing Workflows

### <mark style="color:$warning;">3.8 NIST SP 800-63 Digital Identity Assurance Model</mark>

* 3.8.1 Identity Assurance
* 3.8.2 Authenticator Assurance
* 3.8.3 Federation Assurance
* 3.8.4 Separating Proofing Confidence From Authentication Strength
* 3.8.5 Separating Authentication Strength From Federation Protection
* 3.8.6 Assurance Continuity Across the Authentication Pipeline
* 3.8.7 Assurance Degradation Through Recovery
* 3.8.8 Low-Assurance Alternate Paths as Adversary Targets

### <mark style="color:$warning;">3.9 Identity Assurance Level (IAL) Mechanics</mark>

* 3.9.1 IAL1 Baseline Specifications
* 3.9.2 IAL2 Baseline Specifications
* 3.9.3 IAL3 Baseline Specifications
* 3.9.4 Documentary and Contextual Identity Evidence Requirements
* 3.9.5 Technical Requirements for Identity Resolution
* 3.9.6 Biometric and In-Person Verification Controls
* 3.9.7 Re-Proofing Triggers and Periodic Revalidation
* 3.9.8 Identity Proofing as an Attack Surface Vector

### <mark style="color:$warning;">3.10 Authenticator Assurance Level (AAL) Mechanics</mark>

* 3.10.1 AAL1 Baseline Specifications
* 3.10.2 AAL2 Baseline Specifications
* 3.10.3 AAL3 Baseline Specifications
* 3.10.4 Single-Factor and Multifactor Authenticator Binding
* 3.10.5 Cryptographic Phishing-Resistant Authenticator Controls
* 3.10.6 Hardware-Bound Authenticators
* 3.10.7 Verifier-Impersonation Resistance Protocols
* 3.10.8 Authentication Downgrade and Path-Vector Analysis

### <mark style="color:$warning;">3.11 Federation Assurance Level (FAL) Mechanics</mark>

* 3.11.1 Federation Assurance Level (FAL) Mechanics
* 3.11.2 Relying Party (RP) Security Posture
* 3.11.3 Federation Assertion Payload Mechanics
* 3.11.4 Assertion Signature Integrity and Encryption
* 3.11.5 Audience Restriction Validation Controls
* 3.11.6 Replay and Assertion-Injection Protection
* 3.11.7 Key Management and Replay Mitigation
* 3.11.8 Compromise of a Federation Issuer as Systemic Identity Compromise

### <mark style="color:$warning;">3.12 Federal Credentials as Cryptographic Trust Artifacts</mark>

* 3.12.1 Physical Credential Form Factors
* 3.12.2 Digital Credential Form Factors
* 3.12.3 Hardware and Software Authenticators
* 3.12.4 X.509 Certificate Constructs
* 3.12.5 Private Key Protections and Enclaves
* 3.12.6 Cryptographic Credential-to-Identity Binding
* 3.12.7 Certificate and Credential Revocation Systems
* 3.12.8 Distinguishing Credential Possession from Verified Ownership

### <mark style="color:$warning;">3.13 Personal Identity Verification (PIV) Architecture</mark>

* 3.13.1 PIV Credential Architecture (FIPS 201)
* 3.13.2 Enrollment and Identity Proofing Protocols
* 3.13.3 Secure Credential Personalization and Issuance
* 3.13.4 Smart-Card Cryptographic Authentication Mechanics
* 3.13.5 Structure of PIV Authentication Certificates
* 3.13.6 Nonrepudiation Digital Signatures
* 3.13.7 Asymmetric Encryption for Data Protection
* 3.13.8 PIV Credential Lifecycle Administration

### <mark style="color:$warning;">3.14 Common Access Card (CAC) Implementation in DoD Operations</mark>

* 3.14.1 CAC Design as a DoD PIV Implementation
* 3.14.2 Identity Binding via DoD Personnel Systems
* 3.14.3 CAC Smart-Card Authentication Infrastructure
* 3.14.4 Certificate-Based Access Control Architecture
* 3.14.5 Dual Physical and Logical Access Integration
* 3.14.6 Endpoint Smart-Card Middleware Dependencies
* 3.14.7 Real-Time Certificate Revocation Infrastructure
* 3.14.8 Residual Legacy Authentication Vectors Post-CAC Rollout

### <mark style="color:$warning;">3.15 Electronic Data Interchange Personal Identifier (EDIPI) Integration</mark>

* 3.15.1 Structure of the Ten-Digit EDIPI Standard
* 3.15.2 Persistent Unique Person Identifier Design
* 3.15.3 Cross-System Correlation Across DoD Environments
* 3.15.4 Credential-to-EDIPI Cryptographic Binding
* 3.15.5 Active Directory Schema and Attribute Usage
* 3.15.6 Application Authorization Integration Protocols
* 3.15.7 PII and Privacy Considerations for Persistent Identifiers
* 3.15.8 Persistent Identifiers as High-Value Reconnaissance Targets

### <mark style="color:$warning;">3.16 Federal Public Key Infrastructure (FPKI) Architecture</mark>

* 3.16.1 Hierarchical Topology of the Federal PKI
* 3.16.2 Certification Authority (CA) Operational Roles
* 3.16.3 Trust Anchor Management and Federal Bridge Integration
* 3.16.4 Certificate Policy (CP) Mapping and Enforcement
* 3.16.5 X.509 Certification Path Validation Algorithms
* 3.16.6 CRL and OCSP Revocation Infrastructure
* 3.16.7 Cross-Certification Relationships Across Federal Boundaries
* 3.16.8 FPKI Hierarchy Compromise as Enterprise Identity Compromise

### <mark style="color:$warning;">3.17 Digital Certificates as Standalone Identity Credentials</mark>

* 3.17.1 User Authentication Certificates
* 3.17.2 Machine and Computer Certificates
* 3.17.3 Service and Application Certificates
* 3.17.4 Smart-Card Logon Certificate Specifications
* 3.17.5 Private Key Storage and Non-Exportability Controls
* 3.17.6 Extended Key Usage (EKU) Validation Rules
* 3.17.7 Name Mapping Protocols in Directory Services
* 3.17.8 Certificate Persistence Vectors Post-Password Reset

### <mark style="color:$warning;">3.18 Active Directory Within the Federal Identity Hierarchy</mark>

* 3.18.1 Enterprise Directory Service Role
* 3.18.2 Kerberos and NTLM Authentication Authority
* 3.18.3 Discretionary Access Control List (DACL) Authorization Data
* 3.18.4 Security Group Structure and Transitive Membership
* 3.18.5 Machine Object Identity Management
* 3.18.6 Managed Service Account (MSA/gMSA) Identities
* 3.18.7 PKI Integration via Active Directory Certificate Services (AD CS)
* 3.18.8 Active Directory as the Operational Control Plane Operational Center

### <mark style="color:$warning;">3.19 Microsoft Entra ID as a Cloud Identity Control Plane</mark>

* 3.19.1 Cloud Directory Architecture
* 3.19.2 OpenID Connect, OAuth 2.0, and SAML
* 3.19.3 Enterprise Applications
* 3.19.4 Service Principals and Workload Identities
* 3.19.5 Device Registration and Identity
* 3.19.6 Conditional Access
* 3.19.7 Cloud Role-Based Access Control
* 3.19.8 Cross-Plane Trust With On-Premises Identity

### <mark style="color:$warning;">3.20 Bidirectional Authority in Hybrid Identity Architecture</mark>

* 3.20.1 Active Directory-to-Entra Synchronization
* 3.20.2 Cloud-to-On-Premises Writeback
* 3.20.3 Password Hash Synchronization
* 3.20.4 Pass-Through Authentication
* 3.20.5 Federation Through AD FS and External Identity Providers
* 3.20.6 Synchronization-Service Administrative Authority
* 3.20.7 Hybrid Recovery and Staging Infrastructure
* 3.20.8 Cross-Plane Compromise Propagation

### <mark style="color:$warning;">3.21 Person, Privileged, and External Person Identity Architecture</mark>

* 3.21.1 Workforce Identities
* 3.21.2 Military and Civilian Identities
* 3.21.3 Contractor Identities
* 3.21.4 Guest and Mission-Partner Identities
* 3.21.5 Privileged Person Identities
* 3.21.6 One Person Represented by Multiple Security Principals

### <mark style="color:$warning;">3.22 Non-Person, Device, Service, Application, and Workload Identity</mark>

* 3.22.1 Device Identities
* 3.22.2 Service Accounts
* 3.22.3 Managed Service Accounts
* 3.22.4 Application Identities
* 3.22.5 Workload Identities
* 3.22.6 Automation and Orchestration Identities
* 3.22.7 Ephemeral Identity
* 3.22.8 Non-Person Identity Ownership

### <mark style="color:$warning;">3.23 Authentication and Authorization as Distinct Trust Functions</mark>

* 3.23.1 Establishing Identity Context
* 3.23.2 Establishing Security Context
* 3.23.3 Translating Identity Into Permission
* 3.23.4 Role-Based Access Control
* 3.23.5 Attribute-Based Access Control
* 3.23.6 Discretionary and Mandatory Access Control
* 3.23.7 Conditional and Policy-Based Access
* 3.23.8 Strong Authentication Does Not Guarantee Safe Authorization

### <mark style="color:$warning;">3.24 Federation and Cross-Boundary Identity Translation</mark>

* 3.24.1 Federation Trust
* 3.24.2 Claims Translation
* 3.24.3 Attribute Mapping
* 3.24.4 Cross-Agency Federation
* 3.24.5 Mission-Partner Federation
* 3.24.6 Classification and Cross-Domain Boundaries
* 3.24.7 Local Authorization of External Identities
* 3.24.8 Federation as Distributed Authority

### <mark style="color:$warning;">3.25 Administrative Infrastructure Within the Identity Architecture</mark>

* 3.25.1 Identity Administration Systems
* 3.25.2 Privileged Access Infrastructure
* 3.25.3 Endpoint Management Platforms
* 3.25.4 Virtualization Management
* 3.25.5 Backup and Recovery Infrastructure
* 3.25.6 Certificate Administration
* 3.25.7 Synchronization Platforms
* 3.25.8 Administrative Systems as Hidden Identity Authorities

### <mark style="color:$warning;">3.26 Tier 0, Clean Source, and Effective Authority</mark>

* 3.26.1 Tier 0 as a Relationship
* 3.26.2 Direct and Indirect Administrative Control
* 3.26.3 Clean Source Administration
* 3.26.4 Trustworthy Administrative Endpoints
* 3.26.5 Recovery Infrastructure Authority
* 3.26.6 Effective Authority Beyond Administrative Titles
* 3.26.7 Hidden Tier 0
* 3.26.8 Strategic Trust Concentration

### <mark style="color:$warning;">3.27 Architectural Integration Points as Attack Surfaces</mark>

* 3.27.1 Proofing Interfaces
* 3.27.2 Provisioning Interfaces
* 3.27.3 Synchronization Interfaces
* 3.27.4 Federation Interfaces
* 3.27.5 Certificate Enrollment Interfaces
* 3.27.6 Administrative Interfaces
* 3.27.7 Recovery Interfaces
* 3.27.8 Trust Boundaries as Adversary Pivot Points

### <mark style="color:$warning;">3.28 Identity Telemetry as an Architectural Requirement</mark>

* 3.28.1 Authentication Telemetry
* 3.28.2 Authorization Changes
* 3.28.3 Credential Issuance
* 3.28.4 Directory Modifications
* 3.28.5 Federation Events
* 3.28.6 Synchronization Events
* 3.28.7 Privileged Actions
* 3.28.8 Cross-System Identity Correlation

### <mark style="color:$warning;">3.29 Federal Identity Architecture Through the Lens of the Opponent</mark>

* 3.29.1 Which System Establishes Identity?
* 3.29.2 Which System Can Change Identity Attributes?
* 3.29.3 Which Authority Issues Credentials?
* 3.29.4 Which System Accepts Assertions?
* 3.29.5 Which Principal Can Modify Authorization?
* 3.29.6 Which Administrative Dependency Can Override the Intended Boundary?
* 3.29.7 Which Alternate Path Provides Lower Assurance?
* 3.29.8 Which Trust Authority Produces the Greatest Consequence if Compromised?

### <mark style="color:$warning;">3.30 Federal Identity Architecture and Assurance Principles</mark>

* 3.30.1 Treat Identity as a Multi-System Trust Architecture
* 3.30.2 Distinguish Identity From Accounts
* 3.30.3 Distinguish Authentication From Authorization
* 3.30.4 Preserve IAL, AAL, and FAL Across the Full Transaction
* 3.30.5 Protect Credentials as Trust Artifacts
* 3.30.6 Protect Authoritative Attributes as Authorization Inputs
* 3.30.7 Treat Federation and Synchronization as Security Boundaries
* 3.30.8 Include Person and Non-Person Identity
* 3.30.9 Evaluate Administrative Dependencies as Identity Authority
* 3.30.10 Design Identity Architecture With Adversary Reachability in Mind
