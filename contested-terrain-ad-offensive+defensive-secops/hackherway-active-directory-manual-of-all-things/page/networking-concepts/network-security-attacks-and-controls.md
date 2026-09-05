# Network Security: Attacks and Controls

Chapter Overview

With the rapid growth of the Internet, network security has become an essential aspect of computer and information security. To develop effective security measures, it is crucial to understand the vulnerabilities present in computer networks and the typical attacks that exploit these weaknesses. The first half of this section will introduce you to classical network attacks that have historically exploited common network vulnerabilities and the solutions that have been implemented to prevent or mitigate these attacks. The second half will cover various network security controls, including network architecture, protocols, standards, and software/hardware tools used in modern computer networks.

### introduction to computer networks

As the Internet has expanded, network security has become an integral part of ensuring the safety and integrity of computer systems and information. Network security encompasses measures taken to protect the resources and integrity of computer networks. This section provides an overview of computer networks and the Internet to establish a foundation for understanding network security.

### ISO-OSI Reference Model

The communication problem in computer networks involves transferring data from an application user on one system to an application user on another system through one or more intermediate networks. This problem is addressed using a layered approach through a collection of protocols known as the protocol suite. Each layer addresses a specific aspect of the communications program, and together, they solve the entire communication process. The Open Systems Interconnection (OSI) reference model is an abstract representation of the basic layers involved in solving the communications problem, from top to bottom:

* **Application Layer –** Layer 7
* **Presentation Layer –** Layer 6
* **Session Layer –** Layer 5
* **Transport Layer –** Layer 4
* **Network Layer –** Layer 3
* **Data Link Layer –** Layer 2
* **Physical Layer –** Layer 1

#### Application Layer

Specifies how a particular application uses the network and contacts the application program running on a remote machine.

#### Presentation Layer

Handles the translation and representation of data at the two endpoints of communication.

#### Session Layer

Establishes communications sessions with remote systems and handles security issues such as password authentication before connecting.

#### Transport Layer – OSI Layer 4

Layer 4 is the Transport Layer. This layer provides end-to-end, reliable or best-effort, in-order data packet delivery, along with support for flow control and congestion control. In this layer, we dive into the nitty-gritty specifics of the connection between two nodes and how information is transmitted between them. It builds on the functions of Layer 2, such as line discipline, flow control, and error control.

This layer is also responsible for data packet segmentation, or how data packets are broken up and sent over the network.

Unlike the previous layer, Layer 4 also understands the whole message, not just the contents of each individual data packet. With this understanding, Layer 4 can manage network congestion by not sending all the packets at once.

The data units of Layer 4 go by a few names. For TCP, the data unit is a _packet._ For UDP, a packet is referred to as a _datagram._ I’ll just use the term _data packet_ here for brevity and simplicity.

Transmission Control Protocol (TCP) and User Datagram Protocol (UDP)

TCP and UDP are two of the most well-known protocols in Layer 4.

* **TCP (Transmission Control Protocol)**

A connection-oriented protocol that prioritizes data quality over speed. TCP explicitly establishes a connection with the destination node and requires a handshake between the source and destination nodes when data is transmitted. The handshake confirms that data was received. If the destination node does not receive all the data, TCP will ask for a retry. TCP also ensures that packets are delivered or reassembled in the correct order.<br>

* **UDP (User Datagram Protocol)**

A connectionless protocol that prioritizes speed over data quality. UDP does not require a handshake, which is why it is called connectionless. Because UDP doesn’t have to wait for this acknowledgement, it can send data at a faster rate, but not all the data may be successfully transmitted, and we’d never know. If information is split up into multiple datagrams, unless those datagrams contain a sequence number, UDP does not ensure that packets are reassembled in the correct order.

Troubleshooting OSI Layer 4 Problems

Below are some Layer 4 problems to be aware of:

* All the problems that can crop up on previous layers
* Blocked ports – check your Access Control Lists (ACLs) and firewalls
* Quality of Service (QoS) settings: QoS is a feature of routers/switches that can prioritize traffic, and they can really fuck things up, as well.

