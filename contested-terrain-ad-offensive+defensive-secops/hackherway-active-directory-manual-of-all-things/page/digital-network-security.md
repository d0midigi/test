# Digital Network Security

Digital Network Security

This section provides an overview of fundamental network communications concepts that are essential for understanding various cybersecurity topics, including cryptographic applications such as blockchains and cryptocurrencies. The following sections summarize the key concepts:

Data Communications

The process of transmitting data between applications on remote computing nodes involves a well-defined process of generating data packets and converting them into transmissible bit streams for reliable end-to-end delivery over unreliable and untrustworthy media.

The OSI Model

The Open Systems Interconnection (OSI) model, developed by the International Standards Organization (ISO), is a seven-layered conceptual stack that classifies these well-defined processes. The layers, from bottom to top, are:

1. **L1: Physical Layer:** Responsible for transmitting bits over a physical medium with pre-defined electrical and mechanical specifications.
2. **L2: Data Link Layer:** Organizes bits into frames for node-to-node delivery, adding headers and trailers for error-free transmission.
3. **L3: Network Layer:** Moves packets from source to destination nodes, providing internetworking and media sharing.
4. **L4: Transport Layer:** Provides reliable end-to-end message delivery by overseeing error recovery and flow control processes.
5. **L5: Session Layer:** Establishes, manages, and terminates communication sessions between two remote applications.
6. **L6: Presentation Layer:** Translates between native communication languages, provides data compression, and encryption for secure communications.
7. **L7: Application Layer:** Facilitates access to network resources, such as directory services, mail services, virtual terminals, and file management.

Networking Devices

The Internet is composed of various networking devices, including:

1. **Repeaters:** Operate at the Physical layer, regenerating the bit-stream to ensure reliable transmission.
2. **Bridges:** Operate at both the Physical and Data Link layers, dividing or combining smaller networks. They divide a large network into smaller sub-networks or combine smaller sub-networks of the same type into a larger network. Bridges contain a list of all the nodes connected to either side of it and so it can intelligently filter and forward packets to the intended recipients on either side.
3. **Routers:** Operate at the Physical, Data Link, and Network layers, establishing the best paths for packets to travel from source to destination nodes. Routers gain knowledge about the network configuration and path characteristics from periodic communications with other Routers. Eventually, all routers have knowledge about the network to which they are connected so that each can determine the best path for routing packets. Routers typically use the _Dijkstra_ graph theory algorithm 8 to determine the shortest path to other routers. They also track and update a packet’s lifetime and may eventually “kill” a packet if it has not found its owner within a predetermined time. This mechanism prevents network congestion when disabled nodes cause looping or bouncing because packets reach dead-ends.<br>
4. **Gateways:** Can operate in all seven layers of the OSI model, converting between protocols to enable data transfer across different network types. Physically, a gateway is no more than an additional “leg” of the network, or software running on the router.

These networking concepts provide a foundation for understanding network communications and are essential for exploring cybersecurity topics in subsequent sections.

The Origins of TCP/IP and Its Relationship to the OSI Model

The Advanced Research Projects Agency (ARPA), a U.S. Department of Defense arm, developed TCP/IP in 1969 for connecting computers in a large network called ARPANET, now known as the mighty Internet. Although TCP/IP predates the OSI model, it does not conform exactly to the OSI standard. Instead, TCP/IP combines the application, presentation , and session layers into a single application or message layer. The transport or segment layer is defined either by TCP or UDP, while IP defines the network or datagram layer. The Data Link and Physical layers are network-dependent and consist of organized patterns of frames and bits, respectively.

IP: An Unreliable and Connectionless Protocol

IP is an unreliable and connectionless protocol. Unreliability means that IP does not provide error checking or datagram tracking; however, reliability can be achieved by pairing IP with a reliable transport protocol such as TCP. Connectionless refers to the fact that no virtual circuit is established for the transmission of the entire message, which consists of an ordered series of datagrams. Each datagram is transmitted separately and may not follow the same path. Unlike connection-oriented services, the receiver is not alerted about incoming messages, and it is not expected to acknowledge successful receipt of the entire message once it has been completely transmitted.

