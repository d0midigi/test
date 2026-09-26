# Chapter 6 - FICAM, DoD ICAM, Digital Identity Assurance, and the Identity Lifecycle

## new Chapter 6 — FICAM, DoD ICAM, Digital Identity Assurance, and the Identity Lifecycle.md

### 6.1 Federal Identity, Credential, and Access Management

#### 6.1.1 Identity Exists Before Account Provisioning

An identity represents a person, device, service, workload, application, or other entity before any particular Active Directory, cloud, application, or local account is created for it.

#### 6.1.2 Identity Is Not the Same as an Account

A single identity may correspond to multiple accounts across directories, applications, cloud tenants, mission systems, privileged environments, and partner infrastructures.

#### 6.1.3 Credentialing Does Not Equal Authentication

Credentialing establishes and binds an authenticator to an identity. Authentication occurs later when that authenticator is presented to prove the identity.

#### 6.1.4 Authentication Does Not Equal Authorization

Authentication establishes who or what is attempting access. Authorization determines what that authenticated principal may do.

#### 6.1.5 Access Management Extends Beyond Login

Access decisions may consider role, device state, mission assignment, group membership, assurance level, application context, session risk, location, entitlement, and other attributes after authentication succeeds.

#### 6.1.6 Federation Extends Trust Without Transferring Ownership

A federated partner can assert identity without surrendering administrative ownership of the underlying user or identity system.

#### 6.1.7 Governance Determines Which Identity Facts Matter

Identity architecture must establish which systems are authoritative for particular facts and how those facts are consumed by downstream access decisions.

***

### 6.2 FICAM as an Identity Architecture Discipline

#### 6.2.1 Identity Management

Identity management governs how identities are established, represented, modified, correlated, and eventually removed.

#### 6.2.2 Credential Management

Credential management addresses issuance, binding, activation, storage, use, replacement, revocation, recovery, and destruction of authenticators.

#### 6.2.3 Access Management

Access management governs how authenticated identities obtain authorization to resources, applications, services, facilities, and data.

#### 6.2.4 Federation

Federation allows an identity decision made by one trusted authority to be consumed by another system or security domain.

#### 6.2.5 Governance and Administration

Identity governance determines ownership, accountability, policy, lifecycle, entitlement approval, recertification, exception handling, and evidence requirements.

#### 6.2.6 FICAM as More Than Single Sign-On

Single Sign-On (SSO) is only one operational capability. FICAM addresses the complete system of identity proofing, credentials, authorization, federation, lifecycle, governance, assurance, and trust.

***

### 6.3 Department of Defense Identity, Credential, and Access Management

#### 6.3.1 DoD ICAM as an Enterprise Mission Capability

Department of Defense Identity, Credential, and Access Management (DoD ICAM) enables trusted identity and access decisions across military departments, combatant commands, defense agencies, cloud services, mission partners, contractors, and shared enterprise capabilities.

#### 6.3.2 Enterprise ICAM Does Not Replace Local Identity Engineering

Enterprise identity services cannot compensate for weak local Active Directory permissions, excessive privilege, insecure service accounts, poor certificate configuration, or application authorization defects.

#### 6.3.3 Enterprise Identity and Mission Identity

Mission systems may consume enterprise identity while maintaining additional mission-specific roles, attributes, constraints, or entitlement models.

#### 6.3.4 DoD ICAM and Mission Partners

Coalition, interagency, contractor, and partner operations require mechanisms for recognizing external identities without creating uncontrolled administrative trust.

#### 6.3.5 DoD ICAM and Cloud Identity

Modern DoD identity architecture increasingly spans on-premises Active Directory, Microsoft Entra ID, cloud-native identities, federation, workload identity, and application access.

#### 6.3.6 Disconnected and Tactical ICAM

Identity architecture must account for environments where centralized services are unreachable because of operational, geographic, bandwidth, or mission constraints.

***

### 6.4 The Identity Lifecycle

#### 6.4.1 Establishment

An identity begins when an authoritative process determines that a person or Non-Person Entity (NPE) should be represented within the identity ecosystem.

#### 6.4.2 Sponsorship

Certain identities require an accountable sponsor who establishes the mission or business justification for their existence and continued access.

#### 6.4.3 Identity Proofing

Identity proofing establishes confidence that the claimed identity corresponds to the person or entity being enrolled.

#### 6.4.4 Enrollment

Enrollment collects the information and evidence required to create an identity record and bind one or more credentials.

#### 6.4.5 Account Provisioning

Accounts are instantiated within directories, applications, cloud platforms, privileged environments, or mission systems according to approved need.

#### 6.4.6 Credential Issuance

Passwords, certificates, smart cards, cryptographic keys, passkeys, tokens, and other authenticators may be issued according to the required assurance level.

#### 6.4.7 Credential Binding

A credential has security meaning only when the enterprise can establish which identity it represents and under what conditions it is valid.

#### 6.4.8 Authentication

The identity presents an authenticator or combination of authenticators to establish an authenticated session or transaction.

