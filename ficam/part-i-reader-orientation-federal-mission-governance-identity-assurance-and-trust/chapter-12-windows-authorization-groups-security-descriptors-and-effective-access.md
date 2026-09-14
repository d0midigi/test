# Chapter 12 — Windows Authorization, Groups, Security Descriptors, and Effective Access

### Abstract

Authentication establishes who or what a principal claims to be; authorization determines what that principal can actually do. This chapter examines the Windows authorization model from security identifiers, access tokens, groups, privileges, user rights, security descriptors, discretionary and system access-control lists, access-control entries, inheritance, ownership, Mandatory Integrity Control, User Account Control, and object-specific Active Directory permissions through effective access and delegated authority. Offensive analysis focuses on permission relationships that create privilege escalation, shadow administration, indirect control, token abuse, ownership paths, group nesting, delegated directory rights, and authorization through computers, services, Group Policy, and management infrastructure. Defensive analysis emphasizes least privilege, role separation, administrative tiering, effective-access review, permission baselining, drift detection, telemetry, and attack-path reduction. The chapter establishes a central principle for Windows security: assigned roles and group names do not define authority. Effective authority is determined by the complete set of permissions, identities, tokens, ownership relationships, and control paths Windows evaluates when access is requested.

***

### 12.1 Authentication Ends Where Authorization Begins

#### 12.1.1 Authentication Establishes Identity

#### 12.1.2 Authorization Evaluates Requested Access

#### 12.1.3 Authentication Success Does Not Imply Resource Access

#### 12.1.4 Authorization Occurs Repeatedly After Logon

#### 12.1.5 The Same Principal Can Have Different Authority on Different Resources

#### 12.1.6 Attackers Search for Authorization Weakness After Obtaining Identity

#### 12.1.7 Defenders Must Evaluate Effective Authority, Not Authentication Alone

### 12.2 The Windows Access-Control Model

#### 12.2.1 Security Principals

#### 12.2.2 Securable Objects

#### 12.2.3 Security Identifiers

#### 12.2.4 Access Tokens

#### 12.2.5 Security Descriptors

#### 12.2.6 Access-Control Entries

#### 12.2.7 Access Checks

#### 12.2.8 Windows Authorization Is a Relationship Between Principal, Token, Object, and Requested Right

### 12.3 Security Principals and Security Identifiers

#### 12.3.1 Users

#### 12.3.2 Groups

#### 12.3.3 Computers

#### 12.3.4 Services and Managed Service Accounts

#### 12.3.5 Local and Domain Principals

#### 12.3.6 Well-Known SIDs

#### 12.3.7 SID Persistence

#### 12.3.8 Orphaned SIDs

#### 12.3.9 Names Are Administrative Labels; SIDs Drive Authorization

### 12.4 Windows Access Tokens

#### 12.4.1 Token Creation During Logon

#### 12.4.2 User SID

#### 12.4.3 Group SIDs

#### 12.4.4 Privileges

#### 12.4.5 Integrity Level

#### 12.4.6 Restricted and Deny-Only SIDs

#### 12.4.7 Authentication and Logon Context

#### 12.4.8 The Token Represents the Principal's Effective Local Security Context

### 12.5 Token Expansion and Group Membership

#### 12.5.1 Direct Group Membership

#### 12.5.2 Nested Group Membership

#### 12.5.3 Domain and Local Groups

#### 12.5.4 Universal Group Membership

#### 12.5.5 Foreign Security Principals

#### 12.5.6 SIDHistory

#### 12.5.7 Token Size and Group Expansion

#### 12.5.8 Token Bloat

#### 12.5.9 Nested Membership Can Hide Privilege From Simple Administrative Review

### 12.6 Impersonation, Delegation, and Alternate Security Contexts

#### 12.6.1 Primary Tokens

#### 12.6.2 Impersonation Tokens

#### 12.6.3 Impersonation Levels

#### 12.6.4 Service Impersonation

#### 12.6.5 Delegated Authentication Context

#### 12.6.6 Token Duplication

#### 12.6.7 Impersonation Rights Can Become Privilege-Escalation Paths

#### 12.6.8 Defenders Must Understand Which Services Can Act on Behalf of Other Identities

***

## SECURITY DESCRIPTORS AND ACCESS-CONTROL LISTS

### 12.7 Security Descriptors

#### 12.7.1 Owner

#### 12.7.2 Primary Group

#### 12.7.3 Discretionary Access-Control List

#### 12.7.4 System Access-Control List

