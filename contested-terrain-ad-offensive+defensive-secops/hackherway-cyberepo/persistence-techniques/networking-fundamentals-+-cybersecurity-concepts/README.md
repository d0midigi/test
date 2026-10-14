# Networking Fundamentals + Cybersecurity Concepts

Welcome to my fully detailed notes on networking and cybersecurity. The notes in this document aim to break down complex topics and theories into easy-to-understand concepts. We'll cover internal networks, Demilitarized Zones (DMZs), IP and MAC addressing, network protocols, the OSI Reference Model, VPNs, and the fundamentals of cybersecurity attacks. Let's dive in!

## 1. Internal Networks

### Definition and Purpose

Internet networks are communication highways within an organization, in particular. They connect various devices and allow employees to share information and resources seamlessly. By segmenting networks based on the importance of the devices and the sensitivity of the information and data they may carry and store, organizations can enhance both collaboration and security via network segmentation.

### Explaining the Need for Network Segmentation

Network Segmentation divides a computer network into smaller, isolated zones, known as _subnets_ using firewalls, routers, or switches to control traffic flow, limit the spread of cyberattacks through lateral movement, improve overall security performance, and compliance by applying specific policies to each "leg" (e.g., segmented portion) of the network. I like to look at is creating firewalls within a network, so if one part is breached, the other portions of the segmented network remain functional and unbothered, and ensures the attacker cannot easily access sensitive areas within the remaining operational segments, like a bank keeping all branch data separate from the main financial network.

Some key benefits include:

* **Enhanced Security:** Prevents attackers from moving freely via lateral movement after an initial breach, reducing the attacker's reach further into the network.
* **Improved Performance:** Reduces network congestion by keeping segmented traffic localized and within that segment only.
* **Better Compliance:** Helps meet regulatory requirements like PCI DSS, or HIPAA, by isolating sensitive data and prevents data leakage.
* **Easier Management:** Simplifies troubleshooting and access control issues.

### How to Implement Internal Networks

To set up effective internal networks, consider these strategies:

* **Design Subnets:** Create smaller networks based on departments (like HR, IT, or Finance) to tailor performance and security needs.
* **Use Access Control Lists (ACLs):** Establishing ACLs to restrict access to sensitive data and services based on user roles and responsibilities (e.g., via RBAC).
* **Monitoring and Logging:** Implementing monitoring tools to track network traffic and detect anomalies in near-real-time.

### Demilitarized Zones (DMZs)

#### Definition and Functionality

A Demilitarized Zone (DMZ) is a specialized network segment that acts as a buffer zone between an organization's internal network(s) and the public internet. Its primary function is to enhance security by isolating externally-facing services and assets from internal resources. A DMZ is essentially an extra layer of security for public-facing services like web browsing or emailing services, isolating them from sensitive data.&#x20;

**Purpose:** To allow controlled access to some network services from the internet while Shielding the internal network(s) from direct attacks.

**How it Works:** Servers needing external access (like web or email servers) are placed in a DMZ. Firewalls or edge routers with SACLs control network traffic between the internet and the DMZ, and the internal network(s), so a breach in the DMZ doesn't immediately or necessarily compromise the well-being of the remaining internal network(s). It is always better to have half of a network down than an entire network!

**Example:** A company places its SSL VPN in the DMZ so remote employees can access it, but attackers cannot easily reach employee VPN credentials.

#### Design Considerations

When designing a DMZ, consider the following factors:

* **Public-Facing Services and Assets:** Identifying which services, for example, web servers, email servers, need to be accessible from the internet.
* **Access Control Mechanisms:** Implementing firewalls and IDS to monitor and control network traffic entering and leaving the DMZ.
* **Isolation from Internal Network(s):** Ensuring that the DMZ is segmented from the internal network(s) to prevent unauthorized access.

#### Typical DMZ Architecture

A well-structured DMZ architecture typically includes:

* **Two Domain Controllers:** One domain controller to authenticate DMZ user accounts, and the other as a redundant control in case the primary DC should fail.
* **Two firewalls:** One firewall separates the DMZ from the internet, and the other firewall separates the DMZ from the internal network(s).
* **Load Balancers:** Distributes incoming network traffic to multiple servers to enhance availability and performance.
* **Monitoring Systems:** Utilizing SIEM solutions to analyze and respond to security incidents in near-real-time.