#### 6.4.9 Authorization

The authenticated identity receives permissions or access according to roles, entitlements, attributes, policy, device state, resource sensitivity, and mission context.

#### 6.4.10 Continuous Evaluation

Access may be reevaluated when risk, device condition, employment status, privilege, session characteristics, or other security-relevant factors change.

#### 6.4.11 Recertification

Identity and entitlement owners periodically verify that accounts, credentials, privileges, memberships, and access remain justified.

#### 6.4.12 Suspension

An identity or credential may need temporary disabling when status is uncertain, access is under investigation, or continued use creates unacceptable risk.

#### 6.4.13 Revocation

Credentials and authorization must be invalidated when they are compromised, no longer required, or no longer legitimately associated with the identity.

#### 6.4.14 Deprovisioning

Accounts, group memberships, delegated rights, application assignments, certificates, tokens, roles, and other forms of authority must be removed when the underlying relationship ends.

#### 6.4.15 Destruction and Residual Identity

Deletion does not necessarily erase every artifact. Cached credentials, backup copies, tombstoned objects, certificates, tokens, logs, and historical identifiers may survive beyond account removal.

***

### 6.5 Joiner, Mover, and Leaver Governance

#### 6.5.1 The Joiner Phase

New identities require approved creation, authoritative attributes, appropriate baseline access, credential issuance, and defined ownership.

#### 6.5.2 Baseline Entitlements

New users or NPEs should receive only the access required by their initial role rather than inheriting broad privilege for convenience.

#### 6.5.3 The Mover Phase

Changes in assignment, organization, command, employment status, mission role, or system responsibility should trigger reevaluation of access.

#### 6.5.4 Entitlement Creep

Users commonly accumulate privileges over time when new access is granted without removing permissions associated with previous roles.

#### 6.5.5 The Leaver Phase

Termination, separation, contract completion, mission reassignment, device retirement, or application decommissioning should trigger timely removal of access.

#### 6.5.6 Immediate Versus Scheduled Deprovisioning

Some circumstances require immediate revocation, while others permit a controlled transition based on mission requirements and policy.

#### 6.5.7 Residual Privilege After Departure

Direct permissions, local accounts, API credentials, certificates, service ownership, application roles, shared secrets, and delegated authority may persist after a primary directory account is disabled.

***

### 6.6 Identity Assurance Levels

#### 6.6.1 The Purpose of Identity Assurance

Identity assurance represents confidence that the digital identity corresponds to the subject or entity it claims to represent.

#### 6.6.2 Identity Assurance Level 1

Identity Assurance Level 1 (IAL1) represents contexts where formal identity proofing is not required to establish a strong real-world identity relationship.

#### 6.6.3 Identity Assurance Level 2

Identity Assurance Level 2 (IAL2) establishes stronger confidence through evidence collection and identity-proofing procedures.

#### 6.6.4 Identity Assurance Level 3

Identity Assurance Level 3 (IAL3) provides the highest level of identity-proofing assurance within the NIST digital-identity model.

#### 6.6.5 Identity Proofing and Account Security Are Different Problems

Strong proofing establishes confidence about who the account belongs to but does not protect the account against credential theft, excessive privilege, or compromised authorization.

#### 6.6.6 Assurance Can Degrade Downstream

An identity established at high assurance may ultimately receive lower practical protection when applications accept weak authenticators, insecure recovery, or untrusted attributes.

***

### 6.7 Authenticator Assurance Levels

#### 6.7.1 The Purpose of Authenticator Assurance

Authenticator Assurance Levels (AALs) describe confidence in the mechanisms used to authenticate a claimant.

#### 6.7.2 Authenticator Assurance Level 1

Authenticator Assurance Level 1 (AAL1) provides basic confidence using a single authentication factor appropriate to lower-risk environments.

#### 6.7.3 Authenticator Assurance Level 2

Authenticator Assurance Level 2 (AAL2) requires stronger authentication, typically involving multiple factors or appropriately strong multifactor mechanisms.

#### 6.7.4 Authenticator Assurance Level 3

Authenticator Assurance Level 3 (AAL3) provides the highest authentication assurance and emphasizes phishing resistance, verifier impersonation resistance, and hardware-protected cryptographic authenticators.

#### 6.7.5 Phishing Resistance

An authenticator should resist techniques that trick users into providing reusable secrets or authentication responses to an attacker-controlled service.

#### 6.7.6 Hardware-Backed Authentication

PIV, CAC, FIDO2 security keys, trusted cryptographic hardware, and other device-bound mechanisms can provide stronger protection against credential export and cloning.

#### 6.7.7 Authentication Strength Does Not Determine Authorization Quality

AAL3 authentication does not make an account safe when that account possesses inappropriate privilege or participates in a dangerous attack path.

***

### 6.8 Federation Assurance Levels

#### 6.8.1 Federation Assurance

Federation Assurance Levels (FALs) address protection of assertions and federation transactions between Identity Providers and relying parties.

