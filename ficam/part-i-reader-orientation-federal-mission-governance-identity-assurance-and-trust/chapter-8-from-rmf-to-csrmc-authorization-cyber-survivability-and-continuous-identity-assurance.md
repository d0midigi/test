# Chapter 8 - From RMF to CSRMC: Authorization, Cyber Survivability, and Continuous Identity Assurance

### Abstract

This chapter examines federal cybersecurity risk management through the transition from the Risk Management Framework (RMF) to the Department of Defense Cybersecurity Risk Management Construct (CSRMC). RMF remains foundational to federal security categorization, control selection, implementation, assessment, authorization, and continuous monitoring, while the CSRMC reshapes how those activities are operationalized across DoD environments through automation, continuous authorization, DevSecOps integration, cyber survivability, enterprise inheritance, and threat-informed testing. Chapter 8 follows identity risk across the CSRMC Design, Build, Test, Onboard, and Operations phase while mapping those activities to established RMF functions. Active Directory, FICAM, DoD ICAM, privileged access, FPKI, federation, synchronization, Microsoft Entra ID, Tier 0 dependencies, STIG/SRG compliance, IAVA/IAVB response, POA\&Ms, eMASS, and common controls are examined as continuously changing sources of mission risk and authorization evidence. Attack-path analysis and adversarial validation challenge control assumptions, while continuous identity assurance provides ongoing evidence that identity authority, trust relationships, recovery mechanisms, and defensive controls remain within acceptable mission-risk conditions.

### <mark style="color:$warning;">8.1x From the Risk Management Framework (RMF) to the Cybersecurity Risk Management Construct (CSRMC)</mark>

This chapter places identity security inside the federal Risk Management Framework (RMF) and follows identity risk from preparation and categorization through control selection, implementation, assessment, authorization, and continuous monitoring. Rather than treating RMF as a documentation exercise, the chapter examines how Active Directory, FICAM, DoD ICAM, privileged access, credentialing, federation, synchronization, and Tier 0 dependencies become mission risk and authorization evidence. Readers examine control inheritance, common controls, DISA Security Technical Implementation Guides, vulnerability management, IAVA/IAVB response, Plans of Action and Milestones, eMASS, security testing, operational assessments, configuration drift, and continuous monitoring. Offensive analysis is used to identify attack paths and technical conditions that challenge claimed control effectiveness, while defensive analysis translates those findings into remediation priorities and defensible risk decisions. The chapter culminates in continuous identity assurance: maintaining evidence that critical identity controls, privilege relationships, trust paths, and recovery mechanisms remain acceptable after authorization rather than assuming an Authority to Operate represents a permanent security state.

### <mark style="color:$warning;">8.1 Risk Management as an Engineering Discipline</mark>&#xD;

* 8.1.1 RMF Is More Than an Authorization Process
* 8.1.2 Authorization Does Not Create Security
* 8.1.3 Identity Risk Exists Across the RMF Lifecycle
* 8.1.4 Mission Risk Is the Final Context
* 8.1.5 Offensive Findings Must Be Translated Into Consequence
* 8.1.6 Defensive Controls Must Demonstrate Effectiveness

### <mark style="color:$warning;">8.2 Identity Security Across the RMF Lifecycle</mark>&#xD;

* 8.2.1 Identity Architecture Shapes the Authorization Boundary
* 8.2.2 Authentication and Authorization Dependencies Cross Boundaries
* 8.2.3 Shared Identity Services Create Shared Risk
* 8.2.4 Privileged Relationships Change Between Authorization Milestones
* 8.2.5 Continuous Identity Assurance Connects the RMF Steps

### <mark style="color:$warning;">8.3 RMF Step 1 - Prepare</mark>&#xD;

* 8.3.1 Mission and System Context
* 8.3.2 Identity Stakeholders
* 8.3.3 Identity Trust-System Dependencies
* 8.3.4 Common-Control Providers
* 8.3.5 External and Shared Identity Services
* 8.3.6 Mission Dependencies
* 8.3.7 Preparing for Adversarial Validation

### <mark style="color:$warning;">8.4 Authorization Boundaries and Identity Dependencies</mark>&#xD;

* 8.4.1 System Boundary Versus Identity Boundary
* 8.4.2 Active Directory and PKI Dependencies
* 8.4.3 Federation and Microsoft Entra ID
* 8.4.4 Synchronization
* 8.4.5 Privileged Administration
* 8.4.6 Backup and Recovery
* 8.4.7 Hidden Tier 0
* 8.4.8 The Attacker Does Not Respect the RMF Boundary Diagram

### <mark style="color:$warning;">8.5 RMF Step 2 - Categorize</mark>&#xD;

