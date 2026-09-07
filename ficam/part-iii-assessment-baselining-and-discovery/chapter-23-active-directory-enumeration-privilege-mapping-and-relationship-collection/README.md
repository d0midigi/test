---
icon: virus-covid
---

# Chapter 23 - Active Directory Enumeration, Privilege Mapping, and Relationship Collection

### Abstract

Chapter 23 focuses on how authenticated access to Active Directory exposes a large body of security-relevant metadata that can be used to reconstruct how authority actually operates across the domain and forest. This chapter develops a systematic enumeration workflow for users, groups, computers, organizational units, Group Policy Objects, service accounts, Service Principal Names, delegation, security descriptors, ownership, local administration, sessions, trusts, foreign principals, certificate-related objects, and privileged relationships. Offensive analysis focuses on transforming ordinary directory read access into a defensible map of administrative reach, credential exposure, delegation, shadow privilege, and potential attack-path edges without prematurely exploiting them. Defensive analysis applies the same methodology to identify excessive delegation, stale privilege, unmanaged administrative relationships, credential-placement risk, and discrepancies between documented and effective authority. Native Windows utilities, PowerShell, LDAP, and graph-based collection are treated as complementary evidence sources rather than substitutes for analysis. The chapter establishes enumeration as relationship collection: the objective is not to gather the largest possible directory dump, but to determine which identities can influence which systems, resources, and other identities.
