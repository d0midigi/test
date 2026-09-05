# Distributed Denial of Service (DDoS) Attacks

A Distributed Denial of Service (DDoS) attack constitutes a nefarious endeavor to disrupt the regular flow of network traffic to a designated server, service, or network by inundating it or its adjacent infrastructure with an excessive volume of Internet traffic. The attackers’ goal is to inundate the target with an overwhelming volume of traffic, thus depleting its resources and leading to either a total or partial suspension of the provided service(s).

DDoS assaults capitalize on numerous compromised malware-infested computer systems, employing them as sources of attack traffic. These exploited machines encompass computers as well as other networked resources like IoT (Internet of Things) devices.

At its essence, a DDoS attack mirrors an unforeseen traffic bottleneck on a highway, impeding the smooth progression of regular traffic towards its intended endpoint/destination.

![DDoS attack traffic metaphor](<../.gitbook/assets/0 (21).png>)\
_**FIGURE X:** Illustration depicting traffic impeding the regular smooth progression of traffic._

**Instant Consequence**

The immediate aftermath of DDoS attacks can be quite damaging, as they can instantly halt service, leaving the targeted system unreachable to authorized users.

Importance of Quick Response

It’s imperative to have efficient defenses against DDoS attacks, as the speed at which an attack is detected and responded to plays a critical role in minimizing its effects.

Employing DDoS Hit-and-Run Tactics

Often, DDoS attacks are launched against targets hosted on networks vulnerable to hit-and-run tactics, designed to cause the greatest possible damage in the shortest time frame before you vanish.

Distributed Denial of Service, or DDoS, attacks, particularly those employing hit-and-run tactics, pose the greatest threat to internet infrastructure and services. These attacks are characterized by their brevity and intensity, designed to inflict maximum damage in the shortest amount of time possible before you disappear, leaving minimal traces for cyber investigators to follow.

How Hit-and-Run DDoS Attacks Work

Most successful human-and-machine coupled attacks usually involve a Command and Control (C2, or CC, or C\&C) infrastructure; therefore, a hit-and-run DDoS attack leverages a network of compromised devices, known as a botnet, consisting primarily of Internet of Things (IoT) devices and gadgets, websites, and computers. The botnet is programmed to send rapid, intense waves of bunk network traffic to the target, overwhelming its server, network, and application resources. This onslaught aims to exhaust the target’s capacity, rendering it incapable of handling legitimate traffic, whether it’s serving webpages, processing transactions, or facilitating communications. The result ends up being a denial of service to the users, leading to financial losses and operational disruptions.

Goals Behind Hit-and-Run DDoS Attacks

The primary objective of a hit-and-run DDoS attack is to temporarily disable a service or server without drawing prolonged attention to the attacker. By launching brief, high-volume assaults at irregular intervals or over a period of days or weeks, the attacker seeks to maximize disruption while minimizing the likelihood of being traced or caught. This tactic allows them to achieve their goal of preventing users from accessing a service without engaging a sustained campaign that might alert defenders or attract investigative scrutiny.

Distinction from Persistent DDoS Attacks

Unlike Persistent DDoS attacks, which continue unabated until the attacker decides to stop, or the target successfully defends itself, hit-and-run attacks are transient. They are designed to strike quickly and then vanish, leaving little evidence for forensic analysis. This makes hit-and-run DDoS attacks particularly challenging to defend against, as they require rapid detection and mitigation capabilities to minimize the impact before they disappear.

Implications and Countermeasures

The implications of hit-and-run DDoS attacks are profound, affecting not only the immediate availability of services but also the long-term trust and reliability of online platforms. To counter these attacks, organizations must invest in advanced detection and mitigation technologies, such as Network Behavioral Anomaly Detection (NBAD), which can identify unusual patterns indicative of DDoS activity. Additionally, implementing proactive defense strategies, including traffic shaping and policy-based filtering, can help distinguish between legitimate and malicious traffic, reducing the effectiveness of hit-and-run attacks.

In conclusion, hit-and-run DDoS attacks represent a sophisticated and elusive form of cyber aggression, designed to exploit vulnerabilities in internet infrastructure and services. Understanding their modus operandi and investing in robust defense mechanisms are crucial steps toward protecting against these and similar threats.

