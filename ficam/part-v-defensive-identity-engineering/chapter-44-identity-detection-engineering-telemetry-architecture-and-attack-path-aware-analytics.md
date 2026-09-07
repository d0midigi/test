---
icon: square-terminal
---

# Chapter 44 - Identity Detection Engineering, Telemetry Architecture, and Attack-Path-Aware Analytics

### Abstract

Identity detection engineering converts authentication, authorization, directory, endpoint, network, cloud, PKI, and management telemetry into evidence of adversary movement through the identity graph. This chapter establishes the detection architecture for Part VI by examining telemetry collection, normalization, identity correlation, privileged-context enrichment, behavioral baselining, attack-path-aware analytics, sequence detection, sensor health, and detection validation across Active Directory, Microsoft Entra ID, PKI, endpoints, applications, and hybrid infrastructure. Offensive analysis focuses on which actions generate observable evidence, which telemetry dependencies can be avoided or impaired, and how legitimate administrative mechanisms complicate attribution. Defensive analysis emphasizes independent evidence sources, high-value relationship monitoring, correlation across control planes, detection of new effective authority, and analytics tied to mission-relevant attack paths rather than isolated events. The chapter establishes that identity detection is strongest when defenders can determine not merely that something unusual occurred, but which identity relationship changed, what new authority became reachable, where the adversary can move next, and whether the evidence pipeline itself remains trustworthy.