* 8.5.1 Confidentiality
* 8.5.2 Integrity
* 8.5.3 Availability
* 8.5.4 Identity Infrastructure as Mission Infrastructure
* 8.5.5 Authentication and Authorization Failure
* 8.5.6 Loss of Identity Trust
* 8.5.7 Why Integrity Failure Can Manufacture Authority

### <mark style="color:$warning;">8.6 RMF Step 3 - Select</mark>&#xD;

* 8.6.1 Security and Privacy Controls
* 8.6.2 Control Baselines
* 8.6.3 Tailoring
* 8.6.4 Overlays
* 8.6.5 Compensating Controls
* 8.6.6 Common Controls
* 8.6.7 Control Selection Must Reflect the Attack Surface

### <mark style="color:$warning;">8.7 Identity-Relevant NIST SP 800-53 Control Families</mark>&#xD;

* 8.7.1 Access Control
* 8.7.2 Identification and Authentication
* 8.7.3 Audit and Accountability
* 8.7.4 Configuration Management
* 8.7.5 System and Communications Protection
* 8.7.6 System and Information Integrity
* 8.7.7 Contingency Planning and Incident Response
* 8.7.8 Risk Assessment and Security Assessment
* 8.7.9 Supply Chain Risk Management

### <mark style="color:$warning;">8.8 RMF Step 4 - Implement</mark>&#xD;

* 8.8.1 Controls Become Technical State
* 8.8.2 Authentication and Authorization Controls
* 8.8.3 Privileged Access Controls
* 8.8.4 Directory and Group Policy Controls
* 8.8.5 Certificate, Federation, and Synchronization Controls
* 8.8.6 Logging and Recovery Controls
* 8.8.7 Implementation Statements Must Be Testable
* 8.8.8 Effective Authority Must Match the Documented Control

### <mark style="color:$warning;">8.9 From Control Language to Technical Configuration</mark>&#xD;

* 8.9.1 Security Groups and Delegation
* 8.9.2 Group Policy
* 8.9.3 Authentication Policy
* 8.9.4 Administrative Tiering
* 8.9.5 Certificate Policy
* 8.9.6 Local Administrator Management
* 8.9.7 Auditing and Network Restrictions
* 8.9.8 Evidence Sources and Exceptions

### <mark style="color:$warning;">8.10 RMF Step 5 - Assess</mark>&#xD;

* 8.10.1 Examine
* 8.10.2 Interview
* 8.10.3 Test
* 8.10.4 Technical Validation of Identity Controls
* 8.10.5 Configuration Versus Effective Security
* 8.10.6 Effective Authority
* 8.10.7 Current and Reproducible Evidence

### <mark style="color:$warning;">8.11 Security Assessment and Adversarial Validation</mark>&#xD;

* 8.11.1 Control Assessment and Adversarial Testing Answer Different Questions
* 8.11.2 Attack Paths Can Reveal Incomplete Control Scope
* 8.11.3 Authentication and Authorization Testing
* 8.11.4 Privileged Access Testing
* 8.11.5 Logging and Recovery Validation
* 8.11.6 Proving Consequence Without Unnecessary Exploitation
* 8.11.7 Defensive Validation After Remediation

### <mark style="color:$warning;">8.12 RMF Step 6 - Authorize</mark>&#xD;

* 8.12.1 Authorization Is a Risk Decision
* 8.12.2 Authorization Package Integrity
* 8.12.3 Residual Risk
* 8.12.4 Conditions of Authorization
* 8.12.5 Inherited Identity Risk
* 8.12.6 Authorization Is Not Permanent

### <mark style="color:$warning;">8.13 Identity Risk and the Authorizing Official</mark>&#xD;

* 8.13.1 Translate Technical Detail Into Mission Consequence
* 8.13.2 Explain the Authority Obtained
* 8.13.3 Explain Systems and Missions Reachable
* 8.13.4 Explain Detection and Recovery Difficulty
* 8.13.5 Explain Compensating Controls
* 8.13.6 Explain Residual Attack Paths

### <mark style="color:$warning;">8.14 Attack Paths as Authorization Evidence</mark>&#xD;

* 8.14.1 Effective Authority
* 8.14.2 Credential Reachability
* 8.14.3 Administrative Reachability
* 8.14.4 Tier 0 Exposure
* 8.14.5 Cross-System Dependencies
* 8.14.6 Mission Consequence
* 8.14.7 Attack-Path Remediation as Risk Reduction

### <mark style="color:$warning;">8.15 RMF Step 7 - Monitor</mark>&#xD;

* 8.15.1 Continuous Monitoring Sustains Authorization
* 8.15.2 Identity and Privilege State Change Continuously
* 8.15.3 Configuration Drift
* 8.15.4 Threat-Driven Reassessment
* 8.15.5 Effective-Authority Monitoring
* 8.15.6 New Attack Paths Can Invalidate Old Risk Decisions

