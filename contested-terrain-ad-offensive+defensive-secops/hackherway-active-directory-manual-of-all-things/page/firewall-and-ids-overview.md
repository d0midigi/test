# Firewall and IDS Overview

Firewalls and IDS Overview

* A firewall is a device that filters network traffic between a “protected” enclave, the internal local area network, and a “less trustworthy” network such as a DMZ, or that houses public-facing and publicly accessible web services and content, or “outside” of the perimeter network segregated away from the internal portion of the LAN.
* A firewall is basically an interface to run executable code on a dedicated software or hardware and can allow or deny various types of network protocols, applications, services, IP addresses (zones and ranges), and more.
* As all network traffic (ingress/egress traffic) should pass through the firewall, it is not a point of contention, or bottleneck, or stop-gap for system performance and hence non-firewall functions are normally not performed on that machine running the firewall. In fact, the dedicated appliance or server hosting the firewalling capabilities should be hardened as much as possible (e.g., remove unnecessary services, accounts, internet access, applications, etc.). Essentially, the platform for which the firewall runs on should just have the firewall suite and nothing else – although critical services pertinent to the appliance’s well-being should be kept (e.g., updating services for patches/hotfixes, etc., but should also be hardened, too).
* Since non-firewall code does not exist in the computer for which the firewall may be installed on, it presents difficulties for a malicious actor to make use of any vulnerability to compromise the firewall.
* Design Ideas:
  * Firewalls implement security policies that are specifically designed to address the allowance or denial of certain activities from executing within its “protected” environment.
  * Security policies that dictate what to allow: Standard security best practices dictate a _**“default-deny”**_ ruleset for firewalls, implying that the only network connections allowed in/out are the ones that have been explicitly allowed or denied.
  * Security policies that dictate what to deny: Users and business entities who lack such a detailed understanding to explicitly state what should be allowed in prefer a _**“default-allow”**_ ruleset, in which all traffic is allowed unless it has been explicitly blocked.
    * Even though this configuration is relatively more prone to inadvertent network connections and system compromise, it is more commonly used because of mere lack of knowledge and new applications that come into existence.
* Not all firewalls are made equal.
* One cannot compare the “goodness” of two firewalls based on the security policies they are configured with.
  * **The key factor that drives the selection of a security policy for a firewall is the threats that an installation (network) needs to avoid happening.**

Packet Filtering Firewalls

* **Packet Filters**
* A packet filtering firewall controls access to network packets on the basis of packet address (source or destination) or specific transport protocol type, such as HTTP, Telnet, etc.
  * **Egress Filtering:** Packets are sent out (or are not to be sent out) only to specific networks and/or belonging to specific transport layer protocols.
  * **Ingress Filtering:** Packets belonging to (not belonging to) only certain source networks and/or specific transport layer protocols are allowed entrance to the network.
* A common strategy to avoid IP spoofing attacks is to have the packet filter configured to not allow packets into the network that have a source address that corresponds to the internal network.
  * In other words, if a malicious actor has spoofed a source IP address and that IP address just so happens to be the IP address of a machine belonging to the internal network being protected by the firewall.
* The code for packet filters will become lengthy as we want to block all traffic belonging to specific networks, IP addresses, and transport layer protocols.

Attacks Prevented Using Packet Filtering Firewalls

* In addition to IP spoofing attacks, packet filter firewalls can be configured to avoid source routing and tiny fragmentation attacks.
* Source routing attacks specify the route that a packet should take to bypass security controls and measures; you should configure your packet filtering firewall to discard all source-related packets.
* Tiny fragment attacks use the IP fragmentation option to create extremely small fragments and forces the TCP header information into fewer separate fragments to circumvent filtering rules needing full header information; you should enforce minimum fragment size to include full headers to thwart this attack.

![](<../.gitbook/assets/0 (29).png>)\
_**FIGURE X:** Layers of the TCP stack supported by Packet Filter and Stateful firewalls._

Packet Filters