#### 12.7.5 Control Flags

#### 12.7.6 Self-Relative Security Descriptors

#### 12.7.7 Security Descriptors Define Both Authority and Auditability

### 12.8 Security Descriptor Definition Language

#### 12.8.1 SDDL as a Text Representation of Security Descriptors

#### 12.8.2 Owner and Group Fields

#### 12.8.3 DACL Representation

#### 12.8.4 SACL Representation

#### 12.8.5 ACE Syntax

#### 12.8.6 Well-Known SID Abbreviations

#### 12.8.7 SDDL Supports Precise Authorization Analysis

#### 12.8.8 Incorrect Interpretation Can Conceal Dangerous Rights

### 12.9 Discretionary Access-Control Lists

#### 12.9.1 DACLs Determine Allowed and Denied Access

#### 12.9.2 Null DACL

#### 12.9.3 Empty DACL

#### 12.9.4 Explicit ACEs

#### 12.9.5 Inherited ACEs

#### 12.9.6 Allow and Deny Entries

#### 12.9.7 DACL Modification Can Be Equivalent to Resource Control

#### 12.9.8 `WriteDACL` Is Often an Authority-Expansion Primitive

### 12.10 Access-Control Entries and Evaluation Order

#### 12.10.1 Access-Aallowed ACEs

#### 12.10.2 Access-Denied ACEs

#### 12.10.3 Explicit Versus Inherited ACEs

#### 12.10.4 Canonical ACE Ordering

#### 12.10.5 Object-Specific ACEs

#### 12.10.6 Inheritance Flags

#### 12.10.7 Access Evaluation Is More Complex Than “User Is in Group”

#### 12.10.8 Misreading ACE Order Can Produce Incorrect Effective-Access Conclusions

### 12.11 Standard, Specific, and Extended Rights

#### 12.11.1 Generic Rights

#### 12.11.2 Standard Rights

#### 12.11.3 Object-Specific Rights

#### 12.11.4 Property Rights

#### 12.11.5 Extended Rights

#### 12.11.6 Control Access Rights

#### 12.11.7 GUID-Based Rights in Active Directory

#### 12.11.8 Broad Generic Rights Can Expand Into Several Powerful Specific Rights

### 12.12 Ownership and Permission Control

#### 12.12.1 Owners Receive Special Authorization Consideration

#### 12.12.2 Changing Ownership

#### 12.12.3 `WRITE_OWNER`

#### 12.12.4 Ownership and DACL Modification

#### 12.12.5 Ownership Can Bypass Apparent Permission Restrictions

#### 12.12.6 Stale Ownership Can Preserve Hidden Authority

#### 12.12.7 Ownership Must Be Included in Effective-Access Review

### 12.13 Inheritance

#### 12.13.1 Parent and Child Security Descriptors

#### 12.13.2 Inheritable ACEs

#### 12.13.3 Object and Container Inheritance

#### 12.13.4 Protected DACLs

#### 12.13.5 Explicit Permissions

#### 12.13.6 Inheritance Simplifies Administration but Can Propagate Excessive Authority

#### 12.13.7 Defenders Must Evaluate Where Delegated Rights Ultimately Apply

### 12.14 System Access-Control Lists and Auditing

#### 12.14.1 SACLs Define Audit Policy on Objects

#### 12.14.2 Success Auditing

#### 12.14.3 Failure Auditing

#### 12.14.4 Object Access

#### 12.14.5 Directory Service Access

#### 12.14.6 Audit Volume and Signal Quality

#### 12.14.7 Authorization Without Appropriate Auditing Creates an Evidence Gap

***

## WINDOWS PRIVILEGES AND LOCAL AUTHORIZATION

### 12.15 Windows Privileges and User Rights

#### 12.15.1 Privileges Differ From Object Permissions

#### 12.15.2 User Rights Assignment

#### 12.15.3 Logon Rights

#### 12.15.4 Backup and Restore Privileges

#### 12.15.5 Debug Privilege

#### 12.15.6 Impersonation Privilege

#### 12.15.7 Take Ownership

#### 12.15.8 Powerful Privileges Can Bypass Normal Object Permissions

#### 12.15.9 Local Privilege Must Be Included in Domain Attack Analysis

### 12.16 Mandatory Integrity Control

#### 12.16.1 Integrity Levels

#### 12.16.2 Low

#### 12.16.3 Medium

#### 12.16.4 High

#### 12.16.5 System

#### 12.16.6 Mandatory Labels

#### 12.16.7 No-Write-Up Concepts

