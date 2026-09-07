---
icon: dice-d10
---

# Chapter 31 - Identity Persistence, Durable Access, and Control-Plane Persistence

### Abstract

Persistence in identity environments is the preservation of usable authority after the original foothold, credential, session, or administrative path has been removed. This chapter examines persistence across Active Directory, Microsoft Entra ID, PKI, Group Policy, Kerberos, service identities, applications, federation, synchronization, management platforms, and recovery infrastructure. Offensive analysis focuses on durable identity relationships such as delegated permissions, group control, AdminSDHolder, replication rights, Kerberos keys, delegation, certificate authentication, Shadow Credentials, application identities, privileged roles, synchronization authority, and management-plane access. Defensive analysis emphasizes identifying unauthorized durable relationships, monitoring high-value directory and cloud changes, distinguishing legitimate administration from persistence creation, correlating persistence with subsequent authentication, and restoring trust rather than merely deleting visible artifacts. The chapter establishes that persistence is not defined by malware surviving a reboot. In identity-centric operations, the most consequential persistence may be a legitimate-looking permission, certificate, application, key, role, or trust relationship that allows an adversary to reconstruct authority long after the original compromise appears to have been contained.
