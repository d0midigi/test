# Performing Host Discovery with Nmap

### Performing Host Discovery with Nmap

As a computer network engineer that regularly conducts penetration tests and ethical hacking, a recurring challenge seems to arise when assessing organizations with a large allocation of IP address space. What does one do when faced with multiple class B’s, a few class C’s, and a limited amount of time? Do you stick all of the address spaces in your favorite scanner and hit the _Go_ button, wait until it’s done and hope the results are accurate? How can one be sure that the scanner being used finds all accessible hosts? Do you even know the method your scanner uses to discover which hosts are alive and its methodology to accomplish that?

This section aims to answer the following questions and will illustrate in (a technical high-level manner) the methodology that I use to accurately discover which hosts are accessible prior to conducting port scanning, enumeration, or a vulnerability assessment.

Something to consider: Depending on who you talk to, some may say that unless one performs a scan on all 65535 TCP and UDP ports on every possible IP address in the range, that the penetration tester isn’t being thorough enough. While I do mostly agree that to be completely thorough, one must perform a scan as such, I have rarely, if ever, had the luxury of performing such a scan, as such a feat takes a considerable amount of time. An underlying theme about Information Security is about striking a balance and weighing the pros and cons of everything. If being absolutely thorough and time is of no concern, you’ll more than likely want to run a full, credentialed scan on all IP addresses. If, however, a balance can be struck between being thorough and completing the project on time, read on – you may learn some techniques to improve both the accuracy and efficiency of your scans.

### Understanding Host Discovery

Host discovery refers to the preliminary stage of an ethical hacking security engagement aimed at identifying the live hosts present on a network. This phase is crucial because it helps in determining the number of devices that are accessible, especially when dealing with firewalls where explicit rules may obscure the visibility of all hosts behind them. An anecdotal example illustrates this point: a commercial scanner was used to scan a Class C network, revealing only one host; however, employing the techniques discussed in this section, it was discovered that there were actually seventeen hosts in the DMZ. Commercial scanners often fall short in host discovery due to limited options and configurability, particularly in refining the discovery method.

Given the focus of this section on Nmap and host discovery, we will include in our discussion how Nmap performs its discovery tasks and explore ways to enhance the host discovery phase of a penetration test or vulnerability assessment through Nmap’s options.

### Understanding Nmap’s Default Behavior

Let’s break down a fundamental Nmap command to understand its structure:

nmap -sS -O 172.26.1.0/29

When initiating a port scan, nmap -sS target or a ‘ping sweep (nmap -sP target), Nmap concurrently sends ICMP echo request packets and ‘TCP pings’ to all targets with the scan’s scope. A ‘TCP ping’ is defined as a TCP packet with the ACK flag set, destined for port 80 of the target hosts. The expected response from an accessible host is either a TCP packet with the RST flag set or an ICMP echo reply, indicating the host’s availability. Absence of response suggests the host is either unreachable or protected behind a firewall.

Only after confirming a host’s reachability does Nmap proceed with the port scan. While Nmap’s default discovery method is effective in certain scenarios, it shouldn’t be solely relied upon for accurate host identification. Thankfully, Nmap’s flexibility allows for customization of nearly every aspect of the discovery process.

In addition, this command consists of three main phases:

1. Host Discovery
2. Port Scanning
3. OS Fingerprinting

Since our discussion centers around host discovery, we will concentrate on the first phase, briefly touching upon the others. It’s worth noting, however, that the discovery phase can be skipped altogether by using the -P0 option, directing Nmap straight to the port scanning phase.

Throughout this section we will utilize a DMZ environment with varying firewall rules to demonstrate effective host discovery techniques. The DMZ architecture referenced throughout this section is visually represented below.

![A diagram of a firewall

Description automatically generated](<../../.gitbook/assets/0 (63).png>)

_**FIGURE 1:** Basic DMZ network topology._

#### Scenario 1: Firewall Without Filtering