### <mark style="color:$warning;">8.16 Common Controls, Inheritance, and Shared Responsibility</mark>&#xD;

* 8.16.1 Identity as a Common Control
* 8.16.2 Partial Inheritance
* 8.16.3 Shared Identity Services
* 8.16.4 Common-Control Failure Creates Shared Risk
* 8.16.5 Inherited Risk Must Remain Visible
* 8.16.6 Inheritance Must Not Hide Local Responsibility

### <mark style="color:$warning;">8.17 DISA STIGs, SRGs, and Technical Baselines</mark>&#xD;

* 8.17.1 Technical Baselines Establish Expected State
* 8.17.2 Category I, II, and III Findings
* 8.17.3 Applicability and Not-Applicable Determinations
* 8.17.4 Automated Assessment
* 8.17.5 Microsoft Security Baselines and Vendor Guidance
* 8.17.6 Baseline Compliance Does Not Eliminate Attack Paths

### <mark style="color:$warning;">8.18 Vulnerability Management and Identity Risk</mark>&#xD;

* 8.18.1 Severity Versus Identity Consequence
* 8.18.2 Information Assurance Vulnerability Alerts
* 8.18.3 Information Assurance Vulnerability Bulletins
* 8.18.4 Known Exploited Vulnerabilities
* 8.18.5 Tier 0 Exposure
* 8.18.6 Patching Does Not Automatically Remove the Attack Path

### <mark style="color:$warning;">8.19 Operational Vulnerability Response</mark>&#xD;

* 8.19.1 Triage and Identity Relevance
* 8.19.2 Trust-Boundary Analysis
* 8.19.3 Exploitability and Existing Compromise
* 8.19.4 Dependency-Aware Remediation
* 8.19.5 Emergency Change and Compensating Controls
* 8.19.6 When Vulnerability Management Becomes Incident Response
* 8.19.7 Post-Remediation Validation
* 8.19.8 Closure Evidence and Lessons Learned

### <mark style="color:$warning;">8.20 POA\&Ms and Attack-Path-Informed Remediation</mark>&#xD;

* 8.20.1 Findings as Known Risk
* 8.20.2 Root Cause
* 8.20.3 Remediation Strategy and Milestones
* 8.20.4 Residual Risk
* 8.20.5 Prioritizing Paths Into Tier 0
* 8.20.6 Choke-Point Remediation
* 8.20.7 Closing a POA\&M Requires Technical Validation

### <mark style="color:$warning;">8.21 eMASS, SSPs, and Authorization Evidence</mark>&#xD;

* 8.21.1 Implementation Statements
* 8.21.2 Assessment Results
* 8.21.3 POA\&Ms and Artifacts
* 8.21.4 Common-Control Inheritance
* 8.21.5 System Security Plans
* 8.21.6 Identity Architecture and External Dependencies
* 8.21.7 Artifact Quantity Does Not Equal Assurance Quality

### <mark style="color:$warning;">8.22 Continuous Monitoring and Continuous Diagnostics Mitigation (CDM)</mark>&#xD;

* 8.22.1 Continuous Monitoring Is More Than Vulnerability Scanning
* 8.22.2 Asset, Identity, Credential, and Privilege State
* 8.22.3 Continuous Diagnostics and Mitigation
* 8.22.4 Configuration and Vulnerability State
* 8.22.5 Attack-Path State
* 8.22.6 Recovery Readiness
* 8.22.7 Mission Context

### <mark style="color:$warning;">8.23 Configuration Drift and Continuous Attack-Path Analysis</mark>&#xD;

* 8.23.1 Group Membership and ACL Drift
* 8.23.2 GPO and Authentication Policy Drift
* 8.23.3 Certificate and Federation Drift
* 8.23.4 Synchronization and Cloud Role Drift
* 8.23.5 Attackers Can Deliberately Create Drift
* 8.23.6 Recollecting the Graph After Change
* 8.23.7 Path Reduction as a Security Metric

### <mark style="color:$warning;">8.24 CCRI, CORA, and Independent Assessment Readiness</mark>&#xD;8.24.1 Identity Security as Operational Readiness&#xD; 8.24.2 Privileged Account Hygiene&#xD; 8.24.3 STIG and Vulnerability State&#xD; 8.24.4 Authentication and Account Management&#xD; 8.24.5 Audit Logging&#xD; 8.24.6 Inspector General and Independent Findings&#xD; 8.24.7 Findings as Threat-Hunting Inputs&#xD;<br>

### 8.25 Mission-Aware Change Control&#xD;

