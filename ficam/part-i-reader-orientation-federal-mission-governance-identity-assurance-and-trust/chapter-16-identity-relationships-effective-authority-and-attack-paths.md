# Chapter 16 - Identity Relationships, Effective Authority, and Attack Paths

## Chapter 16 — Identity Relationships, Effective Authority, and Attack Paths

### Chapter Abstract

Identity compromise becomes operationally significant through relationships. A user, computer, service, application, workload, credential, or management system may appear individually low risk yet participate in a chain that ultimately reaches privileged authority. This chapter examines how direct, indirect, transitive, credential-based, administrative, ownership, delegation, management, recovery, and hybrid relationships combine into Active Directory attack paths. Readers learn to model principals and resources as graph nodes, control relationships as edges, distinguish assigned privilege from effective authority, identify hidden Tier 0 dependencies, and recognize choke points where multiple attack paths converge. Offensive analysis focuses on locating practical routes to mission-relevant authority rather than simply targeting obvious privileged groups. Defensive analysis emphasizes relationship inventory, attack-path validation, tier enforcement, telemetry, graph hygiene, drift detection, and remediation by breaking critical edges. The chapter establishes attack-path analysis as a practical method for understanding who can control whom, how authority propagates, and where defenders can most efficiently reduce identity-centric mission risk.

***

### 16.1 Identity Security Is Relational

#### 16.1.1 An Identity Alone Does Not Describe Its Risk

#### 16.1.2 Authority Emerges From Relationships

#### 16.1.3 Principals Control Resources

#### 16.1.4 Principals Can Control Other Principals

#### 16.1.5 Systems Can Control Identities

#### 16.1.6 Relationships Can Cross Technologies and Administrative Boundaries

#### 16.1.7 Attackers Think in Paths

#### 16.1.8 Defenders Must Learn to Think in Paths

### 16.2 Assigned Privilege Versus Effective Authority

#### 16.2.1 Assigned Privilege Is the Visible Layer

#### 16.2.2 Effective Authority Includes Indirect Control

#### 16.2.3 Ownership Can Create Authority

#### 16.2.4 Delegation Can Create Authority

#### 16.2.5 Credential Access Can Create Authority

#### 16.2.6 System Administration Can Create Authority

#### 16.2.7 Recovery Capability Can Create Authority

#### 16.2.8 Attackers Care About What Can Actually Be Controlled

### 16.3 Direct and Indirect Control Relationships

#### 16.3.1 Direct Group Membership

#### 16.3.2 Direct Directory Permissions

#### 16.3.3 Local Administrative Rights

#### 16.3.4 Cloud and Application Roles

#### 16.3.5 Indirect Control Through Another Principal

#### 16.3.6 Indirect Control Through a Host or Service

#### 16.3.7 Indirect Authority Can Be Equivalent to Explicit Administrative Membership

#### 16.3.8 Relationship Analysis Must Include Both Forms

### 16.4 Transitive Authority

#### 16.4.1 A Controls B and B Controls C

#### 16.4.2 Transitivity Creates Attack Paths

#### 16.4.3 Not Every Relationship Is Automatically Transitive

#### 16.4.4 Technical Preconditions Determine Path Validity

#### 16.4.5 Several Weak Relationships Can Form a Strong Path

#### 16.4.6 Path Length Does Not Determine Importance

#### 16.4.7 Attackers Evaluate the Entire Chain

#### 16.4.8 Defenders Must Validate the Entire Chain

***

## DIRECTORY AND HOST RELATIONSHIPS

### 16.5 Groups, ACLs, and Ownership as Control Edges

#### 16.5.1 Direct and Nested Group Membership

#### 16.5.2 Foreign Security Principals and SIDHistory

#### 16.5.3 Directory ACLs

#### 16.5.4 Password Reset and Membership Control

#### 16.5.5 `GenericAll`, `GenericWrite`, `WriteDACL`, and `WriteOwner`

