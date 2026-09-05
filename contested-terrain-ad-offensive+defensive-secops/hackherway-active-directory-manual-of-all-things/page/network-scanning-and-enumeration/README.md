# Network Scanning and Enumeration

| <img src="../../.gitbook/assets/0 (50).png" alt="A close up of a light

Description automatically generated" data-size="original"> | <p>Network Scanning and Enumeration</p><p>CHAPTER OBJECTIVES INCLUDE:</p><p><strong>Network Scanning</strong></p><ul><li>Define Port Scanning, Network Scanning, and Vulnerability Scanning</li><li>Understand the Network Scanning and Enumeration Methodologies</li><li>Understand Ping Sweeping Techniques</li><li>Understand Nmap Command Switches and the Nmap Scripting Engine (NSE)</li><li>Understand SYN, Stealth, XMASS, NULL, SYN/ACK, FIN, and IDLE Scans</li><li>List TCP Communication Flag Types and ICMP Message Levels</li><li>Understand War Dialing Techniques</li><li>Understand Banner Grabbing and OS Fingerprinting Techniques</li><li>Understand How Proxy Servers Are Used in Launching an Attack</li><li>Explain How Anonymizers Work</li><li>Understand IP Spoofing Attacks and Techniques</li></ul><p><strong>Enumeration</strong></p><ul><li>Understand and Explain Enumeration Processes</li><li>Understand Enumeration Methodology</li><li>Explain and Understand NULL Sessions</li><li>Define Types of Enumeration: SNMP, DNS, SMB, RPC, ICMP, DHCP, Active Directory Domain Enumeration and Subdomain Enumeration</li><li>Define Steps in Performing Enumeration Tasks</li></ul> |
| ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Introduction to Network Scanning and Enumeration

Network scanning and enumeration represent, in my view, the 2.5th phase of hacking, focusing on the hacker’s efforts to locate target systems or networks. The classification of this phase varies significantly across different perspectives, with discrepancies arising from the interpretation of the hacking lifecycle stages. While some might categorize network scanning as the second phase, followed by enumeration as either the third, fourth, or even fifth phase, I propose that combining these two processes encapsulates the essence of the hacking lifecycle’s middle stages. Together, they serve to accumulate as much information as possible about your target, acting in tandem to lay the groundwork for subsequent hacking and attacking actions.

These two processes are inherently interconnected; network scanning is a prerequisite for enumeration, and vice versa. Enumeration, without prior scanning, would leave you in the dark about your target’s layout and potential vulnerabilities. Similarly, scanning alone, without the detailed insights gained from enumeration, would limit the effectiveness of identifying exploitable weaknesses. Just as going into battle without knowing the terrain and enemy positions would be unwise, initiating an attack without a clear understanding of the target system’s structure and defenses is equally risky.

Therefore, this chapter aims to delve into the methodologies surrounding both network scanning and enumeration, highlighting their pivotal roles within the ethical hacking lifecycle. By understanding and applying these techniques effectively, ethical hackers can enhance their abilities to identify and exploit vulnerabilities, ultimately strengthening the security posture of the systems you are tasked with protecting.

Introduction to Network Scanning

During network scanning, the hacker continues to gather information regarding the network and its individual host systems. Data such as IP addresses, operating systems, service versions, and installed applications can help the hacker decide which type of exploit to use in hacking a system. _Network scanning_ is the process of locating systems that are in a listening state and responding on the network. Ethical hackers use these techniques to target a systems’ IP address, and more.

As an ethical hacker, it is imperative that you possess an in-depth understanding of network protocols such as TCP, UDP, ICMP, and IP before reading this chapter. Once an adversary has identified a target system and does initial reconnaissance, as discussed in the previous chapter on reconnaissance and footprinting, the adversary concentrates efforts on gaining initial access into the target infrastructure. It should be noted that network scanning is not limited to intrusion alone. It can also be an extended form of reconnaissance (if you think about it) where the adversary obtains even more information about the target, such as what operating system is used, the services that are being run on the systems, and whether any configuration lapses can be identified. The adversary can then strategize an attack, factoring in these aspects.

Network Scanning Defined

_**Scanning**_ is one of the most important phases of intelligence gathering for an adversary. In the process of scanning, the adversary tries to gather information about the specific IP addresses that can be accessed over the Internet, the target’s operating systems and system architecture, and the services running on each computer identified.

