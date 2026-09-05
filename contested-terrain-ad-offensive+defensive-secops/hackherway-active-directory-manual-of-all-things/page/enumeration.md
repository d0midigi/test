# Enumeration

|                      | <h3>CHAPTER</h3> |
| -------------------- | ---------------- |
| <h3>ENUMERATION</h3> | <h3>5</h3>       |

Chapter Objectives

If you have spent any time hacking labs, for example, then you undoubtedly have heard people curse up a blue storm that you need to _script your enumeration!_ There is an absurd amount of scripts available to aid in automating these tasks for you. Automation can save time and brainpower; however, it’s not always the best approach for learning, especially for beginners. When people rely too heavily on automation, they might not understand what’s actually happening. Instead of manually running tools and commands, you end up sifting through output that might be irrelevant or unfamiliar. Running a script with a low-privilege shell, dumping pages of output, and hoping to find a clue for privilege escalation can often lead to missing key details because you haven’t practiced focused searches for specific vulnerabilities and misconfigurations.

Furthermore, the real possibility exists that the scripts you choose to uses might not even highlight the path to privilege escalation in their output. You could run a script that performs various port enumeration tasks, only to find yourself manually redoing much of the work. Different tools might give different results for similar functions, and you need to figure out that a non-standard port is running SSH, HTTP, or some other protocol. Deciding how to enumerate it might involve using different tools and non-default options. I’m only stating this because it needs to be said: you are better off in the long run if you learn to do things yourself before you tell a robot to do it for you.

If you find that scripting makes things easier in the long run, feel free to use them; however, in my experience, it’s better to learn how to do things manually first—get your feet wet before diving in headfirst. Enumeration is a fundamental concept that will always be relevant as long as hacking and cybersecurity exist. Mastering it on your own before relying on scripts is crucial for developing a strong foundation. This approach ensures you fully understand the process and equips you to successfully complete any assessment task, setting you on the path to becoming a successful hacker.

Enumeration is a fundamental concept that spans the entire lifecycle of an attack. In the context of this chapter, enumeration refers to the initial discovery phase, incorporating elements from reconnaissance, footprinting, information gathering, and network scanning. This phase is crucial for understanding the systems in your environment, including determining which ports are open, identifying the services running on those ports, and assessing how these services might be exploited, misconfigured, or used to gain unauthorized access. By understanding user and group access permissions, you'll gain comprehensive visibility into the attack surface.

The information gathered during enumeration will guide your interactions with the technical elements of the target infrastructure, both before and during an attack. This chapter introduces essential commands using some of the most widely used tools in the hacking industry. As an ethical hacker, you’ll find that many of these tools are the same ones used by malicious actors. Additional tools will be covered to further refine your discoveries, along with relevant Metasploit modules and manual exploits.

Keep in mind that tools are constantly evolving, and there are too many to cover in a single chapter. For a more comprehensive list of popular tools, refer to Appendix C of this book. It’s crucial to explore the available resources in depth and experiment with new tools you encounter along the way.

**Network Scanning**

For basic network scanning and port probing, you have the option to either write your own script or use one that's already available. While most hackers rely on Nmap for scanning, there are situations where you might need to use a different tool. The main reason for writing a script is typically when you're on a computer that doesn't have these tools installed and you need to scan quickly. For instance, if you're pivoting into another subnet from a Linux machine with two network interfaces and can't or don't want to install Nmap, you might write a quick bash script to scan the new subnet.

There are countless ways to accomplish this task, so it's beneficial to have multiple options. Be sure to explore the features of each tool mentioned in this and subsequent chapters, especially Nmap, which is one of the most valuable tools you can learn to use effectively.

**What is Enumeration?**

Enumeration is a fascinating creature because it causes systems and infrastructures to react and behave to probing and penetrating introductions in unexpected ways. Steve Wozniak, one of Apple’s founders, mentioned that majority of hacking involves messing with people’s heads, getting others to do unusual things they would, otherwise, not carry out (e.g., a social engineering attack where, for example, an individual divulges sensitive information to another who may not have authorization, or the required rights, or need to know). Enumeration achieves this. It’s also a fundamental part of evaluating any target, ranging from simple reverse DNS (rDNS) lookups to comprehensive OSINT and scanning processes.

Enumeration is crucial in ethical hacking and penetration testing as its main goal is to accomplish the feat of gathering extensive information about a target network, information system, application, service, data, or user(s). This information helps a hacker to get a general idea, understanding, or visualization of the target’s _“lay of the land.”_ The information gathered and correlated can draw a logical picture for the hacker detailing processes, dependencies, and vulnerabilities within the target environment ultimately guiding the hacker to the next phase of the assessment towards effective exploitation opportunities.

In the previous chapters, you learned about footprinting and network scanning. This chapter covers the next phase: enumeration. We will start with an introduction to enumeration concepts. Subsequently, this chapter provides insight into different techniques for Network Basic Input/Output System (NetBIOS), Simple Network Management Protocol (SNMP), Lightweight Directory Access Protocol (LDAP), Network Time Protocol (NTP), Network File System (NFS), Simple Mail Transfer Protocol (SMTP), Domain Name System (DNS), Internet Protocol Security (IPSec), Voice over Internet Protocol (VoIP), Trivial File Transfer Protocol (TFTP), Server Message Block (SMB), Internet Protocol version 6 (IPv6), and Border Gateway Protocol (BGP) enumeration. The chapter will then end with an overview of enumeration countermeasures.

Before we dive into network enumeration, it’s first essential to understand its purpose and its benefits. In this chapter, we’ll explore:

* What is enumeration?
* Enumeration via defaults
* NetBIOS enumeration (among others)
* Using SNMP for enumeration
* After reading this chapter, you will be able to:
* Describe the enumeration step of security testing
* Enumerate Windows OS (Operating System) targets and services
* Enumerate \*nix OS targets and services
* Explain different techniques for NetBIOS enumeration
* Explain different techniques for SNMP enumeration
* Explain different techniques for LDAP and Active Directory (AD) enumeration
* Explain different techniques for NTP enumeration
* Explain different techniques for NFS enumeration
* Explain different techniques for SMTP and DNS enumeration
* Explain other enumeration techniques such as IPSec, VoIP, RPC, Linux/Unix, Telnet, FTP, TFTP, SMB, IPv6, and BGP enumeration
* Hacking and Attacking SNMP
* Apply enumeration countermeasures

**Enumeration Concepts**

Different sections of this chapter deal with the enumeration of different services and ports. Before discussing the action enumeration process, concepts related to enumeration will first be introduced.

**What is Enumeration?**

Network enumeration is a technique typically performed internally, involving active and passive connections to target machines. Unlike passive reconnaissance enumeration carries a higher risk of detection due to the necessity of establishing an active connection and given the fact that most active scanning and enumeration processes are often noisy on the wire, making the probability of getting caught much higher than in using passive enumerating techniques. During enumeration, a hacker accessing a network share, for example, must authenticate (depending on the authentication security posture of the target organization being probed), providing credentials linked to an Access Control List (ACL). This ACL outlines usernames, groups, and permissions for accessing certain resources on the target network. For a hacker, the goal of enumeration is to obtain valuable information without authenticating oneself, potentially exploiting the target machine’s vulnerabilities.

Enumeration is the process of extracting usernames, machine hostnames, network resources, shares, services, local user, group and service memberships from a target system or network. In the enumeration phase, your goal is to crate active connections with the system and send directed queries to that system to gain more information about your target. You can then use the information collected using enumeration to identify vulnerabilities in the system security, which help them exploit the target system. In turn, enumeration allows you to perform password attacks to gain unauthorized access to information system resources. Enumeration techniques work great in intranet environments because they benefit from higher access and visibility to network resources, such as servers, databases, and user directories. Internal networks often have fewer security measures compared to public-facing systems, allowing you to gather detailed information more easily. Additionally, intranet environments tend to have more predictable network structure and configurations, making it simpler to identify and exploit vulnerabilities.

**Common Enumeration Methods**

* **LDAP Enumeration:** Leveraging the Lightweight Directory Access Protocol (LDAP) for gathering information from directories.
* **Network Time Protocol (NTP):** Using NTP to determine the time settings of remote hosts, which can reveal information about the target network topology.
* **SMTP Enumeration:** Employing Simple Mail Transfer Protocol (SMTP) to gather email addresses and domain information.
* **DNS Enumeration:** Extracting DNS records to uncover target domain-related information including subdomains and mail server sensitive information.
* **Null Session:** Establishing null sessions to query services and shares on older operating systems that haven’t disabled this feature.

![A diagram of a diagram

Description automatically generated](<../.gitbook/assets/0 (25).png>)

FIGURE X: Enumeration classification.

In particular, enumeration allows you to collect the following information:

* Network resources
* Network shares
* Routing tables
* Audit and service settings
* Fully Qualified Domain Name (FQDN) details
* Machine names
* Users and groups
* Applications and banners

![](<../.gitbook/assets/1 (14).png>)

Enumeration takes port scanning to the next level. Now that you know how to discover live systems on a network, the next steps are finding what resources are shared on systems, discovering logon accounts and passwords, and gaining access to network resources. Enumeration involves connecting to a remote system, not just identifying that a system is present on a network. Hackers aren’t satisfied with knowing that computer systems are running on a network; their goals are to find live systems and gain access to them. For security testers, enumeration is a more intrusive part of testing, and not having permission from the network’s owner for this step could result in being charged with a criminal offense. Be sure you have a Rules of Engagement (ROE), and written authorization (otherwise known as a “get out of jail free card”), and possibly a Statement of Work (SOW) in place to clearly define what actions you will be taking. During the enumeration process, you attempt to retrieve information and gain access to servers by using company employees’ logon accounts. Knowledge of operating systems and how they store information can be helpful in these activities. Not knowing how Windows and Linux handle shares and file permissions can make accessing information and finding possible vulnerabilities more difficult.

To determine what resources or shares are available on a network, security testers and ethical hackers must use port scanning and footprinting first to determine what OS is used along with what services are tied to that OS and the machine they are housed on. If a network is running a Windows-based environment, for example, you can use specific tools to view shares and possible access resources. As mentioned, enumeration is more intrusive because you're not just identifying a resource; you're attempting to access it to breach it. Enumeration goes beyond passive scanning of a network to find open ports. For example, sometimes this process entails guessing passwords after determining a username. In the activity below, you will use NBTscan (“NBT” stands for NetBIOS over TCP/IP), a tool for enumerating Windows OSs that’s part of the Kali Linux suite of security penetration testing tools.

During enumeration, you may stumble upon a remote Inter-Process Communication (IPC) share such as IPC$ in Windows, which they can probe further to connect to an administrative share by brute-forcing admin credentials and obtain complete information about the file system listing that the share represents.

The previous chapters have highlighted how you can gather the necessary information about your target without any illegal activities; however, enumeration activities may be illegal depending on the organization’s policies and the laws that are in effect. An ethical hacker or pentester should always acquire proper written authorization before performing any enumerating activities.

**Enumeration Techniques**

The following techniques are used to extract information about a target.

**Extract Usernames Using Email IDs**

Every email address contains two parts: a username and a domain name, in the format “username@domainname.”

**Extract Information Using Default Passwords**

Many online resources provide a list of default passwords assigned by manufacturers to their products. Users often ignore recommendations to change the default usernames and passwords provided by the manufacturer or developer of a product. This eases an attacker’s task of enumerating and exploiting their target system.

**Brute-Forcing Active Directory Environments**

Microsoft Active Directory (AD) is very susceptible to username enumeration at the time of user-supplied input verification. This is a known design error in the Microsoft Active Directory implementation. If a user enables the “logon hours” feature, then all of the attempts at service authentication result in different error messages. You can take advantage of this to enumerate valid domain usernames. An attacker who succeeds in extracting valid usernames can conduct a brute-force attack to crack the respective passwords.

**Extract Information Using DNS Zone Transfers**

A network administrator can use DNS zone transfers to replicate DNS data across several DNS servers or back up DNS files. For this purpose, the administrator needs to execute a specific zone transfer request to the Name Server (NS). If the name server permits zone transfers, it will cover all the DNS names and IP addresses hosted by that server to ASCII text.

If the network administrators did not configure the DNS server properly, the DNS zone transfer can be an effective method to obtain information about the target organization’s network. This information may include lists of all named hosts, sub-zones, and related IP addresses. You can perform DNS zone transfers using nslookup (Windows) and dig (Linux) commands as well.

**Extract User Groups From Windows Domains**

To extract user groups from Windows, you should have a registered ID as a user in the Active Directory. You can then extract information from groups in which the user is a member by using the Windows interface or command-line method.

**Extract Usernames Using SNMP**

You can easily guess read-only or read-write community strings by using the SNMP application programming interface to extract usernames.

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/2 (13).png>)

FIGURE X: Techniques for enumeration.

**Services and Ports of Interest to Enumerate**

Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) manage data communications between hosts or nodes on a network.

TCP is a connection-oriented protocol capable of carrying messages or emails over the Internet. It provides a reliable multi-process communications service in a multi-networked environment. The features and functions of TCP include the following:

Supports acknowledgement for receiving data through a sliding window acknowledgement system

* Offers automatic retransmission of lost or acknowledged data
* Allows addressing and multiplexing of data
* A connection can be established, managed, or terminated

**Offers Quality of Service (QoS) transmissions**

UDP is a connectionless protocol that carries short messages over a computer network. It provides unreliable service and does not guarantee message delivery reliability; however, it is faster than its counterpart, TCP, because there is less overhead that UDP has to manage. The applications of UDP include applications such as audio streaming and videoconferencing and teleconferencing.

**Service Port Enumeration**

Services and TCP/UDP ports that can be enumerated include the following:

**TCP/UDP 53: DNS Zone Transfers**

The DNS resolution process establishes communication between DNS clients and DNS servers. DNS clients send DNS messages to DNS server listening on UDP port 53. If the DNS message size exceeds the default size of UDP (512 octets), the response contains only the data that UDP can accommodate, and the DNS server sets a flag to indicate the truncated response. The DNS client can now resend the request via TCP over port 53 to the DNS server. In this approach, the DNS server uses UDP as a default protocol. IN the case of lengthy queries for which UDP fails, TCP is used as a failover solution. Malware such as the ADM worm and the Bonk Trojan uses port 53 to exploit vulnerabilities within DNS servers, providing intruders a way to leverage DNS servers as a launchpad for further attacks.

**TCP/UDP 135: Microsoft RPC Endpoint Mapper**

Remote Procedure Call (RPC) is a protocol used by a client system to request a service from a server. An endpoint is the protocol port on which the server listens for the client’s RPCs. The RPC Endpoint Mapper enables RPC clients to determine the port number currently assigned to a specific RPC service. There is an inherent flaw in the part of RPC that exchanges messages over TCP/IP. The incorrect handling of malformed messages causes this failure. This affects the RPC Endpoint Mapper, which listens on TCP/IP port 135. This vulnerability could allow an attacker to send RPC messages to the RPC Endpoint Mapper process on a server to launch a denial of service (DoS) attack.

**UDP 137: NetBIOS Name Service (NBNS)**

NBNS, also known as the Windows Internet Naming Service (WINS), provides a name resolution service for computers running NetBIOS. NetBIOS name servers maintain a database of the NetBIOS names for hosts and the corresponding IP address the host is using. NBNS aims to match IP addresses with NetBIOS names and queries. Attackers usually attack the name service first. Typically, NBNS uses UDP 137 as its transport protocol. It can also use TCP 137 as its transport protocol for a few operations, though this might never occur in practice.

**TCP 139: NetBIOS Session Service (SMB over NetBIOS)**

TCP 139 is perhaps the most well-known Windows port. It is used to transfer files over a network. Systems use this port for both null-session establishment as well as file and printer sharing. A system administrator considering the restriction of access to ports on a Windows system should make the restriction of TCP 139 a top priority. An improperly configured TCP 139 port can allow an intruder to gain unauthorized access to critical system files or the complete file system, resulting in data theft or other malicious activities.

**TCP/UDP 445: SMB over TCP (Direct Host)**

Windows supports file- and printer-sharing traffic using the SMB protocol directly hosted on TCP. In earlier versions of Windows, SMB traffic required the NetBIOS over TCP (NBT) protocol to work on TCP/IP transport. Directly hosted SMB traffic uses port 445 (TCP and UDP) instead of NetBIOS.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/3 (13).png>)

FIGURE X: Service ports to enumerate.

**UDP 161: Simple Network Management Protocol (SNMP)**

SNMP is widely used in network management systems to monitor network-attached devices such as routers, switches, firewalls, printers, and servers. It consists of a manager and agents deployed to endpoints that, in turn, communicate back to the manager or the “mothership.” The agent receives requests on port 161 from the managers and responds to the managers using port 162.

**TCP/UDP 389: Lightweight Directory Access Protocol (LDAP)**

LDAP is a protocol for accessing and maintaining distributed directory information services over an IP network. By default, LDAP uses TCP or UDP as its transport protocol over port 389.

**TCP 2049: Network File System (NFS)**

NFS protocol is used to mount file systems on a remote host over a network, and users can interact with the file systems as if they are mounted locally. NFS servers listen to its client systems on TCP port 2049. If NFS services are not properly configured, then attackers may exploit the NFS protocol to gain control over a remote system, perform privilege escalation, inject backdoors or malware on a remote host and more.

**TCP 25: Simple Mail Transfer Protocol (SMTP)**

SMTP is a TCP/IP mail delivery protocol. It transfers email across the internet and across LANs and WANs. It runs on the connection-oriented service provided by the TCP protocol and uses the well-known port number 25. The below table lists some commands used by SMTP and their respective syntaxes.

| SMTP Command | SMTP Header Information   | Description                                                                   |
| ------------ | ------------------------- | ----------------------------------------------------------------------------- |
| Hello        | HELO \<sending-host>      | Identifies the sending mail server at the start of an SMTP session.           |
| From         | MAIL FROM:\<from-address> | Specifies the sender’s email address, initiating the email sending process.   |
| Recipient    | RCPT TO:\<to-address>     | Specifies the recipient’s email address for email delivery.                   |
| Data         | DATA                      | Indicates readiness to send the email body, including headers and content.    |
| Reset        | RSET                      | Aborts the current mail transaction and resets the SMTP session.              |
| Verify       | VRFY\<string>             | Verifies if a specified user or mailbox exists on the server.                 |
| Expand       | EXPN\<string>             | Expands a mailing list to show individual member addresses.                   |
| Help         | HELP\[string]             | Requests help information from the server, optionally for a specific command. |
| Quit         | QUIT                      | Terminates the SMTP session, closing the connection.                          |

