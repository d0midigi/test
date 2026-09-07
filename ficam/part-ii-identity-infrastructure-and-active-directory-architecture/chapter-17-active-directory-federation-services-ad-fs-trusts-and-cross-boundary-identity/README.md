---
icon: skyatlas
---

# Chapter 17 - Active Directory Federation Services (AD FS), Trusts, and Cross-Boundary Identity

### Abstract

Identity authority does not stop at the edge of a domain, forest, tenant, enclave, or agency. Trust relationships allow one security boundary to accept authentication or identity assertions originating from another, extending both legitimate access and potential attack paths. This chapter examines Active Directory domain and forest trusts, Kerberos referrals, trust direction and transitivity, trusted-domain objects, foreign security principals, SIDHistory, SID filtering, selective authentication, federation, Microsoft Entra cross-tenant identity, hybrid identity, and mission-partner access. Offensive analysis focuses on trust enumeration, cross-boundary privilege, compromised foreign principals, weak filtering, migration artifacts, shared administrative infrastructure, federation abuse, and upstream identity-provider compromise. Defensive analysis emphasizes trust minimization, explicit authentication scope, privilege isolation, telemetry, relationship recertification, partner governance, and cross-boundary incident containment. The chapter establishes that trust should never be interpreted as general confidence in another environment; it is a specific technical decision about which identities, assertions, attributes, and authority relationships one security boundary is willing to accept from another.



##