### IP Addresses

IP addresses are numerical labels that are assigned to devices that participate in a computer network, serving as unique Identifiers for communications. They operate at Layer 3, the Network Layer, of the OSI Reference Model and are necessary for routing data packets and transmissions across networks.

#### Classifications of IP Addresses

IP addresses can be categorized into several classes based on their ranges and subnetting capabilities:

* **Class A**
  * **Range:** `10.0.0.0` to `10.255.255.255`
  * **Subnet Mask:** `255.0.0.0`
  * **Hosts per Network:** Up to 16,777,214
  * **Usage:** Large networks (e.g., Google).
* **Class B**
  * **Range:** `172.16.0.0` to `172.31.255.255`
  * **Subnet Mask:** `255.255.0.0`
  * **Hosts per Network:** Up to 65,534
  * **Usage:** Medium-sized networks (e.g., university campuses)
* **Class C**
  * **Range:** `192.168.0.0` to `192.168.255.255`
  * **Subnet Mask:** `255.255.255.0`
  * **Hosts per Network:** Up to 254
  * **Usage:** Small networks (e.g., home network)
* **Loopback**
  * **Range:** `127.0.0.0` to `127.255.255.255`
  * **Subnet Mask:** `255.255.255.0`
  * **Usage:** Testing and troubleshooting network applications.

#### Public vs. Private IP Addresses

* **Public IP Addresses:** Assigned by Internet Service Providers (ISPs) and accessible over the internet.
* **Private IP Addresses:** Used within internal networks and not routable on the internet; keeps internal device hidden from the public.

### MAC (Media Access Control) Addresses

#### Definition and Structure

A Media Access Control (MAC) address is a hardware identifier that is assigned to Network Interface Cards of a device for communications at the Data Link Layer, Layer 2 of the OSI Reference Model. It is used to uniquely identify devices on a local network as no two devices can share or have the same MAC address (much like home addresses).

#### Format

A MAC address (Media Access Control) is a unique 48-bit hardware identifier, usually shown as six groups of two hexadecimal digits (`0-9`, `A-F`) separated by colons (e.g., `00:1A:2B:3C:4D:5E`), hyphens (e.g., `00-1A-2B-3C-4D-5E`), or sometimes just concatenated (e.g., `001A2B3C4D5E`).

MAC addresses have two main parts: the first half (24 bits/3 bytes) is the _**OUI (Organizationally Unique Identifier)**_, identifying the device's manufacturer, and the second half (24 bits/3 bytes) is the _**Device Identifier**_, a unique serial number assigned by that manufacturer to that specific Network Interface Card (NIC). Essentially, it is the Manufacturer's Code + The Device's Unique ID.

* **OUI (First Half):** This part identifies the company that made the network hardware (like Intel or Apple) and is assigned by the IEEE.
* **Device Identifier (Second Half):** This is a unique sequence assigned by the manufacturer to distinguish it from all other devices they produce.&#x20;

**Example:** In `01:32:54:76:85:AB`, `01:32:54` is the OUI (manufacturer), and `76:85:AB` is the unique device ID.&#x20;

* **`00:1A:2B`**: Manufacturer (e.g., Cisco).
* **`3C:4D:5E`**: Unique device identifier.&#x20;

#### Example Breakdown

For `00:1A:2B:3C:4D:5E`:

* **48 bits:** Each group of two hex digits represents 8 bits (a byte).
* **OUI (Organizationally Unique Identifier):** The first 24 bits (first three groups) identify the device manufacturer, assigned by the IEEE.
* **NIC Specific:** The last 24 bits are unique to the Network Interface Controller (NIC) within that manufacturer's range.&#x20;

### Common Formats

* **Colon-separated:** `XX:XX:XX:XX:XX:XX` (Most common)
* **Hyphen-separated:** `XX-XX-XX-XX-XX-XX` (Common on Windows)
* **Dot-separated:** `XXXX.XXXX.XXXX` (Less common, used by some systems)
* **Concatenated:** `XXXXXXXXXXXX` (No separators)&#x20;

<br>

<br>

<br>







**Information Sharing:** Enabling se
