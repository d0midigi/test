# ❗ README FIRST-Chapter Outline

{% hint style="danger" %}
## Chapter 7 Crucial Missing Concepts to Consider

The following high-value concepts are strongly recommended for inclusion in this chapter to ensure complete coverage of offensive and defensive FICAM network mechanics:

* **Multicast/Broadcast Name Resolution & IPv6 DNS Takeover:** Poisoning protocols like LLMNR, NBT-NS, mDNS, and rogue DHCPv6 (`mitm6`) are fundamental vectors used to hijack identity transport on local subnets.
* **LDAP Transport Security and Relaying:** LDAP/LDAPS (`TCP 389/636`), LDAP Signing, and Channel Binding Tokens (CBT). Unenforced LDAP signing allows attackers to relay authentication directly into directory updates.
* **SMB Security Controls:** SMB Signing, SMB Encryption, and SMB over QUIC (crucial for modern remote client identity transport)
* **PIV/CAC & PKI Integration with EAP-TLS:** Direct alignment with FICAM high-assurance credential requirements (FIPS 201, NIST SP 800-78) for 802.1X network access.
{% endhint %}

{% hint style="info" %}
## Chapter 7 Technical Scope & Coverage

#### **1. Network Identity Architecture & Transport Dependencies**

* **Core Protocol Suite:** Deep dive into TCP/UDP port mapping for Kerberos (`88`), LDAP/S (`389/636`), SMB (`445`), DNS (`53`), RPC (`135`/dynamic high ports), and RADIUS (`1812/1813`).
* **Active Directory DNS & Locators:** Mechanics of AD-Integrated DNS, SRV record weighting, dynamic update security, and NTP time skew thresholds ($$ $\pm 5$ $$ minutes for Kerberos ticket validity).
* **Enterprise Network Access Control:** Implementation of IEEE 802.1X, RADIUS/NPS, and TACACS+ driving user versus machine authentication boundaries.

#### **2. Offensive Tradecraft & Protocol Exploitation**

* **Name Resolution & DHCP Takeover:** Poisoning LLMNR/NBT-NS/mDNS via Responder and executing IPv6 DNS takeover (`mitm6`) to force netNTLM authentication.
* **Authentication Relaying:** Intercepting unencrypted SMB/HTTP requests and relaying them over LDAP/LDAPS (`ntlmrelayx`) to modify schema objects or elevate domain privileges.
* **Network Access EAP Attacks:** Exploiting weak EAP suites (EAP-MD5, LEAP), rogue RADIUS access point deployment (`hostapd-mana`), and inner-tunnel MS-CHAPv2 hash extraction via `asleap`.

#### **3. Defensive Engineering & FICAM Hardening**

* **Transport Cryptography & Binding:** Enforcing mandatory LDAP Signing, Channel Binding Tokens (CBT), SMB Signing/Encryption, and IPsec Transport Mode.
* **Network Microsegmentation:** Implementing Tier 0/1/2 subnet boundaries, dynamic RPC filtering, and PAW-to-DC restricted network access control lists (ACLs).
* **EAP & NAC Hardening:** Enforcing EAP-TLS with PIV/CAC smart cards, disabling weak legacy protocols (PAP, CHAP, MS-CHAPv2, LEAP), and configuring TEAP (Tunnel Extensible Authentication Protocol) for dual-credential chain validation.

#### Key Learning Objectives

1. Analyze the network transport dynamics of Active Directory, DNS, RPC, SMB, and RADIUS authentication sequences.
2. Execute and Validate network-layer identity attacks including LLMNR/mDNS poisoning, IPv6 DNS interception, NTLM relaying, and EAP inner-tunnel cracking.
3. Configure enterprise transport protections including LDAP Signing/CBT, SMB Encryption, dynamic RPC restrictions, and EAP-TLS certificate validation.
4. Deploy Network Detection and Response (NDR) rules to identify rogue DHCP servers, NTLM relays, and unencrypted identity queries in real time.
{% endhint %}

> _These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._

