# Chapter 4

4.2 Identity Infrastructure as Mission Infrastructure\
4.2.1 Authentication Availability Becomes Service Availability\
4.2.2 Directory Integrity Becomes Mission-Relevant Integrity\
4.2.3 Authorization Integrity Determines Who Can Exercise Mission Authority\
4.2.4 Credential Trust Determines Which Principals Can Be Believed\
4.2.5 Authorization Errors Can Outlive the Original Compromise\
4.2.6 Identity Supports Mission Users and Mission Administrators\
4.2.7 Shared Identity Infrastructure Creates Shared Mission Dependencies\
4.2.8 Identity Belongs in the Mission Dependency Map

4.3 Components of the Federal Identity Trust System\
4.3.1 Active Directory Domain Services (AD DS)\
4.3.2 Public Key Infrastructure (PKI)\
4.3.3 Active Directory Certificate Services (AD CS)\
4.3.4 Active Directory Federation Services (AD FS) Infrastructure\
4.3.5 Microsoft Entra ID and Cloud Identity\
4.3.6 Identity Synchronization\
4.3.7 Privileged Access Management (PAM) Infrastructure\
4.3.8 Authoritative Identity Sources\
4.3.9 Device and Workload Identity Infrastructure\
4.3.10 Identity Governance Platforms (IGA)

4.4 Authority Flows Through Dependencies\
4.4.1 Directory Authority (Explicit Administrative Control)\
4.4.2 Indirect Authority (Nested and Delegated Access Vectors)\
4.4.3 Transitive Authority (Cross-Boundary Control Propagation)\
4.4.4 Authority Through Credential Access (Identity Theft and Replay)\
4.4.5 Authority Through Configuration (Policy and Settings Manipulation)\
4.4.6 Authority Through Software Deployment (Pipeline and Agent Execution)\
4.4.7 Authority Through Infrastructure Control (Management Plane Reachability)\
4.4.8 Authority Through Recovery (Disaster and Emergency Override Channels)

4.5 The Trusted Core\
4.5.1 Domain Controllers Are Necessary but Not Sufficient\
4.5.2 Certification Authorities as Trust Authorities\
4.5.3 Federation Signing Infrastructure\
4.5.4 Synchronization Systems\
4.5.5 Privileged Administration Systems\
4.5.6 Hypervisors and Virtualization Management\
4.5.7 Backup and Recovery Systems\
4.5.8 Endpoint and Configuration Management\
4.5.9 Security Infrastructure as Potential Control Infrastructure\
4.5.10 Automation and Orchestration Platforms

4.6 The Clean Source Principle\
4.6.1 A System Cannot Be Administered Safely From a Less-Trusted System\
4.6.2 Administrative Dependencies Inherit the Target's Security Tier\
4.6.3 Credential Entry Creates Trust Relationships\
4.6.4 Privileged Sessions Carry Trust Between Systems\
4.6.5 Software Supply and Deployment Paths Matter\
4.6.6 Administrative Tooling Must Originate From Trusted Sources\
4.6.7 Recovery Sources Must Also Be Clean\
4.6.8 Clean Source Is a Chain, Not a Single Hardened Workstation

4.7 Identity Trust Versus Network Trust\
4.7.1 Network Location Is Not Proof of Identity\
4.7.2 Authentication Is Not Proof of Device Integrity\
4.7.3 Device Trust Is Not User Trust\
4.7.4 Internal Connectivity Does Not Establish Authorization\
4.7.5 Segmentation and Identity Boundaries Solve Different Problems\
4.7.6 Identity Trust Is Contextual\
4.7.7 Network Compromise Can Influence Identity Trust\
4.7.8 Zero Trust Replaces Implicit Trust With Explicit Evaluation

4.8 Identity Trust Versus Administrative Trust\
4.8.1 Recognizing an Identity Does Not Grant Administrative Authority\
4.8.2 Administrative Authority Can Exist Without Interactive Authentication\
4.8.3 Administrative Rights Can Be Embedded in Delegation\
4.8.4 Administrative Authority Can Be Exercised Through Applications and Services\
4.8.5 Hidden Administrators\
4.8.6 Ownership Can Create Administrative Authority\
4.8.7 Administrative Reach Can Cross Formal Security Boundaries\
4.8.8 Effective Authority Matters More Than Administrative Titles

