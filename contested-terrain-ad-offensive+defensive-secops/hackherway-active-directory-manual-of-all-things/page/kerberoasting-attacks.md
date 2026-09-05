# Kerberoasting Attacks

Kerberoasting Attacks

Kerberoasting is an attack among a sea of many that are built to attack security authentication mechanisms and processes with a goal of bypassing and evading those barriers or layers of effective security. In this section, we will discuss Kerberoasting attacks, as well as other methods of abusing the Kerberos protocol authentication mechanism. But before we dive into how this attack specifically works, it’s important for you to understand how exactly Kerberos authentication works between families of interconnected client/server farms.

_“Kerberos is for authentication not for authorization; this lacuna allows for Kerberoasting.”_

We will discuss how to perform a Kerberoasting attack and remotely pass the Kerberos ticket using Kali Linux. Kerberoasting is considered to be lateral movement, so once you have penetrated the domain client system and obtained the computer shell, then use the following method for abusing Kerberos.

As a hacker, Kerberoasting is one of your most powerful Active Directory (AD) attacks. It allows you to compromise service accounts and use them to perform lateral movement across the entire Active Directory environment. This can lead to a full domain takeover!

This section will take you through how to perform Kerberoasting attacks and see why they are such powerful attacks. First, you will gain a firm understanding of how Kerberos authentication works in modern Active Directory environments and the intherent vulnerability that allows malicious actors to compromise account passwords. Then you will see how to perform Kerberoasting using real-world hacking tools.

Put on your black hoodie, and let’s get started roasting Kerberos!

Understanding Kerberos Authentication

Kerberoasting is a cyberattack targeting the Kerberos authentication protocol, commonly used in Windows networks to securely authenticate users and devices. In a Kerberoasting attack, an attacker uses specialized tools to extract encrypted Kerberos tickets from a network and then attempts to crack the encryption to gain access to sensitive information or network resources.

Before digging deeper into Kerberoasting attacks and how they work, one should understand the architecture of service accounts.

* Service account passwords are the same length and do not expire.
* Most service accounts have elevated permissions and are often members of highly privileged groups like Domain Admins providing full administrative rights into the Active Directory (AD) infrastructure.
* Cracking the service account passwords enabling attackers to exploit the Kerberos mechanisms and compromise the entire AD domain.

**What is the Kerberos Authentication Protocol?**

Kerberos is an authentication protocol commonly used in Windows networks to securely authenticate users and devices. The Kerberos protocol uses tickets to securely authenticate users and devices without transmitting plaintext passwords over the network. These tickets are encrypted using a secret key shared between the user and the authentication server. In a Kerberoasting attack, the attacker can extract these encrypted tickets from the network and then use brute-force or dictionary-based attacks to try and crack the encryption and gain access to the sensitive information or resources that the ticket grants access to.

Modern Windows Active Directory environments have adopted the Kerberos authentication protocol to provide secure access between client systems and network resources. Kerberos authentication relies on passing tickets between client systems, a Key Distribution Center (KDC), and network resources. In simpler terms, the Kerberos protocol defines how clients interact with a network authentication service. Clients obtain tickets from the Kerberos Key Distribution Center (KDC), and they submit these tickets to application servers when connections are established. It uses UDP port 88 by default and depends on the process of symmetric key cryptography.

**Kerberos uses tickets to authenticate a user and completely avoids sending passwords across the network.**

The KDC is usually the Active Directory environment’s Domain Controller (DC), and the network resources, are servers that the client’s workstation needs to access for their job role. Furthermore, there are some key components in Kerberos authentication that play a crucial role in the entire authentication process.

