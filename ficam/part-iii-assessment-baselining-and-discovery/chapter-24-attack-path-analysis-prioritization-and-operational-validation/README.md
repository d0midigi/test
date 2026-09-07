---
icon: user-secret
---

# Chapter 24 - Attack-Path Analysis, Prioritization, and Operational Validation

### Abstract

Before an operational assessment team or an external adversary sends a single IP packet to an enterprise perimeter, critical details regarding its identity architecture, credential conventions, and cloud federation boundaries are already visible across the public internet. In federal and defense contexts, passive identity reconnaissance leverages open-source intelligence (OSINT), public cryptographic registries, and unauthenticated cloud service APIs to construct a comprehensive map of an organization's identity attack surface—all without triggering intrusion detection systems (IDS) or Security Operations Center (SOC) alerts.

Attack-path analysis converts collected identity relationships into an operational model of how authority can actually be reached. This chapter examines how users, groups, computers, credentials, sessions, ACLs, delegation, Group Policy, PKI, trusts, cloud roles, applications, management systems, and recovery infrastructure combine into paths toward mission-relevant control. Readers learn to distinguish graph reachability from practical exploitability, identify path prerequisites, assign confidence, compare path cost, measure path diversity, identify choke points, and prioritize high-value destinations. Offensive analysis focuses on selecting realistic routes, validating critical edges, minimizing operational impact, and proving consequence without unnecessary privilege escalation. Defensive analysis emphasizes path reduction, choke-point remediation, privileged-access isolation, credential-placement control, relationship monitoring, and continuous graph validation. The chapter establishes that the shortest path is not necessarily the most dangerous, the most privileged target is not necessarily the most important, and a finding is not complete until the assessor can explain why the path matters, what assumptions it depends upon, and which relationship should be changed to break it.