#### 6.8.2 Federation Assertion Protection

The security of a federation assertion depends upon cryptographic protection, audience restrictions, issuer validation, replay prevention, and correct relying-party validation.

#### 6.8.3 Holder-of-Key and Stronger Assertion Binding

Stronger federation models can bind assertions to cryptographic proof rather than relying exclusively on possession of a bearer artifact.

#### 6.8.4 Federation Assurance Is Separate From Authentication Assurance

A strongly authenticated user can still be represented by a weakly protected federation assertion.

#### 6.8.5 The Weakest Link Determines Practical Assurance

High IAL and AAL values cannot compensate for insecure federation, token handling, recovery, session management, or downstream authorization.

***

### 6.9 Assurance Chaining

#### 6.9.1 Identity Assurance, Authentication Assurance, and Federation Assurance Are Distinct

IAL, AAL, and FAL answer different questions and should not be treated as interchangeable ratings.

#### 6.9.2 Assurance Must Survive the Entire Access Path

The practical security of an identity transaction depends on proofing, credential issuance, authentication, federation, authorization, session protection, and recovery.

#### 6.9.3 Recovery Can Become an Assurance Downgrade

An AAL3 credential protected by hardware loses practical value if account recovery permits replacement through a substantially weaker process.

#### 6.9.4 Legacy Authentication Can Circumvent Strong Credentials

Password, NTLM, legacy federation, application-specific authentication, or protocol fallback may permit access outside the intended high-assurance path.

#### 6.9.5 Session Theft Can Bypass Authentication

An adversary who steals a valid session token may avoid interacting with the original authenticator entirely.

#### 6.9.6 Assurance Must Be Evaluated Architecturally

The appropriate question is not simply whether MFA is enabled, but whether every viable route to the protected resource maintains the required assurance.

***

### 6.10 Federal Credentials

#### 6.10.1 Personal Identity Verification

Personal Identity Verification (PIV) credentials provide standardized identity, authentication, signing, and encryption capabilities across civilian federal agencies.

#### 6.10.2 Common Access Card

The Common Access Card (CAC) provides Department of Defense personnel with a smart-card credential supporting identity and cryptographic authentication.

#### 6.10.3 Enterprise Identifiers

Identifiers such as the Electronic Data Interchange Personal Identifier (EDIPI) and DoD Identification Number can support identity correlation across systems.

#### 6.10.4 Certificates Within Federal Credentials

PIV and CAC credentials may contain multiple certificates serving authentication, digital-signature, encryption, and other functions.

#### 6.10.5 PIN Protection

The cardholder's Personal Identification Number (PIN) protects use of private cryptographic operations but does not itself represent the complete authentication mechanism.

#### 6.10.6 Hardware Protection

Private keys generated and retained within approved hardware provide stronger protection than exportable software-stored credentials.

#### 6.10.7 Credential Loss and Compromise

Lost, stolen, damaged, or suspected-compromised credentials require rapid revocation and replacement processes.

***

### 6.11 Biometrics and Identity

#### 6.11.1 Biometrics as Identity Evidence

Biometric characteristics can contribute to identity proofing, credential issuance, authentication, and physical-access processes.

#### 6.11.2 Biometric Factors Are Not Secrets

Fingerprints, facial characteristics, iris patterns, and other biometric traits cannot be changed in the same way as passwords.

#### 6.11.3 Biometric Matching Is Probabilistic

Biometric systems evaluate similarity rather than performing exact secret comparison and must account for false acceptance and false rejection.

#### 6.11.4 Biometrics and Federal Credentials

Biometric information may help establish the relationship between the credential holder and the identity represented by a PIV or CAC.

#### 6.11.5 Device-Local Biometrics

Windows Hello, mobile-device biometric unlock, and similar mechanisms often use biometrics to unlock a device-bound cryptographic key rather than transmitting the biometric itself as an authentication secret.

#### 6.11.6 Biometric Data Requires Strong Protection

Compromise of biometric templates can create long-lived privacy and identity risk because the underlying physical characteristic cannot simply be reset.

***

### 6.12 Derived Credentials

#### 6.12.1 Extending Federal Identity Beyond the Physical Card

Derived credentials allow trusted identity established through an existing high-assurance credential to be represented on another approved device.

#### 6.12.2 Mobile and Device-Based Credentials

Mobile phones, tablets, managed endpoints, and hardware security capabilities may support derived credential deployment.

#### 6.12.3 Credential Derivation Must Preserve Assurance

The provisioning process must establish confidence that the derived credential remains bound to the correct identity and protected device.

#### 6.12.4 Device Loss and Revocation

Derived credentials require independent lifecycle, inventory, and revocation processes because compromise of the derived device may not compromise the original physical credential.

#### 6.12.5 Derived Credentials and Zero Trust

Device-bound derived credentials can contribute simultaneously to user authentication and device trust.

***

### 6.13 Authoritative Identity Sources

#### 6.13.1 What Makes a Source Authoritative

