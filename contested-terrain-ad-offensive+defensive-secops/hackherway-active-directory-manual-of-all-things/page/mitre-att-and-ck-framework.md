# MITRE ATT\&CK Framework

\### What Is the MITRE ATT\&CK Framework?

MITRE is a government-backed not-for-profit organization that conducts federally funded cybersecurity research to support defensive IT security across all sectors, including government agencies and defense contractors. The MITRE ATT\&CK (Adversarial Tactics, Techniques, and Common Knowledge) framework is a free and open knowledge base of cybersecurity information first released in 2018. It is designed to help both cybersecurity defenders and offensive security professionals gain Cyber Threat Intelligence (CTI) insights for planning and designing cyber strategies, facilitating communication by providing a common reference vocabulary.

\### MITRE ATT\&CK Matrix

The complete MITRE ATT\&CK framework is divided into three main variants, each containing a subset of tactics, techniques, and procedures (TTP) that apply to specific target IT environments. Each variant is known as a Matrix, valuable for both attackers and defenders.

The three primary Matrices in the ATT\&CK framework are:

1\. \*\*Enterprise Matrix\*\*

2\. \*\*Mobile Matrix\*\*

3\. \*\*ICS (Industrial Control System) Matrix\*\*

The Enterprise and Mobile Matrices are further subdivided into sub-Matrices filtered to contain only those TTP relevant to each environment.

\#### Enterprise ATT\&CK Matrix

The Enterprise ATT\&CK Matrix contains 14 tactics that apply to cyberattacks against enterprise infrastructure. This Matrix can be further divided into 7 sub-Matrices focusing on specific areas:

\- \*\*PRE Matrix\*\*: Focuses on pre-attack activities, offering attackers insights into initial planning, while helping defenders understand early signs of compromise.

\- \*\*Operating Systems Matrices\*\*: Includes tactics tailored for specific operating systems such as Windows, Linux, and macOS, aiding attackers in exploiting system-specific vulnerabilities and defenders in patching them.

\- \*\*Network Matrix\*\*: Covers tactics relevant to network infrastructure attacks, providing attackers with network penetration strategies and defenders with methods to secure their networks.

\- \*\*Cloud Matrix\*\*: Deals with tactics used against cloud infrastructure, giving attackers avenues to exploit cloud environments and defenders strategies to protect them.

\- \*\*Containers Matrix\*\*: Addresses attacks targeting containerized environments, helping attackers find vulnerabilities in container setups and defenders to secure them.

\#### Mobile ATT\&CK Matrix

The Mobile ATT\&CK Matrix contains 14 tactics but differs slightly from the Enterprise Matrix:

\- \*\*Network Effects\*\*: This replaces "Reconnaissance" and provides attackers with methods to intercept data in transit over networks, while defenders gain insights into securing network communications.

\- \*\*Remote Service Effects\*\*: Replaces "Resource Development" and focuses on compromising mobile apps and services, offering attackers detailed methods and defenders countermeasures to protect against them.

This Matrix focuses on target mobile operating systems (iOS and Android) and highlights the unique security challenges associated with mobile devices for both attackers and defenders.

\#### Industrial Control Systems (ICS) ATT\&CK Matrix

The ICS ATT\&CK Matrix contains 12 tactics applicable to cyberattacks against ICS. It includes unique tactics not found in the other Matrices:

\- \*\*Inhibit Response Function\*\*: Involves actions that inhibit safety, protection, quality assurance, or operator intervention functions, useful for attackers to disrupt operations and defenders to detect and prevent such disruptions.

\- \*\*Impair Process Control\*\*: Entails activities that change configuration parameters or firmware to impair process control, causing damage to physical infrastructure, providing attackers with sabotage methods and defenders with protection strategies.

This Matrix does not include the “Credential Access” or “Exfiltration” tactics present in the Enterprise and Mobile Matrices.

\### ATT\&CK Tactics, Techniques, and Procedures

A complete offensive cyber campaign consists of several stages and requires combining multiple tactics to achieve its goal. MITRE ATT\&CK uses the TTP perspective to organize cybersecurity knowledge into a hierarchical framework.

\#### ATT\&CK Tactics

Tactics represent the high-level objectives that adversaries aim to achieve during various phases of an attack. Each tactic encompasses multiple techniques. Here are the detailed tactics across different matrices:

\- \*\*Reconnaissance (Enterprise, ICS)\*\*: Gathering information needed to plan future operations, crucial for attackers to understand their targets and for defenders to recognize early warning signs.

\- \*\*Resource Development (Enterprise, ICS)\*\*: Establishing resources to support operations, essential for attackers to prepare their tools and infrastructure, and for defenders to disrupt these preparations.

\- \*\*Initial Access\*\*: Techniques used to gain an initial foothold within a network, showing attackers how to breach systems and defenders how to secure entry points.

