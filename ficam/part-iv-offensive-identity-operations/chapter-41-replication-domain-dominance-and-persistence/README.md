---
icon: face-clouds
---

# Chapter 41 - Replication, Domain Dominance, and Persistence

### Abstract

Domain dominance and long-term persistence represent the final operational phase of an Active Directory compromise. Once Tier 0 access is established, threat actors seek to embed control mechanisms that survive security audits, password resets, domain controller rebuilds, and administrative sweeps. In federal, defense, and high-assurance enterprises operating under Federal Identity, Credential, and Access Management (FICAM) guidelines, NIST SP 800-53 (AC-2, IA-5) controls, and CISA Zero Trust Maturity Models, defending against domain-level persistence requires a deep understanding of Active Directory internal replication protocols, object schema mechanics, and cryptographic key lifecycles.

This chapter provides a comprehensive technical analysis of domain dominance, Directory Replication Service (DRS) manipulation, and advanced persistence tradecraft. It details DCSync mechanics via MS-DRSR, DCShadow rogue DC injection, Golden and Silver Ticket forgery, AdminSDHolder/SDProp backdoor injection, Directory Service Restore Mode (DSRM) account abuse, and LSASS Skeleton Key memory patching. Furthermore, it delivers actionable defensive engineering controls—including strict DS-Replication DACL auditing, dual `krbtgt` key rotation playbooks, Active Directory Database integrity monitoring, and real-time SIEM event correlation—to eradicate persistent threat actors from enterprise enclaves.

### 41.1 DCSync

### 41.2 DCShadow

### 41.3 Replication Rights

### 41.4 DRSR/DRSUAPI

### 41.5 NTDS.dit Extraction

### 41.6 KRBTGT Compromise

### 41.7 Golden Tickets

### 41.8 Silver Tickets

### 41.9 Diamond Tickets

### 41.10 Sapphire Tickets

### 41.11 PAC Manipulation

### 41.12 AdminSDHolder and SDProp

### 41.13 DSRM Persistence

### 41.14 Skeleton Key

### 41.15 SIDHistory Persistence

### 41.16 ACL and Group Backdoors

### 41.17 Golden Certificates

### 41.18 Rogue Certification Authorities

### 41.19 AD FS Token-Signing Key Compromise

### 41.20 DKM Secrets

### 41.21 Golden SAML

### 41.22 Rogue Federation

### 41.23 Persistent Hybrid and Cloud Trust
