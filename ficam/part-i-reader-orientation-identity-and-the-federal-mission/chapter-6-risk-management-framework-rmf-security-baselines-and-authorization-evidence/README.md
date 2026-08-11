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
