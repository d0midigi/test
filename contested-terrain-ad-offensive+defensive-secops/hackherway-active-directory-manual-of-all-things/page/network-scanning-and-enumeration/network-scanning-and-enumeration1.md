# Network Scanning and Enumeration1

| <img src="../../.gitbook/assets/0 (51).png" alt="A close up of a light

Description automatically generated" data-size="original"> | <p>Network Scanning and Enumeration</p><p>CHAPTER OBJECTIVES INCLUDE:</p><p><strong>Network Scanning</strong></p><ul><li>Define Port Scanning, Network Scanning, and Vulnerability Scanning</li><li>Understand the Network Scanning and Enumeration Methodologies</li><li>Understand Ping Sweeping Techniques</li><li>Understand Nmap Command Switches and the Nmap Scripting Engine (NSE)</li><li>Understand SYN, Stealth, XMAS, NULL, SYN/ACK, FIN, and IDLE Scans</li><li>List TCP Communication Flag Types and ICMP Message Levels</li><li>Understand War Dialing Techniques</li><li>Understand Banner Grabbing and OS Fingerprinting Techniques</li><li>Understand How Proxy Servers Are Used in Launching an Attack</li><li>Explain How Anonymizers Work</li><li>Understand IP Spoofing Attacks and Techniques</li></ul><p><strong>Enumeration</strong></p><ul><li>Understand and Explain Enumeration Processes</li><li>Understand Enumeration Methodology</li><li>Explain and Understand NULL Sessions</li><li>Define Types of Enumeration: SNMP, DNS, SMB, RPC, ICMP, DHCP, Active Directory Domain Enumeration and Subdomain Enumeration</li><li>Define Steps in Performing Enumeration Tasks</li></ul> |
| ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### Technology Brief

After Reconnaissance and Footprinting, you may have enough information about your target to move onto the next phase: Network Scanning and Enumeration. In short, network scanning is a method of mining information from target entities such as identification of hosts on a network, port information and service versions, open ports, OS and asset discovery, plus more. The main objectives of network scanning include:

* To identify live hosts on a network
* To identify open and closed ports
* To identify operating system information
* To identify services running on a network
* To identify active processes on a network
* To identify the presence of security devices, such as firewalls and IDS
* To identify system and network infrastructure, architecture, and topology
* To identify running services and their versions
* To identify open and exploitable vulnerabilities

Network scanning and enumeration represent, in my view, the 2.5th phase of hacking, focusing on the hacker’s efforts to locate target systems or networks. The classification of this phase varies significantly across different perspectives, with discrepancies arising from the interpretation of the hacking lifecycle stages. While some might categorize network scanning as the second phase, followed by enumeration as either the third, fourth, or even fifth phase, I propose that combining these two processes encapsulates the essence of the hacking lifecycle’s middle stages. Together, they serve to accumulate as much information as possible about your target, acting in tandem to lay the groundwork for subsequent hacking and attacking actions.

These two processes are inherently interconnected; network scanning is a prerequisite for enumeration, and vice versa. Enumeration, without prior scanning, would leave you in the dark about your target’s layout and potential vulnerabilities. Similarly, scanning alone, without the detailed insights gained from enumeration, would limit the effectiveness of identifying exploitable weaknesses. Just as going into battle without knowing the terrain and enemy positions would be unwise, initiating an attack without a clear understanding of the target system’s structure and defenses is equally risky.

Therefore, in this chapter, we will lead you through the initial objectives and requirements for performing network scanning and enumeration in support of an ethical hacking security assessment, penetration test, or vulnerability assessment. This includes discussing the final phase of reconnaissance, _vitality._ After that, we will dig into some scenarios in which you will see how you can use these different tools and techniques to their full advantage. Furthermore, this chapter aims to delve into the methodologies surrounding both network scanning and enumeration, highlighting their pivotal roles within the ethical hacking lifecycle. By understanding and applying these techniques effectively, you can enhance your abilities to identify and exploit vulnerabilities, ultimately contribute to strengthening the security posture of the systems you may be tasked to protect.

\
![A diagram of a diagram

Description automatically generated](<../../.gitbook/assets/1 (37).png>)

### CHAPTER OBJECTIVES

In an ethical hacking security assessment, or penetration test, there are implied boundaries. Depending on the breadth and scope of your testing, you may be limited to testing only a certain number or specific type of host or information system, or you may be free to test and probe anything your client owns or operates. Under an agreed upon written, signed, and authorized agreement, or _“get out of jail free”_ card before any scanning activities take place.

To properly scan and identify systems, you first need to know what the end state is for your assessment. Once the network scanning, probing, footprinting, fingerprintint, and enumeration are complete, you should then:

* Confirm that identified IP addresses during the reconnaissance stage are ping’able and online. This is the _**“vitality”**_ phase of reconnaissance.
* Be able to identify the purpose and type of the identified target systems, that is, what they are and what they do, what services they provide, or what their role and/or function is on the network.
* Have specific information about the versions of the services that are running on the systems. This can include BIOS and kernel versions and builds, operating system versions, patch and hotfix versions, and more.
* Have a concise list of targets and services which will directly feed into further penetration testing activities.

### Before You Start

Now that we’re moving into some ethical hacking security assessment, or pentesting scenarios which will actually “touch” the remote systems, we need to be concerned about the rules around our testing methods. With any kind of functional security testing, before any packets are sent or any configurations are reviewed, make sure the client has approved all of the tasks in writing. If any systems become unresponsive, you need to show that management approved the tests you were attempting to conduct. It is not uncommon for system owners to be unaware when a test has been tentatively scheduled for any given system, or clusters of such.

A common document to use for such approval is a _**“Rules of Engagement (RoE)”**_ document. This document should be drafted by the client or system owners and shall contain the ‘dos and ‘don’ts of what you can and what you cannot do, what is deemed in and out-of-bounds during the security assessment. A RoE, at a minimum, should contain and include:

* A detailed list of all concerned parties involved, including testers and responsible system owners, stakeholders, and representatives, with full contact information including off-hours contact information if needed. At least one party on each side should be designated as the primary contact, or POC, for any critical findings, communications, and events that need immediate attention and response.
* A complete asset inventory listing all equipment (both logical and physical) along with Internet Protocol (IP) addresses for testing. This shall include systems that are currently offline, systems that are on any exception lists (deny or allowlists) and excluded systems.
* Rules around compromising systems for deeper penetration and vulnerability exploration.
* Acceptable and unacceptable practices such as compromising physical site security, social engineering employees both in physical and electronic form, access to restricted areas for specialized security assessment testing.
* Agreement of use of data from compromised systems as well as how this (often confidential) data is marked, classified, and stored.
* The time frame for testing (including start and hard stops):
  * The duration of the testing
  * Acceptable times during the day or night, off-hours, and weekends
  * Any times that are prohibited from testing
* Any specific documentation or deliverables that are expected including, but not limited to:
  * Documentation around discoveries and methodologies (including tools) used
  * Proof of Concept (POC) of successful hacking/penetration system compromise and reproducibility
  * Debriefing schedule
  * Reporting and deliverables format
* Limitations of liability for any damage caused by the testing.

Having this type of document agreed to an in place prior to your ethical hacking activities will help to ensure that both you and your client are crystal clear on the level and type of testing to occur. The more precise, granular, and extensive the document is, the less room there is for any misunderstandings. One of the worst situations a hacker can find themselves in is one where the client is furious because the tester brought down a production system without authorization. Agreeing on the rules of engagement and a mutually agreed upon scope of the testing up front can help prevent issues of these types from occurring.

### Why Perform Network Scanning and Enumeration?

If you are given a list of targets, or subnets, some of your work has already been done for you. Most consider the reconnaissance and enumerating phases of security assessments the most frustrating parts of any security engagement as it often involves the hacker to having to go on a lengthy hunt to track down all assets or track down particulars of identified assets with little to no descriptive information about them. In turn, this may motivate you to track down other targets that may exist within trusted subnets that your client may have forgotten about, or simply did not know about. Regardless of this, you need to follow a process to ensure the following:

* You are testing only approved and in-scope targets
* You are accumulating, aggregating, and correlating as much information as possible before increasing the depth of and aggressiveness of your attacks
* You can identify the purposes and types of your targets, that is, what services they provide your client
* You have specific information about the versions and types of services that are running on your client’s systems
* You can recognize your target systems by purpose and resource offerings

Once you have figured out what your targets are and how many of them may or may not be vulnerable, you will then be able to select your tools and exploitation methods. Not only do poor system scanning and enumeration decrease the efficiency and effectiveness of your testing, but also eliminates the extra, unnecessary traffic that increases your chances of being detected. In addition, attacking one service with a method designed for another is insufficient and may create an unwanted or unforeseen Denial of Service (DoS). In general, _**do not test vulnerabilities unless you have been specifically tasked with that job.**_ Do not go on a threat hunt unless specifically authorized and have the allowance to do so. Only test for what is in your agreed up scope. If you do, however, encounter a critical vulnerability that was found by chance, or was not contained within the scope of limitations, it is best to stop all testing at that point, and immediately bring it up to your system owners and management. Keep in mind that transparency is everything when it comes to testing systems that you do not own, and it keeps you out of trouble.

The purpose of this chapter is to help guide and help you understand the need for network scanning and enumeration activities after your reconnaissance, information gathering, footprinting and fingerprinting is complete, and will help you to learn how to best perform these activities with available commercial and open-source tools. We will discuss the specific tools that help reveal the characteristics of your targets, including what services they offer, and the versions and types of resources they offer. Without this foundation, your testing will lack focus, and may not give you the depth in access that you (or your customers) are seeking. Not all tools are created equal, and that is one of the things this chapter will illustrate. Performing a security assessment within time constraints can be difficult enough; let the right tools for the job do some of the heavy lifting for you.

### Introduction to Network Scanning

During the network scanning phase, you will begin to gather information about the target’s purpose – specifically, what ports (and possibly what services) it offers. Information gathered during this phase is also traditionally used to determine the operating system (or firmware version) of the target devices. The list of active targets gathered from the reconnaissance hase is used as the target list for this phase. This is not to say that you cannot specifically target any host within your approved ranges but understand that you may lose time trying to scan a system that perhaps does not exist or may not be reachable from your network location. Often your penetration tests are limited in time frame, so your steps should be as streamlined as possible to keep your time productive. In simpler terms: Scan only those hosts that appear to be alive and online, unless you literally have ‘time to kill.’

**TIP:**

Although more businesses and organizations are becoming aware of the value of ethical hacking security assessments and penetration testing, they still want to see the time/value trade-off. As a result, penetration testing often becomes less an “attacker-proof” test and more a test of the client’s existing security controls and configurations. If you have spent any time researching network attacks, you probably know that most decent attackers will spend as much time as they can spare gathering information on their target before they attack; however, as a penetration tester, your time will likely be billed on an hourly basis, so you need to be able to effectively use that time you have. Make sure your time counts toward providing the best service you can for your client.

Network scanning uses some basic techniques and protocols for determining the accessibility of a system and gathering some basic information on what the system is, and which ports are open on it. The core technologies that we will be focusing on include _**Internet Control Message Protocol (ICMP)**_ and some elements of how _**Transmission Control Protocol (TCP)**_ functions and the available TCP flags.

#### How Scanning Works

During network scanning, your goal as an attacker is to gather as much information as possible about the network you’re targeting. This includes details such as IP addresses, operating systems, service versions, and installed applications. These details are crucial in determining the most effective type of exploit to use for compromising a system. Network scanning is the process of identifying systems that are in a listening state and responding on the network. Techniques such as ping sweeps, port scans, and OS fingerprinting help attackers map out the network architecture and identify potential entry points.

Ethical hackers, while working under legal boundaries, use these same techniques to target a system’s IP address and more. An in-depth understanding of network protocols such as TCP, UDP, ICMP, and IP is essential before delving into this chapter. Once an adversary has identified a target system and performed initial reconnaissance, they focus their efforts on gaining access to the target infrastructure. Network scanning provides valuable insights into the target, including the operating system, running services and potential configuration weaknesses. With this information, you can craft a precise attack strategy to exploit vulnerabilities to gain unauthorized access.

From a defensive standpoint, network scanning is a double-edged sword. While attackers use it to gather information and identify vulnerabilities, defenders use similar techniques to fortify their networks. As a defender, your objective is to continuously monitor and scan your network to identify any unauthorized systems or services. This proactive approach allows you to detect potential security gaps before they ca be exploited by malicious actors.

Ethical hackers, in a defensive role, must also possess a deep understanding of network protocols such as TCP, UDP, ICMP, and IP. This knowledge enables you to better identify unusual traffic patterns and anomalies that may indicate a scanning or reconnaissance attempt. Network scanning helps defenders map their network, understand the services running on various systems, and ensure that configurations adhere to security best practices.

The list of potential targets acquired from the reconnaissance phase can be rather expansive. To streamline the network scanning processes, it makes perfect sense to first determine whether the systems are still up and responsive to ICMP Echo Requests. Although the nonresponsive systems should not be in the list, it is possible that a system was downed after that phase and may not be answering requests when your scanning commences. You can use several methods to test a connected information system’s availability, but the most common technique is through the use of ICMP packets, or _ping packets._

