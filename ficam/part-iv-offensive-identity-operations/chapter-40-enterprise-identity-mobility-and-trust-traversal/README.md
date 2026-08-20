---
icon: waze
---

# Chapter 40 - Enterprise Identity Mobility and Trust Traversal

### Abstract

Active Directory trust relationships and federated identity topologies form the structural web that enables identity mobility across complex enterprise enclaves, subsidiary environments, and multi-tenant cloud ecosystems. In federal, defense, and multinational environments operating under Federal Identity, Credential, and Access Management (FICAM) frameworks and NIST SP 800-207 Zero Trust Architecture, establishing secure trust boundaries is critical to preventing lateral movement between isolated networks. However, legacy trust configurations, mismanaged SID Filtering rules, weak cross-forest Kerberos referrals, and permissive hybrid B2B federation settings often turn administrative boundaries into simple traversal vectors.

This chapter presents an in-depth analysis of trust architecture, cross-domain privilege escalation, and cross-tenant identity traversal. It examines inter-realm Kerberos referral mechanics, SID History injection attacks, Selective Authentication bypasses, and trust key extraction. Furthermore, it expands into cloud and hybrid domains by covering Entra ID Cross-Tenant Access Policies (CTAP), B2B trust exploitation, and AD FS federation abuse. By providing concrete defensive controls—including SID Filtering enforcement, Trust Key rotation, Quarantine Mode configuration, and continuous cross-forest telemetry monitoring—this chapter enables security engineers to harden trust boundaries across enterprise identity ecosystems.

##

### 40.1 SMB

### 40.2 WinRM

### 40.3 WMI

### 40.4 DCOM

### 40.5 RDP

### 40.6 PsExec

### 40.7 Remote PowerShell

### 40.8 Scheduled Tasks

### 40.9 Services

### 40.10 Administrative Shares

### 40.11 Cross-Domain Traversal

### 40.12 Cross-Forest Traversal

### 40.13 Cross-Enclave Traversal

### 40.14 Mission-Partner Traversal

### 40.15 Federation-Assisted Mobility
