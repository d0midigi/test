# Pass the Hash Attack

Pass-the-Hash (PtH) Attack

This section will teach you what a Pass-the-Hash (PtH) attack is and how to perform a PtH attack yourself.

As hackers, we have various lateral movement techniques at our disposal. One of the most commonly used is the PtH attack; you should know how to perform this attack and also know how to protect against it.

If you are on the offensive side, you can use this attack to jump between compromised machines within an Active Directory domain and its supporting infrastructure. If you are on the defensive side, you can use your understanding of this attack technique to secure your Active Directory domain and infrastructure and lock down access to your most valuable assets.

Let’s explore what passing the hash means, how to obtain a hash, and how to perform a PtH attack using real-world hacking tools.

What is Passing the Hash?

Before passing hashes and compromising machines, you must first understand exactly what a hash is. A hash refers to a fixed-size numerical value computed from input data that can be any size. This input data can be a file, a password, or any other piece of information.

A hashing function will take input data, run it through a mathematical algorithm, and produce a unique hash value that is a fixed size. Hashing is a one-way computation. You cannot retrieve the input data from its hash value. This is important because it provides an extra layer of security, or defense in depth. If a machine’s password database is compromised, you cannot determine a user’s password from its hash value, which is why passwords are stored as hashes.

To log into a machine, a user will enter their password in cleartext, and the machine will use the same hashing function it used to create a hash of their original password with the one they are trying to authenticate with. If the password hashes match, then the user is allowed access.

New Technology LAN Manager (NTLM) Authentication

In modern Windows Active Directory environments, Kerberos is the default authentication protocol that Microsoft has adopted and expanded on to provide secure authentication using a ticket-based system; however, many Active Directory environments support legacy systems by allowing NT LAN Manager (NTLM) authentication.

NTLM uses what’s known as a _**challenge/response**_ mechanism for user authentication:

* **Steps 1 and 2:** When a user attempts to access a network resource, the server will challenge the user by sending a random value.
* **Step 3:** The user’s computer will then encrypt this challenge using the user’s password hash and send this encrypted challenge back as a response.
* **Steps 4-5:** The server will verify the response by sending it to the Domain Controller, who will compare them with the stored password hash and determine if that user should have access.
* **Step 6:** The server will send a message back to the user to either confirm or deny their access to the network resource.

![](<../.gitbook/assets/0 (59).png>)

The NTLM authentication protocol used in Microsoft environments has gone through many revisions, each improving the security of the previous. Today, NTLMv2 Session Security is used within modern Active Directory environments when Kerberos authentication fails.

NTLM authentication is used when a client authenticates to a server by IP address (instead of a hostname), if the user attempts to authenticate to a hostname not registered on the Active Directory Domain Name Service ( AD DNS) server, or if a third-party application chooses to use NTLM instead of Kerberos.

For instance, if you want to access a file share in an Active Directory environment, you can use the server’s DNS hostname or IP address to connect to it. If you use the DNS hostname, then Kerberos authentication will be used; however, NTLM authentication will be used if you use the server’s IP address.

Under the hood, this will involve you providing the NTLM hash of your password to the server and it verifying this hash matches the hash it has stored for authenticated users. You will not see this. You will only be asked to provide your user credentials (cleartext password) to authenticate and access the file share.

Pass-the-Hash (PtH) Attacks

In a Pass-the-Hash (PtH) attack, you authenticate to a remote system or service in an Active Directory environment using a target user’s NTLM hash instead of the user’s plaintext password. You then obtain the NTLM hash either by capturing it on the network or by extracting it from a machine they have compromised.

This attack only works when Kerberos is not used for authentication and the server or service the attacker tries to connect to uses NTLM authentication. Another requirement is that _**Server Message Block (SMB)**_ is open (port 445), and the Windows _**File Sharing and Print Sharing**_ feature is enabled. This setup is common in internal enterprise environments as it allows employees to easily share work documents to collaborate on projects.

_The Pass-the-Hash (PtH) attack works for Active Directory domain accounts and the built-in local administrator account for the machine you are trying to authenticate to; however, it cannot be used to authenticate as any other local administrator account._

For instance, if John Smith is a user on Workstation 1 and you want to access this machine, you would first capture John Smith’s NTLM hash, then you must verify that SMB and the Windows **File Sharing and Print Sharing** feature are enabled in the Active Directory environment you want to attack. If these requirements are fulfilled, you can use John Smith’s NTLM has to authenticate to Workstation 1 and impersonate them using various hacking tools.

![Pass the Hash Attacks](<../.gitbook/assets/1 (44).png>)

Obtaining the Hash

First, you must obtain an NTLM hash to perform a PtH attack. This can be done by either capturing the hash on the network or by stealing the hash from a machine you have compromised. First. Let’s look at capturing the hash from the network using the **Responder.**

Responder

_The demonstrations in this section use a vulnerable Windows Active Directory environment. You can learn to create your own virtual hacking environment by following Chapter X and follow along._

