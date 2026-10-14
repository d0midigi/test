# SMB/Windows Admin Shares

The use of SMB/Windows Admin Shares is a well-known tactic that adversaries may use to interact with remote network shares using the Server Message Block (SMB) protocol. By leveraging valid accounts, adversaries can access and perform actions on network shares as the logged-on user.

SMB is a widely used protocol for sharing files, printers, and other resources on Windows networks. Windows systems have hidden network shares such as C$, ADMIN$, and IPC$ that are typically accessible only to administrators and allow for remote file copying and other administrative functions.

Adversaries may exploit SMB shares in conjunction with administrator-level accounts to remotely access networked systems, interact with systems using Remote Procedure Calls (RPCs), transfer files, and execute binaries remotely. This technique has been famously utilized in attacks such as WannaCry, which targeted systems through vulnerable SMB shares.

Security teams should regularly scan their networks for open SMB ports, implement strong access controls and monitoring, and conduct thorough security assessments to identify and address any vulnerabilities that could be exploited by threat actors using SMB/Windows Admin Shares. Reconnaissance activities, such as Nmap scans, can provide valuable insights into the services running on a network and help identify potential security risks.

&#x20;**Recon**

Our initial step is to conduct an nmap scan to identify the service running on the operating system. Since we know that the service typically runs on port 445, we will prioritize focusing on this during our enumeration process.

<figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

After our Nmap scan, we identified that the port and service are open and running. Through enumeration, we discovered that this service ius vulnerable to the EternalBlue exploit. This well-known vulnerability was leaded by Shadow Brokers in 2017 and developed by the NSA (National Security Agency). The exploit has been incorporated into the metasploit Framework and can be used to gain shell access to the vulnerable machine.

However, it is crucial to exercise caution when using such exploits, as they have the potential to severly crash servers. While they have been tested and integrated into frameworks like Metasploit, the unpredicatble nature of computers means that successful exploitation is not guaranteed; therefore, it is recommended to replicate the environment in a virtual machine and test the exploits there before attempting them in an isolated live scenario.

By verifying our set variables in Metasploit and executing the exploit, we were able to successfully gain a shell on the target machine.

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

This successful exploit resulted in gaining SYSTEM access, showcasing how services exposed to the public internet can be exploited by attackers to access a network. Through thorough enumeration and the use of appropriate tools, vulnerabilities on the target machine can be identified and exploited to gain access to the system.

Although this particular vulnerability may not be as prevalent in the wild anymore, it still exists and poses a threat. It serves as a reminder of the importance of regularly assessing and securing network services to prevent unauthorized access and potential security breaches.<br>

###