TL;DR

The Transport Layer provides end-to-end transmissions of messages by segmenting messages into multiple data packets; this layer supports connection-oriented and connectionless communications.

#### Network Layer – OSI Layer 3

Layer 3 is the Network Layer. This is where we send information between and across networks using routers. Instead of just node-to-node communications, we can now achieve network-to-network communications. In addition, the Network layer is also responsible for forwarding data packets from the source to the destination nodes of communication.

Routers are the workhorse of Layer 3 – we couldn’t have Layer 3 without them. They move data packets across multiple networks.

Not only do routers connect to Internet Service Providers (ISPs) to provide access to the Internet, but they also keep track of what’s on their network (remember that switches keep track of all MAC addresses on a network), what other networks they are connected to, and the different paths for routing data packets across these networks.

Routers store all this addressing and routing information in what’s known as a _routing table._ Below is a simple example of a routing table:

![A routing table showing the destination, subnet mask, and interface](<../../.gitbook/assets/0 (53).png>)

The data unit on Layer 3 is the _data packet._ Typically, each data packet contains a frame plus an IP address information wrapper. In other words, frames are _encapsulated_ by Layer 3 addressing information.

The data being transmitted in a packet is also sometimes called the _payload._ While each packet has everything it needs to get to its destination, whether it makes it is another story.

Layer 3 transmissions are connectionless, or best effort – they do not do anything but send the traffic where it’s supposed to go. More on data transport protocols when we discuss Layer 4.

Once a node is connected to the Internet, it is assigned an Internet Protocol (IP) address, which looks either like 172.16.254.1 (IPv4 address convention) or like 2001:0db8:85a3:0000:0000:8a2e:0370:7334 (IPv6 address convention). Routers use IP addresses in their routing tables.

IP addresses are associated with the physical node’s MAC address via the _Address Resolution Protocol (ARP),_ which resolves MAC addresses with the node’s corresponding IP address.

ARP is conventionally considered part of Layer 2, but since IP addresses don’t exist until Layer 3, it’s also part of Layer 3.

Troubleshooting OSI Layer 3 Problems

Here are some Layer 3 problems to watch out for:

* All the problems that can crop up on previous layers 😊
* Faulty or non-functional routers or nodes
* Cabling issues
* Incorrectly configured IP address
* BGP (Border Gateway Protocol) Hijack or rewrite of routing table

Many answers to Layer 3 questions will require the use of command-line tools like ping, trace, show ip route (or sh ip route), or show ip protocols (or sh ip proto).

TL;DR

The Network Layer allows nodes to connect to the Internet and send information across different networks.

#### Data Link Layer – OSI Layer 2

Layer 2, the Data Link layer, defines how data is formatted for transmission, regulates data flow between nodes, and addresses error detection during this process. The Data Link layer is also responsible for organizing data into frames and ensuring reliable data delivery over the physical medium.

In more technical terms:

* **Line Discipline:** Determines who can transmit data, for how long, and manages the timing of data transmissions.<br>
* **Flow Control:** Manages the amount of data that can be transmitted to ensure smooth communications.<br>
* **Error Control (Detection and Correction):** Identifies errors in data transmissions caused by factors like electrical interference or hardware issues. While Layer 2 primarily focuses on error detection, correction often occurs at higher layers of the OSI stack.

The Data Link layer of the OSI model is divided into two sublayers: _Media Access Control (MAC)_ sublayer and the _Logical Link Control (LLC)_ sublayer. Each of these sublayers has specific functions that contribute to the overall operation of the Data Link layer.

‣ Media Access Control (MAC) Sublayer

The MAC sublayer is responsible for controlling how devices on a network gain access to the medium and permission to transmit data. Here are its primary functions:

1. **Frame Delimiting and Recognition:** It defines the frame boundaries and recognizes frame start and end points. This ensures that the data sent and received is properly encapsulated in frames.<br>
2. **Addressing:** It manages MAC addresses, which are unique identifiers assigned to network interfaces for communications on the physical network segment. Each device on a network segment must have a unique MAC address.<br>
3. **Access Control:** This determines which device on the network is allowed to access the medium at any given time. This is crucial in environments where multiple devices might try to send data simultaneously. Different MAC protocols, like _Carrier Sense Multiple Access with Collision Detection (CSMA/CD)_ used in Ethernet networks, manage this access.<br>
4. **Error Handling:** It detects errors in frames through mechanisms like _Cyclic Redundancy Check (CRC)_; however, it does not correct these errors; it simply discards the erroneous frames.<br>
5. **MAC Addressing Assignment:** The MAC sublayer handles the assignment of hardware identification numbers known as MAC (Media Access Control) addresses, which uniquely identify each device on a network due to its unique MAC addresses burned into the firmware of a device’s NIC.<br>
6. **MAC Recognition:** MAC addresses are assigned during manufacturing and are typically recognized automatically by networks.<br>
7. **MACs and NICs:** MAC addresses, as stated previously, are associated with Network Interface Cards (NICs), and switches track all MAC addresses on a network.

‣ _Logical Link Control (LLC) Sublayer_

The LLC sublayer provides an interface between the MAC sublayer and the Network layer. Its main responsibilities include:

1. **Multiplexing:** It allows multiple network protocols to coexist within a multipoint network and to be transmitted over the same network medium. This means it can handle different types of traffic and pass it to the appropriate protocol in the Network layer.
2. **Flow Control:** It manages data flow to ensure that the sending and receiving devices can operate at optimal speeds without overwhelming each other. This is particularly important in preventing data overflow and loss.
3. **Error Checking and Correction:** Unlike the MAC sublayer, the LLC sublayer can provide error checking and correction capabilities. It ensures that the data received is accurate and can request retransmission if errors are detected.
4. **Frame Sequencing:** It manages the sequence of frames to ensure that data is delivered in the correct order. This is particularly important in network protocols that require ordered data delivery.
5. **Packet Management:** Manages framing, addressing, and flow control.<br>
6. **Communications Links:** The speed and method of communication depend on the type of link between nodes, such as Ethernet or WiFi.<br>
7. **Data Unit Components:** The data unit at Layer 2 is a frame, which consists of a header, body, and trailer:<br>
   1. **Header:** Includes MAC addresses for the source and destination nodes.<br>
   2. **Body:** Contains the actual data being transmitted.<br>
   3. **Trailer:** Contains error detection information. When errors are detected, frames might be discarded, or the error might be reported to higher layers for correction. Common error detection mechanisms include _Cyclic Redundancy Check (CRC)_ and _Frame Check Sequence (FCS)_.

![Example of frames, the network layer, and the physical layer](<../../.gitbook/assets/1 (40).png>)

Typically, there is a maximum frame size limit called the Maximum Transmission Unit (MTU). Jumbo frames exceed the standard MTU.

Furthermore, in dividing the responsibilities between the MAC and LLC sublayers, the Data Link layer can more effectively manage and control the physical transmission of data, ensuring efficient, reliable, and error-free communications across network mediums.

Troubleshooting OSI Layer 2 Problems

Here are some common Layer 2 problems to keep a look out for:

* Issues that can occur on Layer 1<br>
* Unsuccessful connections (sessions) between two nodes
* Sessions that are successfully established but intermittently fail
* Frame collisions

The Data Link Layer allows nodes to communicate with each other within a Local Area Network (LAN). It establishes the foundations of line discipline, flow control, and error control.

TL;DR

The Data Link Layer enables communication between nodes within a Local Area Network (LAN). It establishes line discipline, flow control, and error detection. Common issues include unsuccessful or intermittent connections and frame collisions.

#### Physical Layer – OSI Layer 1