| **Kerberos Components**  | **Roles**                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Volunteers (Players)** | <ul><li><strong>Client:</strong> A user who wants to access a specific service</li><li><strong>KDC:</strong> Key Distribution Center that plays a main role in Kerberos authentication. It contains a database of users and application hashes (key), an authentication server, and the <em><strong>Ticket Granting Ticket (TGT)</strong></em> service.</li><li><strong>Application Server:</strong> A dedicated server for specific services.</li></ul>                         |
| **Encryption Keys**      | <ul><li><strong>Krbtgt key:</strong> krbtgt is an account using NTLM hashes</li><li><strong>User Key:</strong> <strong>using user NTLM hash</strong></li><li>Service Key: Using NTLM hash of service that can be a user or computer account</li><li>Session key: which is passed between the user and the KDC</li><li>Service Session Key: to be used between users and services</li></ul>                                                                                       |
| **Tickets**              | <ul><li>The TGT: the ticket presented to the KDC to request for TGSs. It is encrypted with the KDC key.</li><li>The TGS (Ticket Granting Service): the ticket which user can use to authenticate against a service. It is encrypted with the service key</li></ul>                                                                                                                                                                                                               |
| **PAC**                  | <ul><li>The PAC (Privilege Attribute Certificate): a feature included in almost every ticket. This feature contains the privileges of the user and it is signed using the KDC key</li></ul>                                                                                                                                                                                                                                                                                      |
| **Message**              | <ul><li>KRB_AS_REQ: User send request to the TGT to KDC</li><li>KRB_AS_REP: User received the TFT from KDC</li><li>KRB_TGS_REQ: User send request the TGS to KDC, using the TGT</li><li>KRB_TGS_REP: User received the TGS from KDC</li><li>KRB_AP_REQ: User send request authenticate against a service, using the TGS</li><li>KRB_AP_REP: (Optional): Used by service to identify itself against the user</li><li>KRB_ERROR: Message to communicate error conditions</li></ul> |
|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

Kerberos Workflow Using Messages

In an Active Directory domain, every domain controller runs a KDC (Kerberos Distribution Center) service that processes all request for tickets to Kerberos. For Kerberos tickets AD uses the krbtgt account in the AD domain.

The image below shows the major role played by KDC in establishing a secure connection between the server and client and the entire process uses some special components as defined in the table above.

**Why Are Kerberoasting Attacks Prevalent?**

Kerberoasting attacks are prevalent because they can be difficult to detect and prevent. The Kerberos protocol is designed to be secure and efficient, but it relies on the secrecy of the secret keys that are used to encrypt and decrypt the tickets in the authentication process. If an attacker can obtain these secret keys, they can use them to extract and decrypt the tickets, which can then be used to gain access to sensitive information or network resources.

Furthermore, the Kerberos protocol is commonly used in enterprise networks. This makes Windows networks a particularly attractive target for attackers, as a successful Kerberoasting attack on an enterprise network can potentially provide the attacker with access to a large number of sensitive resources and information.

Additionally, the attack can be carried out remotely without the need for the attacker to interact directly with the authentication server or the targeted network resources. This makes it difficult for defenders to identify and stop the attack before it is successful. Overall, the combination of these factors makes Kerberoasting attacks prevalent and potentially damaging organizations relying on the Kerberos protocol for secure authentication.

How Kerberos Authentication Works

Kerberos authentication involves six main steps demonstrated in the diagram below:

![](<../.gitbook/assets/0 (76).png>)

1. **Account Authentication**

In a Kerberoasting attack, the attacker first obtains the necessary permissions to request service tickets from the Kerberos authentication service. This can be done by compromising the account of a legitimate user who has the appropriate permissions. If the attacker is successful to gain access to the network resource that the ticket grants access to, without needing to know the actual password of the user or device that the ticket belongs to. As part of this request, the user asks for a Ticket Granting Ticket (TGT) that allows them access to network resources within the Active Directory environment.

The Kerberoasting technique is an effective method for extracting service account credentials from AD as a regular user without sending any packets to the target system.

1. **Kerberos Service Ticket**

In a Kerberoasting attack, an attacker obtains a large number of service tickets from the Kerberos authentication service and then uses these tickets to try to crack the apsswords of the accounts associated with those tickets. In this technique, an attacker can abuse a valid Kerboros Ticket Granting Ticket (TGT) or sniff network traffic to obtain a Ticket-Granting Service (TGS) ticket that may be vulnerable to brute-force attacks.

The **KDC verifies the user’s identity** and replies with an encrypted TGT and a session key. The TGT is encrypted using the KDCs secret key.

