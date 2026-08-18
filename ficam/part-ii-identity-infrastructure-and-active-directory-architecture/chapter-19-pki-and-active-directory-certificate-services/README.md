---
icon: expeditedssl
---

# Chapter 19 - PKI and Active Directory Certificate Services

### Abstract

Active Directory Certificate Services (AD CS) provides the Public Key Infrastructure (PKI) core for enterprise identity, enabling strong authentication, data encryption, and digital signatures. Within Federal Identity, Credential, and Access Management (FICAM) frameworks, integrating AD CS with Federal PKI (FPKI) trust chains, smart cards (PIV/CAC), and Hardware Security Modules (HSMs) is critical for achieving Authenticator Assurance Level 3 (AAL3) under NIST SP 800-63 and enforcing Zero Trust Access (NIST SP 800-207). However, because client certificates can map directly to Active Directory accounts via Kerberos PKINIT, AD CS functions as a primary Tier 0 control plane component—where minor template or policy misconfigurations can undermine the security of the entire forest.

This chapter delivers a technical analysis of AD CS architecture, certificate enrollment mechanics, and enterprise PKI governance. It examines X.509 certificate construction, CA hierarchies, template configuration, enrollment services (NDES, SCEP, CES/CEP), certificate mapping, and revocation infrastructure (CRLs, OCSP). By analyzing offensive attack vectors—such as arbitrary Subject Alternative Name (SAN) injection (ESC1/ESC6), certificate enrollment abuse (ESC1–ESC13), and CA private key extraction—alongside defensive controls (template hardening, NTAuth Store auditing, HSM integration, and policy enforcement), this chapter equips security engineers to secure public key infrastructure as a resilient identity authority.

##