4.9 Authoritative Identity and Attribute Trust\
4.9.1 Every Identity Fact Has an Origin\
4.9.2 Authoritative Does Not Mean Authoritative for Everything\
4.9.3 Attribute Provenance Is a Security Property\
4.9.4 Security-Relevant Attributes Become Authorization Inputs\
4.9.5 Attribute Manipulation Can Become Privilege Escalation\
4.9.6 Synchronization Does Not Create Authority by Itself\
4.9.7 Conflicting Authorities Create Identity Ambiguity\
4.9.8 Downstream Trust Is Only as Strong as Upstream Attribute Integrity

4.10 Identity Synchronization as a Trust Boundary\
4.10.1 Synchronization Is More Than Data Movement\
4.10.2 On-Premises-to-Cloud Authority\
4.10.3 Cloud-to-On-Premises Authority\
4.10.4 Synchronization Accounts As High-Value Principals\
4.10.5 Password and Credential Synchronization\
4.10.6 Scoping and Transformation Rules\
4.10.7 Synchronization Infrastructure as Hidden Tier 0\
4.10.8 Synchronization Failure and Mission Continuity

4.11 Credential Trust\
4.11.1 Identity and Credential Are Different Concepts\
4.11.2 Credential Strength Does Not Repair Weak Authority\
4.11.3 Credential Issuance Is a Trust Decision\
4.11.4 Authenticator Binding Establishes Security Context\
4.11.5 Credential Recovery Is Part of the Trust Model\
4.11.6 Alternate Credentials Can Preserve Authority\
4.11.7 Revocation Must Match Credential Diversity\
4.11.8 Compromise Must Be Scoped Across Every Credential Type

4.12 Certificate Trust Within the Identity Trust System\
4.12.1 Certificates Can Represent Users, Devices, and Services\
4.12.2 Certification Authorities Determine Which Identities Can Be Asserted\
4.12.3 Certificate Templates Encode Trust Decisions\
4.12.4 Trust Stores Become Security Boundaries\
4.12.5 Private Keys Represent Persistent Authority\
4.12.6 Certificate Mapping Connects Cryptographic and Directory Identity\
4.12.7 Revocation Is an Operational Dependency\
4.12.8 PKI Compromise Can Outlive Password Remediation

4.13 Federation as Distributed Trust\
4.13.1 Federation Separates Authentication From the Resource\
4.13.2 The Identity Provider Becomes an Upstream Authority\
4.13.3 Signing Keys Become Identity Authority\
4.13.4 Claims Carry Security-Relevant Meaning\
4.13.5 Relying Parties Consume Upstream Trust Decisions\
4.13.6 Federation Trust Must Be Scoped\
4.13.7 Federation Failure Must Be Designed For\
4.13.8 Compromise of One Issuer Can Affect Many Relying Systems

4.14 Person Entities and Non-Person Entities (NPE)\
4.14.1 Human Identity Has a Natural Accountability Model\
4.14.2 Non-Person Entities Require Deliberate Ownership\
4.14.3 Machine Identity Is More Than a Computer Object\
4.14.4 Service Identity Can Exercise Persistent Authority\
4.14.5 Application Identity Extends Authority Into APIs and Cloud Services\
4.14.6 NPE Credentials Behave Differently\
4.14.7 NPE Privilege Can Be Difficult to Observe\
4.14.8 Workload Identity Changes the Scale of Governance

4.14 Person Entities and Non-Person Entities\
4.14.1 Human Identity Has a Natural Accountability Model\
4.14.2 Non-Person Entities Require Deliberate Ownership\
4.14.3 Machine Identity Is More Than a Computer Object\
4.14.4 Service Identity Can Exercise Persistent Authority\
4.14.5 Application Identity Extends Authority Into APIs and Cloud Services\
4.14.6 NPE Credentials Behave Differently\
4.14.7 NPE Privilege Can Be Difficult to Observe\
4.14.8 Workload Identity Changes the Scale of Governance

4.15 Federal and Department of Defense Enclaves\
4.15.1 Non-Classified Internet Protocol Router Network (NIPRNet)\
4.15.2 Secret Internet Protocol Router Network (SIPRNet)\
4.15.3 Joint Worldwide Intelligence Communications System (JWICS)\
4.15.4 National Security Systems (NSS)\
4.15.5 Tactical and Disconnected Environments\
4.15.6 Disconnected, Degraded, Intermittent, and Low-Bandwidth (DDIL) Operations\
4.15.7 Local Identity as an Operational Requirement\
4.15.8 Reconnection Creates Trust-Reconciliation Problems

