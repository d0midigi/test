# Lateral Movement

Attackers seldom breach a network at their final destination. They look for the easiest entry point - a forgotten endpoint device, a compromised admin password extracted from the dark web, or an unwitting employee who downloads and installs malware. Once they gain this initial foothold, they use lateral movement, typically with compromised or newly discovered admin accounts to reach their goal: Personally Identifiable Information (PII) data, sensitive emails, strategic information, or anything else of value. They then use unprotected privileged access to steal this data and lock it away with ransomware.

In its simplest terms, lateral movement is when attackers take control of one asset within a targeted network and then obtain privileged access to move around and pivot within the network to further exploit other assets.

_Lateral movement_ techniques are widely used in sophisticated cyberattacks in particular in _**Advanced Persistent Threats (APTs).**_ The adversary uses these techniques to access other hosts from a compromised system and get access to sensitive resources, such as mailboxes, shared folders, or credentials. These can be used in turn for compromise of additional systems, privilege escalation, or stealing more valuable credentials. This type of attack may ultimately give access to Domain Controllers and provide full control of a Windows-based infrastructure or business-related operator accounts.

In this chapter, we refer to lateral movement attacks as connections from a _Windows host_ to a targeted _Windows host_ using calid stolen credentials of an account (e.g., user or service account).

The source host is usually a compromised system in the targeted Windows environment. The first host is compromised in most cases via a spearphishing attack that contains a malicious attachment or link to a site under an attacker’s control. Once compromised and in most of the cases, the attacker usually takes control of the host via a call-back to a Command and Control (C2) server and a reverse shell. After privilege escalation, the adversary can then dump credentials stored in this first compromised host and use them to connect to another host.

Consequently, a lateral movement is a two-step attack as follows:

1. **Capture credentials from a source host.**

The attacker can capture any valid credentials. The credentials are usually obtained through specialized tools that access Windows credential storage or memory. This paper is limited to the theft and misuse of NT hash and Kerberos credentials.

The adversary can potentially get any credentials stored in the compromised system, that are still in use or were used in the past (e.g., cached credentials) and that has not been wiped from memory (if no update is installed). The most interesting credentials are the privileged accounts of the targeted domain, such as helpdesk, admin, privileged service accounts, as well as local administrator accounts, especially if a password is reused or the password generation algorithm is predictable.

1. **Use Stolen Credentials to Access Hosts and Resources**

Once the credentials are stolen, the attacker can use them to access another resource, such as a host or a server (e.g., Exchange email accounts). The attacker can use techniques known as Pass-the-Hash or Pass-the-Ticket with NT hash or Kerberos ticket accordingly.

There are a few facts that are relevant regarding credentials theft and replay:

* **Any user** connecting to a compromised host **may leave credentials in memory** that can be dumped by the attacker (if appropriate updates are not installed(. Windows caches the credentials in memory to provide features like Single Sign-On (SSO).
  * **Accounts solely using&#x20;**_**Network Logon**_**&#x20;or RDP in Restricted Admin mode to log into the compromised target host are not exposed.**
  * **Any other type of logon exposes the credentials, including local, domain users or service accounts.**
* Impacted credentials are not limited to cleartext usernames/passwords, but also **NT hashes, Kerberos Tickets** and **Kerberos Keys** which can be used to request Kerberos TGTs are valid credentials for lateral movements as well.
* The attacker needs **administrative privileges** to access the credentials in the local Windows credential storage or memory (e.g., Windows Security Accounts Manager (SAM), Credential Manager, or Local Security Authority Subsystem Service (LSASS) process. A local privilege escalation vulnerability can be used for this if the compromised user does not have such privileges yet.
* Lateral movements are not limited to access another workstation, but can be used to connect to other resources such as a mailbox on an Exchange server or a business system.
* Lateral movements use standard protocols, like Kerberos and the NTLM protocol, which makes impossible to create a single dedicated Windows event or network IDS (NIDS) rules to detect them.
* One of the advantages of the lateral movement attack is that the attacker can capture credentials and use them later.
* Lateral movement are not Windows-specific problems, as any authentication protocol using SSO has the same issue. Any single sign-on solution requires storing credentials in some valid format so they can be reused to authenticate to other services without re-entering the password each time.

As happened with the 2013 Target breach, attackers may island-hop into a target network from smaller, less protected third-party’s network or they may gain access directly. Regardless, once they’re in, they move laterally across the network until they reach their target or land up something juicy, they know is valuable.

Think back to the SolarWinds attack. If anything positive came from that attack, it’s that even more people now realize how dangerous lateral movement can be – and why it’s important to build up a defense against it. A year later, adversaries broke into the Colonial Pipeline network via a compromised username and password and threatened to seize control of the largest fuel pipeline in the U.S.A. As a result, the Colonial Pipeline shut down the pipeline for the first time in its 57-year history. The company paid 75 bitcoins to ransom the network – almost $4.5 million.

Those attacks were not outliers. Attacks – and their severities – have been on the rise. During 2020, ransomware attacks rose 485% year-over-year. Many factors – the COVID 19 – pandemic, growing numbers of work- from-home workers, and the commoditization of ransomware-as-a-service – drove this growth, but the fact remains: lateral movement attacks will remain part of our reality for a long time.

Perhaps most importantly, this surge in ransomware attacks exposed the weak or reactive security practices that organizations have been forced to cobble together as they react to navigate the technological – and social – change brought on by demand for digital transformation and the hard realities of the pandemic over the last 24 months. Many of these security tools and practices had to be rolled out quickly. As a result, there are gaps that allow attackers to gain access to and move laterally from one system to another with relative ease.

**How Does Lateral Movement Work?**

Network diagrams often show traffic entering and leaving your network on the Y axis and movement within your network on the X axis. That’s why capabilities moving laterally within your network often get called east-west traffic, while capabilities that cross your perimeters are called north-south traffic. It’s how malware designed to perform reconnaissance downloads its weaponization, when it uses lateral movement to achieve a more advantageous vantage point on the network, for example.

![A diagram of different devices

Description automatically generated](<../.gitbook/assets/0 (45).png>)

After cyber attackers breach your perimeter – perhaps by phishing login credentials from an unwitting, overly helpful employee – they use that access to harvest and steal additional privileged user credentials (or even just the hashes) with greater levels of access, ultimately including privileged access.

By stealing the credentials (literally, the identities) of your employees, these cybercriminals move laterally across your network by logging into other accounts and machines, searching for other assets or credentials to steal. They become digital insiders and can stay for days, months, and years – dormant and lurking – until they’re ready to execute their attack.

It is difficult to detect lateral movement attacks because these cybercriminals are masquerading as your trusted users and weaponizing their access. While the breach is occurring, it’s hard to even know it. The access and the account will probably be authorized, even though the bad actor who is dialing in from miles, or continents, away isn’t.

**Three Stages of Lateral Movement**

These stages aren’t unlike the steps a tourist takes in a foreign country when they’re trying to keep a low profile and blend in before they venture out to explore. Even attackers often follow the predictable patterns of human nature.

**Stage 1: Learning the “Lay of the Land”**

Before they can, or even know how to, move laterally across a network, attackers start by laying low and learning about the environment in which they are attacking, or are about to attack, the culture of IT ecosystems, the comings and goings of personnel, and more. They watch your administrative users and devices. They map your network. They’re looking t learn from you, so they can learn how to better strategize their attacks against you.

They want to understand:

* Network hierarchies
* Host naming conventions
* Payload locations
* Operating System versions
* Access control systems

Like the timid tourist navigating a new country, they don’t want to make a wrong move that will expose them. They want to stay invisible.

These bad actors come armed with tools. Their tools tell them where you’re put your firewalls and other endpoint securities. They learn what’s available to access, and where these assets are located in a network. They build their own or adapt open-source tools, but often can purchase the entire stack of attack tools from dark web marketplaces.

During this reconnaissance phase, attackers lurk and gather data until they know enough about you, your privileged users, and your ecosystem. Then, they move.

**Stage 2: Credential Theft**

To do anything inside a network – valid or illicit – you need a user ID and a password that work. Lateral movement is no different. The lowest-tech way to steal a privileged user’s login credentials is still to … just ask for them.

**Phishing**

In phishing, cybercriminals prey on an employee’s trusting nature, unfamiliarity, or even indifference to a technical looking request. They may impersonate your tech support team and ask admin users to enter their ID and password into a fake portal, for example. Or they call your admin user, impersonate a technical employee and hoodwink the user to verify their identity by asking and getting their username and password.

It happens more often than you think. December 2020 research from Security Boulevard shows that over 30% of phishing emails are opened and 12% are clicked through.

**Typosquatting**

One step more complex than phishing, cybercriminals use Typosquatting when they set up a fake website that impersonates a valid one. In the fake site’s URL, they may make a common misspelling to the true website’s name, move a letter, or add a period. Another common method is to add a hyphen and another word to a valid site name.

An example of a typosquatted domain would be similar to www.googl.com, www. G00gle.com, www.googlle.com, www.goggle.com, plus more combinations.

At the fake site, the cybercriminal appropriates the logos, branding, and color scheme of the target company to treat the unwitting visitor to a mimicked user experience.

Once they begin receiving hits, these cybercriminals steal credentials, payment card details, and other PII. After they gain access to a user’s credentials, the attackers then use lateral movement within the network or island-hop to reach the crown jewels.

**Advanced Password-Stealing Scheme**

Beyond phishing and Typosquatting, cybercriminals can also target the user login credentials of even the savviest users on your network – without them ever knowing. Through a Pass-the-Hash (PtH) attack, cybercriminals steal the hashes of a user’s password without ever needing to learn the actual plaintext password. They then use the hashes to authenticate to a remote service or server.

Cybercriminals may also use tools like Mimikatz to pilfer passwords and user credentials stored in the memory of a machine or keylogging tools to steal a password as it’s being typed.

**Stage 3: Intelligence Gathering**

After they’ve gained the confidence to move around your network and have stolen the identity of one or more of your admin users, cybercriminals now set about searching out the assets they want. They move laterally along the paths that will take them there.

From the privileged user they’ve hacked, they move through your network, seeking new and more important locations and users. They hope to find the holy grail – privileged access that’s been left active and forgotten. They need that standing privilege to enter your network’s most protected areas.

**Why it is Difficult to Detect Lateral Movement**

Over the last two years especially, we’ve seen the damage that lateral movement can cause, but it’s an attack strategy that has plagued the industry for years. Why? As an industry, we’ve put a majority of our collective efforts into improving endpoint cybersecurity controls. Privileged access is most commonly an IT function; thus, controls just have not kept up.

Cyberattackers exploit this lack of privileged access management as an easy attack vector. They see it as a simpler task to gain access through a compromised credential or privilege escalation and to ride that lateral movement across the network. That’s what happened in the SolarWinds attack. The cyberattackers gained access to the SolarWinds network and then installed malicious code into Orion, SolarWinds’ software system.

When SolarWinds unknowingly pushed trojanized updates to this software out to as many as 33,000 customers, the malicious code went with it, replicating across cyberspace and granting the attackers footholds in thousands of companies to move laterally. At last count, the fallout from the SolarWinds attack is estimated to have reached some 18,000 SolarWinds customers, ranging from well-known Fortune 500 companies to high-level agencies within the U.S. government.

**Why Breaches Like SolarWinds Are Hardest to Detect**

It’s hard to detect lateral movement within a network because it’s hard to determine who is driving that authorized credential and what their intent might be. It might just look like normal network traffic. SolarWinds customers certainly didn’t automatically red flag their Orion updates as they arrived, even though they had been trojanized with malicious code sent by cyberattackers.

**Using Zero Trust to Contain Lateral Movement**

With the right tools, you can contain lateral movement and mitigate the damage cyberattackers can do to you and your environment.

Even if an intrusion occurs, lateral movement becomes much harder to accomplish if you’ve removed 24x7 administrator access with a Zero Trust model. With a Zero Trust approach, any system must reverify your access and reestablish trust explicitly. That’s not always as easy as it sounds. That’s why excess standing privilege is so prevalent across today’s networks.

| <img src="../.gitbook/assets/1 (31).png" alt="" data-size="original"> | Total instances of standing privilege (from system successfully scanned) |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| <img src="../.gitbook/assets/2 (26).png" alt="" data-size="original"> | Broken down by server                                                    |
| <img src="../.gitbook/assets/3 (23).png" alt="" data-size="original"> | Broken down by workstation                                               |
| <img src="../.gitbook/assets/4 (23).png" alt="" data-size="original"> | Average number by server                                                 |
| <img src="../.gitbook/assets/5 (22).png" alt="" data-size="original"> | Average number by workstation                                            |

**Typical APT Scenario Using Lateral Movement**

Usually, APTs will connect from one workstation to another to obtain higher and higher privileged accounts until they get the credentials of a domain admin account. The next step of the attack will usually be to access the Domain Controller(s) and dump all credentials of the Windows domain.

The following illustration below presents a typical scenario of an ATP with lateral movement.

![](<../.gitbook/assets/6 (24).png>)\
FIGURE X: APT lateral movement.

**Phases of a Targeted Attack**

In an ATP campaign, attackers begin by obtaining data on the target organization such as its network environment and the organizational structure. The gathered data is then used for social engineering ploys to gain entry into a targeted network. Attackers can use compromised email accounts or popular web-based email accounts to send contextually relevant email. This is done to trick employees into opening the email, which can carry exploits and malicious attachments or links.

**Phases of a Targeted Attack**

In an APT campaign, sophisticated attackers strategically initiate the infiltration process by meticulously gathering pertinent information about the target organization, meticulously studying its network environment and analyzing the organizational structure with keen attention to detail. Subsequently, they leverage this meticulously gathered data to construct elaborate social engineering techniques, utilizing a variety of deceptive strategies to gain illicit access into the intricate network infrastructure. Employing various tactics such as utilizing compromised email accounts or popular web-based email services, the attackers craft contextually tailored emails, meticulously engineered to deceive unsuspecting employees, enticing them into unknowingly unleashing a wave of exploits and malicious payloads concealed within attachments or hyperlinks.

Once the threat actors successfully breach the network defenses and establish a tenuous foothold within the system, they proactively engage in establishing and maintaining persistent communication with the compromised computer, tirelessly striving to deepen their access and escalate their privileges by extracting crucial login credentials from the network's repositories harboring invaluable information. It is imperative to note that the threat actors adeptly navigate through the network landscape, gaining insights and potentially exfiltrating sensitive data through seemingly innocuous channels such as perusing documents stored on desktops or exploiting network access to shared drives via regular user accounts.

As the threat actors meticulously sift through the vast data repositories, meticulously identifying the target data set, they skillfully prepare the discovered information for an impending exfiltration process, meticulously orchestrating the covert transfer of the compromised data out of the network undetected.

**Gaining Persistence Across the Network**

Lateral movement plays a critical role in the cyber threat landscape. It encompasses a range of malicious activities, including reconnaissance, credential theft, and the penetration of remote computers. Once threat actors establish communication channels with compromised systems and command and control servers, their next objective is to maintain persistent access throughout the network. This requires them to navigate laterally within the network infrastructure and escalate their privileges using various sophisticated tools. Through these maneuvers, threat actors aim to infiltrate servers housing invaluable data, often referred to as the company's "crown jewels."

In addition to servers, threat actors may also target endpoint systems, such as personal computers where sensitive documents like Microsoft Word, Excel, and PowerPoint files are commonly stored. As threat actors progress deeper into the network, their techniques become increasingly elusive, especially when they exploit Windows features and tools commonly wielded by IT administrators. By acquiring administrative privileges, threat actors ensure that their actions remain concealed and challenging to trace, shielding them from detection and raising the stakes of their malicious movements across the network.

**Journeying Deeper into the Network**

**Reconnaissance**

**In order to move laterally within the breached network and remain persistent without being detected, attackers go to great lengths to gather crucial information that will enable them to navigate the network undetected. This includes obtaining details about the network hierarchy, the specific services utilized on the servers, and the operating systems in place. By meticulously investigating the host naming conventions, attackers can effectively pinpoint the exact assets they wish to target next. Armed with this valuable intelligence, they are able to meticulously map out the network, analyzing each component to strategically plan their next course of action.**

Throughout this process, various sophisticated tools are employed to aid attackers in their quest for unauthorized access. For instance, tools like netstat, a powerful command-line utility, come into play by providing real-time information on network connections and open ports. This data proves invaluable in identifying the running services and internal servers accessible from the compromised computer. Additionally, port scanning tools are used to systematically examine open network ports, enabling attackers to establish tunnel connections between the compromised system and their own system. To circumvent any existing firewall protections, attackers leverage specialized port forwarding tools such as ZXPortMap and ZXProxy (also known as AProxy) to create secure tunnel connections that facilitate their covert operations within the breached network. By deploying these advanced techniques and tools, attackers adeptly navigate the network landscape, poised to carry out their next strategic moves undetected by unsuspecting security measures.

**Stealing Credentials**

**Cracking and Stealing Passwords**

Once threat actors identify other “territories” they need to access, the next step is to gather login credentials. This vital step of obtaining login credentials is crucial for threat actors as it allows them access to sensitive information and systems that they are targeting. In their quest to acquire these credentials, attackers employ a variety of sophisticated techniques and tools such as keyloggers, ARP spoofing, and hooking. Keyloggers are used to capture every keystroke made by a user, including usernames and passwords, providing threat actors with valuable login information. ARP spoofing, on the other hand, involves manipulating network traffic to intercept conversations between systems and steal credentials through spoofed ARP packets. Meanwhile, hooking tools play a significant role in extracting password-related functions to compromise authentication mechanisms. Additionally, threat actors leverage tools like Pwdump to retrieve password hashes from the Windows registry, granting them further access to critical systems. As part of their arsenal, attackers also utilize tools like Windows Credential Editor (WCE), Mapiget, Lslsass, Gsecdump, and CacheDump to exploit vulnerabilities and extract sensitive credentials. Overall, the concerted effort of threat actors in gathering login credentials demonstrates the elaborate methods they employ to infiltrate and compromise targeted systems.

Attackers have become increasingly adept at employing various sophisticated techniques to breach network security. Alongside techniques like phishing and social engineering, another method they utilize is known as “pass the hash.” This method eschews the use of plaintext passwords in favor of hashes to authenticate and escalate privileges once access is gained. By exploiting weaknesses in authentication systems, attackers can leverage these hashes to traverse the network's pathways.

In their arsenal of attacks, threat actors may also deploy brute force attacks. This attack method involves systematically guessing passwords from a pre-determined list until the correct one is found. This persistence and methodical approach can grant intruders unauthorized access to sensitive data and resources within the network.

Armed with this ill-gotten access and knowledge, threat actors can extend their reach within the network, clandestinely moving through different territories and gradually expanding their control. The insidious nature of their activities lies in their ability to fly under the radar, as traditional security measures often focus on detecting failed login attempts rather than successful ones. This oversight by IT administrators allows threat actors to operate in the shadows, exploiting vulnerabilities and infiltrating deeper into the network infrastructure without raising immediate alarms. As a result, organizations must remain vigilant and enhance their security protocols to detect and thwart these sophisticated attacks effectively.

**Infiltrating Computer Networks**

Using stolen credentials, threat actors have the ability to remotely access desktops, a method that is commonly employed by IT support staff. This approach to desktop accessibility may not immediately raise suspicions of an ongoing attack, making it an effective stealthy tactic for infiltrating systems. Furthermore, attackers leverage this access to acquire domain credentials, enabling them to penetrate deeper into networks by logging into various systems, servers, and switches.

By utilizing remote control tools, threat actors are able to extend their reach within the network, allowing them to remotely access and manipulate other desktops. These tools empower attackers to carry out a range of actions, such as launching programs, setting up tasks, and overseeing data collection on interconnected systems. Notable tools and techniques employed for these purposes include remote desktop tools, PsExec, and Windows Management Instrumentation (WMI). It is important to note that the mentioned tools are just a few examples of the array of mechanisms that threat actors utilize in their lateral movement within networks to further their malicious activities and achieve their objectives.

![](<../.gitbook/assets/7 (20).png>)

FIGURE X: Six stages of an APT attack.

**Develop Threat Intelligence**

Detecting lateral movement within a network can be quite challenging due to its elusive nature. However, with the aid of sophisticated monitoring tools and a robust in-depth defense strategy, enterprises can effectively detect related activities that may signal potential threats. It is essential for organizations to establish a comprehensive framework that incorporates both external and local threat intelligence. This intelligence plays a crucial role in identifying key indicators and activities associated with Advanced Persistent Threats (APTs).

In addition to utilizing threat intelligence, IT administrators need to have a deep understanding of their network infrastructure's normal state, known as the baseline. This knowledge serves as a reference point to assess whether any deviations indicate a potential compromise within the system. An important aspect of this monitoring process involves identifying any tools within the network that perform similar functions to those previously discussed. The presence of such tools should prompt a thorough investigation into their usage to ensure they are not being exploited for malicious purposes.

Furthermore, establishing a centralized system for logging all user activities is a reliable method for detecting unauthorized access attempts. By consolidating login information in a single location, organizations can effectively monitor and track user interactions within the network. This centralized approach enhances visibility and simplifies the process of identifying and investigating any suspicious or unauthorized access incidents.

Since blacklisting and traditional AV signature-based solutions won’t mitigate the risks of targeted attacks at this particular stage, enterprises need a robust security technology that can provide real-time local and global intelligence.4 This can help IT administrators understand the nature of the attack they are dealing with. It also supports threat intelligence initiatives with its network-wide security event collection and analysis, which can enable IT administrators to perform remediation and containment plans. These remediation plans should include an advanced threat detection which can determine any malicious content and communications. Such a plan should also include detecting behavior indicative of advanced malware and threat actor activity, threat tracking, analysis, and action that provides real-time threat visibility and in-depth analysis.
