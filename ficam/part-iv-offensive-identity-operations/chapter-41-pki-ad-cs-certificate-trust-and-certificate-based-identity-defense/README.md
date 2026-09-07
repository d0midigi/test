---
icon: face-clouds
---

# Chapter 41 - PKI, AD CS, Certificate Trust, and Certificate-Based Identity Defense

### Abstract

Public Key Infrastructure can strengthen identity assurance only when certificate issuance, enrollment, mapping, private-key protection, and certification-authority administration remain trustworthy. This chapter examines defensive engineering for Active Directory Certificate Services, enterprise certification authorities, certificate templates, enrollment permissions, subject construction, Extended Key Usage, PKINIT, certificate mapping, autoenrollment, enrollment agents, web enrollment, revocation, key archival, hardware security modules, PIV/CAC, device certificates, and certificate-based cloud authentication. Offensive analysis focuses on the trust assumptions that permit an adversary to transform ordinary enrollment, delegated administration, relayable authentication, template control, or CA compromise into another identity. Defensive analysis emphasizes Tier 0 isolation, strong identity binding, least-privilege enrollment, relay-resistant enrollment services, protected private keys, template governance, telemetry, revocation readiness, attack-path reduction, and trusted PKI recovery. The chapter establishes that certificate security must be engineered as identity security: the system is only trustworthy when an adversary cannot obtain, manufacture, map, or preserve a credential representing authority they were never entitled to possess.
