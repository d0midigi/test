---
icon: apartment
---

# Chapter 10 - Domain Controllers, Replication, and Directory State

### Abstract

Domain controllers are the systems through which Active Directory authority becomes persistent, replicated, and operational. This chapter examines writable domain controllers, Read-Only Domain Controllers, Global Catalog servers, Flexible Single Master Operations roles, `NTDS.dit`, Extensible Storage Engine internals, `SYSVOL`, directory replication, replication metadata, Update Sequence Numbers, invocation IDs, convergence, deleted objects, lingering objects, virtualization, backup, restoration, and recovery. Offensive analysis focuses on replication authority, directory database exposure, domain-controller administrative paths, credential-bearing backups, virtualization dependencies, and techniques that allow an adversary to manipulate or extract authoritative identity state. Defensive analysis emphasizes domain-controller isolation, replication-rights governance, state-integrity monitoring, clean administration, backup protection, recovery validation, and detection of unauthorized directory changes. The chapter establishes that domain-controller security is fundamentally a question of directory-state integrity: whoever can read, replicate, alter, restore, or redefine authoritative directory state may possess control over the identities and trust relationships that depend upon it.