Here, we are dealing with a standard DMZ setup, protected by a firewall that filters incoming traffic. For our scenarios, we’ll utilize “pseudo-rulesets” to maintain readability. Please note that the rule syntax combines elements from PR and English, so exact precision is not of real importance – readability is the ultimate goal. Additionally, the version of Nmap employed for these tests is 7.95.

Our scanning host is on the 192.168.5.0/24 network with the IP address 192.168.5.20.

Unless stated otherwise, we will use the following nmap command for all discovery scans:

nmap -sP 172.16.26.1/29

The -sP option specifies that only a discovery scan will be performed, which is the same method used in a default nmap scan.

### Understanding Nmap’s Default Behaviors

To effectively customize Nmap’s behaviors, it’s important to first grasp its default operation, especially regarding host discovery, and recognize when its default settings might fall short. When executing a port scan (e.g., nmap -sS target) or a ping sweep (nmap -sP target) against a network or host, Nmap employs a dual-pronged approach. It dispatches both ICMP ECHO request packets and TCP pings to all potential targets within the scan’s range.

The term TCP ping refers to a TCP packet with the ACK flag activated, intended for port 80 of the target hosts. The anticipated response from an accessible host is either a TCP packet with the RST flag set or an ICMP ECHO reply, signaling that the host is active. **Absence of any response suggests the host is inactive or shielded behind a firewall, rendering it inaccessible via port 80 (HTTP).**

Nmap only proceeds to portscan the target once it confirms the host’s reachability. While the default discovery method of Nmap is effective in some scenarios, it shouldn’t be solely depended upon for determining accessible hosts. Thankfully, Nmap offers extensive flexibility, allowing customization of nearly every aspect of the discovery process.

Below is an example illustrating a default Nmap discovery of a single host on my network:

nmap -sP 172.26.11

**tcpdump Output:**

9:26:49.324016 192.168.5.20 > 172.26.1.1: ICMP: echo request

09:26:49.324083 192.168.5.20.40435 > 172.26.1.1.http: . ack 1942297083 win 3072

In this output, both the ICMP ping and the TCP ping are visible, demonstrating Nmap’s simultaneous use of these methods for host discovery.

#### Scenario 2: Unfiltered Firewall Behavior During Discovery

In our initial scenario, we explored the discovery process in an environment where the firewall doesn’t apply any filtering rules, essentially functioning as a mere router. This setup allows us to observe the unobstructed operation of Nmap during host discovery.

**Command Executed:**

nmap -sP 172.26.1.0/29

**Firewall Configuration:**

* **Rule:** Pass from Any to Any

**tcpdump Output:**

08:59:58.840249 192.168.5.20 > 172.26.1.0: ICMP: echo request

08:59:58.840667 192.168.5.20.60923 > 172.26.1.0.http: . ack 2990889584 win 3072

08:59:58.840726 192.168.5.20 > 172.26.1.1: ICMP: echo request

08:59:58.840764 192.168.5.20.60923 > 172.26.1.1.http: . ack 1015938099 win 3072

...

08:59:58.841103 192.168.5.20 > 172.26.1.6: ICMP: echo request

08:59:58.841140 192.168.5.20.60923 > 172.26.1.6.http: . ack 550856434 win 3072

08:59:58.841178 192.168.5.20 > 172.26.1.7: ICMP: echo request

08:59:58.841215 192.168.5.20.60923 > 172.26.1.7.http: . ack 2476756145 win 3072

08:59:58.841886 172.26.1.2 > 192.168.5.20: ICMP: echo reply

08:59:58.842149 172.26.1.4 > 192.168.5.20: ICMP: echo reply

08:59:58.842377 172.26.1.2.http > 192.168.5.20.60923: R 1228729075:1228729075(0) win 0 (DF)

08:59:58.842699 192.168.5.5 > 192.168.5.20: ICMP: echo reply

08:59:58.842905 172.26.1.4.http > 192.168.5.20.60923: R 1859940754:1859940754(0) win 0 (DF)