The purpose of scanning is to discover exploitable communications channels, probe as many listeners as possible, and keep track of the ones that are responsive or useful to an adversary’s particular needs. In the network scanning phase of an attack, the adversary tries to find various ways to intrude into a target system. The adversary also tries to discover more about the target system by finding out what operating systems are used, what services are running, and whether there are any configuration lapses in the target system. The adversary then tries to form an attack strategy based on facts learned during the scan.

After the active and passive reconnaissance and footprinting phases of the hacking lifecycle have been completed, network scanning and enumeration are performed. Network scanning is used to determine whether a system is on the network and available. Scanning tools are then used to gather information about systems, such as IP addresses, operating system, and services running on the target. The different types of network scanning are as follows:

* _**Port Scanning**_

_**Determine Open Ports and Services**_<br>

Port scanning is the process of checking the services running on the target computer by sending a sequence of messages to break in. Port scanning involves connecting to TCP and UDP ports on the target system to determine if the services are running or are in a listening state. The listening state gives an idea of the operating system and the applications in use. Sometimes, active services that are listening may allow unauthorized user access to systems that are misconfigured or running software that has vulnerabilities.

Port scanning tools enable a hacker to learn about the services available on a given system. Each service or application on a machine is associated with a _**well-known**_ port number. For example, a port scanning tool that identifies port 80 as open indicates a web server running on that system. Hackers need to be familiar with well-known port numbers.

**Note:** On Windows systems, well-known port numbers are located in the C:\Windows\System32\drivers\etc\services file. The Services file is a hidden file by default. To view it, show hidden files in Windows Explorer, double-click the file, and open it with Notepad. A well-rounded ethical hacker will be familiar with the well-known port numbers such as _**FTP (21/22), Telnet (23), HTTP (80), SMTP (25), POP3 (110), HTTPS (443),**_ among many more.

* _**Network Scanning**_

_**Determine IP Addresses, MAC Addresses, Hostnames**_

Network scanning is a procedure for identifying active hosts on a network, either to attack them or as a network security assessment. It is a procedure for identifying active hosts on a network, either to attack them or as a network security assessment. Hosts are identified by their individual IP addresses. Network scanning tools attempt to identify all the _live_ or responding hosts on the network and their corresponding IP addresses.

* _**Vulnerability Scanning**_

_**Determine Presence of Known Weaknesses and Exploits**_

Vulnerability scanning is a method used to check whether a system is exploitable by identifying its vulnerabilities. A vulnerability scanner consists of a scanning engine and a threat and virus database, or catalog. The catalog consists of a list of common files with known vulnerabilities and common exploits for a range of servers. A vulnerability scanner may look for backup files or directory traversal exploits, for example. They may also identify the operating system and version number, including service packs that may be installed. The scanning engine maintains logic for reading the exploit list, transferring the request to the web server and analyzing the requests to ensure the safety of the server. These tools generally target vulnerabilities that are easily fixed by secure host configurations, updated security patches, and a clean web document. During the later attack phase, a hacker can exploit those weaknesses to gain initial access to the target system.

* _**Intrusion Detection System (IDS)**_

_**Determine Malicious Activities and Block**_

An intrusion detection system (IDS) or a sophisticated network security professional with the proper tools can detect active port scanning activities. Scanning tools probe TCP/IP ports looking for open ports and IP addresses, and these probes can be recognized by most security intrusion detection tools. Network and vulnerability scanning can usually be detected as well, because the scanner must interact with the target system over the network.

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

As an ethical hacker, you’re expected to be familiar with the network scanning methodology presented in the figure below. This methodology is the process by which a hacker scans the network. It ensures that no systems or vulnerabilities are overlooked and aids the hacker in efficiently gathering all necessary information to perform an attack. A hacker follows a particular sequence of steps to properly scan a network.

We’ll look at the various stages of this scanning methodology throughout this book, starting with the first three steps – checking for systems that are live and for open ports and service identification. A generic approach has been presented, so the scanning methods may differ based on your specific objectives. The steps involved in network scanning are as follows:

1\. _**Check for live systems:**_ An adversary may start with the objective of checking for live systems on the network.

2\. _**Check for open ports:**_ After the live systems are found, the adversary will look for open ports to determine which services are running on the systems. This can be a vital step, because some services may be of a much higher priority from the adversary’s point of view.

