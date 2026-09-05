# Penetration Testing

### Penetration Testing

### Goals and Types of Penetration Testing

Penetration testing attempts to exploit weaknesses or vulnerabilities in systems, network, human resources, or physical assets to stress test the effectiveness of security control mechanisms.

The different types of penetration tests include network services, web application, client-side, wireless, social engineering, and physical. A penetration test may be performed externally or internally to simulate different attack scenarios and vectors. Depending on the goals set forth by the client, or organizations, a penetration tester may or may not have prior knowledge of the environment and system they’re attempting to penetrate and breach. Various types of penetration tests are known as:

* Black-Box
* Gray-Box
* White-Box

Penetration testing has become an essential tool for IT security teams to understand the strengths and weaknesses

### Goals of a Penetration Test

In recent years, penetration testing has emerged as an essential practice across various organizations, particularly in those industries like retail, banking, and healthcare, where the collection of storage of sensitive or private information (PII) are commonplace. The primary aim of conducting penetration tests is to uncover vulnerabilities or exploit weaknesses, enabling IT security teams to prioritize remediation and address these issues effectively; however, it’s crucial to recognize that these efforts often align with broader business objectives necessitating effective cybersecurity strategies.

Consider a scenario where your organization is vying for a $10 million government contract, contingent upon meeting NIST compliance standards within a strict timeframe. Achieving NIST compliance involves periodic penetration testing. Yet, the overarching reason for engaging in penetration testing transcends mere compliance – it serves as a critical measure of the maturity of your IT security practices.

During a penetration test, a tester evaluates a target environment with the intent to compromise and gain control over targeted systems and networks. The ultimate goal is to identify vulnerabilities within the environment and compile a comprehensive report detailing these findings. Interestingly, the scope of these tests is not confined to specific systems or methodologies; testers have the latitude to launch attacks across the entirety of your organization’s system and infrastructure.

Upon completion of the test and delivery of the final Executive Summary, your organization, or your client organization gains valuable insight into its IT security maturity. This assessment is pivotal in determining whether your current security measures are adequate enough to fulfill business objectives and safeguard the data of your customers, employees, and stakeholders.

### The Different Types and Approaches to Penetration Testing

Penetration tests vary significantly in both approach and the specific parts of the infrastructure they target. Here are some of the different approaches and types of penetration testing you might encounter:

* **External versus Internal:** Tests either focus on external threats or examine vulnerabilities within an internal network.
* **White Box:** You are given full knowledge of the network and system, allowing for a thorough examination.
* **Black Box:** You have no prior knowledge of either the systems, services, or network topology and its operating infrastructure, simulating a real-world external attack.
* **Gray Box:** A mix of white and black box testing, offering a balance between internal and external attack perspectives.

#### TYPES OF PENETRATION TESTS

* **Network Services:** Focuses on vulnerabilities in networked services.
* **Web Application:** Targets web applications for security flaws.
* **Client-**&#x53;ide: Examines vulnerabilities that could affect end-user’s systems.
* **Wireless:** Tests the security of wireless networks.
* **Social Engineering:** Assess how well the organization resists manipulation and human vulnerability tactics.
* **Physical:** Evaluates the security of physical assets and facilities securities.
* **Mobile Applications:** Looks for vulnerabilities in mobile applications and device OSs.
* **IoT (Internet of Things) Devices:** Tests the security of Internet of Things devices.

#### Key Differentiators in Penetration Tests

* **Penetration Tester Experience:** It’s crucial for you to remain certified, and to stay abreast of evolving technologies and remain experienced. Your expertise directly impacts what your client learns from the test and shows them how to properly address vulnerabilities through tried and true techniques.
* **Daily Reporting on Progress:** Transparency is key. You should provide daily updates have your client understand exactly what is being tested and showcase the benefits derived from the gathered insights.
* **Retesting Remediated Vulnerabilities:** After issues have been remediated, retesting is essential to verify the effectiveness of the fixes applied.
* **Integration with Other Security Services:** Penetration testing should complement an organization’s overall security program, integrating with vulnerability assessments and risk management strategies.

Over the past few years, businesses have been bolstering their defenses with advanced technologies like Endpoint Detection and Response (EDR) solutions, Next-Generation Firewalls (NGFWs), and anti-phishing measures; however, adversaries continuously evolve their tactics as well, developing new malware and creative attack vectors to circumvent or bypass traditional security measures. For instance, a _**Kerberoasting attack**_ exploits weak Active Directory policies, allowing unauthorized access to encrypted hashes of user profiles, which can then be cracked offline.