8.25.1 Normal, Emergency, and Security-Driven Change\
8.25.2 Privileged Change\
8.25.3 Rollback\
8.25.4 Evidence\
8.25.5 Post-Change Validation\
8.25.6 Recalculate Attack Paths After Significant Change\
8.25.7 Balance Mission Continuity and Security Integrity\
8.26 Evidence for Continuous Identity Assurance\
8.26.1 Successful and Failed Logons\
8.26.2 Privileged Authentication\
8.26.3 Kerberos and NTLM Activity\
8.26.4 Directory Modifications\
8.26.5 Certificate and Federation Events\
8.26.6 Microsoft Entra Sign-In and Audit Data\
8.26.7 Identity Correlation Across Sources\
8.27 Offensive and Defensive RMF Validation\
8.27.1 Offensive Testing Should Answer a Risk Question\
8.27.2 Demonstrate Preconditions and Consequence\
8.27.3 Determine Whether Existing Controls Detect the Activity\
8.27.4 Defensive Validation Confirms the Control and Telemetry\
8.27.5 Validate Response and Recovery\
8.27.6 Confirm Remediation Removed the Original Path\
8.27.7 Preserve Reproducible Evidence\
8.28 From Periodic Authorization to Continuous Risk Management\
8.28.1 Identity Relationships Change Faster Than Authorization Packages\
8.28.2 Evidence Must Become More Timely\
8.28.3 Significant Change Can Trigger Reassessment\
8.28.4 Active Exploitation Can Trigger Immediate Risk Response\
8.28.5 Automation Improves Timeliness but Does Not Replace Judgment\
8.28.6 Continuous Identity Assurance Supports Better Authorization\
8.29 Part I Synthesis\
8.29.1 Mission\
8.29.2 Governance\
8.29.3 FICAM and Identity Assurance\
8.29.4 FISCAM and Control Assurance\
8.29.5 Identity Trust\
8.29.6 Effective Authority\
8.29.7 Evidence and Risk\
8.29.8 Adversarial Validation\
8.29.9 Continuous Assurance\
8.30 Preparing for Part II\
8.30.1 From Governance to the Architecture of Authority\
8.30.2 Architecture Before Exploitation\
8.30.3 The Next Question Is Who Actually Controls What

* 8.1.1 Why the DoD Has Reconsidered the Traditional Risk Management Framework (RMF) Model
* 8.1.2 Point-In-Time Authorization Cannot Keep Pace With Operational Change
* 8.1.3 Static Compliance Evidence Versus Continuously Changing Cyber Risk
* 8.1.4 Cyber Survivability Changes the Risk Management Objective
* 8.1.5 Automation Changes How Security Evidence Is Produced and Consumed
* 8.1.6 CSRMC Reorganizes Rather Than Erases the Underlying Risk Management Framework Functions
* 8.1.7 NIST RMF Remains Foundational to Federal Risk Management
* 8.1.8 DoD Identity Security Must Be Taught in the Context of the CSRMC Transition

### <mark style="color:$warning;">8.2 Introduction to the Cybersecurity Risk Management Construct (CSRMC)</mark>

* 8.2.1 CSRMC as the DoD Operational Cyber Risk Construct
* 8.2.2 Continuous Rather Than Snapshot Risk Management
* 8.2.3 Cyber Defense at Operational Speed
* 8.2.4 Security Integrated Across System Development and Operations
* 8.2.5 Mission Risk and Cyber Survivability
* 8.2.6 Automated Evidence and Near-Real-Time Risk Visibility
* 8.2.7 Threat-Informed Testing Throughout the Entire Risk Management Lifecycle
* 8.2.8 Continuous Authorization as an Operational Condition

### <mark style="color:$warning;">8.3 The Five CSRMC Lifecycle Phases</mark>

* 8.3.1 Phase 1: Design
* 8.3.2 Phase 2: Build
* 8.3.3 Phase 3: Test
* 8.3.4 Phase 4: Onboard
* 8.3.5 Phase 5: Operations
* 8.3.6 Security Requirements Follow the System From Design Into Operations
* 8.3.7 Risk Is Reassessed as the System and Threat Environment Change

### <mark style="color:$warning;">8.4 Mapping RMF Activities Into the CSRMC Lifecycle</mark>

* 8.4.1 Prepare, Categorize, and Select Within the Design Phase
* 8.4.2 Implement Within the Build Phase
* 8.4.3 Assess Within the Test Phase
* 8.4.4 Authorized Within the Onboard Phase
* 8.4.5 Monitor Within the Operations Phase
* 8.4.6 RMF Activities Become Part of a Continuous Operational Cycle
* 8.4.7 Authorization Evidence Must Move With the System
* 8.4.8 Identity Risk Must Be Evaluated Across Every Phase

### <mark style="color:$warning;">8.5 The Ten Strategic Tenets of the CSRMC</mark>