Layer 1 of the OSI model, known as the Physical Layer, encompasses a vast array of technologies essential for establishing and maintaining connections between network devices. This includes physical network devices, cabling, and the mechanisms through which cables are connected to these devices. Additionally, Layer 1 addresses scenarios where traditional cabling is not required, such as wireless broadband technologies.

To avoid overwhelming detail, this overview categorizes Layer 1 technologies into broader classifications, encouraging further exploration within each category:

* **Encoding/Decoding Schemes:** Provides the encoding/decoding schemes and modulation/demodulation schemes for the actual transmission of data over the physical medium as a sequence of bits (1s and 0s).
* **Nodes and Networking Hardware Components:** Includes devices like hubs, computers, and printers, along with internal hardware components including antennas, amplifiers, and Network Interface Cards (NICs).
* **Device Interface Mechanics:** Focuses on the connection points between cables and devices, detailing connector sizes, shapes, pin counts, and activation states.
* **Functional and Procedural Logic:** Explains the roles of each connector pin in sending or receiving signals and the procedures governing communication initiation between nodes on Layer 2.
* **Cabling Protocols and Specifications:** Covers various standards such as Ethernet (CAT), USB, DSL, specifying parameters like maximum cable lengths, modulation techniques, and synchronization methods.<br>
* **Cable Types:** Discusses options ranging from shielded or unshielded twisted pair to coaxial cables, emphasizing the importance of understanding different cable characteristics.
* **Signal Type:** Differentiates between baseband (single bit stream at a time) and broadband (multiple bit streams simultaneously transmissions).<br>
* **Signal Transmission Method:** Includes wired (electrical, optical) and wireless (radio waves, Bluetooth) options, considering factors like frequency bands (e.g., 2.5 GHz vs. 5 GHz) and voltage levels for cabled connections.

Key Concepts

* **Data Unit on Layer 1:** The basic unit of transmittable digital information is the bit, which is binary (0 or 1). Groups of 8 bits form bytes, representing characters such as letters, numerals, or symbols.
* **Bit Synchronization:** Ensures consistency in the number of bits sent and received over specific intervals, crucial for effective communications.
* **Transmission Modes:** Nodes can operate in simplex (send-only or receive-only), duplex (send and receive), or full-duplex modes, depending on their capabilities.

Troubleshooting Layer 1 Issues

Troubleshooting Layer 1 involves identifying and resolving common problems such as defunct cables (damaged wires or connectors), malfunctioning hardware devices, and disconnected devices. Addressing issues at this level is critical, as failure in Layer 1 can prevent proper functioning beyond this layer.

TL;DR

Layer 1 plays a fundamental role in network communications by defining physical aspects necessary for connecting devices. It encompasses a wide range of technologies and standards, from the materials used in cabling to the electrical and mechanical specifications of connectors and devices. Understanding Layer 1 is essential for anyone involved in network design, maintenance, or troubleshooting.

![](<../../.gitbook/assets/2 (35).png>)

Understanding these layers and their functions is crucial for comprehending network security principles and practices, as each layer presents unique security challenges and solutions.

![What is OSI Model | 7 Layers Explained | Imperva](<../../.gitbook/assets/3 (5).jpeg>)\
_**FIGURE X:** OSI Model vs. TCP/IP Model vs. TCP/IP Protocol Suite._

### TCP/IP Protocol Suite

The TCP/IP model stands for _Transmission Control Protocol/Internet Protocol (TCP/IP)._ The TCP/IP protocol stack is a comprehensive suite of communications protocols that empower the internet and the networking world as we know it today. This stack is the lifeblood of modern digital communications and is the most used model for wide area communications, ensuring that data packets are transmitted across diverse and geographically dispersed networks reliably and efficiently.

#### The Four Layers of the TCP/IP Protocol Stack

At the heart of the TCP/IP protocol stack are four distinct layers, each with a unique role in handling data. The four layers include:

* Link Layer
* Internet Layer
* Transport Layer
* Application Layer

#### Link Layer

