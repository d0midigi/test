# Network Scanning

Network Scanning

Introduction to Network Scanning

As an ethical hacker, it is imperative that you possess an in-depth understanding of network protocols such as TCP, UDP, ICMP, and IP before reading this chapter. Once an adversary has identified a target system and does initial reconnaissance, as discussed in the previous chapter on reconnaissance and footprinting, the adversary concentrates efforts on gaining initial access into the target infrastructure. It should be noted that network scanning is not limited to intrusion alone. It can also be an extended form of reconnaissance (if you think about it) where the adversary obtains even more information about the target, such as what operating system is used, the services that are being run on the systems, and whether or not any configuration lapses can be identified. The adversary can then strategize an attack, factoring in these aspects.

Network Scanning Defined

_**Scanning**_ is one of the most important phases of intelligence gathering for an adversary. In the process of scanning, the adversary tries to gather information about the specific IP addresses that can be accessed over the Internet, the target’s operating systems and system architecture, and the services running on each computer identified.

The purpose of scanning is to discover exploitable communications channels, probe as many listeners as possible, and keep track of the ones that are responsive or useful to an adversary’s particular needs. In the network scanning phase of an attack, the adversary tries to find various ways to intrude into a target system. The adversary also tries to discover more about the target system by finding out what operating systems are used, what services are running, and whether there are any configuration lapses in the target system. The adversary then tries to form an attack strategy based on facts learned during the scan. The different types of network scanning are as follows:

* _**Port Scanning:**_ Port scanning is the process of checking the services running on the target computer by sending a sequence of messages to break in. Port scanning involves connecting to TCP and UDP ports on the target system to determine if the services are running or are in a listening state. The listening state gives an idea of the operating system and the applications in use. Sometimes, active services that are listening may allow unauthorized user access to systems that are misconfigured or running software that has vulnerabilities.
* _**Network Scanning:**_ Network scanning is a procedure for identifying active hosts on a network, either to attack them or as a network security assessment.
* _**Vulnerability Scanning:**_ Vulnerability scanning is a method used to check whether a system is exploitable by identifying its vulnerabilities. A vulnerability scanner consists of a scanning engine and a threat and virus database, or catalog. The catalog consists of a list of common files with known vulnerabilities and common exploits for a range of servers. A vulnerability scanner may look for backup files or directory traversal exploits, for example. The scanning engine maintains logic for reading the exploit list, transferring the request to the web server and analyzing the requests to ensure the safety of the server. These tools generally target vulnerabilities that are easily fixed by secure host configurations, updated security patches, and a clean web document.

The access points that a thief who wants to break into a house looks for are the doors and windows. These are usually a house’s points of vulnerabilities because they are easily accessible. When it comes to computer systems and networks, you can think of ports as being the doors and windows of the system that an intruder uses to gain access. A general rule for computer systems is the more open ports there are on a system, the more the system is vulnerable to threats and breach attempts. There are cases, however, where a system has fewer ports open compared to another machine , but the ports that are open present a much higher level of vulnerability.

Objectives of Scanning

The various objectives for which network scanning is carried out are as follows:

* Detect the live systems running on a network.
* Discover which ports are open: based on the open ports, the adversary will determine the best means of entry into the system.
* Discover the operating system of the target system. This is also known as _**“fingerprinting.”**_ The adversary will formulate a strategy based on the operating system’s vulnerabilities.
* Discover the services and versions running/listening on the target system: this gives the adversary an indication of any vulnerabilities (based on the service) that can be exploited to gain access to the target system.
* Discover the IP address of the target system.
* Identify specific applications or versions of a particular service.
* Identify vulnerabilities in any of the systems in the network: this can be useful in taking counteractive measures to secure the systems from being probed by adversaries.

Scanning Methodology

A malicious actor follows a particular sequence of steps to properly scan a network. A generic approach has been presented, so the scanning methods may differ based on the adversary’s specific objectives. The steps involved in network scanning are as follows:

1._Check for live systems:_ An adversary may start with the objective of checking for live systems on the network.

2\. _Check for open ports:_ After the live systems are found, the adversary will look for open ports to determine which services are running on the systems. This can be a vital step, because some services may be of a much higher priority from the adversary’s point of view.