* 8.5.1 Tenet 1: Automation
* 8.5.2 Tenet 2: Critical Controls
* 8.5.3 Tenet 3: Continuous Monitoring, Control, and Authorization to Operate (ATO)
* 8.5.4 Tenet 4: DevSecOps
* 8.5.5 Tenet 5: Cyber Survivability
* 8.5.6 Tenet 6: Training
* 8.5.7 Tenet 7: Enterprise Services and Inheritance
* 8.5.8 Tenet 8: Operationalization
* 8.5.9 Tenet 9: Reciprocity
* 8.5.10 Tenet 10: Cybersecurity Assessments and Threat-Informed Testing

### <mark style="color:$warning;">8.6 Continuous Authorization Changes the Meaning of an ATO</mark>

* 8.6.1 Traditional ATO as a Point-In-Time Risk Decision
* 8.6.2 Continuous Authorization to Operate (cATO), Interim Authorization to Operate (iATO), and Denied Authorization to Operate (dATO)
* 8.6.3 Continuous Monitoring Provides the Evidence Base
* 8.6.4 Automated Evidence Reduces the Delay Between Change and Risk Awareness
* 8.6.5 Critical Controls Require Persistent Visibility
* 8.6.6 Significant Risk Changes Must Affect Authorization Posture
* 8.6.7 Continuous Authorization Does Not Mean Permanent Authorization
* 8.6.8 Authorization Becomes a Continuously Supported Risk Condition

### <mark style="color:$warning;">8.7 Identity Security Under the CSRMC</mark>

* 8.7.1 Why Identity Becomes a Continuous Cyber-Risk Variable
* 8.7.2 How Privileged Relationships Change Between Formal Assessments
* 8.7.3 How Authentication Methods Change
* 8.7.4 How Certificates and Federation Trust Change
* 8.7.5 How Microsoft Entra Roles and Application Permissions Change
* 8.7.6 Why Synchronization Creates Cross-Control Plane Risk
* 8.7.7 How New Attack Pathways Can Appear Without a Major System Release
* 8.7.8 Why Identity Assurance Must Become Continuous

### <mark style="color:$warning;">8.8 Threat-Informed Testing Is Built Into the Risk Lifecycle</mark>

* 8.8.1 Control Testing Must Reflect Credible Adversary Behavior
* 8.8.2 Penetration Testing for High-Risk Federal AD Systems
* 8.8.3 Attack-Path Analysis
* 8.8.4 Adversarial Validation
* 8.8.5 Mission-Relevant Threat Scenarios
* 8.8.6 Detection Validation
* 8.8.7 Recovery and Survivability Testing
* 8.8.8 Offensive Testing Becomes Risk Evidence Rather Than a Separate Activity

### <mark style="color:$warning;">8.9 Authorization Boundaries and Identity Dependencies</mark>

* 8.9.1 System Boundary Versus Identity Boundary: Technical Delineation
* 8.9.2 Active Directory and Public Key Infrastructure (PKI) Architectural Dependencies
* 8.9.3 Identity Federation Trust Boundaries and Microsoft Entra ID Integration
* 8.9.4 Directory Synchronization Mechanics and Automated Provisioning Pipelines
* 8.9.5 Cross-Boundary Privileged Administration Pathways and Risk Vectors
* 8.9.6 Identity Repository Backup, Disaster Recovery, and State Integrity
* 8.9.7 Uncovering Hidden Tier 0 Assets and Implicit Administrative Control
* 8.9.8 Adversary Dynamics: Why Attackers Ignore Static Authorization Diagrams

### <mark style="color:$warning;">8.10 Security Categorization and Identity Mission Consequence</mark>

* 8.10.1 Assessing Confidentiality Impact Across Enterprise Identity Data Stores
* 8.10.2 Evaluating Integrity Degradation in Authentication and Directory Services
* 8.10.3 Analyzing Availability Impact and Denial of Service (DoS) in Core Identity Infrastructure
* 8.10.4 Classifying Enterprise Identity Infrastructure as Critical Mission Assets
* 8.10.5 Operational Consequence Analysis of Systemic Authentication and Authorization Failure
* 8.10.6 Systemic Blast Radius: Managing the Complete Loss of Enterprise Identity Trust
* 8.10.7 How Identity Integrity Failure Allows Adversaries to Manufacture Authority

### <mark style="color:$warning;">8.11 Security Control Selection and Identity Risk</mark>

* 8.11.1 Mapping NIST SP 800-53 Security and Privacy Controls to Identity Architectures
* 8.11.2 Selecting and Allocating Security Control Baselines (Low, Moderate, High)
* 8.11.3 Tailoring Control Allocations to Match Technical Identity Realities
* 8.11.4 Applying Specialized Identity Overlays for High-Assurance Environments
* 8.11.5 Assessing the Technical Validity of Identity-Focused Compensating Controls
* 8.11.6 Leveraging Common Controls and Enterprise Shared Identity Provider Services
* 8.11.7 Aligning Control Selection Directly to the Identity Attack Surface

### <mark style="color:$warning;">8.12 Identity-Relevant NIST SP 800-53 Control Families</mark>

