---
icon: expeditedssl
---

# Chapter 19 - Active Directory Certificate Services (AD CS), PKI, and Certificate-Based Identity

### Abstract

Certificates can authenticate users, devices, services, applications, and workloads without relying on passwords, making Public Key Infrastructure (PKI) a critical component of the identity control plane. This chapter examines Active Directory Certificate Services (AD CS), certification authorities, certificate templates, enrollment, autoenrollment, subject construction, Extended Key Usage, certificate mapping, revocation, enrollment agents, web enrollment, key archival, and certificate lifecycle management. Offensive analysis focuses on identifying enrollment and template configurations that allow an adversary to obtain certificates representing another identity, abuse delegated enrollment, relay authentication to certificate services, manipulate certificate mappings, or compromise certification authority infrastructure. Defensive analysis emphasizes Tier 0 isolation, template governance, enrollment restrictions, strong identity binding, private-key protection, revocation, telemetry, attack-path analysis, and recovery after PKI compromise. Particular attention is given to PIV/CAC authentication and federal/DoD trust requirements. The chapter establishes that certificate authority is identity authority: any principal capable of obtaining, issuing, modifying, or manufacturing a trusted authentication certificate may possess effective control over the identity the certificate represents.



##
