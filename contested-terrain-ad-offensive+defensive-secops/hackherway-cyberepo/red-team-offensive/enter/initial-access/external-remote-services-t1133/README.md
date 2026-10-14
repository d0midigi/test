---
description: 'MITRE ATT&CK Tactic #T1133'
---

# External Remote Services (T1133)

The use of external remote services is a common tactic employed by adversaries to gain initial access to a network or to estabish persistence within the network. These services, such as VPNs, Citrix, Windows Remote Management, and others, provide a gateway for users to connect to internal enterprise resources from external locations. Adversaries may exploit vulnerabilities in these services to breach the network, especially if they have access to valid accounts obtained through methods like credential phishing or by compromising the enterprise network.

Once an adversary gains access to these remote services, they can use them as a redundant or persistent access mechanism during their operation, enabling them to maintain a presence within the network even if other avenues of access are discovered and closed off. It's crucial for organizations to implement strong authentication mechanisms, regularly monitor remote access activities, and conduct security assessments to identify and address any vulnerabilities in external-facing services that could be exploited by threat actors.