#### 16.5.6 Object Ownership

#### 16.5.7 Replication and Extended Rights

#### 16.5.8 Directory Permission Relationships Become Graph Edges

### 16.6 Computer, Service, and Application Relationships

#### 16.6.1 Computer Accounts Are Both Principals and Resources

#### 16.6.2 Local Administrator Relationships

#### 16.6.3 Machine-Account and Delegation Relationships

#### 16.6.4 Service Accounts Bridge Systems

#### 16.6.5 gMSA Retrieval Rights

#### 16.6.6 Application Permissions and Service Principals

#### 16.6.7 Managed and Workload Identities

#### 16.6.8 Nonhuman Identities Can Form Durable Privilege Paths

### 16.7 Credential and Session Relationships

#### 16.7.1 Credential Access Creates Potential Identity Control

#### 16.7.2 Passwords and Hashes

#### 16.7.3 Kerberos Tickets and Keys

#### 16.7.4 Certificates and Private Keys

#### 16.7.5 Cloud Tokens

#### 16.7.6 Vault and Recovery Access

#### 16.7.7 Active Sessions Create Dynamic Relationships

#### 16.7.8 Credential Placement Can Reverse Expected Administrative Direction

***

## ADMINISTRATIVE CONTROL PLANE

### 16.8 Administrative Workstations and Privileged Sessions

#### 16.8.1 Administrators Carry Authority Onto Endpoints

#### 16.8.2 Authentication Creates Credential Placement

#### 16.8.3 Session Control Can Become Identity Control

#### 16.8.4 Compromising the Administrator May Not Be Necessary

#### 16.8.5 Compromising the Administrative Workstation May Be Enough

#### 16.8.6 Privileged Access Workstations Break Important Paths

#### 16.8.7 Authentication Placement Is an Attack-Path Design Issue

### 16.9 Management and Security Platforms

#### 16.9.1 Endpoint Management

#### 16.9.2 Software Deployment

#### 16.9.3 Configuration Management

#### 16.9.4 Patch and Remote Administration

#### 16.9.5 EDR, SIEM, and Security Platforms

#### 16.9.6 Automation and Orchestration

#### 16.9.7 The Manager May Be More Valuable Than the Managed Asset

#### 16.9.8 A Platform That Controls Tier 0 May Itself Become Tier 0

### 16.10 Virtualization, Backup, and Recovery Authority

#### 16.10.1 Hypervisor Administration

#### 16.10.2 Console, Snapshot, Disk, and Memory Access

#### 16.10.3 Backup Administration

#### 16.10.4 Restore Rights

#### 16.10.5 System-State and Identity Backups

#### 16.10.6 Recovery Accounts and Recovery Platforms

#### 16.10.7 Recovery Authority Is Effective Administrative Authority

#### 16.10.8 Recovery Infrastructure Belongs in the Identity Graph

***

## CROSS-PLANE AUTHORITY

### 16.11 PKI, Federation, Synchronization, and Cloud Relationships

#### 16.11.1 Certification Authorities Create Identity Assertions

#### 16.11.2 Certificate Templates Create Enrollment Relationships

#### 16.11.3 Federation Extends Authentication Upstream

#### 16.11.4 Signing Keys Represent Assertion Authority

#### 16.11.5 Synchronization Moves Identity State Between Systems

#### 16.11.6 Writeback Can Create Reverse Authority

#### 16.11.7 Cloud Roles and Applications Extend the Control Plane

#### 16.11.8 Hybrid Attack Paths Can Cross Several Identity Systems

***

## GRAPH MODELING

### 16.12 Thinking in Nodes and Edges

#### 16.12.1 Nodes Represent Security-Relevant Objects

#### 16.12.2 Edges Represent Relationships

#### 16.12.3 Direction Matters

#### 16.12.4 Edge Meaning Matters

#### 16.12.5 Edge Preconditions Matter

