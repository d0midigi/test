# Network Sniffing

Network Sniffing

In this chapter, we will talk about the various techniques used to sniff traffic across a network. To fully understand this chapter, I would recommend you spend some time reading about how _TCP/IP_ works. A majority of the techniques we will discuss in this chapter directly affect the local area network and not across the Internet. Ideally, it’s best if you can position yourself to be inline with your target on the same local network for your attacks to have any chance of success. Sniffing attacks prove useful when you are performing an internal penetration test yet have a limited scope. The only way to make sure your sniffing attacks guarantee success is by compromising a host and then using that compromised host to sniff traffic on its local network; however, this is a more focused area in subsequent chapters and is fits nicer within the context of post-exploitation activities, where we will learn the different techniques used to discover and evade internal network security mechanisms. Sniffing can be performed on both wired and wireless networks. Wired networks, however, is what our main focus will be within this chapter.

The main goal of this chapter is to familiarize the reader with topics that embody sniffing, such as:

* Hubs and switches and how they distribute traffic across the backbone
* ARP protocols weaknesses and general flaws
* Different types of Man-in-the-Middle (MiTM) attacks
* Sniffers and Sniffing Tools
* DNS spoofing via MiTM attack

Introduction

Network sniffing, commonly known as _**packet sniffing, interception, wiretapping,**_ or _**eavesdropping**_, is a type of network-based attack where you position yourself on a target network such that you can intercept and analyze the traffic passing through it while maintaining cover avoiding detection. It is a type of attack wherein your main goal is to capture unencrypted credentials across the network. Commonly targeted protocols that support the sending of cleartext credentials across the wire include FTP, HTTP, and SMTP.

The best way to protect against sniffing attacks is to use protocols that support encrypted communications; therefore, even if an adversary is able to capture traffic details, the captured data would remain useless to the adversary because of its encryption; however, with a little bit of extra time, effort, determination, and some elbow grease, it is possible to sniff traffic from protocols that use encrypted communications, as discussed later in this chapter.

Types of Sniffing

Sniffing can primarily be divided into two main categories, which include _**active**_ and _**passive sniffing.**_

Active Sniffing

Active sniffing is the process of directly interacting with your target(s) information systems and interconnected network(s) by intercepting ingress and egress packets and requests. ARP spoofing and MAC flooding are common examples of attacks that are currently employed in conjunction with a MiTM. Active sniffing is what our focus will be on throughout this chapter.

Passive Sniffing

In passive sniffing, you do not directly have any interactions with your target. Here, you and your sniffer have the chance to sit back on the network while your sniffer captures traversing packets sent and received by the functional network. Such a scenario is most likely to happen in the case of hub-based networks or wireless networks, which will also be discussed in subsequent sections of this chapter.

Hubs versus Switches

To fully comprehend and understand the concept of sniffing travelling packets across a network, you first should have a firm understanding of the difference between hub-based and switch-based networks. Unlike hubs, which operate on the Physical layer (Layer 1 of the OSI Reference model), switches operate mostly at Layer 2 of the OSI model on which almost all modern networks are based and with some smarter switches that function at the Network layer of the OSI model, often referred to as an _**L3 switch.**_

![](<../../.gitbook/assets/0 (54).png>)

Let us assume for a moment that this topology runs on a hub-and-spoke network and that Host A would like to communicate with Host B. Host A will first forward its traffic to the hub. A hub is designed in such a way that it _broadcasts all the traffic,_ meaning that it forwards that traffic to _all hosts directly connected to that network._

Since IP header information contains the destination address of Host B, any other device receiving the frames will simply drop them. The technical flaw in this design, however, is extreme bandwidth utilization which, in turn, creates _**broadcast storms.**_ The security flaw in this design is that an adversary could run a sniffer to capture all of the traffic that is received on their attacking machine as the traffic is broadcasted on a hub-based network.

To mitigate this issues, intelligent switches were introduced. Switches are considered ‘smart devices’ because, unlike hubs, they do not broadcast its traffic to every interconnected node on the network; it simply will forward the frames only to the host for which the traffic is destined for. Switches use the _**Address Resolution Protocol (ARP)**_ to achieve this and will be discussed in more detail in the following sections.