* 8.12.1 Access Control (AC): Enforcing Technical Authorization Policies
* 8.12.2 Identification and Authorization (IA): Verifying Credentials and Principal Identity
* 8.12.3 Audit and Accountability (AA): Capturing Identity Events and Telemetry
* 8.12.4 Configuration Management (CM): Hardening Directory and Identity Configurations
* 8.12.5 System and Communications Protection (SC): Securing Identity Transport and Trust Bounds
* 8.12.6 System and Information Integrity (SI): Detecting Identity Tampering and Anomalies
* 8.12.7 Incident Response (IR) and Contingency Planning (CP): Identity Disaster Recovery
* 8.12.8 Risk Assessment (RA), Security Assessment (CA), and Supply Chain (SR) Controls

### <mark style="color:$warning;">8.13 Control Implementation: From Requirements to Technical State</mark>

* 8.13.1 Engineering Authentication and Authorization Control Mechanisms
* 8.13.2 Implementing Technical Privileged Access Management (PAM) Safeguards
* 8.13.3 Hardening Active Directory Objects, Organizational Units (OUs), and Group Policy Objects (GPOs)
* 8.13.4 Deploying Certificate-Based Authentication and PKI Cryptographic Controls
* 8.13.5 Securing Identity Federation Engines and Cloud Synchronization Connectors
* 8.13.6 Orchestrating High-Fidelity Logging and System Recovery Architectures
* 8.13.7 Writing Measurable and Testable Control Implementation Statements
* 8.13.8 Verifying Effective Technical Authority Matches Documented System State

### <mark style="color:$warning;">8.14 Common Controls, Inheritance, and Shared Identity Services</mark>

* 8.14.1 Designating Centralized Identity Systems as Enterprise Common Controls
* 8.14.2 Assessing the Assurance Posture of Common-Control Providers
* 8.14.3 Managing Technical Boundaries in Partial Control Inheritance Models
* 8.14.4 Security Architecture for Shared Identity and Single Sign-On (SSO) Services
* 8.14.5 Cascading Failure Risk: Systemic Exposure in Shared Common Controls
* 8.14.6 Maintaining Visibility of Inherited Technical Identity Risk Across Downstream Systems
* 8.14.7 Defining Mission-Partner Responsibilities: Why Inheritance Does Not Relieve System Owners

### <mark style="color:$warning;">8.15 DISA STIGs, SRGs, and Technical Baselines</mark>

* 8.15.1 Applying Security Technical Implementation Guides (STIGs) to Identity Infrastructure
* 8.15.2 Aligning System Designs with Defense-In-Depth Security Requirements Guides (SRGs)
* 8.15.3 Defining the Expected Technical Configuration State across Domain Controllers
* 8.15.4 Categorizing Finding Severities (CAT I, CAT II, CAT III) for Identity Deficiencies
* 8.15.5 Documenting Technically Sound Applicability and Not-Applicable (N/A) Justifications
* 8.15.6 Balancing Automated Compliance Scans with Deep Manual Assessor Inspections
* 8.15.7 Evaluating Mitigation Mechanics in STIG Exceptions and Mitigation Statements
* 8.15.8 Why Baseline STIG Compliance Alone Fails to Eliminate Attack Paths

### <mark style="color:$warning;">8.16 Assessment and Technical Validation</mark>

* 8.16.1 Examine: Rigorous Documentation, Configuration, and Architectural Artifact Review
* 8.16.2 Interview: Questioning System Administrators and Identity Engineers
* 8.16.3 Test: Direct Execution, Technical Probing, and Empirical Control Verification
* 8.16.4 Executing Hands-On Technical Validation of Active Identity Safeguards
* 8.16.5 Uncovering Discrepancies Between Static Configuration and Effective Running State
* 8.16.6 Evaluating Effective Technical Authority via Directory Inspection Scripts
* 8.16.7 Collection Criteria for Timely, Authentic, and Reproducible Audit Evidence
* 8.16.8 Ensuring Assessor Finding Conclusions Are Directly Supported by Collected Evidence

### <mark style="color:$warning;">8.17 Attack Pathways as Risk and Authorization Evidence</mark>

* 8.17.1 Analyzing Credential Reachability and Exposure Across System Boundaries
* 8.17.2 Mapping Administrative Reachability and Lateral Movement Pathways
* 8.17.3 Evaluating Transitive Privilege Chains and Unintended Access Relationships
* 8.17.4 Measuring Tier 0 Infrastructure Exposure to Standard User Compromise
* 8.17.5 Assessing Cross-System and Cross-Cloud-Plane Identity Dependencies
* 8.17.6 Translating Technical Graph Exposure Into Mission Consequence Statements
* 8.17.7 Identifying Critical Attack-Path Choke Points for Strategic Defensive Intervention
* 8.17.8 Demonstrating Measurable Risk Reduction via Attack-Path Severance

