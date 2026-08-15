---
icon: windows
---

# Chapter 13 - Windows Authentication and Kerberos

### Abstract

Chapter 13 explores the intricate role of Windows authentication and how it acts as the foundational gatekeeper of Active Directory, validating identity claims before granting access to network resources. In Federal Identity, Credential, and Access Management (FICAM) architectures, identity assurance demands strong, cryptographically backed authentication mechanisms compliant with the NIST SP 800-63 guidelines. Active Directory relies on two primary protocols: legacy NTLM challenge-response and enterprise Kerberos v5, coordinated locally by the Local Security Authority Subsystem Service (LSASS).

This chapter provides a comprehensive technical teardown of Windows authentication mechanisms, ticket-granting physics, and identity delegation models. It covers NTLM mechanics, Kerberos ticket exchanges (AS/TGS), Privilege Attribute Certificates (PAC), PKINIT smart card authentication, and Kerberos delegation extensions (S4U2Self/S4U2Proxy). By examining threat tradecraft—including Kerberoasting, AS-REP Roasting, Golden/Silver Tickets, Pass-the-Hash/Ticket, and RBCD abuse—alongside defensive configurations (Protected Users, Kerberos FAST, NTLM deprecation, and Authentication Policies/Silos), this chapter enables security engineers to design and defend resilient enterprise authentication boundaries.