3\. _**Fingerprint the operating system:**_ The next phase involves fingerprinting the operating system by figuring out the target’s network layout.

4\. _**Scan for vulnerabilities:**_ Identification of the vulnerabilities in the target’s OS is the next step. The malicious actor may try to exploit these vulnerabilities during an attack.

5\. _**Probe the network:**_ The malicious actor may also choose to actively probe the network or slightly monitor its traffic. This can be accomplished using proxies (which will be discussed later in the chapter). The technique of anonymous surfing makes it hard to trace this activity back to the malicious actor.

Step 1: Check for Live Systems

_Ping Sweep_

The network scanning methodology starts with first checking for systems that are live and listening on the network at the time you plan to scan. A machine that is termed as being _live_ on a network means that there are actively listening devices (e.g., turned on) in either a wired or wireless network. The simplest, although not necessarily the fastest, or most accurate, way to determine whether systems are live on a network is to perform a _**“ping sweep”**_ of the IP address range.

A ping sweep (also known as an _**ICMP sweep**_, and a _**“two-way handshake protocol”**_ ) is a basic network scanning technique to determine which range of IP addresses map to live hosts (computers). Ping sweeps are conducted using tools such as the one show in the image below. While a single ping will tell the user whether one specified host computer exists on the network, a ping sweep consists of ICMP ECHO request sent to multiple hosts. If a given IP address is live, it will return an ICMP ECHO reply. Ping sweeps are among the oldest and slowest methods to scan a network. This utility, distributed across almost all platforms, acts like a roll call for systems; a system that is active on the network answers to the ping query that another system sends out.

The phrase “two-way handshake protocol” reflects the way data packets are sent and received: one host sends data, the other validates it and replies with whether the ping was successful.

Internet Control Message Protocol (ICMP) scanning is the process of sending an ICMP request or _**“ping”**_ to all hosts on the network to determine which ones are up and responding to pings. A benefit of ICMP scanning is that it can run quickly on an entire network. Most hacking tools include a ping-sweep option, which essentially means performing an ICMP request to every host on the network.

“Ping” was first coined as a technical term by the sonar technology industry, when it was associated with the detection capabilities of submarines. A submarine with active sonar projects a sound, or a ping, which bounces back if it encounters an obstacle, like another submarine. This is the technical origin of ping, which is now more commonly linked with IP network utilities, and we can use them as a reconnaissance tool in what we call ping sweeps, as described above.

* Ping is available on any device connected to a network. It’s a command-line utility, a standard component of a network administrator’s capabilities.
* Ping sweep is the more popular name for an Internet Control Message Protocol (ICMP) sweep, a simple way of diagnosing potential network issues and identifying IP addresses used by “live” or “dead” hosts. These hosts are typically computers, but anything can be a host, including printers, computer systems, websites, networks, smart refrigerators, coffee makers, personal home security systems, tablets. Any device that can connect to the internet, and has an IP address, is a host, and is hackable.
* Discover which IP addresses are active or live on the network.
* Detect rogue devices and unauthorized networks.
* Ensure the IP addresses on the network match network documentation and schematics. This ensures robustness in your disaster recovery and COOP, BIA, or BCP procedures.

Although ping sweeps are deemed older than dirt, they are still very relevant and are still very well-used in the hacking field today. If you’ve used it long enough, it’s basically your first go-to tool (even before using Nmap) when needing to scan and map the lay of the land (e.g., the network topology, identify inactive IP addresses, and determining which IP addresses map to live hosts in a DHCP environment).

Ping sweeps are more complex than single pings in that they require more advanced software packages that feature enhancements and capabilities. Some ping sweep software may also have the capacity to reveal other useful information about the hosts, besides their live or dead status. For example, they may be able to tell you whether there was any packet loss during a ping, as well as how long the signal took to return. This information can assist users in diagnosing network vulnerabilities and faults.

Ping and ICMP Sweepers