**Responder** is a tool commonly used in internal penetration testing, ethical hacking, and red teaming exercises to test the security of an organizaiton’s internal network protocols. The tool can capture and relay authentication credentials in a Windows Active Directory environment. You can use the Responder to capture NTLM hashes as they pass around the network for authentication in _**Link-Local Multicast Name Resolution (LLMNR)**_ requests.

At this point, you may ask what LLMNR requests are. LLMNR is a network protocol used in Active Directory environments to identify hosts on a local network when DNS resolution fails. It acts as a fallback mechanism and allows client machines to interact with servers without needing a DNS server.

LLMNR, however, is vulnerable. It has the ability to leak usernames and NTLM hashes when responding to LLMN requests. If a malicious actor positions themselves on the same network as the target machine and intercepts the LLMNR traffic between the target and the server, they can then potentially steal the target user’s NTLM hash. They can also try to crack this hash offline to get the target user’s password or even use the hash in a PtH attack.

This attack is known as an LLMNR Poisoning attack and is demonstrated in the graphic below:

![Obtaining the Hash](<../.gitbook/assets/2 (38).png>)

LLMNR Poisoning in Action with Responder

The Responder comes installed on Kali Linux by default; however, before performing an LLMNR poisoning attack with Responder, you need to meet the following requirements:

* You need to be on the same network as your target machine.
* You need to have the capability of sniffing network packets.

Now you can run the following command to start the Responder tool:

sudo responder -I eth0 -v

![Sudo responder](<../.gitbook/assets/3 (6).jpeg>)

This command will start the Responder on your eth0 network interface (-I) and in verbose mode (-v) provide more output.

Now you have to wait for an event to occur that DNS cannot resolve. For instance, when a user tries to connect to a machine via SMB, SQL, FTP, SMTP, etc, but uses a name that the local DNS server cannot resolve or uses an IP address. This will trigger the machine to send an LLMNR request to find the machine or resource it is trying to access. Responder will capture this LLMNR request and display the NTLM hash for you to use.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/4 (2).jpeg>)

Here I have tried to access the C: drive of the test machine from Workstation1 as the mindhack-admin user. Workstation1 will make a DNS request to the Active Directory DNS server to find out where the test machine is located; however, this machine does not exist. So, the DNS request will fail. Now, Worksation1 will send out an LLMNR request as a fallback. Responder can capture this LLMNR request and steal the user’s NTLM hash

![](<../.gitbook/assets/5 (27).png>)

Responder and Mimikatz

Another way to get your hands on an NTLM hash is to steal it from a machine you have compromised. On Windows machines, NTLM hashes are typically stored in the Security Account Manager (SAM) database. This is part of the Windows Registry and contains various pieces of user account information. You can dump the information in this database and steal NTLM hashes by interacting with the Local Security Authority Subsystem Service (LSASS) process.

An infamous tool for stealing credential information from Windows machines is Mimikatz. It is a powerful post-exploitation tool capable of dumping credentials and performing various lateral movement techniques. One of the tool’s features is extracting passwords and other authentication methods from a target machine, either stored locally or running in memory.

Credential Dumping in Action with Mimikatz

Mimikatz is installed on Kali Linux by default. To extract password hashes using Mimikatz, you need to fulfill the following requirements:

* You need SYSTEM or local administrative access for permissions to interact with the LSASS process.
* You must disable Microsoft Windows Defender’s _Real Time_ protection on the target machine.

Now you can start the Mimikatz console and engage the SeDebugPrivilege so that you can interact with a process owned by another account using the command:

privilege::debug

![A computer screen shot of a blue screen

Description automatically generated](<../.gitbook/assets/6 (29).png>)

Next, you can dump the credentials of all logged on users to a machine using the sekurlsa module and the command:

Sekurlsa::logonpasswords

![Sekurlsa-logonpasswords](<../.gitbook/assets/7 (3).jpeg>)

![](<../.gitbook/assets/8 (22).png>)

This will dump the hashes for all users logged on to a current workstation, including those using Active Directory to log on. You can use the NTLM hashes dumped to perform a Pass-the-Hash (PtH) attack. Let’s save the mindhack-admin user’s NTLM hash for later use.

Modern Windows machines are well protected against Mimikatz. In the real world, a malicious actor would use various obfuscation techniques to get Mimikatz to run:

* Disabling antivirus or _**EDR (Endpoint Detection Response)**_ on the target machine before executing Mimikatz.
* Executing Mimikatz in-memory so that antiviruses cannot detect it on disk.
* Using _**process hollowing**_ to execute Mimikatz inside a legitimate process.

Other Tools

Aside from the Responder and Mimikatz, various other tools can be used to obtain NTLM hashes:

* **Meterpreter:** This tool is part of the Metasploit Framework and contains various post-exploitation functionalities that allows you to extract NTLM hashes from a machine.
* **Empire:** This Post-Exploitation Framework written in PowerShell allows you to dump user credentials and perform lateral movement.
* **Cain and Abel:** This legacy tool only runs on Windows machines. It was commonly used for internal penetration testing engagements to obtain NTLM hashes over the network through unencrypted or weakly encrypted protocols.
* **Inveigh:** This is a tool similar to Responder. It allows you to perform various network-based attacks in an Active Directory environment, such as SMB relay attacks, credential captures, and LLMNR poisoning.

Passing the Hash

Once you have obtained an NTLM hash, you can perform a Pass-the-Hash (PtH) attack using various tools. They all, ultimately, use the stolen NTLM hash to impersonate a user and authenticate to machines the way the compromised users is allowed to access within their Active Directory environment.

PtH with Mimikatz

Mimikatz can be used to both obtain credential material and use it in a PtH attack. This dual-use makes it a powerful tool to add to your hacking arsenal, and its capabilities don’t stop there. It can perform various other lateral movement techniques, including Golden Ticket attacks, Silver Ticket attacks, and DCSync attacks.

Passing the Hash in Action with Mimikatz

To perform a Pass-the-Hash (PtH) attack with Mimikatz, you must meet the following requirements:

* You need SMB enabled on the target machine.
* The target machine’s firewall must be configured to allow incoming SMB traffic.
* You must have the NTLM hash of the user you want to impersonate.
* You need SYSTEM or local administrative access for permissions to interact with the LSASS process.
* You should already have elevated privileges if you used Mimikatz to obtain an NTLM hash.

As either the SYSTEM or local administrator, run the following command from the Mimikatz command line:

privilege::debug

![](<../.gitbook/assets/9 (22).png>)

This command gives your current Mimikatz session debug privileges so you can interact with the processes owned by other users on the system. Now, you can perform the Pass-the-Hash (PtH) attack with the command:

Sekurlsa::pth /user:\<username> /domain:\<domain> /ntlm:\<ntlm\_hash>

For example, if you wanted to target the domain user mindhack-admin, you would run the command:

Sekurlsa::pth /user:mindhack-admin /domain:milkyway.local /ntlm: 2b576acbe6bcfda7294d6bd18041b8fe

![](<../.gitbook/assets/10 (20).png>)

This command spawns a Windows command shell, and a session, that uses the target user’s hash. As such, you can now impersonate the target user, and other machines you now interact with in the Active Directory environment will think you are the target user (e.g., mindhack-admin). This makes moving to other machines a trivial matter.

To test if you have successfully obtained a session as the mindhack-admin, you can run the following command from a Windows command shell:

dir [\\\10.0.200.4\c$](file:///10.0.200.4/c$)

This command lists the contents of Workstation 2’s (10.0.200.4)C: drive. If you run this command from a regular command prompt on Workstation 1, you get an “Access is denied” message:

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/11 (5).jpeg>)

However, if you run this command in the newly created Windows command shell that is impersonating the mindhack-admin user, the contents of the C: drive is listed for you:

![Command in the newly created Windows command shell](<../.gitbook/assets/12 (1).jpeg>)

From here, you can freely execute remote commands on the target machine 10.0.200.4 as the mindhack-admin user.

PsExec

**PsExec** is a command line tool developed by Microsoft and included in their Sysinternals toolset. It was originally designed to allow administrators to execute commands or run programs on remote systems. Hence it is often found in enterprise environments; however, PsExec has been abused by attackers in the past to perform lateral movement in Active Directory environments using stolen credentials.&#x20;

Passing the Hash in Action with PsExec

Kali Linux comes installed with a version of PsExec. To perform a pass the hash attack with PsExec, you must meet the following requirements:

* You need SMB enabled on the target machine.
* The target machine’s firewall must be configured to allow incoming SMB traffic.
* You must have the NTLM hash of the user you want to impersonate.

Once these requirements are met, you can perform a pass the hash attack with PsExec by issuing the following command in your Kali Linux machine:

impacket-psexec -hashes 00000000000000000000000000000000:\<ntlm\_hash> \<username>@\<ip\_address>

For example, to target the mindhack-admin who has access to machine 10.0.200.4 (Workstation 2), you would run the command:

impacket-psexec -hashes 00000000000000000000000000000000:2b576acbe6bcfda7294d6bd18041b8fe mindhack-admin@10.0.200.4

This command gives us a Windows command shell on machine  10.0.200.4. You can perform various post-exploitation activities from here, such as internal reconnaissance or stealing credentials.

_The command used here uses the Impacket version of PsExec. This tool is included in the Impacket framework, a collection of Python scripts that emulate the functionality of common Windows administrator tools._

EvilWinRM

**EvilWinRM** is a post-exploitation tool written in PowerShell which is designed to simplify gaining and maintaining remote access to Windows systems. The tool can provide you with an interactive session where you can perform remote command execution, transfer files, and execute Windows PowerShell commands.

EvilWinRM uses the Windows Remote Management (WinRM) protocol to provide this functionality to bypass the need for Remote Desktop Protocol (RDP) to be enabled on target machines. WinRM is a protocol used heavily in enterprise applications
