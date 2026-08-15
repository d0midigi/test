---
icon: users-line
---

# Chapter 12 - Authorization, Groups, and Effective Access

### Abstract

Chapter 12 teaches us about authorization and how it dictates the ways in which authenticated security principals interact with directory objects and network resources in Active Directory. In Federal Identity, Credential, and Access Management (FICAM) frameworks, achieving Least Privilege (NIST SP 800-53 AC-6) and enforcing Zero Trust security architecture requires precise control over Security Descriptors, Access Control Lists (ACLs), privilege assignments, and group scope mechanics. Without rigorous access controls, misconfigured permissions create hidden operational paths that allow adversaries to execute domain-wide privilege escalation.

This chapter examines the mechanical inner workings of Active Directory authorization. It explores Security Identifiers (SIDs), access token construction, security descriptor evaluation, group architecture paradigms (AGDLP/AGUDLP), Foreign Security Principals (FSPs), and effective access calculations. By evaluating attack vectors—such as ACL-based privilege escalation (`WriteDacl`, `WriteOwner`, `GenericAll`), SID History injection, Primary Group ID abuse, and token bloat—alongside defensive controls (SDProp hardening, explicit SACL auditing, Dynamic Access Control, and automated graph-based ACL analysis), this chapter equips security architects to audit, control, and enforce authorization boundaries under strict federal compliance mandates.

##