| **Product/Vendor**            |                                                                                                                     | **Free Trial?**  | **Top Features**                                |                                        |                                           | **Bottom Line**                                                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------- | ----------------------------------------------- | -------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| SolarWinds IP Address Manager | <img src="../../.gitbook/assets/1 (36).png" alt="Vendor Spotlight: SolarWinds - GovSmart" data-size="original">     | 30-Day           | Generous free trial                             | Built-in IP address scanning           | Automated IP address tracking             | Fantastic for continuous and sophisticated network coverage and impressive integration with other monitoring capabilities |
| SolarWinds Engineer’s Toolset | <img src="../../.gitbook/assets/2 (31).png" alt="Vendor Spotlight: SolarWinds - GovSmart" data-size="original">     | 14-Day           | Simple user interface                           | Support for various file format export | 60+ network management tools              | A versatile range of tools covering all aspects of network monitoring                                                     |
| Zenmap                        | <img src="../../.gitbook/assets/3 (4).jpeg" alt="Zenmap: A GUI Frontend For Nmap Network ..." data-size="original"> | 100% Free        | Searchable database of scans                    | Open-source                            | Topology mapper                           | A great place for beginners to start, with an intuitive interface                                                         |
| Paessler PRTG                 | <img src="../../.gitbook/assets/4 (27).png" alt="Paessler PRTG - Wikipedia" data-size="original">                   | 30-Day           | Full network visibility                         | Customizable system                    | Cloud-based services available            | A customizable system with priced plans based on chosen sensors, rather than device number                                |
| IPHost Network Monitor        | <img src="../../.gitbook/assets/5 (4).jpeg" alt="IPHost Network Monitor for Windows ..." data-size="original">      | 50 Monitors Free | Bypasses machines turned off (no hanging scans) | Quick installation                     | 44+ monitoring types                      | Quick, basic, easy, and low-cost tool with great tech support                                                             |
| Advanced IP Scanner           | <img src="../../.gitbook/assets/6.jpeg" alt="Advanced IP Scanner" data-size="original">                             | 100% Free        | Remote control sessions                         | MAC address detection                  | Shared folder access                      | A free tool specifically designed and attuned to Windows server                                                           |
| Fping                         |                                                                                                                     | 100% Free        | Support for IPv6 networks                       | Link output to DNS                     | Report in various outputs (xml, txt, csv) | A free tool for Linux with multiple ways of entering IP address ranges                                                    |
| Angry IP Scanner              | <img src="../../.gitbook/assets/7 (24).png" alt="fping | Kali Linux Tools" data-size="original">                    | 100% Free        | Multithreading for speed                        | NetBIOS information                    | No installation                           | A free, zero-installation tool known for its ping sweep and port scanning speed                                           |
| Ping Plotter Pro              | <img src="../../.gitbook/assets/8 (2).jpeg" alt="PingPlotter 4.00.3 - Neowin" data-size="original">                 | 14-Day           | Visuals and graphs                              | Multitarget monitoring                 | Perpetually monitor network               | An impressive tool with a free, standard, and professional version available                                              |
| OpManager                     |                                                                                                                     | 30-Day           | Multiple parameters for scanning                | Periodic ping requests                 | Round Trip Time (RTT) reporting           | A simple and basic ping tool, though the overall network management and monitoring package is versatile.                  |

How Ping Works

ECHO Request and ECHO Response are the two fundamental aspects of how ping functions. Essentially, an ECHO request is the packet of data sent to either a specific IP address or a range of IP addresses. The ECHO response then replies, and the nature of the reply can reveal important information about the IP address range the ping was sent to.

When the ECHO request is sent, the input value can either be a host, a domain name, or an IP address. The input determines the route taken by the ECHO request, with the potential to expose any delays or issues with the route, so steps can be taken to fix them. If you input a hostname for a device on a network, for instance, the ping route will be directed to the local DNS server so it can acquire the relevant IP address. A domain name input, on the other hand, will first access the domain’s web server. An IP address input will result in a direct _**Round-Trip Time (RTT)**_ result. Each of these inputs can potentially produce different information, which could inform diagnostics and general IP address management strategies.

A user might identify an issue flagged by an ECHO response via the time output field. During a ping sweep in which all network devices are tested, healthy devices should respond within a narrow time frame. When a device doesn’t comply with the request, this could be indicative of an issue needing to be addressed. It could, for example, mean the device is damaged or overloaded.

Put simply, an ECHO request is the ping, while the ECHO response is the ping reply. Echoes are mostly used for troubleshooting. They can reveal whether TCP/IP stacks are configured correctly and if there are any issues with the routes packets are taking. These functionalities are crucial to successful IP address management because, when used in the right way, they can be responsible for diagnosing and eradicating network faults.