**TCP/UDP 162: SNMP Trap**

An SNMP trap uses TCP/UDP port 162 to send notifications such as optional variable bindings and the sysUpTime value from an agent to a manager.

**UDP 500: Internet Security Association and Key Management Protocol (ISAKMP)/Internet Key Exchange (IKE)**

Internet Security Association and Key Management Protocol (ISAKMP)/Internet Key Exchange (IKE) is a protocol used to set up a Security Association (SA) in the IPSec protocol suite. It uses UDP port 500 to establish, negotiate, modify, and delete Sas and cryptographic keys in a virtual private network (VPN) environment.

**TCP 22: Secure Shell (SSH)**

Secure Shell (SSH) is a command-level protocol mainly used for managing various networked devices securely. It is generally used as an alternative protocol to the unsecure Telnet protocol. SSH uses the client/server communications model, and the SSH server, by default, listens to its client on TCP port 22. Attackers may exploit the SSH protocol by brute-forcing SSH login credentials.

**TCP/UDP 3268: Global Catalog Service (GCS)**

Microsoft’s Global Catalog Service (GCS), a domain controller that stores extra information, uses port 3268. Its database contains rows for every object in the entire organization, instead of rows for only the objects in one domain. Global Catalog allows one to locate objects from any domain without having to known the domain name. LDAP in the Global Catalog server uses port 3268. This service listens to port 3268 through a TCP connection. Administrators use port 3268 for troubleshooting issues in the Global Catalog by connecting to it using LDAP.

**TCP/UDP 5060, 5061: Session Initiation Protocol (SIP)**

The Session Initiation Protocol (SIP) is a protocol used in Internet telephony for voice and video calls. It typically uses TCP/UDP port 5060 (non-encrypted signaling traffic) or 5061 (encrypted traffic with TLS (Transport Layer Security)) for SIP to servers and other endpoints.

**TCP 20/21: File Transfer Protocol (FTP)**

FTP is a connection-oriented protocol used for transferring files over the Internet or within local, or private networks. FTP is controlled on TCP port 21, and for data transmissions, FTP uses TCP port 21. If attackers identify that FTP server ports are open, they can perform enumeration on FTP to find information such as the software version and state of existing vulnerabilities to perform further exploitations such as the sniffing of FTP traffic and FTP brute-force attacks.

**TCP 23: Telnet**

The Telnet protocol is used for managing various networked devices remotely. It is an unsecure protocol, however, as it sends and transmits login credentials in cleartext format; therefore, it is mostly used in private networks. The Telnet server listens to its clients on port 23. Attackers can take advantage of the Telnet protocol to perform banner grabbing attacks on other protocols such as SSH and SMTP, brute-forcing attacks on login credentials, port-forwarding attacks, and many more.

**UDP 69: Trivial File Transfer Protocol (TFTP)**

TFTP is a connectionless protocol used for transferring files over the internet, or within local or private networks. TFTP depends on connectionless UDP; therefore, it does not guarantee the proper transmission of the file to the intended destination. TFTP is mainly used to update or upgrade software and firmware on remote networked devices. It uses UDP port 69 for transferring files to a remote host. Attackers may exploit TFTP to install malicious software or firmware on remote devices.

**TCP 179: Border Gateway Protocol (BGP)**

BGP is widely used by Internet Service Providers (ISPs) to maintain huge routing tables and for efficiently processing Internet traffic. BGP routers establish sessions on TCP port 179. The misconfiguration of BGP may lead to various attacks such as dictionary attacks, resource-exhaustion attacks, flooding attacks, and hijacking attacks.

To defend against these enumeration techniques, organizations should implement robust monitoring and alerting systems, regularly update and patch systems, enforce strict access controls, and educate employees on safe browsing and network hygiene practices.

**Enumeration Methodology**

In the hacking world, you will soon come to know and become very familiar with the enumeration process. The enumeration process requires a systematic approach to collecting data about a target system or network. This process aims to uncover potential vulnerabilities, pinpointing the most vulnerable entry points or attack vectors to establish initial access. Us hackers utilize a variety of methods throughout this phase to meet certain objectives. Typically, the enumeration phase occurs early in the hacking lifecycle, often aligning with the third or fourth stage, although the exact sequence can differ based on the hacking methodology employed. It’s important to note that regardless of the methodology, enumeration should commence early due to its critical role in understanding the technical specifics of the target environment.

For effective enumeration, adhering to recommended best practices is essential. While there’s flexibility in the order of execution, touching upon most of these practices will significantly enhance the success rate of the enumeration process. Here is a detailed list of the enumeration steps and the hacker’s objectives for each:

**Identification of Targets**

* **Your Objective:** To identify the systems or networks that are potential targets for an attack.
* **Your Goal:** Utilize reconnaissance techniques such as footprinting and open-source intelligence (OSINT) to gather information about the target. This can involve searching for the target's IP addresses, domain names, and other identifiers on the internet.

**Port Scanning**

* **Your Objective:** To discover open ports and services running on the target system, which could potentially be exploited.
* **Your Goals:** Use tools like Nmap or Nessus to scan the target's IP address range for open ports. Various scanning techniques such as SYN scanning, FIN scanning, and UDP scanning can be employed to avoid detection and gather information about the target's services and applications.

**System Fingerprinting**

* **Your Objective:** To identify the operating system and software versions running on the target system, which can reveal known vulnerabilities.
* **Your Goals:** Perform banner grabbing by connecting to common services (like HTTP, FTP, SMTP) and analyzing the responses to determine the software versions. Tools like Nmap can also be used for active and passive OS fingerprinting to identify the target's operating system.

![A diagram of a system

Description automatically generated](<../.gitbook/assets/4 (12).png>)

FIGURE X: Enumeration methodology.

**Identification of System Components, Services, Web Servers, and Operating Systems**

* **Your Objective:** To gather detailed information about the target's hardware, software, and network configurations.
* **Your Goals:** Use advanced enumeration techniques to extract information from the target. This can include querying DNS records for subdomains, enumerating SMB shares, and leveraging protocols like SNMP to gather configuration details. Tools like Metasploit can automate some of these tasks.

**Identification of Perimeter Devices and Operating Systems**

* **Your Objective:** To identify firewalls, routers, and other perimeter devices that protect the target network, along with their configurations.
* **Your Goals** Employ techniques such as ping scanning to discover live hosts and network devices. Tools like Nmap can be used to identify the operating systems of these devices, which can reveal potential vulnerabilities or misconfigurations.

The enumeration process is crucial for hackers as it lays the groundwork for subsequent stages of an attack, such as gaining unauthorized access or exploiting vulnerabilities. By carefully identifying targets, scanning ports, fingerprinting systems, and enumerating services and devices, hackers aim to gather comprehensive information about the target environment. This information can then be used to craft targeted attacks, bypass security measures, and exploit weaknesses to achieve their objectives.

### NetBIOS Enumeration

This section describes NetBIOS enumeration, the information obtained, and various NetBIOS enumeration tools. NetBIOS is considered first for enumeration because it extracts a very large amount of information about a target network, such as users and network shares. Before we dive into enumeration tooling techniques, it is first important to understand the inner workings of the NetBIOS protocol so that you can have a firm understanding of how the tools work, relate, and correspond to the core functionalities of the NetBIOS protocol.

### Understanding the NetBIOS Protocol

Short for _**NetBIOS,**_ the _**Network Basic Input/Output System,**_ might sound like a relic from the past (actually it is, but technically it is still in vast use today). It holds a significant place in the history of networking, and contrary to popular belief, NetBIOS is not a protocol itself, but a program designed to facilitate communications between applications across a _**Local Area Network (LAN).**_ Despite its age, understanding NetBIOS remains crucial for anyone involved in hacking, network administration, or network security.

#### NetBIOS Origins and Adoption

Originally developed by IBM, NetBIOS was later embraced by Microsoft, leading to its widespread adoption and eventual status as an industry standard. Its compatibility spans across Ethernet and Token Ring networks, showcasing its versatility and longevity in the field of hacking and networking.

#### Modern Relevance

Even in today’s digital landscape dominated by newer protocols and standards, NetBIOS finds its place within the Windows operating system. Users interacting with network settings will encounter references to NetBIOS, particularly under the _“clients for Microsoft networks”_ section, where file and print services can be managed.

#### Security Considerations

The importance of recognizing NetBIOS extends beyond historical interest. It highlights the necessity of understanding the applications and services running on networked devices, including those that might be accessed via removable storage like USB drives. This awareness is crucial for securing network environments against unauthorized access or malicious activities.

**Note: Remember, not only is it important to know what applications are on target machines, but also what users can run from a thumb drive.**

#### Compatibility and Enumeration

While some functionalities related to NetBIOS might not be supported on newer operating systems, such Windows 7 and above, older systems remain operational in many networks. This diversity necessitates a comprehensive approach to network security and management.

To explore or enumerate NetBIOS-related information, the **nbtstat** utility is an invaluable tool. Available on all Windows systems, nbtstat can be invoked with the -A \<Target IP Address> command to reveal the services running on a target system, along with group memberships and domain affiliations.

**Note: For the detailed functions of nbtstat, simply type nbtstat in the command prompt.**

![A computer screen with white text

Description automatically generated](<../.gitbook/assets/5 (12).png>)

_**FIGURE X:** Results of the nbtstat command output._

Despite its age, NetBIOS remains a pertinent topic in networking and security discussions. Its legacy underscores the importance of understanding foundational technologies and their implications on modern network infrastructures. Whether for educational purposes, network troubleshooting, or security assessments, a grasp of NetBIOS and its associated tools like nbtstat offers valuable insights into the workings of networked environments.

**Enumerating NetBIOS**

The first step in enumerating a Windows system is to take advantage of the NetBIOS API. NetBIOS was originally developed as an API for client software to access local area network (LAN) resources. Windows uses NetBIOS for file and printer sharing and the NetBIOS name is a unique 16-character ASCII string assigned to Windows systems to identify network devices over TCP/IP; 15-characters are used for the device name, and the 16th is reserved for the service or record type. NetBIOS provides the following three services:

* **Naming Service (UDP 137):** Provides name registration and the resolution of constituent systems.
* **Datagram Service (UDP port 138):** Provides fast, connectionless transmission where reliability is not of utmost importance.
* **Session Service** **(TCP port 139):** Used for reliable connection between two systems.

Attackers usually target the NetBIOS service because it is easy to exploit and run on Windows systems even when not in use.

In addition, NetBIOS enumeration can provide you with the following information:

* List of systems in a domain
* File sharing
* Print servers
* Policies
* Passwords

Attackers use NetBIOS enumeration to obtain the following:

* The list of computers that belong to a domain
* The list of shares on the individual hosts in a network
* Policies and passwords

An attacker who finds a Windows systems with port 139 open can check to see which resources can be accessed or viewed on a remote service; however, to enumerate the NetBIOS names, the remote system must have enabled file and printer sharing. NetBIOS enumeration may allow an attacker to read or write to a remote computer system, depending on the availability of shares, or launch a DoS attack.

| NetBIOS Suffix | Description                | Type   | Information Obtained                                                                            |
| -------------- | -------------------------- | ------ | ----------------------------------------------------------------------------------------------- |
| <00>           | Workstation Service Name   | UNIQUE | Hostname                                                                                        |
| <03>           | Messenger Service Name     | UNIQUE | Domain name                                                                                     |
| <1B>           | Domain Master Browser Name | UNIQUE | Messenger service running on the computer                                                       |
| <06>           | Remote Access Service      | UNIQUE | Messenger service running for the logged-in user                                                |
| <20>           | File Service               | UNIQUE | Server service running                                                                          |
| <21>           | Remote Access Client       | UNIQUE | Master browser name for the subnet                                                              |
| <1D>           | Master Browser             | UNIQUE | Domain master browser name, which identifies the primary domain controller (PDC) for the domain |
| \<domain>      | <1E>                       | GROUP  | Browser service elections                                                                       |

TABLE X: NetBIOS name list.

**Note: Microsoft does not support NetBIOS name resolution for IPv6.**

### nbtstat

nbtstat is a Windows utility that helps in troubleshooting NetBIOS name resolution problems. The nbtstat command removes and corrects preloaded entries using several case-sensitive switches. Attackers use nbtstat to enumerate information such as NetBIOS over TCP/IP (NetBT) protocol statistics, NetBIOS name tables for both local and remote computers, and the NetBIOS name cache.

The syntax of the nbtstat command is as follows:

nbtstat \[-a RemoteName] \[-A IP Address] \[-c] \[-n] \[-r] \[-R] \[-RR] \[-s] \[-S] \[Interval]

The table shown below lists various nbtstat parameters and their respective functions.

| nbtstat Parameter | Function                                                                                                                               |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| -a RemoteName     | Displays the NetBIOS name table of a remote computer, where RemoteName is the NetBIOS computer name of the remote computer.            |
| -A IP Address     | Displays the NetBIOS name table of a remote computer, specified by the IP address (in dotted decimal notation) of the remote computer. |
| -c                | Lists the content of the NetBIOS name cache, the table of NetBIOS names and their resolved IP addresses.                               |
| -n                | Displays the names registered locally by NetBIOS applications such as the server and the redirector.                                   |
| -r                | Displays a count of all names resolved by a broadcast or WINS server.                                                                  |
| -R                | Purges the name cache and reloads all #PRE-tagged entries from the lmhosts file.                                                       |
| -RR               | Releases and re-registers all names with the name server.                                                                              |
| -s                | Lists the NetBIOS sessions table converting destination IP addresses to computer NetBIOS names.                                        |
| -S                | Lists the current NetBIOS sessions and their status with the IP addresses.                                                             |
| Interval          | Re-displays selected statistics, pausing at each display for the number of seconds specified in interval.                              |

TABLE X: nbtstat parameters and their respective functions.

The following are some examples for nbtstat parameters and commands:

* The nbtstat command nbtstat -a \<IP address of the remote machine> can be executed to obtain the NetBIOS name table of the remote computer.

![](<../.gitbook/assets/6 (12).png>)

FIGURE X: nbtstat -a command output.

The nbtstat command nbtstat -c can be executed to obtain the contents of the NetBIOS name cache, the table of NetBIOS names, and their resolved IP addresses

.

![](<../.gitbook/assets/7 (11).png>)

FIGURE X. nbtstat command to obtain the content of the NetBIOS name table.

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/8 (11).png>)

**Enumerating Windows Operating Systems**

To understand how an attacker might gain access to resources or shares on a Windows network, we will have a brief discussion on Windows OSs and as they relate to enumeration. By default, little information can be enumerated from Windows systems after Windows 7. The table below describes Windows OSs from Windows 95 to Windows Server 2019.

**Windows OS Descriptions**

| Windows OS Version                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows 95                                 | The first Microsoft GUI product that doesn’t rely on DOS, Windows 95 is the beginning of plug and play and the ActiveX standard used in all Windows versions today. A major enhancement is the Registry, a database storing information about the system’s hardware and software. Previously, this information was stored in text files. Windows 95 runs on standalone and networked computers and uses the FAT16 file system. Version OSR2 adds support for the FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Windows 98 and Me                          | Compared to their predecessors, these versions have an improved file system (FAT32), new hardware support, and better backup and recovery tools. The enumeration process for Windows Me is the same as for Windows 98.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Windows NT 3.51 Server/Workstation         | These operating systems were created with security and enhancement of network functionality in mind. They emphasize domains instead of workgroups and use the client/server model instead of peer-to-peer networks; the server is responsible for authenticating users and giving them access to network resources. The client/server model also allows for having many computers in a domain instead of the limited number of computers in a workgroup. NTFS\* replaces FAT16\* and FAT32\* because of the difficulty in incorporating security in the earlier file systems. NTFS includes file-level security features not possible in FAT.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Windows NT 4.0 Server/Workstation          | These upgrades to Windows NT 3.51 have improved GUIs and performance.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Windows 2000 Server/Professional           | In this major upgrade to NT, Microsoft includes Active Directory (AD) for object storage. AD is more scalable than other available solutions for managing large networks. It uses the _**Lightweight Directory Access Protocol (LDAP)**_, which is still in use today. Also, this update includes the first version of the _**Microsoft Management Console (MMC)**_ and _**Encrypted File System (EFS)**_. Enumeration of these OSs includes enumerating Active Directory.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Windows XP Professional                    | This OS includes Windows 2000 features, such as standards-based security, improved manageability, and MMC. In addition, Windows XP has an improved user interface and better plug-and-play (PnP) support. Security improvements in the kernel data structures make them read-only to prevent rogue applications from affecting the OS core, and Windows File Protection is added to prevent overwriting core system files. With Service Pack 2 (SP2), security is improved further with features such as _**Data Execution Prevention (DEP)**_ and a firewall enabled by default. DEP fixes a security exposure caused by vulnerable running services that malicious actors often use to perform buffer overflow attacks, and the firewall now in place makes it even more difficult for malicious actors to exploit Windows service vulnerabilities and enumerate shares and services. In fact, enumeration of Windows XP SP2 and later systems can be difficult without modifying the actual configuration. Disabling the Windows Firewall is common in corporate networks, but this practice leaves an additional attack surface open for malicious actors to use to enter the network. In these environments, the enumeration processes used for earlier versions of Windows still work much the same way in Windows XP Professional. |
| Windows Server 2003                        | Windows Server 2003 includes improvements over Windows 2000 in some security areas, such as _**Internet Information Services (IIS)**_, and comes in four editions. Generally, all editions include _**Remote Desktop Protocol (RDP)**_, load balancing, VPN support, management services such as _**Windows Management Instrumentation (WMI)**_ and .NET application services. The higher-end editions offer better support for _**Public Key Infrastructure (PKI)**_, certificate services, and Active Directory as well as enhancements to reliability, scalability, manageability, and security. Even with improvements in security and stability, enumeration techniques described for other Windows versions are effective within Windows Server 2003.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Windows Vista                              | Vista comes in several editions and is the first version to introduce _**User Account Control (UAC)**_ and built-in full drive encryption, called BitLocker (available in Vista Enterprise and Ultimate editions). UAC allows running Vista in nonprivileged mode to prevent unwanted code or user actions from damaging or controlling the computer (maliciously or inadvertently); however, UAC has been widely criticized because of its intrusive security prompts that force many users to disable it. In Windows 7, you can configure the frequence of these prompts. Also introduced in this release is _**Address Space Layout Randomization (ASLR)**_, which makes exploitation of overflow-type vulnerabilities much more difficult. By default, Vista in a standalone environment can be difficult to enumerate without modifying its configuration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Windows Server 2008                        | This OS features security options similar to Vista, including BitLocker drive encryption and UAC. Vista and Windows Server 2008 support _**Network Access Protection (NAP)**_ which reduces the possibility of rogue systems being able to access network resources, features, and services, and roles in Windows Server 2008 can be fine-tuned to meet specific needs. A command-line version that requires fewer resources, called Server Core, is available for certain server roles. This version is designed to reduce maintenance, use of resources, and the attack surface. Hyper-V, a full-featured virtualization product, is included with Windows Server 2008 and allows installing guest OSs, such as Linux and other Windows versions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Windows 7                                  | Windows 7 builds on the security advances made in Vista with the introduction of _**AppLocker**_, which allows for control over application execution, including the Action Center in Windows 7 which allows users to view potential configurations in one simple interface. Other improvements include refinements to the UAC feature and Windows Defender, which protect the system from known spyware.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Windows 8.1                                | Boasting “groundbreaking malware resistance,” Windows 8.1 comes with features that make user-level interactions much less dangerous by limiting the privileges of basic users. In addition, Windows 8.1 includes several heap integrity checks designed to make exploitation more difficult. Upgrades to Windows Defender make it a full anti-malware product. SmartScreen is extended for the OS to display an alert when an application is launched on a PC. For the first time, SecureBoot prevents execution of non-trusted boot content, preventing rootkits/bootkits.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Windows Server 2012                        | With this edition, Microsoft introduces _**Authentication Silos**_ to prevent _**Pass-the-Hash (PtH) attacks**_, a major weakness in all earlier versions of Windows servers. It also includes enhanced support for _**Domain Name System Security Extensions (DNSSEC)**_, which relies on digital signatures to prove zone ownership.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Windows 10                                 | Designed for use on tablets, gaming consoles, and traditional PCs, Windows 10 can be found in more places than ever. Numerous security enhancements were brought to Windows 10. One of the more aggressive enhancements is that it only allows trusted apps by default through the _**Device Guard**_. It also adds _**Credential Guard**_, which uses virtualization to protect access tokens from theft by attackers. Originally released in 2015, Windows 10 has improved through many features and security enhancements. Windows 10 was supposed to be the last name change for Windows, but as we know all, we now have Windows 11.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Windows Server 2016                        | Windows Server 2016 features a number of security upgrades. The most important, _**Windows Containers**_, allows for application isolation to protect applications form one another. Windows Defender (malware protection) is now enabled by default. In this version, the option for Telnet server is eliminated completely, so it’s ultimately the users choice to enable or disable that feature. It comes disabled by default. A feature named _**Just Enough Administration (JEA)**_ allows for more detailed access control settings on scheduled tasks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Windows Server 2019                        | Windows Server 2019 was developed concurrently with Windows 10. It contains a number of new features and security measures including container services, storage spaces direct, storage migration services, storage replication, shieled virtual machines, and improved Windows Defender _**Advanced Threat Protection (ATP)**_.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Coming soon to a city near you: Windows 12 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