Broadcast Storms

Broadcast storms equate to hell in a handbag – they’re a mess to untangle and can cause quite a chaotic and confusing situation for the network. Imagine broadcast storms as if there were two houses sharing the same address on the same street, and a postal worker has letters intended for “1337 Network Byte Avenue.” What would happen if the postal worker tried to deliver those letters to two separate locations with the exact same address? Utter chaos and confusion would result, much like the situation with a broadcast storm in computer networks.

Broadcast storms arise when a network is inundated with an excessive amount of broadcast packets, often due to loops or flawed configurations, such as discovering two identical IP addresses within the same network. Systems with duplicate IP addresses pose pure hell for network and system administrators, as these machines engage in a competitive struggle for dominance, resulting in both operating in an unstable up/down state until resolved. Observers might notice the network connections icon fluctuating in the taskbar as it attempts to assert control over the competing machine. Analogously, broadcast storms resemble a scenario where multiple residences share the same postal address; the network’s mail carrier, in this context, is tasked with delivering data to a designated location, finds itself perplexed and overwhelmed due to the apparent duplication of the destination address. Consequently, the network is swamped with irrelevant traffic, time and resources are spent, and these effects cause a decline in performance, increased latency, and bottlenecks, which could culminate in complete system failure. As highlighted, broadcast storms have the ability to inflict a considerable amount of turmoil for all parties involved.

To illustrate further, consider a city where two buildings on the same street share the same mailbox number. When a letter arrives and is destined for one of those mailboxes, the delivery person is stuck in a situation wherein they must decide which building to deliver it to, creating uncertainty and inefficiency. Similarly, in a network experiencing a broadcast storm, the routers and switches are flooded with duplicate broadcast frames, leading to congestion and making it difficult for legitimate traffic to reach its intended destination in an efficient manner.

Attackers can exploit broadcast storms to disrupt network services, spread malware, or perform denial of service (DoS) attacks. Because broadcast storms occur when a network receives too many broadcast packets this, in turn, overwhelms the network’s operational capacities and leads to congestion, packet loss, and degraded network performance. Attackers can trigger a broadcast storm by sending spoofed ARP requests or by exploiting misconfigured network settings on devices that respond excessively to broadcasted traffic.

An attacker might use a tool like **Hping3** to flood the network with ARP spoofing packets, which can lead to broadcast storms. A basic example to explicitly induce a broadcast storm using the Hping3 tool can be done as the following:

![](<../../.gitbook/assets/1 (41).png>)

hping3 -At 192.168.1.255 --arp-spoof 192.168.1.100 192.168.1.101

In this command:

* -At targets the broadcast address 192.168.1.255 of the network.
* \--arp-spoof sends ARP spoofing packets to the specified hosts, namely 192.168.1.100 and 192.168.1.101. These packets trick the hosts into believing that the attacker’s machine is just another legitimate host on the network, causing them to send broadcast traffic to the attacker’s machine instead of the actual intended destination.

Scapy

In addition, the tool **Scapy** is a powerful Python library used for network exploration and security auditing purposes. It can be used to craft custom packets, including those that can trigger broadcast storms, such as ARP spoofing packets.

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/2 (36).png>)

from scapy.all import ARP, Ether, srp

def arp\_spoof(target\_ip, gateway\_ip):

target\_mac = getmacbyip(target\_ip)

gateway\_mac = getmacbyip(gateway\_ip)

packet = ARP(op=2, pdst=target\_ip, hwdst=target\_mac, psrc=gateway\_ip, hwsrc=gateway\_mac)

send(packet, verbose=False)

packet = ARP(op=2, pdst=gateway\_ip, hwdst=gateway\_mac, psrc=target\_ip, hwsrc=target\_mac)

send(packet, verbose=False)

arp\_spoof('192.168.1.1', '192.168.1.100')

Nessus

Nessus is a widely-used vulnerability scanner that can identify misconfigurations and vulnerabilities in a network that could be exploited to trigger a broadcast storm.

Wireshark

While not directly used to exploit broadcast storms, Wireshark can be used by adversaries to monitor network traffic and identify vulnerable points that could be exploited to trigger a broadcast storm.

