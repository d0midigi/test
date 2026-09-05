# 0 TCP TOC

TCP/IP Network Table of Contents

Part I: Open Systems, Standards, and Protocols

* What is an Open System?
* Network Architectures
  * Local Area Networks (LANs)
    * Bus Topology
    * Ring Topology
    * Hub and Spoke Topology
  * Wide Area Networks (WANs)
* OSI (Open Systems Interconnection) Reference Model Layers
  * The Application Layer
  * The Presentation Layer
  * The Session Layer
  * The Transport Layer
  * The Network Layer
  * The Data Link Layer
  * The Physical Layer
* Terminology and Notations
  * Packets
  * Subsystems
  * Entities
  * N-Functions
  * N-Facilities
  * Services
  * Making Sense of the Jargon
  * Queues and Connections
* Standards
  * Setting Standards
  * Internet Standards
* Protocols
  * Breaking Data Apart
  * Protocol Headers
* Summary

Part II – A Quick Overview of TCP/IP Components

* TCP/IP Protocols
  * Telnet
  * File Transfer Protocol (FTP)
  * Simple Mail Transfer Protocol (SMTP)
  * Kerberos
  * Domain Name System (DNS)
  * Simple Network Management Protocol (SNMP)
  * Network File System (NFS)
  * Remote Procedure Call (RPC)
  * Trivial File Transfer Protocol (TFTP)
  * Transmission Control Protocol (TCP)
  * User Datagram Protocol (UDP)
  * Internet Protocol (IP)
  * Internet Control Message Protocol (ICMP)
* TCP/IP History
* Berkeley Unix Implementations and TCP/IP
* OSI and TCP/IP Models
* TCP/IP and Ethernet
* The Internet
  * The Structure of the Internet
  * The Internet Layers
  * Internetwork Problems
* Internet Addresses
  * Subnetwork Addressing
    * The Physical Address
    * The Data Link Address
    * Ethernet Frames
  * IP Addresses
  * Address Resolution Protocol (ARP)
    * Mapping Types
    * The Hardware Type Field
    * The Protocol Type Field
  * ARP and IP Addresses
  * The Doman Name System (DNS)
  * Summary

Part III: Internet Protocol

* Internet Protocol
  * The Internet Protocol Datagram Header
    * Version Number
    * Header Length
    * Type of Service
    * Datagram Length (or Packet Length)
    * Identification
    * Flags
    * Fragment Offset
    * Time to Live (TTL)
    * Transport Protocol
    * Header Checksum
    * Sending Address and Destination Address
    * Options
    * Padding
  * Life of a Datagram
* Internet Control Message Protocol (ICMP)
* IPng: IP version 6
  * IPng Datagram
    * Priority Classification
    * Flow Labels
  * 128-Bit IP Addresses
  * IP Extension Headers
    * Hop-by-Hop Headers
    * Routing Headers
    * Fragment Headers
    * Authentication Headers (AH)
  * Internet Protocol Support in Different Environments
    * MS-DOS
    * Microsoft Windows
    * OS/2
    * Macintosh
    * DEC
    * IBMs SNA
    * Local Area Networks
* Summary

Part IV: TCP and UDP

* Introduction to TCP/IP
  * IP Addresses
  * Subnet Masks
  * Gateway Addresses
  * Protocols in the TCP/IP Suite
  * Automatic IP Address Allocation (APIPA)
  * Manual IP Address Allocation
* IEEE 802.X Standards
* Following a Message
* Ports and Sockets
* TCP Communications with Upper Layers
* Passive and Active Ports
* TCP Timers
  * The Retransmission Timer
  * The Quiet Timer
  * The Persistence Timer
  * The Keep-Alive Timer and the Idle Timer
* Transmission Control Blocks and Flow Control
* TCP Protocol Data Units (PDUs)
* TCP and Connections
  * Establishing a Connection
  * Data Transfer
  * Closing Connections
* User Datagram Protocol (UDP)
* Summary

Part V: Key Components of a Network

* Gateways, Bridges, and Routers
* Gateway Protocols
* Routing Daemons
* Routing
  * Fewest-Hops Routing
  * Type of Service Routing
  * Updating Gateway Routing Information
* The IGP and EGP Gateway Protocols
* Gateway-to-Gateway Protocol (GGP)
* The External Gateway Protocol (EGP)
  * Neighbors and EGP
  * EGP Messages
    * Neighbor Acquisition Messages
    * Neighbor Reachability Messages
    * Poll Messages
    * Update Messages
    * Error Messages
  * EGP to GGP Messages
  * EGP State Variables and Timers
* Interior Gateway Protocols (IGP)
  * The Routing Information Protocol (RIP)
  * The HELLO Protocol
  * The Open Shortest Path First (OSPF) Protocol
    * OSPF Packets
    * HELLO Packets
    * Link State Request and Update Packets
