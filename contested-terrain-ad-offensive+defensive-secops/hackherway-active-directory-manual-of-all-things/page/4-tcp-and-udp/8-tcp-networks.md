# 8 TCP Networks

8\. TCP Networks

**— 8 —**\
**TCP/IP and Networks**

In the previous seven days you have seen TCP/IP and its associated protocols covered in considerable depth. It is now time to begin looking at TCP/IP in a broader sense. Today you learn how TCP/IP can operate with other protocols in a networked system. You also learn about protocols that don't use TCP/IP but are commonly encountered.

It is useful to understand how TCP/IP operates in conjunction with other protocols so that the management of TCP/IP is clearer (you learn about managing a TCP/IP network in the next few days). You might find that some material today is repeated from earlier days, or rephrased slightly to present a different approach to the subject. In a sense, today acts as a summary, albeit incomplete, of the TCP/IP system as a whole.

To round out the day, I look at the miscellaneous optional services provided through TCP/IP. Most are dedicated to a simple task, but they do serve their purpose well and use TCP/IP, hence their inclusion here.

**TCP/IP and Other Protocols**

TCP/IP is not often found as a sole protocol. It is usually one of several protocols used in any given network. Therefore, the interactions between TCP/IP (and its associated protocols) and the other protocols that might be working with it must be understood. It is easiest to begin looking at this subject from a local area network point of view and then expand that view to cover internetworks.

The layers of a TCP/IP protocol, as well as most other OSI-model protocols, are designed to be independent of each other, enabling mixing of protocols. When a message is to be sent over the network to a remote machine, each protocol layer builds on the packet of information sent from the layer above, adding its own header and then passing the packet to the next lower layer. After being received over the network (packaged in whatever network format is required), the receiving machine passes the packet back up the layers, removing the header information one layer at a time.

Replacing any layer in the protocol stack requires that the new protocols can internetwork with the other layers, as well as perform all the required functions of that layer (for example, duplicating the services of the replaced protocol). Also, performing duplicate operations in more than one layer (redundant operations) should be avoided for obvious reasons.

To examine the internetworking of the layers and the substitution or addition of others, a simple installation can be used as a starting point. Figure 8.1 shows a simple layered architecture using TCP and IP with the Ethernet network. Figure 8.1 also shows the assembly of Ethernet packets as they pass from layer to layer.

[**Figure 8.1. A simple layered architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt01.gif)

As you saw earlier in this guide, the process begins with a message of some form from an Upper Layer Protocol (ULP) which itself is passing a message from an application. As the message is passed to TCP, it adds its own header information and passes to the IP layer, which does the same. When the IP message is passed to the Ethernet layer, Ethernet adds its own information at the front and back of the message and sends the message out over the network.

\
![](<../../.gitbook/assets/0 (5).gif>)The operating system itself is not a single layer but runs throughout the entire layered architecture with connections to each layer. The interfaces between the each layer's protocols differ depending on the host machine, but it is convenient to ignore the operating system's influence for simplicity.

Although this simple model might seem ideal, in practice it has a few problems. Most importantly, it requires IP to interface directly with the Ethernet layer. This interface is not a clean one; it has many connections that break from the ideal layered architecture.

**LAN Layers**

To expand on the layered system requires a better understanding of the interfaces to the network layer in a LAN. Figure 8.2 shows an expanded layer architecture for a LAN. This type of architecture applies for collision sense multiple access (CSMA) and collision detect (CD) networks such as Ethernet.

[**Figure 8.2. Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt02.gif)

The LAN involves some additional layers. The Logical Link Control (LLC) layer is an interface between the IP layer and the network layers. There are several kinds of LLC configurations, but it is sufficient at this point to know its basic role as a buffer between the network and IP layers either as a simple system for a connectionless service or as an elaborate system for a connection-based service. LLC is usually used with the High-Level Data Link Control (HDLC) link standard. For connectionless service, this uses an _unnumbered information_ (UI) message frame, whereas connection-based services can use the _asynchronous balanced mode_ (ABM) message frame, both supported by HDLC. The configuration of LLC with respect to TCP/IP is important.

The Media Access Control (MAC) layer was mentioned briefly on Day 2, "TCP/IP and the Internet." MAC is responsible for managing traffic on the network, such as collision detection and transmission times. It also handles timers and retransmission functions. MAC is independent of the network medium but is dependent on the protocol used on the network.

