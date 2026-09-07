---
icon: triple-chevrons-up
---

# Chapter 37 - Authentication Hardening, Credential Boundaries, and Protocol-Resistant Identity Defense

### Abstract

Authentication hardening determines which credentials may represent an identity, where those credentials may be used, and which protocols and systems are permitted to accept them. This chapter examines defensive engineering for Kerberos, NTLM, certificate-based authentication, PIV/CAC, multifactor and phishing-resistant authentication, Windows Hello for Business, service identities, remote administration, delegation, protocol signing, channel binding, Extended Protection for Authentication, and hybrid Microsoft Entra authentication. Offensive analysis focuses on the alternate paths adversaries use when stronger authentication is deployed but weaker protocols, fallback behavior, delegation, credential placement, enrollment processes, or exceptions remain available. Defensive analysis emphasizes assurance-appropriate authentication, protocol reduction, credential isolation, source and target restrictions, managed identities, strong cryptography, telemetry, staged legacy retirement, and continuous validation. Particular attention is given to Identity Assurance Level, Authenticator Assurance Level, and Federation Assurance Level requirements in federal environments. The chapter establishes that authentication strength is determined not by the strongest method deployed, but by the weakest usable path capable of reaching the protected resource.
