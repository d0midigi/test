---
icon: windows
---

# Chapter 13 - Windows Domain Credential and Secret Storage

### Abstract

Chapter 13 examines where authentication material resides after identities, passwords, keys, tickets, certificates, and tokens enter the Windows and hybrid identity environment. It covers NT hashes, Kerberos keys, supplemental credentials, password history, SAM, `SYSTEM`, and `SECURITY` hives, BootKey, LSA secrets, cached domain credentials, machine and trust secrets, service-account passwords, MSAs, gMSAs, dMSAs, KDS root keys, Windows LAPS, DPAPI, Credential Manager, certificate stores, private keys, TPMs, PIV/CAC keys, HSMs, Kerberos ticket caches, keytabs, browser sessions, Entra access and refresh tokens, Primary Refresh Tokens (PRTs), OAuth secrets, managed identities, and workload federation.

It also examines secret exposure through memory, backups, snapshots, logs, scripts, source control, Ci/CD platforms, remote administration, and recovery mechanisms. The chapter emphasizes credential chaining, secret-zero design, tiering, credential rotation, revocation, detection, incident response, and forest-compromise recovery. Its central premise is that authentication cannot remain trustworthy when the artifacts representing identity can be stolen, copied, derived, or recovered elsewhere.
