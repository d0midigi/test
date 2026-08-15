---
icon: id-badge
---

# Chapter 14 - Credential and Secret Storage

### Abstract and Introduction

Security literature frequently references Active Directory's "keys to the kingdom." Depending on the source, this metaphor typically points to one of four constructs:

1. The Domain Controller infrastructure.
2. High-privilege administrative groups (Domain Admins, Enterprise Admins).
3. The master Kerberos Ticket Granting Service (TGS) hash (`krbtgt`).
4. Complex Access Control Lists (ACL) topologies and delegation misconfigurations.

While these elements represent critical operational control points, they overlook the core mechanic of initial access and lateral movement: the raw credential artifacts themselves.

An adversary rarely begins an intrusion with a `krbrtgt` hash or a direct Domain Admin token. Instead, access is established and expanded through compromised credentials - harvested from misconfigured passwords, exposed Active Directory Certificate Services (AD CS) templates and general infrastructure, or cached secrets left unprotected on endpoints. In practice, the primary credential stores host the actual "keys to the kingdom."

Credential storage architecture defines the ultimate boundary of identity assurance in Active Directory and Windows enterprise environments. Within Federal, Identity, Credential, and Access Management (FICAM) frameworks, securing secrets at rest - whether residing in LSASS memory, local registry hives, `NTDS.dit`, database tables, or directory attributes - is fundamental to halting post-exploitation tradecraft. Modern Windows operating systems maintain a layered web of secret stores, extending from legacy NTLM hashes and DPAPI master keys to hypervisor-isolated LSASS structures (Virtualization-Based Security (VBS)) and TPM-bound cloud artifacts.

This chapter delivers a technical analysis of credential storage mechanisms across Windows enterprise environments. It examines the cryptographic structures underlying NT hashes, Kerberos keys, LSA secrets, DPAPI master keys, Windows LAPS (v2), gMSA/dMSA architecture, and Primary Refresh Tokens (PRTs). By analyzing adversary exposure surfaces - such as LSASS memory dumping, offline registry parsing, DPAPI domain key extraction, and cleartext attribute harvesting - alongside defensive controls (Credential Guard, VBS, Protected Users, and Tiered Administration), this chapter details how to eliminate high-risk credential exposure in alignment with Zero Trust principles (NIST SP 800-207, OMB M 19-22), Digital Identity Guidelines (NIST SP 800-63), and security control baselines (NSIT SP 800-53).
