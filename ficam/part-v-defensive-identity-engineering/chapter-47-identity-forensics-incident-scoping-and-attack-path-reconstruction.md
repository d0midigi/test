---
icon: dice-d20
---

# Chapter 47 - Identity Forensics, Incident Scoping, and Attack-Path Reconstruction

### Abstract

Identity forensics reconstructs how an adversary acquired, exercised, expanded, and preserved authority across interconnected identity systems. This chapter examines forensic investigation across Active Directory, Microsoft Entra ID, PKI, endpoints, privileged-access systems, applications, management infrastructure, federation, synchronization, and recovery platforms. Investigators learn to reconstruct authentication sequences, credential exposure, directory changes, privileged relationships, lateral movement, certificate issuance, cloud-role activity, persistence, replication abuse, and control-plane compromise while distinguishing observed evidence from inferred attacker capability. Offensive analysis identifies the artifacts and relationships created as an operator moves through an identity graph; defensive analysis uses those traces to establish the initial foothold, determine which credentials and authorities became untrustworthy, identify alternate paths, and measure the true blast radius. Particular attention is given to temporal reconstruction, replication metadata, independent evidence sources, compromised logging, credential-specific containment, and cross-plane correlation. The chapter establishes that incident scope must follow authority rather than hosts: the investigation is complete only when defenders can explain how the adversary moved, what they could control, which trust relationships were affected, and what must now be restored.
