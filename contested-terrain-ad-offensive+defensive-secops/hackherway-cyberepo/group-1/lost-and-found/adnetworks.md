# ADNetworks

## Chapter 3: Computer Networking Concepts and Fundamentals for Active Directory Security

### Abstract

The digital world we inhabit is fundamentally built up on the principles of computing networks and their underlying protocols of which all network communications rely upon to function correctly. As cybersecurity professionals and ethical hackers — especially those working around Active Directory (AD) — a deep, visceral understanding of this fundamental layer is essential. Without it, every security engagement or penetration test will be impaired. Networks are the central nervous system of the modern enterprise, and Active Directory is often the brain that controls the operations of the entire body.

This chapter explores computer networking fundamentals specifically tailored for ethical hackers and defenders working with Active Directory domain environments: OSI and TCP/IP models, IP addressing and subnetting, ports and protocols, essential network services (DNS, DHCP, ARP, NAT), AD architecture and key protocols (Kerberos, LDAP, SMB, DNS), AD-specific ports, attack vectors against AD, advanced AD security concepts, traffic analysis, and hardening best practices. Practical examples, tips, and security warnings are included to help you identify vulnerabilities and implement defensive measures in enterprise Windows environments.

***

### Learning Objectives

By the end of this chapter, you will be able to:

1. Explain the OSI and TCP/IP models and their relevance to network security
2. Configure and calculate IP addresses, subnet masks, and CIDR notation
3. Identify and explain the purpose of common ports and protocols used in enterprise networks
4. Understand the architecture and components of Active Directory infrastructure
5. Recognize critical Active Directory services and their associated ports and protocols
6. Analyze network traffic to identify normal and malicious Active Directory activity
7. Describe common attack vectors against Active Directory environments
8. Implement security best practices for hardening network services and Active Directory
9. Apply network segmentation and access control principles to secure Active Directory
10. Utilize packet sniffers and analysis tools to investigate Active Directory security incidents

***

## Introduction to the Architecture of Interconnection: Computer Networks and Active Directory

#### Defining Networks in Active Directory Domain Environments

A computer network is a collection of interconnected devices (nodes) that communicate, exchange data, and share resources using established protocols and standards. In AD contexts, networks are more than connectivity: they're the web of trust relationships, authentication mechanisms, authorization frameworks, and data flows that enable users to access resources. AD is inherently network-based and relies on connectivity, name resolution, and inter-service communications. Without networking knowledge, you cannot effectively assess, exploit, or defend AD.

#### Fundamental Purpose of a Computer Network

Networks enable resource sharing and communication. LANs (Local Area Networks) are high-speed, low-latency networks within limited areas (offices, campuses) and typically host domain controllers. WANs (Wide Area Networks) connect geographically dispersed sites. VLANs, MANs, SD-WAN, and other technologies extend or segment networks to meet scale and security needs. For AD security, the LAN is usually the primary operational environment, and gaining internal access to a LAN places an attacker close to AD infrastructure.

TIP: Start AD penetration tests by understanding network architecture. Request or build network diagrams to find domain controllers, segments, and security boundaries. Tools: Nmap, traceroute, passive monitoring.

WARNING: Only perform network scanning, packet capture, or reconnaissance on networks you own or have explicit written permission to test.

DID YOU KNOW? Packet switching concepts were developed independently in the 1960s by Paul Baran and Donald Davies — foundational to TCP/IP.

***

### Network Technologies

Below are common network types and components relevant to AD environments.

#### Local Area Network (LAN)

A LAN connects devices within a limited geographic area (office, campus). Technologies: Ethernet (wired), Wi-Fi (wireless). Key components:

* Router: connects LAN to external networks (internet)
* Switches: connect multiple devices within a LAN and forward frames by MAC address
* Endpoints: computers, servers, printers, etc.
* Network Interface Card (NIC): hardware enabling network access

Wired LANs use Ethernet cabling; WLANs use radio (Wi-Fi).

#### Wide Area Network (WAN)

WANs connect LANs across cities, countries, and continents. Common technologies: leased lines, VPNs, MPLS, SD-WAN, broadband/cellular. WANs matter for AD replication and remote site authentication and have higher latency and traverse untrusted networks when using the public internet.

#### Campus Area Network (CAN)

High-speed private networks connecting multiple LANs within a campus or business park (e.g., university campus).

