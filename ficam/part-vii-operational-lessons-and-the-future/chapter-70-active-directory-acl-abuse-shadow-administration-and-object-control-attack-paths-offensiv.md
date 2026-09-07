---
icon: disease
---

# Chapter 70 - Active Directory ACL Abuse, Shadow Administration, and Object-Control Attack Paths (Offensive)

### Abstract

Active Directory privilege is not confined to Domain Admins, Enterprise Admins, or other obvious administrative groups. Much of the directory’s real authority is encoded in object ownership, access control entries, delegated permissions, extended rights, inheritance, attribute-level write permissions, and relationships that allow one principal to modify another. This chapter examines Active Directory primarily from the offensive perspective, treating discretionary access control lists and security descriptors as a graph of exploitable authority. It explores GenericAll, GenericWrite, WriteDACL, WriteOwner, password-reset rights, group control, Service Principal Name manipulation, Shadow Credentials, Resource-Based Constrained Delegation, Group Policy control, computer-object abuse, Local Administrator Password Solution and group Managed Service Account credential exposure, replication rights, AdminSDHolder, and multi-hop permission chains. Defensive analysis follows with delegation reduction, ownership control, protected-object analysis, permission baselining, attack-path monitoring, directory-change detection, and adversarial validation. The chapter establishes that the most dangerous Active Directory administrator may be a principal whose name never appears in a privileged group.