This chapter dissects the networking protocols that serve as the circulatory system of Active Directory (AD) and FICAM environments. It evaluates how attackers exploit network resolution mechanisms, protocol fallbacks, and unencrypted channels to manipulate identity traffic, while providing the defensive engineering blueprints required to enforce Zero Trust Network Access (ZTNA) and transport-layer protection in alignment with NIST SP 800-207 and CISA Zero Trust Maturity Model guidelines.

#### Technical Scope & Coverage

**1. Identity Protocol Architecture & Transport Dynamics**

* Core AD Protocol Suite: Network flow analysis of DNS resolution, Kerberos authentication (`TCP/UDP 88`), LDAP/LDAPS (`TCP 389/636/3268/3269`), SMB (`TCP 445`), and dynamic RPC ranges (`TCP 135` / dynamic High Ports) across local subnets and domain boundaries.
* Name Resolution Mechanics: Operation of Active Directory Domain Name System (AD DS), Global Catalog locator processes, and legacy fallback broadcast protocols (LLMNR, NBT-NS, mDNS).
* Hybrid & Federated Network Boundaries: Network transport architectures connecting legacy on-premises AD Domain Controllers to Cloud Access Security Brokers (CASB), FICAM SAML/OIDC identity providers (IdPs), and Active Directory Federation Services (ADFS) proxy infrastructure.

**2. Offensive Tradecraft & Network-Level Exploitation**

* Broadcast & Name Resolution Poisoning: Man-in-the-Middle (MitM) positioning via LLMNR/NBT-NS poisoning, mDNS spoofing, and rogue IPv6 DHCP address assignment (`mitm6`) to capture netNTLM challenge-response hashes.
* Protocol Relaying & Cross-Protocol Exploitation: Relaying captured authentication requests across SMB, HTTP, and LDAP/S using tools like `ntlmrelayx`; abusing missing LDAP Signing and Channel Binding Tokens (CBT) to modify directory objects or grant privileges over the wire.
* Network Traversal & Identity Pivoting: Exploiting unconstrained Kerberos delegation over open RPC/SMB network paths to route attacks across network zones and breach air-gapped or segmented administrative subnets.
* Reconnaissance & Traffic Analysis: Passive network sniffing for unencrypted LDAP traffic containing cleartext credentials or sensitive directory queries, and leveraging bloodhound/network mapping tools over permissive firewall policies.

**3. Defensive Engineering & FICAM Network Hardening**

* **Network Microsegmentation & Tier 0 Isolation:** Designing strict network access control lists (ACLs), host-based firewall rules, and microsegmentation boundaries that restrict DC access exclusively to authorized ports and administrative endpoints (PAWs).
* **Transport Cryptography & Binding Enforcements:** Enforcing mandatory LDAP Signing and Channel Binding (CBT), disabling NTLM transport in favor of Kerberos, implementing SMB Signing / SMB Encryption, and evaluating SMB over QUIC for modern remote clients.
* **Protocol Elimination & Network Hardening:** Systematically disabling LLMNR, NBT-NS, and IPv6 (where unused or unmanaged) via Group Policy; enforcing IPsec Transport Mode for secure DC-to-DC and DC-to-Member Server communication.
* **NDR & Telemetry Engineering:** Configuring Network Detection and Response (NDR) sensors and SIEM pipelines to detect anomalous DNS requests, rogue DHCPv6 solicitations, unexpected cross-subnet RPC/SMB traffic, and network-level NTLM relay signatures.

#### Key Learning Objectives

By completing this chapter, readers will be able to:

1. Map and Analyze every network protocol involved in an Active Directory authentication lifecycle and identify exposed network transport vectors.
2. Execute and Validate offensive network attacks, including IPv6 DNS takeover, LLMNR/NBT-NS poisoning, and SMB-to-LDAP authentication relaying.
3. Design and Implement network-level microsegmentation, IPsec policies, and mandatory cryptographic transport rules (LDAP Signing/CBT) that prevent wire-level identity compromise.
4. Deploy network detection rules to identify protocol relaying, rogue name resolution responses, and unauthorized cross-tier identity traffic in real time.