**What is a Command and Control (C2) Infrastructure?**

Command and Control (C2, CC, or C\&C) infrastructure is a system used by cybercriminals to manage and control malware-infected devices, often referred to as _“bots,”_ or _“zombies,”_ within a botnet (more than one bot). This infrastructure serves as the communications hub through which a cybercriminal, or _“bot herder/master,”_ sends instructions to their malware and receives data from infected devices. It is crucial for coordinating malicious human-to-machine coupled-related activities such as launching DDoS attacks, stealing data, spreading malware, and other cybercrimes.

The primary components of C2 infrastructure include command servers and communications channels. Command servers are split into primary and backup servers. **Primary command servers** are the main server that issue commands to the infected devices and are typically well-hidden and protected to avoid detection. **Backup command servers** act as redundant servers that take over if the primary servers are discovered and burned down. Communications channels between the bots and the command servers can vary. Common channels include HTTP/HTTPS, which is often used for covert communications channels as it blends in with regular, innocuous network and web traffic, IRC (Internet Relay Chat), a traditional method where bots connect to an IRC server to receive commands, and Peer-to-Peer (P2P), a decentralized communications method that is harder to disrupt due to its lack of a single point of failure. DNS (Domain Name System) can also be used, leveraging the domain name system to send commands or receive data, helping the malware evade detection.

The process of a C2 infrastructure operation begins with **infection,** where malware infects a device, turning it into part of the botnet. The infected device, or bot/zombie, then connects to the C2 server, often using an encrypted communications channel to avoid detection and evade security mechanisms. The C2 server sends commands to the bot, directing it to perform specific tasks, such as exfiltrating data, launching DDoS attacks, or spreading the infection to other vulnerable, unprotected devices. The bot then executes these commands and sends the results back to the C2 server, which may include stolen data or success/failure reports of specific actions sent by the bot herder to be executed by the bots, or botnet.

C2 infrastructure is used for various malicious purposes. It can coordinate Distributed Denial of Service (DDoS) attacks by managing thousands or millions of infected devices to flood a target with bullshit meaningless network traffic. Does nothing but clog up the pipes and makes us frustrated. It can also be used for data theft, with a bot master directing bots to collect and send back sensitive information like passwords, credit card numbers, or proprietary data. Additionally, it can facilitate spam campaigns by using bots to send large volumes of spam email to random users, or cryptojacking by leveraging the computational power of infected devices to mine cryptocurrencies. Ransomware attacks are also managed through C2 infrastructure, including the distribution of ransomware and communications with infected users for ransom payments.

Detection and mitigation of C2 infrastructure, when used maliciously, can involve several strategies. Network traffic analysis is crucial for monitoring unusual patterns or baselines of network traffic activities or volumes of network traffic, such as sudden network spikes every 10 m minutes, may indicate communications with C2 servers. Anomaly detection can identify deviations from normal network behaviors. Threat intelligence feeds, such as CybserSixGill, provide threat intel and information about known C2 servers and domains, enabling the blocking of malicious IP addresses and domains at the network perimeter. Endpoint Detection and Response (EDR) solutions can also detect and respond to malicious activities on endpoints, conducting regular scans for malware and suspicious activities. Deception technologies, such as honeypots, bait and lure, and decoys, can attract and monitor malicious activities, providing great insights into the different ways in which one can control at C2 server. Collaboration with law enforcement agencies is also essential to take down C2 servers and disrupt botnet operations given the severity that these infrastructures can impose on any given networked entity.

![](<../.gitbook/assets/1 (11).png>)![](<../.gitbook/assets/2 (11).png>)![](<../.gitbook/assets/3 (11).png>)![](<../.gitbook/assets/4 (10).png>)![](<../.gitbook/assets/5 (10).png>)![](<../.gitbook/assets/6 (10).png>)![](<../.gitbook/assets/7 (9).png>)![](<../.gitbook/assets/8 (9).png>)![](<../.gitbook/assets/9 (9).png>)

![](<../.gitbook/assets/10 (9).png>)

**Note:** Detecting a C2 server can involve checking DNS query logs for communications with known malicious domains. A Python script can automate the process, scanning the logs for any indications of interaction with suspicious domains. This kind of proactive monitoring helps you to identify and address potential threats within networks.

