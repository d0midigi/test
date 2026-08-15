---
icon: file-certificate
---

# Chapter 15 - Human, Device, Service, and Non-Person Identity

### Abstract

Active Directory serves as the enterprise identity authority for both human users and a vast ecosystem of Non-Person Entities (NPEs) - including computer accounts, service principals, automated workloads, and device objects. In Federal Identity, Credential, and Access Management (FICAM) architectures, maintaining absolute visibility and control over the entire identity lifecycle (Joiner, Mover, Leaver - JML) across human and non-human accounts is vital for satisfying NIST SP 800-63 guidelines and enforcing Zero Trust policy constraints. Unmanaged NPEs and orphaned accounts frequently represent the weakest link in enterprise defense, offering adversaries unmonitored persistence and privilege escalation pathways.

This chapter provides a detailed analysis of human, device, service, and workload identity architectures within Active Directory. It examines machine account authentication, domain join mechanics (including offline and TPM-bound joins), service account evolutions (from legacy user-based accounts to gMSA and Windows Server 2025 dMSA), and automated identity lifecycle governance. By evaluating offensive tradecraft - such as machine account impersonation, gMSA password blob extraction, Kerberoasting service accounts, and exploiting stale NPE accounts - alongside defensive lifecycle configurations (automated deprovisioning, KDS root key protection, attestation, and periodic recertification), this chapter equips security architects to enforce identity governance across all enterprise entities.