Conversely, defenders can employ several strategies to prevent broadcast storms, such as:

1. **Spanning Tree Protocol (STP):** STP prevents loops in Ethernet networks by disabling certain redundant paths between operational switches. This reduces the likelihood of broadcast storms caused by looping traffic.
2. **Port Security:** By limiting the number of MAC addresses allowed on a switchport, port security can prevent a single port from receiving too much broadcast traffic, thus mitigating the risk of a broadcast storm. Port security also prevents users from BYOD and P2P’ing directly into a network jack.
3. **Rate Limiting:** Implementing rate limiting on network interfaces can control the amount of broadcast traffic that a device can send, preventing a single device from contributing significantly to a broadcast storm.
4. **Virtual Local Area Networks (VLANs):** Segregating network segments into VLANs reduces the scope of a broadcast storm, as broadcasts are limited to the VLAN in which they originate.
5. **Proper Configuration:** Ensuring that network devices are correctly configured and hardened, especially regarding ARP and routing tables, can prevent misconfigurations that lead to broadcast storms.
6. **Monitoring and Alerts:** Regularly monitoring network traffic and setting up alerts to trigger unusual pattern detection and identification, such as sudden spikes in broadcast traffic, can also help detect and mitigate broadcast storms early.

**Preventing Loops in Ethernet Networks with the Spanning Tree Protocol (STP)**

The Spanning Tree Protocol (STP) is designed to prevent loops in Ethernet networks by ensuring that only one path exists between any two nodes. It achieves this by dynamically blocking redundant paths based on the network topology. When STP detects a loop, it disables some of the links in the network to break the loop, thereby preventing broadcast storms caused by looping traffic.

STP operates by electing a _**root bridge**_ within the network, which is the reference point for all spanning tree calculations. Each switch calculates the shortest path to the root bridge and blocks all other paths to ensure that only the shortest path is active. If a change in the network topology requires reevaluation of the spanning tree, STP will recalculate the shortest paths and update the network accordingly.

Common Signs a Network is Experiencing a Broadcast Storm

1. **High Network Traffic:** An unusually high volume of broadcast traffic, often exceeding normal levels by the order of magnitude.
2. **Packet Loss:** Increased packet loss, indicating that the network is struggling to handle the volumes of traffic.
3. **Network Performance Degradation:** Slower network speeds and longer response times, as the network resources are consumed by handling the excess broadcast traffic.
4. **Device Overheating:** Network devices may become overheated due to increased processing demands, potentially leading to hardware failures.
5. **Unresponsive Devices.** Some devices on the network may become unresponsive altogether or disconnect from the network entirely due to the overwhelming broadcast traffic.
6. **Repeated Broadcast Messages:** Seeing the same broadcast message repeated over and over again, which is a clear sign of a broadcast storm.

Promiscuous Mode versus Nonpromiscuous Mode

Before we try to sniff traffic on a network, we need to understand the difference between what a switch in promiscuous mode versus nonpromiscuous mode entails. These two modes are associated with using a device’s network interface card (NIC) and, by default, NICs are shipped in the nonpromiscuous mode, in which we will be able to capture only the traffic that is destined for our computer; however, we can change our NIC to operate in promiscuous mode, which will essentially allow us to forcefully, or brute-force capturing of the network traffic that is not destined for our machine. So, rule number 1 for sniffing is to ensure that the NICs in which you will be working with are operating in promiscuous mode.

Man-in-the-Middle (MiTM) Attacks

The idea behind a MiTM attack is that the adversary places themselves in the middle of the communication stream between a client and a server; therefore, any communications that are being performed between the client and the server will be captured by the adversary. Once the adversary successfully becomes the man in the middle, attacks of many kinds can be employed such as intercepting and capturing all the ingress/egress traffic, denial of service (DoS) attacks, DNS spoofing, ARP poisoning, redirection, IP spoofing, impersonation, packet header manipulation, and session hijacking to name a few.

ARP (Address Resolution Protocol) Basics