1. When the user wants to access a network resource, they **send a request to the KDC asking for a service ticket,** known as a Ticket Granting Service (TGS), for the service (network resource) they want to access. In this request are the user’s TGT, their session key, and the Service Principal Name (SPN) of the service they want to access.
2. The KDC then verifies the user’s request by checking the authenticity of the TGT and **if the user is authorized to access the requested service.** If all the checks are passed, the KDC replies with a TGS and the encrypted session key to the user.
3. When a user wants to access a Kerberos-enabled service, **they send the TGS to said service.**
4. The **service will verify the TGS** and allow the user to interact with the network resource.

_**Ticket Granting Ticket (TGT)**_ verifies the user’s identity – who they are.

_**Ticket Granting Service (TGS) ticket**_ verifies the user’s permissions – can they access this specific resource.

Kerberos Attacks

Kerberos is the primary authentication protocol used in Microsoft Active Directory (AD), having largely replaced the older New Technology LAN Manager (NTLM) due to its enhanced security. While Kerberos is more secure than NTLM, it's important to be aware of potential vulnerabilities that could be exploited in an AD environment.

In this chapter, we'll explore some key Kerberos attacks. A solid understanding of these attacks requires a basic grasp of the Kerberos protocol, which we have covered in a previous article. To summarize briefly: Kerberos operates by using tickets that allow domain users to authenticate with the Key Distribution Center (KDC) and the Authentication Service (AS). These services typically reside on the domain controllers within a domain.

**Kerberos Attack 1: Brute-Force Attacks on Kerberos**

**As an authentication protocol, Kerberos is susceptible to brute-force attacks. A unique aspect of brute-force attacks on Kerberos is that they do not require a domain account—only a connection to the KDC is necessary.**

**During an authentication request (AS-REQ), an attacker can analyze the KDC's response to determine whether a specific user exists. This enables attackers to perform username brute-forcing by leveraging word lists. A key advantage for attackers is that Kerberos pre-authentication failures in Active Directory are logged under Event ID 4771 (Kerberos pre-authentication failed) rather than the more common logon failure event (4625). This difference in logging reduces the likelihood of the attack being detected.**

**To perform a Kerberoasting brute-force attack, you will use tools designed for penetration testing that specialize in brute-forcing. One such tool that was designed specifically for testing AD and Kerberos resilience is Kerbrute, which is commonly used to enumerate valid usernames in an Active Directory environment via Kerberos. To conduct and learn how this attack is executed, follow the below procedure to perform a brute-force attack against Kerberos:**

1. **Install ‘kerbrute’:**