An authoritative source is trusted to establish or maintain a particular identity fact according to defined governance.

#### 6.13.2 Authority Is Attribute-Specific

One system may be authoritative for employment status while another governs clearance, training, device ownership, mission assignment, or privileged-role approval.

#### 6.13.3 Attribute Provenance

Security-sensitive attributes should be traceable to their authoritative origin and the processes allowed to modify them.

#### 6.13.4 Synchronization Creates Copies

An attribute synchronized into Active Directory or Microsoft Entra ID does not become independently authoritative simply because the copy is locally stored.

#### 6.13.5 Conflicting Sources

When two systems can independently assert different values for the same security-relevant attribute, access decisions may become ambiguous or exploitable.

#### 6.13.6 Attribute Integrity as an Authorization Requirement

Authorization can only be as trustworthy as the data used to make the decision.

***

### 6.14 Identity Correlation and Unique Identifiers

#### 6.14.1 Names Are Poor Identity Keys

Display names, usernames, email addresses, and organizational affiliations can change or collide.

#### 6.14.2 Persistent Identifiers

Stable identifiers allow systems to correlate the same identity even when visible attributes change.

#### 6.14.3 EDIPI and DoD Identity Correlation

The Electronic Data Interchange Personal Identifier can provide a durable identifier for correlating DoD personnel identities across systems.

#### 6.14.4 Directory Identifiers

Security Identifiers (SIDs), object Globally Unique Identifiers (GUIDs), immutable identifiers, cloud object identifiers, and application identifiers support technical identity correlation.

#### 6.14.5 Identifier Reuse Is Dangerous

Reassigning an old identifier to a new entity can accidentally transfer historical access or application associations.

#### 6.14.6 Correlation Errors Can Become Authorization Errors

If two identities are incorrectly merged or one identity is represented as another, legitimate access-control logic may produce an illegitimate result.

***

### 6.15 Person Entities

#### 6.15.1 The Human Identity Record

A Person Entity represents an individual whose relationship to the agency, Department, command, mission, contractor, or partner environment can be established.

#### 6.15.2 Employees and Service Members

Federal civilian employees and military personnel commonly have authoritative personnel relationships suitable for enterprise identity provisioning.

#### 6.15.3 Contractors

Contractor identities require explicit sponsorship, contract-based lifecycle governance, and timely termination when the supported relationship changes.

#### 6.15.4 Guests and Mission Partners

External personnel may require access without becoming internally managed workforce identities.

#### 6.15.5 Privileged Person Identities

Administrative identities often require separate accounts, stronger authentication, additional approval, restricted logon paths, and enhanced monitoring.

#### 6.15.6 One Person, Multiple Security Principals

A single person may legitimately possess ordinary user, privileged administrator, application-specific, classified-network, cloud, and mission-specific identities.

***

### 6.16 Non-Person Entities

#### 6.16.1 Defining the NPE

A Non-Person Entity is an identity representing a device, application, service, workload, automation process, system component, or other nonhuman actor.

#### 6.16.2 NPEs Require Ownership

Every NPE should have an accountable human, technical owner, system owner, or mission owner responsible for its purpose and lifecycle.

#### 6.16.3 Service Accounts

Service accounts enable applications and operating-system services to authenticate independently of interactive users.

#### 6.16.4 Device Identities

Computers, network appliances, mobile devices, servers, and embedded systems may authenticate through machine accounts, certificates, keys, or cloud registration.

#### 6.16.5 Application Identities

Applications may authenticate using service principals, client certificates, secrets, managed identities, or workload federation.

#### 6.16.6 Workload Identities

Containers, cloud workloads, serverless components, and ephemeral services require identity that can exist for minutes or seconds rather than years.

#### 6.16.7 Automation Identities

Continuous Integration/Continuous Deployment (CI/CD), configuration management, orchestration, scripting, and Infrastructure as Code systems may operate with substantial authority without human interaction.

#### 6.16.8 NPE Credential Rotation

Automated credential rotation is especially important because nonhuman identities often operate continuously and may be difficult to manually maintain.

#### 6.16.9 NPEs and Excessive Privilege

Service and automation identities frequently accumulate broad access because permissions are granted to maintain availability rather than engineered according to least privilege.

***

### 6.17 Device Identity

#### 6.17.1 A Device Can Be an Independent Security Principal

A device can possess identity independently of the person currently using it.

#### 6.17.2 Active Directory Computer Accounts

Domain-joined devices maintain computer objects, machine credentials, Service Principal Names (SPNs), and secure channels with Active Directory.

#### 6.17.3 Device Certificates

Certificates can provide cryptographic device identity for network authentication, mutual TLS, Internet Protocol Security (IPsec), and other services.

#### 6.17.4 Trusted Platform Modules

Trusted Platform Modules (TPMs) can protect device-bound keys against extraction and cloning.

#### 6.17.5 Cloud Device Identity

Microsoft Entra registered, Entra joined, and hybrid joined devices introduce cloud-side device objects and authentication state.