\- \*\*Execution\*\*: Techniques that result in adversary-controlled code running on a local or remote system, detailing attack methods and defensive measures.

\- \*\*Persistence\*\*: Techniques that adversaries use to maintain their foothold, helping attackers remain undetected and defenders to identify lingering threats.

\- \*\*Privilege Escalation\*\*: Techniques that adversaries use to gain higher-level permissions, showing attackers how to escalate privileges and defenders how to prevent it.

\- \*\*Defense Evasion\*\*: Techniques to avoid detection and mitigation, useful for attackers to bypass security measures and for defenders to improve detection capabilities.

\- \*\*Credential Access (Enterprise, Mobile)\*\*: Techniques for stealing account names and passwords, providing attackers with methods to gain credentials and defenders with ways to protect them.

\- \*\*Discovery\*\*: Techniques used to gain knowledge about the system and internal network, aiding attackers in mapping networks and defenders in detecting reconnaissance activities.

\- \*\*Lateral Movement\*\*: Techniques that allow an adversary to move through a network, helping attackers spread within a network and defenders to detect and block lateral movement.

\- \*\*Collection\*\*: Techniques used to gather information and data, showing attackers how to collect valuable data and defenders how to secure it.

\- \*\*Command and Control\*\*: Techniques used to communicate with compromised systems, detailing how attackers maintain control and how defenders can disrupt these communications.

\- \*\*Exfiltration (Enterprise, Mobile)\*\*: Techniques used to steal data from a network, providing attackers with data exfiltration methods and defenders with strategies to prevent data loss.

\- \*\*Impact\*\*: Techniques that disrupt availability or compromise integrity by manipulating business and operational processes, helping attackers maximize damage and defenders to mitigate impact.

\- \*\*Network Effects (Mobile-only)\*\*: Interception and tampering of data-in-transit over networks, showing attackers methods and defenders how to secure communications.

\- \*\*Remote Service Effects (Mobile-only)\*\*: Compromising mobile apps and services to achieve objectives, providing attackers with strategies and defenders with protective measures.

\- \*\*Inhibit Response Function (ICS-only)\*\*: Actions that inhibit safety, protection, quality assurance, or operator intervention functions, crucial for attackers to disrupt and defenders to secure ICS environments.

\- \*\*Impair Process Control (ICS-only)\*\*: Activities that change configuration parameters or firmware to impair process control, causing damage to physical infrastructure, providing attackers with sabotage techniques and defenders with protection strategies.

\#### Techniques

Techniques are specific methods used by adversaries to achieve their tactical goals. Each tactic can involve multiple techniques. For example, the "Initial Access" tactic might include techniques such as:

\- \*\*Phishing\*\*: Sending fraudulent emails to trick recipients into revealing sensitive information, showing attackers effective phishing methods and defenders how to recognize and block them.

\- \*\*Exploit Public-Facing Applications\*\*: Taking advantage of vulnerabilities in web applications, providing attackers with exploitation strategies and defenders with patching and monitoring techniques.

\#### Sub-techniques

Sub-techniques are more specific forms of techniques that provide detailed views of how an adversary might achieve their objective. For instance, within the "Phishing" technique, sub-techniques could include:

\- \*\*Spear Phishing via Email\*\*: Sending targeted emails to specific individuals, useful for attackers to craft precise phishing campaigns and defenders to train staff against such threats.

\- \*\*Spear Phishing via Link\*\*: Including malicious links in emails, showing attackers effective link placement and defenders how to detect and block malicious links.

\#### Procedures

Procedures are the specific ways in which adversaries implement the techniques. These are real-world examples or case studies of techniques in action. For instance, a procedure for "Spear Phishing via Email" might detail how a specific group conducted a campaign using this method, helping attackers understand successful methods and defenders to analyze and learn from past attacks.

\### MITRE D3FEND

MITRE D3FEND is a knowledge base—defined as a "knowledge-graph" by MITRE—that serves as a library of defensive cybersecurity countermeasures, components, and their associations and capabilities. It is complementary to the MITRE ATT\&CK framework of cybercriminals' tactics, techniques, and procedures (TTP), helping defenders to build robust security measures.

\### MITRE ATT\&CK vs. the Cyber Kill Chain

The Cyber Kill Chain is a cyberattack framework released in 2011 by Lockheed Martin. Like MITRE ATT\&CK, the Cyber Kill Chain categorizes all cyberattack behaviors into sequential tactics.

\#### 7 Stages of the Cyber Kill Chain

1\. \*\*Reconnaissance\*\*: Gathering information on the target, essential for attackers and an early detection point for defenders.

2\. \*\*Weaponization\*\*: Creating a deliverable malicious payload, crucial for attackers and a point for defenders to identify weaponized files.

3\. \*\*Delivery\*\*: Transmitting the payload to the target, showing attackers delivery methods and defenders how to intercept them.