Moreover, internal penetration tests assess the damage a malicious actor could inflict once inside a network. This helps determine if a defensive team can detect the intrusion or if the malicious actor can escalate privileges to gain administrative rights.

By having a firm understanding of these aspects of penetration testing, you can better prepare your client organization against potential threats to better strengthen overall cybersecurity postures.

\
![](<../../.gitbook/assets/0 (61).png>)

_**FIGURE X:** Illustration depicting internal penetration test discovering weaknesses in email security processes._

#### Black Box Penetration Testing

We’ve touched upon Black, White, and Gray box penetration tests earlier. Let’s dive deeper into what a Black Box penetration test entails. In this scenario, you are provided with minimal to no relevant or pertinent information about the IT infrastructure or security protocols in which you are tasked to assess. Essentially, you start off knowing very little about the business’ _lay of the land_ and are tasked with compromising systems and data as if you are a hacker with malicious intentions. The primary advantage of conducting a Black Box test is that it mimics a genuine cyberattack, offering insights into how well your client organization’s defenses hold up against external threats.

The duration of a Black Box penetration test can range from a few days to several months, depending on the complexity of the IT infrastructure and the objectives and scope of your test. Given the extensive planning, execution, testing, and reporting involved, organizations should anticipate spending between $10,000 and $25,000, or even more. One common strategy testers employ during a Black Box test involves utilizing known exploits, such as Kerberoasting, to breach systems. Despite being labeled as a “trial and error” approach, executing these tests requires a high level of technical expertise and proficiency.

To clarify some terminology, you might encounter during discussions about penetration testing: _Ethical hacking_ shares similarities with penetration testing, but also has distinct differences. Ethical hacking is a broader term encompassing hacking techniques employed by ethical hackers, or white hat hackers. While penetration testers identify vulnerabilities and compile reports, ethical hackers typically engage in more comprehensive assessments over longer periods, employing a wider array of attack vectors and conducting thorough exploration of the environment.

Ethical hackers aim to uncover as many security flaws as possible, making their assessments more holistic compared to the point-in-time evaluations conducted by penetration testers. Additionally, ethical hackers often assist with remediation efforts, working closely with organizations and clients to enhance the security of target systems with the explicit permission of the system owners.

#### White Box Penetration Testing

White Box penetration testing, also known as _**clear box**_ or _**glass box testing,**_ grants you full visibility and access to your environment, systems, software, and even the source code. The objective of conducting a white box penetration test is to thoroughly evaluate the strengths and weaknesses of your client’s business systems, providing you with extensive details. This level of access allows for a deeper dive into areas inaccessible during black box testing, such as the quality of code and application design, resulting in more comprehensive assessments and outcomes.

However, white box tests come with their own set of unique challenges. The extensive access can make it more time-consuming to decide which areas to prioritize. Moreover, these tests often necessitate advanced and costly tools like code analyzers and debuggers. Typically, white box tests span between two to four weeks and can range in cost anywhere from $4,000 to $20,000. It’s important to distinguish that while black box penetration tests aim to breach security controls and compromise a business, white box tests are designed to evaluate the security controls, maturity, and vulnerabilities within a business.

It’s also worth noting that the security audits and penetration tests are sometimes conflated, though they serve different purposes. A security audit measures cybersecurity performance against established standards, such as the NIST Cybersecurity Framework (CSF), employing a detailed checklist of security control compliance. Unlike penetration tests, which focus on finding more than one vulnerability to gain access and compromise the environment, security audits offer a broader assessment of the entire security program.

#### Gray Box Penetration Testing

During a Gray Box penetration test, you’re given only partial knowledge or access to an internal network, software, service, or web application. This might mean starting with user privileges on a host and being tasked with escalating those privileges to domain admin levels, or perhaps gaining access to software code and system architecture diagrams. The aim of gray box pentesting is to conduct a more focused and efficient security assessment and analysis of a network compared to what a black box assessment could achieve. By leveraging design documentation for a network, pentesters can immediately target systems posing the greatest risk and value, saving time that would otherwise be spent gathering this information independently. Additionally, having internal account access enables testing of security within the fortified perimeter, simulating a malicious actor who has managed longer-term access to the network. Gray box testing effectively bridges the gap between white box and black box testing, offering a balanced approach by providing limited information about the target system or network. This setup mimics the level of knowledge a hacker with sustained access to a system would accumulate through research and reconnaissance and footprinting efforts.

