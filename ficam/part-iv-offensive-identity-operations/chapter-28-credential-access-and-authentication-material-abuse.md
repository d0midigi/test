---
icon: flask-round-poison
---

# Chapter 28 - Credential Access and Authentication Material Abuse

### Abstract

Credential access is the transition from controlling one security context to acquiring authentication material capable of representing another. This chapter examines how adversaries locate, extract, derive, capture, recover, and reuse passwords, hashes, Kerberos keys and tickets, certificates, private keys, cloud tokens, managed credentials, service secrets, application credentials, and directory-stored authentication material across Windows, Active Directory, Microsoft Entra ID, PKI, endpoints, servers, backups, and management systems. Offensive analysis emphasizes selecting credential targets according to attack-path value, validating exposure with minimal collection, and distinguishing possession of an artifact from practical authentication authority. Defensive analysis focuses on credential isolation, privileged-session placement, LSASS protection, managed identities, secret reduction, hardware-backed keys, retrieval controls, telemetry, rotation, token revocation, certificate response, and trust restoration. The chapter establishes that credential access should never be treated as indiscriminate secret harvesting: the operative question is which authentication artifact materially changes the adversary’s reachable authority and how defenders can prevent that transition.