08:59:58.843263 172.26.1.6 > 192.168.5.20: ICMP: echo reply

08:59:58.843487 172.26.1.6.http > 192.168.5.20.60923: R 550856434:550856434(0) win 0 (DF)

**Outcome:**

* All hosts discovered.

In the tcpdump output, we witness Nmap’s discovery mechanism in action. It broadcasts ICMP and TCP packets to all addresses within the specified subnet (172.26.1.0/29) and awaits responses. Responses from reachable hosts are indicated in yellow, highlighting successful host discovery in an unfiltered firewall environment.

#### Scenario 3: Host Discovery with a Basic Firewall Ruleset

In this scenario, we examine how Nmap’s default discovery method operates under a firewall configured with a generic, or ‘out-of-the-box’ set of rules. This setup provides insights into how Nmap interacts with firewalls that allow certain types of traffic while blocking others.

**Command Executed:**

nmap -sP 172.26.1./29

**Firewall Configuration:**

* Allow TCP traffic on port 80, 53, and 25.
* Drop all other traffic.

**tcpdump Output:**

09:12:21.505016 192.168.5.20 > 172.26.1.0: ICMP: echo request

09:12:21.505125 192.168.5.20.60212 > 172.26.1.0.http: . ack 3755150488 win 3072

...

09:12:21.506577 172.26.1.2.http > 192.168.5.20.60212: R 3464075465:3464075465(0) win 0 (DF)

09:12:21.506830 172.26.1.6.http > 192.168.5.20.60212: R 1701634905:1701634905(0) win 0 (DF)

09:12:21.507104 172.26.1.4.http > 192.168.5.20.60212: R 337683576:337683576(0) win 0 (DF)

**Outcome:**

* All hosts discovered.

Despite the firewall’s generic ruleset, which permits TCP traffic on specific ports and drops everything else, Nmap successfully discovers all hosts. This success is attributed to the firewall’s lack of statefulness, allowing TCP pings to pass unhindered; however, ICMP packets, essential for Nmap’s discovery process, are blocked by the final “cleanup” rule, showcasing the limitations of relying solely on TCP-based discovery methods in environments with restrictive firewall policies.

#### Scenario 4: Host Discovery with a Detailed Firewall Ruleset

In this fourth scenario, we examine how Nmap’s default discovery method functions within a network protected by a firewall configured with a high-level ruleset. This setup is designed to offer a closer examination of how Nmap’s discovery capabilities are affected by targeted firewall restrictions.

**Command Executed:**

nmap -sP 172.26.1.0/29

**Firewall Configuration:**

* Permit TCP traffic destined for specific hosts on particular ports:
  * Port 80 to 172.26.1.2
  * Port 53 to 172.26.1.4
  * Port 25 to 172.26.1.6
* Drop all other traffic.

**tcpdump Output:**

08:05:07.733225 192.168.5.20 > 172.26.1.0: ICMP: echo request

08:05:07.733334 192.168.5.20.44273 > 172.26.1.0.http: . ack 1621467562 win 2048

...

08:05:07.733820 192.168.5.20 > 172.26.1.7: ICMP: echo request

08:05:07.733856 192.168.5.20.44273 > 172.26.1.7.http: . ack 228721671 win 2048

08:05:07.734611 172.26.1.2.http > 192.168.5.20.44273: R 3921129299:3921129299(0) win 0 (DF)

**Outcome:**

* Only 1 host was discovered.

With the firewall’s ruleset becoming increasingly specific, the effectiveness of Nmap’s default discovery method is significantly reduced. The firewall configuration allows only TCP pings destined for specific services (HTTP on port 80, DNS on port 53, and SMTP on port 25) to pass through. Consequently, the majority of ICMP ECHO requests, integral to Nmap’s discovery process, are blocked by the firewall’s “drop all” policy, limiting the discovery to only those hosts explicitly permitted by the firewall rules.

