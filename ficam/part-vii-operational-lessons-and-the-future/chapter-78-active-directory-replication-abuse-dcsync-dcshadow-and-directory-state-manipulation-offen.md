---
icon: grate
---

# Chapter 78 - Active Directory Replication Abuse, DCSync, DCShadow, and Directory-State Manipulation (Offensive)

### Abstract

Active Directory replication is designed to ensure that authoritative directory state converges across domain controllers. For an attacker, however, replication privileges can provide something far more consequential than ordinary administrative access: the ability to retrieve credential material, impersonate replication partners, inject unauthorized directory changes, manipulate security-relevant attributes, and potentially alter identity state while bypassing normal administrative workflows. This chapter examines replication abuse primarily from the offensive perspective, beginning with replication architecture and rights discovery before progressing through DCSync, replication-secret extraction, trust credential recovery, `krbtgt` compromise, DCShadow-style directory modification, rogue replication identities, metadata manipulation, persistence, and stealthy control-plane alteration. Particular attention is given to distinguishing domain administration from replication authority and to understanding how ACLs, delegated rights, domain-controller compromise, and backup access can create equivalent offensive capability. Defensive treatment follows through replication-right reduction, domain-controller isolation, metadata analytics, directory-state baselining, privileged change monitoring, credential rotation, and trust reconstitution. Replication security ultimately determines who is allowed to read or redefine authoritative identity state.
