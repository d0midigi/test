# Networking Concepts 101

\### Abstract

In the era of information technology, computer networks serve as the foundational infrastructure, with protocols acting as the universal language enabling communication across the digital landscape. This chapter lays the groundwork for understanding the essentials of networking, beginning with the necessary hardware components and progressing through network topologies to the operation of prevalent protocols within Ethernet/IP/TCP networks. It culminates in an exploration of Man-in-the-middle attacks. Aimed at individuals seeking to establish or reinforce their comprehension of networking fundamentals.

\### Components

Establishing a computer network necessitates a variety of hardware elements. The specific requirements depend on the nature of the network, encompassing items such as cables, modems, antiquated acoustic couplers housed in modified fruit containers, antennas, or satellite dishes, alongside computers equipped with network interface cards, routers (refer to Sect. 2.14), gateways, firewalls, bridges, hubs, and switches.

A hub functions as a straightforward device into which network cables are plugged, distributing incoming signals equally across all connected ports. This characteristic, however, tends to generate excessive network congestion, leading to hubs becoming less favored in contemporary setups. More commonly, networks now rely on switches, which form the central nervous system of modern networking environments. Unlike hubs, switches possess the capability to memorize the Media Access Control (MAC) addresses of network interfaces linked to each port, directing traffic exclusively to its intended destination. Further elaboration on MAC addresses will be provided in subsequent sections.

Topologies

You can set up and configure computer networks in various ways. Today, the most common configuration is the star network (see Fig. 2.1), where all computers are connected to a central device. The downside of this setup is that the central device is a single point of failure, meaning the entire network will go down if this device fails. This issue can be mitigated by using redundant devices.

Another configuration is the bus network (see Fig. 2.2), where all computers are connected in a line, one after the other. The disadvantage of this topology is that each computer needs two network cards, and traffic must pass through all computers on the network. If one computer fails or is overloaded, connections beyond that point are lost. In recent years, bus networks have become rare and are typically used for specific purposes such as database replication, clustering of application servers, or synchronization of backup servers. These scenarios often require a bus network to reduce the load on the star network.

The ring network (see Fig. 2.3) connects all computers in a circle. It has similar disadvantages to the bus network, but if a computer fails, the network can reroute traffic the other way, preventing complete failure. Although the author has not encountered a productive ring network, it is rumored to be the topology of choice for backbones used by ISPs and large companies.

In networking, you might also come across terms like LAN (Local Area Network), WAN (Wide Area Network), and sometimes MAN (Metropolitan Area Network). A LAN is a local network usually confined to a building, floor, or room. In modern networks, most computers are connected to a LAN via one or more switches. Multiple LANs connected through a router or VPN form a MAN. If the network spans multiple countries or the entire world, like the internet, it is classified as a WAN.

\### ISO/OSI Layer Model

The ISO/OSI layer model technically separates a computer network into seven layers (see Fig. 2.4). Each layer has a specific function, and data packets pass through these layers sequentially in the operating system's kernel up to the layer they operate on (Table 2.1).

\| OSI Layer | Layer Name | Task |

\|-----------|--------------|------------------------------------------------------------|

\| 1 | Physical | Cables, antennas, etc. |

\| 2 | Data-Link | Creates a point-to-point connection between two computers |

\| 3 | Network | Provides addressing for the destination system |

\| 4 | Transport | Ensures data is received in the correct order and retransmits lost packets |

\| 5 | Session | Manages sessions between applications (e.g., using ports) |

\| 6 | Presentation | Converts data formats (e.g., byte order, compression, encryption) |

\| 7 | Application | Defines protocols for services like HTTP |

\### Ethernet

If you've ever purchased a network cable or card from a store, it's almost certain that you own Ethernet hardware, as Ethernet is by far the most widely used network technology today. Ethernet components come with different speed limits such as 1, 10, 100 Mbit, or gigabit, and can use various cable types like coaxial (old school), twisted pair (common), or fiber optic (for high data demands).

Twisted pair cables are divided into STP (Shielded Twisted Pair) and UTP (Unshielded Twisted Pair), as well as patch and crossover cables. STP cables are shielded, making them higher quality than UTP cables. Patch and crossover cables can be distinguished by their plugs: if the colors of the wires are in the same order, it’s a patch cable; otherwise, it's a crossover cable. Crossover cables are used to connect two computers directly, while patch cables connect a computer to a hub or switch. Modern network cards can automatically configure connections, making crossover cables increasingly obsolete.

