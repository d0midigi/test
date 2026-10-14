# Remote Desktop Protocol (RDP) Services

Remote desktop services, such as Microsoft's Remote Desktop Protocol (RDP), are commonly used features that allow users to log into a remote system and access its desktop graphical user interface (GUI). Adversaries may exploit RDP to gain unauthorized access to a system, particularly if the service is enabled and accessible with known credentials.

While remote desktop access can be useful for legitimate purposes, enabling RDP on a system introduces security risks, especially if exposed to the public internet. Attackers can potentially exploit vulnerabilities or find valid credentials to access the service and infiltrate the network.

It is important for organizations to carefully manage and secure remote desktop services to prevent unauthorized access and potential security breaches. Regularly updating and patching systems, utilizing strong passwords, or MFA, and restricting access to only authorized users and accounts can help mitigate the risk of RDP-related attacks.

**Recon**

Let's start by initiating an Nmap scan on port 3389, which is commonly used for the RDP service which can also provide valuable information about the system. We will run the following command:

`nmap -`<mark style="color:orange;">`p`</mark> <mark style="color:blue;">`3389`</mark>` ``<target_IP>`

This will scan the specified target IP address on port 3389 and provide details on the RDP service running on that port. The scan results may indicate the service version, OS detection, and any potential vulnerabilities associated with the RDP service.

It is important to thoroughly analyze the scan results and take appropriate security measures to secure the RDP service, such as implementing strong authentication mechanisms, restricting access, and regularly monitoring and updating the system to prevent unauthorized access and potential security breaches.

<figure><img src="../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

It is crucial to emphasize that searching for accounts or common passwords that can provide access to RDP services without proper authorization is <mark style="color:red;">**illegal**</mark> and <mark style="color:red;">**unethical**</mark>**.** It is important to <mark style="color:red;">**always adhere to legal and ethical guidelines in cybersecurity practices; however, the choice is yours. You have been warned.**</mark>

That being said, it is essential for organizations to actively manage and secure user accounts and credentials, especially for services like RDP that provide remote access to systems. This includes implementing strong password policies, multi-factor authentication, and regular monitoring for unauthorized access attempts.

We will proceed by searching for accounts or commonly used passwords that may grant access to these services. Techniques like OSINT, phishing, and accessing leaked databases can be employed for this purpose. These methods can help us identify user credentials to test on the external remote services used by a company that is accessible via the public internet.

**Exploitation**

In terms of exploitation, this attack does not involve using exploits. Instead, it relies on having valid accounts with RDP permissions or administrator privileges, as these accounts typically allow for remote access via RDP.

In this scenario, our reconnaissance efforts led us to discover some outdated credentials that were exposed in a previous database breach:

`User: John`

`Password: P4$$W0rd123!`

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

After diligent effort, we successfully gained access through the RDP service identified during our initial reconnaissance. This is an uncommon but significant example of how attackers can exploit vulnerabilities to gain access to an organization's internal network. It underscores the importance of robust security measures and continuous monitoring to prevent unauthorized access and protect sensitive information.
