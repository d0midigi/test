# A Primer on Cybersecurity and Cyberattacks

It is in these times that we are being primarily driven by technology. Everything around us, everything we interact with either directly or indirectly, everything the encompasses our normal day to day processes is being driven by technology. This world is more interconnected than it has ever been and continues to adapt and evolve. The global economy rely on people's ability to communicate across time zones and access crucial information from anywhere at any time. Cybersecurity enriches productivity and innovation by providing the confidence needed to work nd communicate online securely.

Cybersecurity encompasses all measures that ensure the protection and integrity of data, whether sensitive or not, within a digital infrastructure. It involves sets of processes, best practices, methodologies, and technological solutions and advancements that help protect critical infrastructure and networks from digital cyberattacks. Capitalizing on the surge in data and the growing number of people working and connecting remotely to branch offices, threat actors and adversaries have devised sophisticated measures and methods to access restricted resources in an unauthorized manner, steal data, sabotage businesses, and extort money. The number of attacks rises as each year passes, with adversaries continuously developing new techniques to evade security detection mechanisms. An effective cybersecurity program integrates people, processes, and technology solutions to mitigate the risk of business interruption, financial loss, company reputation, brand, and trademark damage in the event of a cyberattack.

Individuals and organizations from small to large and within all business sectors face different types of digital threats every day. These threats can include anything from computer attacks or acts of espionage aimed at stealing personal data, targeted attacks to gain economic advantage, or cyberterrorism intended to create insecurity and distrust in large groups. A cyberattack refers to an action designed to target a computer, network, or any element of a computerized information system or data warehouse with the aim of modifying, destroying, disrupting, defacing, or exfiltration of data, as well as exploiting or harming a network. It includes any type of malicious intent or offensive action that targets computer systems, infrastructure, networks, and even personal computers, personal vehicles, or using various methods to steal, modify, or destroy data or systems.

An effective cybersecurity program is not merely a collection of software; it is the strategic integration of people, processes, and technology. By aligning these three pillars, organizations can mitigate the catastrophic risks of business interruption, financial insolvency, and irreparable brand damage that follow a successful breach.

This chapter offers a thorough analysis of the fundamentals of cybersecurity, focusing particularly on technical cyberattacks in general. The aim is to provide a thorough overview of cybersecurity and the principal frameworks and regulations that guide it.

#### The Nature of the Cyberattack

Today, every sector - from small businesses to multinational corporations and government agencies - confronts a relentless tide of digital threats. These range from corporate espionage and the theft of personal data to state-sponsored cyberterrorism designed to destabilize public trust.

A cyberattack is defined as any malicious action targeting a computer, network, or information system with the intent to alter, destroy, or exfiltrate data. These offensive maneuvers exploit vulnerabilities in everything from enterprise-grade servers to personal vehicles, turning the tools of our productivity into vectors for harm.

This writeup provides a comprehensive analysis of cybersecurity fundamentals, with a specific focus on the technical mechanics of modern cyberattacks. We will explore the primary frameworks, compliance regulations, and defensive measures that define the industry today. The structure is organized as follows:

* Section 1.2: A deep dive into technical cyberattacks.
* Section 1.3: An analysis of the "Anatomy of an Attack."
* Sections 1.4 & 1.5: Fundamentals and governing frameworks.
* Section 1.6: Implementation of defensive measures.
* Section 1.7: Compliance and regulatory environments.
* Sections 1.8 & 1.9: Career paths and future industry trends.
* Section 1.10: Summary and conclusions.

### Understanding Cyber Threats

The recent surge in cyberattacks is a direct consequence of the rapid digitalization of social and professional life. The mass adoption of cloud computing, e-commerce, and virtualized environments has provided adversaries with a target-rich environment. Because computer systems possess inherent vulnerabilities at the software, hardware, and network levels, adversaries are constantly "pining" for unpatched weaknesses to exploit.

A cyberattack occurs the moment a threat actor successfully leverages a flaw in firmware, software, or network protocols. These incursions manifest in numerous forms—ranging from Denial of Service (DoS) attacks that paralyze infrastructure to Social Engineering schemes that exploit human psychology. In a highly digitized society, these threats represent a Tier-1 risk to the stability of private corporations, civil institutions, and military organizations alike.

#### Malware

Malware (a portmanteau of "malicious software") refers to any code or application specifically engineered to disrupt system operations, compromise data, or gain unauthorized access. While the technical structure of malware varies, it is primarily defined by its intent: acting against the requirements and safety of the system owner.

Modern malware has evolved into a versatile tool for both independent cybercriminals and state-sponsored actors. It is frequently deployed to exfiltrate intellectual property, encrypt data for ransom, or conduct covert surveillance. Whether its goal is financial extortion or political sabotage, malware remains the most pervasive threat in the cybersecurity landscape.

#### Hijackware (Browser Hijacking)

Hijackware is a type of malicious software that modifies a user's computer or mobile device settings without their permission. This is most commonly seen in web browsers, where the malware changes the default homepage, search engine, or error pages to those of the attacker's choosing.