Chances are that if you have done any type of network troubleshooting, you will recognize this as the protocol that ping uses. The ICMP Echo Request packet is a basic one which Request for Comments (RFC) 1122 (_**Source:**_ [_www.ietf.org/rfc/rfc1122.txt_](http://www.ietf.org/rfc/rfc1122.txt)) says _“every Internet host should implement and respond to.”_ In reality, however, many networks, internally and externally block ICMP echo requests to defend against one of the earliest DoS attacks, the Ping Flood, or Ping of Death attack. They may also block it to prevent scanning from outside the perimeter network, adding an element of stealth.

If ICMP packets are blocked, you can also use TCP ACK packets. This is often referred to as a _**“TCP Ping.”**_ The RFC states that _“unsolicited ACK packets should return a TCP RST.”_ So, if you send this type of packet to a port that is allowed through a firewall or router ACL, such as port 80, the target should respond with an RST indicating that the target is active.

When you combine either ICMP or TCP ping methods to check for active targets in a range, you perform a _ping sweep._ Such a sweep should be done and captured to a log file that specifies identified active machines which you can later input into a vulnerability scanner. Most scanner tools will accept a carriage-return-delimited file of IP addresses (e.g., a .txt, .csv, or XML file), or a file containing identified subnets (e.g., 10.10.10.10-10.10.10.150).

### Integrated Offensive and Defensive Strategy

Network scanning is not limited to intrusion; it is an extended form of reconnaissance where you gather more detailed information about your target. Both attackers and defenders need to be aware of the techniques and tools used in network scanning to either exploit, cause mass pwnage, or protect network assets effectively. Understanding the mindset and tactics, techniques, and procedures (TTPs) of an adversary allows you to anticipate potential attacks and implement solid security measures.

For ethical hackers and security professionals, mastering network scanning is equally important for both offensive and defensive/ethical hacker and unethical hacker/attacker and defender operations. Offensive tactics involve identifying vulnerabilities and exploiting them, while defensive strategies focus on detecting, mitigating, and preventing potential threats. By comprehensively understanding network scanning from both perspectives, you can better protect and attack their networks and respond and react according to the situation at hand.

As an ethical hacker, it is imperative that you possess an in-depth understanding of network protocols such as TCP, UDP, ICMP, and IP before reading this chapter. Once an adversary has identified a target system and does initial reconnaissance, as discussed in the previous chapter on reconnaissance and footprinting, the adversary concentrates efforts on gaining initial access into the target infrastructure. It should be noted that network scanning is not limited to intrusion alone. It can also be an extended form of reconnaissance (if you think about it) where the adversary obtains even more information about the target, such as what operating system is used, the services that are being run on the systems, and whether any configuration lapses can be identified. The adversary can then strategize an attack, factoring in these aspects.

### Overview of Network Scanning

The network scanning phase includes probing a target network to mine extremely useful information for building and strategizing a plan of attack against a specific entity whether it be a person, or an organizational entity. This detailed analysis of a network, its ports, and the services running on it helps create a network architecture, giving you a clearer understanding of your target of interest.

### Fundamentals

Our first step after performing reconnaissance on our target is to commence network scanning. Before we dive into it, I think it’s important to first touch upon a few networking basic concepts. While in the reconnaissance phase, we were gathering information freely available, “_10,000-foot view”_ information. When it comes to networks canning, however, we’re talking about a much more focused effort. Reconnaissance and footprinting may have shown us a range of network addresses the target organization uses, but how can we make use of that information? How can we turn that information into something that is useful and meaningful? By conducting network scanning, network scanning is going to tell us which of those addresses are in use and ideally what’s using those addresses. Now, that means more to me than simply just having a range of addresses and having no idea what to do with them. That’s actionable data.

In sum, _network scanning_ is the process of discovering systems on a network and looking at what open ports and applications may be running. With reconnaissance and footprinting, we wanted to know how big the network was and some general information about its topology and overall makeup. In network scanning, we’ll go into the network and start touching each device to find out more about it. But before we get into the actual process of network scanning, we really need to cover some basic TCP/IP networking knowledge.

A quick overview of the Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) and how they tie into network scanning.

### TCP (Transmission Control Protocol) Communication

We covered some networking basics earlier in this book, but if we’re going to talk network scanning intelligently, we’re going to need to dive just a bit deeper. As you’ll recall, when a recipient system gets a _**frame**_, it checks the physical address to see who the message is intended for. If the address is indeed correct, the recipient opens the frame, checks to make sure the frame is valid, and then ditches the header and trailer, passing the remainder up to Layer 3, the Network layer in the OSI model. There, the Layer 3 address is verified in the _**packet**_ header, along with a few other items, and the headers are stripped off. The remaining _**PDU (Protocol Data Unit)**_ now called a _**segment**_, is passed to Layer 4. At the Transport layer, a slew of important things happens end-to-end delivery, segment order, reliability, and flow-control are all important concepts of Layer 4 functionalities – including a couple of salient issues in the discussion here: TCP flags and port numbering.

**NOTE: Switched networks greatly reduce the number of frames you’’ receive that are not addressed to your system.**

### UDP Connectionless Communication

When two IP-enabled hosts communicate with each other, two methods of data transfer are available at the Transport layer: _connectionless communications_ and _connection-oriented communications._ Recall that there are two types of Internet Protocol (IP) traffic and methods for the establishment of client-host communications: TCP (Transmission Control Protocol) which is a _**connection-oriented protocol**_ and UDP (User Datagram Protocol), _**a connectionless protocol.**_ Connectionless communication is simple to understand: the sender doesn’t care whether the recipient has the bandwidth (at the moment0 to accept the message, nor does the sender really seem to care whether the recipient gets the message at all. Connectionless communication is _“fire and forget.”_ In a much faster way of sending datagrams, the sender a simply fire off as many segments as it wants, relying on the upper layers of the OSI model to handle any subsequent problems. This obviously comes with some disadvantages as well, such as the lack of error correction, reliability and receipt of delivery, retransmissions, and more.

At the Transport layer, connectionless communication is accomplished with UDP. UDP, as you can tell from the datagram structure shown in the figure below, is a low-overhead, simple, and fast transport protocol. The application protocols that use this transport method are moving small amounts of data (sometimes just a single packet or two) and usually are moving them inside a network structure (not across the Internet). Examples of protocols using UDP are _**Trivial File Transfer Protocol (TFTP), Domain Name Service (DNS)**_ (for lookups and name resolution) , and _**Dynamic Host Configuration Protocol (DHCP).**_

![A white rectangular box with black text

Description automatically generated](<../../.gitbook/assets/2 (32).png>)

### TCP Connection-Oriented Communication

TCP is a connection-oriented protocol and establishes connection-oriented communications and although it requires more overhead than its connectionless counterpart, and oftentimes making it slower than connectionless communication, it is a much more orderly, reliable, and secure exchange and makes a lot more sense for transporting large files or for communicating across large network boundaries. Senders will reach out to recipients, before data is ever even sent, to find out whether they’re available and whether they’d be willing to set up a data channel.

Once the data exchange begins, the two hosts continue to talk with one another, making sure flow control is accomplished, so the recipient isn’t overwhelmed and can find a nice way to ask for retransmissions in case something gets lost or dropped along the way. It establishes a connection between two devices before allowing bidirectional communications. This reliable and ordered delivery protocol ensures that data packets arrive in the correct order and without errors. How does all this get accomplished? Using header flags and something known as the TCP three-way handshake.

The following diagram shows a TCP segment header:

![A screenshot of a computer screen

Description automatically generated](<../../.gitbook/assets/3 (24).png>)\
_**FIGURE X:** TCP header._

The flag field in the TCP header is 9 bits long, and it includes several flags that control various aspects of TCP connections. These flags are critical in managing the state of TCP connections, initiating and terminating connections, and ensuring the reliable delivery of data.

The six primary TCP flags are:

1. **URG (Urgent Pointer Field Significant)**
2. **ACK (Acknowledgement Field Significant)**
3. **PSH (Push Function)**
4. **RST (Reset the Connection)**
5. **SYN (Synchronize Sequence Numbers)**
6. **FIN (No More Data From Sender)**

Each of these flags have a specific function within the TCP protocol. Let’s expand on these flags and their properties.

#### URG (Urgent Pointer Field Significant)

* **Purpose:** When this flag is set, it indicates the data inside is being sent out-of-band. Cancelling a message mid-stream is one example.
* **Usage:** When the URG flag is set, the sender indicates that the segment contains urgent data. The receiver should prioritize processing this data immediately. The Urgent Pointer field in the TCP header specifies the position of the urgent data in the segment.
* **Example:** Used in scenarios where some data must be processed immediately, such as interrupt signals.

#### ACK (Acknowledgement Field Significant)

* **Purpose:** Indicates that the Acknowledgement field is significant and should be processed. This flag is set as an acknowledgement to SYN flags. THIs flag is set on all segments after the initial SYN flag.
* **Usage:** The ACK flag is used to acknowledge the receipt of data. When set, it indicates that the Acknowledgement Number field contains a valid acknowledgement of previously received data.
* **Example:** In normal data transfer, the receiver sends segments with the ACK flag set to confirm receipt of data segments.

#### PSH (Push Function)

* **Purpose:** Instructs the receiving TCP stack to push the data to the application layer immediately. This flag essentially forces the delivery of data without concern for any buffering. In other words, the receiving device need not wait for the buffer to fill up before processing the data.
* **Usage:** When the PSH flag is set, it signals the receiver to deliver the data to the application layer without buffering, ensuring timely processing of the data.
* **Example:** Used in interactive applications, such as remote terminal sessions, when data needs to be processed as soon as it arrives.

#### RST (Reset the Connection)

* **Purpose:** Resets the connection.
* **Usage:** The RST flag is used to abruptly terminate a connection in both directions. This can occur if a segment arrives that does not match the current condition state or if a serious error is detected.
* **Example:** If a TCP connection receives a segment it cannot process (e.g., an invalid sequence number), it may respond with a segment that has the RST flag set to reset the connection.

#### SYN (Synchronize Sequence Numbers)

* **Purpose:** This flag is set during the initial communications establishment. It initiates a new TCP connection, synchronizes sequence numbers and indicates negotiation of parameters and sequence numbers.
* **Usage:** The SYN flag is used during the three-way handshake process to establish a TCP connection. The initial sequence number is communicated between the two hosts.
* **Example:** In the first step of the TCP handshake, the client sends a segment with the SYN flag set to initiate a connection.

#### FIN (finish: No More Data From Sender)

* **Purpose:** Indicates that the sender has finished sending data.
* **Usage:** The FIN flag is used to gracefully terminate a connection. When set, it indicates that the sender has no more data to send, and the connection should be closed.
* **Example:** In the TCP connection termination process, the sender sends a segment with the FIN flag set to indicate that it is done sending data.

In addition to these six primary flags, there are three more bits in the flag field that are less commonly discussed:

#### NS (Nonce Sum)

* **Purpose:** Used to protect against accidental corruption of data in TCP streams.
* **Usage:** The NS flag is part of an extension to improve the robustness of TCP against certain types of attacks.

#### CWR (Congestion Window Reduced)

* **Purpose:** Indicates that the sender has received a TCP segment with the ECE flag set and has responded accordingly.
* **Usage:** Used in TCP congestion control mechanisms to signify that the sender has reduced its congestion window as a response to network congestion.

#### ECE (ECN-Echo)

* **Purpose:** Used to signal the network congestion to the sender.
* **Usage:** The ECE flag is part of _**Explicit Congestion Notification (ECN)**_ for TCP/IP networks, indicating that the TCP peer has received a packet with the ECN field set.

To fully understand these flags and their usage, consider what is most often accomplished during a normal TCP data exchange. First, a session must be established between the two communicating client-host systems. To do this, the sender forwards a segment with the SYN flag set, indicating a desire to synchronize a two-way communications session. This segment also contains a sequence number – a pseudorandom number that helps to maintain the legitimacy and uniqueness of this communications session. As an aside, the generation of these numbers isn’t necessarily all that random at all, and plenty of attack examples point that out. Take Kevin Mitnick’s famous TCP Sequence Number Prediction attack, for example.

**NOTE: Know the TCP flags and the TCP three-way handshake well. When conducting targeted attacks, much like a SYN flood, its important to know what flags are set at different points in the process, and what responses a system provides given a particular flag receipt, and what the sequence numbers ‘look like’ during a two-way data exchange, or a two-way handshake.**

When the recipient gets this segment, it responds with the SYN and ACK flags set and acknowledges the sequence number incrementing it by one. Additionally, the return segment contains a sequence number generated by the recipient. All this tells the sender, “Yes, I acknowledge your request to communicate and will agree to synchronization with you. I see your sequence number and acknowledge it by incrementing it. Please use my sequence number in further communications with me so I can keep track of what we’re doing.”

TCP flags and the three-way handshake are important factors for establishing communications channels which support scanning functions. Without TCP, we’d dead in the water-that would be like trying to conduct an assessment scan with limited resources or as they say, _“with your hands tied behind your back.”_

### Benefits of TCP Communications for Ethical Hackers

Understanding this concept of TCP networking is so critical for you to fully grasp for several reasons, including:

#### Network Scanning and Enumeration

* **Port Scanning:** Hackers use tools like Nmap to scan for open ports and services on a target system. Understanding TCP flags helps in crafting different types of scans (e.g., SYN scan, FIN scan, ACK scan) to evade detection and gather information about open and closed ports.
* **Service Enumeration:** By manipulating TCP flags, individuals can infer details about the operating system and services running on a target system, aiding in the enumeration process.

#### Connection Hijacking and Spoofing

* **Session Hijacking:** Knowledge of TCP flags enable the hijacking of existing TCP sessions by injecting malicious packets with the appropriate sequence and acknowledgement numbers, using flags like ACK and RST.
* **IP Spoofing:** Individuals can craft packets with forged IP addresses and manipulate TCP flags to establish or disrupt connections without revealing their identity.

#### Evading Intrusion Detection Systems (IDS)

* **IDS Evasion:** By carefully setting TCP flags, you can craft packets that avoid triggering alarms in intrusion detection systems. Techniques like fragmenting packets and using unusual flag combinations can help in bypassing IDS signatures.

#### Denial of Service (DoS) and Distributed Denial of Service (DDoS) Attacks

* **SYN Flooding:** The SYN flag is used to initiate many half-open TCP connections, overwhelming the target system and causing a denial of service.
* **RST Flooding:** Flooding a target with RST packets can disrupt ongoing connections, leading to service interruptions.

#### TCP/IP Stack Fingerprinting

* **OS Fingerprinting:** Different operating systems and TCP/IP stacks respond differently to various combinations of TCP flags. Tools like Nmap and Xprobe use this behavior to fingerprint the operating system of a target system.
* **Network Fingerprinting:** Understanding how network devices handle TCP flags can help you to map out the network infrastructure and identify potential points of weakness and vulnerability.

#### Exploit Development and Penetration Testing

* **Exploit Development:** When developing exploits, you need to understand how different TCP flags affect network behaviors. This knowledge is essential for crafting payloads that can bypass network defenses and reach the target.
* **Penetration Testing:** Ethical hackers use their understanding of TCP flags to simulate real-world attacks, identify vulnerabilities, and test the strength of network defenses.

#### Traffic Analysis and Monitoring

* **Analyzing Traffic:** By examining the flags set in TCP packets, you can infer the state of a connection, the type of communications taking place, and potential weaknesses in the network protocol stack implementation.
* **Session Reconstruction:** Knowledge of TCP flags help in reconstructing sessions from captured traffic, enabling a deeper understanding of the communications patterns and data exchanges.

#### Vulnerability Discovery

* **Protocol Vulnerabilities:** Understanding TCP flags allows you to discover and exploit protocol-specific vulnerabilities, such as weaknesses in how a system handles certain flag combinations or sequences.
* **Misconfiguration Exploitation:** Misconfigured network devices or improperly implemented TCP/IP stacks may handle TCP flags incorrectly, providing an attack vector for skilled hackers.

For both offensive and defensive security professionals, a deep understanding of TCP flags is essential. It enables you to craft sophisticated attacks and evade defenses, while ethical hackers and network defenders can use this knowledge to better protect systems, identify vulnerabilities, and improve overall network security.

The TCP flag field plays a critical role in the operation of the TCP protocol, enabling reliable, ordered, and error-checked delivery of data. By understanding and appropriately using these flags, you can better manage and secure TCP connections.

### Network Scanning Defined

_**Scanning**_ is one of the most important phases of intelligence gathering for an adversary. In the process of scanning, the adversary tries to gather information about the specific IP addresses that can be accessed over the Internet, the target’s operating systems and system architecture, and the services running on each computer identified.

The purpose of scanning is to discover exploitable communications channels, probe as many listeners as possible, and keep track of the ones that are responsive or useful to an adversary’s particular needs. In the network scanning phase of an attack, the adversary tries to find various ways to intrude into a target system. The adversary also tries to discover more about the target system by finding out what operating systems are used, what services are running, and whether there are any configuration lapses in the target system. The adversary then tries to form an attack strategy based on facts learned during the scan.

After the active and passive reconnaissance and footprinting phases of the hacking lifecycle have been completed, network scanning and enumeration are performed. Network scanning is used to determine whether a system is on the network and available. Scanning tools are then used to gather information about systems, such as IP addresses, operating system, and services running on the target. The different types of network scanning are as follows:

#### Port Scanning

Although there are many different types of port scanners, they all operate in much the same way. There are a few basic types of TCP port scans with the most common type of scan being a SYN scan (or SYN stealth scan), names for the TCP SYN flag, which appears in the TCP connection sequence, or three-way handshake. This type of scan begins by sending a SYN packet to a destination port. The target receives the SYN Packet, responding with a SYN/ACK response if the port is open or an RST if the port is closed. This is typical behavior of most scans; a packet is sent, the return is analyzed, and a determination is made about the state of the system or port. SYN scans are relatively fast and relatively stealthy, because a full three-way handshake is not made, and this, in return, makes the SYN scan not as ‘noisy’ on the networks as others. Because the TCP handshake was not complete, the service on the target does not dee a full connection and will usually not log the transaction.

Other types of port scans that may be used for specific situations, which we will discuss later in the chapter, are ports cans with various TCP flags set, such as FIN, PUSH, and URG. Different systems respond differently to those packets, so there is an element of operating system detection when using these flags, but the primary purpose is to bypass access controls that specifically key in on connections initiated with specific TCP flags set. Later in the chapter, we will be discussing open-source tools including Nmap (Network Mapper), a scanning and enumeration tool. In the table below, you can see a summary of common Nmap options along with its scan types initiated and expected responses. This will help to illustrate some of the TCP flags that can be set and what the expected response is.

### Determine Open Ports and Services

In addition, port scanning is the process of checking the services running on the target computer by sending a sequence of messages to break in. Port scanning involves connecting to TCP and UDP ports on the target system to determine if the services are running or are in a listening state. The listening state gives an idea of the operating system and the applications in use. Sometimes, active services that are listening may allow unauthorized user access to systems that are misconfigured or running software that has vulnerabilities.

Port scanning tools enable a hacker to learn about the services available on a given system. Each service or application on a machine is associated with a _**well-known**_ port number. For example, a port scanning tool that identifies port 80 as open indicates a web server running on that system. Hackers need to be familiar with well-known port numbers. More on this in upcoming subsequent sections below.

**Note: On Windows systems, well-known port numbers are in the C:\Windows\System32\drivers\etc\services file. The Services file is a hidden file by default. To view it, show hidden files in Windows Explorer, double-click the file, and open it with Notepad. A well-rounded ethical hacker will be familiar with the well-known port numbers such as&#x20;**_**FTP (21/22), Telnet (23), HTTP (80), SMTP (25), POP3 (110), HTTPS (443),**_**&#x20;among many more.**

### Determine IP Addresses, MAC Addresses, Hostnames

Network scanning is a procedure for identifying active hosts on a network, either to attack them or as a network security assessment. It is a procedure for identifying active hosts on a network, either to attack them or as a network security assessment. Hosts are identified by their individual IP addresses. Network scanning tools attempt to identify all the _live_ or responding hosts on the network and their corresponding IP addresses.

#### Vulnerability Scanning

**Determine Presence of Known Weaknesses and Exploits**

Vulnerability scanning is a method used to check whether a system is exploitable by identifying its vulnerabilities. A vulnerability scanner consists of a scanning engine and a threat and virus database, or catalog. The catalog consists of a list of common files with known vulnerabilities and common exploits for a range of servers. A vulnerability scanner may look for backup files or directory traversal exploits, for example. They may also identify the operating system and version number, including service packs that may be installed. The scanning engine maintains logic for reading the exploit list, transferring the request to the web server and analyzing the requests to ensure the safety of the server. These tools generally target vulnerabilities that are easily fixed by secure host configurations, updated security patches, and a clean web document. During the later attack phase, a hacker can exploit those weaknesses to gain initial access to the target system.

#### Intrusion Detection System (IDS)

**Determine Malicious Activities and Block**

An intrusion detection system (IDS) or a sophisticated network security professional with the proper tools can detect active port scanning activities. Scanning tools probe TCP/IP ports looking for open ports and IP addresses, and these probes can be recognized by most security intrusion detection tools. Network and vulnerability scanning can usually be detected as well, because the scanner must interact with the target system over the network.

The access points that a thief who wants to break into a house looks for are the doors and windows. These are usually a house’s points of vulnerabilities because they are easily accessible. When it comes to computer systems and networks, you can think of ports as being the doors and windows of the system that an intruder uses to gain access. A general rule for computer systems is the more open ports there are on a system, the more the system is vulnerable to threats and breach attempts. There are cases, however, where a system has fewer ports open compared to another machine , but the ports that are open present a much higher level of vulnerability.

#### TCP Versus UDP Scanning

A TCP connection involves the use of all of the steps involved in the standard TCP three-way handshake which is discussed in further detail below. In a standard three-way handshake, that is the following sequence:

* Source (Host A) sends SYN to target (Host B)
* Target (Host B) responds back to Source (Host A) with a SYN/ACK
* Source (Host A) responds back to the Target (Host B) with an ACK

After the sequence has successfully completed, a communications channel or connection is considered in an established and listening state. As we’ve discussed already, stealth TCP scanning makes use of part of the handshake, but never fully completes the connection. In a stealth scan, the final ACK is never sent back to the target thus the connection is deemed not established and considered or in a closed or downed state.

Scanning UDP is more difficult as it is a connectionless protocol and does not use a handshake like TCP. With UDP, the following sequence is used:

* Source (Host A) sends UDP to Target (Host B)
* Target (Host B) checks to see if the port/protocol is active then takes action accordingly

This makes scanning UDP ports especially challenging. If you receive a response, it will be one of three types:

* ICMP Type 3 message:
  * If the port is closed
  * If the firewall allows the traffic
  * Response from the service itself

Otherwise, no response could mean that the port is open, but it could also mean that the traffic was blocked or simply did not make it to the target and was dropped for some reason, or other.

While it’s typically faster and more productive to perform TCP scans, it can sometimes be worth the time and effort to perform a UDP scan as well. Many administrators tend to focus more on securing TCP-based services and often don’t consider UDP-based services when determining their security policies. With this in mind, you can sometimes find (and exploit) vulnerabilities in UDP-based services, giving you another potential entry point to your target system.

**Table X:** Nmap Options and Scan Types

| Nmap Switch | **Type of Packet Sent**                             | **Response if Open**     | **Response if Closed**            | **Notes**                                                                                                     |
| ----------- | --------------------------------------------------- | ------------------------ | --------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| -sT         | OS-based connect()                                  | Connection made          | Connection refused or timeout     | Basic nonprivileged scan type                                                                                 |
| -sS         | TCP SYN packet                                      | SYN/ACK                  | RST                               | Default scan type with root privileges                                                                        |
| -sN         | Bare TCP packet with no flags (NULL)                | Connection timeout       | RST                               | Designed to bypass nonstateful firewalls                                                                      |
| -sF         | TCP packet with FIN flag                            | Connection timeout       | RST                               | Designed to bypass nonstateful firewalls                                                                      |
| -sX         | TCP packet with FIN, PSH, and URG flags (XMAS tree) | Connection timeout       | RST                               | Designed to bypass nonstateful firewalls                                                                      |
| -sA         | TCP packet with ACK flag                            | RST                      | RST                               | Used for mapping firewall rulesets, not necessarily open ports                                                |
| -sW         | TCP packet with ACK flag                            | RST                      | RST                               | Uses value of TCP window (positive or zero) in header to determine whether filtered port is open or closed    |
| -sM         | TCP FIN/ACK packet                                  | Connection timeout       | RST                               | Works for some BSD systems                                                                                    |
| -sl         | TCP SYN packet                                      | SYN/ACK                  | RST                               | Uses a “zombie” host that will show up as the scan originator                                                 |
| -sO         | IP packet headers                                   | Response in any protocol | ICMP unreachable (Type 3, Code 2) | Used to map out which IPs are used by the host                                                                |
| -b          | OS-based connect()                                  | Connection made          | Connection refused or timeout     | FTP bounce scan used to hide originating scan source                                                          |
| -sU         | Blank User                                          | ICMP                     | ICMP port                         | Used for UDP scanning; can be slow due to timeouts or hangups from open and filtered ports                    |
| -sV         | Subprotocol-specific probe (SMTP, FTP, HTTP, etc.)  | N/A                      | N/A                               | Used to determine services running on open ports; uses service database; can also use banner grab information |
| -O          | Both TCP and UDP packet probes                      | N/A                      | N/A                               | Uses multiple methods to determine target OS/firmware versions                                                |
| -sn         | N/A                                                 | N/A                      | N/A                               | Skips port scan after host discovery                                                                          |

### Objectives of Scanning

The various objectives for which network scanning is carried out are as follows:

* Detect the live systems running on a network.
* Discover which ports are open: based on the open ports, the adversary will determine the best means of entry into the system.
* Discover the operating system of the target system. This is also known as _**“fingerprinting.”**_ The adversary will formulate a strategy based on the operating system’s vulnerabilities.
* Discover the services and versions running/listening on the target system: this gives the adversary an indication of any vulnerabilities (based on the service) that can be exploited to gain access to the target system.
* Discover the IP address of the target system.
* Identify specific applications or versions of a particular service.
* Identify vulnerabilities in any of the systems in the network: this can be useful in taking counteractive measures to secure the systems from being probed by adversaries.

### NETWORK Scanning Methodology

As an ethical hacker, you’re expected to be familiar with the network scanning methodology presented in the figure below. This methodology is the process by which a hacker scans the network. It ensures that no systems or vulnerabilities are overlooked and aids the hacker in efficiently gathering all necessary information to perform an attack. A hacker follows a particular sequence of steps to properly scan a network.

Just as the steps of the overall hacking process can blend into one another, keep in mind that these steps are simply guidelines and not hard-and-fast rules to follow. When you’re on the job, situations and circumstances will occur that might force you to change the order of things. Sometimes the process of completing one phase will seamlessly blend directly into one another. Don’t fret – just go with the flow and get your job done.

We’ll look at the various stages of this scanning methodology throughout this book, starting with the first three steps – checking for systems that are live and for open ports and service identification. A generic approach has been presented, so the scanning methods may differ based on your specific objectives. The steps involved in network scanning are as follows:

1\. _**Check for live systems:**_ Something as simple as a ping can provide this. This gives you a list of what’s actually alive on your target network subnet. Your objective should start off with checking for live systems on the network.

2\. _**Check for open ports:**_ After the live systems are found, look for open ports to determine which services are running on the systems. This can be a vital step, because some services may be of a much higher priority from the adversary’s point of view. Once you know which IP addresses are indeed active, find out what ports they’re listening on.

**3.&#x20;**_**Scan beyond IDS:**_ Sometimes your scanning efforts need to be altered to avoid those pesky intrusion detection systems.

4\. _**Fingerprint the operating system:**_ The next phase involves fingerprinting the operating system by figuring out the target’s network layout.

**5.&#x20;**_**Perform banner grabbing:**_ Banner grabbing and OS fingerprinting will tell you what operating system is on the machines and which services they are running.

6\. _**Scan for vulnerabilities:**_ Identification of the vulnerabilities in the target’s OS is the next step. Perform a more focused look at the vulnerabilities these machines haven’t been patched for yet and try to exploit these vulnerabilities post-attack.

7\. _**Probe the network:**_ The malicious actor may also choose to actively probe the network or slightly monitor its traffic. This can be accomplished using proxies (which will be discussed later in the chapter). The technique of anonymous surfing makes it hard to trace this activity back to the malicious actor.

**8.&#x20;**_**Draw network diagrams:**_ A well-drawn out network diagram will display all the logical and physical pathways to targets you might be interested in.

**9.&#x20;**_**Prepare proxies:**_ This will obscure your efforts to keep you hidden to better evade detection mechanisms.

This methodology has about as much to do with real-life as I have to do with winning an Oscar nomination, but it’s a repetitive and memorization effort you must do. Despite which order you proceed in, if you try and hit most of the steps, you’re probably going to be successful in your network scanning efforts. We’ll dive deeper into each step later in this chapter, but first we need to revisit some networking knowledge essential for successful network scanning.

**NOTE: Commit these network scanning steps to memory and pay close attention to what actions are performed in each – especially which tools might be used to perform those actions.**

### Identifying Targets

\
The first step you want to take when commencing your network scanning strategy is to check for live systems. The simplest and easiest way to do this is to take advantage of a protocol that’s buried in the stack of every TCP/IP-enabled device on the planet – _**Internet Control Message Protocol (ICMP).**_ As I’m sure you’re already aware, IP is what’s known as a connectionless, “fire-and-forget” protocol. It creates a packet by taking data and appending a header, which holds a ton of information, including the “From” and “To” addresses, and allows the sender to fire packets away without regard, as quickly as the stack on the machine will allow. This is done by relying on other layered protocols for transport, error correction, flow-control, and so on.

However, some shortfalls need to be addressed at Layer 3, the Network layer. IP itself has no error messaging function, so ICMP was created to provide for it. It allows for error messaging at the Network layer and presents the information to the sender in one of several ICMP types. The table below lists some of the more relevant message type codes that will be helpful for you to know. The most common of these types are Type 9 (ECHO Request) and Type 0 (ECHO Reply). An ICMP Type 8 packet received by a host tells the recipient, _“Hey, I’m sending you a few packets. When you get them, reply with the same number so I know you’re there.”_ The recipient will respond with an ICMP Type 0, stating, _“Sure, I’m alive. Here are the data packets you just sent me as proof!”_

| ICMP Message Type          | Description and Important Codes                                                                                                                                                                                                                                                                                                                          |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0: Echo Reply              | Answer to a Type 8 Echo Request                                                                                                                                                                                                                                                                                                                          |
| 3: Destination Unreachable | <p>Error messages indicating the host or network cannot be reached. The codes follow:</p><p><strong>0:</strong> Destination network unreachable</p><p><strong>1:</strong> Destination host unreachable</p><p>6: Network unknown</p><p>7: Host unknown</p><p>10: Host administratively prohibited</p><p>13: Communication administratively prohibited</p> |
| 4: Source Quench           | A congestion control message                                                                                                                                                                                                                                                                                                                             |
| 5: Redirect                | <p>Sent when there are two or more gateways available for the sender to use and the best route available to the destination is not the configured default gateway. The codes follow:</p><p><strong>0:</strong> Redirect datagram for the network</p><p><strong>1:</strong> Redirect datagram for the host</p>                                            |
| 8: Echo Request            | A ping message, requesting an ECHO REPLY                                                                                                                                                                                                                                                                                                                 |
| 11: Time Exceeded          | The packet took too long to be routed to the destination (_code 0 is TTL **(Time-to-Live)** expired_)).                                                                                                                                                                                                                                                  |

**TABLE X:** Relevant ICMP Message Types

Because ICMP is built into each TCP/IP device and the associated responses provide detailed information about the recipient host, it makes a good place to start when network scanning. For example, consider an ECHO REQUEST (Type 8) sent to a host that returns a Type 3. The code could tell us whether the host is down (Code 1), the network route is missing or corrupt in our local route tables (Type 0), or a filtering device, such as a firewall, is preventing ICMP messages altogether (Type 13).

**NOTE: The actual payload of a PING packet can range greatly in value amount. The Request for Comment (RFC 792,** [_**https://tools.ietf.org/html/rfc792**_](https://tools.ietf.org/html/rfc792)**) that created and still governs ping never got around to identifying what data is supposed to go into the payload, so it’s usually just enough ASCII code to build the packet up to sufficient length. Knowing this, the payload of an ICMP packet could wind up being the perfect covert channel for you to communicate with each other, using the payload area to simply embed messages. Most people – even security types – wouldn’t even bother when a ping packet or two crossing their paths, never knowing what information was being funneled away right under their noses.**

Some Intrusion Detection Systems (IDS) signatures _do_ look for this, however. For example, a lot of ping utilities designed to take advantage of this have default signatures that any decent IDS can pick up; in Nmap, a “0 byte field” can trigger it, for example. Windows and other operating systems have specific defaults that are supposed to be found in the packet, and their alteration or omission can also trigger a hit. But none of this changes the fact that it’s still a cool hack.

This process, called

Some processes include:

### Step 1: Check for Live Systems

#### Ping Sweep

The network scanning methodology starts with first checking for systems that are live and listening on the network at the time you plan to scan. A machine that is termed as being _live_ on a network means that there are actively listening devices (e.g., turned on) in either a wired or wireless network. The simplest, although not necessarily the fastest, or most accurate, way to determine whether systems are live on a network is to perform a _**“ping sweep”**_ of the IP address range.

A ping sweep (also known as an _**ICMP sweep**_, and a _**“two-way handshake protocol”**_ ) is a basic network scanning technique to determine which range of IP addresses map to live hosts (computers). Ping sweeps are conducted using tools such as the one show in the image below. While a single ping will tell the user whether one specified host computer exists on the network, a ping sweep consists of ICMP ECHO request sent to multiple hosts. If a given IP address is live, it will return an ICMP ECHO reply. Ping sweeps are among the oldest and slowest methods to scan a network. This utility, distributed across almost all platforms, acts like a roll call for systems; a system that is active on the network answers to the ping query that another system sends out.

The phrase “two-way handshake protocol” reflects the way data packets are sent and received: one host sends data, the other validates it and replies with whether the ping was successful.

Internet Control Message Protocol (ICMP) scanning is the process of sending an ICMP request or _**“ping”**_ to all hosts on the network to determine which ones are up and responding to pings. A benefit of ICMP scanning is that it can run quickly on an entire network. Most hacking tools include a ping-sweep option, which essentially means performing an ICMP request to every host on the network.

Ping has been part of networking since its inception, and combining pings to every address within a ra

“Ping” was first coined as a technical term by the sonar technology industry, when it was associated with the detection capabilities of submarines. A submarine with active sonar projects a sound, or a ping, which bounces back if it encounters an obstacle, like another submarine. This is the technical origin of ping, which is now more commonly linked with IP network utilities, and we can use them as a reconnaissance tool in what we call ping sweeps, as described above.

* Ping is available on any device connected to a network. It’s a command-line utility, a standard component of a network administrator’s capabilities.
* Ping sweep is the more popular name for an Internet Control Message Protocol (ICMP) sweep, a simple way of diagnosing potential network issues and identifying IP addresses used by “live” or “dead” hosts. These hosts are typically computers, but anything can be a host, including printers, computer systems, websites, networks, smart refrigerators, coffee makers, personal home security systems, tablets. Any device that can connect to the internet, and has an IP address, is a host, and is hackable.
* Discover which IP addresses are active or live on the network.
* Detect rogue devices and unauthorized networks.
* Ensure the IP addresses on the network match network documentation and schematics. This ensures robustness in your disaster recovery and COOP, BIA, or BCP procedures.

Although ping sweeps are deemed older than dirt, they are still very relevant and are still very well-used in the hacking field today. If you’ve used it long enough, it’s basically your first go-to tool (even before using Nmap) when needing to scan and map the lay of the land (e.g., the network topology, identify inactive IP addresses, and determining which IP addresses map to live hosts in a DHCP environment).

Ping sweeps are more complex than single pings in that they require more advanced software packages that feature enhancements and capabilities. Some ping sweep software may also have the capacity to reveal other useful information about the hosts, besides their live or dead status. For example, they may be able to tell you whether there was any packet loss during a ping, as well as how long the signal took to return. This information can assist users in diagnosing network vulnerabilities and faults.

FYI – FOR YOUR INFORMATION

Infiltrator, Pinger, Friendly Pinger, and WS Ping Pro are all tools that perform ICMP queries. You should be familiar with how to use these tools.

### Ping and ICMP Sweepers

| **Product/Vendor**            |                                                                                                                     | **Free Trial?**  | **Top Features**                                |                                        |                                           | **Bottom Line**                                                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------- | ----------------------------------------------- | -------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| SolarWinds IP Address Manager | <img src="../../.gitbook/assets/4 (28).png" alt="Vendor Spotlight: SolarWinds - GovSmart" data-size="original">     | 30-Day           | Generous free trial                             | Built-in IP address scanning           | Automated IP address tracking             | Fantastic for continuous and sophisticated network coverage and impressive integration with other monitoring capabilities |
| SolarWinds Engineer’s Toolset | <img src="../../.gitbook/assets/5 (24).png" alt="Vendor Spotlight: SolarWinds - GovSmart" data-size="original">     | 14-Day           | Simple user interface                           | Support for various file format export | 60+ network management tools              | A versatile range of tools covering all aspects of network monitoring                                                     |
| Zenmap                        | <img src="../../.gitbook/assets/6 (1).jpeg" alt="Zenmap: A GUI Frontend For Nmap Network ..." data-size="original"> | 100% Free        | Searchable database of scans                    | Open-source                            | Topology mapper                           | A great place for beginners to start, with an intuitive interface                                                         |
| Paessler PRTG                 | <img src="../../.gitbook/assets/7 (25).png" alt="Paessler PRTG - Wikipedia" data-size="original">                   | 30-Day           | Full network visibility                         | Customizable system                    | Cloud-based services available            | A customizable system with priced plans based on chosen sensors, rather than device number                                |
| IPHost Network Monitor        | <img src="../../.gitbook/assets/8 (3).jpeg" alt="IPHost Network Monitor for Windows ..." data-size="original">      | 50 Monitors Free | Bypasses machines turned off (no hanging scans) | Quick installation                     | 44+ monitoring types                      | Quick, basic, easy, and low-cost tool with great tech support                                                             |
| Advanced IP Scanner           | <img src="../../.gitbook/assets/9 (2).jpeg" alt="Advanced IP Scanner" data-size="original">                         | 100% Free        | Remote control sessions                         | MAC address detection                  | Shared folder access                      | A free tool specifically designed and attuned to Windows server                                                           |
| Fping                         |                                                                                                                     | 100% Free        | Support for IPv6 networks                       | Link output to DNS                     | Report in various outputs (xml, txt, csv) | A free tool for Linux with multiple ways of entering IP address ranges                                                    |
| Angry IP Scanner              | <img src="../../.gitbook/assets/10 (17).png" alt="fping | Kali Linux Tools" data-size="original">                   | 100% Free        | Multithreading for speed                        | NetBIOS information                    | No installation                           | A free, zero-installation tool known for its ping sweep and port scanning speed                                           |
| Ping Plotter Pro              | <img src="../../.gitbook/assets/11 (3).jpeg" alt="PingPlotter 4.00.3 - Neowin" data-size="original">                | 14-Day           | Visuals and graphs                              | Multitarget monitoring                 | Perpetually monitor network               | An impressive tool with a free, standard, and professional version available                                              |
| OpManager                     |                                                                                                                     | 30-Day           | Multiple parameters for scanning                | Periodic ping requests                 | Round Trip Time (RTT) reporting           | A simple and basic ping tool, though the overall network management and monitoring package is versatile.                  |

**NOTE: Pinging out of the network ID itself (that is, sending ICMP ECHO REQUEST packets to the network IP address) as&#x20;**_**“ICMP Echo scanning.**_

Another option for identifying machines (not necessarily live ones, but ones that were live at some time) is called a _**“list scan” –**_ basically it just runs a reverse DNS lookup on all Ips in the subnet.

Additionally, not only will a great many devices not respond to the ping, but the actual ping also sweep itself can be noisy, and the systems may alert concerned personnel as to what’s going on. Network Intrusion Detection Systems (NIDS) and host-based IDS (HIDS) can easily and readily pick up on a ping sweep from an external source if not carried out slowly and with some stealth. Be cautious and deliberate with your sweep – roll slow and low are your friends here.

**NOTE: Know ICMP well. Pay particular attention to Type 3 messages and the associated codes, especially Code 13, which lets you know a poorly configured firewall is preventing the delivery of ICMP packets.**

Several applications are available to make the ping sweep as simple as possible for you to pull off. Nmap is, of course, probably the most referenced scanning tool on the exam and in the real world. Angry IP Scanner is another well-known tool; just be careful with it because a lot of antivirus programs consider it a virus. Some other tools of note are SolarWinds Engineer Toolset, Network Ping, OPUtils, SuperScan, Advanced IP Scanner, and a wacky little tool called Pinkie.

**NOTE: When using ping to identify “live” hosts, keep in mind a nonresponse to ICMP does not necessarily mean the host isn’t alive—it simply means it won’t respond to ICMP.**

### How Ping Works

ECHO Request and ECHO Response are the two fundamental aspects of how ping functions. Essentially, an ECHO request is the packet of data sent to either a specific IP address or a range of IP addresses. The ECHO response then replies, and the nature of the reply can reveal important information about the IP address range the ping was sent to.

When the ECHO request is sent, the input value can either be a host, a domain name, or an IP address. The input determines the route taken by the ECHO request, with the potential to expose any delays or issues with the route, so steps can be taken to fix them. If you input a hostname for a device on a network, for instance, the ping route will be directed to the local DNS server so it can acquire the relevant IP address. A domain name input, on the other hand, will first access the domain’s web server. An IP address input will result in a direct _**Round-Trip Time (RTT)**_ result. Each of these inputs can potentially produce different information, which could inform diagnostics and general IP address management strategies.

A user might identify an issue flagged by an ECHO response via the time output field. During a ping sweep in which all network devices are tested, healthy devices should respond within a narrow time frame. When a device doesn’t comply with the request, this could be indicative of an issue needing to be addressed. It could, for example, mean the device is damaged or overloaded.

Put simply, an ECHO request is the ping, while the ECHO response is the ping reply. Echoes are mostly used for troubleshooting. They can reveal whether TCP/IP stacks are configured correctly and if there are any issues with the routes packets are taking. These functionalities are crucial to successful IP address management because, when used in the right way, they can be responsible for diagnosing and eradicating network faults.

To understand ping better, one should be able to understand the basic construct of the TCP/IP packet. When a system does a ping, a single packet is sent across the network to a specific IP address. This packet contains 64 bytes (56 data bytes and 8 bytes of protocol header information). The sender then waits or listens for a return packet from the target system. If the connections are good and the target computer is “alive,” a good return packet can be expected; however, if there is a disruption in the communications, this will not be the case. Ping also details the number of hops the lie between the two computers and the amount of time it takes for a packet to make the complete trip. Remember, this is called the round-trip time. Ping can also be used for resolving host names. In this case, if the packet bounces back when sent to the

IP address, but not when sent to the name, then it is an indication that the system is unable to resolve the name to the specific IP address.

A packet, in the case of ping sweeps, is a formatted unit of data designed to test the route to an IP address. A single pink is conducted via an ICMP ECHO request, which entails sending

### Detecting Ping Sweeps

Almost any IDS or Intrusion Prevention System (IPS) will detect and alert the security administrator to a ping sweep occurring on the network. Most firewall and proxy servers block ping responses so a hacker can’t accurately determine whether systems are available using a ping sweep alone. More intense port scanning must be used if systems don’t respond in a fashionable and timely manner. Just because a ping sweep doesn’t return any active hosts on the network, doesn’t mean they aren’t available – you need to try an alternate method of identification, or scan more than once, sometimes twice – even thrice.

![](<../../.gitbook/assets/12 (20).png>)

_Remember, hacking takes time, patience, and persistence._

![](<../../.gitbook/assets/13 (16).png>)

#### ICMP Scanning

All required information about a system can be gathered by sending ICMP packets to it, a process known as _**“ICMP Scanning.”**_ Since ICMP does not have port abstraction, this cannot be considered a case of port scanning; however, it is useful to determine what hosts in a network are up by pinging them all. The user can also increase the number of pings in parallel with the -L option. It can also be helpful to tweak the ping timeout value with the -T option. The UNIX tool ICMPquery or ICMPush can be used to request the time on the system (to find out which time zone the system is in) by sending an ICMP type 13 message (TIMESTAMP). The netmask on a particular system can also be determined with ICMP type 17 messages (ADDRESS MARK REQUEST). After finding the netmask of a network card, a user can determine all the subnets in use. After getting knowledge about the subnets, the user can target only one subnet and avoid hitting the broadcast addresses. ICMPquery has both a timestamp and address mask request option.

One considerable problem with this method is that personal firewall software- and network-based firewalls can block a system from responding to ping sweeps. Another problem is that the computer must be turned on to be scanned.

![A screenshot of a computer program

Description automatically generated](../../.gitbook/assets/14.gif)

\
_**FIGURE X:** The Infiltrator ping sweep tool._

### Step 2: Check for Open Ports

#### Three-Way Handshake

TCP is a **connection-oriented** protocol, which means that connection establishment is performed prior to data transfer between applications. This connection is possible through the process of the three-way handshake. The _**three-way handshake**_, illustrated below, is implemented to establish connection between hosts. The three-way handshake process goes as follows:

1. The source (Computer A) sends a SYN packet to the destination (Computer B) to establish a TCP connection.
2. The destination, upon receiving the SYN packet sent by the source, starts the TCP session by sending a SYN/ACK packet back to the source.
3. This SYN/ACK packet acknowledges the arrival of the first SYN packet to the source.
4. In conclusion, the source sends an ACK packet back thereby providing acknowledgement for the SYN/ACK packet sent by the destination node.

This allows communication between the source and the destination until either of them issues a FIN packet or an RST packet to close the connection.

![TCP 3 Way Handshake In Detail - DEV Community](<../../.gitbook/assets/15 (16).png>)\
_**FIGURE X:** A typical TCP three-way handshake netflow._

When this segment is received by the original sender, it generates one more segment to finish off the synchronization. In this segment, the ACK flag is set, and the recipient’s own sequence number is acknowledged. At the end of this TCP three-way handshake, a communications channel is opened, sequence numbers are established on both ends, and data transfer can begin.

**NOTE: Some packet-crafting tools available to you include Netscan&#x20;**_**(www.netscantools.com)**_**, Ostinato&#x20;**_**(ostinato.org)**_**, WAN Killer&#x20;**_**(solarwinds.com)**_**, Packeth&#x20;**_**( packet.sourceforge.net)**_**, and LAN Forge FIRE&#x20;**_**(www.candelatech.com).**_

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

**URG:** Urgent alias: Instructs that data contained in packets be processed ASA&#x50;_._

**FIN**_:_ Finish alias: Communicates to the remote client host to close the connection.

**RST:** Reset alias: Resets a connection.

SYN scanning mainly deals with three of the flags, namely, **SYN, ACK,** and **RST.**

Knowing the TCP flags and the communications setup process, I think it’s obvious how a hacker (with a tool capable of crafting segments and manipulating flags) could manipulate, disrupt, manufacture, and even hijack communications between two client-host systems. Want to see for yourself? Jump on the Internet and download and install Colasoft’s Packet Builder _(**Source:**_ [_www.colasoft.com/download/products/download\_packet\_builder.php_](http://www.colasoft.com/download/products/download_packet_builder.php)_),_ as shown in the figure below.

Open it, click the Add button in the menu line, and pick a TCP packet. You can then maneuver up and down the segment to modify the TCP flags and create all sorts of mischief.

![Download Colasoft Packet Builder](<../../.gitbook/assets/16 (17).png>)

**NOTE: Two tips in one for you here! First, Colasoft’s Packet Builder has three views built in: Packet List (displays all constructed packets), Decode Editor (allows you to edit packets), and Hex Editor (displays packets in hex for editing). Second, know that packet builders like Colasoft’s can also be used to create fragmented packets to bypass IDS (and possibly firewalls) in your target network.**

We’ve spent some good time discussing the flags within a segment (keep repeating “SYN, SYN/ACK, ACK” in your head), but there are at least a couple of other fields of great importance while we’re on the subject. The source and destination fields in TCP or UDP communications define the protocols that will be used to process the data. Better stated, they actually define a channel on which to work, and that channel has been generally agreed upon by default to support a specific protocol, but you get the point.

### Scanning Methods

#### SYN Stealth/Half-Open Scan

Since a TCP connect() scan can be detected by an IDS (Intrusion Detection System), hackers started evading the detection by using a technique known as _**“half-open scanning,”**_ as shown in the figure below. It is called this because the adversary does not open a full TCP connection. The adversary sends a SYN packet, impersonating a real connection, and waits for a response. A SYN/ACK indicates the port is in a listening state. An RST is indicative of a nonlistening port. If a SYN/ACK is received, the adversary immediately sends an RST to tear down the connection (actually, the kernel does this for the adversary). The main advantage of this scanning technique is that fewer sites will log it.

However, the adversary needs root privileges to build this custom TCP packet sequence. Sophisticated IDS and firewalling systems are now capable of detecting a SYN packet from the void and prevent such scans from occurring. This is because, like a TCP connect() system call, the half-open scan initiates with a SYN flag, which can easily be monitored by setting up a custom filter in either the IDS or firewall.

On the other hand, a disadvantage is that the adversary must make a custom IP packet to initiate the scan. Building a custom IP packet requires access to SOCK\_RAW (getportbyname (“raw”); under most systems) or /dev/bpf (Berkeley packet filter), /dev/nit (Sun “Network Interface Tap”). This generally requires privileged user access.

Even SYN scanning is not stealthy enough to evade most security detection mechanisms today. Some firewalls and packet filters actively watch and sniff the ingress/egress network traffic for SYNs to restricted ports, and programs such as **Synlogger** and **Courtney** are available to detect these scans. Conversely, some advanced scans may be able to pass through undetected. The term _**stealth,**_ in the context of networking basics, refers to a category of scans where the packets, appearing as normal innocuous traffic, is flagged with a particular set of flags other than SYN, or a combination of flags, no flags set, or all flags set; fragmented packets are used; or filtering devices are avoided by other means. All these techniques resort to inverse mapping to determine open ports.

### SYN/ACK Scan

The TCP three-way handshake methodology is implemented by the SYN/ACK stealth scan. This technique. The difference is that in the last stage, remote ports are identified by examining the packets entering the interface and terminating the connection before a new initialization is triggered.

A stealth scan is done by performing the following steps:

1. To start initialization, the client forwards a single SYN packet to the destination server on the corresponding port.
2. The server then initiates the stealth scanning process, depending on the response sent back.
3. If the server forwards a SYN/ACK response packet, then the port is supposed to be in an open, listening state.
4. The client then responds with an RST packet, closing the connection before it is fully opened.

Below is a Python script using the scapy library to perform a SYN/ACK stealth scan. Step-by-step instructions are included explaining what each part of the code does.

1. **Install Scapy:** You need to have scapy installed. You can do it using pip:

![A black rectangle with white text

Description automatically generated](<../../.gitbook/assets/17 (15).png>)

1. **Construct Code:** After scapy has installed, using SUDO, compile the script and execute to run:

![A screen shot of a computer program

Description automatically generated](<../../.gitbook/assets/18 (15).png>)

### XMAS Scan/FIN Scan

An XMAS scan (also known as a _**FIN Scan)**_ is a type of port scan used in network security to identify listening TCP ports on a target system. The name ‘XMAS’ comes from the fact that the scan sets all the flags in the TCP header (FIN, URG, and PSH), making the packet look “lit up” like a Christmas tree when viewed in a sniffer. Most sniffers will assign TCP packet headers different colors to differentiate between them hence the name XMAS scan. This technique can help evade _some_ firewall rules and detection mechanisms.

* **ACK Flag Probe:** A

### How an XMAS Scan Works

1. **Send a packet with all flags set:** The scanner sends a TCP packet with the FIN, URG, and PSH flags set to the target port.
2. **Interpret the Response:**
   *
     * **No Response:** If the target does not respond, the port is considered **open** or **filtered.**
     * **RST/ACK Response:** If the target responds with an RST/ACK packet, the port is assumed closed.
3. **Effectiveness:** The XMAS scan can be effective against certain operating systems and firewall configurations; however, it might not work on all systems, especially those that comply strictly with the TCP/IP standards (like Windows); therefore, it is mainly directed at UNIX-related systems.

**NOTE: ACK flag probes can also be used to check filtering at the remote end. If an ACK is sent and there is no response, this indicates a stateful firewall is between you and the host. If an RST comes back, there is not.**

#### Prerequisites

1. **Install scapy:** You need to have scapy installed. You can install it using pip:

![A black rectangle with white text

Description automatically generated](<../../.gitbook/assets/19 (13).png>)

### Performing an XMAS Scan

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/20 (9).png>)

1. **Create an XMAS Packet:** In the output above, this step constructs an IP packet with a TCP segment. The dst parameter is the target IP address, and the dport parameter is the target port number. The flags=FPU sets the TCP flags to FIN, URG, and PSH.
2. **Send the XMAS Packet and Receive a Response:** The sr1 function sends the XMAS packet and waits for a single response. The timeout=2 parameter specifies the wait time in seconds for a response. The verbose=0 parameter suppresses detailed output.
3. **Check if We Received a Response:** This step verifies whether the target responded to the XMAS packet.
4. **Check if the Response is an RST:** If the response has a TCP layer and the TCP flags are 0x14 (RST), it indicates that the port is closed.
5. **Handle Unexpected Responses:** If the response is neither expected nor easily interpretable, it prints an unexpected response message.
6. **Handle No Response:** If there is no response from the target, it prints that the port is opened or filtered.

### Usage

Replace target\_ip and target\_port with the desired target IP address and port number you want to scan:

The script above provides a simple yet effective way to perform an XMAS scan to determine the status of a port on a target machine.

### Why Perform an XMAS Scan When You Can Use Nmap?

#### Nmap, Nessus, and Other Scanning Tools

Nmap (Network Mapper) is a versatile and widely-used tool for network discovery and security auditing. It can perform a variety of scans, including SYN, XMAS, ACK, FIN, UDP, and more. Nmap can also detect operating systems, service versions, and perform advanced discovery through its scripting engine, known as NSE, for the Nmap Scripting Engine.

One of the key strengths of Nmap is its great flexibility and generous capabilities making it suitable for both quick scans and in-depth scans, providing you a better avenue for thorough network analysis and a look into what is going on behind the scenes as far as traversing ingress/egress traffic is concerned. Network administrators and security professionals often use Nmap for legitimate security assessments, troubleshooting, and network inventory and asset discovery (I do). Its ability to perform different types of scans, including stealthy ones like an XMAS scan, makes it an awesome tool for understanding the state of your networked systems in real-time.

#### Nessus

Nessus is a vulnerability scanner primarily used to detect vulnerabilities in systems by comparing scan results against its database of known vulnerabilities which is inputted via threat intelligence gathering plugins. It performs detailed scans and can provide extremely comprehensive reports on security issues, misconfigurations, and compliance checks of all sorts. Nessus automates the scanning process, making it an efficient tool for regular security assessments and weekly patch vulnerability scans. Its detailed vulnerability reports and compliance checks are most valuable for presenting to your client a detailed look into the attack surface of their organization. While Nessus _can_ detect open ports, as can an XMAS scan, its focus is simply identifying and reporting vulnerabilities rather than just performing network reconnaissance.

#### XMAS Scan and Stealthy Techniques

An XMAS scan, as stated previously, is a stealthy scanning technique where a TCP packet is sent with the FIN, URG, and PSH flags set. This “lights up” the packets like a Christmas tree, hence the name. The primary goal of an XMAS scan is to detect the status of ports while evading detection mechanisms like firewalls and intrusion detection systems (IDS). If a port is closed, the target typically sends an RST packet response. If the port is open or filtered, there is no response. The stealthiness of the XMAS scan lies in its ability to bypass certain security controls that might flag or block more straightforward scanning techniques. This makes it useful in situations where avoiding detection is critical, such as when performing a black-box assessment.

#### Comparison and Use Cases

While tools like Nmap can perform an XMAS scan, among others, the key difference lies in the intent and context of use. Nmap, Nessus, and similar tools are typically used for legitimate security assessments and troubleshooting within a network. They offer security-rich features and generate detailed reports, making them suitable for regular use. On the other hand, specialized or stealthy techniques like the XMAS scan are often employed when there is a need to evade detection, such as in penetration testing scenarios or by adversaries trying to avoid getting caught.

The choice between using an XMAS Scan/FIN Scan and Nmap (or other scanning-related tools) depends really on the specific requirements of the task you face. Think about it as having to choose between a red apple and a green apple: Both methods have their unique advantages and are suited for different scenarios; however, both have their own set of scaling drawbacks as well. To aid you in decision-making, it is best that you first understand the nuances between the two ultimately helping you to decide which tool or technique best suits your needs, goals, or objectives.

#### XMAS Scan

| **Purpose**                                                                                                                                                                                                                 | **Use Cases**                                                                                                                                                                                                  | **Limitations**                                                                                                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \*An XMAS scan is a type of stealthy port scan that sends only the FIN packet without any other flags set. This makes it difficult for IDS to detect because it does not follow the normal TCP three-way handshake process. | Particularly useful in environments where IDS are heavily deployed and might block or flag standard scans like SYN scans. The goal is to remain undetected while still gathering information about open ports. | While effective in bypassing some IDS, XMAS scans may not be reliable as other types of scans due to variations in how different operating systems handle FIN packets. Some systems might drop the packet entirely, making it seem like the port is closed even if it’s open. |

\*

### Clearing Up Assumed Confusion

_…but you previously stated that XMAS scan lights up all flags hence its name?_

To clarify an XMAS scan, named after the “X” pattern formed by the flags in the TCP header when viewed in binary, sets **all flags** **except the FIN flag.** The means that the SYN, ACK, URG, PSH, and ECE flags are set, but the FIN flag remains unset. This behavior distinguishes the XMAS scan from other types of scans and gives it its characteristic name.

In a typical TCP connection setup, the SYN flag is sent first to initiate a connection, followed by the SYN/ACK response from the server, and finally, the client sends the ACK flag to complete the TCP three-way handshake. In contrast, an XMAS scan sends a packet with _all flags set except the FIN flag._ This packet looks like a malformed TCP segment because it doesn’t adhere to the usual sequence of flag settings during the connection establishment phase.

Because the XMAS scan packet deviates from the standard TCP communication patterns, intrusion detection systems (IDS) and firewalls that rely on recognizing these patterns might not immediately recognize it as a legitimate TCP packet. This can make the XMAS scan more difficult to detect, as it doesn’t trigger the usual responses associated with a legitimate connection attempt.

The main advantage of an XMAS scan is its ability to bypass certain types of intrusion detection mechanisms that are looking for anomalies in the TCP flag settings; however, it’s worth noting that not all systems will respond to an XMAS scan in the same way, and some might simply ignore the packet altogether or send an error message instead of revealing whether a port is open or closed.

| **Purpose**                                                                                                                                                                                                            | **Use Cases**                                                                                                                                                                                                                                         | **Advantages**                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Supports various scanning techniques, including XMAS scans among others like SYN, ACK, UDP, and more.</p><p>Provides a wide range of options for customizing scans according to the environment and objectives.</p> | <p>Nmap is widely used for network discovery and security auditing</p><p>Extensive feature set allows detailed information grabbing about hosts, networks and services</p><p>Suitable for both penetration testing and network asset inventories.</p> | <p>Offers scripting capabilities for post-scanning tasks like vulnerability assessment, service version detection, and more</p><p>Boasts strong community support and regular updates are published</p> |

### IDLE scan

This scan uses a spoofed IP address (an idle zombie system) to elicit port responses during a scan. Designed for stealth, this scan uses a SYN flag and monitors responses as with a SYN scan.

All these scans should be easy enough to decipher given a cursory understanding of TCP flags and what each one is for, apart from the IDLE scan. Sure, the IDLE scan makes use of TCP flags (the SYN and ACK flags, in this case), but the way it’s all used is brilliant (hell, it’s almost elegant) and provides the additional benefit of obfuscation. Because the machine receiving the response from the targets is not your own, the source of the scan is obscured. Confused? No worries – keep reading.

Every IP packet uses something called an _**“IP Identifier (IPID)**_ to help with the problem of keep track of fragmentation (IP packets can be only so big, so a single packet is sometimes fragmented and needs to be put back together at its destination). Most systems simply increase this IPID by one when they send a packet out. For example, the first packet of the day might have an IPID of 31487, and the second 31488. If you understand this concept, can spoof an IP address, and have a remote machine that’s not doing anything, this all makes perfect sense.

First, an attacker sets up or makes use of a machine that isn’t doing anything at all (sitting IDLE). Next, a packet is sent (SYN/ACK) to this IDLE machine and makes note of the IPID in response; the zombie machine isn’t expecting a SYN/Ack and will respond with an RST packet basically stating, _“Can we start over?” I don’t really recognize this communication_

### Port Numbering

Why do we even need port numbers in networking? Well, consider a communications process in its infantile stages. The recipient has verified the frame and packet that belongs to it and knows it has a segment available for processing. But how does it know which Application layer entity is supposed to process it? Maybe it’s an FTP datagram. Or maybe a Telnet request. Or maybe even an email. Without _something_ to identify which upper-layer protocol to hand this information to, the system sits there like a government mid-level manager, paralyzed by indecision.

**NOTE: Internet Assigned Numbers Authority (IANA) maintains something called the Service Name and Transport Protocol Port Number Registry, which is the official list for all port number reservations.**

A port number, inside the Transport layer protocol header (TCP or UDP), identifies which upper-layer protocol should receive the information contained within. Systems use port numbers to identify to recipients what they’re trying to accomplish – that is, assuming the default ports are still being used for their default purposes, but we’ll get to that later. The port numbers range from 0 to 65,535 and are split into three different groups.

* **Well-known ports** 0-1023
* **Registered ports** 1024-49,151
* **Dynamic ports** 49,152-65,535

**NOTE: Ever wonder why port numbers go from 0 to 65,535? If you’ve ever taken a Cisco class and learned any binary math, the answer is rather evident: the field in which you’ll find a port number is 16bits long, and having 16bits gives you 65.535 different combinations, from 0 to all the way up to 65,535.**

Of particular importance to you in becoming a proficient ethical hacker are the well-known port numbers. No, you don’t need to memorize all 1024 of the, but you do need to know many of them. The ports listed in the table below are absolutes – you simply must memorize these or quit reading here.

| **Port Number** | **Protocol** | **Transport Protocol** | **Port Number** | **Protocol** | **Transport Protocol** |
| --------------- | ------------ | ---------------------- | --------------- | ------------ | ---------------------- |
| 20/21           | FTP          | TCP                    | 110             | POP3         | TCP                    |
| 22              | SSH          | TCP                    | 135             | RPC          | TCP                    |
| 23              | Telnet       | TCP                    | 137-139         | NetBIOS      | TCP and UDP            |
| 25              | SMTP         | TCP                    | 143             | IMAP         | TCP                    |
| 53              | DNS          | TCP and UDP            | 161/162         | SNMP         | UDP                    |
| 67              | DHCP         | UDP                    | 389             | LDAP         | TCP and UDP            |
| 69              | TFTP         | UDP                    | 443             | HTTPS        | TCP                    |
| 80              | HTTP         | TCP                    | 445             | SMB          | TCP                    |

**TABLE X:** Important Port Numbers

**NOTE: More times than not, and probably daily, you’ll encounter weird ports and their use – like maybe 631. Did you know that one was the default for the Internet Printing Protocol? How about 179? Would you have guessed BGP? Or maybe 541? Did you pick SYSLOG? The point is, there are literally thousands of port numbers and associations. I can’t put them all in this chapter; therefore, do your best to memorize the common ones and use the process of elimination to whittle down to the best answer.**

Assuming you know which, well-known port number is associated with which upper-layer protocol, you can tell an awful lot about what a system is running just by knocking on the port doors to see what is open. A system is said to listen for a port when it has that port open. For example, assume you have a server hosting a website and an FTP service. When the server receives a message, it needs to know which application is going to handle the message. At the same time, the client that made the request needs to open a port on which to hold the conversation (anything above 1023 will work). The figure below demonstrates how this is accomplished – the server keeps track of which application to use via the port number in the destination port field of the header and answers to the source port number.

\
_**FIGURE X:** Port numbers in use between two communicating hosts._

In reading this, you may be wondering just how those ports are behaving on your own machine. The answer comes from the _state_ the port is in. Suppose you have an application running on your computer that is waiting for another computer to connect to it. Whatever port number your application is set to use is said to be in a _listening_ state. Once a remote system goes through all the handshaking and checking to establish a session over that open port on your machine, your port is said to be in an _established_ state. In short, a listening port is one that is waiting for a connection, while an established port is one that is connected to a remote computer, or device with an IP address.

**NOTE: CurrPorts is a tool you’ll definitely want to play with when it comes to ports. It displays a lot of all currently opened TCP/IP and UDP ports on your local computers, including information about the process that opened that port, the process name, full path, version information, the time it was created, and the user who created it. Far more high-level than running netstat.**

Ports can be in other states as well. For instance, remember that packets can be received out of order and sometimes take awhile to get in? Imagine your port sitting there in a listening state. A remote system connects, and off you go – with the data exchange humming along. Eventually either your system or the remote system will close the session. But what happens to any outstanding packets that haven’t made their way yet? A port state of CLOSE\_WAIT shows that the remote side of your connection has closed the connection, whereas a TIME\_WAIT state indicates that your side has closed the connection. The connection is kept open for a little while to allow any delayed packets to be matched to the connection and handled appropriately. If you’d like to see this in action on your Windows machine, open a command prompt and use an old standby: netstat. Typing netstat -an (see image below) displays all connections and listening ports, with addresses and port numbers in numerical form. If you have admin privileges on the box, use netstat -b, and you can see the executable tied to the open port.

**NOTE: Malicious scammers often use the netstat command as part of a social engineering tactic to trick users into believing that their computer is compromised and that they need to pay for unnecessary or fraudulent services. Once scammers persuade a victim to grant remote access to their computer using tools like TeamViewer, AnyDesk, or similar software, they open a command prompt and run the netstat -an command.**

**The scammer then explains the output of the netstat command to the victim, claiming that the various connections listed are evidence of hackers or malware currently accessing their computer. They might point out foreign addresses and suggest these are hackers connected to the victim’s machine. To resolve the issue, the scammer offers a solution which often involves the victim paying for fake antivirus software, security services, or fraudulent support subscriptions.**

### Subnetting

Let me share with you something I find neat. Most ethical hacking or penetration testing textbooks I’ve noticed contain a network section, and that’s great, as knowing how networks operate is a core KSA (Knowledge, Skill, Ability) every hacker should have. The one problem is that subnetting is never covered. In looking through 7 different books on ethical hacking topics only one of them presented and touched on subnetting. You may now be asking yourself, _“Why do we even need subnetting? What’s the point?”_ The answer, dear reader, is that depending on what type of hacking engagement you may take part of you will most likely run into certain situations where you don’t have access to an online subnet calculator hence making you have to use your brain to subnet a network. Supposedly you know this already, so this section will be a breeze (and I promise to keep it as short and sweet as possible); however, in keeping with my promise to cover everything, we just must get into it.

As I’m sure you’re already aware, your system has no idea about the rest of the world, and frankly doesn’t care. As far as it is concerned, its responsibility is to pass messages it receives to whatever application inside needs them, and to send messages only to systems inside its own neighborhood (network) – in effect, only systems it can see and touch, logically. It’s the job of someone else in the neighborhood (the router) to get the messages delivered to outside, unknown systems. And the only way that device must identify which networks are local and which networks are remote is the subnet mask. So, what is a subnet mask? To answer that, let’s first talk about what an IPv4 address entails.

**NOTE: IPv4 has three main address types:**

* **Unicast:** Acted on by a single recipient.
* **Multicast:** Acted on only by members of a specific group.
* **Broadcast:** Acted on by everyone in the network.

As you’re already aware (because you should know this already), IP addresses are really 32bits, each set to 1 or 0, separated into four octets by decimal points. Each one of these addresses is made up of two sections – a network identifier and a host identifier. The bits making up the network portion of the address are used much like the ZIP code on letters. Local post offices (like routers) don’t care about who, individually, a message is addressed for; they only care about which post office (network) to get the message to. For example, the friendly sorting clerk here at my local post office doesn’t care that the letter I put in the box to mail is addressed to the Wu Tang Clan; he only cares about the ZIP code. Once my letter gets to the post office serving the city Wu Tang reside in, the individual address will be looked at. It’s the same with IP addresses – something inside the destination network will be responsible for getting it to the right host, or its intended destination. It’s the router’s job to figure out what the network address is for any given IP, and the subnet mask is key.

A subnet mask is a binary pattern that is matched against any IP address to determine which bits belong to the network side of the address, with the binary starting from left to right, turning on all the 1;s until the mask is complete. For example, if your subnet mask wants to identify the first 12bits as the network identification bits, the mask will look like this:

11111111.11110000.00000000.00000000

Translate this to decimal and you get 255.240.0.0. Were you to pair this with an IP address, it would appear as 12.197.44.8, 255.240.0.0. Another common way of expressing this is to simply use a slash followed by the number of network bits. Continuing our example, the same pair would appear as 12.197.44.8/12.

**NOTE: You might hear things like “we need to sniff that slash 24,” or “we need to block that slash 16 from upstream.” Often networks that have been subnetted, in slang terms, is referred to simply as just a “slash” \<subnetted network>.**

Here are some rules you’ll need to know about IP addresses and the bits that make them up:

* If all the bits in the host field are 1’s, the address is a broadcast (that is, anything sent to that address will go to everything on that network).
* If all the bits in the host field are set to 0’s, that’s the network address.
* Any combination other than these two present the usable range of addresses in that network.

Let’s look at an example. Say you have an address of 172.17.15.12, and your subnet mask is 255.255.0.0. To see the network and host portions of the address, first convert the IP address from decimal notation to binary, convert the subnet mask to binary, and stack the two, as shown here:

Every bit from left to right is considered part of the network ID until you hit a zero in the subnet ID. This is all done in the flash of an eye by an XOR comparison (sometimes called an XOR gate) in the router. An XOR compares two binary inputs and creates an output: if the two inputs are the same, the output is 0; if they’re different, the output is 1. If you look at the subnet underneath the address (in binary), it’s easy to see how the XOR creates the network ID, but for most beginners (and not to complicate the issue further), it’s just as easy to draw the line and see where the division happens:

So, what this shows us is that the address 172.17.15.12 is part of a network addressed as 172.17.0.0, demonstrated by turning all the host bits to zero, as shown next:

The usable addresses within the 172.17.0.0 network can be found by changing the host bits. The first bit available is the first address, and all bits turned on except the last one comprise the last address (all bits turned on represent the broadcast address). This is displayed in the following illustration:

**NOTE: Broadcast addressing has two main types. Limited broadcast addresses are delivered to every system inside the broadcast domain, and they use IP address 255.255.255.255 (destination MAC FF:FF:FF:FF:FF:FF). Routers ignore all limited broadcasts and do not even open the packets on receipt. Directed broadcasts are sent to all devices on a subnet, and they use the subnet’s broadcast address (for example, the direct broadcast address for 192.168.17.0/24 would be 192.168.17.255). Routers may act on these packets, depending on what’s involved.**

This is easy enough when “the line” is drawn right on a decimal point. But what about when it falls in the middle of an octet? For example, consider the address 192.168.17.39 with a subnet mask of 255.255.255.224. The same process can be followed, but notice the line demarking the network and host bits now falls in the middle of the last octet:

Although it looks difficult, if you follow the same process discussed earlier—bringing down all the network bits and manipulating the host bits to show all zeros, all host bits off except the first, all host bits on except the last, and all host bits on—you can show the network ID, first, last, and broadcast addresses with ease:

One final thing you may be asked about involving subnetting is applying the mask to a host and determining what network it’s on. For example, suppose you have an IP address of 192.168.17.52/28, and you need to find out what network it’s on. If you use the same principles we just talked about—that is, translate the IP and mask into bits, stack them, draw your line, turn all host bits to zero—you’ll get your answer. Another, quicker way is to simply look at the first 28 bits only and…voilà! See the following illustration for a little more clarity:

**NOTE:** A fun differentiation you almost always see on tests is that between routing and routed protocols. Basically, a routed protocol is one that is being packaged up and moved around. IPv4 and IPv6, for instance, are routed protocols. A routing protocol is the one that decides the best way to get to the destination (for example, BGP, OSPF, or RIP).

Clear as mud, right? Trust me, don’t worry too much about it – the more you study and apply its theory, subnetting will become second nature to you; however, this _is_ a skill you’ll need in the real world, and you’ll find tips and tricks to help you out (for example, the network ID will always be some multiple of the decimal value of the last bit of the mask). Check out Internet resources for subnetting tips and tricks and use whatever feels best for you —and you’ll be fine. There is a whole lot more involved in addressing and routing that we’re just not going to get into here because it’s beyond the scope of this chapter; however, you maybe asked to identify a network ID, or figure out which address belongs to which network, or something like that. And that’s what I’ve laid out here for you.

Relevant ICMP Message Types

Because ICMP is built into each TCP/IP device and the associated responses provide detailed information about the recipient host, it makes a good place to start when network scanning. For example, consider an Echo Request (Type 8) sent to a host that returns a Type 3. The code could tell us whether the host is down (Code 1), the network route is missing or corrupt in our local route tables (Type 0), or a filtering device, such as a firewall, is preventing ICMP messages altogether (Type 13).

**NOTE The actual payload of a PING packet can range greatly in value amount. The request for comment (RFC 792, https://tools.ietf.org/html/rfc792) that created and still governs ping never got around to identifying what data is supposed to go into the payload, so it’s usually just enough ASCII code to build the packet up to sufficient length. Knowing this, the payload of an ICMP packet could wind up being the perfect covert channel for hackers to communicate with each other, using the payload area to simply embed messages. Most people—even security types —wouldn’t even bother with a ping packet or two crossing their paths, never knowing what information was being funneled away right beneath their noses.**

A few intrusion detectiosponses you expect from ports, and how stealthily the scan works. As far as your exam is concerned, count on being asked about each of these scan types at least once. Generally speaking, there are seven generic scan types for port scanning: • Full connect Also known as a TCP connect or full open scan, this runs through a full connection (three-way handshake) on ports, tearing it down with an RST at the end. It is the easiest to detect but it’s possibly the most reliable. Open ports will respond with a SYN/ACK, and closed ports will respond with an RST. • Stealth Also known as a half-open scan (and as a SYN scan). Only SYN packets are sent to ports (no completion of the three-way handshake ever takes place). Responses from ports are the same as they are for a TCP connect scan. This technique is useful in hiding your scanning efforts, possibly bypassing firewalls and monitoring efforts by hiding as normal traffic (it simply doesn’t get noticed because there is no connection to notice). • Inverse TCP flag This scan uses the FIN, URG, or PSH flag (or, in one version, no flags at all) to poke at system ports. If the port is open, there will be no response at all. If the port is closed, an RST/ACK will be sent in response. You know, the inverse of everything else.

**NOTE Naming conventions for scans in cybersecurity world can sometimes get kind of funny. Versions of the inverse TCP flag scan used to be called the FIN scan or the NULL scan. Stealth scans used to be known as SYN scans. Why do they change names? Your guess is as good as mine!**

**Open-Source Tools**

To start our discussion on open -source tools in this chapter, we’ll begin by discussing tools that aid in the network scanning phase of an assessment. Remember, these tools will scan a list of targets in an effort to determine which hosts are up and which ports are open.

### Nmap

Port scanners accept a target or a range as input, send a query to specified ports, and then create a list of the responses for each port. The most popular scanner is Nmap, written by Fyodor and available from [www.insecure.org](http://www.insecure.org/). Fyodor’s multipurpose tool has become a standard item among hackers and pentesters, network auditors and red teams alike. The intent of this book is not to teach you all of the different ways to use Nmap; however, we will focus on a few different scan types and options to make the best use of your scanning time and to return the best information to increase your attack depth.

Nmap Usage

**How to use:**

**Nmap \[Scan Type(s)] \[Options] Target(s)**

**Input fields:**

**\[Scan Type] is the type of scan to perform. Different scan options are available and are discussed throughout this chapter.**

**\[Options] include a wide variety of configuration options including DNS resolution, use of traceroutes, and more.**

_**Target**_**&#x20;is the target specification which can be a single host, a list of hostnames or IP addresses, or a full network.**

**Output:**

**Displays host information to the screen depending on scan type and options selected including accessibility of the host, active ports, and fingerprint data. There are also options available to output this data to a file.**

**Typical output: (extract)**



#### Nmap: Ping Sweep

Before scanning active targets, consider using Nmap’s ping sweep functionality with the -sn option. This option will not port-scan a target, but it will report which targets are up. When invoked as root with nmap -sn ip\_address, Nmap will send ICMP echo and timestamp packets as well as TCP SYN and ACK packets to determine whether a host is up. If the target addresses are on a local Ethernet network, Nmap will automatically perform an ARP scan versus sending out the packets and waiting for a reply. If the ARP request is successful for a target, it will be displayed. To override this behavior and force Nmap to send IP packets use the -send-ip option. If the sweep is needed to pass a firewall, it may also be useful to use a TCP ACK scan in conjunction with the TCP SYN scan. Specifying -PA will send a single TCP ACK packet which may pass certain stateful firewall configurations that would block a bare SYN packet to a closed port. In previous Nmap releases, this type of scan was invoked using the -sP option.

By understanding which techniques are useful for which environments, you increase the speed of your sweeps. This may not be a big issue when scanning a handful of systems, but when scanning multiple /24 networks, or even a /16, you may need this extra time for other testing. In the example illustrated below, the standard pings weep was the fastest for this particular environment, but that may not always be the case.

#### Nmap: ICMP Options

If Nmap can’t see the target, it won’t scan the target unless the -Pn (do not ping) option is used. This option was invoked using the -P0 and -PN option in previous Nmap releases. Using the -Pn option can create problems because Nmap will try to scan each of the target’s ports, even if the target isn’t up, which can waste time. To strike a good balance, consider using the -P option to select another type of ping behavior. For example, the -PP option will use ICMP timestamp requests and the -PM option will use ICMP netmask requests. Before you perform a full sweep of a network range, it might be useful to do a few limited tests on known IP addresses, such as web servers, DNS, and so on, so that you can streamline your ping sweeps and cut down on the number of total packets sent, as well as the time taken for the scans.

#### Nmap: Output Options

Capturing the results of the scan is extremely important, as you will be referring to this information later in the testing process, and depending on your client’s requirements, you may be submitting the results as evidence of vulnerability. The easiest way to capture all the needed information is to use the -oA flag, which outputs scan results in three different formats simultaneously: plaintext (.nmap), greppable text (.gnmap), and XML (.xml). The .gnmap format is especially important to note, because if you need to stop a scan and resume it at a later date, Nmap will require this file to resume, by using the -resume switch. Note the use of the -oA flag in the illustration below.

TIP:

Penetration testing can take some heavy computing resources when you are scanning and querying multiple targets with multiple threads. Running all of your tools from a LiveCD directly may not be the most efficient use of your resources on an extended pentest. Consider performing a hard-drive installation of your toolset so that you can expand and fully utilize the tools. Utilizing a virtual machine is another option to help better utilize machine resources while eliminating the need to install all of your tools individually. Basically, keep your penetration test scope in mind when you are designing your resources so that you do not get caught on the job without enough resources.

#### Nmap: Basic Scripting

When you specify your targets for scanning, Nmap will accept specific IP addresses, address ranges in both CIDR format such as /8, /16, and /24, as well as ranges using 192.168.1.100-200-style notation. If you have a hosts file, which may have been generated from your ping sweep earlier (hint, hint), you can specify it as well, using the -iL flag. There are other, more detailed Nmap parsing programs available such as the Nmap::Parser module for Perl (_**Source:** http://code.google.com/p/nmap-parser/_), but the illustration below shows how you can use the awk command to create a quick and dirty hosts file from an Nmap ping sweep. Scripting can be a very powerful addition to any tool but remember to check all the available output options before doing too much work, as some of the heavy lifting may have been done for you.

\
awk

#### Nmap: Speed Options

Nmap allows the user to specify the speed, or aggressiveness of the scan, or the amount of time from when the probe was sent to reply received, and therefore, how fast packets are sent. On a fast local area network (LAN), you can optimize your scanning by setting the -T option to 4, or Aggressive, usually without dropping any packets during the send. If you find that a normal scan is taking a very long time due to ingress filtering, or a firewall device, you may want to enable Aggressive scanning. If you know that an IDS sits between you and your target, and you want to be as stealthy as possible, using -T0 or Paranoid should accomplish what you need; however, it will take a longer time to finish a scan, perhaps several hours, depending on your scan parameters. The table below shows the timing template options for Nmap.

\
_**FIGURE X:** Using awk to parse Nmap output results._

#### Nmap: Port-Scanning Options

Besides ping sweeps, Nmap also does port scanning to identify which ports are open on a given target system. As part of our scan, we should find out which ports are open and then later determine which services (and versions) are using those ports as part of the enumeration phase. There are many options for performing this type of scan (as listed in Table below), but we’re going to focus on SYN scanning for this example. By using the -sS option with Nmap, you are able to do a port scan on a target or group of targets using a SYN scan. This is the default scan mechanism used by Nmap and is one of the most commonly performed scans due to its speed, stealth, and compatibility with most target operating systems. With this type of scan, no full TCP connection is made, and it is therefore considered a “half-open” scan. The figure below shows the results of a SYN scan against some sample hosts. This produces a listing of the open ports on the target, and possibly open/filtered ports, if the target is behind a firewall. The ports returned as open are listed with what service the ports correspond to, based on port registrations from the Internet Assigned Numbers Authority (IANA), as well as any commonly used ports, such as 31337 for Back Orifice. By default, Nmap 5.30 scans over 1000 ports for common services. This will catch most open TCP ports that are out there; however, sneaky system administrators may run services on uncommon ports, practicing security through obscurity. Without scanning those uncommon ports, you may be missing these services. If you have time, or you suspect that a system may be running other services, run Nmap with the -p0-65535 parameter, which will scan all 65,536 TCP ports. Note that this may take a long time, even on a LAN with responsive systems and no firewalls, possibly up to a few hours. Performing a test such as this over the Internet may take even longer, which will also allow more time for the system owners, or watchers, to note the excessive traffic and shut you down.

\
_**FIGURE X:** Nmap TCP SYN Scan._

#### Nmap: Stealth Scanning

For any scanning that you perform, it is not a good idea to use a connect scan (-sT), which fully establishes a connection to a port. Excessive port connections can create a DoS condition with older machines and will definitely raise alarms on any IDS. For that reason, you should usually use a stealthy port-testing method with Nmap, such as a SYN scan. Even if you are not trying to be particularly stealthy, this is much easier on both the testing system and the target.

In addition to lowering your profile with half-open scans, you may also consider the ftp or “bounce” scan and idle scan options which can mask your IP from the target. The ftp scan takes advantage of a feature of some FTP servers, which allow anonymous users to proxy connections to other systems. If you find during your enumeration that an anonymous FTP server exists, or one to which you have login credentials, try using the -b option with user:pass@server:ftpport. If the server does not require authentication, you can skip the user:pass, and unless FTP is running on a nonstandard port, you can leave out the ftpport option as well. This type of scan works only on FTP servers, allowing you to “proxy” an FTP connection, and many servers today disable this option by default.

The idle scan, using -sI zombiehost:port, has a similar result but a different method of scanning. This is detailed further at Fyodor’s web page, http://nmap.org/book/idlescan.html, but the short version is that if you can identify an intermediate target (zombie) with low traffic and predictable fragment identification (IP ID) values, you can send spoofed packets to your real target, with the source set to the zombie or idle target. The result is that an IDS sees the idle scan target as the system performing the scanning, keeping your system hidden. If the idle target is a trusted IP address and can bypass host-based access control lists, even better! Do not expect to be able to use a bounce or idle scan on every penetration test engagement but keep looking around for potential targets. Older systems, which do not offer useful services, may be the best targets for some of these scan options.

Core Technology

TIP:

So far, we have focused on TCP-based services because most interactive services that may be vulnerable run over TCP. This is not to say that UDP-based services, such as rpcbind, tftp, snmp, nfs, and so on, are not vulnerable to attack. UDP scanning is another activity which could take a very long time, on both LANs and wide area networks (WANs). Depending on the length of time and the types of targets you are attacking, you may not need to perform a UDP scan. However, if you are attacking targets that may use UDP services, such as infrastructure devices and SunOS/Solaris machines, taking the time for a UDP scan may be worth the effort. Nmap uses the flag -sU to specify a UDP scan.

_Netenum: Ping Sweep_

If you need a very simple ICMP ping sweep program that you can use for scriptable

applications, netenum might be useful. It performs a basic ICMP ping and then

replies with only the reachable targets. One quirk about netenum is that it requires

a timeout to be specified for the test. If no timeout is specified, it outputs a CRdelimited dump of the input addresses. If you have tools that will not accept

a CIDR-formatted range of addresses, you might use netenum to simply expand

that into a listing of individual IP addresses. Fig. 3.4 shows the basic usage of

netenum in ping sweep mode with a timeout value of 5, as well as network address

expansion mode showing the valid addresses for a CIDR of 192.168.1.0/24,

including the network and broadcast addresses.

3.2 Scanning 107

Netenum USAGE

How to use:

netenum destination \[Timeout] \[Verbosity]

Input fields:

Destination is the target specification which can be a single host or a full network/

subnet.

\[Timeout] is a value to use for the scan. Any value greater than 0 will use pings to scan.

\[Verbosity] is a value 0–3 that determines how verbose the output is.

Output:

Displays active hosts to the screen. Can be redirected to a file or to another command for

scripted scans.

Typical outpuIf you need a very simple ICMP ping sweep program that you can use for scriptable

applications, netenum might be useful. It performs a basic ICMP ping and then

replies with only the reachable targets. One quirk about netenum is that it requires

a timeout to be specified for the test. If no timeout is specified, it outputs a CRdelimited dump of the input addresses. If you have tools that will not accept

a CIDR-formatted range of addresses, you might use netenum to simply expand

that into a listing of individual IP addresses. Fig. 3.4 shows the basic usage of

netenum in ping sweep mode with a timeout value of 5, as well as network address

expansion mode showing the valid addresses for a CIDR of 192.168.1.0/24,

including the network and broadcast addresses.

3.2 Scanning 107

Netenum USAGE

How to use:

netenum destination \[Timeout] \[Verbosity]

Input fields:

Destination is the target specification which can be a single host or a full network/

subnet.

\[Timeout] is a value to use for the scan. Any value greater than 0 will use pings to scan.

\[Verbosity] is a value 0–3 that determines how verbose the output is.

Output:

Displays active hosts to the screen. Can be redirected to a file or to another command for

scripted scans.

Typical output:

#### Unicornscan: Port Scan and Fuzzing

Unicornscan is different from a standard port-scanning program; it also allows you to specify more information, such as source port, packets per second sent, and randomization of source IP information, if needed. For this reason, it may not be the best choice for initial port scans; rather, it is more suited for later _**“fuzzing”**_ or experimental packet generation and detection; however, just as Nmap has capabilities which far exceed that of a ping sweep, Unicornscan can be used for basic port scans in addition to its more complex features.

**Unicornscan USAGE**

**How to use:**

unicornscan \[Options] Target(s):Port(s)

**Input fields:**

\[Options] are very wide ranging and control the type of scan performed as well as very

granular control over the packets sent. A list of all options can be seen by using the -h option.

Target(s) is the target specification which can be a single host or a range using a CIDR

mask.

Port(s) are the ports to scan.

**Output:**

Displays identified ports and their status to the screen

Recommended Reading and Resources

Network scanning and enumeration are foundational skills in the field of information and cyber security, essential for assessing the security posture of a system or network. Below is a curated list of recommended readings and resources that cover various aspects of network scanning and enumeration techniques, tools, and best practices. This list includes books, online courses, and articles that cater to beginners as well as seasoned professionals looking to deepen their expertise.

| _“Nmap Network Exploration and Security Monitoring,”_ by Gordon Lyon                                                          | A comprehensive guide to using Nmap for network exploration and security auditing. It covers everything from basic usage to advanced features and scripting.                                             |
| ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _“Metasploit: The Penetration Tester’s Guide,”_ by David Kennedy, Devon Kearns, Jim O’Gorman, Mati Aharoni, and Michael Davis | While not exclusively focused on network scanning and enumeration, this book offers valuable insights into penetration testing methodologies including the use of Metasploit for network reconnaissance. |
| _“Network Warrior,”_ by Gary A. Donahue                                                                                       | Offers practical advice for managing and securing network infrastructure. It includes chapters on network scanning and enumeration tools and techniques.                                                 |

**Online Courses**

1. **Network Penetration Testing by Udemy**

Covers a broad range of topics related to network penetration testing, including scanning and enumeration techniques.

1. **Learn Network Scanning and Enumeration by Coursera**

Part of a larger course on cybersecurity, this module focuses specifically on network scanning and enumeration.

1. **Introduction to Network Security Assessment by Cybrary**

Provides a solid foundation in network security assessment, including scanning and enumeration techniques.

**Articles and Blogs**

1. _**“How to Do Network Discovery and Mapping,”**_ by Paul Rascagneres

An article that delves into the basics of network discovery and mapping, covering tools and techniques commonly used in the field.

1. _**“Network Scanning Techniques,”**_ by Peter Kim

Offers an overview of various network scanning techniques, including port scanning, ping scanning, and OS fingerprinting.

1. _**“The Art of Network Enumeration,”**_ by Chris McNab

Explores the art of network enumeration, focusing on the importance of gathering accurate and complete information about a target network.

**Websites and Forums**

1. **Nmap Project Website**

The official website for Nmap, a free and open-source tool for network discovery and security auditing. It offers extensive documentation, tutorials, and forums for users.

1. **Reddit r/netsec**

A subreddit dedicated to network security where you can find discussions, tips, and resources on network scanning and enumeration.

1. **Stack Exchange Network Engineering**

A Q\&A site for network engineers and administrators. You can find answers to specific questions about network scanning and enumeration here.

Why Stealthiness is Important in Ethical Hacking<br>