The physical layer in the Network architecture is composed of several services. The Attachment Unit Interface (AUI) provides an attachment between the machine's physical layer and the network medium. Typically, the AUI is where the network ports or jacks are located.

The Medium Attachment Unit (MAU) is composed of two parts: the Physical Medium Attachment (PMA) and the Medium Dependent Interface (MDI), both of which can be considered as separate parts as shown in the figure. The MAU is responsible for managing the connection of the machine to the LAN medium itself, as well as providing basic data integrity checking and network medium monitoring. The MAU has functions that check the signal quality from the network and test routines for verifying the network's correct operation.

When these layers are added to the layered architecture for a protocol stack, the IP-Ethernet layer is separated. This is shown in Figure 8.3. This type of configuration is more common than the one shown in Figure 8.1 and is usually called the IP/802 configuration (because Ethernet is defined by the IEEE 802 specification).

[**Figure 8.3. TCP/IP with LLC/MAC.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt03.gif)

The IP/802 LAN can be connectionless using a simple form of LLC called LLC Type 1, which supports unnumbered information (UI). The LLC and MAC layers help separate IP from the physical layer. More headers are added to the message packet, but these have useful information. The LLC header has both source and destination service access points (SAP) in it to identify the layers above.

UDP is frequently used instead of TCP in this type of network. UDP is not as complex as TCP, so the entire network's complexity is reduced. However, UDP has no message integrity functionality built in, so a different form of LLC (called LLC Type 2) is used that implements these functions. LLC Type 2 provides the data integrity functionality that TCP usually provides, such as sequencing, transfer window management, and flow control. The disadvantage is that these functions are now below the IP layer, instead of above it. In case of fatal problems with the LLC layer, this can result in problems that must be dealt with in the application layer itself.

\
![](<../../.gitbook/assets/1 (4).gif>)The differences between TCP and LLC Type 1 versus UDP and LLC Type 2 must be carefully weighed by a system administrator. The TCP/LLC 1 combination is more complex than UDP/LLC 2 but offers excellent reliability and integrity, whereas UDP/LLC 2 is better for high-throughput networks. In some cases, UDP/LLC 2 results in duplicated functions, because the LLC versions differ considerably among vendors.

**NetBIOS and TCP/IP**

A popular PC-oriented network operating system is NetBIOS, which can be cleanly integrated with TCP/IP. Figure 8.4 shows the network architecture for this kind of LAN. NetBIOS resides above the TCP or UDP protocol, although it usually has solid links into that layer (so the two layers cannot be cleanly separated). NetBIOS acts to connect applications together in the upper layers, providing messaging and resource allocation.

[**Figure 8.4. The NetBIOS Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt04.gif)

Three Internet port numbers are allocated for NetBIOS. These are for the NetBIOS name service (port 137), datagram service (port 138), and session service (port 139). There is also the provision for a mapping between Internet's Domain Name Service (DNS) and the NetBIOS Name Server (NBNS). (DNS is covered in detail on Day 11, "Domain Name Service.") The NetBIOS Name Server is used to identify PCs that operate in a NetBIOS area. In the interface between NetBIOS and TCP, a mapping between the names is used to produce the DNS name.

IP can be configured to run above NetBIOS, eliminating TCP or UDP entirely and running NetBIOS as a connectionless service. In this case, NetBIOS takes over the functions of the TCP/UDP layer, and the upper layer protocols must have the data integrity, packet sequencing, and flow control functions. This is shown in Figure 8.5. In this architecture, NetBIOS encapsulates IP datagrams. Strong mapping between IP and NetBIOS is necessary so that NetBIOS packets reflect IP addresses. (To do this, NetBIOS codes the names as IP._nnn_._nnn_._nnn_._nnn_.)

[**Figure 8.5. Running IP above NetBIOS.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt05.gif)

This type of network requires that the upper layer protocols (ULPs) handle all the necessary features of the TCP protocol, but the advantage is that the network architecture is simple and efficient. For some networks, this type of approach is well suited, although the development of suitable ULPs can be problematic at times.

**XNS and TCP/IP**

The Xerox Network System (XNS) was widely used in the past and still retains a reasonable percentage of network use. XNS is popular because Xerox released the code to the public domain, hence making it a cost-effective network system. In most cases, XNS protocols were designed to work with Xerox's Ethernet, as well. XNS now appears in several commercial network software packages.

