---
icon: square-exclamation
---

# Chapter 6 - Risk Management Framework (RMF), Security Baselines, and Authorization Evidence

#### Abstract

The Risk Management Framework (RMF) is sometimes experienced operationally as a collection of artifacts: a system security plan, control implementation statements, assessment results, Plans of Action and Milestones, vulnerability scans, diagrams, inventories, and an authorization package assembled for review. Those artifacts are necessary, but they are evidence of the process rather than the purpose of the process.

RMF exists to support risk decisions about systems and the missions that depend upon them.

That distinction is especially important for identity infrastructure. Active Directory, Public Key Infrastructure (PKI), federation, privileged-access services, synchronization platforms, administrative workstations, and other components of the identity trust system frequently provide services to many systems simultaneously. Their security posture cannot be evaluated sensibly by treating every dependent application as though it possessed an independent identity architecture. In many environments, portions of identity security function as common or shared controls whose implementation and failure can affect many authorization boundaries at once.

The National Institute of Standards and Technology (NIST) Risk Management Framework remains organized around seven steps—Prepare, Categorize, Select, Implement, Assess, Authorize, and Monitor—and integrates security and privacy risk management throughout the system life cycle. NIST Special Publication (SP) 800-37 Revision 2 remains the governing RMF publication, while the NIST SP 800-53 control catalog has continued to evolve; NIST issued Release 5.2.0 of the Revision 5 controls in August 2025.

Within the Department of Defense, DoD Instruction (DoDI) 8510.01, _Risk Management Framework for DoD Systems_, remains the department-level RMF instruction. DoD implementation is supplemented by Security Technical Implementation Guides (STIGs), Security Requirements Guides (SRGs), vulnerability-management processes, continuous cybersecurity activities, assessment practices, and authorization evidence maintained through DoD processes and tooling.

The central argument of this chapter is that identity security must remain visible throughout that lifecycle. Identity is not merely represented by controls in the Identification and Authentication family. It affects Access Control, Account Management, Audit and Accountability, Configuration Management, Contingency Planning, Incident Response, System and Communications Protection, System and Information Integrity, and numerous other areas because identity establishes who or what may exercise authority throughout the system.

A well-written authorization package should therefore describe the identity architecture that actually exists. A well-executed assessment should test that architecture rather than merely confirm that required sentences appear in documentation. A well-managed Plan of Action and Milestones should represent risk that is genuinely being reduced. Continuous monitoring should identify when the approved identity state begins to diverge from the operational one.

RMF becomes meaningful to identity security when documentation, technical state, adversarial exposure, and mission risk describe the same environment.

#### Keywords

Risk Management Framework; RMF; NIST SP 800-37; NIST SP 800-53; security controls; common controls; control inheritance; authorization; assessment; STIG; SRG; eMASS; POA\&M; continuous monitoring; identity risk; Active Directory; mission risk

#### Key Terms

**Risk Management Framework (RMF):** The structured process defined by NIST for managing security and privacy risk across the system life cycle through preparation, categorization, control selection, implementation, assessment, authorization, and continuous monitoring.

**Security control:** A safeguard or countermeasure prescribed for an information system or organization to protect confidentiality, integrity, availability, privacy, operations, assets, individuals, other organizations, or national interests from identified risks. NIST SP 800-53 provides the principal federal security and privacy control catalog.

**Common control:** A security or privacy control whose implementation supports more than one system and is therefore inherited, wholly or partly, by multiple authorization boundaries.

**Control inheritance:** The condition in which a system relies upon a control or portion of a control implemented and managed by another organizational entity, shared service, or common-control provider rather than implementing the entire capability independently.

**Authorization boundary:** The defined collection of system components for which an Authorizing Official evaluates and accepts responsibility for security and privacy risk under the applicable authorization process.

**Residual risk:** Risk remaining after applicable safeguards, countermeasures, mitigations, and controls have been implemented.

**Security control assessment:** The process of determining whether controls are implemented correctly, operating as intended, and producing the desired outcome with respect to meeting established security and privacy requirements. NIST SP 800-53A Revision 5 provides the federal assessment methodology and procedures aligned to the Revision 5 control catalog.

**Authorization:** A risk-based decision by an accountable authorizing official regarding whether operation of the system, or use of common controls, is acceptable given the evidence and residual risk presented.

## 6.1 Risk Management Framework

RMF is a decision architecture, not a documentation process.

It connects controls to systems, missions, threats, dependencies, and consequences. NIST organizes RMF into seven steps: Prepare, Categorize, Select, Implement, Assess, Authorize, and Monitor. It integrates security and privacy risk management throughout the system life cycle.

This model fits identity security particularly well. Identity infrastructure rarely belongs conceptually to one application. Domain Controllers, PKI, federation, privileged-access platforms, synchronization services, and administrative workstations can serve many authorization boundaries.

Their authority is relational. A technically healthy forest can retain dangerous delegated control. A sound PKI can permit unintended authentication authority. A hardened privileged-access platform can still depend on a lower-tier management plane.