#### 6.17.6 Device Compliance Is Not Device Identity

A system can be correctly identified while operating in an unhealthy or compromised security state.

#### 6.17.7 Device Identity as an Authorization Signal

Modern access decisions may require both a valid user identity and a trusted device.

***

### 6.18 Service and Workload Identity

#### 6.18.1 Traditional Service Accounts

Long-lived user accounts historically used to run services often create problems involving static passwords, interactive logon, password expiration, and privilege accumulation.

#### 6.18.2 Managed Service Accounts

Managed Service Accounts (MSAs) reduce manual password management for services tied to individual hosts.

#### 6.18.3 Group Managed Service Accounts

Group Managed Service Accounts (gMSAs) support services operating across multiple approved hosts while Active Directory manages credential rotation.

#### 6.18.4 Delegated Managed Service Accounts

Delegated Managed Service Accounts (dMSAs) extend managed service identity capabilities in newer Windows Server environments.

#### 6.18.5 Managed Cloud Identities

Cloud platforms may issue managed identities that eliminate the need to store static application credentials.

#### 6.18.6 Workload Identity Federation

Workload federation allows applications to exchange trusted external identity assertions for temporary credentials rather than storing long-lived secrets.

#### 6.18.7 Short-Lived Credentials

Reducing credential lifetime limits the value of a stolen workload credential.

#### 6.18.8 Service Identity Ownership

Automated credentials do not remove the need for human accountability over the identity's privileges and lifecycle.

***

### 6.19 Identity Sponsorship

#### 6.19.1 Sponsorship Establishes Accountability

A sponsor confirms that an identity has a legitimate mission or business reason to exist.

#### 6.19.2 Contractor Sponsorship

Contractor identities require sponsors who understand the work being performed and the access necessary to perform it.

#### 6.19.3 Guest Sponsorship

External users should remain associated with an internal sponsor capable of validating continued need.

#### 6.19.4 NPE Sponsorship

Services, applications, automation identities, devices, and workloads also require accountable ownership even when traditional personnel sponsorship does not apply.

#### 6.19.5 Sponsor Departure

Access should not become orphaned when the individual responsible for an identity leaves or changes assignment.

#### 6.19.6 Sponsorship Recertification

Long-lived external and non-person identities should periodically require renewed justification.

***

### 6.20 Access Governance

#### 6.20.1 Entitlements Express Relationships

Access should represent an identifiable relationship between a principal, a resource, a mission requirement, and an accountable approver.

#### 6.20.2 Direct Permission Versus Governed Permission

Granting an account directly to a resource may be technically functional while producing poor lifecycle visibility and difficult recertification.

#### 6.20.3 Role-Based Access Control

Role-Based Access Control (RBAC) assigns permissions according to defined functions or responsibilities.

#### 6.20.4 Attribute-Based Access Control

Attribute-Based Access Control (ABAC) evaluates properties of the user, device, resource, environment, or request to make authorization decisions.

#### 6.20.5 Discretionary Access Control

Discretionary Access Control (DAC) allows owners or authorized administrators to control permissions on protected objects.

#### 6.20.6 Mandatory Access Control

Mandatory Access Control (MAC) applies centrally enforced security policy that individual owners cannot arbitrarily override.

#### 6.20.7 Policy-Based and Conditional Access

Cloud and modern identity platforms may combine identity, device, risk, network, session, and application conditions to control access dynamically.

#### 6.20.8 No Access Model Automatically Produces Least Privilege

RBAC, ABAC, DAC, MAC, and Conditional Access can all be misconfigured or implemented with unnecessarily broad authority.

***

### 6.21 Role-Based Access Control

#### 6.21.1 Roles Represent Functions

A role should represent a meaningful function rather than becoming a convenient collection of unrelated permissions.

#### 6.21.2 Users-to-Roles-to-Permissions

RBAC separates individual identities from direct permission assignment by placing functional roles between them.

#### 6.21.3 Role Explosion

Overly granular designs can create hundreds or thousands of roles that become difficult to govern.

#### 6.21.4 Role Accumulation

Users may accumulate old roles when movement between assignments does not remove previous entitlements.

#### 6.21.5 Privileged Roles

Administrative roles require stronger approval, authentication, monitoring, activation, and review than ordinary access.

#### 6.21.6 RBAC and Active Directory Groups

Security groups commonly implement portions of RBAC but group membership alone does not constitute a complete governance model.

***

### 6.22 Attribute-Based Access Control

#### 6.22.1 Attributes as Authorization Inputs

ABAC can evaluate identity, device, resource, mission, classification, organization, location, or other contextual attributes.

#### 6.22.2 Attribute Authority Matters

A dynamic access rule becomes dangerous when the attribute controlling it can be modified by an untrusted principal.

#### 6.22.3 Claims-Based Authorization

Federation and modern identity systems frequently convert authoritative attributes into claims consumed by applications.

#### 6.22.4 Device Attributes

