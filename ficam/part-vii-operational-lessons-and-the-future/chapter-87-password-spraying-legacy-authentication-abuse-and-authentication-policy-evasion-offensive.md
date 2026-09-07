---
icon: jira
---

# Chapter 87 - Password Spraying, Legacy Authentication Abuse, and Authentication-Policy Evasion (Offensive)

### Abstract

Password-based authentication remains exploitable even in environments that deploy PIV/CAC, multifactor authentication, smart-card enforcement, conditional access, and modern passwordless methods because legacy protocols, fallback paths, service identities, hybrid systems, emergency workflows, and inconsistent policy enforcement often preserve alternate routes to the same identity. This chapter examines authentication-policy evasion primarily from the offensive perspective, progressing from account and password-policy reconnaissance through password spraying, low-and-slow authentication, account-state inference, Kerberos preauthentication behavior, NTLM and legacy protocol exposure, hybrid identity synchronization, federation endpoints, VPN and remote-access services, cloud authentication, and fallback from phishing-resistant authentication to reusable credentials. Particular attention is given to identifying where an agency’s nominal authentication assurance differs from the assurance actually enforced by every reachable service. Defensive treatment follows through passwordless migration, PIV/CAC enforcement, legacy authentication retirement, smart-lockout engineering, authentication-policy segmentation, telemetry correlation, and adversarial validation. The chapter establishes that strong authentication is meaningful only when weaker alternate paths cannot reach the same authority.