XNS can use IP, as shown in Figure 8.6. The Sequenced Packet Protocol (SPP) is above the IP layer, providing some TCP function, although it is not as complete a protocol. In the ULP layer is the Courier protocol, which provides presentation and session layer services.

[**Figure 8.6. The XNS Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt06.gif)

XNS uses the term _Internet Transport Protocols_ to refer to the set of protocols used, including IP. Among the protocols is the Routing Information Protocol (RIP) and an error protocol similar to the Internet Control Message Protocol (ICMP).

**IPX and UDP**

Novell's NetWare networking product has a protocol similar to IP called the Internet Packet Exchange (IPX), which is based on Xerox's XNS. The IPX architecture is shown in Figure 8.7. IPX usually uses UDP for a connectionless protocol, although TCP can be used when combined with LLC Type 1.

[**Figure 8.7. The IPX Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt07.gif)

The stacking of the layers (with IPX above UDP) ensures that the UDP and IP headers are not affected, with the IPX information encapsulated as part of the usual message process. As with other network protocols, a mapping is necessary between the IP address and the IPX addresses. IPX uses network and host numbers of 4 and 6 bytes, respectively. These are converted as they are passed to UDP.

It is possible to reconfigure the network to use IPX networks by using TCP instead of UDP and substituting the connectionless LLC Type 1 protocol. This results in the architecture shown in Figure 8.8. When using this layer architecture, IP addresses are mapped using ARP.

**ARCnet and TCP/IP**

ARCnet is widely used for LANs and has an Internet RFC for using it with IP. The architecture is similar to that of the IPX-based network but with ARCnet replacing IPX, as shown in Figure 8.9. Messages passed down from IP are encapsulated into ARCnet datagrams.

[**Figure 8.9. The ARCnet-based Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt09.gif)

A special placement of the IP datagram behind the client data area of the ARCnet header ensures that IP compatibility is maintained if the message must pass out of the ARCnet network (through a converter). IP addresses are mapped to ARCnet addresses using ARP. The protocol also supports RARP to some extent.

**FDDI Networks**

The Fiber Distributed Data Interface (FDDI) is an ANSI-defined high-speed network that uses fiber-optic cable as a transport medium. FDDI is gaining string support because of the high throughout that can be achieved. For TCP/IP, FDDI uses a layered architecture like the other networks discussed. FDDI differs slightly from other media in that there are two sublayers for the physical layer.

FDDI's addressing scheme is similar to other Ethernet networks, requiring a simple mapping, as seen with the Ethernet system. IP and ARP can both be used over FDDI. IP is used with the LLC Type 1 connectionless service.

The frame size for FDDI is set to 4,500 bytes, including the header and other framing information. After that is taken into account, there are 4,470 bytes available for data. (The Internet RFC for FDDI defines 4,096 bytes for data and 256 bytes for header layers above the MAC layer.) This large packet size can cause problems for some gateways, so routing for FDDI packets must be carefully chosen to prevent truncation or corruption of the packet by a gateway that can't handle the large frame size. In case of doubt, FDDI packets should be reduced in size to 576 data bytes.

**X.25 and IP**

X.25 networks modify the network architecture by using an OSI TP4 layer on top of IP, and the X.25 Packet Layer Procedures (PLP) layer below IP. This is shown in Figure 8.10. TP4 is a TCP-like protocol that does not use port identifiers. The destination and source fields in the header are the _transport service access points_ (TSAPs). TP4 is more complex than TCP, which sometimes works against it.

[**Figure 8.10. The X.25-based Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt10.gif)

X.25 is not often used on a LAN, but it is used as a connection to a packet-switched network. An Internet RFC defines the rules for X.25 IP-based packet switching, including the limits for IP datagram sizes (576 bytes) and virtual circuits.

**ISDN and TCP/IP**

The Integrated Services Digital Network (ISDN) provides packet-switched TCP/IP networks. The architecture is shown in Figure 8.11. IP is not in the stack because it is usually incorporated into CLNP. (Both TCP and IP can be used with ISDN instead of OSI TP4 and CLNP, but the ISDN versions are optimized for that network.)

[**Figure 8.11. The ISDN-based Network architecture.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt11.gif)