### <mark style="color:$warning;">8.18 Authorization and the Authorizing Official (AO)</mark>

* 8.18.1 Formalizing System Authorization as an Executive Risk Acceptance Decision
* 8.18.2 Validating Authorization Package Integrity, Accuracy, and Completeness
* 8.18.3 Evaluating Residual Identity Exposure Prior to Granting an ATO
* 8.18.4 Establishing Formal Conditions of Authorization (COA) for Identified Identity Risks
* 8.18.5 Quantifying Operational Risk Passed Down Through Inherited Identity Services
* 8.18.6 Articulating Achievable Adversary Authority to Authorizing Officials
* 8.18.7 Transparently Explaining Detection Latency and Incident Recovery Complexity
* 8.18.8 Mandating That Authorization Status Remains Backed by Continuous Technical Evidence

### <mark style="color:$warning;">8.19 Vulnerability Management and Identity Risk</mark>

* 8.19.1 Contextualizing Vulnerability CVSS Severity Against Identity Mission Impact
* 8.19.2 Operationalizing Information Assurance Vulnerability Alerts (IAVAs) in Identity Systems
* 8.19.3 Processing Information Assurance Vulnerability Bulletins (IAVBs) Across Directories
* 8.19.4 Prioritizing CISA Known Exploited Vulnerabilities (KEV) Affecting Identity Platforms
* 8.19.5 Evaluating Vulnerability Exposure on Tier 0 Domain Controllers and Identity Hubs
* 8.19.6 Performing Trust-Boundary Analysis to Determine Vulnerability Blast Radius
* 8.19.7 Dependency-Aware Remediation: Patching Core Identity Nodes Without Outages
* 8.19.8 Why Applying Software Patches Does Not Automatically Sever Graph Attack Paths

### <mark style="color:$warning;">8.20 Plans of Action and Milestones (POA\&M) and Attack-Path-Informed Remediation</mark>

* 8.20.1 Documenting Identified Identity Deficiencies as Formal Risk Findings
* 8.20.2 Performing Root-Cause Analysis Beyond Surface-Level System Configurations
* 8.20.3 Developing Attack-Path-Informed Remediation Strategies for POA\&Ms
* 8.20.4 Structuring Measurable Remediation Milestones and Binding Deadlines
* 8.20.5 Re-calculating Expected Residual Risk Upon Milestone Completion
* 8.20.6 Prioritizing POA\&M Execution Based on Paths Leading to Tier 0 Assets
* 8.20.7 Maximizing Remediation Efficiency via Choke-Point Elimination
* 8.20.8 Requiring Independent Technical Re-Testing Before Formal POA\&M Finding Closure

### <mark style="color:$warning;">8.21 eMASS, SSPs, and Authorization Evidence</mark>

* 8.21.1 Structuring the System Security Plan (SSP) around Identity Control Architecture
* 8.21.2 Authoring Precise, Testable Control Implementation Statements in eMASS
* 8.21.3 Ingesting Assessment Results and Artifact Evidence into Authorization Repositories
* 8.21.4 Managing POA\&M Tracking and Verification Status within eMASS
* 8.21.5 Mapping and Auditing Common-Control Inheritance Relationships in eMASS
* 8.21.6 Documenting Hybrid Identity Architecture and External Cloud Dependencies
* 8.21.7 Uploading High-Quality Technical Supporting Artifacts (Scripts, Logs, Configurations)
* 8.21.8 Quality vs. Quantity: Why Massive Artifact Dumps Do Not Equal Control Assurance

### <mark style="color:$warning;">8.22 Continuous Monitoring and Continuous Diagnostics and Mitigations (CDM)</mark>

* 8.22.1 Evolving Continuous Monitoring Beyond Passive Vulnerability Scanning
* 8.22.2 Tracking Real-Time Asset Discovery and Identity Association States
* 8.22.3 Continuous Monitoring of Credential Strength, Lifecycle, and Privilege States
* 8.22.4 Auditing System Configuration Baseline Drift and Vulnerability Posture
* 8.22.5 Integrating CISA Continuous Diagnostics and Mitigation (CDM) Sensors
* 8.22.6 Dynamic Attack-Path Graph Monitoring Across Enterprise Directories
* 8.22.7 Validating Backup Integrity and Disaster Recovery Readiness Continuously
* 8.22.8 Maintaining Real-Time Mission Context in Security Information Systems

### <mark style="color:$warning;">8.23 Configuration Drift and Continuous Attack-Path Analysis</mark>

