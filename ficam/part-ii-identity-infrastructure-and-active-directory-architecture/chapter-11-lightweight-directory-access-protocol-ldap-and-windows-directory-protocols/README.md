---
icon: osi
---

# Chapter 11 - LDAP and Windows Directory Protocols

### Abstract

Chapter 11 shows us how Active Directory relies on a suite of application-layer and Remote Procedure Call (RPC) protocols that facilitate identity, queries, cross-forest authentication, administration, and directory replication. In Federal Identity, Credential, and Access Management (FICAM) architectures, these protocols serve as the primary transport mechanism for high-assurance credential evaluation and access policy enforcement; however, unencrypted, unsigned, or unauthenticated protocol mechanisms introduce severe security vectors, including credential interception, NTLM relaying, coercion primitives, and rogue directory replication.

This chapter provides a thorough analysis of Active Directory network protocols, covering the Lightweight Directory Access Protocol (Secure), LDAP/S, Simple Authentication and Security Layer (SASL), Netlogon (MS-NRPC), and core Microsoft RPC interfaces (SAMR, LSARPC, DRSR/DRSUAPI, EFSRPC, and MS-RPRN). By comparing and contrasting protocol mechanics against offensive methodologies, such as LDAP relaying, ZeroLogon, DCSync, authentication coercion, and RPC interface enumeration - alongside defensive configurations and secure implementations (LDAP Server Signing, Channel Binding Tokens, RPC filters, and Netlogon secure channel enforcement), this chapter arms security engineers with the 'know-how' to audit, restrict, and secure directory protocols in alignment with NIST SP 800-53 controls.

### Key Terminology

Remote Procedure Call (RPC); credential interception; NTLM Relay; coercion primitives; LDAP/LDAPS; SASL; Netllogon (MS-NRPC), SAMR;
