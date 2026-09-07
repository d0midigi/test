---
icon: grip-vertical
---

# Chapter 33 - Domain Dominance, Replication Abuse, and Identity Control-Plane Compromise

### Abstract

Domain dominance occurs when an adversary gains authority over the systems, keys, permissions, or replication mechanisms that establish identity trust across an Active Directory domain. At this point, the problem is no longer compromise of individual accounts; the attacker may be able to recover credential material, alter directory state, manufacture authentication artifacts, redefine privilege, or recreate access after ordinary remediation. This chapter examines domain-controller authority, directory replication, DCSync, NTDS.dit exposure, `krbtgt`, Kerberos trust keys, privileged directory permissions, AdminSDHolder, Group Policy, PKI dependencies, management infrastructure, and recovery systems as components of the identity control plane. Offensive analysis emphasizes proving domain-level consequence without unnecessary credential harvesting or destructive modification. Defensive analysis focuses on Tier 0 isolation, replication-rights governance, domain-controller protection, privileged-path reduction, telemetry, compromise scoping, key rotation, clean recovery, and attack-path recalculation. The chapter establishes that domain dominance is fundamentally a loss of confidence in authoritative identity state.
