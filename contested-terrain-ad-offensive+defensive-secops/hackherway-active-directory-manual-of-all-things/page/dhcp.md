# DHCP

DHCP (Dynamic Host Configuration Protocol)

Introduction

Dynamic Host Configuration Protocol (DHCP) is a network management protocol used to automate the process of configuring devices on IP networks, allowing them to use network services such as DNS, NTP (Network Time Protocol), and any communications protocols based on UDP (User Datagram Protocol) or TCP (Transmission Control Protocol). DHCP enables devices to request IP addresses and other network parameters automatically, reducing the need for a network administrator to configure these settings manually.

How DHCP Works

DHCP operates on a client-server model where the server dynamically assigns IP addresses and other network configurations to clients. The process involves four main steps:

1. **DHCP Discover:** The client broadcasts a DHCP Discover packet to find available DHCP servers.
2. **DHCP Offer:** DHCP servers on the network respond with a DHCP Offer packet containing an IP address and other network configuration details.
3. **DHCP Request:** The client selects an offer and responds with a DHCP Request packet, indicating the chosen server.
4. **DHCP Acknowledge:** The selected DHCP server sends a DHCP Acknowledge packet to confirm the IP address lease and provide the network configuration.

Components of DHCP

* **DHCP Server:** A server that holds the network configuration parameters and leases out IP address dynamically to clients.
* **DHCP Client:** A device that requests an IP address and network configuration from a DHCP server.
* **IP Lease:** A temporary IP address assigned to a client by the DHCP server. It has a lease time, after which it must be renewed.

DHCP Options

DHCP allows additional configuration parameters, known as _Options_, to be delivered to clients. Some common DHCP options include:

* **Subnet Mask**

A subnet mask is a 32-bit binary number that splits an IP address into a network address and a host address. The network portion of the IP address ensures that data packets reach the correct network, while the host portion identifies a specific device on that network.

* **Default Gateway**

A default gateway is a piece of hardware or software that acts as a router to connect a device to a remote network segment when the device doesn’t know where the destination is. It’s the first path that information takes between systems and the exit point for all packets in a network that are destined for outside the network.

* **DNS Server**

A Domain Name System (DNS) server translates domain names and URLs into IP addresses that computers can use to find webpages. This process is called _DNS resolution._

* **Domain Name**

A domain name is a unique address that identifies and allows users to access a specific website on the internet. It’s also known as a URL, or Uniform Resource Locator. Domain names are made up of a name and a _top-level domain (TLD)_, such as “.com” or “.net,” and are separated by dots, or periods. For example, “google.com” is the domain name for Google.

* **Lease Time**

Lease time is the amount of time a device can use an IP address before it needs to be renewed or replaced. It’s a setting that network managers configure when devices get IP addresses from a DHCP server. When a DHCP server sends an IP address to a device, it also sends a lease time. Once the lease expires, the DHCP server reclaims the IP address, and it can be reassigned to another device.

Security Considerations

While DHCP simplifies network management, it also introduces many security challenges, such as:

* **DHCP Spoofing**

You can set up a rogue DHCP server to provide incorrect, or spoofed IP addresses, default gateways, or DNS servers, leading to man-in-the-middle (MiTM) attacks.

* **DHCP Starvation**

You can exhaust pools of available IP addresses by repeatedly requesting IP addresses, causing a denial of service (DoS) for legitimate users.

Ethical Hacking Techniques

You can employ various techniques to test the securities of DHCP implementations, including:

* **DHCP Starvation Attack**

Simulate a DHCP starvation attack to ensure the network you are testing can handle address exhaustion attacks.

* **Rogue DHCP Server Detection**

Deploy tools to identify unauthorized DHCP servers on the network.

* **Monitoring and Logging**

Ensure DHCP server logs are reviewed regularly to detect any suspicious activities.

Mitigation Strategies

To secure DHCP services, consider the following strategies and best practices:

* Implement network access controls to limit who can access the network.
* Use DHCP snooping on switches to filter out unauthorized DHCP messages.
* Regularly update and patch DHCP servers to protect against vulnerabilities.

DNS (Domain Name System)

Introduction

The Domain Name System (DNS) is a hierarchical and decentralized naming system used to resolve human-readable domain names into machine-readable numerical values coded in binary known as IP addresses. DNS is a fundamental component of the internet, enabling users to access websites using domain names instead of numeric IP addresses.

How DNS Works

DNS resolution involves translating a domain name into an IP address through a series of queries and responses. The process generally follows these steps:

1. **Query**

A client sends a DNS query for a domain name to a DNS resolver.

1. **Resolver**

The resolver checks its cache for the requested domain, if not found, it queries a _root DNS server._

1. **Root Server**

The root server responds with the address of a top-level domain (TLD) server (e.g., .com, .net, .gov, .org).

1. **TLD Server**

The TLD server responds with the address of the authoritative DNS server for the domain.

1. **Authoritative Server**

The authoritative server provides the IP address associated with the domain name.

1. **Response**

The resolver returns the IP address to the client, which can then initiate communications with the target server.

DNS Records

DNS records provide the necessary information to route requests correctly. Key DNS record types include:

* **A Record**

This record, known as an _A Record,_ maps a domain name to an IPv4 (Internet Protocol version4) address.

* **AAAA Record**

These records map domain names to IPv6 addresses.

* **CNAME (Common Name) Record**

CNAME records map alias names to canonical domain names.

* **MX (Mail Exchange) Record**

This record specifies mail exchange servers for a domain.

* **NS (Name Server) Record**

NS records indicate the authoritative name servers for any domain.

* **PTR (Pointer) Record**

PTRs map IP addresses to domain names for reverse DNS (rDNS) lookups.

DNS Security Issues

DNS, being a critical part of internet infrastructure, faces several security threats:

* **DNS Spoofing (Cache Poisoning) Attack**

In this attack, you insert false DNS responses into a resolver’s cache, redirecting users to malicious sites.

* **DNS Amplification Attack**

DNS amplification attacks exploit DNS servers to launch volumetric Denial of Service (DoS) attacks by sending small queries that generate large responses to the target.

* **DNS Tunneling**

DNS tunneling encodes data in DNS queries and responses to bypass firewalls and exfiltrate data.

Ethical Hacking Techniques

Opposite of attack techniques against DHCP and DNS servers, you can also use various techniques to assess and enhance DNS security, by implementing the following strategies:

* **DNS Spoofing Simulation**

You can test how DNS servers and DNS clients respond to spoofed responses.

* **DNSSEC (DNS Security Extensions) Implementation**

You can use DNSSEC to evaluate the effectiveness of DNS Security Extensions (DNSSEC) in preventing spoofing and tampering of DNS queries, and DHCP IP address pools and reservations.

* **Traffic Analysis**

It’s important to conduct network traffic analysis daily to monitor DNS network traffic for unusual network patterns or behaviors that may deviate from the normal network traffic baseline to identify, detect, and prevent ongoing attacks.

Mitigation Strategies

To enhance DNS security, you can effectively suggest and recommend mitigation strategies to your client organization the implementation of the following strategies:

* **DNSSEC**

Deploy DNSSEC to ensure data integrity and authentication by digitally signing DNS records.

* **Rate Limiting**

Implement rate limiting to mitigate the impact of DNS amplification attacks.

* **Regular Continuous Monitoring (ConMon)**

Continuously monitor DNS network traffic for signs of abuse and anomalies.

* **Network Segmentation**

You can recommend isolating DNS servers from other critical network components to contain the impact of any compromise. Given the criticality of DNS, segment and isolate your DNS servers away from the production LAN, preferably in a DMZ. This way, if your DNS servers are breached, the adversaries are confined within the DMZ and cannot move laterally within the LAN, thereby preventing further infection. Having an adversary disrupt your entire production LAN is much worse than having one contained in a small, isolated DMZ.