#### 12.16.8 MIC Adds a Mandatory Layer Beyond the DACL

#### 12.16.9 Integrity Level Is Not a Substitute for Administrative Isolation

### 12.17 User Account Control

#### 12.17.1 Standard and Administrative Tokens

#### 12.17.2 Split Tokens

#### 12.17.3 Elevation

#### 12.17.4 Consent and Credential Prompts

#### 12.17.5 Admin Approval Mode

#### 12.17.6 Remote UAC Considerations

#### 12.17.7 UAC Is a Security Boundary Reduction Mechanism, Not a Complete Privilege Boundary

#### 12.17.8 Attackers Often Seek Paths That Avoid or bypass interactive elevation entirely

***

## GROUPS AND AUTHORIZATION DESIGN

### 12.18 Active Directory Group Scope and Type

#### 12.18.1 Security Versus Distribution Groups

#### 12.18.2 Domain Local Groups

#### 12.18.3 Global Groups

#### 12.18.4 Universal Groups

#### 12.18.5 Scope Determines Valid Membership and Resource Use

#### 12.18.6 Group Design Influences Token Expansion and Administrative Clarity

#### 12.18.7 Poor Group Architecture Creates Hidden Authorization

### 12.19 Group Nesting and Role Architecture

#### 12.19.1 Account-to-Role-to-Resource Design

#### 12.19.2 AGDLP

#### 12.19.3 AGUDLP

#### 12.19.4 Nested Role Groups

#### 12.19.5 Administrative Groups

#### 12.19.6 Resource Groups

#### 12.19.7 Proper Nesting Improves Reviewability

#### 12.19.8 Excessive Nesting Obscures Effective Authority

### 12.20 Local Groups and Endpoint Authority

#### 12.20.1 Local Administrators

#### 12.20.2 Remote Desktop Users

#### 12.20.3 Remote Management Groups

#### 12.20.4 Local Group Membership Through Domain Groups

#### 12.20.5 Restricted Groups

#### 12.20.6 Group Policy Preferences

#### 12.20.7 Local Administrative Relationships Create Lateral-Movement Paths

#### 12.20.8 Domain Review Must Include Endpoint Authorization

***

## ACTIVE DIRECTORY AUTHORIZATION

### 12.21 Directory Object Authorization

#### 12.21.1 Users

#### 12.21.2 Groups

#### 12.21.3 Computers

#### 12.21.4 Organizational Units

#### 12.21.5 Group Policy Objects

#### 12.21.6 Managed Service Accounts

#### 12.21.7 Certificate and Identity Infrastructure Objects

#### 12.21.8 Different Objects Expose Different Security-Relevant Rights

### 12.22 Delegated Directory Administration

#### 12.22.1 Delegation of Control

#### 12.22.2 Object Creation and Deletion

#### 12.22.3 Attribute Modification

#### 12.22.4 Password Reset

#### 12.22.5 Group Membership Modification

#### 12.22.6 SPN Modification

#### 12.22.7 Computer Object Control

#### 12.22.8 Delegation Should Be Evaluated by What It Enables, Not by the Wizard Label

### 12.23 Dangerous Directory Permission Relationships

#### 12.23.1 `GenericAll`

#### 12.23.2 `GenericWrite`

#### 12.23.3 `WriteDACL`

#### 12.23.4 `WriteOwner`

#### 12.23.5 Password Reset

#### 12.23.6 Group Membership Control

#### 12.23.7 SPN and Authentication-Relevant Attribute Control

#### 12.23.8 Replication Rights

#### 12.23.9 Certificate and Delegation Rights

#### 12.23.10 A Single ACE Can Become the First Edge in a Much Larger Attack Path

### 12.24 AdminSDHolder and Protected Authorization

#### 12.24.1 Protected Accounts and Groups

#### 12.24.2 AdminSDHolder Security Descriptor

#### 12.24.3 SDProp

#### 12.24.4 `adminCount`

#### 12.24.5 Inheritance Protection

#### 12.24.6 Historical Privilege and Residual Protection

#### 12.24.7 AdminSDHolder Abuse Can Create Durable Privileged Access

#### 12.24.8 Defensive Review Must Include Both Protected Principals and the Protection Mechanism

***

## EFFECTIVE AUTHORITY

### 12.25 Effective Access and Shadow Administration

#### 12.25.1 Assigned Role Versus Effective Capability

#### 12.25.2 Nested Group Authority

#### 12.25.3 ACL-Derived Authority