**Note: Many of the enumeration techniques that work with older versions of Windows OSs still work with the newer versions.**

| <img src="../.gitbook/assets/9 (10).png" alt="Lightbulb and gear with solid fill" data-size="original"> | FYI: FOR YOUR INFORMATION |   |
| ------------------------------------------------------------------------------------------------------- | ------------------------- | - |
|                                                                                                         |                           |   |

**Enumeration Attacks**

Enumeration attacks, specifically _**Golden Ticket**_ attacks, are sophisticated techniques utilized by hackers to gain unrestricted access to an organization’s entire domain, including devices, files, and Active Directory domain controllers. This type of attack exploits the _**Kerberos**_ authentication protocol used within Windows networks, allowing hackers to bypass standard authentication checks and maintain persistent access to the network.

**Golden Ticket Attack Overview**

A Golden Ticket attack involves manipulating the Kerberos authentication protocol to create a forged _**Ticket Granting Ticket (TGT)**_. This forged ticket grants an individual the same privileges as a legitimate TGT, effectively providing them access to any service or machine within the domain. This attack targets the _**krbtgt**_ account which is a critical component of the Kerberos system responsible for encrypting and signing all domain tickets. By extracting the NTHash of the krbtgt account and identifying the domain’s _**Security Identifier (SID),**_ individuals can craft a Golden Ticket that replicates the domain administrator’s privileges.

**Golden Ticket Execution Process**

To provide you with a general idea of how Kerberos Golden Ticket attacks work, consider the following:

1. **Initial Breach:** The Golden Ticket attack begins with an initial breach of a target information system, often targeting a _**tier 0**_ asset or an account tied to the built-in Domain Admins group. This initial compromise is a vital part of the attack for obtaining the necessary privileges to proceed with the attack.
2. **Privilege Escalation:** After breaching the system, individuals escalate their privileges to that of a domain admin. This step is most essential for accessing the krbtgt account and extracting its NTHash.
3. **Extracting the NTHash;** The NTHash of the krbtgt account is obtained, usually from the _**Local Security Authority Subsystem Service (LSASS)**_ process or the NT Directory Services (NTDS.dit) file located on any Domain Controller (DC) within the domain. Tools like **Mimikatz** or **Impacket** can be used to perform this extraction.
4. **Crafting the Golden Ticket:** With the NTHash and the domain SID, individuals can craft a Golden Ticket. This ticket is a forged (illegal) Kerberos ticket that functions like a legitimate _**Ticket Granting Ticket (TGT),**_ often replicating the domain administrator’s privileges.
5. **Utilization:** The crafted Golden Ticket, in turn, provides individuals with extensive and enduring access to the target network, allowing them to move undetected and unrestricted across the domain.

![](<../.gitbook/assets/10 (10).png>)

FIGURE X: Understanding the importance of Tier 0 assets.

**Golden Ticket Mitigation Strategies**

To mitigate the risk of Golden Ticket attacks, as an ethical hacker knowledgeable about this particular attack and the way it functions, need to guide client organizations to implementing several security measures to protect against this type of attack. Mitigating strategies may include:

* **Rigorous Password Policies:** Enforce strong and regularly updated passwords for accounts, especially those with high privileges like the krbtgt account.
* **Network Activity Monitoring:** Guide your client into implementing continuous monitoring of network activities to detect unusual patterns that may indicate an attack.
* **Limit Access:** Restricting access to make it harder for individuals to obtain the password hash of the KRBTGT user.
* **Regular Audits:** Guide your client into cybersecurity best practices and good cybersecurity hygiene by conducting regular audits of privileged accounts and permissions to identify and rectify any unnecessary or excessive privileges. Implementing the _**principle of least privilege**_ and granting only the minimum permissions necessary for a user to complete their daily work tasks will lessen the attack surface thus making the task of account breach and compromise more difficult to complete.

This is only one example of the many attacks one can carry out against a target entity by using enumerating techniques; and one that can provide defenders with the necessary security implementations and countermeasures to thwart these types of attacks that most start with account breach via a weak or poorly configured password or password policy.

Now, let’s discuss enumeration weak points before exploring the tools, techniques, and processes to accomplish attack and defense executions and implementations.

**Weak Points of Enumeration**

When it comes to enumeration, hackers often seek out the most accessible vulnerabilities, akin to “low-hanging fruit” first. This approach focuses on identifying the simplest entry points, or attack vectors, first. Among the earliest targets for hackers are simple elements such as business cards and Windows groups, which can inadvertently expose sensitive information.

**Business Cards as Weak Points**

At first glance, a business card might seem totally harmless, containing only basic details such as one’s name, address, position, and company affiliation; however, the inclusion of an email address can prove problematic. Many organizations use directory services, including Active Directory, to manage usernames, which correspond to network login credentials. Typically, users log in using a format like ‘domain\username’ (e.g., domainkrack\ysilva), but directory services often also recognize email addresses in the form of username@domain.com (e.g., yourname@gmail.com).

For an attacker, obtaining a business card equates to acquiring half of the necessary information for unauthorized access: the login name. Given that email addresses are readily available on company websites, the primary concern shifts to the password aspect. Thus, a business card can serve as a valuable starting point for an attacker seeking to infiltrate a network via enumeration.

**Windows Groups Enumeration**

Windows groups, managed by an organization’s IT department, play a crucial role in controlling access to resources. These groups are assigned security identifiers (SIDs) and can include user accounts or other SIDs. When a user attempts to access a resource, their credentials are verified against the groups they belong to determine if they have the necessary permissions.

An attacker, in turn, can enumerate these Windows groups to identify which user accounts belong to specific groups, such as “marketing folks,” thereby gaining insight into the structure for an organization’s access control mechanisms. This enumeration can reveal the composition of departments and potentially uncover access rights to sensitive resources.

One key point to keep in mind is that both business cards and Windows groups represent early targets for attackers due to the ease with which they can reveal sensitive information unbeknownst to you. Business cards, despite appearing innocuous, can disclose email addresses that correspond to valid usernames within an organization’s directory services. Meanwhile, enumerating Windows groups can reveal the membership of user accounts across various departments, providing a roadmap for further penetration testing or exploitation efforts.

**Default Passwords: A Persistent Issue**

One of my greatest frustrations revolves around the widespread use of default passwords. It’s understandable why this happens – technology evolves rapidly, and sometimes the importance of changing default settings doesn’t register until after the fact, or after it’s too late. For instance, when purchasing a new router, the excitement of setting it up and connecting to the internet can overshadow the importance of changing the factory default credentials. This oversight leaves devices vulnerable to unauthorized access, as many devices ship with easily guessed default passwords.

The availability of databases listing default passwords further exacerbates the problem. While these resources are primarily useful for IT professionals needing quick access to common defaults, they also pose a risk if left unchanged. An attacker with access to such a database could easily find the default password for a device and attempt to gain unauthorized access.

**Network Ports and Services**

Recognizing the significance of certain ports and services is crucial for maintaining network security. Here’s a rundown of some key ones:

* **DNS (Domain Name System)** operates primarily on **port 53**, handling the translation of domain names to IP addresses.
* **SMTP (Simple Network Management Protocol),** used for email transmissions, runs on **port 25.**
* **Microsoft RPC (Remote Procedure Call)** endpoints communicate over **TCP port 135.**
* **Global Catalog Service (GCS),** a condensed version of Active Directory, queries **port 3286.**
* **NetBIOS Naming Service,** more commonly referred to as _**Windows Internet Naming Service (WINS)**_ translates computer names to IP addresses, utilizing **port 137** for both TCP and UDP translations.
* **LDAP (Lightweight Directory Access Protocol)** employed by directory services like Active Directory, operates on TCP and UDP **port 389.**
* **SMB (Server Message Block),** which facilitates sharing resources and folders, communicates over **TCP port 139.**
* **SNMP (Simple Network Management Protocol),** used for managing devices on IP networks, operates on **UDP port 161,** with **TCP port 445** also commonly associated with SMB.

Understanding these services and their corresponding ports is essential, not just for exams, but for everyday network management. While blocking these ports might limit functionality, it’s akin to avoiding freeways due to the increased risk of accidents. Instead, the focus should be on monitoring traffic at these ports closely, as unexpected activities could signal potential security issues. Ultimately, the challenge lies in balancing the convenience and functionality of these services with the imperative need for vigilant monitoring and proactive security measures.

**Addressing Default Password Vulnerabilities to Thwart Enumeration Attacks**

The reliance on default passwords is a recurring frustration, highlighting a concerning lack of awareness among users. A study highlighted by CNN in 2022 revealed that 90% of credit card readers were using the same default password, either 166816 or z66816. While this statistic serves as a wake-up call, it’s important to clarify that the goal is not to exploit these vulnerabilities but to underscore the pervasive nature of default settings across various devices and systems.

Defaults are a significant security concern due to their ubiquity. From servers and routers to smartphones and WiFi devices, the temptation to skip the configuration step and use default settings is vastly prevalent. This practice not only compromises security but also introduces vulnerabilities that can be exploited by malicious actors.

**Dangers of Complacency**

The mantra :complacency will be your downfall rings true in the context of default passwords. As technology continues to proliferate, from servers and desktops to mobile devices and networking equipment, the pressure to quickly set up and deploy these devices is immense. Often, this haste leads to the deployment of devices with default user accounts and passwords still intact.

It’s crucial never to leave default user accounts or passwords in place, regardless of the perceived insignificance of the device. Whether it’s a personal smartphone, a tablet, or a home router, the principle remains the same: **always change default settings immediately upon deployment!**

**Real-World Use Case: ATM Vulnerabilities**

A vivid example of the dangers posed by default settings involves an ATM incident where a traveler discovered an ATM screen prompting for a password before inserting their card. Attempting common default codes, the traveler eventually stumbled upon a successful combination, gaining access to the ATM’s administrative interface. Although their actions were ethical and reported to the store staff, this incident underscores the potential for misuse of default settings.

In this scenario, either a recent service visit had not been properly concluded, or a software glitch was at play. Regardless, the reliance on default settings exposed a vulnerability that could have been exploited for illicit financial gains. The reliance on default passwords and settings across various devices and system not only makes the job of enumeration for a malicious actor a lot easier because half of the legwork is already done, which, in turn, poses a significant security risk. It’s imperative to prioritize the removal of default credential settings and the adoption of strong, unique passwords, or two-factor and multifactor authentication implementations to safeguard against potential breaches. Awareness and vigilance are key to mitigating the risks associated with default settings and enhancing overall cybersecurity posture.

**NetBIOS Basics**

Before learning how to enumerate Microsoft systems, you need to review the basics of how Network Basic Input/Output System (NetBIOS) works. NetBIOS is a Windows programming interface that allows computers to communicate across a Local Area Network (LAN). Most Windows OSs use NetBIOS to share files and printers. NetBIOS listens on UDP port 137 (NetBIOS Name service) and 138 (NetBIOS Datagram service) and TCP port 139 (NetBIOS Session service). File and printer sharing in Windows also requires an upper-level service called Server Message Block (SMB), which runs on top of NetBIOS. In Windows 2000 and later, SMB listens on TCP port 445 and doesn’t need to use NetBIOS over TCP/IP unless support for older Windows versions is required.

**Note: Enumeration is a process of discovery. Using one enumeration tool may lead to a discovery that directs you to use another enumeration tool. For example, if you had used Nmap and learned that a device had UDP ports 137 and 138 and TCP port 139 (all the NetBIOS ports) open, you might then use a NetBIOS enumeration tool such as NBTscan to see what more you could discover about that device.**

The computer names you assign to Windows systems are called NetBIOS names and have a limit of 16 characters; the last character is reserved for a hexadecimal number (00 to FF) that identifies the service running on the computer; therefore, you can use only 15 characters for a computer name, and NetBIOS adds the last character automatically to identify the service that has registered with the OS. For example, if a computer is running the Server service, the OS stores this information in a NetBIOS table.

A NetBIOS name must be unique on a network. The table below lists the NetBIOS suffixes that correspond to the services, or resource-types, running on a computer. You don’t need to memorize all these suffixes. Malicious actors often exert more effort to attack computers identified as Domain Controllers because these systems store more information, including logon names for user accounts and network resources. You can perform an Internet search to find a more comprehensive list of NetBIOS suffixes.

| NetBIOS Name        | NetBIOS Name or Suffix | Information Obtained                                                                                                    |
| ------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| \<hostname>         | 00                     | The Workstation service registered the computer name (also called the NetBIOS name).                                    |
| \<hostname>         | 20                     | Registered by the Server service. A computer must have this service running to share printers and files over a network. |
| \<hostname>         | 22                     | Registered by the Microsoft Exchange Interchange service.                                                               |
| \<hostname>         | 23                     | Registered by the Microsoft Exchange Store service. A store is where mailboxes and public folders are stored.           |
| \<hostname>         | 24                     | Registered by the Microsoft Exchange Directory service.                                                                 |
| \<hostname>         | 87                     | Signifies that Microsoft Exchange Message Transfer Agent (MTA) is running on the computer.                              |
| \<domain name>      | 00                     | Indicates that Domain Name System (DNS) is running.                                                                     |
| \<domain name>      | 1C                     | Identifies the computer as a domain controller.                                                                         |
| \<iNet-Services>    | 1C                     | Indicates that IIS is running.                                                                                          |
| \<IS-computer name> | 00                     | Also indicates that IIS is running.                                                                                     |

**NetBIOS Null Sessions**

Historically, one of the biggest vulnerabilities of NetBIOS systems is a null session, which is an unauthenticated connection to a Windows computer that uses no logon and password values. Many enumeration tools covered in this chapter establish a null session to gather information such as logon accounts, group membership, and file shares from an attacked computer. This vulnerability has been around for more than a decade and is still present in Windows XP. Null sessions have been disabled by default in Windows Server 2003, although administrators can enable them if they are needed for some reason.

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/11 (9).png>)

In Windows Vista and Server 2008, null sessions aren’t available and can’t be enabled, even by administrators. You might ask, “Why are we talking about these ancient operating systems? Who even uses Windows XP anymore?” (For one, I do – for testing and hacking purposes). You would be surprised. If you as an ethical hacker find an older operating system, you have just discovered a major security vulnerability as these operating systems are no longer supported and do not receive security updates. Your courses of action include upgrading the operating system, isolating the vulnerable ancient OS so it is not connected to any networks, or decommissioning the system.

**NetBIOS Enumeration Tools**

NetBIOS enumeration tools explore and scan a network within a given range of IP addresses and lists of computers to identify security loopholes or flaws in networked systems. As mentioned previously, the tools listed below also enumerate operating systems (OSs), users, groups, Security Identifiers (SIDs), password policies, services, service packs, and hotfixes, NetBIOS shares, transports, sessions, disks, and security event logs, and way more.

The nbtstat command is a powerful enumeration tool included with all versions of Windows. To display the NetBIOS table, you issue the nbtstat -a IPaddress command. If you want to run NetBIOS locally, the command is nbtstat-s. The figure below shows the entry LON-DC1. The 20 represents the Server service running on the LON-DC1 computer. The NetBIOS table also shows that ADATUM is a domain controller, as indicated by the 1C suffix.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/12 (9).png>)\
FIGURE X: nbtstat command output.

Another built-in Windows tool is the net view command, which gives you a quick way to see whether there are any shared resources on a computer or server. To display the syntax for this command, type net view ?. Using the net view command, a malicious aactor can view remote shares, as shown in the figure below.

You can also use the IP address of computers you discovered with port scanning tools. For example, the figure below shows the command used on a remote Windows 10 computer. A share name called wow is displayed. The next command an attacker could use against this computer is \\\mindhackdivathinkpad32gb\wow to explore the share drive and look for interesting files.

