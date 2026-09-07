---
icon: user-injured
---

# Chapter 30 - Lateral Movement, Remote Administration, and Identity Propagation

### Abstract

Lateral movement is the process of using existing authority to reach additional systems, services, identities, and administrative contexts. In Active Directory and hybrid environments, movement commonly occurs through legitimate remote-administration mechanisms, reusable credentials, Kerberos tickets, service accounts, management platforms, administrative shares, remote desktop, PowerShell remoting, Windows Management Instrumentation, Server Message Block, cloud sessions, and application identities. This chapter examines how adversaries select movement paths, evaluate network reachability, reuse authentication material, inherit active sessions, traverse administrative boundaries, and use trusted management infrastructure to expand operational reach. Offensive analysis emphasizes path selection, minimal-impact validation, and movement toward mission-relevant objectives rather than indiscriminate host compromise. Defensive analysis focuses on administrative tiering, segmentation, protocol restriction, credential isolation, remote-session controls, telemetry correlation, and disruption of movement chains. The chapter establishes that lateral movement is fundamentally identity propagation: authority moves when credentials, sessions, tokens, permissions, or trusted administrative relationships are accepted by another system.