![](<../.gitbook/assets/11 (8).png>)![](<../.gitbook/assets/12 (8).png>)![](<../.gitbook/assets/13 (8).png>)![](<../.gitbook/assets/14 (8).png>)![](<../.gitbook/assets/15 (8).png>)

Command and Control infrastructure is a critical component in the operation of botnets and other forms of malware. Understanding this infrastructure is essential for knowing how to detect, respond, mitigate, and recommend mitigations from the impact of cyber threats, safeguarding network integrity, and protecting sensitive information from cybercriminals.

### How DDoS Attacks Work

DDoS attacks leverage interconnected networks of Internet-connected machines, including infected computers and devices like IoT gadgets, which have been compromised by malware sometimes unbeknownst to the user. These compromised devices, often referred to as _“bots,”_ or _“zombies,”_ collectively form a _“botnet.”_

Once a botnet has been established, you are effectively able to control each bot, enabling them to orchestrate an attack by issuing instructions remotely.

During an attack, each bot within the botnet inundates the targeted server or network with requests directed at its IP address. This onslaught can overwhelm the server or network, resulting in a disruption of normal traffic, effectively causing a denial of service.

The challenge in mitigating DDoS attacks lies in distinguishing between the attack traffic generated by the botnet and legitimate traffic, as each bot appears to be a genuine Internet-connected device.

### How to Identify a DDoS Attack

The primary indication of a DDoS attack is a sudden slowdown or unavailability of a site or service; however, as various factors, including legitimate increases in network traffic, can cause similar performance issues, further investigation becomes necessary on your part. Traffic analytics tools play a crucial role in identifying potential signs of a DDoS attack:

1. Unusual amounts of traffic originating from a single IP address or IP range.
2. A surge in traffic from users who share common behavioral traits, such as device type, geolocation, or web browser version.<br>
3. An unexpected increase in requests directed towards a specific page or endpoint.<br>
4. Abnormal traffic patterns that deviate from the norm, such as spikes occurring at odd times of the day or patterns that seem unnatural (e.g., a spike in traffic every 10 minutes).

Moreover, there are additional, more specialized indicators of a DDoS attack that may vary depending on the specific type of attack being initiated and launched.

### Common Types of DDoS Attacks

To comprehend the workings of different DDoS attacks, it’s beneficial to understand the structure of a network connection first. Internet connections are composed of various components, or “layers,” each serving a specific purpose, akin to constructing a house from the ground up.

The OSI (Open Systems Interconnection) model provides a conceptual framework delineating network connectivity into seven distinct layers. These layers, depicted below, facilitate communications between devices on a network by defining standardized protocols and functions for each tier:

![The OSI model 7 layers: application, presentation, session, transport, network, data link, physical](<../.gitbook/assets/16 (8).png>)\
_**FIGURE X:** Illustration depicting the OSI (Open Systems Interconnection) model: a conceptual framework governing protocols for network communication flows._

DDoS attacks are commonly categorized into three types: Application-Layer attacks, IP or Protocol-based attacks, and Volumetric attacks, each with distinct characteristics and objectives. Hackers may employ one or multiple attack vectors or adapt their tactics in response to countermeasures implemented by the target. HTTP Floods are another variant of DDoS you can include within this list and for which we will discuss later in this section.

### Application-Layer Attacks

**Objective**

These attacks, also known as Layer 7 DDoS attacks (referring to the 7th layer of the OSI model, the Application Layer) aim to overwhelm the target’s resources to induce a denial of service.

**Target**

The attack focuses on the layer responsible for generating web pages on the server and delivering them in response to HTTP requests.

**Method**

While individual HTTP requests are relatively inexpensive to execute on the client-side, they can impose significant computational load on the target server. This is because the server often needs to load multiple files and execute database queries to generate a complete web page.

**Challenge**

Layer 7 DDoS attacks pose a challenge for defense mechanisms due to the difficulty in distinguishing between malicious and legitimate network traffic.

![A diagram of a computer system

Description automatically generated](<../.gitbook/assets/17 (7).png>)\
_**FIGURE X:** Illustration depicting an application layer attack._