### Penetration Testing – Ethical Hacking, Red Teaming, Capture the Flag (CTF), and Bug Bounty Programs

Over recent years, the landscape of penetration tests has expanded significantly, leading to potential confusion among organizations. Understanding the distinctions between penetration tests, ethical hacking, red teaming, and activities like Capture the Flag (CTF) competitions and bug bounty programs is crucial for IT security organizations aiming to evaluate their cybersecurity posture and performance accurately. Penetration testing remains a fundamental method for organizations to assess their security maturity and identify potential vulnerabilities within their environment; however, the market now offers a variety of options, making it essential to stay informed about the latest and most effective ways to evaluate cybersecurity performance. Terms such as penetration testing, ethical hacking, red teaming, and CTF exercises are often confused, even among seasoned cybersecurity professionals With new types of testing emerging annually, keeping abreast of developments ensures you’re leveraging the most effective strategies for effectively assessing cybersecurity performance.

![A diagram of a question

Description automatically generated with medium confidence](<../../.gitbook/assets/1 (46).png>)

What Is Red Teaming – A More Advanced Assessment Process

Red Teaming represents a more sophisticated and focused form of security assessment compared to traditional penetration testing efforts. Its primary objective is to rigorously test an organization’s detection and response capabilities. Unlike penetration testing, which aims to identify as many vulnerabilities as possible, red team assessments simulate actual attack scenarios with great detail, often without informing the organization beforehand. This approach allows the red team to leverage various attack methods to access critical and sensitive data, effectively mimicking the attack methods, tactics, techniques, and procedures (TTPs) of real adversaries.

Red Team assessments tend to be longer and more thorough investigations into security vulnerabilities and their potential impacts, employing methods such as social engineering, wireless testing, and physical security testing. Essentially, red team assessments are designed to test the organization’s detection and response capabilities by attempting covert access to sensitive information in any possible manner.

Capture the Flag (CTF) Exercises

Capture the Flag (CTF) exercises offer another great dimension to penetration testing. These exercises assign you specific goals, such as exfiltrating a particular data file or accessing a certain system, often set up in a competitive environment where teams vie to achieve their objectives first. CTF exercises differ from traditional penetration tests by frequently using test environments, third-party platforms, and by using deliberately vulnerable applications within vulnerable environments, making them more about evaluating your skills as a pentester or ethical hacker rather than about assessing production systems for flaws and weaknesses. CTF exercises and competitions serve as a valuable tool for recruiting new talent, as companies are known to hire on-the-spot at these events and enhances your testing capabilities in testing systems in a controlled yet competitive environment.

Understanding the distinctions between these various forms of security assessments can help lessen confusion not only for yourself, but for your client who may be having trouble in deciding which assessment they should use to best suit their security needs. Each method serves a unique purpose and addresses different aspects of security preparedness, making the complementary components of a comprehensive security strategy for all involved.

![A graph showing a bar graph

Description automatically generated with medium confidence](<../../.gitbook/assets/2 (40).png>)

What’s the Difference Between Penetration Testing and Ethical Hacking?

Penetration testing and ethical hacking, while similar in their objectives to identify vulnerabilities within systems, have distinct differences in their methodologies and scopes. Below is a table showcasing the distinct differences:

| Penetration Testing |                                                                                                   |
| ------------------- | ------------------------------------------------------------------------------------------------- |
| Focus               | Primarily targets specific vulnerabilities within a system or network to assess security posture. |
| Scope               | Limited to the areas defined for testing, focusing on identified weaknesses                       |
| Duration            | Typically shorter, ranging from a few hours to a few days, depending on the scope.                |
| Objective           | To identify vulnerabilities and provide recommendations for remediation.                          |
| Access              | Requires access only to the systems or networks designated for testing.                           |

| ETHICAL hACKING |                                                                                                                                                                                                                            |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Focus           | Aims to uncover a wide range of vulnerabilities using various attack vectors.                                                                                                                                              |
| Scope           | Broader, covering the entire IT environment to provide a comprehensive security evaluation.                                                                                                                                |
| Duration        | Longer, often spanning several weeks or months, to allow for a thorough exploration of the environment.                                                                                                                    |
| Objective       | Aim to simulate real-world attacks to assess organization’s ability to respond to such threats.                                                                                                                            |
| Access          | Requires access to a wider range of systems and networks beyond the immediate scope of the test. Scopes are later modified upon agreement and is dependent upon severity of finding and organization’s tolerance for risk. |