#### 16.12.6 Graphs Simplify Complexity Without Eliminating Analysis

#### 16.12.7 Graphing Does Not Replace Operator Judgment

### 16.13 Identity Graph Nodes and Relationship Types

#### 16.13.1 Users and Groups

#### 16.13.2 Computers and Services

#### 16.13.3 Applications and Workloads

#### 16.13.4 Policies and Management Systems

#### 16.13.5 Certificate Authorities and Identity Providers

#### 16.13.6 Recovery and Backup Systems

#### 16.13.7 Member Of, Admin To, Owns, Can Modify, and Can Reset

#### 16.13.8 Can Execute, Retrieve, Enroll, Delegate, Synchronize, or Restore

### 16.14 Anatomy of an Attack Path

#### 16.14.1 Entry Node

#### 16.14.2 Intermediate Control

#### 16.14.3 Privilege Escalation

#### 16.14.4 Lateral Movement

#### 16.14.5 Credential Access

#### 16.14.6 Final Authority

#### 16.14.7 Mission Consequence

#### 16.14.8 A Path Is Valuable Only If Its Relationships Are Usable

### 16.15 Attack-Path Preconditions

#### 16.15.1 Network Reachability

#### 16.15.2 Authentication Capability

#### 16.15.3 Required Privilege

#### 16.15.4 User Interaction

#### 16.15.5 Credential Presence

#### 16.15.6 Service and Host Configuration

#### 16.15.7 Timing and Operational State

#### 16.15.8 A Graph Edge Without Its Preconditions Can Overstate Risk

### 16.16 Path Cost, Probability, and Confidence

#### 16.16.1 Technical Complexity

#### 16.16.2 Reliability

#### 16.16.3 Noise and Detection Exposure

#### 16.16.4 Time and User Interaction

#### 16.16.5 Credential Requirements

#### 16.16.6 Observed Versus Theoretical Paths

#### 16.16.7 Technical Validation Increases Confidence

#### 16.16.8 Attackers Prefer Reliable Paths, Not Merely Short Paths

***

## TIER 0 AND TRUST INVERSION

### 16.17 Tier 0 as a Relationship Problem

#### 16.17.1 Tier 0 Is Not Merely a List of Systems

#### 16.17.2 Anything That Can Control Tier 0 May Become Tier 0

#### 16.17.3 Credential Authority Can Extend Tier 0

#### 16.17.4 Management Authority Can Extend Tier 0

#### 16.17.5 Recovery and Virtualization Can Extend Tier 0

#### 16.17.6 PKI and Cloud Authority Can Extend Tier 0

#### 16.17.7 Tier 0 Must Be Discovered Through Effective Control

### 16.18 Hidden Tier 0 and the Clean Source Principle

#### 16.18.1 Backup Platforms

#### 16.18.2 Hypervisors

#### 16.18.3 Software Deployment

#### 16.18.4 Endpoint and Security Management

#### 16.18.5 PKI and Synchronization

#### 16.18.6 Administrative Repositories and Automation

#### 16.18.7 A Lower-Tier Dependency Can Create Trust Inversion

#### 16.18.8 The Administrative Source Must Be at Least as Trusted as the Target

***

## OFFENSIVE ATTACK-PATH ANALYSIS

### 16.19 Attack Objectives and Initial Nodes

#### 16.19.1 Domain Admin Is Not Always the Objective

#### 16.19.2 Mission-System Control May Be Enough

#### 16.19.3 Certificate or Backup Authority May Be Enough

#### 16.19.4 Application or Cloud Authority May Be Enough

#### 16.19.5 Compromised User

#### 16.19.6 Compromised Workstation or Server

#### 16.19.7 Service, Application, or External Identity

#### 16.19.8 The Objective Should Define the Path Search

### 16.20 Privilege-Escalation, Lateral-Movement, and Credential Paths

#### 16.20.1 Group Paths

#### 16.20.2 ACL and Ownership Paths

#### 16.20.3 Delegation Paths