### Leveraging an Application Layer-based DDoS in Ethical Hacking

As an ethical hacker, you can leverage Application Layer-based DDoS attacks to evaluate the effectiveness of your target organization’s defenses against such threats. Here is how you can do so:

1. **Simulating Attack Scenarios**\
   You can simulate various application layer DDoS attack scenarios, such as HTTP floods or a Slowloris attack, to assess the target’s web applications or services’ resilience. By overwhelming the applications with a high volume of requests, you can better determine how they respond under stress and whether they are susceptible to denial-of-service

attack conditions.<br>

1. **Testing Load Balancers and Web Application Firewalls (WAFs)**\
   You can test the effectiveness of load balancers and WAFs in mitigating application layer DDoS attacks. By bypassing or evading these security measures and successfully overloading the target applications, you can identify weaknesses in the organization’s defense mechanisms and recommend vast improvements.
2. **Analyzing Response Mechanisms**\
   You can analyze how your target’s applications respond to different types of DDoS attacks and monitor for error codes, certain server responses, and application behaviors during an active ongoing attack. This analysis can provide insights into the effectiveness of the target’s mitigation strategies.

### Volumetric Attacks

Volumetric DDoS attacks aim to disrupt the availability of online services by flooding the target’s network infrastructure with an overwhelming volume of traffic. The primary objective is to exhaust the target’s network bandwidth, rendering it incapable of processing legitimate requests and using a denial-of-service condition. By saturating the target’s network resources, hackers can seek to disrupt operations, inflict financial losses, and damage the reputation of the targeted organization.

**Target**

The targets of volumetric DDoS attacks include various network components such as routers, switches, firewalls, and servers. Additionally, specific services or applications hosted on the target’s infrastructure may be targeted, including web servers, email servers, DNS servers, and online gaming platforms. Hackers may select targets based on their strategic value, perceived vulnerabilities, or the potential impact of disruption on the target’s operations and stakeholders.

![A diagram of a system that has a number of objects on it

Description automatically generated](<../.gitbook/assets/18 (7).png>)\
_**FIGURE X**: Illustration depicting a volumetric DDoS attack._

**Method**

Volumetric DDoS attacks leverage botnets, which are networks of compromised devices under the control of the hacker, or “bot herder.” These botnets are orchestrated to generate and transmit a massive volume of innocuous network traffic to the target, overwhelming its network infrastructure. Hackers can employ various techniques to amplify the volume of the attack traffic, including reflection and amplification attacks.

#### Reflection Attacks

In reflection attacks, the hacker spoofs the source IP address of the network traffic to appear as if it originates from the target, causing intermediary servers to send responses back to the target, amplifying the volume of traffic.

#### Amplification Attacks

Amplification attacks aim to exploit protocols that allow for small requests to generate large responses, such as DNS amplification, or NTP amplification, magnifying the impact of the attack.

### Hyper-Volumetric DDoS Attacks

A hyper-volumetric DDoS (Distributed Denial of Service) attack is a type of cyberattack aimed at overwhelming a network, service, or server with a massive amount of traffic. The goal is to consume all available bandwidth, processing power, or other resources, rendering the target unable to respond to legitimate requests. These attacks utilize a large number of compromised systems, often part of a botnet, to generate an enormous volume of traffic. The sheer scale of these attacks can cripple even the most resilient infrastructures, making them a significant threat.

Performing a UDP Flood Attack

This Python script performs a UDP flood attack, sending a large number of UDP packets to the target IP address and port.

### Leveraging Volumetric DDoS in Ethical Hacking

Ethical hackers can leverage their expertise to assist organization’s in mitigating the risks posed by volumetric DDoS attacks. By simulating volumetric attacks in controlled environments, you can identify vulnerabilities in the target’s network infrastructure and assess the effectiveness of existing DDoS protection mechanisms. Through penetration testing and vulnerability assessments, you can evaluate the resilience of the target’s defenses against volumetric DDoS attacks and recommend mitigation measures to enhance security posture. Additionally, you can provide guidance on implementing network security best practices, such as deploying load balancers to distribute malicious traffic, Intrusion Detection and Prevention Systems (IDS/IPS), and traffic filtering mechanisms, to mitigate the impact of volumetric DDoS attacks and to help your client safeguard against future threats.

