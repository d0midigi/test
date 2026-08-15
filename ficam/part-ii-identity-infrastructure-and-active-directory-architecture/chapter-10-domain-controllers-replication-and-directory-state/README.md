---
icon: apartment
---

# Chapter 10 - Domain Controllers, Replication, and Directory State

### Abstract

Domain Controllers (DCs) serve as the authoritative security hubs of Active Directory, managing database state, processing authentication requests, and replicating directory updates across the enterprise. In Federal Identity, Credential, and Access Management (FICAM) frameworks, the integrity of high-assurance identity credentials relies directly on the physical, logical, and cryptographic resilience of Domain Controllers and their storage architecture.

Chapter 10 examines the mechanical inner workings of Active Directory Domain Controllers, replication topologies, and low-level database operations. It analyzes the Extensible Storage Engine (ESE), database structures (`NTDS.dit`), database encryption keys (BootKey and Password Encryption Key (PEK)), and replication state mechanics. By contrasting internal directory operations against offensive tradecraft - including DCSync operations, VSS database extraction, RODC cache poisoning, and lingering object manipulation - this chapter delivers defensive engineering practices required to secure identity databases in alignment with Zero Trust principles and NIST Sp 800-53 security controls.