#### Virtual Local Area Network (VLAN)

Logical grouping of devices into isolated broadcast domains on the same physical switch infrastructure. VLANs enable segmentation and reduce broadcast traffic but are not a full security boundary by themselves.

Figure: Diagram of a Virtual Local Area Network (VLAN) (image retained)

#### Wireless Local Area Network (WLAN)

Wireless networks (Wi‑Fi) connect devices without cables using access points. Wireless signals propagate beyond physical walls, making them intrinsically more exposed than wired networks.

Figure: Diagram of a Wireless Local Area Network (WLAN)

#### Software-Defined Wide Area Network (SD-WAN)

SD‑WAN abstracts WAN control into software, enabling centralized policy, multi-transport routing (MPLS, broadband, LTE), and dynamic path selection for cloud-first architectures.

Figure: Diagram of a Software-Defined Wide Area Network (SD-WAN)

#### Bluetooth / Body Area Network (BAN)

BANs are very short-range low-power networks (wearables, sensors). Bluetooth Low Energy (BLE) is common; these devices are typically heavily constrained and can present attack vectors if joined to enterprise networks.

Physical topologies (star, mesh) and logical architectures (protocol stacks) both affect functionality and security.

***

### OSI Model: Your Networking Foundation

The OSI model is a conceptual 7-layer model to think about networking and troubleshooting. It's useful for mapping attacks and defenses to specific layers.

{% stepper %}
{% step %}
### Layer 1 — Physical Layer

Deals with physical transmission (cables, connectors, NICs, radio waves). Attacks: wiretaps, rogue devices via unused jacks, cable cutting, RF interference. Mitigations: physical security (locked rooms), 802.1X NAC, monitored ports.
{% endstep %}

{% step %}
### Layer 2 — Data Link Layer

Responsible for node-to-node transfer and MAC addressing (Ethernet, Wi‑Fi). Key concepts: MAC addresses, switches, ARP, VLANs.

Attacks: MAC spoofing, MAC flooding, ARP poisoning (man-in-the-middle). Tools: arpspoof, bettercap, Responder. Mitigations: port security, DHCP snooping, dynamic ARP inspection, VLAN hardening.
{% endstep %}

{% step %}
### Layer 3 — Network Layer

Routing and IP (IPv4/IPv6), ICMP, fragmentation. Attacks: IP spoofing, routing manipulation (BGP hijack), fragmentation evasion. Mitigations: anti-spoofing filters (BCP38), secure routing practices, monitoring.
{% endstep %}

{% step %}
### Layer 4 — Transport Layer

TCP/UDP; ports and connection semantics (three-way handshake, SYN floods). Attacks: SYN floods, session hijacking, TCP RST injection, UDP amplification. Defenses: SYN cookies, stateful firewalls, rate limiting.
{% endstep %}

{% step %}
### Layer 5 — Session Layer

Manages sessions; in practice, many functions are in higher/lower layers. Relevant to Kerberos sessions and RPC session state. Attacks: session hijacking, session fixation. Monitoring of session behavior is important.
{% endstep %}

{% step %}
### Layer 6 — Presentation Layer

Data representation, encryption, compression. SSL/TLS operates here. Attacks: SSL stripping, certificate validation bypass, compression-related attacks (CRIME). Ensure correct TLS configurations and certificate validations.
{% endstep %}

{% step %}
### Layer 7 — Application Layer

Top-level protocols (HTTP, DNS, LDAP, SMB, Kerberos). Most application attacks (LDAP injection, Kerberoasting, Golden Ticket) occur here. Deep knowledge of application protocols is required for both offense and defense.
{% endstep %}
{% endstepper %}

WARNING: OSI is conceptual. Real protocols may span layers (e.g., TLS sits between transport and application).

DID YOU KNOW? The OSI model was created by ISO in 1984. Although TCP/IP is the dominant practical stack, OSI remains an excellent teaching aid.

***

### 3.3 The TCP/IP Model: Real-World Networking

The TCP/IP model is the practical four-layer model used in real networks: Network Access (Link), Internet, Transport, and Application. It maps to OSI functions and is useful for real-world troubleshooting.