This scenario focuses on the importance of considering network security configurations when planning network scanning activities, as they can greatly influence the visibility and accessibility of hosts within any given network.

#### Scenario 5: Analyzing Host Discovery with a Stateful Firewall

In this fifth scenario, we encounter a firewall configured to perform stateful inspection alongside a highly specific ruleset. This setup introduces a new layer of complexity to the network environment, affecting how Nmap’s default discovery method operates.

**Command Executed:**

nmap -sP 172.26.1.0/29

**Firewall Configuration:**

* Specifically permit TCP traffic to certain hosts on designated ports, with state tracking enabled:
  * Port 80 to 172.26.1.2
  * Port 53 to 172.26.1.4
  * Port 25 to 172.26.1.6
* Drop all other traffic.

**tcpdump Output:**

08:46:23.548456 192.168.5.20.44390 > 172.26.1.2.http: . ack 3476163011 win 2048

08:46:23.548468 192.168.5.20 > 172.26.1.3: ICMP: echo request

...

08:46:23.548789 192.168.5.20 > 172.26.1.7: ICMP: echo request

08:46:23.548825 192.168.5.20.44390 > 172.26.1.7.http: . ack 2518875875 win 2048

**Outcome:**

* No hosts discovered.

In this scenario, despite sending both standard TCP pings and ICMP packets, there are no replies received from the hosts. This outcome is primarily due to the firewall’s stateful inspection feature combined with its specific ruleset. The firewall tracks the state of connections initiated from allowed sources to the specified destinations on the permitted ports. Any unsolicited incoming traffic, including the TCP ACK packets used by Nmap for its TCP pings, is dropped because it does not match any existing connection states tracked by the firewall.

Furthermore, the firewall’s “cleanup” rule blocks ICMP packets, which are essential for Nmap’s discovery process. This combination of stateful inspection and specific rules effectively prevents Nmap’s default discovery method from identifying any hosts in the network, highlighting the challenges posed by modern firewall technologies to traditional scanning techniques.

This scenario highlights the necessity for scanners like Nmap to adapt to advanced network defenses, potentially requiring alternative discovery methods or the use of evasion techniques to bypass strict firewall rules and successfully identify hosts within a network.

### Host Discovery with Advanced Nmap Techniques

In the preceding scenarios, we observed that Nmap’s default discovery options were insufficient against certain firewall configurations. To overcome these limitations and enhance our ability to discover hosts, we need to leverage Nmap’s advanced features. This section examines customizing TCP pings, a critical technique for navigating through sophisticated firewall protections.

#### Customizing TCP Pings

Nmap’s default TCP pings employ a TCP packet with the ACK flag set, targeting port 80 (HTTP). This approach often fails against stateful firewalls, which scrutinize each packet against known connection states. If the packet doesn’t correspond to an ongoing session, it’s deemed suspicious and discarded, preventing host discovery.

To circumvent this issue, we can customize the TCP ping. One effective strategy involves replacing the ACK flag with the SYN flag, which initiates a new connection attempt. This can be achieved using the -PS option in Nmap:

nmap -sP -PS 172.26.1.2

This command sends a SYN packet to port 80 of the target host (172.26.1.2), which is less likely to be filtered by stateful firewalls unless specifically prohibited by other rules.

Further customization is possible by specifying a different destination port with the -PS option. For instance, targeting port 25 (SMTP) instead of the default port 80:

nmap -sP -PS25 172.26.1.2

This command sends a SYN packet to port 25, potentially evading filters that block HTTP traffic.

#### Specifying Source Ports

Another customization technique involves setting a specific source port for TCP packets. This can sometimes bypass overly permissive firewall rules, especially those that inadvertently allow traffic from unexpected source ports; however, this approach is generally unreliable and should be used cautiously:

**Command Executed:**

nmap -sP 172.26.1.0/29 -g 53

**tcpdump Output:**

10:52:02.083065 192.168.5.20 > 172.26.1.0: ICMP: echo request

