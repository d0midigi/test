---
icon: apartment
---

# Chapter 10 - Directory Services, LDAP, SMB, RPC, and Windows Identity Protocols

### Abstract

Chapter 10 analyzes the network-facing protocol interfaces used to query, modify, administer, authenticate, and replicate Active Directory and Windows-based identity services. It details LDAP operations, including searches, binds, filters, controls, signing, sealing, StartTLS, LDAPS, channel binding, Global Catalog (GC) access, security descriptors, and directory modifications. It also examines essential administrative mechanisms - such as SMB, named pipes, RPC, Endpoint Mapper, SAMR, LSARPC, Netlogon, DRSR, DFS-R, Remote Registry, Service Control Manager, Windows Management Instrumentation (WMI), DCOM, and Windows Remote Management (WinRM) - highlighting how they simultaneously expand the network attack surface.

Rather than presenting isolated mitigations, Chapter 10 introduces holistic architectural defenses, including authentication relay, authentication coercion, Extended Protection for Authentiation (EPA\_, signing, channel binding, and protocol hardening. Additionally, it maps these activities to protocol telemetry and Windows security events, demonstrating how defenders can monitor both legitimate and malicious identity operations. The core theme is that many identity-based attacks exploit valid protocol behaviors rather than software flaws, making an advanced understanding of protocol mechanics indispensable for both offensive operators and defensive engineers.
