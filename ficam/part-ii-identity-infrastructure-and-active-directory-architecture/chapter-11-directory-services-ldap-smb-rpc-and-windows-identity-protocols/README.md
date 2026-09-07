---
icon: osi
---

# Chapter 11 - Directory Services, LDAP, SMB, RPC, and Windows Identity Protocols

### Abstract

Active Directory authority is exposed through a collection of network protocols that allow clients, administrators, applications, and domain controllers to discover, authenticate to, query, modify, and manage identity infrastructure. This chapter examines Lightweight Directory Access Protocol (LDAP), Global Catalog access, Server Message Block (SMB), Microsoft Remote Procedure Call (MSRPC), named pipes, Netlogon, SAMR, LSARPC, DRSR, WinRM, WMI/DCOM, Remote Registry, and related Windows management interfaces. Particular attention is given to signing, encryption, channel binding, Extended Protection for Authentication, authentication negotiation, protocol fallback, coercion, and relay resistance. Offensive analysis examines how adversaries enumerate identity state, abuse exposed management interfaces, coerce authentication, relay credentials, and chain legitimate protocols into attack paths. Defensive analysis emphasizes protocol reduction, signing and binding requirements, segmentation, endpoint hardening, telemetry, and validation of legacy dependencies. The chapter establishes that protocol exposure is identity exposure: the security of Active Directory depends not only on credentials and permissions, but on how identity services are reached and how authentication is protected in transit.

### Key Terminology