To understand ping better, one should be able to understand the basic construct of the TCP/IP packet. When a system does a ping, a single packet is sent across the network to a specific IP address. This packet contains 64 bytes (56 data bytes and 8 bytes of protocol header information). The sender then waits or listens for a return packet from the target system. If the connections are good and the target computer is “alive,” a good return packet can be expected; however, if there is a disruption in the communications, this will not be the case. Ping also details the number of hops the lie between the two computers and the amount of time it takes for a packet to make the complete trip. Remember, this is called the round-trip time. Ping can also be used for resolving host names. In this case, if the packet bounces back when sent to the IP address, but not when sent to the name, then it is an indication that the system is unable to resolve the name to the specific IP address.

A packet, in the case of ping sweeps, is a formatted unit of data designed to test the route to an IP address. A single pink is conducted via an ICMP ECHO request, which entails sending

Infiltrator, Pinger, Friendly Pinger, and WS Ping Pro are all tools that perform ICMP queries. You should be familiar with how to use these tools.

Detecting Ping Sweeps

Almost any IDS or Intrusion Prevention System (IPS) will detect and alert the security administrator to a ping sweep occurring on the network. Most firewall and proxy servers block ping responses so a hacker can’t accurately determine whether systems are available using a ping sweep alone. More intense port scanning must be used if systems don’t respond in a fashionable and timely manner. Just because a ping sweep doesn’t return any active hosts on the network, doesn’t mean they aren’t available – you need to try an alternate method of identification, or scan more than once, sometimes twice – even thrice.

![](<../../.gitbook/assets/9 (20).png>)

Remember, hacking takes time, patience, and persistence.

![](<../../.gitbook/assets/10 (16).png>)

_ICMP Scanning_

All required information about a system can be gathered by sending ICMP packets to it, a process known as _**“ICMP Scanning.”**_ Since ICMP does not have port abstraction, this cannot be considered a case of port scanning; however, it is useful to determine what hosts in a network are up by pinging them all. The user can also increase the number of pings in parallel with the -L option. It can also be helpful to tweak the ping timeout value with the -T option. The UNIX tool ICMPquery or ICMPush can be used to request the time on the system (to find out which time zone the system is in) by sending an ICMP type 13 message (TIMESTAMP). The netmask on a particular system can also be determined with ICMP type 17 messages (ADDRESS MARK REQUEST). After finding the netmask of a network card, a user can determine all the subnets in use. After getting knowledge about the subnets, the user can target only one subnet and avoid hitting the broadcast addresses. ICMPquery has both a timestamp and address mask request option.

One considerable problem with this method is that personal firewall software- and network-based firewalls can block a system from responding to ping sweeps. Another problem is that the computer must be turned on to be scanned.

_Remember, hacking takes time, patience, and persistence._

![A screenshot of a computer program

Description automatically generated](../../.gitbook/assets/11.gif)\
_**FIGURE X:** The Infiltrator ping sweep tool._

Step 2: Check for Open Ports

_Three-Way Handshake_

TCP is a **connection-oriented** protocol, which means that connection establishment is performed prior to data transfer between applications. This connection is possible through the process of the three-way handshake. The _**three-way handshake**_, illustrated below, is implemented to establish connection between hosts. The three-way handshake process goes as follows:

1. The source (Computer A) sends a SYN packet to the destination (Computer B) to establish a TCP connection.
2. The destination, upon receiving the SYN packet sent by the source, starts the TCP session by sending a SYN/ACK packet back to the source.
3. This SYN/ACK packet acknowledges the arrival of the first SYN packet to the source.
4. In conclusion, the source sends an ACK packet back thereby providing acknowledgement for the SYN/ACK packet sent by the destination node.

This allows communication between the source and the destination until either of them issues a FIN packet or an RST packet to close the connection.

![TCP 3 Way Handshake In Detail - DEV Community](<../../.gitbook/assets/12 (19).png>)\
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

Description automatically generated](<../../.gitbook/assets/13 (15).png>)

1. **Construct Code:** After scapy has installed, using SUDO, compile the script and execute to run:

![A screen shot of a computer program

Description automatically generated](<../../.gitbook/assets/14 (16).png>)

_XMAS Scan/FIN Scan_