4\. \*\*Exploitation\*\*: Triggering the payload to exploit a vulnerability, providing attackers with exploitation techniques and defenders with patching strategies.

5\. \*\*Installation\*\*: Installing malware on the target system, helping attackers establish presence and defenders to detect and remove malware.

6\. \*\*Command and Control\*\*: Establishing a remote command channel, crucial for attackers to control compromised systems and for defenders to disrupt these channels.

7\. \*\*Actions on Objectives\*\*: Completing the mission objectives, such as data theft or system destruction, helping attackers achieve goals and defenders to prevent them.

The Cyber Kill Chain differs fundamentally from the MITRE ATT\&CK framework by asserting that all cyberattacks must follow a specific sequence of tactics to achieve success; MITRE ATT\&CK makes no such claim. Another

difference is that the Cyber Kill Chain posits that breaking any phase of the “kill chain” will stop an attacker from achieving their goal, thus protecting the defender. MITRE ATT\&CK, on the other hand, is a comprehensive knowledge base that correlates environment-specific cybersecurity information along a hierarchy of tactics, techniques, procedures, and other common knowledge, such as attribution to specific adversarial groups.

\### How to Use the MITRE ATT\&CK Framework

Because ATT\&CK includes both a broad, high-level perspective and granular, low-level information, security teams can use it to bridge knowledge gaps between distinct cyberattack objectives and detailed information. This makes it a powerful tool for cybersecurity education and planning enterprise security programs, providing valuable insights for both attackers and defenders.

\### MITRE ATT\&CK Use Cases

\- \*\*Threat Modeling\*\*: Organizations can use the framework to better understand potential threat scenarios against their infrastructure, helping defenders to identify and mitigate threats and attackers to plan their strategies.

\- \*\*Enhanced Incident Response\*\*: By aligning real-world incidents to the ATT\&CK matrix, responders can categorize and respond to threats in a structured way, providing attackers insights into successful attacks and defenders into response strategies.

\- \*\*Improved Red and Blue Teaming\*\*: The matrix can be used for emulating adversarial behaviors (red teaming) and enhancing detection capabilities (blue teaming), helping attackers refine their techniques and defenders to improve their defenses.

\- \*\*Security Posture Assessment\*\*: Organizations can evaluate their defensive measures against the listed techniques to identify potential areas for improvement, helping defenders to strengthen their security and attackers to find gaps.

Because it is a comprehensive knowledge base of cyberattack information, ATT\&CK can serve as a checklist of attack goals and methodologies. You can use this checklist to justify implementing security controls, ensuring they are comprehensive and offer some degree of protection against all elements that comprise real-world cyberattacks.

ATT\&CK can also be used by penetration testers, red teams, and security product testers to emulate realistic cyberattacks. ATT\&CK enables simulated adversaries to understand the attack landscape and apply the same tactics and techniques as real-world attackers.

\### FAQ

\*\*What Does MITRE ATT\&CK Mean?\*\*

ATT\&CK stands for Adversarial Tactics, Techniques, and Common Knowledge.

\*\*What is the MITRE ATT\&CK Framework?\*\*

MITRE ATT\&CK is a free and open knowledge base of cyberattack strategies and related information designed to help cybersecurity analysts and other stakeholders gain Cyber Threat Intelligence (CTI) insight and facilitate communication about offensive and defensive cybersecurity.

\*\*What is the MITRE ATT\&CK Matrix?\*\*

The MITRE ATT\&CK Matrix is a hierarchical framework of attack tactics and techniques that comprise cybercriminals’ individual goals and strategies. There are three primary ATT\&CK Matrices, each addressing distinct environments: Enterprise, Mobile, and Industrial Control Systems.

\### How Does the MITRE ATT\&CK Framework Help Enterprises?

When paired with a comprehensive cybersecurity platform, the MITRE ATT\&CK Framework helps enterprises to address cyber threats and breaches using proven methods and workflows. By investigating the early-stage tactics used by adversaries, enterprises can mitigate attacks more efficiently and effectively, ensuring their networks remain secure.

\### Why Is It Important to Cover These Bases?

Adversaries are constantly evolving, making it essential for enterprises to stay one step ahead to keep their networks safe and secure. While breaches are an unfortunate and inevitable truth, following the MITRE ATT\&CK framework can help you quickly and effectively remove adversaries from your networks to minimize damage.

The MITRE ATT\&CK framework stands as a trusted and comprehensive guideline for understanding and countering cyber adversaries' methods. By cataloging the lifecycle of cyberattacks and detailing adversaries' objectives and techniques, the framework helps enterprises anticipate threats and respond adeptly to potential breaches. Integrating this framework with robust cybersecurity solutions enables enterprises to fortify their defenses and adapt to the constantly changing digital threat landscape. In the high-stakes realm of cybersecurity, staying informed, vigilant, and adaptive with tools like the MITRE ATT\&CK framework can make the difference between a minor setback and a significant breach.