RMF gives these conditions a place as risk. Its value depends on the analysis supporting it.

If an authorization boundary omits an identity dependency, its controls may be evaluated elsewhere. They may not be evaluated at all. If an assessment verifies MFA but ignores alternate authentication, its evidence can overstate assurance.

RMF becomes shallow only when the technical analysis is shallow.

### 6.1.1 Prepare

Prepare establishes the context for meaningful risk decisions. It defines roles, priorities, assumptions, risk strategy, stakeholders, and common-control considerations before control selection begins.

For identity infrastructure, preparation must avoid defining the system too narrowly. A mission application may depend on Active Directory, enterprise PKI, privileged access, cloud identity, and a SIEM. The application cannot distinguish legitimate users without these external services.

The authorization package should identify those dependencies, including inherited ones. It should also characterize the identity population. Workforce users, privileged operators, partners, contractors, and non-person entities create different risks.

Preparation prevents control selection against an imaginary system.

### 6.1.2 Categorize

Categorization establishes potential confidentiality, integrity, and availability impact. FIPS 199 supplies the federal model. RMF uses the result in later control and risk decisions.

Identity infrastructure often has inherited impact. A Domain Controller need not store mission data to affect access to it. A Certification Authority can affect trusted authentication across systems. A federation service can issue assertions for high-impact applications.

Identity compromise can expose resources, impersonate users, alter privileges, or disrupt operations. Its impact should reflect the authority it can reach. Treat enterprise identity services as explicit categorization and architecture concerns.

### 6.1.3 Select

Select determines controls and parameters for the system’s categorization, environment, and risk. NIST SP 800-53 supplies the control catalog. NIST SP 800-53B supplies control baselines.

Identity security spans the catalog. Account lifecycle affects Account Management. Privileged access affects least privilege, separation of duties, remote access, and administrative restrictions. Authentication affects Identification and Authentication, federation, remote access, and incident containment.

Directory auditing supports Audit and Accountability. Domain Controller recovery supports Contingency Planning. Group Policy supports Configuration Management.

Select controls by the identity function being protected. Do not search only for “identity” controls. Ask which controls depend on the wider identity trust system.

### 6.1.4 Implement

Implementation turns a selected control into system behavior.

Least privilege becomes group memberships, delegation, role assignments, authentication restrictions, administrative workstations, and privileged workflows. Account management becomes provisioning, sponsorship, disablement, recertification, service-account ownership, and synchronization.

Strong authentication becomes actual PIV or CAC use, Kerberos, certificate mapping, modern authenticators, recovery processes, and alternate paths. Audit becomes policy, SACLs, service logs, cloud telemetry, forwarding, retention, and detection content.

Avoid statements such as “access follows least privilege.” Identify the enforcing authority. State which groups, roles, policies, or platforms impose the restriction. State how separation events reach downstream systems. State how certificates map to accounts and which alternate paths remain.

The strongest evidence is an independently observable technical state.

### 6.1.5 Assess

Assessment determines whether controls are implemented correctly, operate as intended, and achieve their required outcome.

Identity assessment combines configuration compliance with adversarial reasoning. Limiting Domain Admin membership is useful. It is incomplete if another principal can modify that group, reset an administrator password, alter a Domain Controller GPO, control a management platform, or obtain an impersonation-capable certificate.

Distinguish direct implementation from effective outcome. Assessment need not become a penetration test. It can analyze directory permissions, certificate templates, replication rights, and attack paths without exploiting production systems.

The attacker’s model tests whether the intended control outcome is true.

### 6.1.6 Authorize

Authorization converts evidence into an accountable risk decision. The Authorizing Official accepts residual risk under stated conditions. An Authority to Operate is not a permanent certificate of security.

Identity evidence should describe effective authority, not only visible configuration. A list of five Domain Admins offers limited assurance. Better evidence identifies their workstations, group modifiers, password-reset delegates, management-plane dependencies, certificate authority paths, and emergency-access processes.

Both packages may include the same screenshot. Only one describes the control plane.

### 6.1.7 Monitor

Monitor makes RMF continuous. Authorization approves a point-in-time state. Identity environments change immediately through administration, integration, patching, role changes, trust changes, and new vulnerabilities.

Security state is perishable. A temporary administrator may remain assigned. A delegated permission may expand. A certificate template may be copied. A synchronization scope may change.

Continuous monitoring must observe identity relationships as well as host vulnerabilities. It determines whether the assumptions supporting authorization remain true.

## 6.2 Identity as a Common Control Provider

Identity infrastructure demonstrates why common controls exist. Shared services avoid separate identity proofing, credentials, workforce directories, and privileged-access mechanisms for every application.

Applications can inherit authentication from Active Directory, PIV validation from enterprise PKI, lifecycle status from authoritative personnel systems, and authentication telemetry from a centralized SIEM.

Common controls create efficiency and aggregate risk. A local weakness can affect one system. A weakness in a shared identity control can affect every relying system.

### 6.2.1 Common identity services concentrate assurance