4.16 Cross-Domain Solutions and Identity\
4.16.1 Cross-Domain Identity Is Not Ordinary Domain Trusts\
4.16.2 Identity Translation Creates a Security Decision Point\
4.16.3 Attribute Integrity Becomes Critical\
4.16.4 Identity Mapping Across Security Domains\
4.16.5 Authorization Must Remain Local to the Destination Security Domain\
4.16.6 Asymmetric Consequence of Compromise\
4.16.7 Cross-Domain Trust Must Remain Explicit\
4.16.8 Cross-Domain Identity Requires Strong Accountability and Auditability

4.17 Mission-Partner and Coalition Identity\
4.17.1 Collaboration Without Administrative Merger\
4.17.2 Sponsorship Establishes Local Accountability\
4.17.3 Partner Access Must Have a Lifecycle\
4.17.4 Trust Should Be Narrower Than Connectivity\
4.17.5 External Assurance Claims Require Deliberate Acceptance\
4.17.6 Local Authorization Must Constrain External Identity\
4.17.7 Partner Compromise Becomes a Shared Identity Incident\
4.17.8 Federation Failure Must Not Become Mission Paralysis

4.18 Contractor-Operated and Shared Identity Infrastructure\
4.18.1 Contractual Boundaries Are Not Technical Security Boundaries\
4.18.2 Administrative Authority Can Cross Employer Boundaries\
4.18.3 Managed Service Providers Can Become Identity Authorities\
4.18.4 Shared Services Concentrate Authority\
4.18.5 Shared Services Create Shared Risk\
4.18.6 Shared Administrative Platforms Expand Blast Radius\
4.18.7 Contractor Separation Must Remove Technical Authority\
4.18.8 Responsibility Must Remain Traceable

4.19 Hidden Dependencies and Identity Risk\
4.19.1 Documented Architecture Rarely Shows Every Trust Relationship\
4.19.2 Administrative Convenience Creates Durable Dependencies\
4.19.3 Legacy Services Preserve Unexpected Authority\
4.19.4 Automation Can Hide Privilege Behind Service Accounts\
4.19.5 Recovery Dependencies Differ From Operating Dependencies\
4.19.6 Security Dependencies Can Be More Important Than Service Dependencies\
4.19.7 Manual Workarounds Can Become Persistent Trust Paths\
4.19.8 Dependency Mapping Must Include Authority

4.20 Compromise Propagation Through the Trust System\
4.20.1 Identity Compromise Is Often Nonlinear\
4.20.2 Low-Privilege Compromise Can Become High-Impact Compromise\
\*4.20.3 Authentication Pathways Can Become Attack Pathways\
4.20.4 Administrative Pathways Can \*Become Attack Pathways\
4.20.5 Credential Pathways Can Become Attack Pathways\
4.20.6 Recovery Pathways Can Become Attack Pathways\
4.20.7 Cross-Technology Pathways Matter\
4.20.8 Trust Concentration Creates Choke Points

4.21 Translating Technical Identity Failure Into Mission Consequence\
4.21.1 Technical Impact Is Not Yet Mission Impact\
4.21.2 Authority Determines Potential Consequence\
4.21.3 Identity Failure Can Deny Mission Access\
4.21.4 Identity Failure Can Manufacture Unauthorized Authority\
4.21.5 Loss of Integrity Can Exceed Loss of Availability\
4.21.6 Loss of Trust Can Persist After Service Restoration\
4.21.7 Mission Impact Includes Recovery Cost\
4.21.8 Mission Security Depends on Identity When the Mission Depends on Identity

4.22 Assume Breach Across the Identity Trust System\
4.22.1 Compromise of One Component Must Not Automatically Become Compromise of All\
4.22.2 Prevention Still Matters\
4.22.3 Containment Must Follow Authority\
4.22.4 High-Value Trust Authorities Require Isolation\
4.22.5 Detection Should Focus on Trust Changes\
4.22.6 Identity Compromise Must Be Scoped Beyond the First Affected Account\
4.22.7 Recovery Must Reestablish Trust Deliberately\
4.22.8 Assume Breach Requires Architecture That Can Survive Breach

4.23 Map the Identity Trust System\
4.23.1 Identify the Authorities\
4.23.2 Identify the Consumers\
4.23.3 Identify the Administrative Pathways\
4.23.4 Identify the Credential Pathways\
4.23.5 Identify the Trust Pathways\
4.23.6 Identify the Synchronization Pathways\
4.23.7 Identify the Recovery Pathways\
4.23.8 Find the Hidden Tier 0

