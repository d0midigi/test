# Flexible Single Master Operations (FSMO) in Active Directory

## Introduction to FSMO Roles

FSMO stands for Flexible Single Master Operations, a term that originated from Microsoft’s work to address the limitations of the multi-master replication model in AD. FSMO roles ensure the functioning and consistency of the Active Directory across a Windows domain by assigning a specific critical task to designated controllers and providing a single authority process change. By centralizing these operations within specific domain controllers, FSMO roles help maintain the integrity and stability of Active Directory environments.

There are five unique FSMO roles. By default, when you create an Active Directory domain, all FSMO roles are assigned to the first domain controller in the forest. Domain admins can reassign FSMO roles to other domain controllers if needed.

### 🔸The Importance and Need for FSMO Roles

Before we jump into the actual FSMO roles, it is important to understand the multi-master architecture that creates the need for them.

### 🔸Multi-Master Model vs. Single-Master Model

Microsoft’s early network architecture was built on a Single-Master Model in which a single server held the writable database copy containing all user and computer object accounts. This server was solely responsible for making additions or modifications to the account database. Other servers in the network maintained read-only copies of the database. While these servers could authenticate users, they could not change the database. If the master went offline or malfunctioned, no new accounts could be created, and existing accounts could not be modified. This created a single point of failure.

To address the limitations of the Single-Master Model, Microsoft transitioned to a Multi-Master Model in Active Directory (AD), where each domain controller (DC) maintains a writable copy of the account database. This design ensures redundancy and resilience, as operations can continue even if one DC becomes unavailable; however, this multi-master approach introduced the potential for conflicts, where different DCs might attempt to make conflicting changes simultaneously. To prevent such inconsistencies and maintain AD’s integrity and performance, Microsoft introduced Flexible Single Master Operations (FSMO) roles.

### 🔸Importance of FSMO Roles in AD

By assigning FSMO roles, Active Directory ensures that essential operations—such as updates to the schema, domain naming, and time synchronization—are handled in an orderly and consistent manner. If the DC holding a specific FSMO role goes down, the role can be transferred to another DC, ensuring continuity. The distribution of FSMO roles is crucial for maintaining a balanced and efficient network, and organizations can customize this distribution based on their specific needs and best practices for performance and redundancy.

### 🔸The Five FSMO Roles in Active Directory Explained

Active Directory has five unique FSMO roles:

* Schema Master (forest level)
* Domain Naming Master (forest level)
* Relative ID (RID) Master (domain level)
* Primary Domain Controller (PDC) Emulator (domain level)
* Infrastructure Master (domain level)

Let’s learn more about each FSMO role and its specific function within the Active Directory infrastructure:

## <mark style="color:yellow;">1. Schema Master</mark>

### 🔸What is the Schema Master FSMO Role?

The Schema Master is an AD enterprise-level FSMO roles, and there can be **only one** Schema Master in any Active Directory forest. The schema defines the object classes (types of objects, like users, groups, and computers) and their corresponding attributes that can exist in the AD database (`ntds.dit`).

### 🔸When and How the Schema Master Is Used

Sometimes, the Schema needs to be changed or updated, for example, to add a new required object type or attribute. To prevent overlapping or conflicting updates, only the DC with the Schema Master role can process changes to the overall AD schema. Whenever a schema update is made, the Schema Master ensures the changes are replicated to all other DCs in the forest, ensuring each DC has a local partial copy to prevent conflicts whenever future domain changes to the schema are made; in other words, all DCs are "on the same page."

If a schema update is required, the Schema Master must be available to process these changes; however, schema changes are relatively infrequent and don't happen on an occurring basis in most AD environments. Circumstances that can require a schema change include upgrading Active Directory, integrating certain types of enterprise-wide software, raising the functional level of the forest, and upgrading the operating system of a domain controllers to a higher version than currently exists in the forest.

## <mark style="color:yellow;">2. Domain Naming Master</mark>

### 🔸Roles and Responsibilities of the Domain Naming Master FSMO Role

The Domain Naming Master is an enterprise-level role; there is **only one** Domain Naming Master in an Active Directory forest. It is the only DC capable of adding new Domains and application partitions to the forest or removing existing ones from the forest.

### 🔸Common Scenarios Involving the Domain Naming Master FSMO Role

There may be times where you may need to alter your AD forest as your business evolves, or additional domains come into play and may be added to your forest because of a merger or acquisition. Since the addition and removal of domains and partitions are infrequent and rarely time-critical operations, the Domain Naming Master role has little overhead, and its loss can be expected to result in little to no operational impact.