Every network card in an Ethernet network has a unique MAC address used to address devices on the network. The MAC address consists of six pairs of hexadecimal numbers separated by colons (e.g., aa:bb:cc:11:22:33). Contrary to popular belief, computers in a local TCP/IP network are accessed via their MAC addresses, not IP addresses. Additionally, the MAC address can be spoofed, as the operating system writes the MAC address into the Ethernet header and systems like GNU/Linux or \*BSD can change the MAC address with a single command.

The Ethernet header (see Fig. 2.5) contains the source and destination MAC addresses, a type field, and a checksum. The type field specifies the protocol following Ethernet, such as 0x0800 for IP or 0x0806 for ARP.

Finally, CSMA/CD (Carrier Sense Multiple Access/Collision Detect) explains how data is sent over an Ethernet network. A computer first listens to check if the wire is free. If another device is transmitting, it waits a random number of seconds before trying again. If the channel is clear, it sends the data. If two devices transmit simultaneously, a collision occurs, and each device must detect this, wait randomly, and retransmit the data.

\### 2.5 VLAN

A VLAN (Virtual Local Area Network) separates several networks on a logical basis. Only devices on the same VLAN can communicate with each other. VLANs were invented to define a network's structure independently of its physical hardware, to prioritize connections, and to minimize broadcast traffic. Although they were not designed with security in mind, a common misconception is that VLANs enhance security. This is not reliable since there are several methods to bypass VLAN separation (see Sect. 4.5).

Switches implement VLANs in two different ways: by tagging packets using an IEEE 802.1q Header (see Fig. 2.6), which is inserted after the Ethernet header, or by defining them by port. The 802.1q method is newer and allows the creation of VLANs that span multiple switches.

\### 2.6 ARP

ARP (Address Resolution Protocol) translates between layer 2 (Ethernet) and layer 3 (IP). It is used to resolve MAC addresses to IP addresses. The reverse operation is performed by RARP (Reverse Address Resolution Protocol). The structure of an ARP header can be seen in Fig. 2.7.

For example, when a source host (192.168.2.13) attempts to communicate with a destination host (192.168.2.3) for the first time, it will broadcast a message to all devices on the network: “Hello, here is Bob, to all, listen! I want to talk to Alice! Who has the MAC address of Alice?!”

In technical terms, this ARP request looks like this:

\`\`\`

ARP, Request who-has 192.168.2.3 tell 192.168.2.13, length 28

\`\`\`

The destination host (192.168.2.3) will then reply:

\`\`\`

ARP, Reply 192.168.2.3 is-at aa:bb:cc:aa:bb:cc, length 28

\`\`\`

\### 2.7 IP

IP, like Ethernet, is a connectionless protocol, meaning it does not establish a continuous connection between devices. IP is used to define the source and destination hosts at layer 3, to find the quickest path between communication partners by routing packets (see Sect. 2.14), and to handle errors using ICMP (Sect. 2.8). One common error is the "host not reachable" packet.

IP also handles fragmentation, breaking larger packets into smaller ones to fit the MTU (Maximum Transmission Unit). It uses a TTL (Time-to-Live) header to avoid endless loops in the network. Each hop a packet passes through decreases the TTL by one; if TTL reaches zero, the packet is discarded, and the source host is notified via ICMP.

Today, there are two versions of IP: IPv4 and IPv6. They differ significantly, not just in the size of IP addresses. IPv6, for example, can be extended through optional headers and is more complex. This text covers only IPv4.

An IPv4 address (e.g., 192.168.1.2) consists of four bytes, each represented by a number between 0 and 255. Each IP network node also requires a netmask, such as 255.255.255.0, which defines the network's size and is used to calculate the network's starting address. The first IP of a network is called the network address, and the last one is the broadcast address, which cannot be used by hosts.

For a computer to communicate over an IP network, it first calculates its network address using its IP address and netmask. For example, with an IP of 192.168.1.2 and a netmask of 255.255.255.0:

\| Binary Representation | Decimal Representation |

\|------------------------------|-----------------------------|

\| IP Address | 192.168.1.2 |

\| 11000000.10101000.00000001.00000010 | |

\| Netmask | 255.255.255.0 |

\| 11111111.11111111.11111111.00000000 | |

\| Network Address (Binary AND) | 192.168.1.0 |

\| 11000000.10101000.00000001.00000000 | |

The netmask shows how many bits of an IP address are reserved for the network and how many for the host. In our example, the first 24 bits are for the network (/24 or CIDR block). If the destination network is different, the packet is sent to the default gateway; otherwise, it is routed within the same network.

\### 2.8 ICMP

ICMP (Internet Control Message Protocol) is used by IP for error handling. It sets a type and code field in its header to define the error (see Fig. 2.10).

Many are familiar with ICMP through the ping command, which sends an ICMP echo-request and expects an echo-response to check if a computer is reachable and to measure latency. Other ICMP messages include redirect-host, which informs a host of a better router to use. Table 2.2 lists all ICMP type and code combinations.

\### 2.9 TCP

TCP (Transmission Control Protocol) manages sessions between computers. It establishes a new session using the Three-Way Handshake (see Fig. 2.13) and numbers all packets to ensure they are received in order. The destination host acknowledges each packet received correctly and requests retransmission if necessary. TCP also uses ports to address programs on a host, with commonly used protocols like HTTP, FTP, and IRC having default ports below 1024 (e.g., HTTP typically uses port 80).

A typical TCP header includes source and destination ports, sequence and acknowledgment numbers, flags for session management, and a window size (see Fig. 2.11). The window size defines the buffer for received but not yet processed packets, indicating the sender to slow down if the buffer is full.

The Three-Way Handshake involves three steps:

1\. The initiating computer sends a packet with the SYN flag and an Initial Sequence Number (e.g., 1000).

2\. The destination responds with a packet with SYN and ACK flags, an Initial Sequence Number (e.g., 5000), and the Acknowledgment Number incremented by one (1001).

3\. The initiator sends a final packet with the ACK flag, using the acknowledgment number from the SYN/ACK packet as its sequence number and the previous sequence number plus one as its acknowledgment number, completing the handshake.

If a packet hits a closed port, the destination sends a RST (reset) packet to indicate the request was invalid, as per RFC793. Many firewalls, however, block these RST packets to obscure the presence of the service and increase security.

\### 2.10 UDP

UDP (User Datagram Protocol) is a simpler alternative to TCP. It does not provide session management, meaning it does not guarantee the delivery, order, or integrity of the packets. This makes UDP faster and more suitable for applications that require quick data transmission, such as online gaming, live broadcasts, or VoIP (Voice over IP). The structure of a UDP header is straightforward and consists of the source port, destination port, length, and checksum (see Fig. 2.14).

\### 2.11 DHCP

DHCP (Dynamic Host Configuration Protocol) is a network management protocol used to automate the process of configuring devices on IP networks. It allows devices to request IP addresses and networking parameters automatically, reducing the need for a network administrator to manually assign IP addresses. The process of a DHCP transaction includes four steps, known as DORA: Discovery, Offer, Request, and Acknowledgment.

1\. \*\*Discovery\*\*: A client broadcasts a DHCPDISCOVER message to locate available DHCP servers.

2\. \*\*Offer\*\*: A DHCP server responds with a DHCPOFFER message, offering an IP address to the client.

3\. \*\*Request\*\*: The client replies with a DHCPREQUEST message, indicating it accepts the offer.

4\. \*\*Acknowledgment\*\*: The server sends a DHCPACK message to finalize the configuration.

\### 2.12 DNS

DNS (Domain Name System) translates human-readable domain names (e.g., www.example.com) into IP addresses (e.g., 192.0.2.1). This system is essential for the usability of the internet, as it allows users to access websites using easy-to-remember names instead of numerical IP addresses.

When a user enters a domain name into their browser, the DNS resolver client queries the DNS server. If the server has the requested domain in its cache, it responds with the corresponding IP address. If not, the server will query other DNS servers in a hierarchical manner until it finds the correct IP address.

\### 2.13 NAT

NAT (Network Address Translation) allows multiple devices on a local network to share a single public IP address for accessing the internet. This helps conserve the limited number of available public IP addresses and provides an added layer of security by hiding internal IP addresses from external networks.

There are several types of NAT:

\- \*\*Static NAT\*\*: Maps a single private IP address to a single public IP address.

\- \*\*Dynamic NAT\*\*: Maps a private IP address to a public IP address from a pool of available public addresses.

\- \*\*PAT (Port Address Translation)\*\*: Maps multiple private IP addresses to a single public IP address, using different ports to distinguish between the connections.

\### 2.14 Routing

Routing is the process of selecting paths in a network along which to send network traffic. Routers are devices that perform this function, directing data packets based on their destination IP addresses. Routing can be static or dynamic:

\- \*\*Static Routing\*\*: Involves manually configuring routing tables with fixed paths.

\- \*\*Dynamic Routing\*\*: Uses protocols like OSPF (Open Shortest Path First), BGP (Border Gateway Protocol), and RIP (Routing Information Protocol) to automatically update routing tables based on network changes.

\### 2.15 Firewall

A firewall is a network security device that monitors and controls incoming and outgoing network traffic based on predetermined security rules. Firewalls can be hardware-based, software-based, or a combination of both. They are used to establish a barrier between trusted internal networks and untrusted external networks, such as the internet.

Firewalls operate at different layers of the OSI model:

\- \*\*Packet Filtering Firewalls\*\*: Operate at the network layer, filtering packets based on IP addresses, ports, and protocols.

\- \*\*Stateful Inspection Firewalls\*\*: Operate at the transport layer, tracking the state of active connections and making decisions based on the context of the traffic.

\- \*\*Application Layer Firewalls\*\*: Operate at the application layer, inspecting the payload of packets and making decisions based on the content.

\### 2.16 VPN

A VPN (Virtual Private Network) extends a private network across a public network, allowing users to send and receive data as if their devices were directly connected to the private network. VPNs provide privacy, security, and anonymity by encrypting the data transmitted over the public network.

There are different types of VPNs:

\- \*\*Remote Access VPN\*\*: Allows individual users to connect to a private network remotely.

\- \*\*Site-to-Site VPN\*\*: Connects entire networks to each other, typically used to link branch offices to a main office.

VPN protocols include:

\- \*\*PPTP (Point-to-Point Tunneling Protocol)\*\*: An older protocol with basic security.

\- \*\*L2TP (Layer 2 Tunneling Protocol)\*\*: Often combined with IPsec for better security.

\- \*\*OpenVPN\*\*: An open-source protocol known for its strong security and flexibility.

\- \*\*IKEv2/IPsec (Internet Key Exchange version 2)\*\*: Provides robust security and is widely used in mobile devices.

\### 2.17 Conclusion

Understanding the basics of networking, including VLANs, ARP, IP, ICMP, TCP, UDP, DHCP, DNS, NAT, routing, firewalls, and VPNs, is essential for anyone working in IT or cybersecurity. Each of these components plays a critical role in the functioning and security of modern networks. As technology continues to evolve, staying informed about the latest developments and best practices in networking is crucial for maintaining secure and efficient network operations.

\### 2.10 UDP

UDP (User Datagram Protocol) is, like TCP, a protocol of the transport layer, but in contrast to TCP, it lacks session support and is therefore classified as stateless. It doesn’t care about packet loss or order and only implements addressing of programs through ports. A typical UDP header can be seen in Fig. 2.14.

UDP works by the principle of “fire and forget” and is mostly used for streaming services like internet radio or television, but it's also the most commonly used transport protocol for DNS. The advantage of UDP is the small size its header adds to the packet, resulting in much higher speed.

\### 2.11 An Example Network

An Ethernet/TCP/IP network is what you think of nowadays when you hear the term network, as it is by far the most common one. It consists of five layers instead of the theoretical seven layers of the ISO/OSI model. For a quick refresh: Ethernet is on Layer 2, IP (Internet Protocol) on Layer 3, TCP (Transport Control Protocol) or UDP (see Sect. 2.10) on Layers 4–6, and services like HTTP, SMTP, and FTP on Layer 7.

Let's see how an HTTP packet passes through all those layers one after another. In our example, we want to get the index page of www.springer.com/. First, our computer parses the URL www.springer.com/ into the following components: HTTP as the application protocol to be used, the hostname www, the domain springer, the Top-Level-Domain - TLD for short - (com), and the resource we try to receive in this case /.

Armed with this information, our computer constructs the following HTTP-Header (Layer 7):

\`\`\`

GET / HTTP/1.1

Host: www.springer.com

\`\`\`

Next, we head on to TCP (layers 4–6). It establishes a connection by the use of the Three-Way Handshake, addressing the destination port 80 (HTTP) and a random source port to connect the browser with the network.

IP (Layer 3) recognizes that it cannot use www.springer.com for addressing since it can only use IP addresses such as 62.50.45.35, so it makes a DNS query to resolve the IP for the hostname. We will learn more about DNS in Chap. 6. Now IP checks if the destination host is in the same network as our computer. This is not the case; therefore, a lookup into the routing table is necessary to retrieve the address of the next hop. There is no entry for the destination network, thus the default gateway is used to send the packet to the outside world. Last but not least, IP writes the address of the network card used to send the packet into the source address, and our packet travels to the next layer.

On Layer 2, the packet gets received by the Ethernet protocol. ARP takes care of resolving the MAC address of the destination IP address and remembers them in the ARP cache, ensuring it doesn’t have to ask the network for every packet. Ethernet writes the MAC of the outgoing network card as the source into the header and forwards the packet to the last layer (physical), in this case, the driver of the network card, which will translate the packet to zeros and ones and transmit it on the medium.

\### 2.12 Architecture

From the perspective of clients, a network can have two logical structures: client/server or peer-to-peer (P2P).

A client/server architecture (e.g., HTTP) consists of a computer (server) that implements one or more services and another computer (client) that consumes a service. The client sends a request, and the server answers with a response if it likes the format of the request and thinks the client is authorized to ask.

In a Peer-to-Peer (P2P) architecture (e.g., file sharing), all computers are equal. Everyone can admit and consume a service at the same time. Most network connections rely on the client/server architecture.

\### 2.13 Gateway

A gateway connects a network with one or more other networks. The most common task of a gateway is to be the so-called “default gateway,” the router to whom all packets are sent, which don’t match any other local routes of a computer's routing table.

Nowadays, a gateway manages the connection of a local area network (LAN) with the internet and is therefore equal to a router. Some decades ago, a gateway was responsible for translating between different kinds of networks like Ethernet and Token-Ring.

\### 2.14 Router

Looking at routers, you can differentiate at least two kinds: internet routers administered by your internet service provider (ISP) and home routers to connect your LAN to the internet and hopefully protect you from most attacks.

Home routers are also often called gateways because they manage the interaction of a network with another. They receive all packets from internal hosts that should be sent to some computer on the internet, write their own public IP address received from the ISP as the source address into it, and forward them to the next router of the ISP.

Internet routers also forward packets, and how that is governed, more, or less depends on a utilizing a huge routing table. They don’t have a static routing table but use different protocols like RIP, OSPF, and BGP to share routing information between each other and find the shortest or otherwise quickest way to the desired destination.

With the help of the command traceroute, one can determine all internet routers a packet passes between their own computer and the destination host, at least if the router replies on certain packets.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/0 (55).png>)

Microsoft Windows \[Version 10.0.22631.3880]

(c) Microsoft Corporation. All rights reserved.

C:\Users\mindhackdiva>tracert www.example.com

Tracing route to www.example.com \[2606:2800:21f:cb07:6820:80da:af6b:8b2c]

over a maximum of 30 hops:

1 4 ms 4 ms 3 ms syn-2403-7005-0906-0f8b-0000-0000-0000-0001.res6.murtceps.com \[2403:8001:302:a8e::1]

2 12 ms 17 ms 22 ms 2403-78d5-0002-00a0-0000-0000-0000-0001.inf6.murtceps.com \[2403:90c5:1:f0::1]

3 15 ms 11 ms 14 ms lag-60.hacknet02h.netops.kraken.com \[2602:e000:0:5::2:12e]

4 \* \* \* Request timed out.

5 15 ms 13 ms 14 ms lag-21.rcr0trustcraft.netops.kraken.com \[2602:e000:0:4::22]

6 \* \* \* Request timed out.

7 \* \* \* Request timed out.

8 15 ms 14 ms 16 ms 2001-1998-0000-0008-0000-0000-0000-0705.inf6.forrestnymph.com \[2001:1998:0:8::705]

9 16 ms 12 ms 19 ms po-68.core1.lac.edgecastcdn.net \[2606:2800:4062:f::1e]

10 13 ms 13 ms 12 ms 2606:2800:21f:cb07:6820:80da:af6b:8b2c

Trace complete.

Bridge

A bridge is a Layer 2 router that sometimes acts as a firewall.

Proxies

A proxy receives requests from a client and sends them to the destination host, presuming it is the real source of the request. It differs from a router in that it acts on Layers 4 to 6 (TCP/UDP) up to Layer 7 (Application) instead of playing on Layer 3 like a router.

Most proxies additionally have the capability to deeply understand the protocol they are working on. This way, they can suppress other protocols that a client may try to speak over its port and filter dangerous/unwanted contents like spam and malware. Furthermore, a proxy could force a user to authenticate by password or smart card before he or she is allowed to use its service.

Normally, a proxy must be explicitly configured by the user. A web proxy, for example, gets inserted into a browser’s configuration, but a special kind of proxy exists where a router or firewall automatically redirects a connection through a proxy without a user realizing it. Such a proxy is called a transparent proxy. Most internet service providers nowadays use such a proxy, at least on HTTP ports, for performance reasons. The proxy caches all static web contents like images and videos on its hard disk. In some countries, transparent proxies are also used to censor and observe internet access.

Some web proxies insert a PROXY-VIA entry into the HTTP header, letting a user know that their connection flows over these proxies and which IP address the proxy has. The existence of this header in a transparent proxy is unlikely and may be a hint of misconfiguration or a slacking sysadmin.

Interested readers could, for example, use the following script to get an overview of all HTTP information sent by their browser to every web server they use:

\[www.codekid.net/cgi-bin/env.pl]

(_**Source:** http://www.codekid.net/cgi-bin/env.pl_)

Virtual Private Networks (VPNs)

Virtual Private Networks (VPN) is a collection of security mechanisms that only have in common the protection of a connection by using encryption and/or authentication. Nearly all VPNs support the possibility to secure access to a whole network and, thanks to powerful cryptography, also protect against espionage and manipulation; therefore, it operates on the protocol stack either on Layers 3, 4, or 7. It can be commonly said that the deeper the VPN intercepts the connection, the more secure it can be because it can prevent attacks on each layer.

Typical protocols or protocol stacks are IPsec, Point-to-Point Tunneling Protocol (PPTP), and OpenVPN. Mostly, they are used to connect outside agencies and to integrate roadrunners (employees who connect to the company network through a mobile internet connection).

Firewalls

A firewall is neither a product nor a tiny, magical box with lots of blinking LEDs, even if more IT security companies try to let you think so. A firewall is a security concept. It serves to protect the network and computers from being attacked and is only as effective as the combination of its components.

Typical parts of a firewall contain:

* Packet filters
* Built-in IDS and malware scanning (antimalware) capabilities
* Intrusion Prevention System (IPS)
* Log analyzer
* Continuous system updates
* Antivirus scanner
* Proxy server capabilities
* Honeypot Creation
* Virtual Private Network (VPN) capability

A packet filtering firewall works on both Layers 3 and 4 of the OSI model and decides which packets shall pass, be dropped, rejected, or redirected depending on its rule set.

HIDS and NIDS

Intrusion detection systems can be classified into two different types: host- and network-based intrusion detection systems. A Host Intrusion Detection System (HIDS for short) locates successful attacks on a local computer by, for example, continuously checking all files and directories against a database of cryptographic checksums.

A Network Intrusion Detection System (NIDS) detects attacks in the network traffic and can operate on all layers at the same time. Its functionality can be compared to a virus scanner because it searches for signatures of known attacks. Additionally, it has the possibility to learn what is classified as normal traffic in a network, and the anomaly detection component alarms packets that differ from it.

Attacks recognized by NIDS can be prevented thanks to an intrusion prevention system (IPS). In the easiest case, it just inserts the attacking IP address into a list of IPs to block, and the packet filter will drop everything from them. Be careful: this isn’t the best way to deal with attacks. A smart attacker could forge packets from legitimate and important systems and cut you completely off from the net; therefore, it would be better to rewrite the attack packets in such a way that they cannot do any damage anymore or to at least protect certain IPs from being blacklisted.

Honeypots

A honeypot is a simulated server or whole simulated network of easy-to-crack services. Depending on its purpose, it is used to keep script kiddies and crackers away from production systems, to have a pre-alert system, and to log and analyze new cracking techniques, viruses, worm codes, and more.

Last but not least, the most important component: a continuous system upgrade and patch workflow! Without current security updates, you will never get security at all. A firewall consists of software like a normal desktop computer.

Man-in-the-Middle Attacks (MiTM)

Man-in-the-Middle attacks (MiTM attacks for short) behave like a proxy but on an unintentional basis. Some individuals consider transparent proxies of ISPs a Man-in-the-Middle attack.

All MiTM attacks have in common to partly or entirely redirect the traffic of a victim to themselves and afterwards forward it to the real destination. This can be realized through different techniques such as _**ARP Cache Poisoning**_, _**DNS-Spoofing**_, or _**ICMP Redirection**_. Not only can an attacker steal the complete traffic, including sensitive data like usernames and passwords, but also drop connections at will and manipulate content to fool the victim.