ARP stands for Address Resolution Protocol and operates within the Data Link layer (Layer 2) of the OSI Reference model. Its purpose is to _resolve an IP address to a MAC address._ Any piece of hardware that connects to the Internet has a unique MAC address, and like an IP address, is akin to a home address: it is unique to the home to which it is assigned, and it never changes.

How ARP Works

![](<../../.gitbook/assets/3 (26).png>)

So, let’s for a minute imagine a scenario shown in the image above, where on a switch-based network, Host A with an IP address of 192.168.1.2 would like to communicate with host B with an IP address of 192.168.1.3. To communicate in a local area, Host A would need to have the MAC address of Host B.

Host A will look inside its ARP cache and see if the entry for Host B’s IP address is present within its ARP table. If it’s not present, Host A will send an ARP broadcast packet to every device on the network asking, _“Who has Host B’s IP address?”_

Once Host B receives the ARP request, it will send an ARP reply by telling Host A _“I am Host B and here is my MAC address.”_ The MAC address would then be saved inside the ARP table. An ARP cache contains a list of the IP and MAC addresses of every host we have communicated with, including devices that were once online now in an offline state.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/4 (29).png>)

ARP Attacks

There are two main types of attack vectors that could be leveraged to employ ARP attacks:

* MAC Flooding
* ARP Poisoning, or ARP Spoofing

MAC Flooding Attack

Here, we will discuss MAC flooding first, as in my humble opinion, it is easier to explain. The idea behind a MAC flooding attack is to send a huge amount of ARP replies to a switch, thereby overloading the CAM table of the switch. Once the switch overloads, it goes into dumb hub mode (yes, it is really called that) meaning that it will forward the traffic to every single computer on the network. All the attacker needs to do now is run a sniffer to capture all the traffic. This attack does not work for every switch; newer switches are now shipped with built-in protection against this type of attack.

Macof

Macof is part of the dsniff series of tools, which I will demonstrate once we get to the ARP spoofing section. Macof fills the CAM table in less than a minute or so, since it sends a huge number of MAC entries – almost 155,000 per minute, to be specific.

Usage

The usage of the Macof tool is extremely simple. All we need to do is execute “macof” command from our terminal. Take a look at the following screenshot below:

![Bahman Alasgarov on LinkedIn: The example shows a sample output of the macof  command on a Linux…](<../../.gitbook/assets/5 (25).png>)

Once the CAM table has been flooded, we can open Wireshark and start sniffing and capturing the traffic. By default, Wireshark is set to capture traffic in the promiscuous mode; however, you don’t need to sniff while in promiscuous mode when a switch goes into dumb hub mode since the traffic is already promiscuous.

ARP Poisoning

ARP poisoning is a very popular attack and can be used to intercept communications. This can be achieved by sending fake “ARP replies.” As discussed earlier, the ARP protocol always trusts that the reply is coming from a legitimate device. Due to this flaw in its design, it can in no way verify that the ARP reply was sent from the legitimate, correct devices.

The way it works is that you send a spoofed ARP reply to any computer on a network to make it believe that a certain IP is associated with a certain MAC address of a certain device, thereby poisoning its ARP cache that keeps tract of IP-to-MAC addresses.

![A diagram of a computer network

Description automatically generated](<../../.gitbook/assets/6 (28).png>)

Let’s have a look at the scenario presented in this image. The hacker sniffs all the traffic using the ARP spoofing attack. We have a switch with the IP of 192.168.1.2. We have two hosts, namely, ‘bob,’ with the IP address 192.168.1.3 and ‘alice’ with the IP address 192.168.1.4. The attacking computer located on the network has the IP address of 192.168.1.10.

To launch an ARP spoofing attack, you essentially send two spoofed ARP replies. Your first reply will be sent to ‘alice’ telling ‘bob’ that ‘alice’ is at the MAC address of the attacking machine, which is ‘bb.bb.bb.bb,’ so now all communications going from ‘bob’ to ‘alice’ will be forwarded to the attacking machine. Now, you will need to send a spoofed ARP reply to ‘alice,’ as well telling that ‘bob’ is located at the attacking machine’s MAC address, since he wants to sniff the traffic going from ‘alice’ to ‘bob’ as well. So, through ARP spoofing, you now find yourself as the man in the middle, sniffing traffic between the two hosts.