The Link layer is the foundational layer that deals with the physical network connection between devices. It’s responsible for the actual transmission of data over the network hardware. The Link layer of the TCP/IP model combines the functionalities of the Data Link layer and Physical layer of the OSI model. The Link layer supports the organization of data into frames and their encoding/decoding mechanisms. The structure and retransmission of the frames depends on the topology and hardware technology (like Ethernet, Token Ring, and X.25) used for the network. A data packet is referred to as a _segment_, _datagram,_ and _frame_ at the Transport, Internet, and Link layers, respectively.

#### Internet Layer

The second layer, the Internet layer, takes care of logical addressing and routing. It ensures that data packets find their way across complex networks to reach the correct destination.

#### Transport Layer

Here, the focus is on reliable data transfer. Protocols like TCP ensure that the data reaches its destination in the right order and without errors. The Transport layer of the TCP/IP model is like the Transport layer of the OSI model.

#### Application Layer

The topmost layer, the Application layer, is where user-interface applications come into play. It facilitates the interactions between software applications and the lower layers of the TCP/IP stack. The Application layer of the TCP/IP model oversees the responsibilities of the Application, Presentation, and Session layers of the OSI model.

### The Significance of TCP/IP in Computer Networking

The TCP/IP protocol stack is not just a set of rules; it’s the framework that dictates how data is exchanged over the internet. Without it, the seamless connectivity and communication we enjoy across various devices and platforms would not be possible. This fundamental protocol suite serves as the foundation of the modern Internet and computer networking, and its significance lies in several key aspects, including:

1. **Standardization:** TCP/IP standardizes how data packets should be transmitted, routed, and received across networks. This standardization allows different types of devices and systems to communicate with each other seamlessly.
2. **Reliability:** TCP/IP ensures reliable and orderly delivery of data packets from a source to a destination. Because TCP is a connection-oriented protocol, it guarantees and provides error-checking and retransmission mechanisms to ensure that data arrives intact and in the correct order.
3. **Scalability:** TCP/IP’s hierarchical structure allows for the creation of large, complex networks like the Internet. It can handle a vast number of devices and users, making it scalable for both small local networks and the global Internet.
4. **Interoperability:** TCP/IP enables devices and networks from different vendors to communicate with each other. This interoperability is crucial for widespread adoption and growth of the Internet and interconnected networks.
5. **Versatility:** TCP/IP supports a variety of applications and services on the Internet, including email, web browsing, file transfer, and streaming media, to name a few. Its versatility makes it suitable for a wide range of use cases.
6. **Flexibility:** TCP/IP is adaptable and can work over various types of networking technologies, including wired and wireless networks and connections. It can handle different network topologies and is agnostic to the underlying physical infrastructure.
7. **Security:** While not inherently secure, TCP/IP protocols can be implemented with additional security measures such as encryption, VPNs, firewalls, and intrusion detection systems to enhance network security and protect data during transmission.
8. **Global Connectivity:** TCP/IP’s universality and widespread adoption have facilitated global connectivity, enabling people, devices, and systems worldwide to communicate and access information across the Internet.

In essence, TCP/IP is a crucial component of computer networking as it provides the essential framework for communications, data exchanges, and the functioning of the Internet. Its reliability, scalability, and interoperability have made it a foundational technology in today’s modern computing and networking systems.

### TCP Connection Establishment

The two most used transport layer protocols dominate the TCP/IP protocol suite: _Transmission Control Protocol (TCP)_ and the _User Datagram Protocol (UDP)._ TCP stands out as a **connection-oriented** protocol that operates on a byte-stream basis, ensuring reliable and sequential data delivery. On the other hand, UDP operates without establishing a connection, functioning on a message-based approach and offering only a best-effort service for delivering data from one end to another; therefore, it is known as a **connectionless** protocol.

For processes utilizing TCP, a pivotal step before any data exchange is the establishment of a connection. This phase involves a mutual exchange of information regarding the capabilities and resources each host possesses, setting the stage for the upcoming communications session. Such an exchange is crucial as it allows the TCP process on one host to tailor its data transmission rate in alignment with the available resources, such as memory buffer space, on the receiving host’s side.

