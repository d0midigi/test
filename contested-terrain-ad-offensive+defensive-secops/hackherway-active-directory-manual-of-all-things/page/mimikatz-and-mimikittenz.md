# Mimikatz and Mimikittenz

Mimikatz and Mimikittenz

With the emergence of numerous credential dumping tools, Mimikatz has become an extremely potent tool for attackers targeting Windows users. It allows intruders to retrieve plain text passwords and dump password hashes from memory. This paper will provide a comprehensive overview of Mimikatz's capabilities and potential impacts. It will cover several Mimikatz modules used for credential dumping and conclude with strategies and techniques to prevent Mimikatz attacks.

Mimikatz, created by Benjamin Delpy (also known as gentilkiwi), was first introduced in 2011. Delpy demonstrated significant vulnerabilities in Microsoft authentication protocols, revealing how susceptible they were to attacks. Attackers exploit these vulnerabilities in Windows systems to gain access to internal storage. Benjamin Delpy's creation, Mimikatz, has become one of the most widely used and downloaded tools among hackers.

Mimikatz offers a variety of modules to gather and exploit Windows credentials on targeted systems. These modules can capture passwords in clear text, LM (LAN Manager) hashes, NTLM (New Technology LAN Manager) hashes, and Kerberos tickets, including Golden and Silver Kerberos Tickets. Mimikatz is compatible with all Windows versions from Windows XP onwards, making it a versatile tool for attackers.

2.1 Active Directory

Active Directory (AD) is Microsoft's directory service, essentially functioning as a database that runs on Windows Server. It allows administrators to manage access to network resources and user permissions. Everything in Active Directory is stored as an object, which can be a group, user, application, or device. This object-based storage makes it easier for administrators to search and manage information across the network.

2.2 Malware Taxonomy

2.2.1 Malware Categories

Botnets: Botnets allow attackers to access systems on a large scale by infecting multiple computers that can be controlled from a central Command and Control (C2C) server. They often spread like worms and are typically made up of Internet Relay Chat (IRC) bots, which accept commands such as "DDOS" to launch attacks or "run/exploit" to open applications on the targeted system.

Spyware: Spyware monitors or tracks its targets to steal data. It collects information from the target system and sends it to the attacker. Examples include keyloggers, sniffers, and spybots.

Keyloggers: Collect keyboard logs to gather sensitive information like bank details, passwords, and confidential messages.

Sniffers: Track and monitor internet traffic in real-time, capturing all data sent or received by the computer.

Spybots: Enter a computer system to collect and transfer information to a third party.

Rootkits: Designed to modify the operating system and create a backdoor for remote access, rootkits operate in a way that makes them difficult to detect. They are often combined with other malware to conceal their code and may modify monitoring tools, making detection challenging.

Backdoors: Malicious code that gains unauthorized access to a computer system without user permission. Once executed, it connects the attacker to the target computer.

2.3 Malware Detection Approaches

2.3.1 Signature-Based Detection

Signature-based detection involves identifying malware by its unique signature, a set of bits that defines its structure. While this method is quick and effective for known malware, it cannot detect zero-day threats or new malware variants.

2.3.2 Behavior-Based Detection

This approach tracks the activities of a sample program, classifying it as malicious or benign based on observed behaviors. It involves extracting behaviors, creating attributes, and using machine learning algorithms to determine if the program is harmful. System calls, API calls, and changes in files or registry are used to analyze behavior.

2.3.3 Features-Based Detection

Heuristic-based detection employs rules and machine learning to detect malware. It involves teaching the system using specific features and then testing data to identify anomalies. This method is effective for detecting new malware but may result in high false positive and false negative rates.

2.3.4 Model-Learning Based Detection

This method uses linear temporal logic formulas to identify relationships between features, classifying software as malicious or benign. It is effective against stealth and packing techniques.

2.3.5 Deep-Learning Based Detection

Deep learning, a subset of artificial intelligence, is used in malware detection and classification. It significantly reduces feature dimensions but is vulnerable to evasion attacks. While promising, deep learning requires further research for broader application in malware detection.

2.4 Malware Detection for Various Devices

Malware detection across different platforms involves monitoring activities and classifying them as normal or dangerous based on machine learning algorithms.

2.4.1 Malware Obfuscation Techniques

Malware researchers use obfuscation techniques to conceal their code, making it difficult for victims and antivirus software to detect or understand the malware.

2.4.2 Malware Detectors

Malware detectors are programs that use rules, hashes, and signatures to identify malware. Detection methods include signature-based and behavior-based approaches.

\### 2.2 NTDS.dit

The NTDS.dit file can be considered the heart of Active Directory, as it stores user accounts and other essential data. This file, used by AD, is often referred to as a database. It contains information about user objects, including their various attributes, groups, and group memberships. Additionally, it stores the password hashes for all users in the domain. Both LAN Manager (LM) and NT hashes of passwords are generated by Windows and stored in the Local Security Accounts Manager (SAM) database (\`C:\Windows\System32\config\SAM\` file) or in the Active Directory (\`C:\Windows\NTDS\NTDS.dit\` file).

\### 2.3 Kerberos

Kerberos is a well-known computer security protocol that authenticates service requests across a network between two or more hosts, often over the Internet. It uses secret key cryptography and a trusted third party for client-server authentication and user identity verification. Kerberos is designed to avoid storing passwords locally and sending passwords over the Internet, providing mutual authentication, meaning both the server's and user's authenticity are verified.

\### 2.4 LSASS and LSA

LSASS stands for Local Security Authority Server Service, and LSA stands for Local Security Authority. Within Windows, the \`lsass.exe\` executable is responsible for preserving and saving user credentials in memory for both local and domain users. LSASS is an implementation of the Local Security Authority, with "LSA" representing the concept and "lsass.exe" being the process that implements many of the LSA functions.

\### 2.5 KDC

The Key Distribution Center (KDC) is a critical component in cryptography, responsible for issuing keys to users in a network that shares sensitive or confidential data. Whenever a connection is established in a network, the KDC is requested by both parties to generate a unique password, which is then used for verification by the end systems. The KDC employs symmetric encryption, allowing access to more than two systems in a network by creating a unique ticket-type key for secure connection establishment. This key facilitates the secure sharing, movement, and transfer of data and information. Before communication begins, the Key Distribution Center acts as the primary server responsible for this process.