**Common Characteristics**

* Malicious Redirects: Automatically sending a user to a predetermined website (often containing further malware or fraudulent ads) regardless of what they typed in the address bar.
* Toolbar Injection: Installing unwanted toolbars that are difficult to remove and track user browsing habits.
* DNS Hijacking: Modifying the system's DNS settings to ensure the user always reaches the attacker's servers.

#### Crimeware

Crimeware is a class of malware designed specifically to automate cybercrime. Unlike general malware that might be used for mischief or protest, crimeware is built for financial gain. It often serves as a "toolkit" for non-technical criminals to launch sophisticated attacks.

* Automation: It automates the theft of login credentials and financial information.
* Delivery: Often distributed via "Exploit Kits" that identify vulnerabilities in a visitor's browser automatically.
* Persistence: Designed to remain on a system for long periods to continuously siphon data or resources.

#### RAM Scrapers

RAM Scrapers (or Memory Scrapers) are a specialized type of malware that harvests data while it is being processed in the system's Random Access Memory (RAM). This is particularly dangerous because many security protocols encrypt data while "at rest" (on a hard drive) or "in transit" (moving over a network), but the data must be decrypted in the RAM to be processed.

* Point-of-Sale (PoS) Attacks: These are most commonly used to steal credit card track data from retail payment terminals.
* Volatile Data Theft: Once the computer is turned off, the evidence in the RAM is often lost, making these attacks difficult to investigate forensically.

#### Web Skimmers (Digital Skimming)

Also known as "Magecart" attacks, web skimmers are malicious scripts injected into e-commerce websites, typically on checkout pages. They act as a digital version of the physical "skimmers" found on ATMs.

* Data Interception: As a customer enters their credit card number and CVV into a legitimate website, the script silently copies the data and sends it to the attacker's server.
* Supply Chain Risk: These attacks often occur by compromising a third-party JavaScript library that many websites use (such as a chat bot or analytics tool).

#### SQL Injection (SQLi)

While SQL Injection (SQLi) is a technique, "SQLi Malware" refers to automated tools and scripts used to exploit vulnerabilities in a web application's database layer.

* The Goal: To bypass authentication, view sensitive user tables, or even gain administrative control over the database server.
* The Mechanism: It inserts malicious SQL statements into entry fields for execution (e.g., entering code into a "Username" box).

#### Rogue Security Software

Commonly referred to as "Scareware," this malware uses social engineering to shock or frighten users into thinking their computer is infected with hundreds of viruses.

* The Scam: A pop-up appears with a realistic-looking "Windows System Scan" showing numerous threats.
* The Goal: To trick the user into "purchasing" a full version of the fake antivirus to "clean" the non-existent threats, thereby gaining the user's credit card information.

#### Social Engineering: The "Human Hacking"

While technically a methodology rather than a software type, Social Engineering is the foundation of most successful cyberattacks. It relies on psychological manipulation to trick people into divulging confidential information.

* Phishing: Sending fraudulent communications that appear to come from a reputable source (Email).
* Smishing & Vishing: Phishing via SMS (text) or Voice (phone calls).
* Pretexting: Creating a fabricated scenario (e.g., "I'm from the IT department and we need to reset your password") to steal data.

#### Mobile Malware

With the rise of smartphones, malware has transitioned to mobile operating systems (iOS and Android). These apps often masquerade as legitimate utilities—like battery doctors, wallpaper apps, or games—to gain extensive permissions.

* Permission Abuse: Requesting access to the microphone, camera, contacts, and SMS messages to spy on the user.
* Premium SMS Scams: Forcing the phone to send messages to "premium-rate" numbers, charging the user's phone bill directly.

### The Anatomy of an Attack

Understanding individual threats is only the first step. To defend a network, one must understand the lifecycle of an attack, often referred to as the Cyber Kill Chain. This process typically follows these stages:

1. Reconnaissance: Researching and identifying targets.
2. Weaponization: Coupling malware with an exploit into a deliverable payload.
3. Delivery: Transmitting the weapon to the target (via email, web, or USB).
4. Exploitation: Triggering the malware's code to exploit a vulnerability.
5. Installation: Installing a backdoor or persistence mechanism.
6. Command & Control (C2): Gaining outside control of the system.
7. Actions on Objectives: Stealing data, destroying systems, or encrypting files.

**Types of Malware (Overview)**