Datagram Structure and IP Addresses

Each datagram consists of a 20-60 byte header and a data portion, with a total length not exceeding 65,536 bytes. The header contains essential information for routing and delivery, including fields for source IP address, destination IP address, and datagram lifetime. Other fields relate to packet fragmentation, service class, reference protocol, routing, timing, management, and alignment controls.

IP addresses in the current Internet Version (IPv4) consist of four bytes that define a class type, network identification (NID), and host identification (HID). Currently, only one of the five address classes is available for use, with the first two already full. The fourth class is reserved for multicasting, and the fifth is reserved for future use.

Sub-Protocols of IP

IP supports three additional sub-protocols: Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP), and Internet Control Message Protocol (ICMP), or _ping._ ARP is used to associate an IP address with the physical address of a device, typically the Network Interface Card (NIC) hard-coded address. Hosts and routers use ARP to find the physical address associated with an IP address by broadcasting an ARP query packet to every node on its sub-network and receiving an answer only from the owner. RARP allows a host to determine its IP address when it knows only its physical address. The host broadcasts its physical address in an RARP request packet and receives its IP address ony from the network node that knows it.

ICMP enables hosts to determine when an IP datagram is undeliverable. This sub-protocol plays a crucial role in troubleshooting network issues.

Transport Layer Protocols: TCP and UDP

Both TCP and UDP represent the Transport layer portion of the protocol. TCP is a reliable, connection-oriented protocol, whereas UDP is unreliable and connectionless, making it simpler. Both UDP and TCP connections are port-to-port, unlike IP, which provides host-to-host connectivity.

The multi-tasking operating system of the host machine assigns a port to each active process. A port is essentially a data buffer associated with a process. As such, UDP and TCP segment headers carry both the source and destination port addresses.

TCP, being a reliable protocol, contains identification and sequencing numbers to identify specific lost or damaged segments. TCP sets up an end-to-end virtual circuit for the entire duration of the segment transmission, so that the end ports know to expect more datagrams and check their sequencing. This virtual circuit session should not be confused with the Session layer protocol, which is concerned with the entire message exchange, not just the segment.

TCP achieves reliability by adding header information that facilitates error detection, acknowledgements, and frame retransmission. This ensures that data is transmitted accurately and reliably over the network.

Mobile IP: Enabling Seamless Connectivity for Mobile Units

Mobile IP is a standard proposed by the Internet Engineering Task Force (IETF) that enables a mobile unit (MU) to maintain a fixed home address while roaming across different networks. This allows remote applications to interact with the MU transparently, without interruption , as it moves seamlessly across IP-based networks. The scope of this standard is limited to packet-switched connections based on IP.

To facilitate this mobility, Mobile IP relies on the existence of a home agent network node. When the MU attaches to a foreign network, it registers with a foreign agent, which assigns a new _care-of address._ The MU obtains a new care-of address through Dynamic Host Configuration Protocol (DHCP) and registers it with the home agent. This registration process occurs either directly or indirectly via the foreign agent, depending on the nature of the attachment.

Mobile IP utilizes User Datagram Protocol (UDP) with retransmission parameters to avoid the complexities of Transmission Control Protocol (TCP). After registration, packets arriving at the home agent are redirected to the foreign agent at the care-of address. The foreign agent then substitutes the destination -IP address with the static home-IP address and delivers the packets to the MU.

Mobile IP is implemented at the Network layer of the OSI model, ensuring that applications running above, such as TCP, remain unaware of roaming as the MU changes its point of attachment to the network. Applications will continue to see the MUs static home-IP address as its source address when sending data and as the destination address when receiving data. As a result, Mobile IP implementation provides seamless application connectivity as the MU roams and attaches to new IP nodes.

![A diagram of a network

Description automatically generated](<../.gitbook/assets/0 (24).png>)\
_**FIGURE X:** Illustration of a Mobile IP process._