Centralized identity services improve consistency. They can apply common authentication requirements, propagate authoritative employment status, and impose stronger administrative controls.

They also concentrate assurance. A federation service can carry extensive authentication authority with little mission data. A synchronization platform can influence identities across boundaries. A Certification Authority can act as a trust anchor for thousands of events.

Protect these services according to the authority others inherit from them.

### 6.2.2 Common control does not mean complete control

Systems inherit specific capabilities, not “identity” as a whole.

An application may inherit authentication while assigning local roles. It may inherit workforce lifecycle while retaining local accounts. It may accept enterprise certificates while performing its own certificate-to-account mapping. It may consume centralized logs while failing to generate needed events.

Document each inherited capability explicitly. This prevents responsibility from disappearing between organizations.

### 6.2.3 Common-control failure is a shared-risk event

Material compromise of a common identity service changes the risk of every dependent system. A compromised identity source, CA, federation service, or privileged-access platform can affect relying systems without directly attacking them.

The incident becomes a shared-risk event. The provider must coordinate with inheriting systems. Authorization boundaries remain separate, but identity failure crosses them.

## 6.3 Control Inheritance and Shared Services

Inheritance is more than a reference to a common-control package. A system inherits only the capability the provider actually supplies.

An enterprise directory can authenticate a user. PKI can provide credential assurance. A federation service can issue an assertion. A local application can transform claims and assign authority. The final access decision depends on every layer.

### 6.3.1 Inheritance should follow technical responsibility

Determine inheritance by identifying which component performs the security function.

An enterprise service may create and disable workforce identities. A local application may still assign privileged roles. PKI may issue and revoke certificates. A local mapping table may still associate certificates with accounts.

Test inheritance at the integration point. A local fallback can defeat centralized authentication. Local accounts can outlive centrally disabled identities.

### 6.3.2 Shared services create boundary interfaces

Inherited controls create interfaces between a provider and consumer. These may use Kerberos, SAML, LDAP, SCIM, or certificate validation.

A secure service does not guarantee a secure integration. A relying party can accept an incorrect token audience. A valid certificate can map to the wrong account. Deprovisioning can fail after central disablement.

Providers must demonstrate correct service operation. Consumers must demonstrate correct use. Inheritance does not remove interface responsibility.

### 6.3.3 Inherited risk must reach the Authorizing Official

Provider findings can change the risk accepted by inheriting systems. Do not duplicate every provider finding into every package. Establish a method to identify material downstream effects.

A minor logging deficiency may have limited impact. A privileged-authentication bypass can change the posture of every relying system. Inheritance is a continuing dependency, not a one-time reference.

## 6.4 Identity Risk Within RMF

Identity risk includes incorrect establishment, weak authentication, excessive authorization, compromised credentials, unsafe federation, stale lifecycle state, indirect privileged control, and corruption of trusted identity systems.

RMF records and accepts risk. Technical analysis must identify the failed trust-chain component and its consequence.

### 6.4.1 Authentication risk

Authentication risk occurs when a system accepts an untrusted claimant as a principal. It includes weak passwords, phishable MFA, stolen certificates, unsafe recovery, and legacy authentication paths.

Identify the weakest path that can produce the relevant authority. A privileged administrator can use phishing-resistant authentication and still face risk through a password-based fallback.

Document the effective authentication architecture, not merely its strongest component.

### 6.4.2 Authorization risk

Authorization risk exists when an authenticated principal has authority inconsistent with mission, policy, role, or architecture.

Direct membership is only one source of authority. Nested groups, delegation, ACEs, enrollment rights, management platforms, synchronization privileges, application roles, and trusts can create effective access.

For Tier 0 and other high-value systems, analyze effective control. Use that analysis as evidence for restricted privileged access.

### 6.4.3 Credential risk

Credential risk includes compromise of authentication material and compromise of systems that generate, store, replace, or recover it.

Passwords, hashes, Kerberos keys, cached credentials, certificates, private keys, LAPS secrets, managed-service-account material, refresh tokens, application secrets, and sessions can all convey authority.

Risk depends on reuse and reach. A CA or federation signing key can manufacture trusted identity material. It requires different treatment from a local workstation credential.

### 6.4.4 Federation risk

Federation imports identity decisions across a boundary. It depends on the identity provider, signing material, claims processing, relying-party configuration, and partner lifecycle.

An issuer can be wrong. Signing material can be compromised. Claims can be unsafe. A relying party can accept an assertion for another audience. An external identity can remain valid after local authorization should expire.

Document the trust relationship and each side’s security function. “Single sign-on” does not describe the authority being imported.

### 6.4.5 Privileged-access risk

Privileged access creates control-plane risk. Privileged identities can alter the systems that determine how identities, applications, credentials, networks, and controls operate.

Tier 0 administrators, CA administrators, federation administrators, virtualization administrators, backup administrators, and privileged-access platforms can each influence identity authority. Document effective administrative capability, not only traditional privileged groups.

The security boundary is defined by control. Indirect control of a Tier 0 system remains Tier 0 authority.