To circumvent replay errors, both processes select an arbitrary initial sequence number for the data packets they dispatch. Each byte within the data stream is assigned a unique and sequentially increasing number. In TCP parlance, the sequence number attributed to a data packet corresponds to the first byte of data contained within that packet.

The intricacies of the TCP connection-establishment are encapsulated in a mandatory communications establishment process known as the _TCP Three-Way Handshake._ The three-way handshake mechanism is a robust process ensuring reliable session initiation. For instance, consider a process on Host A desiring to commence a session with a counterpart on Host B. It begins by dispatching a Synchronization (SYN) packet to Host B, embedding an initial sequence number, say X. Additionally, the SYN packet carries details about the available memory resources through the _Advertised Window_ field within the TCP header, providing Host B with the necessary information to manage the incoming data effectively. This three-way handshake is the cornerstone of establishing a stable and reliable TCP session, paving the way for the seamless transfer of data across the network.

The TCP three-way handshake is a critical process that establishes a reliable connection between two hosts over a network. After the initial SYN packet is sent by Host A, the process continues as follows:

1. **SYN-ACK:**

Upon receiving the SYN packet, Host B responds with a SYN-ACK (Synchronization Acknowledgement) packet. This packet serves two purposes:

1. It acknowledges the receipt of the initial SYN packet from Host A by including an acknowledgement number (usually the initial sequence number from Host A plus one); and
2. It also contains Host B’s own initial sequence number, setting the stage for the two-way communication.
3. **ACK:**

To complete the handshake, Host A sends an ACK (Acknowledgement) packet back to Host B. The final step acknowledges the receipt of Host B’s SYN-ACK packet. The acknowledgement number in this packet is the initial sequence number from Host B plus one.

With the exchange of these packets, the connection is established, and both hosts are ready to start the data transfer process. This three-step process ensures that both sides are synchronized and agree on the initial sequence numbers, which are crucial for maintaining the order and integrity of the data packets that will follow.

The three-way handshake is a fundamental component of the TCP protocol, as it sets up a reliable session where both hosts have agreed upon the sequence and acknowledgement numbers, ensuring that each host is ready to send and receive data. This methodical approach is what makes TCP a reliable protocol for transmitting data across networks, where packet loss, duplication, and out-of-order arrival can occur.

### Lost SYN Packets in TCP Three-Way Handshake

The TCP three-way handshake is a cornerstone of network communication, ensuring a reliable connection between two hosts; however, what happens and what do you do if you are in the middle of an ethical hacking security assessment, performing a UDP flood attack, or stress test against a WAF, and suddenly realize a SYN packet is lost during this critical process? Yes, this is possible, and it can happen, and it’s a total pain in the ass to deal with, but nonetheless, should this ever happen to you read on to learn about the mechanisms that TCP employs and what you can do to handle such situations.

When a SYN packet is sent from one host to another, it’s expected that the receiving host will respond with a SYN-ACK packet. If the sending host doesn’t receive this packet, possibly due to it being lost, dropped, discarded, or corrupted, it will not proceed to the next step, and no one passes Go or collects $200. Instead, TCPs built-in mechanisms kick in to recover from this loss.

Thankfully, TCP implements a retransmission timeout (RTO) for SYN packets. If the sender does not receive a SYN-ACK response with a certain time frame, it will retransmit the SYN packet.This timeout period is dynamically calculated based on the network’s current conditions, ensuring that the packet is resent in a timely manner without overwhelming the network.

If the SYN-ACK packet is lost during the handshaking process, the sender of the original SYN will not receive the expected ACK. As a result, the sender’s RTO will expire.

OSI Layer-Related Network Attacks

![Functions and attacks at each layer of OSI model | Download Scientific  Diagram](<../../.gitbook/assets/4 (1).jpeg>)
