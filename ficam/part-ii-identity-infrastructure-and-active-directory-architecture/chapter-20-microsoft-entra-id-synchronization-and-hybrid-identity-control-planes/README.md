---
icon: lock-a
---

# Chapter 20 - Microsoft Entra ID, Synchronization, and Hybrid Identity Control Planes

### Abstract

Hybrid identity connects on-premises Active Directory with Microsoft Entra ID, cloud applications, device identity, federation, synchronization, and modern authentication services. This chapter examines Microsoft Entra Connect Sync, Microsoft Entra Cloud Sync, password hash synchronization, pass-through authentication, federation, source anchors, attribute flow, writeback, hybrid device identity, Primary Refresh Tokens, privileged cloud roles, application identities, and the administrative systems that bridge on-premises and cloud authority. Offensive analysis focuses on synchronization-account compromise, connector abuse, attribute manipulation, writeback paths, token theft, cloud-to-on-premises privilege relationships, application consent, and control-plane dependencies that allow compromise to move between environments. Defensive analysis emphasizes authoritative-source governance, synchronization hardening, Tier 0 treatment of identity bridges, privileged-role isolation, conditional access, telemetry correlation, configuration baselining, and recovery after hybrid compromise. The chapter establishes that hybrid identity is not simply directory synchronization: it is a bidirectional trust and administration system whose security depends on understanding exactly which identity attributes, credentials, devices, applications, and administrative authorities can influence each control plane.



##
