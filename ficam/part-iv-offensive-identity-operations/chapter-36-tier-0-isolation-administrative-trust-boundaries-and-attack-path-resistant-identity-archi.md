---
icon: box-ballot
---

# Chapter 36 - Tier 0 Isolation, Administrative Trust Boundaries, and Attack-Path-Resistant Identity Architecture

### Abstract

Defensive identity engineering begins by constraining where authority can originate, where it can travel, and which systems are permitted to influence the identity control plane. This chapter establishes the architectural foundation for attack-path-resistant Active Directory and hybrid identity environments through Tier 0 isolation, administrative trust boundaries, clean administrative sources, management-plane separation, credential containment, dedicated privileged identities, network segmentation, and explicit control of upstream dependencies. Offensive analysis examines how adversaries defeat nominal tiering through cross-tier authentication, shared management systems, virtualization, backup, PKI, synchronization, automation, security tooling, and other hidden administrative paths. Defensive analysis focuses on discovering effective Tier 0, separating control planes, eliminating trust inversions, constraining administration, and validating that lower-trust systems cannot influence higher-trust authority. The chapter treats administrative architecture as a graph problem rather than a collection of privileged groups. Its central principle is simple: a protected identity system is only as trustworthy as the least-trusted system capable of administering, recovering, configuring, authenticating, or replacing it.