ISDN uses a more complex architecture than most networks, replacing gateways and routers with _terminal adapters_ and _ISDN nodes._ These perform the equivalent functions but have a more rigid (and complex) internal architecture. The details are not relevant here, so the interested reader is referred to a good ISDN guide.

**Switched Multi-Megabit Data Services and IP**

The Switched Multi-Megabit Data Services (SMDS) system is a public packet-switched connectionless service that provides high throughput with large packet sizes (up to 9188 data bytes). SMDS uses a subscriber-to-network and network-to-subscriber access mechanism for flow control. SMDS works with IP by interfacing the SMDS to the LLC layer.

SMDS using IP supports multiple logical IP subnetworks (LISs), which can be managed separately but treated as a single unit by SMDS. This method requires all the subnetworks to have to same IP address. The architecture of the SMDS layers is quite complex, so they are not covered in detail here. SMDS uses LLC Type 1 frames.

**Asynchronous Transfer Mode (ATM) and BISDN**

Two new protocols for high-speed internetworks that are becoming popular are Asynchronous Transfer Mode (ATM) and Broadband ISDN (BISDN). The architecture on the user's machine is similar to the TCP/IP architectures discussed earlier, although additional layers can be added to provide new services, such as video and sound capabilities.

The router, gateway, or other device that accesses the high-speed network is more complex as well. Called a _terminal adapter_ (as with ISDN), it provides a sophisticated interface between user layers and adaptation layers, which are application-specific. From the terminal adapter, traffic is passed to the ATM service, which provides switching and multiplexing services.

**Windows 95 and TCP/IP**

Because Windows 95 is supposed to become the dominant operating system on PC machines running a DOS or Windows operating system, it is worth taking a quick look at how Windows 95 integrates networking software into its kernel. The approach used by Windows 95 is similar to that of Windows NT and OS/2, so the knowledge is useful for many operating systems on common client devices in today's LANs.

Windows 95 refines the network architecture used in Windows for Workgroups and Windows NT, resulting in better performance and reliability, as well as catering to the demands of different network requirements such as multiple protocol support. Because Windows 95 supports many different network protocols in 16- and 32-bit Virtual Mode Driver (VxD) versions, the architecture must provide the flexibility to accommodate a number of structures.

The Windows 95 architecture is layered; a layered architecture is the most common networking structure (such as OSI and TCP/IP). The network architecture used in Windows 95 is known as Microsoft's Windows Open Services Architecture (WOSA). WOSA was developed to enable applications to work with several different network types, and it includes a set of interfaces designed to enable coexistence of several network components.

The networking software components of Windows 95 are shown in their respective layers in Figure 8.12. Many of the network components are familiar from earlier versions of Windows for Workgroups, Windows NT, or other operating systems and communications protocols. I look at each layer in the Windows 95 architecture in a little more detail so that the function of each component is better understood. Because 32-bit applications are becoming dominant with Windows 95 and Windows NT, I'll look at them in this section. Older 16-bit applications are treated slightly differently, but the principles are the same.

