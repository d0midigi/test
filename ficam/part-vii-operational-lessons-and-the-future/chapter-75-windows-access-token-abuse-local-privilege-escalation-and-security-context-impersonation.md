---
icon: tire
---

# Chapter 75 - Windows Access Token Abuse, Local Privilege Escalation, and Security-Context Impersonation (Offensive)

### Abstract

A foothold on a Windows system does not automatically provide the authority needed to reach credentials, administrative interfaces, services, or Active Directory. The adversary must determine which security contexts exist locally and whether one can be stolen, impersonated, duplicated, elevated, or caused to perform an action on the attacker’s behalf. This chapter examines Windows local privilege escalation primarily from the offensive perspective, treating access tokens, privileges, service identities, process ownership, logon sessions, named-pipe impersonation, scheduled tasks, service control, local groups, User Account Control, and delegated operating-system rights as identity attack surfaces. Particular attention is given to transitions from standard user to local administrator or SYSTEM and to the subsequent extraction or reuse of domain-level authentication material. Defensive treatment follows through privilege reduction, service hardening, token isolation, Credential Guard, Local Security Authority protection, User Account Control configuration, privileged-session separation, endpoint telemetry, and attack-path validation. The chapter establishes that local privilege escalation matters because controlling a stronger Windows security context can expose stronger identity authority.
