---
icon: podcast
---

# Chapter 45 - Authentication Analytics, Kerberos and NTLM Detection, and Identity Behavior Analysis

### Abstract

Authentication telemetry is one of the richest and most difficult evidence sources in identity security because legitimate activity is constant, repetitive, distributed, and highly dependent on user, device, service, protocol, and application context. This chapter examines detection engineering for Kerberos, NTLM, password-based authentication, privileged logons, remote access, service accounts, certificate authentication, cloud sign-ins, multifactor authentication, device context, tokens, and session behavior across Active Directory and Microsoft Entra ID. Offensive analysis focuses on the authentication patterns produced by password spraying, credential reuse, ticket abuse, relay, service-account misuse, forged authentication artifacts, anomalous privilege use, and movement between trust boundaries. Defensive analysis emphasizes behavioral baselining, protocol-aware analytics, sequence detection, source-target correlation, privileged-context enrichment, anomaly scoring, and adversarial validation. The chapter establishes that malicious authentication is rarely identifiable from a single successful logon. Defenders must determine whether the identity, authenticator, protocol, source, target, timing, and resulting authority form a pattern consistent with legitimate mission activity.