#### 12.25.4 Ownership-Derived Authority

#### 12.25.5 Credential-Derived Authority

#### 12.25.6 Computer and Service Control

#### 12.25.7 GPO and Management-System Authority

#### 12.25.8 Shadow Administrators

#### 12.25.9 “Not a Domain Admin” Does Not Mean “Cannot Control the Domain”

### 12.26 Authorization Through Systems and Services

#### 12.26.1 Control of a Computer Can Become Control of Its Administrators

#### 12.26.2 Control of a Service Can Become Control of Its Identity

#### 12.26.3 Control of Group Policy Can Become Endpoint Authority

#### 12.26.4 Control of Endpoint Management Can Become Enterprise Authority

#### 12.26.5 Control of Backup Can Become Recovery Authority

#### 12.26.6 Control of PKI Can Become Authentication Authority

#### 12.26.7 Effective Authorization Extends Beyond Directory ACLs

#### 12.26.8 These Relationships Become Formal Attack-Path Edges in Later Chapters

### 12.27 Least Privilege, Separation of Duties, and Privileged Access

#### 12.27.1 Least Privilege Is About Effective Capability

#### 12.27.2 Separation of Duties

#### 12.27.3 Administrative Role Separation

#### 12.27.4 Privileged Access Workstations

#### 12.27.5 Just-in-Time Privilege

#### 12.27.6 Just Enough Administration

#### 12.27.7 Temporary Privilege Is Preferable to Permanent Privilege

#### 12.27.8 Privilege Reduction Must Preserve Mission Operations

#### 12.27.9 “Permanent Administrator” Should Be the Exception, Not the Default Model

***

## OFFENSIVE AND DEFENSIVE AUTHORIZATION ANALYSIS

### 12.28 Offensive Authorization Assessment

#### 12.28.1 Enumerate Groups

#### 12.28.2 Expand Nested Membership

#### 12.28.3 Enumerate ACLs

#### 12.28.4 Identify Object Owners

#### 12.28.5 Identify Dangerous Extended Rights

#### 12.28.6 Identify Local Administrative Relationships

#### 12.28.7 Identify Shadow Administrators

#### 12.28.8 Identify Cross-Tier Control

#### 12.28.9 Validate Practical Consequence

#### 12.28.10 Stop When Authority Is Defensibly Proven

### 12.29 Defensive Authorization Engineering, Telemetry, and Drift

#### 12.29.1 Baseline Privileged Groups

#### 12.29.2 Baseline Sensitive ACLs

#### 12.29.3 Baseline Ownership

#### 12.29.4 Baseline User Rights

#### 12.29.5 Monitor Group Membership Changes

#### 12.29.6 Monitor Directory Permission Changes

#### 12.29.7 Monitor Privileged Token and Logon Activity

#### 12.29.8 Detect Authorization Drift

#### 12.29.9 Recertify Effective Authority, Not Merely Assigned Roles

#### 12.29.10 Recalculate Attack Paths After Privilege Changes

### 12.30 Federal/DoD Authorization and Preparing for Chapter 13

#### 12.30.1 Least Privilege Supports Federal Access-Control Requirements

#### 12.30.2 Separation of Duties Must Be Technically Enforced

#### 12.30.3 Privileged Access Requires Defensible Evidence

#### 12.30.4 STIG and Security Baselines Influence Windows Authorization

#### 12.30.5 FICAM Governance Must Ultimately Become Technical Access Control

#### 12.30.6 Zero Trust Requires Per-Request Authorization, Not Network Location Alone

#### 12.30.7 RMF Evidence Should Demonstrate Effective Access

#### 12.30.8 Offensive Assessment Can Reveal Authorization the Control Population Missed

**12.30.9 From Authorization to Authentication**

Chapter 12 established how Windows decides what an authenticated principal may do. Those decisions depend on the security context presented to the operating system, but that context must first be created through an authentication mechanism.

Chapter 13 therefore moves backward one step in the identity transaction and examines Windows authentication itself: Local Security Authority, LSASS, Security Support Provider Interface, Kerberos, NTLM, PKINIT, delegation, authentication policies, and the mechanisms that transform credentials into authenticated security contexts.

**12.30.10 The Next Question**

**How does Windows prove the identity behind the token—and what happens when an adversary steals, replays, forges, or redirects that proof?**

**Chapter 12:** what an authenticated identity can do. **Chapter 13:** how Windows proves that identity in the first place. **Chapter 16:** how those permissions and identities later combine into multi-step attack paths across the wider environment.