[**Figure 8.12. The Windows 95 networking software architecture showing the components.**](https://www.softlookup.com/tutorial/tcp_ip/08tyt12.gif)

* **API:** The standard Win32 Application Programming Interface (API, the same system used with Windows NT). The API handles remote file operations and remote resources (printers and other devices). The Win32 APIs are used for programming applications.
* **Multiple Provider Router (MPR):** The MPR routes all network operations for Windows 95, as well as implementing network functions common to all network types. Win32 APIs communicate directory with the MPR, although some can be routed straight through. The MPR is a 32-bit protected mode DLL.
* **Network Provider:** The network provider implements the network service provider interface. Only the MPR can communicate with the network provider. The network provider is a 32-bit protected mode DLL.
* **IFS Manager:** The IFS Manager routes filesystem requests to the proper filesystem driver (FSD). The IFS Manager can be called directly by network providers.
* **Network Filesystem Driver (FSD):** The FSD implements the particular remote filesystem characteristics. The FSD can be used by the IFS Manager when the filesystem of the local and remote machines match. The FSD is a 32-bit protected mode VxD (virtual device driver).
* **Network Transport:** The network transport is a VxD that implements the device-specific network transport protocol. Multiple network transports can be active at a time. The network FSD interfaces with the network transport, usually with a one-to-one mapping, although that is not necessarily the case.
* **Network Driver Interface Specification (NDIS):** A vendor-independent software specification that defines interactions between the network transport and device driver. Windows 95 supports both 32-bit and 16-bit NDIS versions.
* **Network Adapter Driver:** The network adapter driver VxD controls the actual network hardware device. NDIS communicates with the driver, which sends packets over the network. Windows 95 uses Media Access Control (MAC) drivers.

One of the key features of Windows 95 is the inclusion of support for multiple concurrent protocols. The default protocol is NetWare's IPX/SPX. Also included are NetBIOS and NetBEUI drivers, and a complete 32-bit VxD for TCP/IP. All these drivers are plug-and-play enabled, allowing dynamic loading and unloading.

Windows 95's support for multiple protocols is achieved through the Network Driver Interface Specification (NDIS), which is a superset of the NDIS used in Windows for Workgroups and Windows NT. The NDIS 3.1 driver has three parts: the protocol itself (which can be implemented by third-party vendors) and protocol manager, the MAC or mini-port, and the mini-port wrapper. The NDIS protocol manager loads and unloads protocols as needed.

The version of NDIS included with Windows 95 adds plug-and-play enhancements and new mini-drivers. The plug-and-play capability is added to the protocol manager and the Media Access Control (MAC) layer, letting network drivers load and unload dynamically. The mini-driver (which is compatible with the mini-driver models used in Windows NT 3.5) decreases the amount of code that must be written to support a network adapter.

Windows 95 enables support for many network servers concurrently. This is an improvement over Windows for Workgroups 3.11, which enabled only its own network and one additional network. The server support of Windows 95 is provided by the Network Provider Interface (NPI). Using multiple network protocols at the same time, you can set up a Windows 95 machine to use TCP/IP for UNIX networks, and NetBEUI or IPX/SPX for local PC networks, if you want. Alternatively, as you see on Day 10, "Setting Up a Sample TCP/IP Network: DOS and Windows Clients," you can set Windows 95 to be a pure TCP/IP-based machine.

**Optional TCP/IP Services**

TCP/IP networks offer a number of optional services that users and applications can use. All these optional services have strict definitions for their protocols. These optional services and their assigned port numbers are shown in Table 8.1.<br>

**Table 8.1. Optional TCP/IP services.**

| _**Service**_       | _**Port**_ | _**Description**_                                                 |
| ------------------- | ---------- | ----------------------------------------------------------------- |
| Active Users        | 11         | Returns the names of all users on the remote system               |
| Character Generator | 19         | Returns all printable ASCII characters                            |
| Daytime             | 13         | Returns the date and time, day of the week, and month of the year |
| Discard             | 9          | Discards all received messages                                    |
| Echo                | 7          | Returns any messages                                              |
| Quote of the Day    | 17         | Returns a quotation                                               |
| Time                | 37         | Returns the time since January 1, 1900 (in seconds)               |

**Active Users**

The Active Users service returns a message to the originating user that contains a list of all users currently active on the remote machine. The behavior of the TCP and UDP versions is the same. When requested, the Active Users service monitors port 11 and, upon establishment of a connection, responds with a list of the currently active users and then closes the port. UDP sends a datagram, and TCP uses the connection itself.

**Character Generator**

The Character Generator service is designed to send a set of ASCII characters. Upon receipt of a datagram (the contents of which are ignored), the Character Generator service returns a list of all printable ASCII characters. The behavior of the TCP and UDP versions of the Character Generator are slightly different.

The TCP Character Generator monitors port 19, and upon connection ignores all input and sends a stream of characters back until the connection is broken. The order of characters is fixed. The UDP Character Generator service monitors port 19 for an incoming datagram (remember, UDP doesn't create connections) and responds with a datagram containing a random number of characters. Up to 512 characters can be sent.

Although this service might seem useless, it does have diagnostic purposes. It can ensure that a network can transfer all 95 printable ASCII characters properly, and it can also be used to test printers for their capability to print all the characters.

**Daytime**

The Daytime service returns a message with the current date and time. The format it uses is the day of the week, month of the year, day of the month, time, and the year. Time is specified in a _HH_:_MM_:_SS_ format. Each field is separated by spaces to enable parsing of the contents.

Both TCP and UDP versions monitor port 13 and, upon receipt of a datagram, return the message. The Daytime service can be used for several purposes, including setting system calendars and clocks to minimize variations. It also can be used by applications.

**Discard**

The Discard service simply discards everything it receives. TCP waits for a connection on port 9, whereas UDP receives datagrams through that port. Anything incoming is ignored. No responses are sent.

The Discard service might seem pointless, but it can be useful for routing test messages during system setup and configuration. It can also be used by applications in place of a discard service of the operating system (such as /dev/null in UNIX).

**Echo**

The Echo service returns whatever it receives. It is called through port 7. With TCP, it simply returns whatever data comes down the connection, whereas UDP returns an identical datagram (except for the source and destination addresses). The echoes continue until the port connection is broken or no datagrams are received.

The Echo service provides very good diagnostics about the proper functioning of the network and the protocols themselves. The reliability of transmissions can be tested this way, too. Turnaround time from sending to receiving the echo provides useful measurements of response times and latency within the network.

**Quote of the Day**

The Quote of the Day service does as its name implies. It returns a quotation from a file of quotes, randomly selecting one a day when a request arrives on port 17. If a source file of quotations is not available, the service fails.

**Time**

The Time service returns the number of seconds that have elapsed since January 1, 1990. Port 37 is used to listed for a request (TCP) or receive an incoming datagram (UDP). When a request is received, the time is sent as a 32-bit binary number. It is up to the receiving application to convert the number to a useful figure.

The Time service is often used for synchronizing network machines or for setting clocks within an application.

**Using the Optional Services**

As already mentioned, the optional services can be accessed from an application. Users can directly access their service of choice (assuming it is supported) by using Telnet. A simple example is shown here:

$ telnet merlin 7

Trying...

Connected to merlin.tpci.com

Escape character is '^T'.

This is a message

This is a message

Isn't this exciting?

Isn't this exciting?

\<Ctrl+T>

$ telnet merlin 13

Trying...

Connected to merlin.tpci.com

Escape character is '^T'.

Tues Jun 21 10:16:45 1994

Connection closed.

$ telnet merlin 19

!"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefg

"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefgh

\#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefghi

$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefghij

%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefghijk

&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefghijkl

'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\[\\]^\_abcdefghijklm

\<Ctrl+T>

$

In this example, a connection to port 7 starts an Echo session. Everything typed by the user is echoed back immediately, unchanged. Then a connection to port 13 provides the Daytime service, showing the current date and time. The connection is broken by the service once the data is sent. Finally, the Character Generator is started. Both the Echo and Character Generator services were terminated with the Telnet break sequence of Ctrl+T.

**Summary**

I covered a lot of material in this chapter, mostly about the way TCP/IP can interact with other networking systems and protocols. By combining TCP/IP with existing networks, the advantages of both can be gained, as well as offering compatibility with a wide range of TCP-based devices.

I have also looked at several protocols that round out the TCP/IP family. These are mostly basic services, but they are essential to the proper operation of a TCP/IP-based network.

**Q\&A**

**What is the role of the Media Access Control (MAC) layer in a network architecture?**

The MAC layer handles traffic for the network, including collisions and timers. The MAC is independent of the network's physical medium, but its exact role and implementation depend on the network protocols.

**What is the difference between LLC Type 1 and LLC Type 2?**

Logical Link Control (LLC) Type 1 is a simpler form that supports unnumbered information, designed for TCP. LLC Type 2 is for UDP and offers message integrity functionality.

**What is XNS?**

XNS is the Xerox Network System, a networking design that Xerox released to the public domain. Because XNS is essentially free, it has gained a lot of support. XNS supports Ethernet.

**What is ISDN?**

The Integrated Services Digital Network is a packet-switched high-speed network that supports broadband (many channel) communications.

**Why is a simple network protocol like the Character Generator supported?**

As simple as it may be, the Character Generator protocol (and many others like it) is used for basic tasks and queries that would require much more complex coding and operations when performed as part of a larger protocol. The Character Generator protocol is useful for testing communications. It is small, fast, easy to implement, and easy to understand.

**Quiz**

1. What components make up a Medium Attachment Unit (MAU) and what are their roles?
2. What is FDDI? Why is it popular?
3. What is the role of the Discard service?
4. The Time protocol is often used by network devices. What is its role?
5. Does the presence of a second network protocol (like IPX) affect the basic TCP/IP protocol suite's operations?
