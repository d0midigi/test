# Active Directory Privilege Escalation

Active Directory Privilege Escalation

Executive Summary

Microsoft Active Directory is the very foundation of cyber security and privileged access at 85% of organizations, and within Active Directory deployments lie thousands of privilege escalation paths.

Anyone who could identify these privilege escalation paths in Active Directory could easily compromise virtually any IT resource of choice, and in the worst case, the entire foundational Active Directory itself. This is **alarming** considering that historically 100% of all major recent cyber security breaches involved the compromise and misuse of a single account that possessed privileged access in Active Directory.

In organizations that operate on the Microsoft Windows Server platform, the entirety of their building blocks of cyber security (e.g., all organizational user accounts, computer accounts, and security groups that protect all organizational IT resources, are stored, managed, and secured in Active Directory. These building blocks are represented as Active Directory objects and protected by access control lists (ACLs) within which lie permissions that allow and deny access to a large number of users and groups.

In every Active Directory domain, within ACLs of thousands of Active Directory objects lie hundreds of thousands of permissions and it is their net cumulative resulting effect (e.g., effective permissions) that govern who has what privileged access on each one of these thousands of Active Directory objects. Organizations thus require the ability to accurately calculate effective permissions in Active Directory; astonishingly the ability to accurately calculate effective permissions doesn’t exist in Active Directory.

Consequently, organizations have been provisioning access in proverbial dark for years now, and as a result, at organizations worldwide, today there exists an ocean of excessive privileged access within which lie thousands of privilege escalation paths leading to the compromise of all Active Directory content, and anyone who can accurately identify them could easily exploit them to inflict damage.

Technical Summary

Active Directory Privilege Escalation is an exploitation technique where you identify and exploit unauthorized access in ACLs of Active Directory objects to compromise them and escalate privilege.

Active Directory privilege escalation lets one compromise domain user accounts, computer accounts, security groups and other Active Directory content, including privileged users and groups. The compromise of a single Active Directory privileged user or group is sufficient to obtain complete command and control over the entire Active Directory, and is tantamount to complete compromise.

In organizations that operate on Microsoft’s Windows Server platform, all organizational user accounts, computer accounts, and security groups are stored, managed, and secured in their Active Directory. These building blocks are represented as Active Directory objects and are protected by access control lists within which exist permissions that allow and deny access to a large number of users and groups. The permissions specified in the ACLs of Active Directory objects determine the effective permissions provisioned on these objects, which in turn govern who can enact various administrative tasks such as resetting passwords and changing group memberships, modifying access etc., on these objects.

Anyone who could enact such tasks on Active Directory objects could gain control over them, in effect escalating privilege, so privilege escalation involves finding and exploiting unauthorized access to do so. For example, if the effective permissions on the _Domain Admins_ security group allow one the ability to change its membership, s/he could easily add his/her/any domain user account to the group’s membership, and in doing so would have easily escalated privileges to a domain admin.

Root Cause Example

Active Directory privilege escalation is made possible by the existence of unidentified/unauthorized effective permissions resulting from the security permissions provisioned on Active Directory objects.

Specifically, in the ACL of every Active Directory object reside numerous security permissions, and it is their net resulting effect (e.g., effective permissions) that determine who actually has what access. The accurate calculation of Active Directory effective permissions is very difficult, and because most organizations do not have accurate effective permissions insight, access changes made over years have resulted in a substantial amount of unidentified/unauthorized access, paving privilege escalation paths. As an example, assume that the ACL protecting the CEOs domain user account contains one hundred permissions, fifty explicit and fifty inherited, eighty of which allow and twenty deny access, each one specifying various permissions to various users and groups, many of which contain nested groups as well.

The actual resulting access allowed on the CEOs domain user account will depend on the outcome of the cumulative impact of each one of these one hundred permissions (e.g., effective permissions). Based on resulting effective permissions, it so happened that a single permission granted to a single incorrectly nested group resulted in a team of fifty contractors accidentally ended up getting sufficient effective permissions to reset the CEOs password, even though they’re not supposed to be able to do so. This one little technicality ended up creating fifty privilege escalation paths to the CEOs account. In this manner, over time, in every Active Directory, thousands of privilege escalation paths have been created. Unfortunately, this organization may never discover them as it doesn’t have the ability to accurately calculate effective permissions, but any perpetrator who has the ability, could find and exploit them.

Top Five Attack Vectors

Active Directory privilege escalation is a very powerful and effective exploitation technique because it can be used to very quickly compromise and gain escalated privileges on any Active Directory object. Specifically, if one has sufficient effective permissions to be able to enact certain administrative tasks on an Active Directory object, all s/he would need to do to escalate privilege is enact the task. Active Directory privilege escalation can be used to target and compromise any domain user account, domain computer account, domain security group, organizational unit (OU), service connection point, etc.

The following are the Top Five most prevalent ways to escalate privilege in Active Directory:

1. _**Reset a domain user account’s password:**_ Resetting a domain user account’s password would let one instantly take over the account by logging in using the newly set password.
2. _**Change a domain security group’s membership:**_ Changing a domain security group’s membership would let on instantly add any controlled account as a member of the group.
3. _**Modify the permissions/ACL protecting an object:**_ Modifying the permissions protecting an Active Directory object would let one gain complete administrative control over the object.
4. _**Taking ownership of an object:**_ Taking ownership of an Active directory object would grant one the implicit ability to modify permissions on the object and gain control over it.
5. _**Link a malicious GPO to an OU:**_ Linking a single malicious GPO to an OU would ultimately let one gain administrative over all computers whose computer accounts reside in that OU.

**Note: Smartcard authentication can also be defeated by simply disabling their use on domain user accounts.**

Multi-Step Privilege Escalation Example

For instance, one could identify and exploit a three-step privilege escalation path starting from a regular domain user account and ultimately leading to domain admin equivalent access. Skilled individuals often employ multi-step Active Directory privilege escalation to gain root access:

Consider a hacker who possesses sufficient skill or tooling to accurately determine effective permissions in Active Directory is able to identify the following three privilege escalation paths –

1. _**John Doe can change the Domain Admins Group Membership:**_ Hacker calculates effective permissions on the _Domain Admins_ group to uncover that _John Doe_ can change its membership.
2. _**Jane Doe can modify permissions on John Doe’s account:**_ Next, the hacker calculates effective permissions on _John Doe’s_ account to uncover that _Jane Doe_ can modify access on his account.
3. _**Jim Doe can reset Jane Doe’s password:**_ Finally, the hacker calculates effective permissions on Jane Doe’s account to uncover that _Jim Doe_ can reset Jane Doe’s account password.

By simply utilizing default read access granted to _Authenticated Users,_ and the ability to accurately determine effective permissions on Active Directory objects, the hacker has found an easily exploitable three-step privilege escalation path, starting from a minimally protected domain user account leading to the all-powerful _Domain Admins_ security group, all achievable within seconds.

In essence, the hacker uncovered a multi-step privilege escalation path wherein if they could compromise _Jim Doe’s_ account, s/he would be literally one password reset, one ACL change and one security group membership change away from gaining all-powerful _Domain Admin_ access.

**Minutes to Compromise**

Today, in the sea of privileged access in Active Directory lie thousands of privilege escalation paths that can be exploited to compromise the vast majority of organizational IT resources within minutes. Specifically, in virtually every Active Directory deployment today, there exist thousands of privilege escalation paths to every single object in Active Directory, including to their all privileged accounts and groups, executive accounts, large Ous, high-value computer accounts, groups, etc.

In fact, a single change in just one permission in an ACL of one Active Directory object could result in everyone having complete command and control over the entire organization –

1. Just one change to one ACL could be used to compromise all accounts in Active Directory
2. Just one Group Policy Object (GPO) linked to one OU could be used to compromise thousands of computers
3. Just one change to one security group could grant access to all organizational IT resources
4. Just one change to one service connection point (e.g., AD Azure Connect) could wreak havoc
5. Just one change in Active Directory could instantly result in a massive cyber security breach

Incidentally, today literally anyone with a domain user account and sufficient expertise/tooling could query their Active Directory and easily find themselves of easily exploitable privilege escalation paths.

Yet, not a single organization in the world knows exactly who can make such changes in their Active Directory, and no one, not their CISOs, not their Auditors, not even their Domain Admins, have a clue.

Six Dangerous Myths

Today, most organizations are operating on a dangerously false sense of security, based on the belief that recent cyber security and privileged access management (PAM) solutions can mitigate this risk. Today, every organizations, its CISO and Domain Admins must be aware of the following six dangerous myths –

1. _**We analyze Active Directory Permissions:**_ What controls and determines privileged access in Active Directory is not _“who has what permissions”_ but _“who has what effective permissions.”_
2. _**We use Active Directory Auditing:**_ Auditing is merely a reactive measure informing you that a perpetrator has (already) engaged in an action that has (already) compromised your security.
3. _**We use a Privileged Session Manager:**_ Privileged Session Managers only monitor privileged users’ activities. This specific risk can be enacted upon by anyone who has a domain admin account.
4. _**We use an Enterprise Password Vault/Manager:**_ A mere password reset performed directly on a domain user account in Active Directory can circumvent any password vault/manager.
5. _**We use Multi-Factor Authentication (MFA):**_ MFA on domain user accounts can be turned off at a button’s click by making a single change directly on the user account in Active Directory.
6. _**We use Advanced Threat Analytics and/or Threat Intelligence:**_ Both can be easily subverted as recon can be easily disguised and spread over time, and the actual attack only takes seconds.

Mitigation

The risk posed by Active Directory privilege escalation is 100% mitigatable, as doing so only requires the desire and ability to accurately identify, lockdown, and maintain least privileged access in Active Directory.

The keys to all privileged access in Active Directory (e.g., the keys to accurately identify, locking down, and maintaining least privileged access in Active Directory) lie in Active Directory Effective Permissions.

Active Directory effective permissions control all privileged accesses provisioned in Active Directory.

They control exactly who can:

1. Create, delete, and manage all privileged, executive, and in fact all user accounts and groups
2. Change the membership of all domain security groups that ultimately protect all IT resources
3. Join computers as well as link GPOs to Ous to ultimately control all domain-joined computers.

Unfortunately, for years now, most organization’s have incorrectly believed that to assess privileged access in Active Directory, all they need to audit is _“who has what permissions in Active Directory”_ when, in fact, nothing could be further from the truth, for there’s only one correct way to assess privileged access in Active Directory and that’s to audit _“who has what effective permissions.”_

In fact, Active Directory effective permissions are so important that the three tabs in Microsoft’s native tooling, one is for Effective Permissions. Sadly, that tab remains inaccurate and inadequate.

Today, as an ethical hacker, it is imperative that you know what Active Directory effective permissions are because without them not a single object in Active Directory can be secured, and it is in effective permissions that lie the keys to correctly and completely mitigating this cyber security risk.

Risk Mitigation

This cyber security risk can be reliably mitigated, and all organizations that value foundational cyber security hygiene must take this risk seriously and consider making its mitigation a top corporate priority.

Organizations can mitigate this risk by enacting five simple steps:

1. _**Awareness:**_ From the CEO to Domain Admins, you, as an ethical hacker must gain an understanding of why and how this organizational risk impacts the cyber security of the entire organization.
2. _**Expertise:**_ You must guide your client organization to ensure that their IT personnel have the expertise and experience required to understand and use essential concepts like Active Directory Effective Permissions.
3. _**Capability:**_ You must guide your client organization to ensure that they possess/acquire the essential capability needed to accurately and trustworthy calculate effective permissions in Active Directory.
4. _**Empowerment:**_ IT defenders should be tasked with the objective of assessing and mitigating this risk and ideally simultaneously attaining and maintaining Least Privileged Access (LPA) in Active Directory, and they should be provided the resources required to accomplish their objectives.
5. _**Accountability:**_ From the CEO to the CISO to the IT Manager to the Domain Admins/IT Teams who manage privileged access in Active Directory, an accountability chain must be established.

From a technical standpoint, mitigating this security risk involves learning how to correctly assess and lockdown privilege access (effective permissions) in Active Directory, and then implementing a high-priority IT project aimed at attaining and maintaining LPA in the organization’s Active Directory.

In summary, organizations that possess the desire, expertise, and capability required to accurately assess and lockdown privileged access in their Active Directory can easily mitigate this risk today.

Paramount to Organizational Cyber Security

In every Windows Server-based IT infrastructure worldwide, the vast majority of all privileged access as well as the most powerful Domain Admin equivalent privileged access resides in Active Directory.

The keys to all privileged access, _the keys_ to accurately identifying, locking down and maintaining all privileged access in Active Directory lie in accurately determining Active Directory effective permissions. Consequently, from the CEOs account to the Domain Admins group, not a single Active Directory object can be secured without being able to accurately determine Active Directory effective permissions.