Denial of Service (DoS) Attacks

Another attack that is possible with ARP spoofing is a _**denial of service (DoS) attack.**_ This attack works by associating the victim router’s IP address to an IP address that simply does not exist, thereby denying the victim access to the Internet and local network resources: when the victim tries to connect to the Internet, they will reach a nonexistent place. The bit bucket. The attack is performed by sending spoofed ARP replies to the victim’s router’s MAC address that does not exist. Again, in a real penetration testing environment, you would rarely perform these types of attacks, as you will be more focused on launching the ARP spoofing attack.

Tools of the Trade

Now, let’s talk about some of the popular tools we have at our disposal and ones that can be used to perform MiTM attacks.

Dsniff

Dsniff is versatile command-line ARP spoofing suite of tools and includes many tools to sniff various types of network traffic. The most popular of them is ARP spoof, which will be demonstrated next. The Dsniff project is currently abandoned, so does not actively receive updates nor does it have a technical support staff; however, given the tools capabilities, I find that the tool still works as intended and is great for performing Man-in-the-Middle (MiTM) attacks.

This suite includes the following tools:

* **arpspoof:** Used for poisoning the ARP cache by forging ARP replies
* **mailsnarf**: Used to sniff email messages sent from protocols like SMTP and POP
* **msgsnaf**: Sniffs all instant messaging conversations
* **Webspy**: Used to sniff all the URLs that a victim has visited
* **urlsnarf**: Sniffs all visited URLs
* **macof**: Used to perform a MAC flooding attack

Using the ARP Spoof Tool to Perform MiTM Attacks

Before we perform a man-in-the-middle attack, we need to enable IP forwarding so that the traffic could be forwarded to the destination correctly. To enable it, you can use the following command:

echo 1 >/proc/sys/net/ipv4/ip\_forward

We can confirm that port forwarding is enabled by using the cat command to display the contents of the ip\_forward file. “1” means that IP forwarding is enabled; “0” means it is disabled.

![](<../../.gitbook/assets/7 (26).png>)

Now that we have enabled IP forwarding, we need to gather the following information to perform our man-in-the-middle attack:

1. Attacker’s IP address
2. Victim’s IP address
3. Default gateway

* **Attacker’s IP address:** This will be the IP address of my BackTrack machine, which is 192.168.75.138.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/8 (21).png>)

* **Victim’s IP address:** My victim machine has an IP address of 192.168.75.142 (also router address).

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/9 (21).png>)

* **Default gateway:** The default gateway is the IP address of my router, which is 192.168.75.142. Next, we would take note of the victim’s MAC address associated with each of them. We can view the MAC addresses in the ARP cache by running the arp -a command in the Windows command-line interface (CLI) or PowerShell terminal.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/10 (18).png>)

From this ARP cache, we can see that we have the MAC address of the default gateway (192.168.75.2) and our machine (192.168.75.138). Our goal is to tell the default gateway that the victim’s IP address is associated with our MAC address and vice versa.

Let’s try the tool arpspoof to get this job done.

Usage

The basic syntax for arpspoof is as follows:

arpspoof -i \[Interface] -t \[Target Host]

In this case, our interface is eth0, and our targets are 192.168.75.2 (the gateway) and 192.168.75.142 (the victim). So, our full command would be as follows:

arpspoof -i eth0 -t 192.168.75.142 192.168.75.2

![](<../../.gitbook/assets/11 (17).png>)

* -i eth0 specify the network interface for sniffing and arpspoofing.
* -t target denotes the target IP address.
* 192.168.75.142 is the victim’s IP address.
* 192.168.75.2 is the default gateway IP address.

Note: If conducting this MiTM attack on a wireless network, replace -I eth0 with -I wlan0.

On taking a look at the ARP cache again, we find that our gateway MAC address has been replaced with our MAC address. So, anything that the victim sends to the gateway will be forwarded to us from now on.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/12 (21).png>)

We also need to issue the same command in a reverse manner because when we are in the middle, we need to send ARP replies both ways.

