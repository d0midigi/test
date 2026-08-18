---
icon: user-key
---

# Chapter 21 - Federation, Entra ID, and Hybrid Identity

### Abstract

Chapter 21 discusses how hybrid identity architectures bridge legacy on-premises Active Directory with cloud environments, serving as the connective identity mesh for federal agencies, military branches, and defense contractors. Within the Federal Identity, Credential, and Access Management (FICAM) framework, federating identity across Azure Government (GCC High, IL4/IL5/IL6) requires strict enforcement of NIST SP 800-207 Zero Trust principles, OMB M-19-17 mandates, and CMMC requirements. Because hybrid synchronization and federation tools bridge on-premises control planes with cloud control planes, they present high-value targets for advanced threat actors seeking cross-domain lateral movement and cloud tenant takeover.

This chapter provides a technical analysis of hybrid identity, cross-realm federation protocols, and cloud identity architecture. It evaluates SAML, OAuth 2.0, OpenID Connect, and WS-Trust token flows alongside AD FS claims transformation, Entra Connect synchronization mechanics (PHS, PTA, Federation), and cross-tenant access controls. By examining offensive attack vectors - such as Golden SAML assertion forgery, `MSOL_` service account compromise, Primary Refresh Token (PRT) theft, and Device Code Flow phishing - alongside defensive controls (Conditional Access, Continuous Access Evaluation, and cross-tenant policy enforcement), this chapter equips defense engineers to secure hybrid identity boundaries against cross-plane exploitation.
