# 6.8 eMASS and Authorization Evidence

The Enterprise Mission Assurance Support Service (eMASS) is where much of the Department of Defense Risk Management Framework becomes a durable authorization record. Within the material already established for this book, eMASS serves as the system of record for system categorizations, security plans, control implementation statements, assessment results, Plans of Action and Milestones (POA\&Ms), and authorization decisions. For identity-security findings, it is also where evidence demonstrating implementation and remediation is ultimately connected to the broader risk picture.

For the Active Directory security engineer, the difficult part is rarely uploading an artifact. The harder problem is translating a technically complex identity environment into evidence that accurately supports the security claim being made.

A production forest does not naturally organize itself according to RMF control statements. It contains users, computers, groups, Organizational Units, Group Policy Objects, Access Control Lists, trust relationships, service identities, certificate infrastructure, replication topology, authentication policies, privileged management systems, and a long history of administrative decisions. Some of those objects directly implement controls. Others alter how those controls behave. Still others create indirect paths through which an adversary can reach the same privileged outcome without touching the configuration that was originally assessed.

The authorization package has to make that environment understandable without pretending it is simpler than it is.

A control implementation statement might say that privileged access is restricted to authorized administrators. That statement is only useful when the evidence behind it identifies how privileged access is actually constrained. Dedicated administrative accounts, restricted logon locations, controlled group membership, privileged administrative workstations, authentication policies, access-management systems, auditing, and recertification may all contribute to the implementation.

If the evidence package contains only a screenshot of Domain Admins membership, the evidence proves the contents of one group at one point in time. It does not prove the broader claim.

Good authorization evidence follows the mechanism.

If Group Policy enforces the control, preserve the policy configuration and effective application state.

If directory permissions enforce it, collect the relevant Access Control Entries.

If a Privileged Access Management system mediates administrative access, provide evidence from that workflow.

If certificate-based authentication is part of the implementation, the certificate trust, enrollment model, mapping behavior, and applicable authentication policy belong in the evidence chain.

If a control is inherited, identify exactly what capability is inherited and where local responsibility resumes.

The authorization record should make it possible for an assessor to move from requirement to implementation to evidence without having to guess what happens between them.

An eMASS package becomes technically weak when those links are missing.