* Network Access: Ethernet, Wi‑Fi — physical + data link functions. Useful place to start troubleshooting and packet captures.
* Internet: IP (IPv4/IPv6), routing, ICMP, ARP boundary functions.
* Transport: TCP/UDP; port numbers; stateful vs stateless semantics.
* Application: All high-level protocols (Kerberos, LDAP, SMB, DNS, HTTP).

TIP: For Active Directory troubleshooting and security, thinking in TCP/IP layers (Network Access → IP → TCP/UDP → AD protocols) is practical.

***

## 4. IP Addressing and Subnetting

### 4.1 IPv4 Addressing Fundamentals

IPv4 addresses are 32-bit numbers presented in dotted-decimal (e.g., 192.168.1.100). They identify both the network and host portions to enable hierarchical routing.

Classful ranges (historical):

* Class A: 0.0.0.0–127.255.255.255 (10.0.0.0/8 private)
* Class B: 128.0.0.0–191.255.255.255 (172.16.0.0–172.31.255.255 private)
* Class C: 192.0.0.0–223.255.255.255 (192.168.0.0/16 private)
* Class D: 224.0.0.0–239.255.255.255 (multicast)
* Class E: 240.0.0.0–255.255.255.255 (experimental)

Special addresses:

* 127.0.0.0/8 — loopback (127.0.0.1)
* 0.0.0.0 — unspecified / default route context-dependent
* 255.255.255.255 — limited broadcast
* 169.254.0.0/16 — APIPA / link-local (assigned when DHCP fails)

In AD contexts, domain controllers should have stable IPs (static or DHCP reservations); misconfigured IPs/DNS cause authentication and service issues.

DID YOU KNOW? IPv4 address exhaustion drove RFC 1918 private addressing and the long-term adoption of NAT.

TIP: Keep accurate IP Address Management (IPAM) records for AD infrastructure (DCs, DNS, DHCP, gateways).

***

### 4.2 Subnet Masks and CIDR Notation

Subnet masks divide network and host bits. CIDR notation (e.g., /24) gives the number of network bits.

Common masks:

* /8 (255.0.0.0) — \~16.7M hosts
* /16 (255.255.0.0) — \~65k hosts
* /24 (255.255.255.0) — 254 usable hosts
* /25.. /30 etc. for finer allocations

Subnetting example (10.100.0.0/16 allocated across multiple subnets) demonstrates efficient use (use /23 for \~500 hosts, /25 for \~100 hosts, etc.). Subnets map to AD site design and affect which DCs clients use.

VLSM (Variable Length Subnet Masking) allows mixed subnet sizes within networks.

WARNING: Miscalculating subnets causes connectivity issues. Document scopes, DHCP pools, reserved addresses, and infrastructure assignments.

TIP: Plan for growth — allocate slightly larger subnets than immediate needs to avoid renumbering later.

***

### 4.3 Private vs. Public IP Addresses

Public IPs are globally routable, allocated by RIRs. Private IPs (RFC 1918): 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 — not routable on the internet and used internally with NAT for internet access.

In Active Directory environments, internal infrastructure (DCs, member servers) uses private addresses. NAT provides a degree of topology hiding, but once attackers have internal access, private addressing offers no protection.

Special ranges: loopback (127/8), APIPA (169.254/16), multicast (224/4), reserved (240/4).

DID YOU KNOW? RFC 1918 private addressing was published in 1996 to mitigate IPv4 scarcity.

TIP: Document address ranges and purposes, including reserved ranges and infrastructure addresses.

***

### 4.4 IPv6: The Future of Addressing

IPv6 uses 128-bit addresses (hexadecimal groups separated by colons). Key address types:

* Global Unicast (2000::/3) — public, routable
* Link-Local (fe80::/10) — auto-configured, local-only
* Unique Local Addresses (ULA fc00::/7, typically fd00::/8) — private equivalents
* Multicast (ff00::/8) — replaces broadcast
* Anycast — same address on multiple nodes, routed to nearest

Features: SLAAC (autoconfiguration), large address space, streamlined headers, optional IPsec, elimination of NAT as a necessity (though some deployments use NAT66).

Security notes: Windows prefers IPv6 when available. IPv6 is often overlooked in environments that "don't use IPv6" — endpoints may still have IPv6 enabled by default, creating attack surface. Mitigate by properly securing or disabling IPv6 where appropriate.

TIP: During AD assessments, check IPv6 configuration (ipconfig /all or Get-NetIPAddress), DNS AAAA records, and IPv6 support in monitoring tools.

