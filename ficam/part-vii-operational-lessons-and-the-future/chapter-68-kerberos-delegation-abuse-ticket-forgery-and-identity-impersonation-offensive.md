---
icon: xbox
---

# Chapter 68 - Kerberos Delegation Abuse, Ticket Forgery, and Identity Impersonation (Offensive)

### Abstract

Kerberos is designed to let authenticated principals obtain service-specific authorization without repeatedly presenting long-lived credentials, but the same trust model creates powerful offensive opportunities when service accounts, delegation settings, ticket-signing keys, computer accounts, or directory permissions are compromised. This chapter examines Kerberos primarily from the attacker’s perspective: ticket acquisition, service-ticket targeting, delegation discovery, unconstrained and constrained delegation, Resource-Based Constrained Delegation, S4U extensions, service-account compromise, ticket reuse, forged authentication material, cross-domain trust, and the movement from one compromised identity into broader impersonation authority. Particular attention is given to the difference between possessing a password and possessing the ability to mint, request, redirect, or reuse Kerberos authentication. Defensive treatment follows the offensive analysis through delegation reduction, key protection, service-account hardening, encryption policy, privileged-authentication boundaries, ticket analytics, directory-change monitoring, and attack-path validation. The chapter establishes that Kerberos security depends not only on cryptography, but on who controls the principals and relationships that authorize ticket issuance and impersonation.
