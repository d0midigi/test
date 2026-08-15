---
icon: rocket-launch
---

# Chapter 7 - Identity Infrastructure Networking

### Abstract

Identity infrastructure relies on legacy and modern network transport protocols to perform authentication, directory lookups, policy enforcement, and trust validation. In Federal Identity, Credential, and Access Management (FICAM) architectures, securing transport paths is as vital as securing stored identity secrets. Unencrypted, unauthenticated, or loosely segmented network connections expose Kerberos tickets, NTLM challenges, RADIUS requests, and directory queries to network-based adversaries.

This chapter analyzes the networking mechanics powering Active Directory (AD) and Network Access Control (NAC) environments. It explores how attackers exploit protocol fallbacks, weak EAP implementations, broadcast name resolution, and missing transport-layer signatures to intercept or relay identity traffic. Corresponding defensive blueprints provide the configurations required to build Zero Trust Network Access (ZTNA) boundaries, enforce cryptographic transport, and achieve FICAM alignment under NIST SP 800-207 and NIST SP 800-53 controls.

### Key Terminology

Identity, Credential, and Access Management (ICAM); Federal Identity, Credential, and Access Management (FICAM); Active Directory (AD) security; identity infrastructure; network segmentation; trust boundaries; authentication flows; Directory Services integration; credential theft prevention; privilege escalation mitigation; lateral movement defense; Zero Trust Architecture (ZTA); protocol hardening