Device compliance, registration, ownership, operating-system state, and risk may affect authorization.

#### 6.22.5 Environmental Attributes

Location, network, time, session risk, and resource state can further constrain access.

#### 6.22.6 ABAC Complexity

Fine-grained policy can become difficult to understand when many attributes and conditions interact.

#### 6.22.7 Effective Access Must Remain Explainable

Security teams should be able to determine why a user was granted or denied access even when complex attribute logic is used.

***

### 6.23 Separation of Duties

#### 6.23.1 No Single Principal Should Control Every Critical Step

High-impact identity processes may require multiple independent approvals or administrative roles.

#### 6.23.2 Credential Issuance

Identity proofing, credential approval, issuance, and activation may be deliberately separated.

#### 6.23.3 Privileged Access

The ability to request, approve, activate, and audit privileged access should not necessarily reside with the same individual.

#### 6.23.4 PKI Administration

Certification authority administration, certificate management, auditing, and key operations may require separated responsibilities.

#### 6.23.5 Separation Must Survive Indirect Control

Formal role separation fails when one administrator can modify the accounts, systems, or permissions of the supposedly independent role.

#### 6.23.6 Technical Enforcement Beats Procedural Assumption

Separation of duties is stronger when architecture prevents conflicting actions rather than depending only on policy.

***

### 6.24 Least Privilege and Effective Authority

#### 6.24.1 Least Privilege Is an Outcome

An account is least privileged only when its effective authority is no greater than required for its mission function.

#### 6.24.2 Direct Membership Is Only One Source of Privilege

Nested groups, object permissions, ownership, local administration, delegated rights, certificates, cloud roles, application permissions, and management systems can all create authority.

#### 6.24.3 Effective Authority Must Be Calculated

Security review should determine what the principal can actually cause to happen across the identity trust system.

#### 6.24.4 Time-Bound Privilege

Privileged Identity Management and Just-in-Time mechanisms can reduce the amount of time sensitive authority remains active.

#### 6.24.5 Just Enough Administration

Just Enough Administration (JEA) and constrained administration models restrict operators to defined tasks rather than broad administrator roles.

#### 6.24.6 Privilege Must Be Recertified

Long-lived privilege should not survive simply because nobody remembers why it was originally granted.

***

### 6.25 Access Recertification

#### 6.25.1 Recertification Is a Security Control

Periodic review challenges the assumption that previously approved access remains appropriate forever.

#### 6.25.2 Resource Owners Must Understand What They Approve

An approval process is ineffective when reviewers cannot identify what a group, application role, certificate permission, or cloud entitlement actually grants.

#### 6.25.3 Privileged Access Requires Higher Scrutiny

Administrative roles, Tier 0 permissions, certificate authority access, synchronization privileges, and federation authority require more frequent or more rigorous review.

#### 6.25.4 NPE Entitlements Must Be Reviewed

Service accounts, applications, managed identities, automation, and workloads should not be excluded from recertification simply because they are nonhuman.

#### 6.25.5 Dormant Access

Access that has not been used for an extended period should trigger evaluation rather than automatically remaining available.

#### 6.25.6 Recertification Evidence

Approvals, removals, exceptions, owners, dates, and rationale should remain traceable for assessment and authorization.

***

### 6.26 Credential Governance

#### 6.26.1 Credential Issuance Must Follow Identity Assurance

A strong credential issued to the wrong identity provides strong authentication for the wrong person.

#### 6.26.2 Multiple Credentials per Identity

An identity may possess passwords, smart cards, certificates, FIDO authenticators, passkeys, recovery mechanisms, tokens, or application-specific credentials simultaneously.

#### 6.26.3 Credential Inventory

Identity owners must know which authenticators remain active for sensitive identities.

#### 6.26.4 Rotation

Passwords, service secrets, cryptographic keys, certificates, and application credentials require lifecycle-appropriate rotation.

#### 6.26.5 Recovery

Recovery methods should receive assurance commensurate with the credential they can replace.

#### 6.26.6 Revocation

A compromised authenticator must be invalidated across all systems that continue to recognize it.

#### 6.26.7 Credential Diversity Complicates Incident Response

Resetting the domain password may not invalidate certificates, refresh tokens, Kerberos tickets, cached credentials, browser sessions, or cloud application secrets.

***

### 6.27 Federation Governance

#### 6.27.1 Federation Is a Security Architecture Decision

Establishing federation means agreeing to rely on another authority's identity decisions.

#### 6.27.2 Trust Agreements Define What Is Accepted

Federation governance should identify trusted issuers, accepted claims, authentication expectations, intended audiences, and revocation procedures.

#### 6.27.3 Authentication Assurance Must Be Interpretable

The relying party must understand what an external authentication claim actually means rather than assuming all MFA or certificate authentication is equivalent.

#### 6.27.4 Claims Must Be Scoped

External group, role, organization, device, or privilege claims should not automatically map into unrestricted local authority.

#### 6.27.5 Signing-Key Compromise Expands Consequence