Bug Bounty Programs

Bug bounty programs incentivize the discovery of vulnerabilities in software by offering rewards usually in the form of cash payouts to researchers who find and report responsibly on these issues. Initially popularized by tech giants like Facebook and Google, these programs have evolved to offer significant financial rewards for identifying critical vulnerabilities. Companies now offer substantial payouts for significant findings, and the participation has expanded to include former criminal hackers, attracted by lucrative incentives for discovering vulnerabilities.

Network Service and Vulnerability Assessment and Penetration Testing (VAPT)

This type of testing focuses on identifying exploitable vulnerabilities in networks, systems, hosts, and network devices, such as routers, switches, and firewalls. The goal is to uncover real-world opportunities for adversaries to compromise systems and networks, potentially leading to unauthorized access or complete takeover. The duration of a network vulnerability assessment and penetration test varies based on the size and complexities of the network, but generally ranges from one week to four weeks.

![A diagram of a computer network

Description automatically generated](<../../.gitbook/assets/3 (29).png>)

How Does a Network Service Penetration Test Work?

There are 6 main steps to performing a network service penetration test including:

Why Should You Perform a Network Service Penetration Test? Network penetration tests should be performed to protect your business from common network-based attacks including: • Firewall Misconfiguration And Firewall Bypass • IPS/IDS Evasion Attacks • Router Attacks • DNS Level Attacks: • Zone Transfer Attacks • Switching Or Routing Based Attacks • SSH Attacks • Proxy Server Attacks • Unnecessary Open Ports Attacks • Database Attacks • Man In The Middle (MITM) Attacks • FTP/SMTP Based Attacks Given that a network provides mission-critical services to a business, it is recommended that both internal and external network penetration tests be performed at least annually. This will provide your business with adequate coverage to protect against these attack vectors. External Network Assessment Perimeter networks in almost every organization are attacked every day and even small external vulnerabilities can be damaging. External network penetration testing identifies vulnerabilities on infrastructure devices and servers accessible from the outside internet. External penetration testing assesses the security posture of the routers, firewalls, Intrusion Detection Systems (IDS) and other security appliances which filter malicious traffic from the internet. Internal Network Assessment The benefit of an Internal Network Assessment in ensuring a breach of your external network will not result in a breach of your organizational assets. The local area network should be tested as if you have an insider threat or an attacker on the inside of the organization. Pen testers should look for privileged company information and other sensitive assets. This usually involves incorporating a variety of tools, uncovering user credentials, and attempting to compromise both virtual and physical machines present in the network environment.

Web Application Penetration Testing First

A web application (web app) is an application program that is stored on a remote server and delivered over the Internet through a browser interface. Web services are web apps by definition and many, although not all, websites contain web apps. Users can access a Web application through a web browser such as Google Chrome, Mozilla Firefox or Safari. Web application penetration testing is used to discover vulnerabilities or security weaknesses in web based applications. It uses different penetration techniques and attacks with aims to break into the web application itself. The typical scope for a web application penetration test includes web based applications, browsers, and their components such as ActiveX, Plugins, Silverlight, Scriptlets, and Applets. These types of tests are far more detailed and targeted and therefore is a more complex test. To complete a successful test, the endpoints of every webbased application that interacts with the user on a regular basis must be identified. This requires a fair amount of effort and time from planning to executing the test, and finally compiling a useful report. The techniques of web application penetration testing are continuously evolving with time due to the increase in threats coming from web applications day by day.

How Does a Web Application Penetration Test Work?

As suggested previously, penetration testers are trained to think with the adversary’s perspective in mind. This allows you to attempt exploitations during the test in ways that an actual adversary might. As a result, applications are stress-tested for any known or previously undiscovered points of entry or vulnerability. Pentesters may use any number of attacks to compromise an application including:

* Cross-Site Scripting (XSS) Attacks: 40% of all Attacks
* SQL Injection (SQLi) Attacks: 24% of all Attacks
* Password Cracking Attacks
* DoS And DDoS Attacks
* Directory Traversal Attack
* Local File Inclusion (LFI)
* Broken Authentication and Session Management Attacks
* File Upload Flaws
* Cross-Site Request Forgery (CSRF) Attacks
* Security Misconfigurations