3\. _Fingerprint the operating system:_ The next phase involves fingerprinting the operating system by figuring out the target’s network layout.

4\. _Scan for vulnerabilities:_ Identification of the vulnerabilities in the target’s OS is the next step. The malicious actor may try to exploit these vulnerabilities during an attack.

5\. _Probe the network:_ The malicious actor may also choose to actively probe the network or slightly monitor its traffic. This can be accomplished using proxies (which will be discussed later in the chapter). The technique of anonymous surfing makes it hard to trace this activity back to the malicious actor.

Step 1: Check for Live Systems

_Ping Sweep_

A _**“ping sweep”**_ (also known as an ICMP sweep) is a basic network scanning technique to determine which range of IP addresses map to live hosts (computers). Ping sweeps are conducted using tools such as the one show in the image below. While a single ping will tell the user whether one specified host computer exists on the network, a ping sweep consists of ICMP ECHO request sent to multiple hosts. If a given IP address is live, it will return an ICMP ECHO reply. Ping sweeps are among the oldest and slowest methods to scan a network. This utility, distributed across almost all platforms, acts like a roll call for systems; a system that is active on the network answers to the ping query that another system sends out.

To understand ping better, one should be able to understand the basic construct of the TCP/IP packet. When a system does a ping, a single packet is sent across the network to a specific IP address. This packet contains 64 bytes (56 data bytes and 8 bytes of protocol header information). The sender then waits or listens for a return packet from the target system. If the connections are good and the target computer is “alive,” a good return packet can be expected; however, if there is a disruption in the communications, this will not be the case. Ping also details the number of hops the lie between the two computers and the amount of time it takes for a packet to make the complete trip. This is called the round-trip time. Ping can also be used for resolving host names. In this case, if the packet bounces back when sent to the IP address, but not when sent to the name, then it is an indication that the system is unable to resolve the name to the specific IP address.

_ICMP Scanning_

All required information about a system can be gathered by sending ICMP packets to it, a process known as _**“ICMP Scanning.”**_ Since ICMP does not have port abstraction, this cannot be considered a case of port scanning; however, it is useful to determine what hosts in a network are up by pinging them all. The user can also increase the number of pings in parallel with the -L option. It can also be helpful to tweak the ping timeout value with the -T option. The UNIX tool ICMPquery or ICMPush can be used to request the time on the system (to find out which time zone the system is in) by sending an ICMP type 13 message (TIMESTAMP). The netmask on a particular system can also be determined with ICMP type 17 messages (ADDRESS MARK REQUEST). After finding the netmask of a network card, a user can determine all the subnets in use. After getting knowledge about the subnets, the user can target only one subnet and avoid hitting the broadcast addresses. ICMPquery has both a timestamp and address mask request option.

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/0 (9).gif>)\
_**FIGURE X:** The Infiltrator ping sweep tool._

Step 2: Check for Open Ports

_Three-Way Handshake_

TCP is a **connection-oriented** protocol, which means that connection establishment is performed prior to data transfer between applications. This connection is possible through the process of the three-way handshake. The _**three-way handshake**_, illustrated below, is implemented to establish connection between hosts. The three-way handshake process goes as follows:

1. The source (Computer A) sends a SYN packet to the destination (Computer B) to establish a TCP connection.
2. The destination, upon receiving the SYN packet sent by the source, starts the TCP session by sending a SYN/ACK packet back to the source.
3. This SYN/ACK packet acknowledges the arrival of the first SYN packet to the source.
4. In conclusion, the source sends an ACK packet back thereby providing acknowledgement for the SYN/ACK packet sent by the destination node.

This allows communication between the source and the destination until either of them issues a FIN packet or an RST packet to close the connection.

![TCP 3 Way Handshake In Detail - DEV Community](<../../.gitbook/assets/1 (38).png>)\
_**FIGURE X:** A typical TCP three-way handshake netflow._

_TCP Communication Flags_

Standard TCP communications monitor the TCP packet header that holds the flags. _**TCP communication flags**_ govern the connection between client hosts and give instructions to the system. The flags function as follows:

* **SYN:** Synchronize alias: Initiates connection between to hosts
* **ACK:** Acknowledgement alias: Establishes connection between hosts
* **PSH:** Push alias: System is accepting requests and forwarding buffered data

| **Computer A**   |                            | **Computer B** |
| ---------------- | -------------------------- | -------------- |
|                  |                            |                |
| 192.168.1.2:2342 | -------syn-------🡪        | 192.168.1.3:80 |
| 192.168.1.2:2342 | 🡨----syn/ack------        | 192.168.1.3:80 |
| 192.168.1.2:2342 | -------ack-------🡪        | 192.168.1,3:80 |
|                  | **Connection Established** |                |

_**FIGURE X:** The TCP three-way handshake establishes a connection between listening hosts_

* **URG:** Urgent alias: Instructs that data contained in packets be processed ASA&#x50;_._
* **FIN**_:_ Finish alias: Communicates to the remote client host to close the connection.
* **RST:** Reset alias: Resets a connection.

SYN scanning mainly deals with three of the flags, namely, **SYN, ACK,** and **RST.**

Scanning Methods

_SYN Stealth/Half-Open Scan_

Since a TCP connect() scan can be detected by an IDS (Intrusion Detection System), hackers started evading the detection by using a technique known as _**“half-open scanning,”**_ as shown in the figure below. It is called this because the adversary does not open a full TCP connection. The adversary sends a SYN packet, impersonating a real connection, and waits for a response. A SYN/ACK indicates the port is in a listening state. An RST is indicative of a nonlistening port. If a SYN/ACK is received, the adversary immediately sends an RST to tear down the connection (actually, the kernel does this for the adversary). The main advantage of this scanning technique is that fewer sites will log it.

However, the adversary needs root privileges to build this custom TCP packet sequence. Sophisticated IDS and firewalling systems are now capable of detecting a SYN packet from the void and prevent such scans from occurring. This is because, like a TCP connect() system call, the half-open scan initiates with a SYN flag, which can easily be monitored by setting up a custom filter in either the IDS or firewall.

On the other hand, a disadvantage is that the adversary must make a custom IP packet to initiate the scan. Building a custom IP packet requires access to SOCK\_RAW (getportbyname (“raw”); under most systems) or /dev/bpf (Berkeley packet filter), /dev/nit (Sun “Network Interface Tap”). This generally requires privileged user access.

Even SYN scanning is not stealthy enough to evade most security detection mechanisms today. Some firewalls and packet filters actively watch and sniff the ingress/egress network traffic for SYNs to restricted ports, and programs such as **Synlogger** and **Courtney** are available to detect these scans. Conversely, some advanced scans may be able to pass through undetected. The term _**stealth,**_ in the context of networking basics, refers to a category of scans where the packets, appearing as normal innocuous traffic, is flagged with a particular set of flags other than SYN, or a combination of flags, no flags set, or all flags set; fragmented packets are used; or filtering devices are avoided by other means. All these techniques resort to inverse mapping to determine open ports.

_SYN/ACK Scan_

The TCP three-way handshake methodology is implemented by the SYN/ACK stealth scan. This technique. The difference is that in the last stage, remote ports are identified by examining the packets entering the interface and terminating the connection before a new initialization is triggered.

A stealth scan is done by performing the following steps:

1. To start initialization, the client forwards a single SYN packet to the destination server on the corresponding port.
2. The server then initiates the stealth scanning process, depending on the response sent back.
3. If the server forwards a SYN/ACK response packet, then the port is supposed to be in an open, listening state.
4. The client then responds with an RST packet, closing the connection before it is fully opened.

Below is a Python script using the scapy library to perform a SYN/ACK stealth scan. Step-by-step instructions are included explaining what each part of the code does.

1. **Install Scapy:** You need to have scapy installed. You can do it using pip:

![A black rectangle with white text

Description automatically generated](<../../.gitbook/assets/2 (33).png>)

1. **Construct Code:** After scapy has installed, using SUDO, compile the script and execute to run:

![A screen shot of a computer program

Description automatically generated](<../../.gitbook/assets/3 (25).png>)