An adversary controlling an Identity Provider's token-signing authority may impersonate identities without stealing their authenticators.

#### 6.27.6 Federation Relationships Require Lifecycle Management

Trusts must be created, reviewed, modified, suspended, and terminated deliberately.

#### 6.27.7 Federation Failure Requires an Incident Path

The receiving environment needs procedures for rapidly restricting or disabling an external trust when the upstream identity authority is suspected of compromise.

***

### 6.28 Mission-Partner Identity Governance

#### 6.28.1 Mission Trust Should Be Narrower Than Identity Recognition

Recognizing an external identity should not automatically grant broad access to mission systems.

#### 6.28.2 Sponsorship Creates Local Accountability

External access requires a responsible internal owner who can confirm why the identity should continue to exist.

#### 6.28.3 Identity Translation Can Become a Security Boundary

Mapping an external role, identifier, or claim into a local identity or entitlement must be treated as an authorization decision.

#### 6.28.4 Partner Assurance Must Be Explicitly Trusted

External MFA, device, identity-proofing, or certificate claims should be accepted only when the assurance process behind them is understood.

#### 6.28.5 Partner Compromise Requires Local Response

An external identity-provider breach may require local session revocation, account suspension, trust restriction, or emergency access changes.

#### 6.28.6 Mission Continuity Must Survive Federation Failure

Critical operations should consider what happens when partner federation or external identity services are temporarily unavailable.

***

### 6.29 Identity Governance for Privileged Accounts

#### 6.29.1 Privileged Identity Requires Stronger Governance

Accounts capable of changing identity infrastructure require stricter control than ordinary workforce accounts.

#### 6.29.2 Separate Administrative Identities

Administrative work should generally use dedicated privileged identities rather than routine user accounts.

#### 6.29.3 Privilege Activation

Just-in-Time or approval-based activation can reduce persistent exposure.

#### 6.29.4 Privileged Authentication

PIV, CAC, FIDO2, hardware-backed keys, authentication policies, and other phishing-resistant mechanisms can increase confidence in privileged authentication.

#### 6.29.5 Privileged Workstations

Administrative credentials should be used from devices whose security posture matches the sensitivity of the systems being administered.

#### 6.29.6 Emergency and Break-Glass Accounts

Emergency identities require tightly governed storage, monitoring, testing, and usage procedures because ordinary controls may intentionally not apply.

#### 6.29.7 Privileged Account Recovery

Recovery procedures must not provide an easier path to privilege than normal authentication.

***

### 6.30 Identity Governance for Non-Person Entities

#### 6.30.1 Every NPE Needs a Purpose

An identity without a documented technical or mission function becomes difficult to justify, monitor, or retire.

#### 6.30.2 Every NPE Needs an Owner

Ownership should survive staffing changes and be associated with the system or mission rather than an individual's memory.

#### 6.30.3 Interactive Logon Should Be Deliberate

Service and automation identities generally should not receive interactive logon rights unless a defined operational requirement exists.

#### 6.30.4 Static Credentials Should Be Minimized

Managed credentials, workload federation, managed identities, and short-lived tokens reduce reliance on long-lived secrets.

#### 6.30.5 Privilege Should Match the Workload

Applications and services should receive only the APIs, resources, directories, systems, and data required for their function.

#### 6.30.6 NPE Activity Must Be Distinguishable

Logging should allow defenders to determine which workload, service, application, device, or automation identity performed an action.

#### 6.30.7 NPE Deprovisioning Is Often Neglected

Decommissioned applications and services frequently leave behind accounts, certificates, secrets, SPNs, role assignments, and API permissions.

***

### 6.31 Identity Debt

#### 6.31.1 Identity Debt Accumulates Gradually

Stale accounts, abandoned groups, unused certificates, forgotten service principals, old trusts, excessive privileges, and obsolete authentication methods accumulate as environments evolve.

#### 6.31.2 Operational Exceptions Become **Permanent**

Temporary access, migration privileges, emergency accounts, and compatibility configurations often survive long after the event that justified them.

#### 6.31.3 Identity Debt Creates Attack Paths

An individual stale condition may appear harmless until it connects a low-privilege principal to more consequential authority.

#### 6.31.4 Cloud Identity Produces Its Own Debt

Unused application registrations, stale service principals, guest accounts, consent grants, old secrets, and abandoned cross-tenant relationships can become long-lived exposure.

#### 6.31.5 Governance Is the Primary Control Against Identity Debt

Lifecycle ownership, recertification, inventory, expiration, attestation, and deprovisioning prevent identity systems from becoming collections of forgotten trust.

***

### 6.32 FICAM, DoD ICAM, and Zero Trust

#### 6.32.1 Zero Trust Depends on Authoritative Identity

A Policy Decision Point cannot make a defensible access decision using identity data whose origin or integrity is uncertain.

#### 6.32.2 Strong Authentication Is Necessary but Not Sufficient

Identity assurance, authorization, device trust, resource context, session risk, and privilege remain relevant after authentication.