WARNING: Don't neglect IPv6 — attackers can exploit misconfigured IPv6 while defenses focus on IPv4.

***

## 5. Ports and Protocols: The Language of Networks

### 5.1 Understanding Ports

Ports (0–65535) identify services on hosts. Combine an IP address and port to form a socket. IANA port ranges:

* Well-known: 0–1023 (standard services, require admin privilege)
* Registered: 1024–49151 (vendor/app assigned)
* Dynamic/Private (ephemeral): 49152–65535 (client source ports)

Remember to specify protocol (TCP/UDP) when documenting ports (e.g., TCP/443 vs UDP/53).

Port scanning is primary reconnaissance for service discovery. Common scan types: TCP Connect, SYN (half-open), FIN/NULL/XMAS, and UDP (slow and noisy).

TIP: For AD engagements, initially scan targeted AD ports (88, 389, 636, 445, 3268, 3269) instead of full-range scans to minimize noise and disruption. Coordinate with defenders.

WARNING: Port scanning without authorization is illegal.

DID YOU KNOW? Considering both TCP and UDP doubles the effective port space — 65,536 TCP + 65,536 UDP.

***

### 5.2 TCP vs. UDP: Connection-Oriented vs. Connectionless

TCP: connection-oriented, reliable (three-way handshake, sequence numbers, retransmission, ordered delivery, flow & congestion control). Attacks: SYN flood, session hijacking, RST injection.

UDP: connectionless, unreliable, low-latency (no handshake), suited for real-time applications. Attacks: UDP flooding, amplification. Some protocols using UDP are DNS, certain Kerberos/initial exchanges, SNMP, DHCP.

In AD:

* Kerberos uses UDP and TCP on port 88 (prefers UDP for small requests, falls back to TCP for large responses).
* DNS uses UDP 53 for queries, TCP 53 for zone transfers/large responses.
* LDAP uses TCP 389 (reliable).
* SMB uses TCP 445.

TIP: Scan both TCP and UDP for relevant services, but target known UDP services rather than exhaustive UDP scans.

WARNING: Security tools often focus on TCP; UDP can be abused for C2 or tunneling (e.g., DNS over UDP).

***

### 5.3 Common Ports Every Ethical Hacker Must Know

Key ports and security notes (selected):

* FTP — 20/21 TCP (plaintext credentials)
* SSH/SFTP — 22 TCP (secure remote access; check keys and weak passwords)
* Telnet — 23 TCP (plaintext; obsolete)
* SMTP — 25 TCP (mail relay; check open-relay)
* DNS — 53 TCP/UDP (critical for AD; monitor for zone transfer, tunneling)
* DHCP — 67/68 UDP (rogue DHCP attacks)
* TFTP — 69 UDP (no auth; used for device configs)
* HTTP — 80 TCP (plaintext)
* HTTPS — 443 TCP (TLS)
* NTP — 123 UDP (time sync; critical for Kerberos)
* SNMP — 161/162 UDP (default community strings are common risk)
* Kerberos — 88 TCP/UDP (primary AD auth)
* LDAP — 389 TCP/UDP (plaintext binds risk)
* LDAPS — 636 TCP (LDAP over TLS)
* SMB — 445 TCP (file sharing; frequent attack vector)
* NetBIOS — 137/138/139 (legacy name services; poisoning)
* RPC Endpoint Mapper — 135 TCP (RPC dynamic ports)
* Global Catalog — 3268/3269 TCP (forest-wide queries)
* RDP — 3389 TCP (brute-force target)
* WinRM — 5985/5986 TCP (PowerShell remoting)
* MSSQL — 1433 TCP (databases)
* MySQL — 3306 TCP

A consolidated reference table is useful to keep at hand during engagements.

TIP: Create a custom cheat-sheet for the environments you test that maps ports to likely service versions, default credentials, and enumeration techniques.

WARNING: Port numbers alone do not guarantee what service runs there — always fingerprint services (banners, version probes).

***

## 6. Essential Network Services

### 6.1 DNS: The Internet's Phone Book

DNS translates names to addresses and is deeply integrated with Active Directory. AD relies on DNS SRV records to locate domain controllers and services.

Important record types for AD:

* A — IPv4 address
* AAAA — IPv6 address
* SRV — service location (critical for DC discovery, e.g., \_ldap.\_tcp.dc.\_msdcs.domain)
* PTR — reverse lookup
* NS — authoritative name servers
* SOA — zone authority and timing parameters
* TXT — arbitrary text (SPF, DKIM, other metadata)

DNS resolution flow: client cache → recursive resolver → cache/recursive resolution (root → TLD → authoritative). In AD, DCs register A, SRV, and related records; clients query SRV to find DCs.

AD-integrated DNS benefits: dynamic updates, AD replication of DNS data, secure dynamic updates.

DNS attacks and concerns for AD:

* Cache Poisoning (DNS spoofing) — mitigated by DNSSEC (not widely deployed)
* DNS Hijacking — control of authoritative records leads to wide redirections
* DNS Tunneling — covert channels for C2 or exfiltration
* DNS Amplification — DDoS amplification vectors
* WPAD abuse — proxy auto-discovery attacks to intercept web traffic
* DNSAdmins privilege abuse — special AD privilege allowing dangerous operations (DLL loading into DNS service on DCs can yield SYSTEM rights)

TIP: When troubleshooting AD, always verify DNS: SRV records for DCs, forward and reverse lookups, and correct registration (Resolve-DnsName or nslookup).

DID YOU KNOW? Root servers are represented by 13 named addresses (a.root-servers.net…m.root-servers.net) but are globally distributed via anycast.

***

### 6.2 DHCP: Automatic IP Configuration

DHCP automates IP assignment and network configuration. The DORA exchange: Discover → Offer → Request → Acknowledge.

Common DHCP options: subnet mask, gateway (router), DNS servers, domain name, lease time, NTP servers, TFTP/boot options (PXE).

Security risks:

* Rogue DHCP servers can hand out malicious DNS, gateway, or short lease times, enabling man-in-the-middle or interception of authentication traffic.
* DHCP starvation attacks exhaust address pools.
* DHCP snooping (switch feature) helps mitigate rogue servers by marking trusted ports and building bindings used by Dynamic ARP Inspection and IP Source Guard.

In AD environments, DHCP servers should be authorized in AD to prevent rogue DHCP servers. DHCP ⇄ DNS integration can dynamically register client A/PTR records; ensure secure dynamic updates.

TIP: When testing, rogue DHCP servers can be effective for credential capture, but highly disruptive — use only with authorization and coordination.

DID YOU KNOW? DHCP evolved from BOOTP; BOOTP required static mapping files.

***

### 6.3 ARP: Bridging Layer 2 and Layer 3

ARP maps IPv4 addresses to MAC addresses on local LAN segments. Process: ARP request (broadcast) → ARP reply (unicast) → ARP cache entry.

Gratuitous ARP updates help detect IP conflicts and update caches.

ARP attacks:

* ARP Poisoning / ARP Spoofing — attacker sends forged ARP replies to associate attacker MAC with gateway or other hosts → man-in-the-middle (MITM) position. Tools: arpspoof, ettercap, bettercap. Combined with Responder to capture credentials (LLMNR/NBT-NS poisoning), this is a common internal attack technique. Ensure IP forwarding is enabled on attacker to avoid immediate outage if performing tests.

Mitigations:

* Dynamic ARP Inspection (switch feature) with DHCP snooping binding table
* Static ARP for critical hosts (not scalable)
* Encryption at higher layers (TLS, IPsec) reduces impact of MITM on confidentiality
* Network segmentation reduces ARP attack scope

TIP: ARP scanning (e.g., arp-scan or nmap -PR) is effective for local host discovery even when ICMP is blocked.

DID YOU KNOW? ARP has no built-in authentication — historically difficult to retrofit with security; enterprise switches now offer DAI to mitigate spoofing.

WARNING: ARP poisoning can cause outages — only perform with authorization and caution.

***

### 6.4 NAT and PAT: Address Translation

NAT rewrites IP addresses at network boundaries to enable private addressing internally while communicating on the public internet. Types:

* Static NAT — one-to-one mapping (public ↔ private) for servers requiring inbound access
* Dynamic NAT — pool mapping for outbound connections
* Port Address Translation (PAT) / NAT overload — many internal hosts share one public IP via unique source ports (common in enterprise edge routers)

Security implications:

