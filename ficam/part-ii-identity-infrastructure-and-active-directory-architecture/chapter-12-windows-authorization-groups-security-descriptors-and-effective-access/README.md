---
icon: users-line
---

# Chapter 12 - Windows Authorization, Groups, Security Descriptors, and Effective Access

### Abstract

Authentication establishes who or what a principal claims to be; authorization determines what that principal can actually do. This chapter examines the Windows authorization model from security identifiers, access tokens, groups, privileges, user rights, security descriptors, discretionary and system access-control lists, access-control entries, inheritance, ownership, Mandatory Integrity Control, User Account Control, and object-specific Active Directory permissions through effective access and delegated authority. Offensive analysis focuses on permission relationships that create privilege escalation, shadow administration, indirect control, token abuse, ownership paths, group nesting, delegated directory rights, and authorization through computers, services, Group Policy, and management infrastructure. Defensive analysis emphasizes least privilege, role separation, administrative tiering, effective-access review, permission baselining, drift detection, telemetry, and attack-path reduction. The chapter establishes a central principle for Windows security: assigned roles and group names do not define authority. Effective authority is determined by the complete set of permissions, identities, tokens, ownership relationships, and control paths Windows evaluates when access is requested.
