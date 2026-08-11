---
icon: fingerprint
---

# Chapter 5 - FICAM and DoD ICAM

### Abstract

Federal Identity, Credential, and Access Management (FICAM) provides the federal government's enterprise approach for designing, planning, and operating common Identity, Credential, and Access Management (ICAM) processes. Its significance is broader than authentication technology. FICAM addresses how identities are established, how credentials are associated with those identities, how attributes are governed, how access is granted and removed, how federation allows externally managed identities to be trusted, and how those processes are governed across an agency. The current FICAM Architecture explicitly treats identity management, credential management, access management, federation, and governance as interdependent parts of an enterprise ICAM program rather than as isolated technical capabilities. ([1](https://www.idmanagement.gov/arch/))

Within the Department of Defense, ICAM must support a more operationally diverse environment. Identity services may be delivered at the DoD enterprise, Component, Community of Interest, or local level, and mission-partner identity functions may originate outside DoD entirely. The DoD Enterprise ICAM Reference Design recognizes that reality and provides architectural guidance for how those capabilities interact rather than prescribing one universal implementation. It also explicitly recognizes that mission requirements can require Component or local services when enterprise services do not satisfy operational needs.

This distinction is critical for federal Active Directory security.

An Active Directory account is not the beginning of identity. It is one technical representation of an identity whose authoritative existence may have been established elsewhere. Likewise, successful domain authentication is not the end of ICAM. The resulting principal may still require authorization based on attributes, role, device context, mission assignment, policy, or federation relationships maintained outside the domain.

The identity lifecycle therefore extends on both sides of Active Directory.

Before an account exists, a subject may be sponsored, proofed, vetted, enrolled, and associated with authoritative attributes. After an account is created, credentials must be bound, access granted, permissions maintained, role changes reflected, authenticators replaced, and access eventually removed. FICAM's current lifecycle guidance emphasizes that identity management extends from creation and proofing through maintenance and deactivation rather than reducing identity governance to credential issuance. ([2](https://www.idmanagement.gov/playbooks/ilm/))

For offensive and defensive security practitioners, this broader model exposes attack surfaces that traditional domain-centric assessments can miss. The adversary may target the credential rather than the account, the attribute rather than the credential, the provisioning path rather than the directory object, or the federation relationship rather than the local authentication system. An apparently secure Active Directory configuration can still inherit risk from an upstream identity process or downstream authorization system.

Chapter 5 establishes that lifecycle and trust model before the book moves into the network and directory architecture that implements significant portions of it.

### Keywords

FICAM; DoD ICAM; identity lifecycle; identity proofing; credential management; access management; federation; digital identity assurance; IAL; AAL; FAL; PIV; CAC; EDIPI; authoritative attributes; mission-partner identity; non-person entity

### Key terms

**Federal Identity, Credential, and Access Management (FICAM):** The federal government's enterprise approach for designing, planning, and executing common ICAM processes across identity management, credential management, access management, federation, and governance. ([1](https://www.idmanagement.gov/arch/))

**Identity proofing:** The process through which evidence is collected, validated, and verified to establish confidence that a claimed identity corresponds to the subject presenting that claim. NIST SP 800-63A-4 defines the current federal technical requirements for identity proofing and enrollment across three Identity Assurance Levels. ([3](https://csrc.nist.gov/pubs/sp/800/63/a/4/final))

**Credential:** An object or data structure that authoritatively binds an identity to at least one authenticator or provides information through which that binding can be established.

**Authenticator:** Something the claimant possesses and controls for use in an authentication protocol. Authentication assurance concerns confidence that the claimant controls one or more authenticators bound to the subscriber account. ([4](https://csrc.nist.gov/pubs/sp/800/63/b/4/final))

**Authoritative attribute:** An identity or authorization attribute whose value originates from a source designated as authoritative for that information.

**Federation:** An arrangement in which separately administered systems rely on an identity provider or credential service provider to convey authenticated identity information and, where applicable, subscriber attributes to relying parties. ([5](https://csrc.nist.gov/pubs/sp/800/63/c/4/final))

**Person Entity:** A human subject represented within an ICAM environment.

**Non-Person Entity (NPE):** A non-human entity requiring identity, credential, authentication, authorization, or lifecycle treatment, such as a device, service, application, workload, or automated process.