Fist, you’ll need to install ‘kerbrute.’ You can download it from my GitHub repository at (_**Source:**_ [_https://github.com/d0midigi/kerbrute_](https://github.com/d0midigi/kerbrute)).

wget https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute\_linux\_amd64

chmod +x kerbrute\_linux\_amd64

mv kerbrute\_linux\_amd64 /usr/local/bin/kerbrute

1. **Prepare a list of Usernames:**

You need a wordlist of potential usernames to brute-force. This can be a custom list or a commonly used one such as ‘rockyou.txt,’ which also can be downloaded from my GitHub repository at (_**Source:** https://github.com/d0midigi/SecLists/tree/master/Passwords/Leaked-Databases_)

Admin

user1

john.doe

jane.smith

1. **Run ‘kerbrute:’**

Use the kerbrute tool to enumerate valid usernames by testing them against the Kerberos KDC:

kerbrute userenum -d \<domain> --dc \<domain controller IP> usernames.txt

* Replace \<domain? With your target domain (e.g., ‘example.com’).
* Replace \<domain controller IP> with the IP address of the domain controller.
* ‘usernames.txt’ is the file containing the list of usernames to brute-force. In this example, replace usernames.txt with rockyou.txt wordlist.

**Example:**

kerbrute userenum -d example.com --dc 192.168.1.10 usernames.txt

1. **Analyze the Results**

The tool will attempt to authenticate each username against the Kerberos KDC and will list out the valid usernames based on the responses from the KDC.

**Note: Be aware that even though Kerberos brute-force attacks might not trigger the usual logon failure events, they can still be detected by monitoring for unusual activities, such as repeated authentication requests.**

![A screen shot of a computer

Description automatically generated](<../.gitbook/assets/1 (56).png>)

**FIGURE X: Kerberos user enumeration brute-force attack.**

Attackers can enumerate usernames in Kerberos by analyzing the specific error codes returned by the Key Distribution Center (KDC) when an authentication request fails. Here are the key Kerberos error codes that you can use to determine whether a username exists:

**Key Kerberos Error Codes for Username Enumeration**

| **User Status** | **Kerberos Error**                                                     |
| --------------- | ---------------------------------------------------------------------- |
| Present/Enabled | KDC\_ERR\_PREAUTH\_REQUIRED: Additional pre-authentication required    |
| Locked/Disabled | KDCP\_ERR\_CLIENT\_REVOKED: The client’s credentials have been revoked |
| Does Not Exist  | KDC\_ERR\_C\_PRINCIPAL\_UNKNOWN: Client not found in Kerberos database |

**Challenges in Troubleshooting Kerberos User Enumeration**

Kerberos user enumeration can be challenging to troubleshoot because it relies on effective Kerberos monitoring. This monitoring must be capable of detecting an unusually high number of AS-REQ requests that don’t result in follow-up requests.

To ensure these events are logged, you first need to adjust the default settings for monitoring account logins. This can be done by configuring group policies under:

COMPUTER CONFIGURATION\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Account Logon

Set the following policies:

* **Audit Credential Validation**
* **Audit Kerberos Authentication Service**
* **Audit Kerberos Service Ticket Operations**

to the value **“Success and Failure”** so that both successful and failed logins are logged. After configuring these settings, you can search the event log for **Event ID 4768** and the associated string “**0x6.**”

**Why Isn’t Searching for Event ID 4768 Enough?**

Event ID 4768 is generated whenever a Ticket Granting Ticket (TGT) is requested or granted, including legitimate requests; therefore, monitoring this event alone isn’t siccicent enough. The string ‘0x6’ corresponds to the error code “KDC\_ERR\_C\_PRINCIPAL\_UNKNOWN,” which indicates that the requested principal (username) is unknown. You can only suspect Kerberos enumeration if this error code appears frequently in a short time span.

**Detecting Other Attacks Using Event Logs**

These settings also help you to detect other Kerberos attacks, such as _**password spraying.**_ To detect this, ensure event logging is configured as described above, then monitor the event log for **Event ID 4771** (“Kerberos pre-authentication failure”). You should be alert if there is an unusually high number of these events in a short period.

To effectively monitor these logs, it’s recommended to use additional tools, ideally a Security Information and Event Management (SIEM) system, to continuously monitor Active Directory, and respond to potential attacks immediately.

**Kerberos Attack 2: AS-REP Roasting Attack**

AS-REP Roasting is a Kerberos attack where attackers exploit the absence of Kerberos pre-authentication to steal and crack parts of an AS\_REP message offline. This attack targets user accounts that have Kerberos pre-authentication disabled. When pre-authentication is disabled, anyone can send an AS\_REQ request to the KDC on behalf of that user and receive an AS-REP message in return. The AS\_REP message includes data encrypted with the user’s NTLM hash. You can then use this encrypted data to attempt to crack the user’s password offline.

**How AS-REP Roasting Works**

1. **Identifying Vulnerable Accounts:** You identify user accounts in Active Directory that have Kerberos pre-authentication disabled.
2. **Receiving AS\_REP Request:** You send an AS\_REQ request to the KDC for the vulnerable user account.
3. **Receiving AS\_REP Response:** The KDC responds with an AS\_REP message, which includes information encrypted with the user’s NTLM hash.
4. **Cracking the Password:** You then extract the encrypted portion of the AS\_REP message and attempts to crack the NTLM hash offline, potentially revealing the user’s password.

**Default Settings and Disabling Pre-Authentication**

By default, kerberos pre-authentication is enabled in Active Directory, which helps prevent such attacks; however, it can be disabled for a specific user account through the following setting:

1. Open **Active Directory Users and Computers (ADUC)**
2. Locate the user account you wish to modify.
3. Right-click the account and select **Properties**.
4. Navigate to the **Accounts** tab.
5. In the **Account options** section, check the box labeled **“Do not require Kerberos preauthentication.”**

**Disabling pre-authentication for an account exposes it to AS-REP Roasting attacks, so it is generally recommended to keep pre-authentication enabled to mitigate this risk.**

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/2 (48).png>)

**FIGURE X:** Windows account options that disable Kerberos pre-authentication.

**Attack**

When pre-authentication is enabled, a user requesting access to a resource begins the Kerberos authentication process by sending an Authentication Service Request (AS-REQ) message to the domain controller (DC). In this AS-REQ, the timestamp is encrypted using the hash of the user’s password. The DC then compares this encrypted timestamp with its stored hash of the user's password. If they match, the DC sends back an Authentication Service Response (AS-REP) message. This AS-REP message includes a Ticket Granting Ticket (TGT), which the user will use for future access requests. Additionally, the AS-REP contains information hashed with the user's password.

However, if pre-authentication is disabled, the security of this process is compromised. An attacker can send an AS-REQ on behalf of any user to the DC and receive an AS-REP in response. This AS-REP contains data encrypted with the user’s password hash. The attacker can then use this encrypted data to attempt to crack the user's password offline. By doing so, they try to decrypt the AS-REP to obtain meaningful plaintext, indicating that the decryption key (i.e., the user’s password) has been correctly guessed.

![A computer screen shot of a computer code

Description automatically generated](<../.gitbook/assets/3 (35).png>)

FIGURE X: AS-REP Roasting attack us CrackMapExec.

Advantages for Attackers

**No Domain Account Required:** This attack can be executed without needing a valid domain account—just a connection to the Key Distribution Center (KDC).

**Domain User Accounts:** If attackers do have access to a domain user account, they can conduct an LDAP query to identify other user accounts in the domain that have Kerberos pre-authentication disabled. This significantly reduces the amount of guesswork required.

**Combining Attacks:** Even without a domain account, attackers can guess usernames. This guessing process becomes easier when combined with other Kerberos attacks, such as Kerberos user enumeration, which helps in identifying valid usernames.

This combination of methods makes AS-REP Roasting a powerful tool for attackers targeting Kerberos environments where pre-authentication is not enforced. Therefore, it is crucial to ensure that pre-authentication is enabled for all accounts in Active Directory to mitigate this risk.

**Mitigation for Defenders**

To protect your network from AS-REP Roasting and other Kerberos attacks, it’s important to ensure that all accounts in your domain have Kerberos pre-authentication enabled. Although this has been the default setting since Kerberos v5, it’s a good idea to verify that no accounts have been misconfigured. You can perform an LDAP query to identify any users who have pre-authentication disabled and then correct the setting for those accounts.

In addition to enabling pre-authentication, enforcing a strong password policy in Active Directory is crucial. A robust password policy ensures that even if an account is vulnerable, the encryption remains difficult to crack. Strong passwords make it virtually impossible for attackers to break the encryption by guessing the password, protecting the account from offline attacks. Moreover, a secure password policy encourages users to create strong passwords across the board, reducing the risk of brute-force attacks and other common password-based threats.

**Kerberoasting Attack 3: Kerberos Rusting Attack**

The goal of Kerberoasting is to obtain Ticket Granting Service (TGS) tickets for services running on behalf of user accounts in Active Directory (AD), rather than computer accounts. This is useful because some of these TGS tickets are encrypted with keys derived from user passwords. Attackers can then perform brute force attacks offline to try to decrypt the credentials associated with these user accounts.

Only a single domain account is needed to carry out a Kerberoasting attack, as the attacker can request Service Principal Names (SPNs) without requiring any special privileges. This makes Kerberoasting a potent technique for extracting and potentially cracking service account passwords within a domain.

**Attack**

**In a Kerberoasting attack, an attacker targets TGS (Ticket Granting Service) tickets that are encrypted with user passwords by requesting these tickets for service accounts. Here's a detailed look at the process:**

**### What are SPNs?**

**Service Principal Names (SPNs) are unique identifiers for services running on a network. They are used by Kerberos authentication to associate a service instance with a specific user account. SPNs enable a client application to request authentication for a service without needing to know the actual account name of the service.**

**### Kerberoasting Attack Process**

**1. \*\*SPN Request\*\*: The attacker requests TGS tickets by specifying an SPN associated with a service in Active Directory. This can be any SPN, and no special privileges are required to make this request.**

**2. \*\*Ticket Issuance\*\*: If the SPN is registered in Active Directory, the domain controller responds with a TGS ticket. This ticket is encrypted using the secret key of the account running the service.**

**3. \*\*Brute Force Attack\*\*: The attacker obtains the TGS ticket, which contains encrypted information. Since the ticket is encrypted with the service account’s password hash, the attacker can attempt to crack this encrypted information offline using brute force techniques.**

**4. \*\*Password Extraction\*\*: If successful, the attacker can decrypt the ticket to obtain the service account's plaintext password.**

**### Key Points**

**- \*\*Service Accounts\*\*: The attack focuses on service accounts because their TGS tickets are encrypted with the password of the account running the service.**

**- \*\*No Special Rights Needed\*\*: Any domain account can request TGS tickets for SPNs, making this attack relatively easy to execute if SPNs are exposed.**

**- \*\*Offline Cracking\*\*: The ability to perform offline brute-force attacks makes it easier for attackers to try various passwords against the encrypted TGS tickets, as they are not constrained by real-time constraints like online authentication attempts.**

**By understanding SPNs and how they are used in Kerberos authentication, you can better secure your environment against Kerberoasting attacks by ensuring that service accounts use strong, complex passwords and regularly reviewing and managing SPNs.**

![A screen shot of a computer

Description automatically generated](<../.gitbook/assets/4 (38).png>)

**FIGURE X:** Kerberoasting attack using Impacket-GetUserSPNs.

\### Solution to Protect Against Kerberoasting

To protect against Kerberoasting attacks, ensure that Service Principal Names (SPNs) are used for machine accounts rather than user accounts. This reduces the risk of exposing user passwords through TGS tickets. If using user accounts for services is unavoidable, Microsoft’s Group Managed Service Accounts (gMSAs) can help mitigate the risk. gMSAs provide robust password management by automatically changing and securely handling passwords.

\### Prerequisites for Using gMSAs

1\. \*\*Domain Functional Level\*\*: Must be Windows Server 2012 or higher.

2\. \*\*Operating System\*\*: Windows Server 2012 R2 or later.

3\. \*\*Active Directory PowerShell Module\*\*: Installed on the Domain Controller (DC) and the servers where gMSAs will be used.

4\. \*\*SQL Server\*\*: SQL Server 2014 or later if using gMSAs for SQL Server.

\### Steps to Set Up gMSAs

\#### Step 1: Install Active Directory PowerShell Module on DC

If the Active Directory PowerShell module is not already installed on your DC, you can install it using the following PowerShell command:

\`\`\`powershell

Install-WindowsFeature -Name RSAT-AD-POWERSHELL

\`\`\`

\#### Step 2: Check and Create the Root Key for Key Distribution Service

The creation of gMSAs requires a root key for the Key Distribution Service (KDS). First, check if the root key exists. Use the following PowerShell command:

\`\`\`powershell

Test-KdsRootKey -KeyId (Get-KdsRootKey).KeyId

\`\`\`

\- \*\*If the root key exists\*\*, the command will return \`True\`.

\- \*\*If the root key does not exist\*\*, you will receive an error. In this case, you need to create the root key using:

\`\`\`powershell

Add-KdsRootKey -EffectiveImmediately

\`\`\`

\### Additional Steps (if needed)

After verifying or creating the root key, follow the additional steps in the Microsoft guide for configuring and deploying gMSAs to ensure the service accounts use robust passwords and are protected against Kerberoasting.

By implementing these measures, you can enhance your security posture and reduce the risk of Kerberoasting attacks in your Active Directory environment.