#### 16.20.4 Local Administrative Paths

#### 16.20.5 Credential-Reuse Paths

#### 16.20.6 Service and Management Paths

#### 16.20.7 PKI, Cloud, and Recovery Paths

#### 16.20.8 Several Path Types Often Combine in One Operation

### 16.21 Choke Points and Path Diversity

#### 16.21.1 Many Paths Can Converge on One Relationship

#### 16.21.2 Group Choke Points

#### 16.21.3 Management-System Choke Points

#### 16.21.4 Credential and PKI Choke Points

#### 16.21.5 Removing One Path May Leave Several Others

#### 16.21.6 Independent Paths Increase Adversary Resilience

#### 16.21.7 Shared Preconditions Reveal Better Remediation Targets

#### 16.21.8 Choke-Point Removal Can Collapse Large Portions of the Graph

***

## DEFENSIVE ATTACK-PATH ENGINEERING

### 16.22 Build the Defender's Graph

#### 16.22.1 Start With High-Value Assets

#### 16.22.2 Work Backward From Authority

#### 16.22.3 Identify Direct and Indirect Administrators

#### 16.22.4 Identify Credential Readers

#### 16.22.5 Identify Management and Recovery Systems

#### 16.22.6 Identify External Trust and Hybrid Dependencies

#### 16.22.7 Continue Until the Boundary Is Defensible

#### 16.22.8 Documentation Should Reflect Effective, Not Intended, Authority

### 16.23 Baseline Effective Authority and Detect Drift

#### 16.23.1 Expected Privileged Paths

#### 16.23.2 Approved Delegation

#### 16.23.3 Approved Management and Recovery Paths

#### 16.23.4 Approved Cross-Boundary Relationships

#### 16.23.5 New Groups, ACLs, Roles, or Integrations Create New Edges

#### 16.23.6 Credential Placement Creates Dynamic Drift

#### 16.23.7 One New Edge Can Change the Entire Risk Model

#### 16.23.8 Continuous Collection Is Required for Continuous Understanding

### 16.24 Breaking and Prioritizing Attack Paths

#### 16.24.1 Remove the Edge

#### 16.24.2 Restrict the Edge

#### 16.24.3 Remove Credential Exposure

#### 16.24.4 Separate Administrative Tiers

#### 16.24.5 Replace Shared Identity

#### 16.24.6 Harden the Choke Point

#### 16.24.7 Improve Detection When the Relationship Cannot Be Removed

#### 16.24.8 Prioritize by Destination Value, Exposure, Reliability, and Mission Consequence

#### 16.24.9 Remediation Should Maximize Risk Reduction per Change

***

## TELEMETRY AND DETECTION

### 16.25 Relationship Telemetry

#### 16.25.1 Group Membership Changes

#### 16.25.2 ACL and Ownership Changes

#### 16.25.3 GPO and Delegation Changes

#### 16.25.4 Computer and Service Identity Changes

#### 16.25.5 Certificate and Application Permission Changes

#### 16.25.6 Cloud Role Changes

#### 16.25.7 Recovery and Management Configuration Changes

#### 16.25.8 Relationship Changes Can Be More Important Than Malware Indicators

### 16.26 Attack-Path-Aware Detection Engineering

#### 16.26.1 Authentication Data Creates Dynamic Graph Context

#### 16.26.2 Who Authenticated Where?

#### 16.26.3 Which Privileged Identities Touch Which Systems?

#### 16.26.4 Detect Path Construction

#### 16.26.5 Detect Path Activation

#### 16.26.6 Detect Path Persistence

#### 16.26.7 Choke Points Produce High-Value Telemetry

#### 16.26.8 Graph Context Can Improve Alert Prioritization

***

## TOOLING AND VALIDATION

### 16.27 Attack-Path Enumeration and BloodHound

#### 16.27.1 Native Directory Queries

#### 16.27.2 PowerShell and LDAP