Other test scenarios include:

* Deployment Management Testing
* Identity Management Testing
* Input Validation Testing
* Error Handling
* Cryptography
* Business Logic Testing

Why Should You Perform a Web Application Penetration Test?

Web applications are by far the most common method of compromise against e-commerce websites or really any company with an internet presence. A key reason to perform a web application penetration test is to identify security weaknesses or vulnerabilities within the web-based applications and its components like a database, source code, and the backend network. It also helps by prioritizing the determined weak- nesses or vulnerabilities and provides possible solutions to mitigate them.

In software application development it’s considered best practice to continuously improve the codebase although security is rarely considered a primary objective in the application development process. _**“Deploying a secure and agile code”**_ is the phrase often used to describe this practice. Agile code deployment is the preferred method over large batch deployments, as the more variables introduced into the code in a single deployment, the more opportunities there are to create bugs or errors leading to security vulnerabilities. As a result, a “technical debt” forms, where developers gradually spend more time implementing fixes to problems than they do improving the functionality of the software by developing new features or updates.

In contrast, agile methodologies use a sandbox environment or copy of the codebase in a clean testing environment to test code functionality and usability prior to launching the software into production. If the initial deployment is unsuccessful, developers can easily single out issues and roll the code back to previous version history. The problem with application development up until now is that that security has not been considered with daily code deployment.

Client Side Penetration

Testing client-side penetration testing, also known as _**“internal pen testing**_,” is the act of trying to exploit vulnerabilities in client-side application programs such as an email clients like Microsoft Outlook, web browsers (e.g., Chrome, Firefox, Safari), Macromedia Flash, Adobe Acrobat and others. Client-side penetration tests are similar in goals to other penetration tests and are performed to answer the following questions:

* How reliable is the security posture of an organization through client-side apps?
* Are there any vulnerabilities in these apps? (Most of these apps do have vulnerabilities)
* What harm can an attacker do by exploiting these vulnerabilities?
* How can a malicious actor exploit a vulnerability?
* Are the access rights and privileges for employees set correctly? (This is critical to understanding how an attack may move through an organization)
* How can the detected weak points be remediated quickly and cost effectively?

How Does a Client Side Penetration Test Work?

Pentesters run a network vulnerability scan as part of a penetration test to identify and categorize applications at risk. The image above shows a Nessus scan of vulnerabilities found on a host. The issue here is that the host is missing a variety of security updates for several application and that without updates through patches the host is vulnerable to an attack. The scanner also lists the Common Vulnerabilities Exposures (CVE) for each vulnerability. The scan will recommend applying an update or patch as you see above to resolve the vulnerability. The pen tester doesn’t typically apply patches but rather exploits vulnerabilities to gain entry to your network and systems.

Why Should You Perform a Client Side Penetration Test?

As suggested, a client-side vulnerability often takes the form of unpatched software on a desktop or laptop. Depending on the nature of the vulnerable application, an individual could exploit it using a malicious email attachment or by convincing the user to visit a malicious web site; yes, this is a phishing attack.

When assessing your organization’s exposure to such threats via client-side penetration testing, you should mimic two common scenarios:

* Attackers targeting specific employees with messages carrying malicious payload or by pointing the victim to a malicious web site
* Large-scale client-side infection campaigns that rely on victims to visit compromised web sites that deliver client-side exploits, possibly through malicious banner ads
* Client-side tests are performed to identify specific cyber-attacks including
  * Cross-Site Scripting Attacks
  * Clickjacking Attacks
  * Cross-Origin Resource Sharing (CORS)
  * Form Hijacking
  * HTML Injection
  * Open Redirection
  * Malware Infection

![](<../../.gitbook/assets/4 (32).png>)

Wireless Penetration Testing

Many organizations continue to overlook wireless security as an attack surface, and, therefore, fail to establish required defenses and monitoring, even though wireless technologies are now ubiquitous in executive suites, financial departments, government offices, retail, and frankly almost everywhere nowadays. Wireless penetration testing involves identifying and examining the connections between all devices connected to the business’s WiFi. These devices include laptops, tablets, smartphones, and any other internet of things (IoT) devices. For many pen testers, “wireless” was once synonymous with “WiFi,” the ever-present networking technology, and many organizations deployed complex security systems to protect these networks.