<figure><img src="../../../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">3. RID Master</mark>

### 🔸What is the RID Master Role?

Relative Identifier Master (RID Master) is a domain-level role; there is one RID Master in each domain in an AD forest. It is responsible for allocating RID pools to the DCs in its domain's order to ensure that each security principal (such as a user or group) has a unique Security Identifier (SID).

#### 🔸RIDs and SIDs

A SID is a variable-length alphanumerical string that looks like this:

```
`S-1-5-21-1234567890-1234567890-1234567890-1001`
```

The first part of the string is the domain SID, which is the same for all SIDs in a domain. The last part is the RID, which is unique for each SID in the domain. In the example above, `1001` is the RID assigned to a particular security principal in the domain.

<figure><img src="../../../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

### 🔸Functionality and Usage of RID Master

The RID Master assigns RID pools to DCs. Each pool consists of a unique, contiguous range of RIDs, which the DC can use to generate a unique SID when it creates a security principal. By centrally managing the distribution of RIDs, the RID Master ensures that no two domain controllers allocate the same RID to different security principals, guaranteeing each SIDs uniqueness within the domain.

Once a DC is assigned a RID pool from the RID Master, it does not need to communicate with the RID Master every time it creates an AD object; however, losing a domain's RID Master will eventually lead to an inability to create new objects in the domain since the pools on the DCs will be depleted. In mature AD environments, this would take a considerable length of time as there are relatively few objects created.

Generally, the RID Master role is assigned to the primary Domain Controller (PDC) in a domain because the PDC typically receives the most attention from administrators and, therefore, has high availability. In mature domains, the overhead generated by the RID Master role is negligible. Though this role is not as critical as some of the other FSMO roles, it is still important to ensure connectivity to the RID Master to prevent future AD headaches.

<figure><img src="../../../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">4. PDC Emulator (PDCE)</mark>

### 🔸Understanding the PDC Emulator Role: Explanation and History

Primary Domain Controller (PDC) is a term from the days of Windows NT, when a single DC had a Writable copy of the directory. Today, most DCs in a domain are Writable, but there is still one designated DC that emulates the role of a PDC. Each domain in an Active Directory forest contains one DC with the PDCE role assigned to it.

### 🔸PDC Emulator Functions in AD

The Primary Domain Controller Emulator is responsible for the following functions:

#### 🔸**Time Synchronization**

The PDCE is the authoritative time source for the domain; all workstations and member servers sync their time with the PDC emulator. In a multi-domain forest, the PDCE in the forest Root domain is the timekeeper for all the other PDC emulators in the forest. To maintain accurate timekeeping throughout the forest, the PDC emulator in the Root domain should be configured to synchronize with an external reliable time source, such as NASA's world clock. **Time is a very big deal in Active Directory.** For instance, the Kerberos authentication protocol will fail if the difference between the clock of a requesting host and the clock of the authenticating DC exceeds the specified maximum (5 minutes by default); this helps counter certain malicious activities, such as NTP replay attacks.

#### 🔸**Password Changes and Authentication**

When a user's password is changed, the change is initially made on the DC that authenticated the user. This committed password update is immediately replicated to the domain's PDCE. If an account attempts to authenticate against a DC that has not yet received a recent password change through scheduled replication, the request is then passed to the domain PDCE, which will then process the authentication requests and instruct the requesting DC to either accept or reject it. This behavior ensures that passwords can reliably be processed even if recent changes have not yet fully propagated through scheduled replication.

#### 🔸**Account Lockout Status**

Similarly, if an account gets locked out due to multiple failed login attempts, the lockout is processed at the PDC emulator immediately, and the lockout status is replicated to all DCs in the domain to ensure that a locked-out account cannot log on to another DC. When an administrator unlocks an account, that change is immediately replicated throughout the domain.

#### 🔸**Group Policy Updates**

If updates are made to a Group Policy Object (GPO), they are initially committed to the DC with the PDC Emulator role. This prevents versioning conflicts that could occur if a GPO happened to be modified on two DCs of approximately the same time.

#### 🔸**Backwards Compatibility**

In organizations that still have legacy devices or software that are dependent on Windows NT, the PDCE emulator can serve as a PDC. This includes functioning as the _**Master Browser**_, which collects and distributes information about applications and devices on an AD domain network.

#### 🔸**Distributed File System (DFS)**