#### 16.27.3 BloodHound Graph Representation

#### 16.27.4 Nodes and Edges

#### 16.27.5 Path Queries

#### 16.27.6 High-Value Targets

#### 16.27.7 Choke Points and Effective Control

#### 16.27.8 Microsoft and Other Identity-Security Telemetry

#### 16.27.9 No Single Tool Sees the Entire Identity Trust System

### 16.28 Collection Quality, False Positives, and False Confidence

#### 16.28.1 Incomplete Collection Produces Incomplete Graphs

#### 16.28.2 Stale Collection Produces Stale Conclusions

#### 16.28.3 Sessions and Local Groups Change Rapidly

#### 16.28.4 Cloud Roles and Applications Change Rapidly

#### 16.28.5 An Edge Is Not Automatically an Exploit

#### 16.28.6 Network, Version, and Configuration Matter

#### 16.28.7 A Missing Edge Does Not Prove No Relationship Exists

#### 16.28.8 Manual Validation Remains Necessary

***

## FEDERAL, DOD, AND INCIDENT RESPONSE

### 16.29 Federal/DoD Attack-Path Assurance and Incident Response

#### 16.29.1 Attack Paths Translate Effective Authority Into Mission Risk

#### 16.29.2 Attack Paths Can Support RMF Assessment

#### 16.29.3 Attack Paths Can Support Continuous Monitoring

#### 16.29.4 Attack Paths Can Support POA\&M Prioritization

#### 16.29.5 Cross-Enclave and Mission-Partner Dependencies Must Be Modeled

#### 16.29.6 Compromise Scope Is a Graph Question

#### 16.29.7 Blast Radius Is Effective Reach, Not Subnet Size

#### 16.29.8 Containment Should Break the Adversary's Available Paths

#### 16.29.9 Recovery Must Validate That Malicious Relationships No Longer Exist

### 16.30 Offensive/Defensive Synthesis and Preparing for Chapter 17

#### 16.30.1 Offensive Validation Should Prove Useful Authority, Not Chase Prestige Privilege

#### 16.30.2 Validate Preconditions Before Exploitation

#### 16.30.3 Demonstrate Consequence With Minimal Mission Impact

#### 16.30.4 Record the Exact Relationship That Failed

#### 16.30.5 Defensive Validation Must Recollect the Environment

#### 16.30.6 Closing a Finding Does Not Prove the Path Is Gone

#### 16.30.7 Metrics Should Measure Path Reduction, Choke Points, and Reachable Authority

#### 16.30.8 The Graph Is Never Finished

**16.30.9 Attacker Journal — The Shortest Path Was Not the Best Path**

A graph may reveal a short route toward privileged authority, yet that route may require touching a heavily monitored Tier 0 system. A longer path through an overlooked service identity, management platform, or administrative session may be more reliable and less observable.

The attacker evaluates operational cost, not simply hop count.

**16.30.10 Defender Journal — Remove the Choke Point, Not Fifty Symptoms**

Dozens of attack paths may appear to require dozens of unrelated fixes. If most converge on one management platform, credential relationship, delegation, or administrative group, correcting that choke point can eliminate much of the reachable graph at once.

**16.30.11 Field Note — Ask Who Can Control the Administrator**

“Who are the administrators?” is too narrow.

Also ask:

Who can modify those administrators? Who can reset their credentials? Who can control their workstations? Who can change the groups containing them? Who can issue them another credential? Who can restore systems containing their secrets? Who can administer the management platforms that administer their targets?

The first question produces an administrator list.

The rest produce the actual security boundary.

**16.30.12 From Internal Authority to Cross-Boundary Trust**

Chapter 16 established how authority propagates through relationships inside and across identity systems. The next chapter extends that graph beyond a single domain, forest, tenant, or administrative boundary.

**16.30.13 The Next Question**

**When one identity environment trusts another, exactly what crosses that boundary—and what can an attacker carry with it?**