An XMAS scan (also known as a _**FIN Scan)**_ is a type of port scan used in network security to identify listening TCP ports on a target system. The name ‘XMAS’ comes from the fact that the scan sets all the flags in the TCP header (FIN, URG, and PSH), making the packet look “lit up” like a Christmas tree when viewed in a sniffer. Most sniffers will assign TCP packet headers different colors to differentiate between them hence the name XMAS scan. This technique can help evade _some_ firewall rules and detection mechanisms.

How an XMAS Scan Works

1. **Send a packet with all flags set:** The scanner sends a TCP packet with the FIN, URG, and PSH flags set to the target port.
2. **Interpret the Response:**
   *
     * **No Response:** If the target does not respond, the port is considered **open** or **filtered.**
     * **RST/ACK Response:** If the target responds with an RST/ACK packet, the port is assumed closed.
3. **Effectiveness:** The XMAS scan can be effective against certain operating systems and firewall configurations; however, it might not work on all systems, especially those that comply strictly with the TCP/IP standards (like Windows); therefore, it is mainly directed at UNIX-related systems.

Prerequisites

1. **Install scapy:** You need to have scapy installed. You can install it using pip:

![A black rectangle with white text

Description automatically generated](<../../.gitbook/assets/15 (15).png>)

Performing an XMAS Scan

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/16 (16).png>)

1. **Create an XMAS Packet:** In the output above, this step constructs an IP packet with a TCP segment. The dst parameter is the target IP address, and the dport parameter is the target port number. The flags=FPU sets the TCP flags to FIN, URG, and PSH.

![A black rectangular object with white text

Description automatically generated](<../../.gitbook/assets/17 (14).png>)

1. **Send the XMAS Packet and Receive a Response:** The sr1 function sends the XMAS packet and waits for a single response. The timeout=2 parameter specifies the wait time in seconds for a response. The verbose=0 parameter suppresses detailed output.

![A black rectangular with white text

Description automatically generated](<../../.gitbook/assets/18 (14).png>)

1. **Check if We Received a Response:** This step verifies whether the target responded to the XMAS packet.

![A black rectangular object with white text

Description automatically generated](<../../.gitbook/assets/19 (12).png>)

1. **Check if the Response is an RST:** If the response has a TCP layer and the TCP flags are 0x14 (RST), it indicates that the port is closed.

![A black background with white text

Description automatically generated](<../../.gitbook/assets/20 (8).png>)

1. **Handle Unexpected Responses:** If the response is neither expected or easily interpretable, it prints an unexpected response message.
2. **Handle No Response:** If there is no response from the target, it prints that the port is opened or filtered.

Usage

Replace target\_ip and target\_port with the desired target IP address and port number you want to scan:

The script above provides a simple yet effective way to perform an XMAS scan to determine the status of a port on a target machine.

Why Perform an XMAS Scan When You Can Use Nmap?

_Nmap, Nessus, and Other Scanning Tools_

Nmap (Network Mapper) is a versatile and widely-used tool for network discovery and security auditing. It can perform a variety of scans, including SYN, XMAS, ACK, FIN, UDP, and more. Nmap can also detect operating systems, service versions, and perform advanced discovery through its scripting engine, known as NSE, for the Nmap Scripting Engine.

One of the key strengths of Nmap is its great flexibility and generous capabilities making it suitable for both quick scans and in-depth scans, providing you a better avenue for thorough network analysis and a look into what is going on behind the scenes as far as traversing ingress/egress traffic is concerned. Network administrators and security professionals often use Nmap for legitimate security assessments, troubleshooting, and network inventory and asset discovery (I do). Its ability to perform different types of scans, including stealthy ones like an XMAS scan, makes it an awesome tool for understanding the state of your networked systems in real-time.

_Nessus_

Nessis is a vulnerability scanner primarily used to detect vulnerabilities in systems by comparing scan results against its database of known vulnerabilities which is inputted via threat intelligence gathering plugins. It performs detailed scans and can provide extremely comprehensive reports on security issues, misconfigurations, and compliance checks of all sorts. Nessus automates the scanning process, making it an efficient tool for regular security assessments and weekly patch vulnerability scans. Its detailed vulnerability reports and compliance checks are most valuable for presenting to your client a detailed look into the attack surface of their organization. While Nessus _can_ detect open ports, as can an XMAS scan, its focus is simply identifying and reporting vulnerabilities rather than just performing network reconnaissance.

_XMAS Scan and Stealthy Techniques_

