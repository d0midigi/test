---
icon: game-board-simple
---

# Chapter 99 - Active Directory Object Deletion, Tombstone Reanimation, Lingering Objects, and Replication Residue Abuse (Offensive)

### Abstract

Deleting an Active Directory object does not immediately erase every trace of its identity or security state. Tombstones, deleted-object containers, Recycle Bin data, replication metadata, stale replicas, lingering objects, backups, and restored objects create a complex lifecycle in which identity state can survive removal or reappear later. This chapter examines deletion and replication residue primarily from the offensive perspective, focusing on object removal as defense evasion, reanimation of previously privileged principals, residual security identifiers, restored ACLs, deleted computer identities, stale replication partners, lingering objects, authoritative restoration, and the possibility that compromised state can return through recovery or replication. Defensive treatment follows through deletion protection, Recycle Bin governance, replication health monitoring, metadata review, stale-domain-controller removal, recovery validation, identity reconciliation, and trust restoration.
