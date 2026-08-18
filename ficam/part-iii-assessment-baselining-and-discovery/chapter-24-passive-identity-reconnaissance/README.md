---
icon: user-secret
---

# Chapter 24 - Passive Identity Reconnaissance

### Abstract

Before an operational assessment team or an external adversary sends a single IP packet to an enterprise perimeter, critical details regarding its identity architecture, credential conventions, and cloud federation boundaries are already visible across the public internet. In federal and defense contexts, passive identity reconnaissance leverages open-source intelligence (OSINT), public cryptographic registries, and unauthenticated cloud service APIs to construct a comprehensive map of an organization's identity attack surface—all without triggering intrusion detection systems (IDS) or Security Operations Center (SOC) alerts.

This chapter details the covert methodologies used to audit and map an enterprise’s external identity footprint. It covers personnel and organizational OSINT, passive DNS and Certificate Transparency (CT) log analysis, exposure identification across public code repositories and breach datasets, and the extraction of Microsoft Entra ID / SAML federation metadata. Furthermore, it explores cloud tenant discovery, public identity portal fingerprinting, and external attack surface mapping. By establishing a rigorous reconnaissance hypothesis framework, this chapter equips identity security engineers, Red Teams, and ISSOs to evaluate public visibility, reduce external identity leakage, and harden public-facing identity infrastructure against passive reconnaissance techniques.
