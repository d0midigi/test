---
description: From Small Business Deployment to Post-Exploitation Mayhem-And How to Stop It
---

# LLMNR Poisoning Attack & Defense Strategies

Lab Gold Card

| Role            | OS / IP                             | Function                          |
| --------------- | ----------------------------------- | --------------------------------- |
| DC01            | Windows Server 2022 - 192.168.56.10 | Root domain controller (demo.red) |
| SRV-WEB         | Windows Server 2019 - 192.168.56.20 | IIS + MSSQL (service accounts)    |
| WKSTN-01        | Windows 11 - 192.168.56.30          | Domain-joined workstation         |
| Kali            | 192.168.56.100                      | Attacker platform                 |
| Attacker-Domain | evil.red                            | External forest for trust demos   |

{% hint style="info" %}
### **Note:**

All scripts are run **inside an isolated VMware Workstation segment**; **no traffic leaves the host**.
{% endhint %}

Introduction to Active Directory

Definition

> > “Active Directory is a **distributed directory service** that **stores information about objects on a network** and makes this information **easy for administrators and users to find and use**.”

In plain English:\
AD = **phone-book** + **authentication gate** + **policy engine** for Windows-centric networks.

#### 1.2 Purpose in One Slide

* **Centralized identity** (one account, many services)
* **Scalable authentication** (Kerberos, NTLM, LDAPS)
* **Fine-grained authorization** (groups, OUs, GPOs, ACLs)
* **Single-management plane** (users, PCs, printers, DHCP, DNS, PKI, SCCM…)

#### 1.3 Small-Company Scenario (50 Users, 3 Servers)

**Pain before AD**

* Local accounts on every PC → help-desk resets **daily**.
* File-server shares use **CSV lists** → nightmare when staff leave.
* No **group policy** → USB sticks, random software, weak passwords.

**AD Solution in 2 Hours**

1. Install **AD-Domain-Services** on Windows Server → promote to DC.
2. Join PCs + servers → users log in once (SSO).
3. Create **Finance**, **HR**, **IT** OUs → link GPOs → USB blocked, 14-char password, Office auto-installed.
4. **Print server**, **DHCP**, **DNS** integrated → zero-config for clients.

**ROI**: 1 FTE help-desk saved ≈ **$60 k/year**.

***

### 2. Understanding AD Fundamentals

#### 2.1 Domain = Administrative Boundary

* **DNS namespace** (demo.red)
* **Security boundary** (password policies, trusts)
* **Replication unit** (all DCs replicate **entire domain** NC)
* **Policy container** (GPOs linked to domain root affect every object)

#### 2.2 Domain Controller (DC) – The Crown-Jewel Server

**Roles** (FSMO + Infrastructural)

| Role                  | Scope  | Loss Impact                                 |
| --------------------- | ------ | ------------------------------------------- |
| PDC Emulator          | Domain | Password changes fail, time-sync drift      |
| RID Master            | Domain | New objects fail when RID pool is exhausted |
| Infrastructure Master | Domain | Cross-domain group-to-user links stale      |
| Schema Master         | Forest | Schema updates impossible                   |
| Domain Naming Master  | Forest | New domains / trusts fail immediately       |

Extra Built-In Parts

* SYSVOL -&#x20;





bhhbhugg
