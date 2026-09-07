---
icon: brightness
---

# Chapter 34 - Cross-Forest, Federation, Hybrid, and Cross-Boundary Identity Control-Plane Compromise

### Abstract

Compromise of one identity authority becomes significantly more dangerous when other environments continue to trust what that authority asserts. This chapter examines how domain, forest, tenant, federation, certificate, synchronization, mission-partner, and application trust relationships can extend identity control-plane compromise beyond the original security boundary. It covers Active Directory forest trusts, foreign security principals, SIDHistory, selective authentication, federation services, signing authority, Microsoft Entra hybrid identity, cross-tenant access, synchronization, certificate trust, privileged management dependencies, and mission-partner identity. Offensive analysis focuses on determining which downstream systems accept identities, claims, attributes, certificates, or administrative actions originating from a compromised authority and demonstrating cross-boundary consequence without unnecessary expansion. Defensive analysis emphasizes trust minimization, boundary-specific authorization, upstream-authority monitoring, isolation, coordinated containment, key and certificate rotation, partner notification, and revalidation of accepted identity assertions. The chapter establishes that compromise propagation follows trust rather than network topology: an environment can remain technically uncompromised while its authorization decisions are corrupted by an identity authority it still believes.
