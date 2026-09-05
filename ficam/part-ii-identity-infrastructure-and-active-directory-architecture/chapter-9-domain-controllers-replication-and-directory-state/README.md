---
icon: compass
---

# Chapter 9 - Domain Controllers, Replication, and Directory State

### Abstract

Chapter 9 examines the systems and data structures that maintain authoritative Active Directory state. It covers writable and Read-Only Domain Controllers (RODCs), Global Catalog (GC) servers, Flexible Single Master Operations (FSMO) roles, replication topology, Knowledge Consistency Checker (KCC) behavior, DRSR, DRSUAPI, Update Sequence Numbers, Invocation IDs, up-to-date vectors, replication metadata, conflict resolution, deleted objects, lingering objects, and database convergence.

This chapter also examines `NTDS.dit`, Extensible Storage Engine (ESE) architecture, transaction logs, `SYSVOL`, registry hives, BootKey protection, system-state backups, and forest-recovery concepts. Repliation rights and DCSync are introduced as examples of how legitimate control-plane functionality can become credential-access authority. Defensive topics include domain controller hardening, hypervisor and backup exposure, replication telemetry, directory-state validation, and incident response considerations. The chapter frames replication not simply as an availability mechanism but as the process by which identity authority is distributed, synchronized, corrupted, investigated, and ultimately restored.