Although you can download or buy enumeration tools, you should learn how to take advantage of the tools available in Windows as well. A simple command-line utility can give you the name of a logged-on user, and a guess of that user’s password can give you access to the system quickly. Many password-cracking programs can determine a password ina matter of seconds. A quick Internet search will reveal many free password-craking programs you can try; however, hackers can often guess passwords without needing a special program because some users are careless when creating passwords. For example, many users, despite the guidelines in company security policies, use simple passwords, such as “password” or p@\$$w0rd. Some systems also have the default logon credentials that users often neglect to change, such as a username of “admin” with a password that is also “admin.” You can find lists of default credentials for various devices online. Many password-cracking programs mentioned earlier can be used to brute-force and attempt thousands of logons using dictionaries and wordlists containing thousands of password combinations. These directories include well-known poor passwords (like password1234) and well-known default credentials such as “admin” or “administrator.”

![](<../.gitbook/assets/13 (9).png>)

FIGURE X: net view command output.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/14 (9).png>)

FIGURE X: Using the net view command with a hostname.

**Additional Enumeration Tools**

**enum4linux**

As you have seen, several built-in Windows tools can assist you in enumerating NetBIOS systems. One of these tools is enum4linux, a tool for enumerating information from Windows and Samba systems. It is written in Perl and uses the Samba tools smbclient, rpclient, net, and nmblookup. Because enum4linux is written in Perl, you must run it on a system that supports Perl, such as Kali Linux OS.

**Key Features**

* RID cycling (When RestrictAnonymous is set to 1)
* User listing (When RestrictAnonymous is set to 0)
* Listing of group membership information
* Share enumeration
* Detecting if host is in a workgroup or a domain
* Identifying the remote operating system
* Password policy retrieval (using polenum)

Enum4linux enumerates information from Windows and Samba systems. It attempts to offer similar functionality to enum.exe. The tool usage can be found below followed by examples.

**Dependencies**

You will need to have the Samba package installed as this script is basically just a wrapper around a rpcclient, net, nmblookup, and smbclient.

**Usage**

![](<../.gitbook/assets/15 (9).png>)

**Examples**

Below are examples which demonstrate most of the features of enum4linux. Output has been edited for brevity.

**Verbose Mode**

Before we dive into the features of enum4linux, it’s worth pointing out that verbose mode shows you the underlying commands being run by enum4linux (rpcclient, smbclient, and more). This is useful if you want to use the underlying commands manually, but can’t figure out the syntax to use. Note the lines beginning with \[V] in the output below:

![A computer screen shot of a program code

Description automatically generated](<../.gitbook/assets/16 (9).png>)

**The “Do Everything” Option**

As you read through the following section, you’ll probably think that there are many options you need to remember; however, that is not the case. If you just want enum4linux to try to enumerate all of the information it can from a remote host, just use the -a option.

![](<../.gitbook/assets/17 (8).png>)

Note: This doesn’t perform dictionary-based shared name guessing, but it does pretty much everything else.

**Obtain List of Usernames (RestrictAnonymous = 0)**

This feature is similar to enum.exe -U IP. It returns a complete list of usernames if the server allows it. On Windows 2012 and above, the RestrictAnonymous registry setting must be set to 0 (disabled) for this feature to work. The user list is shown twice in two different formats because type different underlying commands are used to retrieve the data.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/18 (8).png>)

**Obtain a List of Usernames (Using Authentication)**

If you’ve managed to obtain a username and password for the target host, you can use it to retrieve a complete list of users regardless of the RestrictAnonymous settings. In the example below, I used the administrator account, but any account will do.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/19 (6).png>)

**Obtaining a List of Usernames via RID Cycling (RestrictAnonymous = 1)**

To obtain the usernames corresponding to a default range of RIDs (500-550, 1000-1050) use the -r option:

![A computer screen shot of a computer

Description automatically generated](<../.gitbook/assets/20 (4).png>)

You can specify a custom range of RIDs using the -R option. This implies -r, so there is no need for you to specify the -r option.

Before RID cycling can start, enum4linux needs to get the SID from the remote host. It does this by requesting the SID of a known username or group (no deviation from normal RID-cycling processes). You can see in the above output a list of known usernames. These are tried in turn, until enum4linux finds the SID of the remote host.

If you’re very unlucky, this list won’t be good enough and you won’t be able to get the SID. In this case, use the -k option to specify a different known username:

You can specify a list using commas:

**Group Membership**

If the remote host allows it, you can get a list of groups and their members using the -G option (like in enum.exe):

As with the -U option for user enumeration, you can also specify -u user -p pass to provide login credentials if required. Any user account will do, you don’t have to be an admin.

**Host and Domain Workgroups**

Enum4linux uses rpcclient’s lsaquery command to ask for a host’s domain SID. If we get a proper SID, we can infer that it is part of a domain. If we get the answer S-0-0, we can infer the host is part of a workgroup. This is done by default, so no command line options are required:

**Getting nbtstat Information**

The -n option causes enum4linux to run nmblookup and does some extra parsing on its output to provide human-readable information about the remote host.

**Listing Windows Shares**

If the server allows it, you can obtain a complete list of shares with the -S option. This uses smbclient under the bonnet which also grabs the browse list. Enum4linux will also attempt to connect to each share with the supplied credentials (null session); however, you could use -u user -p pass). It will then report whether it could connect to the share and whether it was possible to retrieve directory listings.

Some hosts won’t let you retrieve share lists. In these situations, it is still possible to perform a dictionary attack to guess share names. Below, is a demonstration detailing the -s option failing:

The output below shows the use of the -s option with a dictionary file guessing the names of shares identified:

**Getting OS Information**

The -o option retrieves operating system information using the smbclient command. Certain versions of Windows, such as the 2003 version, can return Service Pack (SP) information.

**Getting Printer Information**

You can retrieve information about networked printers known to the remote device using the -i option. This is useful for enumerating printers on a network that could possibly be vulnerable to port 80 or port 443 attacks and also providing an extra attack surface to enter the target network via vulnerable printer shares, or unsecured print servers.

**DumpSec**

DumpSec is a popular enumeration tool for Windows systems developed by Foundstone, now part of McAfee, designed to enumerate Windows systems for potential security vulnerabilities. It provides you detailed information about users, groups, permissions, services, shares, and other system configurations that could be exploited. By analyzing this data, you can identify weak points in a system’s security posture.

**Key Features of DumpSec**

User Enumeration: Lists all users on the system along with details such as account status, password age, and last login time.

Group Enumeration: Shows all groups on the systems and their members.

Permission Auditing: Analyzes file system permissions and registry permissions to identify potential security risks.

Service Enumeration: Lists services running on the system, including service names, display names, start types, and logon accounts.

Share Enumeration: Displays shared resources available on the system, including share name, path, and permissions.

Policy Auditing: Checks system policies like password policy, account lockout policy, and audit policy settings.

**How DumpSec Works**

DumpSec operates by querying Windows APIs (Application Programming Interfaces) to retrieve information about various aspects of a target system’s configuration. It does not exploit vulnerabilities, per se, but rather reports on configurations that could lead to vulnerability exploitation. It’s built as a read-only tool, meaning it does not modify system settings or configurations during its use and operation.

**Using DumpSec**

DumpSec is a command-line tool, so it’s operated through the Windows Command Prompt or the PowerShell terminal. Some examples of how to use the DumpSec tool for various tasks are detailed below:

**Enumerating Users**

To enumerate all users on the system, simply run DumpSec without any arguments:

dumpsec /users

This command lists all local user accounts along with details such as full name, description, and account status.

**Enumerating Groups**

To list all groups on the system and their members, use the following command:

dumpsec /groups

This provides information about each group, including members and group types.

**Auditing File System Permissions**

To audit permissions on the file system, specify the directory path after the /rfga switch:

dumpsec /rfga=”C:\path\to\directory”

This will display the permissions set on the specified directory, including who has what kind of access.

**Auditing Registry Permissions**

Similarly, to enumerate registry permissions, use the /rfga switch followed by the registry key path:

dumpsec /rfga=”HKLM\Software\Microsoft\Windows NT\CurrentVersion”

This command shows permissions for the specified registry key.

**Enumerating Services**

To list services running on the target system, use:

dumpsec /services

This command provides details about each service, including its state, start type, and the account it runs under.

**Using DumpSec for Reconnaissance**

Hackers often leverage tools like DumpSec to gather intelligence about a target system as part of the reconnaissance, footprinting, and information gathering phase. This information can then be used to identify vulnerabilities, plan and strategize attacks, and potentially gain unauthorized access. While DumpSec itself is a legitimate tool used mainly for auditing user and group accounts, understanding how it might be misused can help defenders to better protect their security infrastructures.

The primary use of DumpSec in an attack scenario involves gathering detailed information about a target system’s configuration, which can reveal potential weaknesses.

Below is an example of how we can utilize DumpSec to fulfill our reconnaissance needs and tasks:

**User Enumeration**

We can enumerate users to identify potential targets for social engineering attacks or to find accounts that may have been overlooked in security audits.

dumpsec /users > users.txt

This command exports a list of all users to a text file, which can then be analyzed for targets of interest.

**Group Enumeration**

Knowing which users belong to which groups can help you to understand the organizational structure and possibly identify high-value targets as well.

dumpsec /groups > groups.txt

This command saves information about groups and their members, aiding in the identification of privileged accounts.

**Permission Auditing**

By auditing file system and registry permissions, you can identify directories or keys where improper permissions might allow you to escalate privileges or execute code.

dumpsec /rfga="C:\path\to\sensitive\directory" > dir\_permissions.txt

dumpsec /rfga="HKLM\Software\Microsoft\Windows NT\CurrentVersion" > reg\_permissions.txt

These commands help identify weak permissions that could be exploited.

**Service Enumeration**

Enumerating services can reveal outdated software versions vulnerable to known exploits or services running under accounts with excessive privileges.

dumpsec /services > services.txt

This command lists all services, which you can then cross-reference with databases of known vulnerabilities.

**Exploitation Based on DumpSec Findings**

After gathering intelligence with DumpSec, you can move on to the exploitation phase, targeting vulnerabilities identified during your reconnaissance. Some hypothetical scenarios based on common findings include:

**Exploiting Weak Permission Sets**

If DumpSec reveals a directory with weak permission sets, you could attempt to place a malicious script there, which could then be executed by a privileged service or user.

echo ^\<malicious\_script^> > C:\path\to\vulnerable\directory\evil.exe

This command places a malicious executable in a vulnerable directory, potentially allowing it to be executed with elevated privileges.

**Leveraging Outdated Software**

If a service is running an outdated version of software is identified, you can exploit known vulnerabilities in that software to gain unauthorized access.

exploit\_framework exploit/outdated\_service

This command represents using an exploit framework to target a known vulnerability in an otherwise outdated service.

**Defense Against Misuse**

Understanding how tools like DumpSec can be misused is crucial for defenders. Implementing least privilege principles, regularly auditing permissions, keeping software up to date, and monitoring for unusual activities can mitigate many risks associated with reconnaissance activities conducted with DumpSec.

While DumpSec is a valuable tool for legitimate security audits, its capabilities can also be leveraged for malicious reasons and purposes. By understanding potential misuse scenarios and defense scenarios, ethical and unethical hackers can better defend against such attacks and learn from defense activities to better strategize offensive attacks against the target. Continuous vigilance, regular system audits, and adherence to security best practices are essential components of any good security posture.

**NetBIOS Enumerator**

