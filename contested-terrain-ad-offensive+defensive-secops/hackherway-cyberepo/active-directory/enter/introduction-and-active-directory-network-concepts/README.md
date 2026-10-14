---
description: >-
  A Practical Ethical Hacking Guide to Active Directory-Offensive and Defensive
  Security Approaches (CNA/CND)
cover: ../../../.gitbook/assets/hhw-brand-banner.gif
coverY: 0
coverHeight: 303
layout:
  width: wide
  cover:
    visible: true
    size: full
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# Introduction & Active Directory Network Concepts

## Introduction

**Active Directory (AD) is a Microsoft directory service centralizing network management by organizing users, computers, and resources (like printers, files) in a hierarchical database, enabling secure authentication, authorization, and security policy enforcement via Group Policy Objects (GPO)  across Windows networks, replacing local logins with Single Sign-On (SSO) for an entire domain/forest structure (Domains, trees, forests), making large networks and their components manageable.**

**Core Network Concepts AD Manages**

* **Centralized Database:** A single repository (`ntds.dit`) for all User' and device information, unlike decentralized workgroups.
* **Authentication & Authorization:** Verifies users (who are you?) and grants access to specific resources (what can you do?).
* **Hierarchical Structure:** Organizes objects logically:
  * **Objects:** Computers, groups, printers.
  * **Organizational Units:** Containers for objects (e.g., by department) to apply user- and computer-based security policies.
  * **Domains:** Groups of objects sharing a database, a security boundary.
  * **Trees:** Multiple Domains with a shared namespace.
  * **Forests:** A collection of trees, representing the entire organizational structure.
* **Domain Controllers (DCs):** Servers hosting the AD database and handling authentication requests.
* **Group Policy Objects (GPOs):** Rules (security configurations) applied to OUs or Domains to enforce security standards for policy compliance.
* **Trusts:** Logical links or pathways between Domains/forests allowing resource sharing.

How It Works (Simplified)

1. **Logon:** User enters credentials on a computer.
2. **Authentication (AuthN):** AD (via a DC) Verifies the user's identity against its database (Kerberos/NTLM).
3. **Authorization (AuthZ):** AD checks permissions (from GPOs/ACLs) to see what resources (files, apps) the User' is allowed to access.
4. **Resource Access:** User accesses only permitted resources across the network.

Active Directory (AD) is an essential component for managing networked systems within many business environments. At its core, AD provides a centralized platform for organizing, managing, and securing network assets and resources, including computers, User' accounts, and other network-related assets and accesses such as file shares or print servers.

Developed by Microsoft, AD is a cornerstone of many enterprise-level Windows networks worldwide that offers a range of features that facilitate efficient administration of IT resources. This tutorial is designed for beginners, aiming to provide a fundamental understanding of Active Directory's structure and full capabilities, as well as hands-on guidance for basic tasks.

Understanding AD is crucial for anyone who aspires to work in network administration or IT support. As a directory service, it serves as a centralized database that stores information about objects within the network, such as users, groups, computers, and printers. This allows administrators to manage permissions and access to network resources effectively.

Advantages of Active Directory

One of the most significant advantages of using AD is its ability to streamline the management of a large number of resources and users all at once. Administrators can create and manage user accounts, assign and enforce security policies, and automate tedious administrative tasks such as pushing out patches, or locking down systems preventing users from accessing certain parts of the network. Additionally, ADs hierarchical structure makes it scalable, suitable for organizations of various sizes from small businesses to large corporations.

In this tutorial, we will cover the basics of Active Directory, including its key components, how to access and navigate its interface, manage users and groups, and organizes resources using Organizational Units (OUs). Whether you are new to network administration or looking to broaden your IT skills, this guide will provide you a comprehensive introduction to the world of Active Directory.

**Ethical hackers**-authorized, paid, and often contractually bound to silence-simulate real-world attacks to measure how far an intruder can pivot through your estate before you notice.

## Network Assessments

### External Penetration Test

We attack from the public Internet, mapping every IP, subdomain, and leaked credential we can find through avenues such as OSINT (Open-Source Intelligence), then Chaining vulnerabilities until we either pop a shell or hit the agreed-upon scope limit.\
**Effort:** 32-40 hours of testing + 8-16 hours of reporting and writing.

### Internal Penetration Test

**Assume Breach:** We drop a box on your LAN (or VLAN-hop from a "visitor" port) and go after Domain Admin, GPOs, file shares, and the crown-jewel databases, specifically `ntds.dit.`\
**Effort:** 32-40 hours baseline (scalable with network size) + 8-16 hours of reporting.

### Web Application Penetration Test

We treat your app like a hostile user with Burp Suite, a custom wordlist, and the OWASP Top 10 checklist. Logic flaws, JWT confusion, and forgotten API endpoints all count.\
**Floor Price:** 32-40 hours + 8-16 hours write-up.

### Wireless Network Penetration Test

**One SSID at a time:** guest, PSK, or 802.1x. We bring high-gain antennas, rogue APs, and a healthy respect for FCC rules.\
**Per-SSID:** 4-8 hours on-site +2-4 hours documentation.

### Physical & Social Engineering Penetration Test

Badge cloning, lock-picking, and a convincing "new-hire" smile. We also run phishing, vishing, smishing, and quishing campaigns that are designed to measure click-through rates, credential harvest, and SOC response time.\
Typical Campaign: 16-40 hours +4-8 hours reporting.

### Specialty Engagements

Mobile, IoT, vehicle CAN-bus, red team (weeks-to-months), purple team (continuous), and anything else that runs code and has an IP address.