arpspoof -i eth0 -t 192.168.75.2 192.168.75.142

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/13 (17).png>)

If we take a look at the ARP cache of the victim’s machine now, we will find our MAC address associated with both IP address (the default gateway and the victim).

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/14 (17).png>)

Sniffing Network Traffic with Dsniff

We have successfully poisoned the ARP cache; now, let’s explore a couple of sniffers that capture network traffic. Our first stop is dsniff, a versatile command-line sniffer often described as a “Swiss army knife” for network monitoring.

To use dsniff, simply type ‘dsniff’ into your terminal. This command is designed to intercept and capture any plaintext passwords transmitted over the network. For instance, while dsniff was running, I accessed an FTP account. Since FTP uses plaintext protocols, dsniff was able to capture my login credentials.

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/15 (17).png>)

Sniffing Images with Driftnet

If our objective is to monitor what the victim is viewing in their web browser, we have a powerful tool at our disposal named driftnet, which conveniently comes pre-installed with the BackTrack Linux OS, another popular penetration testing distro. Driftnet allows us to capture and view all the images that the victim browses through, providing insight into their online activities.

Driftnet Use Case:

The difficulty intensifies when aiming to inspect pictures, photographs, JPEGs, PNGs, and other graphical files within this traffic flow. Despite observing that these images and other graphic files traverse the network or airwaves, deciphering their content remains elusive.

Suppose our objective is to determine if an individual we suspect of espionage for a foreign government is transmitting or receiving covert images via their computer These images could encompass sensitive information such as maps, schematics, proprietary knowledge, spy photos, and more, all of which contain confidential details critical to national security. How might we proceed?

Initially, we must intercept the target’s traffic by positioning ourselves between the target and their router. This setup ensures that all the internet-bound traffic passes through us first. Following this, we employ the driftnet yet again to detect, capture, and reconstruct these images obtained via the network traffic. Driftnet saves these images to our local storage and displays them on our screen as it would with any graphical file.

Launching Driftnet

To use the driftnet tool, you would execute the following command in the terminal:

driftnet

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/16 (18).png>)

Notice that when we do this, a small window opens below our terminal. In my case here, it opened in the lower left hand, but it may open on any free screen real estate that is available. Maximize the driftnet window as this is where driftnet displays the images it finds and reconstructs.

From this point forward, any Internet traffic sent or received by our victim will pass through our system, allowing us to filter, reconstruct, view, and save the images contained within.

As we await the moment our victim accesses the Internet, we remain vigilant. Sooner than later, images will start appearing in the driftnet window on our screen.

![A collage of a person with a beard

Description automatically generated](<../../.gitbook/assets/17 (16).png>)

It seems our victim has a keen interest in sports, as evidenced by their visit to www.espn.com, where the driftnet application successfully captured and displayed the images from the victim’s browsing session. While this activity might seem benign to some, it doesn’t rule out the possibility of illicit activities; therefore, we’ll keep driftnet operational to continue capturing images as our victim navigates the internet or transfers files.

Locating Saved Images via Driftnet

Even though the initial batch of images appears harmless, we might still wish to archive them for closer inspection. Moreover, maintaining our Man-in-the-Middle (MiTM) position and keeping driftnet active ensures continuous surveillance of incoming messages.

Returning to the driftnet command terminal reveals that driftnet indicates the storage location of the captured images.

Driftnet typically saves images to the /tmp directory within a randomly generated subdirectory, often misspelled (e.g., drifnet instead of drif**t**net). This quirk can occasionally lead to confusion.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/18 (16).png>)

To locate the images, ensure that you replicate the spelling mistake in the directory name. Navigate to the specified directory to review what driftnet has captured and stored:

![](<../../.gitbook/assets/19 (14).png>)

Within moments, driftnet has amassed a collection of images, primarily JPEGs and GIFs, but it’s capable of capturing and reconstructing a variety of file formats, including MPEG videos and audio files.

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/20 (10).png>)

Driftnet Verbose Mode

To run driftnet in verbose mode, simply run: driftnet -v. This command enables driftnet to capture and display images from the network traffic passing through the machine where it’s run. By doing so, it essentially gives us a glimpse into the victim’s browsing history, specifically the images they’ve viewed, which can be invaluable for reconnaissance purposes in a penetration testing scenario.