By default, DFS root servers will periodically request updated DFS namespace information from the PDCE. This behavior can lead to resource bottlenecks, but enabling the `Dfsutil.exe RootScalability` parameter will allow DFS Root servers to request updates from the closest responding DC.

The PDC Emulator role should be placed on a highly accessible and well-connected, high-performance DC, since the loss of the DC with this role can have an immediate and significant impact on business operations.

<figure><img src="../../../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">5. Infrastructure Master</mark>

### 🔸Role of the Infrastructure Master FSMO Role

Infrastructure Master is a domain-level role whose primary function is handling the references of cross-domain objects in a multi-domain forest. The Infrastructure Master compares objects in its domain against objects in other Domains in the same forest and synchronizes them with the Global Catalog (GC) servers.

### 🔸When and Why Infrastructure Master Is Needed

These actions are not needed in certain cases. Obviously, in environments with only one AD domain, there are no cross-domain references to handle. And if all of the DCs in a domain are global cataloging servers (which is common today because of better network bandwidth), they will all have up-to-date information without solely relying on the Infrastructure Master FSMO role.

### 🔸Infrastructure Master FSMO Role Responsibilities

The Infrastructure Master is assigned the following responsibilities:

#### 🔸**Cross-Domain Object References**

In a multi-domain forest, objects from one domain might be referenced in another domain. A typical example is when a user from one domain is added to a security group in another domain. In this scenario, a placeholder (called a _**“phantom object”**_) is created in the group’s domain to represent the user from the other domain. Phantom objects track and manage persistent references to deleted objects and link-valued attributes that refer to objects in another domain in the forest.

#### 🔸**Updating Group-to-User References**

The Infrastructure Master is responsible for updating an object’s SID and distinguished name (DN) in a cross-domain object reference and translating _**Globally Unique Identifiers (GUIDs)**_, SIDs and DNs between domains in a forest.

#### 🔸**Stale Object Cleanup**

The Infrastructure Master regularly checks its domain for objects that are no longer valid (such as objects from deleted trusts) and removes them.

If a DC with the Infrastructure Master role fails, the impact is mainly administrative. Though cross-domain object link names might not resolve correctly during its absence, cross-domain group memberships will continue to function as normal.

<figure><img src="../../../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

### 🔸FSMO Roles in Forest and Domain Contexts <a href="#fsmo-roles-in-forest-and-domain-contexts" id="fsmo-roles-in-forest-and-domain-contexts"></a>

#### 🔸Forest-Level FSMO Roles

As you can see from the list above, the last two FSMO roles operate forest-wide, meaning only one DC in the forest can be the role holder. In other words, every Active Directory Forest has a single Schema Master and a single Domain Naming Master.

#### 🔸Domain-Level FSMO Roles

The other three FSMO roles operate within the jurisdiction of a single domain. In each domain, there is one Infrastructure Master, one RID Master, and one PDC Emulator. Each domain will host these three FSMO roles in environments with multiple domains on one or more DCs.

### 🔸Managing FSMO Roles <a href="#managing-fsmo-roles" id="managing-fsmo-roles"></a>

#### 🔸Identifying FSMO role holders

Knowing which DCs in your AD environment host the 5 FSMO roles is important. There are multiple ways of identifying the DCs that own FSMO roles. One quick way is using command prompt using the following command:

```
netdom query fsmo /domain:<DomainName>
```

Here is an example:

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/ef28738f3cd5e574f01c44d185002933d0893361-658x258.webp" alt="Image"><figcaption></figcaption></figure>

You can also use PowerShell using the following script:

```
(Get-ADForest).Domains |

ForEach-Object{ Get-ADDomainController -Server $_ -Filter {OperationMasterRoles -like "*"}} | `

