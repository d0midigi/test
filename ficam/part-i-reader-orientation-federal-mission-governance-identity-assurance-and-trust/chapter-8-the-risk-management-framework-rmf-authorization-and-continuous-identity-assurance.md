# Chapter 8 - The Risk Management Framework (RMF), Authorization, and Continuous Identity Assurance

### Abstract

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