Using Driftnet and MiTM to View Target’s Graphic Files

Throughout our prior Man-in-the-Middle (MiTM) attacks, we’ve successfully positioned ourselves between two users to observe their communications. This interaction can be monitored using tools like **Wireshark** and other packet sniffing utilities. As demonstrated below, Wireshark provides a comprehensive breakdown of each packet transmitted across the network. Utilizing Wireshark, we’re capable of capturing these packets for thorough examination at a later time.

When applying the Wireshark filter for “HTTP,” we’re able to focus solely on HTTP traffic passing through, which includes packets containing images; however, the challenge arises when attempting to view or reconstruct these images, as they frequently span across multiple packets, making direct visualization impossible.

\
urlsnarf and Webspy

Urlsnarf and Webspy are components of the dsniff toolkit, designed for capturing and analyzing network traffic. Urlsnarf specifically monitors and logs the URLs visited by a target, providing insights into their browsing habits. On the other hand, Webspy goes a step further by actively opening the webpages that the target has visited directly in the attacker’s browser.

For instance, an attacker could use urlsnarf to monitor the URLs accessed by a victim. Similarly, Webspy can replicate the victim’s browsing experience by displaying the webpages they’ve visited. To use Webspy, you must specify additional parameters, such as the network interface and the victim’s IP address. To run Webspy using the victim IP address, run this command:

In this command, -i eth0 specifies the network interface, and 192.168.75.142 is the IP address of the victim. With this setup, Webspy will attempt to replicate the victim’s browsing session, mirroring webpages they access in near-real-time.

As urlsnarf tracks the URLs visited by the victim, it alerts the attacker whenever the victim navigates toa new webpage. This real-time tracking allows the attacker to stay informed about the victim’s current online activities. For example, if the victim visits www.facebook.com, urlsnarf would notify the attacker, and Webspy could then automatically open Facebook in the attacker’s browser, mirroring the victim’s browsing session accurately.

Sniffing with Wireshark

If you explored Chapter 3 titled “Networking Concepts 101,” you’ll recall seeing Wireshark in action, where I illustrated the TCP/IP Three-Way Handshake and the processes of port scanning. Originally known as _**Ethereal**_, Wireshark stands out as one of the premier packet sniffers and protocol analyzers available. Its utility extends beyond the realm of hackers and penetration testers, serving network administrators in diagnosing network issues. Given its comprehensive nature, it’s impractical to cover every facet of Wireshark in this chapter; nonetheless, I’ll provide a concise introduction.

Our aim here is to use Wireshark to intercept plaintext passwords transmitted over the network. Let us proceed:

**Step 1:** Launch Wireshark by typing Wireshark in the terminal. Upon launching, click the “Capture” button at the top and then click on the “Analyze” button.

**Step 2:** Choose the network interface you wish to monitor and click “Start;” in this example, it is a Cisco AnyConnect VPN Virtual Miniport Adapter for Windowsx64.

**Step 3:** Wireshark will begin recording all passing network traffic. On the victim’s machine, I’ll log into a website that employs HTTP authentication, and I’ll attempt to halt the capture on my machine once the login is successful.

**Step 4:** Given the volume of packets, we need to instruct Wireshark to filter for only HTTP POST requests. In the filter tab, enter: http.request.method==POST

Upon inspection, the initial request observed is a “POST” request directed to the destination 75.98.17.25 from our victim, whose source IP is 192.168.75.142.

**Step 5:** Right-clicking on the packet and selecting “Follow TCP Stream” reveals the original POST request made by the victim’s browser. The output displays the username “admin” and the password “pass.”

Wireshark offers a variety of filters to sift through different types of traffic, some of which we’ve discussed. For a deeper dive into Wireshark’s capabilities, I recommend consulting the official Wireshark manual available at www.wireshark.org.

**Step 1: Employing arpspoof for Positioning**

For placing ourselves right in the middle, we’ve utilized both arpspoof and MiTM attacks. Either tool can serve this purpose, though for simplicity and brevity, we’ll use arpspoof in this section.