* NAT provides topology hiding and blocks unsolicited inbound traffic by default (a basic security benefit) but is not a substitute for stateful firewalls.
* Protocols embedding IP addresses in payloads can break under NAT (FTP, SIP) and require ALGs (can be buggy).
* Logging and attribution are harder: public IP is shared, so correlating external events to internal hosts requires NAT logs + DHCP logs.
* NAT devices maintain state — can be resource-exhausted (DoS) by attackers.

AD considerations: AD typically runs inside private addressing; NAT is normally not present between DCs and clients. Avoid NAT between AD nodes; site-to-site VPNs should route (not NAT) internal addresses. Remote access for admins should use VPNs and reverse proxies rather than port-forwarding DCs.

DID YOU KNOW? NAT was conceived as a temporary solution to IPv4 exhaustion in 1994 and became a long-term fixture in networking.

TIP: Document NAT rules and port forwards (public ↔ private mappings) for incident response. Never rely on NAT as the primary security control.

WARNING: UPnP-enabled NAT allows internal hosts (and malware) to open inbound ports — disable UPnP at the perimeter unless explicitly required and controlled.

***

## 7. Introduction to Active Directory

### 7.1 What is Active Directory?

Active Directory (AD) is Microsoft’s directory service for Windows domains. It is a database, authentication system, authorization framework, management platform, and identity infrastructure. Key capabilities:

* Hierarchical organization: domains, trees, forests
* Multi-master replication across domain controllers (DCs)
* Uses LDAP for directory access, Kerberos for authentication, and DNS for service location
* Integrated DNS and Group Policy (GPO) for centralized management
* Extensible schema for application integration (e.g., Exchange)

Security impact: AD is a high-value target. Compromise of Domain Admin or Enterprise Admin yields broad control over the Windows environment. Defenses focus on least privilege, monitoring, tiered administration, and protecting DCs and backups.

DID YOU KNOW? The AD database file (ntds.dit) uses the Extensible Storage Engine (ESE) and contains password hashes for all accounts — making backups and the backup process a high-value target for attackers.

TIP: First reconnaissance goal: map domain structure, domain names, DC locations, trusts. Tools: nltest, Get-ADDomain/Get-ADForest/Get-ADTrust (PowerShell), BloodHound, PowerView.

WARNING: Attacking DCs is dangerous — they are critical infrastructure. Avoid actions that cause outages.

***

### 7.2 Domain Controllers and Domain Services

Domain Controllers (DCs) host Active Directory Domain Services (AD DS). Key properties:

* DCs store a full writable replica of the domain database (ntds.dit).
* AD replication is multi-master; certain FSMO roles are single-master for specific operations.

FSMO (Flexible Single Master Operations) roles:

Forest-wide (one per forest):

* Schema Master — only DC that can modify the schema
* Domain Naming Master — responsible for adding/removing domains in the forest

Domain-wide (one per domain):

* RID Master — allocates pools of RIDs (for SIDs) to DCs
* PDC Emulator — critical for time sync, password change prioritization, and legacy compatibility
* Infrastructure Master — updates cross-domain references (avoid placing on GC unless all DCs are GCs)

RODC (Read-Only Domain Controller): for insecure locations; read-only DB, credential caching controlled by policy, unidirectional replication to avoid DC changes replicating up.

Virtual DCs: watch out for snapshot/restore issues (VM-Generation ID mitigates older snapshot pitfalls); ensure host security.

Backups: use System State backups. Beware of tombstone lifetime for deletes and authoritative restore procedures. Backups (and backup infrastructure) should be tightly secured.

TIP: Use at least two DCs per domain, distribute DCs across sites/datacenters for redundancy, and avoid concentrating all FSMO roles on one DC.

WARNING: Compromising DC backups (ntds.dit) provides offline access to all domain password hashes — protect backups vigorously (encryption, access control, offline storage).

***

### 7.3 Active Directory Objects: Users, Groups, and Computers

Objects in AD:

* User objects — attributes: samAccountName, userPrincipalName, distinguishedName, objectSid, objectGUID, displayName, mail, memberOf, pwdLastSet, lastLogon/lastLogonTimestamp, badPwdCount, userAccountControl flags (disable, password never expires, smartcard required, DONT\_REQ\_PREAUTH, etc.), servicePrincipalName (SPN), adminCount (indicates protected admin membership)
  * SPNs are key Kerberos targets (Kerberoasting)
  * adminCount = 1 marks accounts that were or are privileged (AdminSDHolder protections)