* Summary

Part VI: Telnet and FTP

* Telnet
  * Telnet Connections
  * Telnet Commands
  * TN3270
* File Transfer Protocol (FTP)
  * FTP Commands
  * FTP Connections
  * FTP Third-Party Transfers
  * Anonymous FTP Access
  * FTP Servers
* Trivial File Transfer Protocol (TFTP)
  * TFTP Commands
  * TFTP Packets
* Simple Mail Transfer Protocol (SMTP)
  * SMTP Commands
* The Berkeley Utilities
  * The hosts.equiv and .rhosts Files
  * rlogin
  * rsh
  * rcp
  * rwho
  * ruptime
  * rexec
* Summary

Part VII: Configuration

* Configuration Files
  * Symbolic Machine Names: /etc/hosts
  * Network Names: /etc/networks
  * Network Protocols: /etc/protocols
  * Network Services: /etc/services
* Setting the Host name
* The Loopback Driver
* Managing ARP
* User ifconfig
* The inted Daemon
* The netstat Command
  * Communications End Points
  * Network Interface Statistics
  * Data Buffers
  * Routing Table Information
  * Protocol Statistics
* The ping Utility
* Tracing a Connection
* Summary

Part VIIII: Network: Servers

* The Sample Network
* Configuring TCP/IP Software
* Unix TCP/IP Configuration
  * Configuring SCO Unix
  * Configuring Linux
  * Configuring Solaris
  * Configuring Windows Server
* Testing Server Configurations After Implementation
* Pseudo-ttys
* User Equivalence
* Anonymous FTP
* Configuring SLIP and PPP
* Remote Printing
* Configuring SNMP
* Summary

Part X: Network: Clients

* DOS-Based TCP/IP: FTP Software’s PC/TCP
  * Installing PC/TCP
    * The AUTOEXEC.BAT File
    * The CONFIG.SYS File
    * The PROTOCOL.INI File
    * The PCTCP.INI File
    * The Windows SYSTEM.INI File
  * Windows for Workgroups Using NetBIOS
  * Testing PC/TCP
* Windows-Based TCP/IP: NetManage’s Chameleon
  * Installing Chameleon
    * The AUTOEXEC.BAT File
    * The CONFIG.SYS File
    * The SYSTEM.INI File
    * The PROTOCOL.INI File
  * Configuring Chameleon
  * Testing Chameleon
* Configuring Windows 95 for TCP/IP
  * Installing TCP/IP
  * Further TCP/IP Configuration
  * Testing TCP/IP
* Winsock
  * Trumpet Winsock
  * Installing Trumpet Winsock
  * Configuring the TCP/IP Packet Driver
* Summary

Part XI: DNS

* Domain Name Service (DNS)
  * DNS Structure
  * The Name Server
  * Resource Records
  * IN-ADDR-ARPA
  * Messages
  * The Name Resolver
  * Configuring a Unix DNS Server
    * Entering the Resource Records
    * Completing the DNS Files
    * Starting the DNS Daemons
    * Configuring a Client
* BOOTP Protocol
  * BOOTP Messages
* Network Time Protocol (NTP)
* Summary

Part XII: Information Services

* Network File System (NFS)
* NFS Protocols
  * Remote Procedure Call (RPC)
    * Port Mapper
  * External Data Representation (XDR)
  * Network File System Protocol
  * Mount Protocol
  * File Locking
  * Remote Execution Service (REX)
  * rusers and spray
* Configuring NFS
  * Configuring Unix as an NFS Server
  * Setting Up a Unix NFS Client
  * Setting up Windows-Based NFS
* Network Information Service (NIS)
* Configuring NIS
  * Setting UP a NIS Domain
  * NIS Daemons
  * Setting Up an NIS Master
  * Setting Up NIS Slaves
  * Setting UP NIS Clients
* RPC and NFS Administration
  * rpcinfo
  * nfsstat
* Summary

Part XIII: Management

* Network Management Standards
* What is SNMP?
  * Management Information Base (MIB)
  * Simple Network Management Protocol (SNMP)
  * Setting UP SNMP Under Unix
  * SNMP Commands
* Network Topologies
* Configuring a Network
* Monitoring and Basic Troubleshooting Utilities
  * Troubleshooting the Network Interface
  * Troubleshooting the Network (IP) Layer
  * Troubleshooting TCP and UDP
  * Troubleshooting the Application Layer
* Security
* Summary

Chapter XIIII: Socket Programming

* Development of the Socket Programming Interface
* Socket Services
  * Transmission Control Block
  * Creating a Socket
  * Binding the Socket
  * Connection to the Destination
  * The open Command
  * Sending Data
  * Receiving Data
  * Server Listening State
  * Getting Status Information
  * Closing a Connection
  * Aborting a Connection
  * Unix Forks
* Summary