10:52:02.083260 192.168.5.20.domain > 172.26.1.0.http: . ack 2177885259 win 3072

10:52:02.083301 192.168.5.20 > 172.26.1.1: ICMP: echo request

10:52:02.083346 192.168.5.20.domain > 172.26.1.1.http: . ack 2684323392 win 3072

10:52:02.083384 192.168.5.20 > 172.26.1.2: ICMP: echo request

10:52:02.083421 192.168.5.20.domain > 172.26.1.2.http: . ack 1438652920 win 3072

10:52:02.083459 192.168.5.20 > 172.26.1.3: ICMP: echo request

10:52:02.083496 192.168.5.20.domain > 172.26.1.3.http: . ack 771338950 win 3072

10:52:02.083534 192.168.5.20 > 172.26.1.4: ICMP: echo request

10:52:02.083570 192.168.5.20.domain > 172.26.1.4.http: . ack 3541039396 win 3072

10:52:02.083608 192.168.5.20 > 172.26.1.5: ICMP: echo request

10:52:02.083645 192.168.5.20.domain > 172.26.1.5.http: . ack 2586779353 win 3072

10:52:02.083683 192.168.5.20 > 172.26.1.6: ICMP: echo request

10:52:02.083719 192.168.5.20.domain > 172.26.1.6.http: . ack 45434507 win 3072

10:52:02.083757 192.168.5.20 > 172.26.1.7: ICMP: echo request

10:52:02.083794 192.168.5.20.domain > 172.26.1.7.http: . ack 1886752887 win 3072

10:52:02.084616 172.26.1.2.http > 192.168.5.20.domain: R 1438652920:1438652920(0) win 0 (DF)

10:52:02.084845 172.26.1.4.http > 192.168.5.20.domain: R 3541039396:3541039396(0) win 0 (DF)

10:52:02.085219 172.26.1.6.http > 192.168.5.20.domain: R 45434507:45434507(0) win 0 (DF)

This command specifies port 53 (DNS) as the source port, leveraging a potential loophole in the firewall’s ruleset that permits DNS traffic from any port to any host in the DMZ.

As an ethical hacker, knowing how to customize TCP pings and exploiting firewall logic errors are powerful techniques for enhancing host discovery with Nmap. By adapting to the specific characteristics of network defenses, we can navigate around restrictions and uncover hidden hosts; however, it’s crucial to use these advanced options responsibly, mindful of the ethical implications and legal considerations associated with network scanning.

### Customizing ICMP Messages for Host Discovery

In scenarios where firewalls aggressively filter out ICMP ECHO requests (used by the -sP option in Nmap for host discovery), alternative ICMP message types can serve as effective alternatives. Recent versions of Nmap support two such ICMP message types: **Timestamp Requests** and **Address Mask Requests.** These methods can bypass certain firewall restrictions and provide a means to determine if a host is online.

#### Using ICMP Timestamp Requests (-PP)

ICMP Timestamp Requests (Type 13) and Replies (Type 14) are used to measure the round-trip time between two hosts. When Nmap sends a Timestamp Request, it expects a Timestamp Reply (Type 14) in return. If a reply is received, Nmap concludes that the host is alive.

**Command Executed:**

nmap -sP -PP 172.26.1.4

**tcpdump Output:**

13:32:05.780376 192.168.5.20 > 172.26.1.4: icmp: time stamp query id 47345 seq 0 (DF)

13:32:05.781066 172.26.1.4 > 192.168.5.20: icmp: time stamp reply id 47345 seq 0 : org 0x0 recv 0x3c339bd xmit 0x3c339bd

#### Using ICMP Address Mask Requests (-PM)

ICMP Address Mask Requests (Type 17) and Replies (Type 18) are typically used by routers to discovery the network mask of a directly connected network. Sending an Address Mask Request can be a way to check if a host responds to ICMP messages other than echo requests. If a Type 18 packet is received, the host is considered alive.

**Command Executed:**

nmap -sP -PM 172.26.1.4