Today, wireless takes on a much broader meaning -- not only encompassing the security of WiFi systems, but also the security of Bluetooth, Zigbee, Z-Wave, DECT, RFID, NFC, contactless smart cards, and even other proprietary wireless systems. The testing of wireless networks generally includes:

* WiFi network identification, including wireless fingerprinting, information leakage and signal leakage
* Determine encryption weaknesses, such as encryption cracking, wireless sniffing and session hijacking
* Identifying vulnerabilities to penetrate a network by using wireless or evading WLAN access control measures
* Identify legitimate user identities and credentials to access otherwise private networks and services.

![A computer network with devices connected to it

Description automatically generated](<../../.gitbook/assets/5 (29).png>)

How Does a Wireless Penetration Test Work?

Wireless attacks have become a very common security issue when it comes to networks. This is because such attacks can really get a lot of information that is being sent across a network and use it to commit some crimes in other networks. Every wireless network is vulnerable to such kinds of attacks, and it is, therefore, important that all the necessary security measures are taken to prevent the data leakage that can be caused by such attacks. One of the most important phases of a wireless penetration test is the information-gathering phase. For example, an access point could still be using default credentials that the device shipped with. If the attacker knows the make and model of the device, then they can deploy a wireless attack to take down or access the network. Next, the pen tester identifies vulnerabilities in the discovered hardware, checks the WiFi signal strength beyond the organization’s physical area, and checks the visible nodes in the WiFi network. As a result, this will map any workstation, server or other devices publicly visible and accessible in the network. Examples of wireless penetration testing attacks include:

* Bypassing WLAN Authentication: Shared Key, MAC Filtering, Hidden SSIDs
* Cracking WLAN Encryption: WEP, WPA/WPA2 Personal and Enterprise
* Understanding encryption based flaws (WEP, TKIP, CCMP)
* Attacking the WLAN Infrastructure: Rogue Devices, Evil Twins, DoS Attacks, MITM, WiFi Protected Setup (WPS)
* Advanced Enterprise Attacks: 802.1x, EAP, LEAP, PEAP, EAP-TTLS
* Attacking the Wireless Client: Honeypots and Hotspot attacks, Caffe-Latte, Hirte, Ad-Hoc Networks and Viral SSIDs, WiFishing
* Breaking into the Client: Metasploit, Social Engineering Toolkit (SET)
* Enterprise WiFi Worms, Backdoors and Botnets

Why Should You Perform a Wireless Penetration Test?

Poorly secured WiFi networks are targeted by more sophisticated cybercriminals and organized crime groups to gain a foothold in the network. The attacks are among the most lucrative. Access to a business network can allow ransomware to be installed and if malware can be installed on POS systems, the credit/debit card numbers of tens or hundreds of thousands of customers can be stolen. Also, cybercriminals may use a rogue wireless device, or access point. This is an unauthorized WiFi device added onto the network that isn’t under the management of the network admins. They allow potential attackers a gateway into the network. This sort of device can be maliciously installed if the attacker has direct access to the wired network, but often they are added by staff that are not aware of the implications.

Another wireless hack technique is “Spoofing” a WiFi network, which simply means copying it, which can create an “Evil Twin.” This is a network that looks and behaves identically, or at least similarly, to a legitimate network. If the attacker sets up a router with the same name and password as one of your habitual networks, you probably won’t give it a second thought when you connect, or your computer connects automatically. There are dozens of wireless attacks like those described above that could compromise your network, systems and data. Conducting a pen test to uncover common vulnerabilities will eliminate another attack vector and reduce your overall attack surface. Before performing a wireless penetration test you should consider the following:

* Have all access points been identified and how many use poor encryption methods?
* Is the data flowing in and out of the network encrypted and if so, how?
* Are there monitoring systems in place to identify unauthorized users?
* Is there any possibility the IT team could have misconfigured or duplicated a wireless network?
* What are the current measures in place to protect the wireless network? Are all wireless access points using the WPA protocol?

Social Engineering Tests

Social engineers are the type of hackers who exploit the one weakness that is found in almost every organization: human behavior and psychology. Using a variety of media, including phone calls, social media, and predominately e-mail these attackers trick people into providing access to sensitive data or other company assets. The Verizon 2019 Data Breach Investigations Report (DBIR) found e-mail phishing to be the top threat action variety in all breaches analyzed. Phishing, spear phishing, whaling and other forms of e-mail attacks have dominated the cybercrime landscape for the past several years.