#### 6.32.3 Device Identity Becomes Part of Access Trust

Zero Trust increasingly evaluates the identity and state of both the user and the device requesting access.

#### 6.32.4 Continuous Access Evaluation Changes the Meaning of a Session

Authentication need not create unconditional trust lasting until logout or token expiration.

#### 6.32.5 NPE Identity Is Essential to Zero Trust

Applications, services, workloads, automation, and devices must be identifiable and governable when implicit network trust is removed.

#### 6.32.6 Federation Extends the Zero Trust Decision Surface

External identity assertions become additional inputs that must be validated, scoped, and continuously governed.

#### 6.32.7 FICAM Provides the Identity Discipline Zero Trust Requires

Identity proofing, credential management, authoritative attributes, lifecycle governance, federation, access management, and assurance provide the structure necessary for identity-centric Zero Trust decisions.

***

### 6.33 Identity Governance as an Attack-Surface Control

#### 6.33.1 Dormant Accounts Become Adversary Opportunities

Accounts that are no longer actively managed may retain valid credentials and forgotten access.

#### 6.33.2 Excessive Entitlement Expands Blast Radius

A compromised identity becomes more dangerous when historical permissions, nested memberships, cloud roles, or application access exceed current need.

#### 6.33.3 Weak Recovery Can Defeat Strong Authentication

Attackers may target credential replacement, help-desk procedures, enrollment, or account recovery when direct authentication is difficult.

#### 6.33.4 Attribute Manipulation Can Manufacture Authority

Changing an identity attribute may produce dynamic group membership, federation claims, certificate issuance, or application privilege without modifying traditional group membership.

#### 6.33.5 Federation Can Extend Compromise

An attacker who compromises an upstream identity authority may gain access to multiple relying systems through legitimate trust relationships.

#### 6.33.6 Service Accounts and NPEs Offer Durable Access

Nonhuman identities may provide long-lived, low-visibility access because they are expected to operate continuously.

***

### 6.34 Identity Governance as a Detection Source

#### 6.34.1 Lifecycle Events Create Security Telemetry

Account creation, enablement, disablement, modification, credential reset, role assignment, and deletion generate observable events.

#### 6.34.2 Privilege Changes Require Monitoring

Group membership, delegated rights, directory roles, application permissions, certificate enrollment rights, and ownership changes may indicate authority expansion.

#### 6.34.3 Authentication Must Be Interpreted in Lifecycle Context

A successful login by an identity that should have been disabled is a governance failure and potentially an incident indicator.

#### 6.34.4 NPE Behavior Requires Baselines

Service and workload identities often exhibit predictable patterns whose deviation may reveal credential theft or misuse.

#### 6.34.5 Federation and Cloud Logs Extend Identity Visibility

Sign-in logs, token issuance, application consent, role activation, cross-tenant activity, and federation events reveal identity actions beyond the on-premises domain.

#### 6.34.6 Governance Data Enhances Threat Hunting

Sponsor, owner, role, expected system, credential type, lifecycle state, and privilege information can help defenders distinguish legitimate identity use from anomalous activity.

***

### 6.35 Measuring Identity Governance Effectiveness

#### 6.35.1 Number of Accounts Is Not an Assurance Metric

Large inventories alone do not establish whether identities are accurate, justified, or safely governed.

#### 6.35.2 Dormant Account Rate

The percentage of unused but enabled identities can indicate lifecycle weakness.

#### 6.35.3 Privileged Identity Population

The number and distribution of privileged identities help reveal whether elevated access is appropriately constrained.

#### 6.35.4 Credential Age

Long-lived credentials, secrets, keys, and certificates may indicate unmanaged lifecycle or rotation failures.

#### 6.35.5 Recertification Completion

Completion statistics matter only when the underlying review actually challenges access.

#### 6.35.6 Orphaned Identity Rate

Accounts, NPEs, applications, certificates, or entitlements without accountable owners represent governance failure.

#### 6.35.7 Mean Time to Deprovision

The delay between termination of need and removal of access directly affects exposure.

#### 6.35.8 Path to Privilege

A mature metric should examine how many identities possess direct or indirect routes toward Tier 0 and other high-value authority.

***

### 6.36 Preparing for Chapter 7

#### 6.36.1 From Identity Governance to Risk Management

Chapter 6 established what federal identities are, how they are proofed, credentialed, authenticated, authorized, federated, governed, recertified, and retired. Chapter 7 places those identity mechanisms inside the Risk Management Framework.

#### 6.36.2 Identity as an Authorization and Common-Control Problem

The next chapter examines how Active Directory and connected identity services are categorized, selected, implemented, assessed, authorized, inherited, continuously monitored, and represented through Risk Management Framework evidence.

#### 6.36.3 From Identity Assurance to System Assurance

The reader now moves from evaluating the trustworthiness of individual identities and credentials to evaluating whether the larger identity system provides defensible security assurance to every mission system that depends upon it.