**tcpdump Output:**

13:37:11.452204 192.168.5.20 > 172.26.1.4: icmp: address mask request (DF)

Note: While these ICMP message types can be effective in certain situations, it’s important to note that not all operating systems respond to the requests. For example, Address Mask Requests are most likely to elicit a response from routers rather than general-purpose hosts. Additionally, even if a firewall allows these custom ICMP packets, the behavior of the receiving host plays a significant role in whether a response is generated.

These techniques highlight the versatility of Nmap in host discovery, offering alternatives when traditional methods face barriers imposed by network security measures.

### Piecing it Together: Integrating Advanced Techniques for Comprehensive Host Discovery

In this final scenario, we aim to explore comprehensive host discovery methods in a challenging network environment characterized by a stateful firewall with specific rules that drop all traffic except for TCP traffic to specific ports on certain hosts. Our goal is to identify all hosts within a DMZ network segment, despite the restrictive firewall configuration.

#### Initial Attempt with Default TCP Ping

We begin with a default TCP ping using Nmap, targeting port 80 (HTTP):

**Enforced Firewall Ruleset:**

_pass from any to 172.26.1.2 proto tcp port 80 keep state_

_pass from any to 172.26.1.4 proto tcp port 53 keep state_

_pass from any to 172.26.1.6 proto tcp port 25 keep state_

_drop all_

**Command Executed:**

nmap -sP -PS80 172.26.1.0/29

**tcpdump Output:**

11:03:11.198359 192.168.5.20.49989 > 172.26.1.0.http: S 3857711107:3857711107(0) win 1024

11:03:11.198465 192.168.5.20.49989 > 172.26.1.1.http: S 3508535339:3508535339(0) win 1024

11:03:11.198506 192.168.5.20.49989 > 172.26.1.2.http: S 1017118803:1017118803(0) win 1024

11:03:11.198544 192.168.5.20.49989 > 172.26.1.3.http: S 832045179:832045179(0) win 1024

11:03:11.198582 192.168.5.20.49989 > 172.26.1.4.http: S 2873622691:2873622691(0) win 1024

11:03:11.198620 192.168.5.20.49989 > 172.26.1.5.http: S 1101529291:1101529291(0) win 1024

11:03:11.198658 192.168.5.20.49989 > 172.26.1.6.http: S 99614963:99614963(0) win 1024

11:03:11.198696 192.168.5.20.49989 > 172.26.1.7.http: S 3741843739:3741843739(0) win 1024

11:03:11.199453 172.26.1.2.http > 192.168.5.20.49989: S 92167158:92167158(0) ack

1017118804 win 5840 \<mss 1460> (DF)

The tcpdump output shows SYN packets being sent to various addresses within the range, but only the host at 172.26.1.2 (our web server) responds, indicating that it is the only host reachable via port 80.

#### Adjusting for Specific Services

Recognizing the firewall’s restrictions, we adjust our approach by changing the destination port of the TCP ping to port 25 (SMTP), a service that might be running on other hosts:

**Command Executed:**

nmap -sP -PS25 172.26.1.0/29

**tcpdump Output:**

11:05:06.000617 192.168.5.20.38849 > 172.26.1.0.smtp: S 3544186883:3544186883(0) win 2048

11:05:06.000720 192.168.5.20.38849 > 172.26.1.1.smtp: S 4056940587:4056940587(0) win 2048

11:05:06.000759 192.168.5.20.38849 > 172.26.1.2.smtp: S 3272605779:3272605779(0) win 2048

11:05:06.000797 192.168.5.20.38849 > 172.26.1.3.smtp: S 4168614011:4168614011(0) win 2048

11:05:06.000835 192.168.5.20.38849 > 172.26.1.4.smtp: S 586154147:586154147(0) win 2048

11:05:06.000872 192.168.5.20.38849 > 172.26.1.5.smtp: S 3571974347:3571974347(0) win 2048