4.24 Federal Identity Trust and Zero Trust Architecture (ZTA)\
4.24.1 Zero Trust Depends Upon Reliable Identity\
4.24.2 Strong Authentication Is Necessary but Insufficient\
4.24.3 Device Identity Becomes Part of Access Trust\
4.24.4 Authorization Must Reflect Current Context\
4.24.5 Policy Enforcement Depends Upon Upstream Authorities\
4.24.6 Continuous Evaluation Changes Session Trust\
4.24.7 Compromised Identity Data Can Corrupt Zero Trust Decisions\
4.24.8 Zero Trust Does Not Eliminate the Trusted Core

4.25 Effective Authority as the Real Security Boundary\
4.25.1 Formal Privilege Versus Effective Authority\
4.25.2 Direct Permission Is Only One Form of Control\
4.25.3 Credential Access Can Produce Equivalent Authority\
4.25.4 Delegation Can Produce Equivalent Authority\
4.25.5 Software Deployment Can Produce Equivalent Authority\
4.25.6 Certificate Issuance Can Produce Equivalent Authority\
4.25.7 Recovery Capability Can Produce Equivalent Authority\
4.25.8 The Security Boundary Must Enclose Every Pathway Capable of Exercising Equivalent Control

4.26 Hidden Tier 0 and Authority Equivalence\
4.26.1 Tier 0 Is Determined by Control, Not Product Name\
4.26.2 Direct Control of the Identity Control Plane\
4.26.3 Indirect Control of the Identity Control Plane\
4.26.4 Credential Equivalence to Administrative Control\
4.26.4 Configuration Equivalence to Administrative Control\
4.26.6 Recovery Equivalence to Administrative Control\
4.26.7 Management Infrastructure as Hidden Tier 0\
4.26.8 Reclassifying Assets According to Effective Authority

4.27 Strategic Identity Choke Points\
4.27.1 Trust Concentration Creates Strategic Importance\
4.27.2 Domain Controllers as Directory Choke Points\
4.27.3 Certification Authorities as Credential Choke Points\
4.27.4 Federation Issuers as Assertion Choke Points\
4.27.5 Synchronization Platforms as Cross-Plane Choke Points\
4.27.6 Privileged Access Infrastructure as Administrative Choke Points\
4.27.7 Backup and Recovery Infrastructure as Restoration Choke Points\
4.27.8 Protecting Choke Points Can Break Multiple Attack Pathways Simultaneously

4.28 Recovery Infrastructure as Identity Authority\
4.28.1 Recovery Is Not Separate From the Trust System\
4.28.2 Backups Can Contain Identity Authority\
4.28.3 Restored Directory State Can Reintroduce Compromise\
4.28.4 Restored PKI State Can Reintroduce Untrusted Keys\
4.28.5 Restored Federation State Can Reintroduce Signing Authority\
4.28.6 Recovery Credentials Require Tier-Appropriate Protection\
4.28.7 Recovery Systems Must Be Included in Clean-Source Architecture\
4.28.8 Trust Restoration Requires Validation, Not Merely Service Restoration\
4.29 The Federal Identity Trust System Through the Lens of the Opponent\
4.29.1 Which System Can Establish a New Identity?\
4.29.2 Which System Can Modify Security-Relevant Identity Attributes?\
4.29.3 Which System Can Issue a Trusted Credential?\
4.29.4 Which System Can Assert Identity to Other Systems?\
4.29.5 Which System Can Modify Authorization?\
4.29.6 Which Administrative Dependency Can Override the Intended Boundary?\
4.29.7 Which Recovery Path Can Restore or Recreate Authority?\
4.29.8 Which Single Compromise Produces the Greatest Expansion of Effective Authority?\
4.30 Federal Identity Trust-System Principles\
4.30.1 Treat the Identity Boundary as Larger Than the Active Directory Domain\
4.30.2 Map Authority Rather Than Product Boundaries\
4.30.3 Distinguish Authentication Trust From Administrative Trust\
4.30.4 Treat Authoritative Attributes as Security-Relevant Inputs\
4.30.5 Treat Synchronization and Federation as Trust Boundaries\
4.30.6 Include Person and Non-Person Entities\
4.30.7 Identify Hidden Tier 0 Through Effective Authority\
4.30.8 Extend Clean-Source Protection Through Every Administrative Dependency\
4.30.9 Protect Strategic Identity Choke Points\
4.30.10 Treat Recovery Infrastructure as Identity Authority\
4.30.11 Translate Identity Compromise Into Mission Consequence\
4.30.12 Design the Trust System to Contain Compromise Rather Than Assume It Can Always Be Prevented\
4.30.13 Restore Trust, Not Merely Service Availability\
4.30.14 Evaluate Every Trust Relationship Through the Lens of the Opponent