* Groups — types: Security vs Distribution; scopes: Domain Local, Global, Universal
  * Best practice AGDLP / AGUDLP for scalable delegation and permissions
  * Built-in privileged groups: Enterprise Admins, Schema Admins, Domain Admins, Administrators, Account Operators, Backup Operators, DNSAdmins (dangerous when DNS runs on DCs), Group Policy Creator Owners
* Computer objects — represent hosts, have SIDs, dNSHostName, OS attributes, servicePrincipalName for services. Computer accounts have machine passwords (auto-rotated every 30 days) and can be abused for pass-the-hash or Silver Ticket attacks.
* Service accounts — run services, often long-lived passwords, can have SPNs (Kerberoasting risk). Use gMSA where possible; enforce least privilege and strong passwords.

DID YOU KNOW? The built-in Administrator account has RID 500 and special properties (cannot be locked out in the same way) — it's a frequent attacker target.

TIP: During recon, enumerate privileged group membership, SPNs, adminCount flags, and nested groups. Tools: PowerView, bloodhound, Get-AD\* PowerShell cmdlets.

***

### 7.4 Organizational Units and Group Policy

OUs organize objects and are the primary containers for delegation and Group Policy (GPO) linkage.

Design principles:

* Keep OUs simple and driven by management and policy needs (delegation and GPO application), not purely HR org charts.
* Separate user and computer OUs for policy clarity.
* Use OU design to support tiered administrative models (Tier 0: DCs/admin infra; Tier 1: servers; Tier 2: endpoints).

GPOs contain Computer Configuration and User Configuration sections, processed in order: Local → Site → Domain → OU (LSDOU). Features affecting policy precedence:

* Enforced (No Override)
* Block Inheritance
* Security Filtering (limit which principals a GPO applies to)
* WMI Filtering (conditional GPO application)
* Loopback processing (for kiosk/shared machines)

Security-relevant settings include password policies, account lockout, user rights assignments, audit policy, Windows Firewall, AppLocker, and administrative templates.

Attack vectors involving GPOs:

* GPO modification can deploy malware, scheduled tasks, or configuration changes across many systems
* Legacy Group Policy Preferences (GPP) stored credentials encrypted with a known key — still present in many environments (search SYSVOL for xml files with cpassword)
* Unrestricted GPO change permissions are a serious privilege escalation/persistence risk

TIP: Audit who can modify GPOs, restrict GPO creation/editing, monitor SYSVOL for unauthorized changes, and search for legacy GPP cpassword instances.

***

## 8. Active Directory Network Architecture

### 8.1 Active Directory Ports and Protocols

Active Directory relies on many ports and protocols — blocking or misconfiguring any of them can break directory functionality. Below are the core AD ports and their purposes and security notes.

#### Core Authentication and Directory Services (summary)

* Kerberos: TCP/UDP 88 — AD primary authentication (AS-REQ/AS-REP, TGS-REQ/TGS-REP)
* LDAP: TCP/UDP 389 — Directory queries/modifications; plaintext if not using TLS
* LDAPS: TCP 636 — LDAP over TLS (encrypted)
* Global Catalog LDAP: TCP 3268 (unencrypted) / 3269 (LDAPS) — forest-wide searches
* Kerberos password change: TCP/UDP 464 — password change operations

#### File Sharing and Replication

* SMB / Microsoft-DS: TCP 445 — file shares, SYSVOL, named pipes, many Windows services. Extremely attacked; must not be exposed to the internet. Ensure proper segmentation and SMB signing/encryption where necessary.

(End of converted content for the provided excerpt)

***

Notes about the conversion:

* All original URLs and image references were preserved exactly.
* Navigation elements and redundant table-of-contents blocks were removed.
* Long sequential numbered instructional processes were preserved with stepper blocks for conceptual layering (OSI) to improve readability in GitBook.
* No external content was added; all text and technical details are from the original content you provided.
* If you want, I can:
  * Convert remaining sections (full chapter continues beyond SMB) into the same GitBook-optimized markdown structure.
  * Create tabs for transport-specific commands or package-manager blocks if you have code snippets to format.
  * Turn any FAQ sections into expandable details (collapsible) blocks if you provide them.