11:05:06.000910 192.168.5.20.38849 > 172.26.1.6.smtp: S 667418867:667418867(0) win 2048

11:05:06.000948 192.168.5.20.38849 > 172.26.1.7.smtp: S 902824219:902824219(0) win 2048

11:05:06.001909 172.26.1.6.smtp > 192.168.5.20.38849: S 203047548:203047548(0) ack

667418868 win 5840 \<mss 1460> (DF)

This time, the tcpdump output reveals that SYN packets are sent to all addresses within the range, and importantly, a SYN/ACK packet is received from the host at 172.26.1.6. This indicates that this host is running an SMTP service and is accessible via port 25, suggesting that it is the only host besides the web server that has been successfully identified so far.

Because we see that SMTP server (172.26.1.6) replies, let’s change the destination TCP port to 53 to probe for our DNS server.

**Command Executed:**

nmap -sP -PS53 172.26.1.0/29

**tcpdump Output:**

11:06:52.601522 192.168.5.20.51592 > 172.26.1.0.domain: S 2862088195:2862088195(0) win 4096

11:06:52.601623 192.168.5.20.51592 > 172.26.1.1.domain: S 3921149995:3921149995(0) win 4096

11:06:52.601662 192.168.5.20.51592 > 172.26.1.2.domain: S 3150970963:3150970963(0) win 4096

11:06:52.601699 192.168.5.20.51592 > 172.26.1.3.domain: S 4262985851:4262985851(0) win 4096

11:06:52.601736 192.168.5.20.51592 > 172.26.1.4.domain: S 3247440035:3247440035(0) win 4096

11:06:52.601773 192.168.5.20.51592 > 172.26.1.5.domain: S 1634730187:1634730187(0) win 4096

11:06:52.601811 192.168.5.20.51592 > 172.26.1.6.domain: S 947388659:947388659(0) win 4096

11:06:52.601848 192.168.5.20.51592 > 172.26.1.7.domain: S 2042102043:2042102043(0) win 4096

11:06:52.602957 172.26.1.4.domain > 192.168.5.20.51592: S 328239288:328239288(0) ack

3247440036 win 5840 \<mss 1460> (DF)

With our DNS server (172.26.1.4) having responded, we’ve successfully accounted for all hosts within our DMZ; however, this achievement brings forth a critical consideration: in real-world external assessments, obtaining information about the systems and services available within a network is rarely straightforward. It’s not easy. Like most hacking efforts, it takes time, persistence, and patience. This lack of initial knowledge complicates the task of discovering hosts efficiently, particularly when faced with stringent firewall configurations designed to restrict access.

To conduct a thorough discovery in such environments, employing TCP Ping sweeps with a wide array of destination and source ports becomes essential. Targeting the destination ports commonly associated with internet services is a prudent starting point. Meanwhile, selecting source ports that are less frequently blocked by firewalls, such as port 20 and 53, can increase the likelihood of successful probes.

Automating this process can significantly streamline the discover phase. Writing a script to execute these scans and analyze the results can save considerable time and effort. An example of such script is available at _http://www.moonpie.org/tools/discover.tgz_, demonstrating how Perl can be utilized to automate the discovery process across a variety of ports.

This approach highlights the adaptability and creativity in network reconnaissance, especially when dealing with complex security architectures. By leveraging a broad spectrum of TCP Ping sweeps and automating the process, we can effectively navigate around network defenses to uncover all hosts and their services, thereby completing a comprehensive discovery mission.

Through these steps, we demonstrated how to employ Nmap’s advanced features to navigate around restrictive firewall rules and identify hosts within a network. Initially, we attempted to use a default TCP ping targeting port 80, which was only successful for the web server. By adjusting our approach to target port 25, we were able to identify an additional host running an SMTP service.

The scenario demonstrates the importance of understanding both the capabilities of Nmap and the specific network security measures when conducting host discovery. By tailoring our scanning techniques to the characteristics of the network environment, we can achieve more comprehensive results, even in challenging conditions.