Ensuring Seamless Mobility with Mobile IP

The home agent plays a crucial role in maintaining transparency by re-encapsulating arriving packets with a new IP address destination wrapper to the care-of address. The foreign agent then unwraps the packet before forwarding the Mobile Unit (MU). This re-encapsulates process is often a subset of a secure tunneling protocol, such as IPSec. As a result, Mobile IP can accommodate a VPN-style tunnel between the home agent and foreign agent.

A secure connection between the home and foreign agents is essential to prevent rogue network entities from updating the home agent with a fake care-of address, redirecting packets to an unintended destination.

When MUs roam, they must either discover home and foreign agents through advertisements or solicit prospective agents. Several MUs can share a single care-of address, as each MUs home address remains unique and unchanged during tunneling transit. After “de-tunneling,” each MU receives packets intended from them.

MUs capable of running Mobile IP can serve as their own foreign agent, provided they have access to a DHCP server for IP address management. In this case, the care-of address is referred to as a co-located care-of address. When acting as its own foreign agent, the MU must also be capable of running the required tunneling protocol.

Foreign agents can directly route packets from the MU to the remote host and bypass the home agent during the reverse trip. Hosts capable of implementing a directory cache of care-of addresses and a tunneling protocol can bypass the home agent, reducing network traffic congestion and potentially inefficient routes.

Although Mobile IP is a leading proposal for seamless roaming in next-generation Internet applications, there are several disadvantages to consider. For instance, if the point of MU attachment changes faster than the round-trip time for a packet, packets may be lost due to outdated routing tables. Additionally, TCP timers are not adaptively reconfigurable and depend on network connection parameters. This can lead to inefficient data communications links when switching between slower and faster wireless connections. As tunnel overhead and network delays change while the MU roams, remote applications may unnecessarily increase error and flow control handshakes, exacerbating the problem.

Firewalls

To address the topic of firewalls and their role in preventing unauthorized access and communications within an intranet, or network, we’ll expand upon the initial discussion to include various types of firewalls and simulate a scenario of firewall evasion. This will involve understanding the operation of firewalls, exploring different types, and then demonstrating how one might attempt to evade these defenses.

Understanding Firewalls

Firewalls play a damn important role in network security. Afterall, they are considered the first line of network perimeter defense, and among them, packet filtering firewalls are foundational. They operate at the Network layer, examining incoming and outgoing packets based on predetermined criteria. Understanding their operations and implications in ethical hacking assessments is essential for modern cybersecurity strategies in today’s day in age. This section will explore the intricacies of packet filtering firewalls, amongst others, and their intersection with hacking, evasion, and defense.

Functioning of Packet Filtering Firewalls

Packet filtering firewalls work by inspecting data packets as they move across the network. They evaluate

* **Packet Filtering Firewalls**

Inspecting incoming and outgoing packets based on predefined rules to allow or block ingress/egress network traffic, applications, protocols, by packets, or by IP address ranges and zones.

* **Stateful Inspection Firewalls**

These firewalls keep track of active connections and allow traffic based on the state of these connections.

* **Application-Level Gateways (Proxying Firewalls)**

Acting as an intermediary for requests from clients seeking resources from other servers.

* **Next-Generation Firewalls (NGFW)**

NGFWs combine traditional firewall capabilities with additional features like Intrusion Prevention Systems (IPSs), application awareness, and advanced threat protection.

Types of Firewalls

1. **Network Address Translation (NAT) Firewalls:** These firewalls translate IP addresses from one network to another, hiding the internal network structure from external entities.
2. **Circuit-Level Gateway (Proxy Server):** Operates at the Session layer, controlling the establishment of TCP connections.
3. **Application-Level Gateway (Proxy Server):** Acts as an intermediary for requests from clients seeking resources from other servers.
4. **Next-Generation Firewall (NGFW):** Offers advanced security features beyond traditional firewalls, including deep packet inspection and intrusion prevention.