* 8.23.1 Detecting Unauthorized Group Membership Changes and DACL/SACL Drift
* 8.23.2 Monitoring Group Policy Object (GPO) and Authentication Policy Drift
* 8.23.3 Auditing Public Key Infrastructure Certificate and Federation Trust Drift
* 8.23.4 Tracking Azure AD/Entra Directory Synchronization and Cloud Role Drift
* 8.23.5 Identifying Unmonitored Administrative Dependency and Delegation Drift
* 8.23.6 Adversarial Drift Creation: Detecting Stealthy Attacker-Planted Persistence Paths
* 8.23.7 Automated Recalculation of the Enterprise Attack Graph Following Major Drift
* 8.23.8 Establishing Attack-Path Reduction as a Core Enterprise Security Metrics

### <mark style="color:$warning;">8.24 Mission-Aware Change Control and Operational Readiness</mark>

* 8.24.1 Governing Normal, Emergency, and Security-Driven Infrastructure Changes
* 8.24.2 High-Assurance Controls Surrounding Privileged System Changes
* 8.24.3 Developing Reliable System State Rollback Procedures for Failed Changes
* 8.24.4 Post-Implementation Validation Protocols for Identity Infrastructure Changes
* 8.24.5 Preparing for Command Cyber Readiness Inspections (CCRI)
* 8.24.6 Navigating Cyber Operational Readiness Assessments (CORA) and Independent Audits
* 8.24.7 Utilizing Operational Assessment Findings as Inputs for Defensive Threat-Hunting
* 8.24.8 Assessing How Significant Infrastructure Changes Alter System Risk Posture

### <mark style="color:$warning;">8.25 Evidence for Continuous Identity Assurance</mark>

* 8.25.1 Collecting and Analyzing High-Fidelity User Authentication Event Logs
* 8.25.2 Auditing Privileged Authentication Sequences and Administrative Logons
* 8.25.3 Monitoring Legacy Protocol Telemetry (Kerberos Delegation, NTLM Usage)
* 8.25.4 Real-Time Tracking of Directory Modifications and Privilege Escalations
* 8.25.5 Ingesting PKI Certificate Lifecycle and Federation Assertion Audit Trails
* 8.25.6 Processing Microsoft Entra ID Interactive Sign-In and System Audit Telemetry
* 8.25.7 Cross-Source Correlation of Identity Telemetry Across On-Premises and Cloud
* 8.25.8 Using Telemetry Evidence to Prove That Accepted Risk Assumptions Remain Valid

### <mark style="color:$warning;">8.26 From Periodic Authorization to Continuous Identity Assurance</mark>

* 8.26.1 Velocity Mismatch: Identity Relationships Evolve Faster Than Static Authorization Packages
* 8.26.2 Transitioning to Real-Time and Automated Evidence Collection Pipelines
* 8.26.3 Defining System Boundary and Identity Architecture Triggers for Reassessment
* 8.26.4 Operationalizing Immediate Risk Response Triggers During Active Exploitation Events
* 8.26.5 Leveraging Automation for Timeliness While Retaining Human Engineering Judgment
* 8.26.6 Threat-Informed Testing: Utilizing Adversarial Penetration Testing as Risk Evidence
* 8.26.7 Continuous Revalidation of Disaster Recovery and Key Rebinding Readiness
* 8.26.8 Operationalizing Continuous Identity Assurance to Drive Continuous ATO (cATO)

### <mark style="color:$warning;">8.27 RMF, CSRMC, and Continuous Identity Assurance Principles</mark>

* 8.27.1 Aligning RMF Execution Directly with Cyber Supply Chain Risk Management (C-SCRM) Governance
* 8.27.2 Enforcing Continuous Verification of Identity Control Effectiveness Over Paper Compliance
* 8.27.3 Eliminating Structural Blind Spots Across Hybrid Identity and Cross-Cloud Boundaries
* 8.27.4 Treating Identity Infrastructure as Primary Mission Infrastructure in Risk Decisions
* 8.27.5 Sustaining Continuous Risk-Based Authorization Backed by Real-Time Technical Evidence



### Author Chapter Notes

The last point (8.8.8 Offensive Testing Becomes Risk Evidence Rather Than a Separate Activity) is especially important for Contested Terrain. CSRMC actually strengthens the rationale for the architecture of the book: DoD is explicitly moving toward threat-informed testing, continuous assessment, automation, cyber survivability, and operational risk visibility - the same reason I have been integrating offensive and defensive identity analysis rather than treating pentesting as something that is disconnected from governance.

Abstract should begin with:&#x20;

_"In September 2025, the Department of Defense announced implementation of the Cybersecurity Risk Management Construct (CSRMC) as its new approach to cybersecurity risk management, shifting the Department from predominantly point-in-time RMF execution toward automated, threat-informed, continuously monitored risk management and authorization."_

This is stronger for publication because it says exactly what the DoD source supports without implying that DoDI 8510.01 and the underlying NIST RMF architecture have already ceased to apply everywhere. As of 2026, they have not.