### Protocol Attacks

Protocol attacks, often referred to as _“state-exhaustion attacks,”_ represent a sophisticated strategy within the realm of cyber warfare, designed to inflict service disruptions by relentlessly consuming server resources as well as the resources of network infrastructure components like firewalls and load balancers.

These attacks strategically exploit vulnerabilities inherent in Layers 3 (network layer) and 4 (transport layer) of the OSI stack, the backbone of network communications. By targeting these layers, protocol attacks aim to undermine the very foundation of digital connectivity, rendering the intended target unreachable and susceptible to crippling downtime.

![DDoS Protection: 8 Simple Tactics](<../.gitbook/assets/19 (5).png>)\
_**FIGURE X:** Illustration depicting a protocol attack._

At the heart of protocol attacks lies a calculated exploitation of the intricacies of networking protocols, such as the Internet Protocol (IP) at Layer 3 and the Transmission Control Protocol (TCP) or User Datagram Protocol (UDP) at Layer 4. By overwhelming these layers with an onslaught of malicious traffic, hackers can disrupt the normal flow of communications between devices, effectively severing the connections between the target and its users.

Unlike application layer attacks, which focus on inundating specific services or applications with a barrage of requests, protocol attacks operate at a deeper level, aiming to exhaust the underlying infrastructure itself. The distinction underscores the strategic intent of protocol attacks: to destabilize the very framework upon with digital communications relies, rather than merely disrupting individual services or applications.

Moreover, protocol attacks pose a formidable challenge for defenders due to their nuanced nature and the critical role played by Layers 3 and 4 in facilitating network communications. As attack strategies and tactics continuously evolve, security defenders and offenders must remain vigilant and employ robust mitigation and/or attack strategies to safeguard/penetrate the security layers and the pervasive threat posed by protocol attacks.

In essence, protocol attacks represent a sophisticated form of cyber assault, leveraging vulnerabilities in core networking protocols to disrupt digital connectivity and inflict widespread service disruptions. By exploiting weaknesses in Layers 3 and 4 of the OSI stack, these attacks underscore the ever-present need for proactive cybersecurity measures and vigilant defense strategies in an increasingly interconnected digital landscape.

### Leveraging Protocol-Based DDoS in Ethical Hacking

1. **Assessing Network Infrastructure**\
   Ethical hackers can assess the target organization’s network infrastructure for vulnerabilities that could be exploited in protocol-based DDoS attacks, such as SYN floods or UDP amplification attacks. By analyzing how network devices react and handle incoming network traffic and protocol interactions, you can identify potential weaknesses and assess the organization’s ability to withstand such attacks.
2. **Stress Testing Network Devices**\
   You can conduct stress tests on the target’s network devices, such as routers, switches, and firewalls, to evaluate their resiliencies against protocol-based DDoS attacks. By generating simulated attack traffic and monitoring device performance metrics under load, you can better determine whether your organization’s network infrastructure can effectively mitigate or withstand the impact of such attacks.
3. **Recommendation of Mitigation Measures**\
   Based on your findings, you can provide recommendations for improving your target organization’s defenses against both application layer and protocol-based DDoS attacks. This can include implementing additional security controls, fine-tuning network configurations, or enhancing response procedures to better detect and mitigate DDoS attacks in the future.

By leveraging application layer and protocol-based DDoS attacks in a penetration testing engagement, you can better help your organization to identify and address vulnerabilities in their defenses, ultimately enhancing their resiliencies against potential cyber threats of this nature.

### HTTP Floods

HTTP Flood attacks resemble repeatedly hitting refresh in a web browser across numerous computers simultaneously. The server gets quickly overwhelmed by a flood of HTTP requests, leading to a denial-of-service situation.

Such attacks vary in complexity. Simpler approaches involve accessing a single URL using the same set of attacking IP addresses, referrers, and user agents. On the other hand, more intricate versions employ numerous attacking IP addresses and randomly target URLs while using diverse referrers and user agents.