1. Viruses: Self-replicating code.
2. Worms: Network-spreading program.
3. Trojan Horse: Deceptive software masquerading as legitimate.
4. Backdoor: Unauthorized system access.
5. Ransomware: Data encryption for extortion.
6. Spyware: Secret monitoring and data collection.
7. Grayware (PUP): Unwanted software that slows systems.
8. Adware: Advertising-supported software.
9. Keyloggers: Recording keystrokes to steal credentials.
10. Rootkit: Deep system infiltration for remote control.
11. Fileless Malware: Memory-resident attacks using system tools.
12. Malvertising: Malicious code spread through online ads.
13. Botnets: Networks of remotely controlled "zombie" devices.
14. Hijackware: Taking over browser or system settings.
15. Crimeware: Tools designed to automate financial crimes.
16. Mobile Malware: Malicious applications targeting smartphones.
17. Social Engineering/Phishing: Psychological manipulation.
18. RAM Scrapers: Theft of data directly from system memory.
19. Web Skimmers: Theft of payment info from e-commerce sites.
20. Rogue Security Software: Fake antivirus scams.
21. SQL Injection Malware: Database exploitation tools.
22. Cryptojacking: Unauthorized use of resources to mine crypto.
23. Exotics: Specialized ransomware patterns.
24. Hybrid Malware: Combo threats (e.g., a Worm-Trojan).
25. Wipers: Software intended for permanent data destruction.

#### Virus

The virus is the oldest, most common form of malware. A computer virus is a type of malicious software (malware) that replicates itself by modifying other computer programs and inserting its own code. These programs spread via email attachments, file downloads, or USB drives, aiming to steal data, destroy files, or disrupt system performance.

**Types of Computer Viruses**

* Boot Sector Virus: Affects the master boot record (MBR).
* Direct Action Virus: Attacks specific file types (.exe, .com).
* Resident Virus: Hides in the RAM.
* Macro Virus: Targets applications like MS Word.
* Polymorphic Virus: Changes its code to evade detection.
* Web Scripting Virus: Uses malicious code on websites.

**Famous Examples of Computer Viruses**

* ILOVEYOU (2000): Disguised as a "love letter."
* Stuxnet (2010): Sophisticated worm targeting industrial systems.
* Melissa (1999): A macro virus that sent itself to email contacts.

#### Trojan Horse

This program hides inside seemingly innocuous, legitimate software. Unlike viruses, Trojans do not self-replicate; they rely on user deception. Once activated, they can steal data, damage systems, or create backdoors for hackers.

**Common Types of Trojan Horses**

* Remote Access Trojan (RAT): Provides full administrative control.
* Banking Trojan: Designed to steal financial credentials.
* Fake Antivirus Trojan: Mimics security software to trick users into paying.

**Famous Examples of Trojan Horses**

* Zeus (Zbot): Infamous banking Trojan.
* Tiny Banker (Tinba): Stealthy Trojan targeting financial institutions.

#### Drive-By Download

This attack entails the discreet insertion of a malicious script into a website's code. It occurs when malware is installed without the user's consent, often just by visiting an infected page.

**Types of Drive-By Downloads**

* Unauthorized Downloads: Automatic installation via browser exploits.
* Malvertising: Malicious code hidden within online ads.
* Watering Hole Attacks: Targeting sites a specific group of users frequent.

#### Logic Bomb

This type of malware is added to an application and triggered by a specific event, such as a logical condition or a specific time and date.

* UBS Incident (2006): Administrator caused $3.1 million in damages.
* Siemens Case (2019): Software programmed to malfunction for repair work.

#### Worms

A computer worm is a self-replicating type of malware that spreads across networks without needing a host file or human intervention.

**Types of Computer Worms**

* Email Worms: Spread via contact lists.
* Network Worms: Scan for vulnerabilities in protocols.

**Famous Examples of Computer Worms**

* Morris Worm (1988): First major worm to disrupt the internet.
* SQL Slammer (2003): Infected 75,000 victims within 10 minutes.
* WannaCry (2017): A ransomware worm using the EternalBlue exploit.

#### Adware

Adware (advertisement-supported software) automatically displays or downloads advertisements. While some is legitimate, malicious adware acts as malware by gathering user data or hijacking browsers.

**Types of Adware**

* Browser Hijackers: Alter browser settings to redirect users.
* Spyware-Adware: Records browsing habits to serve targeted ads.

#### Hijackware

Hijackware modifies a user's computer or mobile device settings without permission, most commonly seen in web browsers changing the homepage or search engine.

#### Crimeware

Crimeware is a class of malware designed specifically to automate cybercrime for financial gain, often including "toolkits" for non-technical criminals.

#### Mobile Malware

Malware that targets mobile operating systems (iOS and Android), often masquerading as utilities like "battery doctors" to gain extensive system permissions.

#### Social Engineering and Phishing

Also known as "Human Hacking," this relies on psychological manipulation to trick people into divulging confidential information.

#### RAM Scrapers

Specialized malware that harvests data while it is being processed in the system's Random Access Memory (RAM), often targeting unencrypted Point-of-Sale (PoS) data.

#### Web Skimmers (Digital Skimming)

Malicious scripts (like Magecart) injected into e-commerce checkout pages to steal credit card information in real-time.

#### Rogue Security Software

"Scareware" that uses fake security alerts to frighten users into purchasing fraudulent software or revealing credit card details.

#### Cryptojacking

Malware that hijacks a device's processing power to mine cryptocurrency for the attacker, leading to system slowdowns and high energy costs.

#### Wipers

Wipers are designed for the sole purpose of permanent data destruction. Unlike ransomware, there is no decryption key offered; the data is simply erased or rendered unrecoverable.