According to the Verizon report over 70% of all cyber-attacks start with a phishing scam. Unsuspecting employees are sent an e-mail with a malicious attachment or malicious link and because they are not trained at spotting the scams open the attachment or click on the link unleashing the malware into corporate systems. Social engineering tests are where a malicious actor attempts to persuade or trick users into giving them sensitive information, such as a username and password. Common types of social engineering tests used by pen testers include:

* Phishing
* Spear Phishing
* Whaling Attacks
* Tailgating
* Imposters who pose as company employees, 3rd party vendors, or partners
* Name Dropping
* Pre-Texting
* Dumpster Diving
* Eavesdropping

How Does a Social Engineering Test Work?

* What is phishing exactly? Most phishing scams demonstrate the following characteristics:
* Seek to obtain personal information, such as names, addresses and social security numbers.
* Use link shorteners or embed links that redirect users to suspicious websites in URLs that appear legitimate.
* Use attachments like Microsoft Word or Excel often from e-mail addresses that appear trusted.
* Incorporates threats, fear and a sense of urgency to manipulate the user into acting promptly.

Some phishing emails are more poorly crafted than others to the extent that their messages sometimes intentionally have spelling and grammar errors to target poorly trained users. Social engineering penetration testing is the practice of attempting typical phishing or other social engineering scams on an organization’s employees to understand the level of vulnerability to this type of attack. Social engineering pen testing is ultimately designed to test employees’ compliance with the security policies and practices defined by management.

Why Should You Perform Social Engineering Tests?

According to Verizon and other recent reports, 98% of all cybercrime rely on some form of social engineering to initiate the scam. As we suggested prior, this is because employee errors including opening malicious attachments and clicking malicious links are the most significant threat to an organization’s security. No matter how good cybersecurity technology is in an organization, human error can help cybercriminals circumvent even the best defenses. Social engineering tests and awareness programs have proven to be the most effective steps an organization can take to prevent being breached. An excellent social engineering and email phishing platform, KnowBe4, simulates an email phishing attack.

When the user clicks on the malicious link, they’re taken to a page that informs them that it was a phishing test…and they failed. Remediation training is then provided to help inform users on the most current phishing attacks and how to avoid them.

![A close-up of a sign

Description automatically generated](<../../.gitbook/assets/6 (31).png>)

Physical Penetration Testing

Just like a penetration test on IT infrastructures or systems, physical penetration testing, or physical intrusion testing, will uncover real-world opportunities for malicious insiders or cybercriminals to be able to compromise physical barriers (e.g., locks, sensors, cameras, keypads, mantraps) in such a way that allows for unauthorized physical access to sensitive areas leading up to data breaches and system/network compromise. This type of test is an attack simulation carried out by security consultants trained in physical security control to:

* Test perimeter security including alarms, motion detectors, security guards, and other physical and electronic barriers
* Identify physical security control flaws present in the environment
* Understand the level of real-world risk for your organization
* Help remediate physical security vulnerabilities

The overall time to complete a physical pen test depends on the size and complexity of the in-scope facilities. That said, most tests take anywhere from two weeks to six weeks, start to finish. In general, the number of locations, number of physical barriers tested, and the objective will ultimately determine the cost.

![A cartoon of a dog with a computer and a door

Description automatically generated](<../../.gitbook/assets/7 (28).png>)

How Does a Physical Penetration Test Work?

Physical security is an often-overlooked component of data and system security. While frequently forgotten, it is no less critical than timely patches, appropriate password policies, and proper user permissions. Organizations can have the most hardened servers and network but that doesn’t make the slightest difference if someone can gain direct access to a keyboard or, worse yet, march your hardware right out the door. Pen testers use any number of methods during a physical penetration test including:

* Mapping Perimeter Entrances
* Lock Picking Entry Points
* Remotely Accessing Sensitive Information
* Targeting Server Rooms, Wires, Or Cables
* Exploiting Fire And Cooling Systems
* Intercepting EM Waves
* Dumpster Diving
* Breaking RFID Tag Encryption
* Tailgating
* Accessing Unprotected Network Jacks
* Checking Rooms For Unattended Devices
* Shoulder Surfing
* Social Engineering

![A group of computer servers

Description automatically generated](<../../.gitbook/assets/8 (23).png>)