Imagine you’re browsing a website, and every time you hit the refresh button, your web browser sends a request to the server asking for the page to be reloaded. Now, picture this happening not just from your computer, but from thousands or even millions of computers simultaneously. Each of these requests consumes server resources, such as CPU processing power, memory, and bandwidth.

In an Application Layer DDoS attack, the hacker orchestrates this scenario on a large scale (think the Mirai botnet). They commandeer a network of compromised computers, also known as bots or zombies, to flood the targeted server with an overwhelming number of HTTP requests. These requests appear to be legitimate at first glance, as they mimic the behaviors of regular web HTTP traffic, making them difficult to distinguish from genuine requests and attribution.

The attack can also vary in sophistication. At the simpler end, you might direct all your bots to target a single URL, using the same set of IP addresses, referrers (the websites that supposedly linked to the target), and user agents (identifiers that specify the type of browser or device). This straightforward approach can still cause significant disruption if executed at a large enough scale.

However, as defenses evolve, so do the attack strategies and tactics. More complex versions of the attack might involve a diverse range of IP addresses, making it harder to block or filter out malicious traffic. Additionally, you may target multiple URLs across a website, or even random URLs to exploit weaknesses in a server’s handling of different requests. They might also vary the referrers and user agents for each request, further complicating detection and mitigation efforts.

In essence, an Application Layer DDoS attack capitalizes on the fundamental mechanisms of web browsing to overwhelm and incapacitate the target entity, causing disruption to legitimate users and services. Its effectiveness lies not just in the volume of requests, but also in the sophistication of its execution and the challenge it poses to defenders in distinguishing between malicious and legitimate network traffic.

### DDoS Attack Motivators

DDoS attack motives encompass a wide spectrum of objectives, ranging from ideological convictions to financial gain and strategic cyber warfare. Let’s explore each motive in detail:

**Ideology**

Hacktivist groups, exemplified by entities like the _Killnet_ group, employ DDoS attacks to target organizations – be they governments, political figures, or corporations – that clash with their ideological stance. While hacktivists may not always possess advanced technical skills, they leverage readily available tools to disrupt operations. Notable examples include the collective actions of Anonymous or sporadic hacktivist campaigns related to topical issues such as the COVID-19 pandemic.

Business Competition/Competitors

In cases where DDoS attack serve as weapons in corporate rivalry, they are often orchestrated by professional threat actors. These attacks aim to disrupt competitors’ online presence, thereby enticing their clientele to switch allegiance while inflicting financial and reputational harm. Reports suggest that the aftermath of successful DDoS attacks could financially cripple small businesses, with recovery costs exceeding $100,000, while larger enterprises might face expenses upwards of $2 million per incident.

Cyber Vandalism/Script Kiddies

Cyber vandals, script kiddies, or “skiddz,” devoid of clear criminal, political, or ideological agendas, engage in disruptive cyberattacks for the “fun of it,” or to see “how far they can get,” or push the envelope. Utilizing off-the-shelf, mostly open-source tools and created by other authors, like the Low Orbit Ion Cannon (LOIC) and DDoS-for-hire, or DDoS-as-a-Service, wreak havoc on digital platforms, leaving chaos in their wake.

Extortion

In instances of cyber extortion, cybercriminals leverage DDoS attacks – of the mere threat thereof – to extract monetary gains from their targets, exploiting fear and human vulnerability for illicit profits.

Cyber Warfare

Sophisticated adversaries, including Advanced Persistent Threats (APTs) and state-sponsored threat actors, orchestrate DDoS attacks as components of cyber warfare campaigns. These assaults typically target a nation’s critical infrastructure (ICS/SCADA), encompassing sectors such as finance, healthcare, transportation, and communications services.

Smokescreen

In a tactical maneuver, adept threat actors deploy DDoS attacks to divert attention away from their actual primary objective or to weaken security defenses. By creating artificial vulnerabilities, they pave the way for more insidious attacks, such as network breaches, data exfiltration, and malware infiltration, under the guise of chaos and confusion.

In sum, DDoS attack serve as versatile tools wielded by a diverse array of actors, each driven by distinct motives raging from ideological fervor to strategic advantage and financial gain. Understanding these motives is essential for crafting strategies, whether it be offense or defensive strategies, in this dynamic industry.

DoS and DDoS Tools