(_**Source:**_ http://nbtenum.sourceforge.net)

The NetBIOS Enumerator tool shows you how to use remote network support and to deal with other various network protocols, such as SMB. As shown in the figure below, attackers use NtBIOS Enumerator to enumerate details such as NetBIOS names, usernames, domain names, and Media Access Control (MAC) addresses for a given range of IP addresses.

Note: I’m using the Parrot Security OS to launch NetBIOS Enumerator.

FIGURE X: nbtstat command output-enumerating NetBIOS.

FIGURE X: nbtstat command output for enumerating name servers.

### Network Enumeration Tools

#### Nmap ("Network Mapper")

(_**Source:**_ [https://nmap.org/download](https://nmap.org/download))

As a vulnerability management analyst that regularly conducts penetration and vulnerability assessments, a recurring challenge seems to arise when assessing an organizations with a large allocation of IP address space. What does one do when faced with multiple class Bs, a few class Cs, and a limited amount of time? Do you stick all of the address space in your favorite scanner and hit the _Go_ button, wait until it’s done and hope the results are accurate? How can you be sure that your scanner found all the hosts that are accessible? Do you even know the method your scanner uses to discover which hosts are alive?

This section of enumeration tools will attempt to answer the above questions and will illustrate (at a very high-level technical fashion), the methodology that I use to accurately discover which hosts are accessible prior to conducting port scanning or a vulnerability assessment.

**Note: Some may say that unless one performs a scan on all 65535 TCP and UDP ports on every possible IP address in the range, that the penetration tester isn’t being thorough enough. While I do agree that in order to be completely thorough, one must perform a scan as stated, but I have rarely, if ever had the luxury of performing such a scan, as it usually takes a considerable amount of time to complete given that there are 65,535 ports to scan. An underlying theme about Information Security is about striking a balance and weighing the pros and cons. If being absolutely thorough and time is of no consideration, you’ll more than likely want to run a full, blind scan on all IP addresses. If, however, a balance can be struck between being thorough and completing the project on time, read on – you may learn some techniques to improve both the accuracy and efficiency of your scans.**

**What is Host Discovery?**

Host discovery is a term I’ll use to describe a certain phase of a penetration test, where one attempts to determine the accessible hosts on a network. Many times, if a firewall ruleset is written explicitly, it is difficult to accurately determine the number of hosts that are behind a firewall. A colleague of mine once ran a high-priced commercial scanner against an almost full Class C and found only one host. Using the techniques outlined in this section, I was able to determine that there was not just one, but seventeen hosts in this particular segregated DMZ. This commercial scanner has very few options for host discovery and is not very configurable when it comes to fine tuning the discovery method.

Since this section is about Nmap and host discovery, we’ll talk specifically about how Nmap does its discovery and we’ll learn how to use Nmap’s options to improve the discovery phase of a penetration test or vulnerability assessment

To start off, let’s dissect the following very basic Nmap command:

Nmap -sS -O 172.26.1.0/29

There are three distinct phases with the above Nmap command. They are:

* Host discovery
* Port scanning
* OS Fingerprinting

In this section, we will use a DMZ environment with a variety of different firewall rulesets to illustrate the best methods for discovering hosts behind a firewall. The DMZ architecture that we will use is depicted below in the following illustration.

Our scanning host sits on the 192.168.5.0/24 network and has the IP address of 192.168.5.20.

Unless otherwise stated, we will use the following Nmap command for all discovery scans:

Nmap -sP 172.26.1.0/29

The -sP option specifies that only a discovery scan will be performed, and is the same discovery method used in a default Nmap scan.

**Exploring Nmap’s Default Behavior**

Before we learn how and why it might be necessary to modify Nmap’s behavior, we should have a solid understanding of its default behaviors, and how it may be insufficient in performing host discoveries.

An example of a basic Nmap scan looks like this:

nmap -v -Pn -sS -sV -O -p0-65535 -T4 \<Target IP Address>

In this example, I am telling Nmap to do an aggressive (-T4) and verbose (-v) stealth scan (-sS) on the TARGET IP that gives me the service and version details (-sV) of discovered ports, as well as the operating system (-O), while scanning every port under the sun (-p0-65535).

* **Description:** Nmap is a free and open-source network scanner designed to discover hosts and services on a computer network, thus creating a "map" of the network.
* **Use Cases:** Attackers use Nmap to identify open ports, running services, and operating systems on target networks. Defenders use it to audit their network for open ports and misconfigured services.

#### Wireshark

(_**Source:**_ https://www.wireshark.org/download.html)

* **Description:** Wireshark is a network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.
* **Use Cases:** Attackers can use Wireshark to analyze captured network packets to identify sensitive information or vulnerabilities. Defenders use it to monitor network traffic for anomalies and potential security breaches.

### System Enumeration Tools

#### Metasploit Framework

(_**Source:**_ https://www.metasploit.com/download)

* **Description:** Metasploit is a penetration testing framework that makes hacking simple. It's an essential tool for many attackers and defenders due to its extensive database of exploits and payloads.
* **Use Cases:** Attackers use Metasploit to exploit vulnerabilities identified during enumeration. Defenders use it to test their systems against known exploits to identify and patch vulnerabilities.

#### PowerShell Empire

(_**Source:**_ https://www.kali.org/tools/powershell-empire/)

* **Description:** PowerShell Empire is a post-exploitation framework that uses PowerShell agents without needing PowerShell.exe. It enables administrators and attackers to execute PowerShell agents without having PowerShell.exe present on the target system.
* **Use Cases:** Attackers might use Empire to establish persistence and move laterally across a network post-exploitation. Defenders can use it to understand attack vectors and improve detection mechanisms.

### User and Group Enumeration Tools

#### BloodHound

(_**Source:**_ https://bloodhound.readthedocs.io/en/latest/installation/windows.html)

* **Description:** BloodHound uses graph theory to reveal the hidden and often unintended relationships within an Active Directory environment. It maps out user permissions and potential attack paths.
* **Use Cases:** Attackers use BloodHound to identify paths to domain dominance. Defenders use it to audit Active Directory configurations and harden against attack paths identified by the tool.

#### Mimikatz

(_**Source:**_ https://github.com/ParrotSec/mimikatz)

* **Description:** Mimikatz is a tool designed to aid in the extraction of credentials from Windows systems. It can dump plaintext passwords, hash values, and Kerberos tickets.
* **Use Cases:** Attackers use Mimikatz to extract credentials for lateral movement and privilege escalation. Defenders use it to test the resilience of their systems against credential dumping attacks and to enforce security policies that mitigate such risks.

#### Hyena

(_**Source:**_ https://community.spiceworks.com/t/systemtools-software-hyena/977517)

* **Description:** Hyena is a comprehensive enumeration tool for Windows environments. It simplifies the day-to-day administration of users, groups, computers, and domains. Hyena offers a graphical user interface to manage Active Directory objects, system services, event logs, and disk space utilization. It integrates with various Windows management utilities and provides extensive reporting options.
* **Use Cases:** Hyena is able to facilitate:
  * **Active Directory Management:** Managing users, groups, and computers within Active Directory.
  * **System Administration:** Monitoring and managing system services, event logs, and disk space on network computers.
  * **Security Management:** Reviewing and modifying permissions and security settings across the target network.
  * **Reporting:** Generating detailed reports on user activities, group memberships, and system configurations.
  * **Troubleshooting:** Diagnosing and resolving system issues by analyzing event logs and service statuses.

#### Nsauditor Network Security Auditor

(_**Source:**_ http://www.nsauditor.com/)

* **Description:** Nsauditor Network Security Auditor is a network security and vulnerability scanning tool that can also perform enumerating tasks such as identification and addressing of security issues within networks. It offers a suite of utilities for auditing network security, monitoring network traffic, detecting vulnerabilities, and managing network resources. Nsauditor provides detailed analysis and reporting on network health and security.
* **Use Cases:** Nsauditor Network Security Auditor is able to facilitate:
  * **Vulnerability Assessment:** Scanning the network for vulnerabilities, misconfigurations, and security weaknesses.
  * **Network Monitoring:** Monitoring network traffic and analyzing data to detect potential security threats and anomalies.
  * **Security Auditing:** Auditing network security policies and configurations to ensure compliance with best practices and regulations.
  * **Intrusion Detection:** Identifying unauthorized access attempts and potential security breaches.
  * **Resource Management:** Managing and optimizing network resources by analyzing bandwidth usage and device performance.

#### Global Network Inventory

(_**Source:**_ http://soft.udm4.com/Network-and-Internet/Global\_Network\_Inventory.html)

* **Description:** Global Network Inventory is a network enumeration tool that allows you to collect detailed information about network devices and assets. It can scan IP networks, Windows domains, and workgroups to gather hardware and software inventory data. The tool provides extensive reporting capabilities, allowing you to maintain an up-to-date record of all networked devices and their configurations.
* **Use Cases:** Global Network Inventory is able to facilitate:
  * **Network Asset Management:** Keeping track of all network devices, including servers, workstations, routers, and switches.
  * **Software Inventory:** Auditing installed software on network computers to ensure compliance with licensing agreements.
  * **Hardware Inventory:** Collecting detailed information about hardware components for maintenance and upgrade planning.
  * **Change Management:** Monitoring changes in network device configurations to detect unauthorized alterations.
  * **Compliance Reporting:** Generating reports required for regulatory compliance and IT audits.

#### Advanced IP Scanner

(_**Source:**_ https://www.advanced-ip-scanner.com/)

* **Description:** Advanced IP Scanner is a fast and robust network scanner that can locate and scan all devices connected to your network. It provides information about each device, including IP and MAC addresses, device names, and shared resources. It also integrates with Radmin, a remote administration tool, to allow remote control of computers.
* **Use Cases:** Advanced IP Scanner is able to facilitate:
  * **Network Discovery:** Quickly identifying all devices connected to a network for initial setup or troubleshooting.
  * **Device Management:** Managing devices by accessing shared folders and remote control features.
  * **Troubleshooting:** Identifying devices that are causing network issues or are misconfigured.
  * **Network Security:** Detecting unauthorized devices connected to the network.
  * **Remote Administration:** Using the integration with Radmin to perform remote tasks and control network computers.

### File and Directory Enumeration Tools

#### DirBuster/DirSearch

(_**Source:**_ https://sourceforge.net/projects/dirbuster/)

* **Description:** These tools are used for brute-forcing directories and files on web servers.
* **Use Cases:** Attackers use them to discover hidden directories and files that may contain vulnerabilities or sensitive information. Defenders use them to audit web servers for misconfigurations and hidden content.

#### Lynis

(_**Source:**_ https://cisofy.com/downloads/lynis/)

* **Description:** Lynis is an open-source security auditing tool. Used to evaluate the security defenses of Linux and Unix-based systems.
* **Use Cases:** Primarily used by defenders to perform extensive health scans of systems to detect security issues and provide compliance testing.

Enumeration tools play a pivotal role in both attack and defense scenarios. While attackers leverage these tools to discover vulnerabilities and plan exploits, defenders use them to proactively identify weaknesses and strengthen their security posture. Understanding and utilizing these tools effectively is essential for anyone involved in cybersecurity, whether for offensive or defensive purposes.

### Enumerating User Accounts

#### pstools

Enumerating user accounts using the PsTools suite helps in controlling and managing remote systems from the command line. The following are some commands for enumerating user accounts.

#### PsExec

PsExec is a lightweight Telnet replacement that can execute processes on other systems, complete with full interactivity for console applications, without having to install client software manually. PsExec’s most powerful use case is the launch of interactive command prompts on remote systems and remote-enabling tools such as ipconfig that otherwise cannot show information about remote systems. The syntax of the PsExec command is as follows:

psexec \[\\\computer\[, computer2\[,…] | @file]]\[-u user] \[-p psswd] \[-n s] \[-r servicename] \[-h] \[-l] \[-s] \[-e] \[-x] \[-I \[session]] \[-c executable \[-f|-v]] \[-w directory] \[-d] \[-\<priority>] \[-a n, n, …] cmd \[arguments]

#### PsFile

PsFile is a command line utility that shows a list of files on a system that opened remotely, and it can close opened files either by name or by a file identifier. The default behavior of PsFile is to list the files on the local system opened by remote systems. Typing a command followed by “-“ displays information on the syntax for that command. The syntax of the PsFile command is as follows:

psfile \[\\\RemoteComputer \[-u Username \[-p Password]]] \[\[Id | path] \[-c]]

#### PsGetSid

PsGetSid translates SIDs to their display name and vice versa. It works on built-in accounts, domain accounts, and local accounts. It also displays the SIDs of user accounts and translates an SID into the name that represents it. It works across the network to query SIDs remotely. The syntax of the PsGetSid command is as follows:

psgetside \[\\\computer \[, computer\[,…] | @file] \[-u username \[-p password]]] \[account|SID]

#### PsKill

PsKill is a kill utility that can kill processes on remote systems and terminate processes on the local computer. Running PsKill with a process ID (PID) directs it to kill the process of that ID on the local computer. If a process name is specified, PsKill will kill all processes that have that name. One need not install a client on the target computer to use PsKill to terminate a remote process. The syntax of the PsKill command is as follows:

pskill \[- ] \[-t] \[\\\computer \[-u username] \[-p password]] \<process name } process id>

#### PsInfo

PsInfo is a command line tool that gathers key information about local or remote legacy Windows systems, including the type of installation, kernel build, registered organization and owner, number of processes and their type, amount of physical memory, installation data of the system, and expiration data in the case of a trial version. By default, PsInfo shows information for the local system. A remote computer name can be specified to obtain information for a remote system. The syntax of the PsInfo command is as follows:

psinfo \[\[\\\computer\[,computer \[,…] | @file \[-u user \[-p psswd]]] \[-h] \[-s] \[-d] \[-c \[-t delimiter]] \[filter]

#### PsList

PsList is a command line tool that displays the Central Processing Unit (CPU) and memory information or thread statistics. Tools in the Resource Kits, pstat and pmon, show different types of data only for the processes on the system on which the tools are run.

#### PsLoggedOn

PsLoggedOn is an applet that displays both the locally logged-in users and users logged in via resources for either the local computer or a remote one. If a username is specified instead of a computer, PsLoggedOn searches for the computers in the network neighborhood and reveals if the user currently logged in. PsLoggedOn defines a locally logged-in user is one that has a profile loaded into the registry; therefore, PsLoggedOn determines who is logged in by scanning the keys under the HKEY\_USERS key. For each key that has a name or user SID, PsLoggedOn looks up the corresponding username and displays it. To determine who logged into a computer via resource shares, PsLoggedOn uses the NetSessionEnum API. The syntax of the PsLoggedOn command is as follows:

psloggedon \[- ] \[-l] \[-x] \[\\\computername | username]

#### PsLogList

The elogdump utility dumps the contents of an Event Log on a local or remote computer. PsLogList is a clone of elogdump except that PsLogList can log in to remote systems in situations where the user’s security credentials would not permit access to the Event Log, and PsLogList retrieves message strings from the computer on which the event log is stored. The default function of PsLogList is to display the contents of the System Event Log on the local computer with visually friendly formatting. The syntax of the PsLogList command is as follows:

psloglist \[- ] \[\\\computer\[, computer\[,…] | @file \[-u username \[-p password]]] \[-s \[-t delimiter]] \[-m # | -n # | -h # | -d # | -w] \[-c] \[-x] \[-r] \[-a mm/dd/yy] \[-b mm/dd/yy] \[-f filter] \[-I ID\[,ID\[,…] | -e ID\[,ID\[,…]]] \[-o event source\[, event source] \[,…]]] \[-q event source\[,event source] \[,…]]] \[-l event log file] \<eventlog>

**PsPasswd**

PsPasswd can change an account password on local or remote systems, and administrtors can create batch files that run PsPasswd on the computers they manage to perform a mass change of the administrator password. PsPasswd uses Windows password reset APIs; therefore, it does not send passwords over the network in the cleartext. The syntax of the PsPasswd command is as follows:

Pspasswd \[\[\\\computer\[, computer\[,…] | @file \[-u user \[-p psswd]]] Username \[NewPassword]

**PsShutdown**

PsShutdown can shut down or reboot a local or remote computer. It requires no manual installation of client software. The syntax of the PsShutdown command is as follows:

Psshutdown \[\[\\\computer\[, computer\[,…] | @file \[-u user \[-p psswd]]] -s|-r|-h|-d|-k|-a|-l|-o \[-f] \[-c] \[-t nn|h:m] \[-n s] \[-v nn] \[-e \[u|p] :xx:yy] \[-m “message”]

**Enumerating Shared Resources Using the Net View Command**

Net view is a command line utility that displays a list of computers in a specified workgroup or shared resources available on a specified computer. It can be used in the following manner:

Net view \\\\\<computername>

In the above command, \<computername> is the name or IP address of a specific computer, the resources or which are to be displayed.

Net view \\\\\<computername> /ALL

The above command displays all the shares on the specified remote computer, along with hidden shares.

* Net view /domain
* The above command displays all the shares in a domain.
* Net view /domain:\<domain name>
* The above command displays all the shares on the specified domain.

The figure below shows the shared resources available on the specified target computer.

FIGURE X: Output of the net view command.

**SNMP Enumeration**

Simple Network Management Protocol (SNMP) allows you to manage network devices from a remote location; however, SNMP has many security vulnerabilities, such as lack of auditing. Attackers may take advantage of these vulnerabilities to perform account and device enumeration. This section describes SNMP enumeration, the information extracted via SNMP enumeration, and various SNMP enumeration tools used to enumerate user accounts and devices on a target system.

**Overview of SNMP**

SNMP, or Simple Network Management Protocol, is a cornerstone of network management, facilitating the monitoring and management of network devices. Introduced to streamline the management of network components, SNMP enables administrators to collect information from various devices across a network, such as routers, switches, firewalls, and servers, in a standardized manner.

**The Evolution of SNMP**

Over the years, SNMP has evolved through several versions, each introducing improvements and new features. These iterations reflect the ongoing efforts to balance usability with security, a theme that resonates throughout the evolution of network management protocols.

**The Technology Triangle**

The concept of the technology triangle emphasizes the inherent trade-offs between security, performance, and usability. As network administrators strive to simplify management processes, they often lean towards solutions that enhance the ease of use; however, this pursuit can inadvertently compromise security, a critical consideration in the context of SNMP.

**SNMP and Device Management**

SNMP operates at the Application Layer, Layer 7, of the OSI (Open Systems Interconnection) Reference model, enabling network devices to communicate with a centralized management station. This communication allows for the collection of vital statistics, such as device status, performance metrics, and configuration details. By aggregating this information, administrators can effectively monitor and manage network health, troubleshoot issues, and ensure optimal performance.

**Challenges and Risks**

Despite its benefits, SNMP presents several challenges and risks. One of the primary concern is **security**. Because SNMP relies on community strings (akin to passwords) for authentication, improper configuration can expose devices to unauthorized access. Attackers can exploit these vulnerabilities to gather sensitive information or disrupt network operations.

**Mitigating Risks**

To mitigate the risks associated with SNMP, it’s crucial to follow best practices for configuration and security. This includes:

* Using strong, unique community strings and restricting access to SNMP communications.
* Implementing SNMPv3, which provides enhanced security features, including authentication and encryption.
* Regularly reviewing and updating SNMP configurations to align with current security standards and threat landscapes.

SNMP plays a vital role in network management, offering administrators a streamlined method for collecting and analyzing data from network devices; however, its ease of use comes with security considerations. Administrators must navigate the technology triangle carefully, prioritizing security alongside usability to protect network assets effectively. By adhering to best practices and leveraging the latest versions of SNMP, organizations can harness the power of this protocol while minimizing associated risks.

FIGURE X: SNMP clients gather performance intel and report what it gathers back to a centralized management server.

Beyond its designation as an Application Layer (L7) protocol, SNMP operates over UDP and is instrumental in overseeing and managing routers, hubs, and switches within an IP network. Consequently, SNMP agents are strategically placed on both Windows and Unix-based networks across various networking devices. Their primary function is to gather and transmit essential management data and metrics to an SNMP manager.

Operating at the application layer of the OSI model, SNMP utilizes UDP for transport, simplifying the management of network components by providing a standardized way to collect and organize information about these devices.

These agents serve as pivotal intermediaries, bridging the gap between the network devices and the SNMP manager. They adeptly translate device-specific data into a universally comprehensible format, facilitating seamless communication between the disparate elements of the network.

**SNMP and the OSI Model**

Operating at the Application Layer (Layer 7) of the OSI model, SNMP interacts with the lower layers to facilitate its operations. Specifically, SNMP relies on the following layers:

* **Physical Layer (Layer 1):** Ensures that the physical connections between devices are established and maintained, allowing SNMP messages to travel across the network.
* **Data Link Layer (Layer 2):** Responsible for framing and unframing the data packets, ensuring reliable data transfer between devices.
* **Network Layer (Layer 3):** Manages routing of SNMP messages across different networks, determining the path that packets take to reach their destination.
* **Transport Layer (Layer 4):** While SNMP primarily uses UDP (a connectionless protocol), it can also utilize TCP (a connection-oriented protocol) for secure communication, ensuring that SNMP messages are delivered reliably.
* **Session Layer (Layer 5):** Although SNMP does not establish sessions in the traditional sense, this layer's role in managing dialogues between applications is conceptually aligned with SNMP's operation.
* **Presentation Layer (Layer 6):** SNMP messages are structured in a way that is independent of the underlying network architecture, ensuring that the presentation of data is consistent across different platforms and devices.
* **Application Layer (Layer 7):** This is where SNMP operates, providing a framework for managing network devices and collecting information about their status and performance.

**SNMP Operations Across Layers**

SNMP's ability to manage and monitor network devices hinges on its interaction with these layers. For instance, SNMP uses the Network Layer to route messages to the correct device, relying on IP addresses to identify targets. The Transport Layer ensures that SNMP messages are delivered reliably, even in the presence of network congestion or packet loss.

Moreover, SNMP leverages the Data Link Layer to frame its messages for transmission over the network. This layering ensures that SNMP can operate efficiently across various network architectures, from simple peer-to-peer networks to complex, distributed systems.

**Security Considerations**

As SNMP operates at the application layer, it inherits the security characteristics of the protocols used at this level, primarily UDP. However, SNMPv3 introduced significant enhancements to security, incorporating authentication and encryption mechanisms to protect SNMP messages from unauthorized access and tampering.

SNMP's interaction with the OSI model's layers is multifaceted, enabling it to perform its critical role in network management. By leveraging the capabilities of the lower layers, SNMP can effectively monitor and manage network devices, ensuring optimal network performance and reliability.

**SNMP Management Processes**

The SNMP manager, equipped with this translated data, is capable of presenting near-real-time information regarding network statistics and metrics to administrators. Through sophisticated processing, it transforms the raw, machine-understandable code into a user-friendly format. This transformation ensures that administrators receive timely, accurate insights into the performance and activities of network endpoints.

Such a mechanism fosters an environment conducive to the efficient monitoring and management of network devices. It guarantees optimal network performance and reliability, empowering administrators with the necessary tools to maintain a healthy and responsive network infrastructure.

Furthermore, SNMP enumeration is the process of creating a list of the user’s accounts and devices on a target computer using SNMP. SNMP employs two types of software components for communication: the SNMP agent and SNMP management station. The SNMP agent is located on the networking device, and the SNMP management station communicates with the agent.

Almost all the network infrastructure devices such as routers and switches contain an SNMP agent for managing the system or devices. The SNMP management station sends requests to the agent, after receiving the request, the agent replies. Both requests and replies are configuration variables accessible by the agent software. SNMP management stations send requests to set values to some variables. _**Traps**_ let the management station know if an abnormal event such as a reboot or an interface failure has occurred at the agent’s side.

SNMP contains the following two passwords for configuring and accessing the SNMP agent from the management station.

* **Read Community String**
  * The configuration of the device or system can be viewed with the help of this password.
  * These strings are public.
  * That is a vulnerability for exploitation.
* **Read/Write Community String**
  * The device configuration can be changed or edited using this password.
  * These strings are private.

For further security, make sure the private r/w community string is encrypted and that the SNMP is at version 3.

When you leave the community strings at the default setting, attackers can use these default community strings (passwords) for changing or viewing the configuration of the device or system. Attackers enumerate SNMP to extract information about network resources such as hosts, routers, devices, and shares as well as network information such as ARP (Address Resolution Protocols) tables, routing tables, device-specific information, and traffic statistics.

Commonly used SNMP enumeration tools include OpUtils (Source: https://www.manageengine.com) and Network Performance Monitor (NPM) (Source: https://www.solarwinds.com).

**Inner-Workings of SNMP**

SNMP uses a distributed architecture comprising SNMP managers, SNMP agents, and several related components. The following are some commands associated with SNMP.

* **GetRequest:** Used by the SNMP manager to request information from an SNMP agent.
* **GetNextRequest:** Used by the SNMP manager continuously to retrieve all the data stored in an array or table.
* **GetResponse:** Used by an SNMP agent to satisfy a request made by the SNMP manager.
* **SetRequest:** Used by the SNMP manager to modify the value of a parameter within an SNMP agent’s Management Information Base (MIB).
* **Trap:** Used by an SNMP agent to inform the pre-configured SNMP manager of a certain event.

The communication process between an SNMP manager and SNMP agent is as follows:

1. The SNMP manager (Host X, 10.10.2.1) uses the GetRequest command to send a request for the number of active sessions of the SNMP agent (Host Y, 10.10.2.15). To perform this step, the SNMP manager uses an SNMP service library such as the Microsoft SNMP Management API library (Mgmtapi.dll) or Microsoft WinSNMP API library (Wsnmp32.dll).
2. The SNMP agent (Host Y) receives the message and verifies if the community string (Compinfo) is present on its MIB, checks the request against its list of access permissions for that community, and verifies the source IP address.
3. If the SNMP agent does not find the community string or access permission in Host Y’s MIB database and the SNMP service is set to send an authentication trap, it sends an authentication failure trap to the specified trap destination, Host Z.
4. The master agent component of the SNMP agent calls the appropriate extension agent to retrieve the requested session information from the MIB.

Using the session information retrieved from the extension agent, the SNMP service forms a return SNMP message that contains the number of active sessions and the destination IP address (10.10.2.1) of the SNMP manager, Host X.

Host Y sends the response to Host X.

FIGURE X: Illustration of the working of SNMP.

**Management Information Base (MIB)**

MIB is a virtual database containing a formal description of all the network objects that SNMP manages. It is a collection of hierarchically organized information. It provides a standard representation of the SNMP agent information and storage. MIB elements are recognized using Object Identifiers (OIDs). An OID is the numeric name given to an object and begins with the root of the MIB tree. The OID can uniquely identify the object in the MIB hierarchy.

MIB-managed objects include scalar objects, which define a single object instance, and tabular objects, which define a group of related object instances. OIDs include the object’s type (such as counter, string, or address), access level (such as read or read/write), size restrictions, and range information. The SNMP manager converts the OIDs into a human-readable display using the MIB as a codebook.

You can access the contents of the MIB by using a web browser either by entering the IP address and Lseries.mib or by entering the DNS library name and Lseries.mib. For example, http://IP.Address/Lseries.mib or http://library\_name/Lseries.mib. Microsoft provides a list of MIBs that are installed with the SNMP service in the Windows resource kit. The major MIBs are as follows:

* **DHCP.MIB:** Monitors network traffic between DHCP servers and remote hosts
* **HOSTMIB.MIB:** Monitors and manages host resources
* **LNMIB2.MIB:** Contains object types for workstations and server services
* **MIB\_II.MIB:** Manages TCP/IP-based Internet using a simple architecture and system
* **WINS.MIB:** For the Windows Internet Name Service (WINS)

**Enumerating SNMP Using SnmpWalk**

SnmpWalk is a command line tool that allows you to scan numerous Simple Network Management Protocol (SNMP) nodes instantly and identify a set of variables that are available for accessing the target network. Using this tool, attackers target the root node so that information from all the sub-nodes such as routers and switches can be fetched. The information can be retrieved in the form of an object identifier (OID), which is part of the management information base (MIB) associated with the devices having SNMP enabled.

You can execute the following command to retrieve SNMP information from the target device:

Snmpwalk -v1 -c public \<Target IP Address>

The above command allows attackers to view all the OIDs, variables, and other associated information. Using this command, you can also retrieve all the data in transit to the SNMP server from the SNMP agent, including the server being used, user credentials, and other parameters.

FIGURE X: SnmpWalk tool output.

**Other SnmpWalk Commands:**

* Command to enumerate SNMPv2 with a community string of public:

snmpwalk -v2c -c public \<Target IP Address>

* Command to search for installed software:

snmpwalk -v2c -c public \<Target IP Address> hrsWInstalledName

* Command to determine the amount of RAM on the host:

snmpwalk -v2c -c public \<Target IP Address> hrMemorySize

* Command to change an OID to a different value:

snmpwalk -v2c -c public \<Target IP Address> \<OID> \<New Value>

* Command to change the sysContact OID:

snmpwalk -v2c -c public \<Target IP Address> sysContact \<New Value>

**Enumerating SNMP Using Nmap**

You can use the snmp-processes Nmap Scripting Engine (NSE) script against an SNMP remote server to retrieve information related to the hosted SNMP services.

nmap -sU -p 161 –script=snmp-processes \<Target IP Address>

The above Nmap command, when executed, retrieves a list of all the running SNMP processes along with the associated ports on the target host.

Other Nmap commands to perform SNMP enumeration include:

nmap -sU -p 161 –script=snmp-sysdescr \<Target IP Address> ->Retrieves information regarding SNMP server type and operating system details.

nmap -sU -p 161 –script=snmp-win32-software \<Target IP Address> -> Retrieves a list of all the applications running on the target machine.

FIGURE X: Nmap using the snmp-processes NSE script.

**SNMP Enumeration Tools**

SNMP enumeration tools are used to scan a single IP address or a range of IP addresses of SNMP-enabled network devices to monitor, diagnose, and troubleshoot security threats.

**snmp-check (snmp\_enum Module)**

(_**Source:**_ https://www.nothink.org)

snmp-check is an open-source tool distributed under the GNU General Public License (GPL). Its goal is to automate the process of gathering information on any device with SNMP support (Windows, Unix-like, network appliances, printers). snmp-check allows the enumeration of SNMP devices and places the output in a human-readable and user-friendly format. It could be useful for penetration testing or systems monitoring.

You use this tool to gather information about the target, such as contact, description, write access, devices, domain, hardware, and storage information, hostname, Internet Information Services (IIS) statistics, IP forwarding, listening UDP ports, location, mountpoints, network interfaces, network services, routing information, software components, system uptime, TCP connections, total memory, uptime, and user accounts.

FIGURE X: The snmp-check tool showing system information and user accounts.

FIGURE X: The snmp-check tool showing network information and interfaces.

**SoftPerfect Network Scanner**

(_**Source:**_ https://www.softperfect.com)

SoftPerfect Network Scanner can ping computers, scan ports, discover shared folders, and retrieve practically any information about network devices via Windows Management Instrumentation (WMI), SNMP, Hypertext Transfer Protocol (HTTP), SSH, and PowerShell. It also scans for remote services, registry, files, and performance counters; offers flexible filtering and display options; and exports NetScan results to a variety of formats ranging from Extensible Markup Language (XML) to JavaScript Object Notation (JSON).

Moreover, SoftPerfect Network Scanner can check for a user-defined port and report if one is open. In addition, it can resolve hostnames and auto-detect the local and external IP range. It supports remote shutdowns and Wake-on LAN.

You can use this tool to gather information about a shared folder and network devices.

FIGURE X: SoftPerfect Network Scanner.

The following are some additional SNMP enumeration tools:

**Network Performance Monitor (NPM)**

(_**Source:**_ https://www.solarwinds.com)

* **Description:** Network Performance Monitor (NPM) is a comprehensive network monitoring tool designed to help IT professionals manage and optimize the performance of their networks. It provides real-time insights into network status, performance metrics, and potential issues through a user-friendly dashboard.
* **Use Cases:**
  * **Network Performance Monitoring:** Continuously monitors network devices and interfaces to ensure optimal performance and quickly identifies performance bottlenecks.
  * **Fault Detection and Alerts:** Detects network faults and issues, sending real-time alerts to administrators for rapid troubleshooting and resolution.
  * **Capacity Planning:** Analyzes historical performance data to help with capacity planning and future network growth requirements.
  * **Bandwidth Utilization:** Tracks bandwidth usage across the network, helping to identify and manage bandwidth hogs and ensure fair distribution of network resources.
  * **Customizable Dashboards and Reports:** Provides customizable dashboards and reports to meet the specific needs of different users and stakeholders.

**OpUtils**

(_**Source:**_ https://www.manageengine.com)

* **Description:** OpUtils is a network monitoring and management software that provides a suite of tools for IP address management, switch port mapping, network diagnostics, and more. It is designed to help network administrators efficiently manage their network infrastructure.
* **Use Cases:**
  * **IP Address Management:** Automates the process of managing and tracking IP addresses, helping to prevent IP conflicts and ensuring efficient IP utilization.
  * **Switch Port Mapping:** Maps and monitors switch ports, providing visibility into the devices connected to each port and helping with capacity planning and troubleshooting.
  * **Network Diagnostics:** Includes tools for diagnosing network issues, such as ping, traceroute, and SNMP tools, helping administrators quickly identify and resolve problems.
  * **Rogue Device Detection:** Detects unauthorized devices on the network, enhancing network security by preventing potential threats.
  * **Bandwidth Monitoring:** Monitors bandwidth usage in real-time, helping to identify and manage network traffic patterns.

**PRTG Network Monitor**

(_**Source:**_ https://www.paessler.com)

* **Description:** PRTG Network Monitor is an all-in-one network monitoring solution that provides comprehensive monitoring of network devices, traffic, applications, and more. It is known for its ease of use and powerful monitoring capabilities.
* **Use Cases:**
  * **Network Device Monitoring:** Monitors the status and performance of all network devices, including routers, switches, servers, and more.
  * **Traffic Analysis:** Analyzes network traffic to identify usage patterns, detect anomalies and optimize network performance.
  * **Application Monitoring:** Monitors the performance and availability of applications, ensuring they are running smoothly and efficiently.
  * **Cloud and Virtual Environment Monitoring:** Provides monitoring capabilities for cloud services and virtual environments, ensuring seamless operation across different platforms.
  * **Custom Alerts and Reports:** Offers customizable alerting and reporting features, enabling administrators to receive timely notifications and generate detailed reports based on their specific needs.

**Engineer's Toolset**

(_**Source:**_ https://www.solarwinds.com)

* **Description:** Engineer's Toolset is a collection of over 60 network management tools designed for network engineers. It provides a wide range of utilities for network discovery, diagnostics, monitoring, and troubleshooting.
* **Use Cases:**
  * **Network Discovery:** Includes tools for discovering network devices and mapping the network topology, providing a comprehensive view of the network infrastructure.
  * **Diagnostics and Troubleshooting:** Offers various diagnostic tools, such as ping, traceroute, DNS analyzer, and SNMP tools, helping engineers quickly identify and resolve network issues.
  * **Real-Time Monitoring:** Monitors network performance in real-time, providing instant visibility into the health and status of network devices and connections.
  * **Configuration Management:** Helps manage and back up device configurations, ensuring consistency and facilitating recovery in case of configuration changes or failures.
  * **Security and Compliance:** Includes tools for assessing network security and compliance, helping to identify vulnerabilities and ensure adherence to security policies and regulations.

**LDAP Enumeration**

Various protocols enable communication and management of data transfers between network resources. All these protocols carry valuable information about network resources along with the data. An external user who successfully enumerates that information by manipulating the protocols can break into the network and may misuse the network resources. The Lightweight Directory Access Protocol (LDAP) is one such protocol that accesses the directory listings. This section focuses on LDAP enumeration, the information extracted via LDAP enumeration, and LDAP enumeration tools.

LDAP is an Internet protocol for accessing distributed directory services. LDAP access directory listings within Active Directory or from other directory services. LDAP is a hierarchical or logical form of a directory, similar to a company’s organizational chart. Directory services may provide any organized set of records, often in a hierarchical and logical structure, such as a corporate email directory. It uses DNS for quick lookups and the fast resolution of queries. A client starts an LDAP session by connecting to a Directory System Agent (DSA), typically on TCP port 389, and sends an operation request to the DSA. The Basic Encoding Rules (BER) format is used to transmit information between the client and server.

In addition, you can anonymously query the LDAP service for sensitive information such as usernames, addresses, departmental details, and server names, which you can use to launch attacks.

**Manual and Automated LDAP Enumeration**

You can use both manual and automated approaches for LDAP enumeration. Some of the commands that can be used for LDAP enumeration are as follows:

**Manual LDAP Enumeration**

You can perform manual LDAP enumeration using Python. Follow the steps given below to perform manual LDAP enumeration using Python.

Using Nmap, check whether the target LDAP server is listening on port 389 for LDAP and port 636 for secure LDAP (LDAPS).

If the target server is listening on the specified ports, initiate the enumeration process by installing LDAP using the following command:

pip3 install ldap3

As shown in the code given below, create a server object (server), specify the target IP address or hostname and port number. If the target server is listening on LDAPS, specify use\_ssl = True.

Retrieve the Directory System Agent (DSA)-specific entry (DSE) naming contexts by specifying get\_info = ldap3. ALL.

Now, create a connection object, connection, and initiate a call to bind().

If the connection is successful, True is displayed on the screen as follows:

\>>> import ldap3

\>>> server = ldap3.Server(‘Target IP Address’, get\_info = ldap3.ALL, port =389)

\>>> connection = ldap3.Connection(server)

\>>> connection.bind()

True

Now, you can fetch information such as the domain name and naming context using the following script:

\>>>server.info

FIGURE X: LDAP enumeration using Python script.

After obtaining the naming context, retrieve all the directory objects using the script given below:

\>>>connection.search(search\_base=’DC=DOMAIN, DC=DOMAIN’, search\_filter=’ (&(objectClass=\*))’, search\_scope=’SUBTREE’, attributes=’\*’)

True

\>>connection.entries

FIGURE X: LDAP enumeration output.

Now, use the following script to dump the entire LDAP:

\>>connection.search(search\_base=’DC=DOMAIN, DC=DOMAIN’, search\_filter=’(&(objectClass=person))’, search\_scope=’SUBTREE’, attributes=’userPassword’)

True

\>>>connection.entries

**Automated LDAP Enumeration**

You can use the ldap-brute NSE script to brute-force LDAP authentication. By default, it uses the built-in username and password lists. The userdb and passdb script arguments can be employed to use custom lists.

nmap -p 389 –script ldap-brute –script-args ldap.base=’”cn=users,dc=MHD,dc=com “’\<Target IP Address>

FIGURE X: Nmap ldap-brute NSE script output.

**LDAP Enumeration Tools**

There are many LDAP enumeration tools that access directory listings within Active Directory (AD) or other directory services. Using these tools, you can enumerate information such as valid usernames, addresses, and departmental details from different LDAP servers.

**Softerra LDAP Administrator**

(_**Source:**_ https://www.ldapadministrator.com)

Softerra LDAP Administrator is an LDAP administration tool that works with LDAP servers such as Active Directory (AD), Novell Directory Services, and Netscape/iPlanet. It browses and manages LDAP directories. As shown in the figure below, you can use Softerra LDAP Administrator to enumerate user details such as the username, email address, and department.

FIGURE X: Softerra LDAP Administrator.

**Ldapsearch**

(_**Source:**_ https://linux.die.net)

Ldapsearch is a shell-accessible interface for the ldap\_search\_ext(3) library call. Ldapsearch opens a connection to an LDAP server, binds it, and performs a search using the specified parameters. The filter should conform to the string representation of the search filters, as defined in RFC 4515. If not provided, the default filter, (objectClass=\*), is used.

If ldapsearch finds one or more entries, the attributes specified by attrs are returned. If \* is listed, all user attributes are returned. If + is listed, all operational attributes are returned. If no attrs are listed, all user attributes are returned. If only 1.1 is listed, no attributes are returned.

The search results are displayed using an extended version of the LDAP Data Interchange Format (LDIF). The option -L controls the output format.

You can use ldapsearch to enumerate AD users. This allows you to establish connections with an LDAP server to perform different searches using specific filters. The following command can be used to perform an LDAP search using simple authentication:

ldapsearch -h \<Target IP Address> -x

If the above command is executed successfully, the following command can be executed to obtain additional details related to the naming contexts:

ldapsearch -h \<Target IP Address> -x -s base namingcontexts

For example, from the output of the above command, if the primary domain component can be identified as DC=htb, DC=local, the following command can be used to obtain more information about the primary domain:

Ldapsearch -h \<Target IP Address> -x -b “DC=htb, DC=local”

The following commands can be used to retrieve information about a specific object or all the objects in a directory tree:

ldapsearch -h \<Target IP Address> -x -b “DC=htb, DC=local” ‘(objectClass=Employee)’ -> retrieves information related to the object class Employee.

Ldapsearch -x -h \<Target IP Address> -b “DC=htb,DC=local” “objectclass=\*” -> retrieves information related to all the objects in the directory tree.

The following command retrieves a list of users belonging to a particular object class:

ldapsearch -h \<Target IP Address> -x -b “DC=htb,DC=local” ‘(objectClass=Employee)’ sAMAccountName sAMAccountType

FIGURE X: ldapsearch output.

The following are some additional LDAP enumeration tools:

**AD Explorer**

(_**Source:**_ https://docs.microsoft.com)

* **Description:** AD Explorer is a tool from Microsoft's Sysinternals suite designed for browsing and managing Active Directory (AD) databases. It provides a detailed, hierarchical view of the AD structure, allowing administrators to explore objects, attributes, and permissions within the directory.
* **Use Cases:**
  * **Directory Browsing:** Allows administrators to browse the AD database in a structured and intuitive manner, making it easy to locate specific objects and attributes.
  * **Object and Attribute Viewing:** Displays detailed information about AD objects and their attributes, helping administrators understand the directory's structure and data.
  * **Snapshot Functionality:** Enables the creation of snapshots of the AD database for offline viewing and analysis, useful for auditing and troubleshooting purposes.
  * **Search and Filtering:** Provides advanced search and filtering capabilities to quickly find specific objects or attributes within the AD.
  * **Permissions Analysis:** Helps administrators analyze and manage permissions, ensuring that appropriate access controls are in place.

**LDAP Admin Tool**

(_**Source:**_ https://www.ldapsoft.com)

* **Description:** LDAP Admin Tool is a graphical user interface (GUI) for managing and administering LDAP directories. It simplifies the tasks of browsing, searching, and modifying LDAP directory entries.
* **Use Cases:**
  * **Directory Management:** Facilitates the management of LDAP directories, allowing administrators to add, modify, and delete directory entries with ease.
  * **Search and Querying:** Offers powerful search and querying capabilities to find specific entries and attributes within the LDAP directory.
  * **Schema Management:** Helps manage LDAP schemas, including adding or modifying schema elements to accommodate organizational needs.
  * **Data Import and Export:** Provides tools for importing and exporting directory data, simplifying data migration and backup tasks.
  * **Access Control Management:** Assists in managing access controls and permissions, ensuring secure and appropriate access to directory resources.

**LDAP Account Manager**

(_**Source:**_ https://www.ldap-account-manager.org)

* **Description:** LDAP Account Manager (LAM) is a web-based tool for managing LDAP directory services. It provides a user-friendly interface for managing user accounts, groups, and other directory objects.
* **Use Cases:**
  * **User Account Management:** Simplifies the creation, modification, and deletion of user accounts in the LDAP directory, including setting attributes like passwords and roles.
  * **Group Management:** Allows administrators to manage groups, including adding or removing members and setting group attributes.
  * **Self-Service Portal:** Provides a self-service portal for users to manage their own accounts, such as updating personal information or changing passwords.
  * **Template-Based Management:** Uses templates to standardize the creation and management of directory objects, ensuring consistency and compliance with organizational policies.
  * **Customizable Interface:** Offers a customizable interface to meet the specific needs of different organizations and user roles.

**LDAP Search**

(_**Source:**_ https://securityxploded.com)

* **Description:** LDAP Search is a command-line utility used for querying LDAP directories. It is part of the OpenLDAP suite and allows administrators to perform complex searches and retrieve specific directory entries and attributes.
* **Use Cases:**
  * **Complex Queries:** Enables the execution of complex LDAP queries, using filters and search parameters to retrieve specific entries and attributes.
  * **Automation and Scripting:** Can be integrated into scripts and automation workflows to perform regular directory searches and data retrieval tasks.
  * **Bulk Data Retrieval:** Allows for the bulk retrieval of directory data, useful for auditing, reporting, and data analysis purposes.
  * **Troubleshooting and Diagnostics:** Assists in troubleshooting and diagnosing directory issues by enabling detailed searches and analysis of directory data.
  * **Integration with Other Tools:** Can be combined with other command-line tools and utilities to enhance LDAP directory management and reporting capabilities.

**NTP and NFS Enumeration**

Administrators often overlook the Network Time Protocol (NTP) server when considering security; however, if queried properly, it can provide valuable network information to an attacker; therefore, it is necessary to know what information an attacker can obtain about a network through NTP enumeration. The Network File System (NFS) is used for the management of remote file access. NFS enumeration helps attackers to gather information such as a list of clients connected to the NFS server, along with their IP addresses, and exported directories.

This section describes NTP enumeration, the information extracted via NTP enumeration, various NTP enumeration commands, NTP enumeration tools, and NFS enumeration techniques and tools.

**NTP Enumeration**

NTP is designed to synchronize network clocks of networked computers. It uses UDP port 123 as its primary means of communication. NTP can maintain time within an error of 10 ms over the public Internet. Furthermore, it can achieve an accuracy of 200 µs or better in LANs under ideal conditions.

The following are some pieces of information you can obtain by querying an NTP server:

* List of hosts connected to the NTP server
* Clients IP addresses in the network, their system names, and OSs
* Internal IPs, if the NTP server is in the demilitarized zone (DMZ)

**NTP Enumeration Commands**

NTP enumeration commands such as ntpdate, ntptrace, ntpdc, and ntpq are used to query an NTP server for valuable information.

**ntpdate**

This command collects the number of time samples from several time sources. Its syntax is as follows:

ntpdate \[-46bBdqsuv] \[-a key] \[-e authdelay] \[-k keyfile] \[-o version] \[-p samples] \[-t timeout] \[ -U user\_name] server \[…]

| -4           | Force DNS resolution of given hostnames of the IPv4 namespace                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------- |
| -6           | Force DNS resolution of given hostnames to the IPv6 namespace                                                 |
| -a key       | Enable the authentication function/specify the key identifier to be used for authentication                   |
| -B           | Force the time to always be slewed                                                                            |
| -b           | Force the time to be stepped                                                                                  |
| -d           | Enable debugging mode                                                                                         |
| -e authdelay | Specify the processing delay to perform an authentication function                                            |
| -k keyfile   | Specify the path for the authentication key file as the string “keyfile”; the default is /etc/ntp/keys        |
| -o version   | Specify the NTP version for outgoing packets as an integer version, which can be 1 or 2; the default is 4     |
| -p samples   | Specify the number of samples to be acquired from each server, with values ranging from 1-8; the default is 4 |
| -q           | Query only; do not set the clock                                                                              |
| -s           | Divert logging output from the standard output (default) to the system syslog facility                        |
| -t timeout   | Specify the maximum wait time for a server response; the default is 1 s                                       |
| -u           | Use an unprivileged port for outgoing packets                                                                 |
| -v           | Verbose mode; logs ntpdate’s version identification string                                                    |

TABLE X: ntpdate parameters and their respective functions.

FIGURE X: ntpdate command; shows debugging information for a given IP address.

**ntptrace**

This command determines where the NTP server obtains the time from and follows the chain of NTP servers back to its primary time source. You can use this command to trace the list of NTP servers connected to the network. Its syntax is as follows:

ntptrace \[-n] \[-m maxhosts] \[servername/IP\_address]

| -n          | Do not print hostnames and show only IP address; may be useful if a name server is down |
| ----------- | --------------------------------------------------------------------------------------- |
| -m maxhosts | Set the maximum number of levels up the chain to be followed                            |

TABLE X: ntptrace parameters and their respective functions.

**Example:**

\# ntptrace

Localhost: stratum 4, offset 0.0019529, synch distance 0.143235

10.10.0.1: stratum 2, offset 0.01142

73, synch distance 0.115554

10.10.1.1: stratum 1, offset 0.0017698, synch distance 0.011193

**ntpdc**

This command queries the ntpd daemon regarding its current state and requests changes in that state. You can use this command to retrieve the state and statistics of each NTP server connected to the target network. Its syntax is as follows:

ntpdc \[ -46dilnps ] \[ -c command ] \[hostname/IP\_address]

| -4 | Force DNS resolution of the given hostname to the IPv4 namespace                                                                                                 |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -6 | Force DNS resolution of the given hostname to the IPv6 namespace                                                                                                 |
| -d | Set the debugging mode to on                                                                                                                                     |
| -c | Following argument is interpreted as an interactive format command; multiple -c options may be given                                                             |
| -i | Force ntpdc to operate in the interactive mode                                                                                                                   |
| -l | Obtain a list of peers known to the server(s); this switch is equivalent to -c listpeers                                                                         |
| -n | Output all host addresses in the dotted-quad numeric format, rather than hostnames                                                                               |
| -p | Print a list of the peers as well as a summary of their states; this is equivalent to -c peers                                                                   |
| -s | Print a list of the peers as well as a summary of their states, but in a slightly different format from that for the -p switch; this is equivalent to -c dmpeers |

FIGURE X: ntpdc parameters and their respective functions.

FIGURE X: ntpdc command output.

**ntpq**

This command monitors the operations of the NTP daemon ntpd and determines its performance. Its syntax is as follows:

ntpq \[-46dinp] \[-c command] \[host/IP\_address]

| -4 | Force DNS resolution to the given hostname to the IPv4 namespace                      |
| -- | ------------------------------------------------------------------------------------- |
| -6 | Force DNS resolution of the given hostname to the IPv6 namespace                      |
| -c | Following argument is an interactive format command; multiple -c options may be given |
| -d | Debugging mode                                                                        |
| -i | Force ntpq to operate in the interactive mode                                         |
| -n | Output all host addresses in the dotted-quad numeric format, rather than hostnames    |
| -p | Print a list of the peers as well as a summary of their states                        |

TABLE X: ntpq parameters and their respective functions.

**Example:**

ntpq> version

ntpq 4.2.8p15@1.3728-o

ntpq> host

Current host is localhost

FIGURE X: ntpq command output.

Note: In many Linux distributions, the NTP daemon ntpd has been joined with Chrony, chronyd. Both the daemons synchronize the local system’s time with a remote time server.

**NTP Enumeration Tools**

NTP enumeration tools are used to monitor the working of NTP and SNTP servers in the network and help in the configuration and verification of connectivity from the time client to the NTP servers.

**PRTG Network Monitor – PRTG NetMon**

(_**Source:**_ https://www.paessler.com)

PRTG monitors all systems, devices, traffic, and applications of IT infrastructure by using various technologies such as SNMP, WMI, and SSH. You can use (fantastic tool, by the way) Paessler’s PRTG (Paessler’s Router Traffic Grapher) Network Monitor (NetMon) to retrieve SNTP server details such as the response time from the server, active sensors with the server, and synchronization time.

FIGURE X: PRTG Network Monitor.

The following are some NTP enumeration tools:

**Nmap**

(_**Source:**_ https://nmap.org)

* **Description:** Nmap (Network Mapper) is a powerful and versatile open-source network scanning tool used for network discovery and security auditing. It can detect open ports, identify services running on those ports, and determine the operating system and other characteristics of network devices.
* **Use Cases:**
  * **NTP Service Detection:** Scans networks to identify devices running NTP (Network Time Protocol) services and determine their versions.
  * **Network Discovery:** Discovers devices on a network and maps their connections, providing a comprehensive overview of the network infrastructure.
  * **Security Auditing:** Identifies vulnerabilities and misconfigurations in NTP services, helping to enhance network security.
  * **Compliance Checking:** Ensures that NTP servers are configured according to organizational policies and industry standards.
  * **Penetration Testing:** Used by ethical hackers to identify and exploit weaknesses in NTP configurations during security assessments.

**Wireshark**

(_**Source:**_ https://www.wireshark.org)

* **Description:** Wireshark is a widely-used network protocol analyzer that captures and interactively analyzes network traffic. It provides deep inspection of hundreds of protocols, including NTP.
* **Use Cases:**
  * **Traffic Analysis:** Captures and analyzes NTP traffic to understand communication patterns and diagnose issues.
  * **Troubleshooting:** Helps identify and resolve problems related to NTP synchronization, such as incorrect timestamps or communication failures.
  * **Security Monitoring:** Detects suspicious NTP traffic that may indicate network attacks or misconfigurations.
  * **Performance Optimization:** Analyzes NTP traffic to ensure optimal time synchronization across network devices.
  * **Protocol Education:** Used as an educational tool to learn about the NTP protocol and its implementation details.

**UDP-Proto-Scanner**

(_**Source:**_ https://labs.portcullis.co.uk)

* **Description:** UDP-Proto-Scanner is a tool designed to scan UDP ports and identify the protocols running on them. It helps detect services that use UDP, such as NTP, and determine their presence and activity on the network.
* **Use Cases:**
  * **UDP Service Discovery:** Identifies UDP services, including NTP, running on network devices by scanning UDP ports.
  * **Security Assessment:** Detects potentially vulnerable or misconfigured UDP services, including NTP, for security auditing purposes.
  * **Network Inventory:** Provides an inventory of active UDP-based services across the network, helping with network management and monitoring.
  * **Incident Response:** Assists in identifying unusual or unauthorized UDP services that could indicate a security breach or compromise.
  * **Compliance Verification:** Ensures that UDP services, including NTP, are configured according to security policies and compliance requirements.

**NTP Server Scanner**

(_**Source:**_ https://www.bytefusion.com)

* _**Description:**_ NTP Server Scanner is a specialized tool for discovering and analyzing NTP servers within a network. It focuses on identifying NTP servers, checking their configurations, and assessing their performance.
* **Use Cases:**
  * **NTP Server Discovery:** Scans the network to find active NTP servers and gather information about them.
  * **Configuration Checking:** Verifies the configuration settings of NTP servers to ensure they meet best practices and security standards.
  * **Performance Monitoring:** Monitors the performance of NTP servers, including their synchronization accuracy and response times.
  * **Security Analysis:** Identifies potential security issues in NTP server configurations, such as open access or outdated software versions.
  * **Network Time Management:** Helps maintain accurate time synchronization across the network by ensuring all NTP servers are properly configured and functioning.

**NFS Enumeration**

NFS is a type of file system that enables users to access, view, store, and update files over a remote server. These remote data can be accessed by the client in the same way it is accessed on the local system. Depending on the privileges assigned to the clients, they can either only read or both read and write the data.

An NFS system is generally implemented on a computer network in which the centralization of data is required for critical resources. The Remote Procedure Call (RPC) is used to route and process the request between clients and servers.

To accomplish the task of sharing files and directories over the network, the “exporting” process is used; however, the client first attempts to make the file available for sharing by using the “mounting” process. The /etc/exports location on the NFS server contains a list of clients allowed to share files on the server. In this approach, to access the server, the only credential used is the client’s IP address. NFS versions before version 4 run on the same security specification.

Enumerating NFS services enables attackers to identify the exported directories, list of clients connected to the NFS server along with their IP addresses, and the shared data associated with the IP addresses. After gathering this information, the attackers can spoof their IP addresses to gain full access to the shared files on the server.

As shown in the screenshot, the rpcinfo command has been run to scan the target’s IP address for an open NFS port (port 2049) and any NFS-related services running on it:

rpcinfo -p \<Target IP Address>

FIGURE X: The rpcinfo command displaying open NFS port and services.

As shown in the figure below, I ran the following command to view a list of shared files and directories:

showmount -d \<Target IP Address>

FIGURE X: The showmount command displaying a shared directory.

Further, you can use various other commands and tools to gain access to the NFS server and upload malicious files on the server to launch further attacks.

**NFS Enumeration Tools**

NFS enumeration tools scan a network within a given range of IP addresses or a single IP address to identify the NFS services running on it. These tools also assist in obtaining a list of RPC services using the portmap command, a list of NFS shares, and a list of directories accessible through NFS; further, they allow downloading a file shared through the NFS server. Attackers use tools such as RPCScan and SuperEnum to perform NFS enumeration.

**RPCScan**

(**Source:** https://github.com/hegusung/RPCScan)

RPCScan communicates with RPC services and checks misconfigurations on NFS shares. As shown in the figure below, I ran the following command to enumerate a target IP address for active NFS services:

python3 rpc-scan.py \<Target IP Address> --rpc

FIGURE X: RPCScan tool displaying open NFS ports and services using Python and Parrot OS.

**SuperEnum**

(_**Source:**_ https://github.com/ncoderz/superenum)

SuperEnum includes a script that performs the basic enumeration of any port. As shown in the figure below, I used the ./superenum script and then entered a text file named “Target.txt” having a target IP address and list of IP addresses for enumeration.

FIGURE X: The SuperEnum tool running a script to enumerate NFS.

After scanning a target IP address, the script displays all the open ports, as shown in the below figure. Score! Port 2049 has an NFS service running.

FIGURE X: The SuperEnum tool displaying open NFS ports.

**SMTP and DNS Enumeration**

This section describes enumeration techniques to extract information related to network resources. It also covers DNS enumeration techniques that yield information about the DNS servers and network infrastructure of the target organization. The section also discusses both SMTP and DNS enumeration techniques, covering SMTP enumeration, the process of obtaining a list of valid users on an SMTP (email) server, SMTP enumeration tools, DNS zone transfer enumeration, DNS cache snooping, and DNS zone walking.

**SMTP Enumeration**

Mail systems commonly use SMTP with POP3 and IMAP, which enable users to save messages in the server mailbox and download them from the server when necessary. SMTP uses mail exchange (MX) servers to direct mail via DNS. It runs on TCP port 25, 2525, or 587.

SMTP provides the following three built-in commands:

* **VRFY:** Validates users

**$ telnet 192.168.168.1 25**

**Trying 192.168.168.1…**

**Connected to 192.168.168.1.**

**Escape character is ‘^]’.**

**220 CAmailserver ESMTP Sendmail 8.9.3**

**HELO**

**501 HELO requires domain address**

**HELO x**

**250 CAmailserver Hello \[10.0.0.86], pleased to meet you**

**VRFY Yvonne**

**250 Super-User \<Yvonne@CAmailserver>**

**VRFY Ennovy**

**550 Ennovy…User unknown**

* **EXPN:** Displays the actual delivery addresses of aliases and mailing lists

**$ telnet 192.168.168.1 25**

**Trying 192.168.168.1…**

**Connected to 192.168.168.1.**

**Escape character is ‘^]’.**

**220 CAmailserver ESMTP Sendmail 8.9.3**

**HELO**

**501 HELO requires domain address**

**HELO x**

**250 CAmailserver Hello \[10.0.0.86], pleased to meet you**

**EXPN Yvonne**

**250 Super-User \<Yvonne@CAmailserver>**

**EXPN Ennovy**

**550 Ennovy… User unknown**

* **RCPT TO:** Defines the recipients of the message

**$ telnet1 192.168.168.1 25**

**Trying 192.168.168.1 …**

**Connected to 192.168.168.1.**

**Escape character is ‘^]’.**

**220 CAmailserver ESMTP Sendmail 8.9.3**

**HELO**

**501 HELO requires domain address**

**HELO x**

**250 CAmailserver Hello 910.0.0.86], pleased to meet you**

**MAIL FROM: Yvonne**

**250 Yvonne… Sender ok**

**RCPT TO: Alyssa**

**250 Alyssa… Recipient ok**

**RCPT TO: Ennovy**

**550 Ennovy… User unknown**

SMTP servers respond differently to VRFY, EXPN, and RCPT TO commands for valid and invalid users; therefore, valid users on the SMTP server can be determined. Attackers can directly interact with SMTP via the Telnet prompt and collect a list of valid users on the SMTP server.

You can perform SMTP enumeration using command line utilities such as Telnet and netcat or by using tools such as Metasploit, Nmap, NetScanTools Pro, and smtp-user-enum to collect a list of valid users, delivery addresses, message recipients, and more.

**SMTP Enumeration Using Nmap**

_(**Source:** https://nmap.org)_

* The following command, when executed, lists all the SMTP commands available in the Nmap directory:

Nmap -p 25, 365, 587 -script=smtp-commands \<Target IP Address>

* Run the following command to identify SMTP open relays:

Nmap -p 25 -script=smtp-open-relay \<Target IP Address>

* Run the following command to enumerate all the mail users on the SMTP server:
* Nmap -p 25 -script=smtp-enum-users \<Target IP Address>

\
FIGURE X: Showing the output of the smtp-enum-users NSE script.

**SMTP Enumeration Using Metasploit**

Attackers use the Metasploit framework to enumerate SMTP users. The framework contains an SMTP enumeration module that allows attackers to connect to the target SMTP server and enumerate usernames using predefined wordlists. The SMTP server uses its inbuilt method **VRFY** to validate the usernames in the worldlist file with the users present on the server and displays the matched list of users.

**Steps to Enumerate SMTP Users Using Metasploit**

* **Step 1:** Launch Metasploit **msfconsole** and switch to the relevant auxiliary scanner to initiate the process: **auxiliary/scanner/smtp/smtp\_enum.**

**msf > use auxiliary/scanner/smtp/smtp\_enum**

**msf auxiliary (smtp\_enum)>**

* **Step 2:** Use the command **show options** to view the entire list of options required to perform this task. Alternatively, the command **show evasion** can be used to view the list of options to evade security solutions.



FIGURE X: Metasploit tool showing smtp\_enum options.

* **Step 3:** Use the option **set RHOST** to set the target SMTP server’s IP address or a range of IP addresses.
* **Step 4:** By default, the Metasploit framework uses default wordlists located at **/usr/share/64metasploit-framework/data/wordlists/unix\_users.txt** to enumerate SMTP users. The **USER\_FILE** option can be set to use custom wordlists.

**msf auxiliary (smtp\_enum) > set USER\_FILE \<location of wordlists file>**

* **Step 5:** Use the command **show advanced** to view the complete list of available options in the SMTP user enumeration module.
* **Step 6:** Execute the **run** command to begin the enumeration process. It scans the given wordlists with the SMTP server users and lists all the matched usernames.

\
FIGURE X: Screenshot of Metasploit showing smtp\_enum advanced options.



FIGURE X: Metasploit tool retrieving SMTP users.

As shown in the figure above, attackers can obtain a list of valid SMTP users from the target SMTP server and can use this information to initiate targeted attacks.

**SMTP Enumeration Tools**

SMTP enumeration tools are used to perform username enumeration. Attackers can use the usernames obtained from this enumeration to launch further attacks on other systems in the network.

* **NetScanTools Pro**

_(**Source:**_ [_https://www.netscantools.com_](https://www.netscantools.com/)_)_

NetScanTools Pro’s SMTP Email Generator tool tests the process of sending an email message through an SMTP server. Attackers use NetScanTools Pro for SMTP enumeration and extract all the email header parameters, including confirm/urgent flags. Attackers can also record the email session in a log file and then view the communications between NetScanTools Pro and the SMTP server in the log file.

FIGURE X. NetScanTools Pro.

* **Smtp-user-enum**

_(**Source:**_ [_http://pentestmonkey.net_](http://pentestmonkey.net/)_)_

Smtp-user-enum is a tool for enumerating OS-level user accounts on Solaris via the SMTP service (sendmail). Enumeration is performed by inspecting the responses to VRFY, EXPN, and RCPT TO commands. As show in the figure above, smtp-user-enum needs to be passed on to a list of users and at least one target running an SMTP service. The syntax for using smtp-user-enum is as follows:

Smtp-user-enum.pl \[options] (-u username | -U file-of-usernames) (-t host | -T file-of-targets)

*
  * **-m n:** Maximum number of processes (default: 5)
  * **-M mode:** Specify the SMTP command to use for username guessing from among EXPN, VRFY, and RCPT TO (default: VRFY)
  * **-u user:** Check if a user exists on the remote system
  * **-f addr:** Specify the from email address to use for “RCPT TO” guessing (default: user@example.com)
  * **-D dom:** Specify the domain to append to the supplied user list to create email addresses (default: none)
  * **-U file:** Select the file containing usernames to check via the SMTP service
  * **-t host:** Specify the server host running the SMTP service
  * **-T file:** Select the file containing hostnames running the SMTP service
  * **-p port:** Specify the TCP port on which the SMTP service runs (default: 25)
  * **-d:** Debugging output
  * **-t n:** Wait for a maximum of n seconds for the reply (default: 5)
  * **-v:** Verbose
  * **-h:** Help message

FIGURE X: smtp-user-enum tool output.

**DNS Enumeration Using Zone Transfer**

DNS zone transfer is the process of transferring a copy of the DNS zone file from the primary DNS server to a secondary DNS server. In most cases, the primary DNS server maintains a backup or secondary server for redundancy, which holds all the information stored in the primary server. The DNS server uses zone transfer to distribute changes made to the main server to the secondary server(s). An attacker performs DNS zone transfer enumeration to locate the DNS and access records of the target organization. If the DNS server of the target organization allows zone transfers, then attackers can perform DNS zone transfer to obtain DNS server names, hostnames, machine names, usernames, IP addresses, aliases, and more, assigned within a target domain.

In DNS enumeration using zone transfer, an attacker attempts to retrieve a copy of the entire zone for a domain from the DNS server. Attackers can perform DNS zone transfer using tools such as nslookup, dig command, and DNSRecon. If the DNS transfer setting is enabled on the target name server, it will provide the DNS information; else, it will return an error stating it has failed or refused the zone transfer.

To perform a DNS zone transfer, the attacker sends a zone transfer request to the DNS server pretending to be a client; the DNS server then sends a portion of its database as a zone to the attacker. This zone may contain a large amount of information about the DNS zone network.

* **Dig Command**

Attackers use the **dig** command on Linux-based systems to query the DNS name servers and retrieve information about the target host addresses, name servers, mail exchanges, and more. As shown in the figure below, attackers can use the following command to perform DNS zone transfers:

dig ns \<target domain>

The above command retrieves all the DNS name servers of the target domain. Next, attackers use one of the name servers from the output of the above command to test whether the target DNS allows zone transfers. They use the following command for this purpose:

Dig @\<domain of name server> \<target domain> axfr

FIGURE X: Linux DNS zone transfer using the dig command.

* **nslookup Command**

_(_**Source:** _https://docs.microsoft.com)_

You can use the nslookup command on Windows-based systems to query the DNS name servers and retrieve information about the target host addresses, name servers, mail exchanges, and more. As shown in the figure below, you can use the following command to perform DNS zone transfers.

**Nslookup**

Set querytype=soa

\<target domain>

The above command sets the query type to the _**Start of Authority (SOA)**_ record to retrieve administrative information about the DNS zone of the target domain **certifiedhacker.com.** The following command is used to attempt to transfer the zone of the specified name server:

/ls -d \<domain of name server>

FIGURE X: Windows DNS zone transfer using the nslookup command.

* **DNSRecon**

_(_**Source:** _https://_

Attackers use DNSRecon to check all NS records of the target domain for zone transfers. As shown in the figure below, attackers can use the following command for DNS zone transfers:

dnsrecon -t axfr -d \<target domain>

In the above command, the **-t** option specifies the type of enumeration to be performed, **axfr** is the type of enumeration in which all NS servers are tested for a zone transfer, and the **-d** option specifies the target domain.

FIGURE X: DNS zone transfers using DNSRecon.

**Attacking SNMP**

**DNS Cache Snooping Attack**

DNS cache snooping is a type of DNS enumeration technique in which an attacker queries the DNS server for a specific cached DNS record. By using this cached record, the attacker can determine the sites recently visited by the user. This information can further reveal important information such as the name of the owner of the DNS server, its service provider, the name of its vendor, and bank details. By using this information, the attacker can perform a social engineering attack on the target user. Attackers perform DNS cache snooping using various tools such as the dig command, and DNSRecon.

Attackers use the following two DNS cache snooping methods to snoop on a target domain.

* **Non-Recursive Method**

In this method, to snoop on a DNS server, attackers send a non-recursive query by setting the _**Recursion Desired (RD)**_ bit in the query header to zero. Attackers query the DNS cache for a specific DNS record such as A, CNAME, PTR, CERT, SRV, and MX. If the queried record is present in the DNS cache, the DNS server responds with the information indicating that some user on the system has visited a specific domain. Otherwise, the DNS server responds with the information about another DNS server that can return an answer to the query, or it replies with the **root.hints** file containing information about all root DNS servers.

Attackers use the **dig** command followed by the name and IP address of the DNS server, domain name, and type of DNS record file. The **+norecurse** option is used to set the query to non-recursive.

dig @\<IP of DNS server> \<Target domain> A +norecurse

As shown in the screenshot below, the status **NOERROR** implies that the query was accepted but no answer was returned, thereby indicating that no user from the system had visited the queried site.

FIGURE X: A dig query for a site that is not cached.

* **Recursive Method**

In this method, to snoop on the DNS server, attackers send a recursive query by setting the +recurse option instead of the +norecurse option. Similar to the non-recursive method, the attackers query the DNS cache for a specific DNS cache for a specific DNS record such as A, CNAME, PTR, CERT, SRV, and MX.

In this method, the _**Time to Live (TTL)**_ field is examined to determine the duration for which the DNS record remains in the cache. Here, the TTL value obtained from the result is compared with the TTL that was initially set in the TTL field. If the TTL value in the result is less than the initial TTL value, the record is cached, indicating that someone on the system has visited the site; however, if the queried record were not present in the cache, it will be added to the cache after the first query is sent.

Attackers use the same **dig** command as in the non-recursive method but with the **+recurse** option instead of the **+norecurse** option:

**Dig @\<IP of DNS server> \<Target domain> A +recurse**

As shown in the figure below, the TTL value for the domain **certifiedhacker.com** is considerably high, which strongly suggests that the domain record was not in the cache when the query was issued.

FIGURE X: A dig query for a cached site.

**DNS Zone Walking Attack**

Domain Name System Security Extensions (DNSSEC) zone walking is a type of DNS enumeration technique in which an attacker attempts to obtain internal records if the DNS zone is not properly configured. The enumerated zone information can assist the attacker in building a host network map.

Organizations can use DNSSEC to add security features and enhancements to the DNS data and provide protection against known threats to the DNS. This security feature uses digital signatures based on public-key cryptography to strengthen authentication in DNS. These digital signatures are stored in the DNS name servers along with common records such as MX, A, AAAA, and CNAME.

While DNSSEC provides internet security, it is also susceptible to a vulnerability called _**zone enumeration**_ or _**zone walking.**_ By exploiting this vulnerability, you can obtain vital information of a target domain, based on which they may launch internet-based attacks.

To overcome the zone enumeration vulnerability, a new version of DNSSEC that uses Next Secure version 3 (NSEC3) is used. The NSEC3 record provides the same functionality as NSEC records, except that it provides cryptographically hashed record names that are designed to prevent the enumeration of record names present in the zone.

To perform zone enumeration, you can use various DNSSEC zone enumerators such as **LDNS, DNSRecon, nsec3map,** and **DNSwalk.**

**DNSSEC Zone Walking Tools**

DNSSEC zone walking tools are used to enumerate the target domain’s DNS record files. These tools can also perform zone enumeration on NSEC and NSEC3 record files and further use the gathered information to launch attacks such as denial of service (DoS) attacks and phishing attacks.

* **LDNS**

_(_**Source:** _https://www.nlnetlabs.nl)_

LDNS-walk enumerates the DNSSEC zone and obtains results on the DNS record files.

As shown in the figure below, you can use the following query to enumerate a target domain **iana.org** using the DNS server **8.8.8.8** to obtain DNS record files:

**Ldns-walk @\<IP of DNS Server> \<Target domain>**

FIGURE X: LDNS displaying results on the target domain.

* **DNSRecon**

_(_**Source:** _https://_

DNSRecon is a zone enumeration tool that assists users in enumerating DNS records such as A, AAAA, and CNAME. It also performs NSEC zone enumeration to obtain DNS record files of a target domain.

A shown in the screenshot below, you can use the following query to perform zone enumeration against a target domain **certifiedhacker.com:**

**Dnsrecon -d \<target domain> -z**



FIGURE X: DNSRecon displaying results on the target domain.

**DNS and DNSSEC Enumeration Using Nmap**

**DNS Enumeration Using Nmap**

Attackers use Nmap to scan domains and obtain a list of subdomains, records, IP addresses, and other valuable information from the target host.

* Run the following command to list all the available services on the target host:

**Nmap –script=broadcast-dns-service-discovery \<Target Domain>**



**What Are the Steps Involved in Performing Enumeration?**

Hackers need to be methodical in their approach to hacking. The following steps are an example of those a hacker might perform in preparation for hacking a target system.

**1.** Extract usernames using enumeration.

**2.** Gather information about the host using NULL sessions.

**3.** Perform Windows enumeration using well-known tool and techniques.

**4.** Acquire user account using the command line switches provided.

**5.** Perform SNMP port scanning.

**Chapter Summary**

In this chapter, you learned how to:

* **Understand how to enumerate user accounts.** Enumeration involves making active connections to systems through either SMB/CIFS or NetBIOS vulnerabilities and querying target systems for information.
* Be aware of the type of information that can be enumerated on a system. The type of information enumerated by hackers includes network resources and shares, users and groups, and applications and banners.
* Understand NULL sessions. Connecting to a target system using a blank password is known as a NULL session. NULL sessions are often used by hackers to connect to target systems and then run enumeration tools against the system.
* Know the types of enumeration tools. NetBIOS and SNMP enumerations can be performed using tools such as SNMPUtil and enum4linux.
* Know how to perform a DNS zone transfer on Windows operating systems. Nslookup can be used to perform DNS zone transfers.
* Understand SNMP enumeration countermeasures. Turn off the SNMP services, or change the default read and read/write community strings and names.
* Know how to identify vulnerable accounts. Tools such as User2SID, SID2User, and UserInfo can be used to identify vulnerable user, group, and service accounts.
* File Transfer Protocol (FTP) uses TCP port 21. This is a well-known port number and can be found in the Windows services file.
* The Hypertext Transfer Protocol Secure (HTTPS) uses TCP port 443. This is a well-known port number and can be found in the Windows services file.
* War dialing involves placing calls to a series of numbers in hopes that a modem will answer the call. It can be used to test the security of a remote-access system.
* Banner grabbing is not detectable; therefore, it is considered passive OS fingerprinting.
* A port, network, and vulnerability are the three types of scanning.
* A SYN packet is followed by a SYN/ACK packet. Then, an ACK finishes a successful TCP connection, or the TCP Three-Way Handshake.
* An XMAS scan has all flags set.
* The command nmap -Ss paranoid performs a SYN scan every 300 seconds or every 5 minutes.
* Block the ports used by NetBIOS null sessions. These are ports 139 and 445.
* Port 137 is used for NetBIOS null sessions.
* The SNMP read/write community name is the password used to make changes to the device configuration.
* Ports in the 135 to 139 range indicate the system has SMB services running and is susceptible to null sessions.
* Enumeration is the process of finding usernames, machine names, network shares, and services on the network.
* SID2User is a command line tool to find a username from a SID.
* Nslookup is a Windows tool that can be used to initiate a DNS zone transfer that sends all the DNS records to a hacker’s system.
* A null session involves connecting to a system with no username or password.
* The best countermeasure to SNMP enumeration is to remove the SNMP agent from the device. Doing so prevents it from responding to SNMP requests.

**Recommended Reading and Resources**

Here is a curated list of 15 recommended resources for learning about ethical hacking, with special focus on enumeration and other aspects of the field. Each entry includes a brief description and a link for further exploration.

**Literature:**

1. _**“Hacking: The Art of Exploitation,”**_**&#x20;by Jon Erickson**

_(**Source:** https://www.amazon.com/Hacking-Art-Exploitation-Jon-Erickson/dp/0321502786)_

* A seminal text that dives deep into the technical aspects of hacking, providing a firm understanding of the tools and techniques employed by hackers.

1. _**“The Basics of Hacking and Penetration Testing: Ethical Hacking and Penetration Testing Made Easy,”**_**&#x20;by Patrick Engebretson**

_(**Source:** https://www.amazon.com/Basics-Hacking-Penetration-Testing-Ethical/dp/0128000447)_

* Offers a clear, concise introduction to the core concepts and techniques used in penetration testing with practical exercises for beginners.

1. _**“CEH Certified Ethical Hacker: All-in-One Exam Guide,”**_**&#x20;by Matt Walker**

_(**Source:** https://www.amazon.com/CEH-Certified-Ethical-Hacker-Exam-Guide/dp/111943818X)_

* Comprehensive guide covering all topics necessary to pass the CEH exam, aimed at those aspiring to become certified ethical hackers.

1. _**“The Hacker Playbook 2: Practical Guide to Penetration Testing,”**_**&#x20;by Peter Kim**

_(**Source:** https://www.amazon.com/Hacker-Playbook-Practical-Guide-Penetrating/dp/1593275079)_

* Provides real-world scenarios and practical steps for conducting effective penetration tests, suitable for intermediate-level readers.

1. _**“Red Team Field Manual (RTFM) v2,”**_**&#x20;by Ben Clark**

_(**Source:** https://www.amazon.com/Red-Team-Field-Manual-Ben/dp/0991102807)_

* Offers insights into the mindset and tactics of red teams, focusing on advanced penetration testing and adversarial thinking.

1. _**“Hands-On Hacking: The Practice of Hacking for Testers,”**_**&#x20;by Peter Kim**

(_**Source:** https://www.amazon.com/Hands-Hacking-Practice-Hacking-Testers/dp/1593275095_)

* Focuses on practical exercises and real-world scenarios, making it an excellent choice for those looking to apply their hacking skills in a controlled environment.

1. _**“Metasploit: The Penetration Tester’s Guide,”**_**&#x20;by David Kennedy, Devon Kearns, Mati Aharoni, and Chris Eagle**

(_**Source:** https://www.amazon.com/Metasploit-Penetration-Testers-Guide-Kennedy/dp/1118026470_)

* A comprehensive guide to using Metasploit for penetration testing, covering everything from setup to exploiting vulnerabilities.

**Online Courses:**

1. _**“The Complete Cyber Security Course! Volume 1: Hackers Exposed”**_

(_**Source:** https://www.udemy.com/course/the-complete-cyber-security-course/_)

* An online course that covers the basics of cybersecurity, including ethical hacking techniques and best practices for securing networks.

1. _**“The Complete Ethical Hacking Bootcamp”**_

(_**Source:** https://www.udemy.com/course/the-complete-ethical-hacking-bootcamp/_)

* A comprehensive bootcamp that covers the fundamentals of ethical hacking, including enumeration, scanning, and exploitation techniques.

1. _**“Kali Linux: Assessing Wireless Networks”**_

(_**Source:** https://www.packtpub.com/product/kali-linux-assessing-wireless-networks/9781783553361_)

* Focuses on assessing wireless networks using Kali Linux, a popular distribution for penetration testers and security professionals.

1. _**“Wireshark Network Analysis: The Official Wireshark Certified Analyst Study Guide”**_

(_**Source:** https://www.amazon.com/Wireshark-Network-Analysis-Certified-Study/dp/0134608091)_

* Covers the use of Wireshark for network analysis, providing solid foundations in packet analysis and network troubleshooting.

1. _**“Penetration Testing: A Hands-On Introduction to Hacking”**_

(_**Source:** https://www.amazon.com/Penetration-Testing-Hands-Hacking-Introduction/dp/1118026470)_

* Introduces readers to the world of penetration testing, emphasizing the importance of ethics and legality in the field.

1. _**“The Web Application Hacker’s Handbook: Discovering and Exploiting Security Flaws”**_

(_**Source:** https://www.amazon.com/Web-Application-Hackers-Handbook-Discovering-Exploiting-Security/dp/1118026470_)

* Focuses on discovering and exploiting security flaws in web applications, providing a deep dive into web application security.

1. _**“The Social Engineer’s Toolkit (SET)”**_

(_**Source:** https://www.trustedsec.com/products/social-engineers-toolkit-set/_)

* A collection of tools designed to aid in social engineering assessments, teaching readers how to leverage human interaction to gain unauthorized access.

1. _**“OWASP Top Ten Project”**_

(_**Source:** https://owasp.org/index.php/Main\_Page_)

* A project focused on creating a list of the top ten most critical web application security risks, providing guidance on how to mitigate these vulnerabilities.

These resources offer a mix of books, online courses, and official documentation that collectively cover the breadth of ethical hacking, from beginner to advanced topics, ensuring a comprehensive understanding of the field.