An XMAS scan, as stated previously, is a stealthy scanning technique where a TCP packet is sent with the FIN, URG, and PSH flags set. This “lights up” the packets like a Christmas tree, hence the name. The primary goal of an XMAS scan is to detect the status of ports while evading detection mechanisms like firewalls and intrusion detection systems (IDS). If a port is closed, the target typically sends an RST packet response. If the port is open or filtered, there is no response. The stealthiness of the XMAS scan lies in its ability to bypass certain security controls that might flag or block more straightforward scanning techniques. This makes it useful in situations where avoiding detection is critical, such as when performing a black-box assessment.

_Comparison and Use Cases_

While tools like Nmap can perform an XMAS scan, among others, the key difference lies in the intent and context of use. Nmap, Nessus, and similar tools are typically used for legitimate security assessments and troubleshooting within a network. They offer security-rich features and generate detailed reports, making them suitable for regular use. On the other hand, specialized or stealthy techniques like the XMAS scan are often employed when there is a need to evade detection, such as in penetration testing scenarios or by adversaries trying to avoid getting caught.

The choice between using an XMAS Scan/FIN Scan and Nmap (or other scanning-related tools) depends really on the specific requirements of the task you face. Think about it as having to choose between a red apple and a green apple: Both methods have their unique advantages and are suited for different scenarios; however, both have their own set of scaling drawbacks as well. To aid you in decision-making, it is best that you first understand the nuances between the two ultimately helping you to decide which tool or technique best suits your needs, goals, or objectives.

XMAS Scan

| **Purpose**                                                                                                                                                                                                                 | **Use Cases**                                                                                                                                                                                                  | **Limitations**                                                                                                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \*An XMAS scan is a type of stealthy port scan that sends only the FIN packet without any other flags set. This makes it difficult for IDS to detect because it does not follow the normal TCP three-way handshake process. | Particularly useful in environments where IDS are heavily deployed and might block or flag standard scans like SYN scans. The goal is to remain undetected while still gathering information about open ports. | While effective in bypassing some IDS, XMAS scans may not be reliable as other types of scans due to variations in how different operating systems handle FIN packets. Some systems might drop the packet entirely, making it seem like the port is closed even if it’s open. |

\*Clearing Up Assumed Confusion

_…but, you previously stated that XMAS scan lights up all flags hence its name?_

To clarify the correct understanding of an XMAS scan.

An XMAS scan, named after the “X” pattern formed by the flags in the TCP header when viewed in binary, sets **all flags** **except the FIN flag.** The means that the SYN, ACK, URG, PSH, and ECE flags are set, but the FIN flag remains unset. This behavior distinguishes the XMAS scan from other types of scans and gives it its characteristic name.

In a typical TCP connection setup, the SYN flag is sent first to initiate a connection, followed by the SYN/ACK response from the server, and finally, the client sends the ACK flag to complete the TCP three-way handshake. In contrast, an XMAS scan sends a packet with _all flags set except the FIN flag._ This packet looks like a malformed TCP segment because it doesn’t adhere to the usual sequence of flag settings during the connection establishment phase.

Because the XMAS scan packet deviates from the standard TCP communication patterns, intrusion detection systems (IDS) and firewalls that rely on recognizing these patterns might not immediately recognize it as a legitimate TCP packet. This can make the XMAS scan more difficult to detect, as it doesn’t trigger the usual responses associated with a legitimate connection attempt.

The main advantage of an XMAS scan is its ability to bypass certain types of intrusion detection mechanisms that are looking for anomalies in the TCP flag settings; however, it’s worth noting that not all systems will respond to an XMAS scan in the same way, and some might simply ignore the packet altogether or send an error message instead of revealing whether a port is open or closed.

Nmap

| **Purpose**                                                                                                                                                                                                            | **Use Cases**                                                                                                                                                                                                                                         | **Advantages**                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Supports various scanning techniques, including XMAS scans among others like SYN, ACK, UDP, and more.</p><p>Provides a wide range of options for customizing scans according to the environment and objectives.</p> | <p>Nmap is widely used for network discovery and security auditing</p><p>Extensive feature set allows detailed information grabbing about hosts, networks and services</p><p>Suitable for both penetration testing and network asset inventories.</p> | <p>Offers scripting capabilities for post-scanning tasks like vulnerability assessment, service version detection, and more</p><p>Boasts strong community support and regular updates are published</p> |

Why Stealthiness is Important in Ethical Hacking
