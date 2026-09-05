---
icon: osi
---

# Chapter 11 - Windows Authentication, Groups, Security Descriptors, and Effective Access

### Abstract

Chapter 11 examines how Windows converts authenticated identity into actual authority. It covers security principals, Security Identifiers (SIDs), access tokens, security descriptors, DACLs, SACLs, Access Control Entries (ACEs), ownership, standard and generic rights, object-specific permissions, extended rights, privileges, integrity levels, user rights, and access evaluation. Active Directory gropu architecture is explored through Domain Local, Global, and Universal groups, nesting, AGDLP and AGUDLP, token expansion, SID History, Foreign Security Principals, local groups, and Group Policy-driven authorization.

The chapter distinguishes effective access from effective control, emphasizing that a principal may control another identity through password reset, group modification, DACL manipulation, GPO control computer-object permissions, PKI authority, service identity, or management infrastructure without appearing in a traditional administrator group. Shadow administrators, `AdminSDHolder`, delegation, separation of duties, Just-In-Time (JIT) access, and least privilege are treated as attack-pathway problems. The chapter ultimately establishes authorization graphing as a central method for identifying who can actually control what.

### Key Terminology