Select-Object Domain, HostName, OperationMasterRoles
```

Here is an example below using PowerShell:

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/b1ee54f8478b46add31d8712fa5d7353ac2f2519-780x267.webp" alt="Image"><figcaption></figcaption></figure>

You can also find which DC’s are assigned FSMO roles using Windows Active Directory Tools. Using Active Directory Users and Computers, right-click on your domain and select Operations Masters as shown below:

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/bab40cd284d7b91c834d997f194f9317c53961d8-521x626.webp" alt="Image"><figcaption></figcaption></figure>

Then click on each tab to find the three domain FSMOs.

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/c0f257a79406900c9981f6fe6c37831231f00d30-495x570.webp" alt="Image"><figcaption></figcaption></figure>

You can use _**Active Directory Domains and Trusts**_ to find which DC holds the Domain Naming Master role by right-clicking on Active Directory Domains and Trust and then selecting Operations Master, as shown below.

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/ee03b9032c4d752db14c1ab5549a6d3c4f28b8a2-780x422.webp" alt="Image"><figcaption></figcaption></figure>

Which will then pull up the following pop up to identify the current role holder.

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/a2ce4e2884d686b9afb147a33999d04bcc307eeb-467x342.webp" alt="Image"><figcaption></figcaption></figure>

The process of identifying the Schema Master FSMO is a little more involved. You can find its identity using the Active Directory Schema snap-in; however, the snap-in does not appear by default within Windows Server. To gain access to it you need to register it using the `Schmmgmt.dll` file. To do this, click Start > Run, and type `regsvr32 schmmgmt.dll` in the Open box. Then click OK as shown below.

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/64fe8d0d6daaf3073d186b27499f3fa9bf7c6bc5-468x295.webp" alt="Image"><figcaption></figcaption></figure>

Once successfully registered, you need to do the following:

1. On the Console menu, click **Add/Remove Snap-in**, click Add, double-click Active Directory Schema, click Close, and then click OK.
2. Right-click Active Directory Schema in the top-left pane, and then click Operations Masters to view the server holding the schema master role.

An example is shown in the screenshot below:

<figure><img src="https://cdn.sanity.io/images/r09655ln/production/de01783943c0ddc852530eaf21ac2ea2f3c5536f-780x466.webp" alt="Image"><figcaption></figcaption></figure>

This will give you access to the snap-in from which you can right click on Active Directory Schema and choose Operations Master.

### 🔸Transferring and Seizing FSMO Roles

#### 🔸When and How to Transfer FSMO Roles

While Active Directory will automatically assign the FSMO roles to your DCs, there are times when you may want to transfer a role to another DC. For instance, you may need to take a DC down for maintenance that currently holds an assigned role. Both domain and enterprise admins have the discretion to move these roles between domain controllers as needed.

#### 🔸Seizing FSMO Roles

For FSMO role transfers, both the current holder and the target domain controller roles must be active and network connected. If the current FSMO role holder is unavailable and can’t be restored, a domain or enterprise admin will need to seize the role. As this is a more abrupt move, seizing an FSMO role should only be conducted when necessary.

### 🔸Best Practices and Troubleshooting <a href="#best-practices-and-troubleshooting" id="best-practices-and-troubleshooting"></a>

#### 🔸Optimizing FSMO Role Placement for Greater Efficiency

While there are no hard and fast rules concerning FSMO placement within Active Directory, the following recommendations will garner you the best results:

* Place the PDC Emulator and RID Master on a reliable domain controller with good connectivity, that is readily available to other domain controllers, as their roles are critical for day-to-day Active Directory activities.
* If possible, the Infrastructure Master should not be placed on a global catalog server. This is not possible, of course, if all DCs are global catalog servers.
* Place the two forest-side roles (Schema Master and Domain Naming Master) on the same DC, as they are not utilized very often.

#### 🔸Common Issues and Solutions

There are some key instances that might indicate that an FSMO is unavailable. For instance, any attempt to update the AD schema will result in an error if the Schema Master is down. You will also be unable to add or remove domains in the forest if the Domain Naming Master is not accessible. In these circumstances, you need to confirm which DC has that role and verify that it is accessible.

The inability to access a DC with an assigned FSMO role can result from multiple factors, including:

* The server being offline or powered down
* Network connectivity issues
* DNS configuration errors or failures

Troubleshooting these issues may require you to use network diagnostic tools to verify connectivity throughout the network, verify DNS settings including `SRV` records, and ensure the physical and logical health of the server holding the FSMO role. If the problem persists, consider transferring the role to another healthy DC or, as a last resort, seizing the role if the current holder is permanently unavailable.

### 🔸Monitoring and Auditing FSMO Roles

Because these FSMO roles are so critical, you should regularly monitor the servers that hold these roles. At a very basic level, you can check the event logs on your domain controllers. Specific events can indicate when the FSMO roles were transferred or seized. Your organization may also use monitoring or management software that might have historical data or alerts related to FSMO role changes. There are also third-party tools out there that offer far more functionality.&#x20;

### 🔸Final Thoughts

As we have seen, FSMO roles are important for both business continuity and security. Therefore, it’s vital to audit all changes to your FSMO roles. It is best practice that you automate this monitoring and configure it to alert you to any suspicious change so you can take action before it leads to downtime or a data breach.
