# CHAPTER 7.
# POLICY DELIVERY AND DIRECTORY DATA: GROUP POLICY, SYSVOL, AND NTDS.DIT

## ABSTRACT

Active Directory governs two distinct but inseparable categories of infrastructure: the policy that tells every domain-joined system how to behave, and the data that tells the directory who every principal is and what they are permitted to do. This chapter examines both. Group Policy is the mechanism through which configuration, security settings, software deployment, and administrative controls flow from domain controllers to every workstation, server, and user session in the enterprise. SYSVOL is the shared file system that carries Group Policy Objects and logon scripts across the domain, replicated among domain controllers through the File Replication Service or the Distributed File System Replication engine. NTDS.dit is the Extensible Storage Engine database file that is Active Directory — every identity, every credential, every relationship, every attribute in the domain stored in a single structured file on every domain controller. Together, these three components represent some of the most valuable and most attacked infrastructure in a Windows environment. An adversary who controls Group Policy controls every domain-joined system. An adversary who extracts NTDS.dit holds every credential in the domain. This chapter examines how each component works, how it is structured, and why its integrity is foundational to the identity trust system examined throughout this book.

## KEYWORDS

Group Policy; Group Policy Object; SYSVOL; NTDS.dit; Extensible Storage Engine; Directory Information Tree; Credential storage; Domain controller; DFSR; Password encryption key

## KEY TERMS

- **Group Policy Object (GPO):** A collection of policy settings stored in Active Directory and on SYSVOL that defines configuration and security requirements applied to users and computers in a domain.

- **Group Policy Container (GPC):** The Active Directory object in the domain partition that stores a GPO's metadata, version number, and links.

- **Group Policy Template (GPT):** The file system component of a GPO stored in SYSVOL, containing the actual policy settings, scripts, and associated files.

- **SYSVOL:** A shared directory tree replicated among all domain controllers in a domain, hosting Group Policy Templates, logon scripts, and other domain-wide files.

- **File Replication Service (FRS):** The legacy Windows service that replicated SYSVOL content among domain controllers, deprecated and replaced by DFSR.

- **Distributed File System Replication (DFSR):** The modern replication engine that replaced FRS for SYSVOL replication, providing more efficient and reliable content synchronization among domain controllers.

- **NTDS.dit:** The Active Directory database file — New Technology Directory Services, Directory Information Tree — stored on every domain controller and containing the complete directory data for the domain.

- **Extensible Storage Engine (ESE):** The transactional database engine underlying NTDS.dit, also used by Exchange Server and other Microsoft products.

- **Password Encryption Key (PEK):** A domain-unique symmetric key used to encrypt password hash values stored in NTDS.dit, itself encrypted with the SYSTEM boot key.

- **SYSTEM hive:** The registry hive containing the boot key (SYSKEY) used to encrypt the PEK, required alongside NTDS.dit to extract usable credential data.

- **Volume Shadow Copy Service (VSS):** The Windows infrastructure that creates point-in-time snapshots of volumes, commonly used to extract a copy of NTDS.dit from a live domain controller without taking the file system offline.

---

## 7.1 THE TWO PILLARS OF DOMAIN CONTROL

Every domain controller in an Active Directory environment is simultaneously responsible for two distinct categories of critical data. The first is configuration authority — the policies, settings, scripts, and controls that determine how every domain-joined system behaves, what software it runs, what security settings it enforces, and what users can and cannot do. The second is identity authority — the structured record of every principal in the domain, their credentials, their group memberships, their permissions, their relationships, and their history. These two categories are carried by different mechanisms, stored in different places, and replicated through different systems. But they share one fundamental property: whoever controls them controls the domain.

Group Policy and SYSVOL carry the configuration authority. NTDS.dit carries the identity authority. Neither is more important than the other, and both are attack targets of the highest order. This chapter examines how each works at the structural level — not because the mechanics are interesting for their own sake, but because understanding how they work is the prerequisite for understanding how they fail, how they are attacked, and how those attacks are detected and defended.

---

## 7.2 GROUP POLICY: HOW CONFIGURATION AUTHORITY FLOWS

Group Policy is the mechanism through which an Active Directory domain administrator can define a configuration requirement once and have it automatically applied to thousands of machines or user sessions. It is one of the most powerful features of Windows domain management and, predictably, one of the most powerful levers an adversary seeks to control.

### 7.2.1 WHAT GROUP POLICY ACTUALLY IS

Group Policy is not a single object or a single file. It is a two-part system. The policy settings, metadata, and version information are stored as an object in Active Directory — the Group Policy Container (GPC). The actual configuration content, scripts, templates, and associated files are stored on SYSVOL — the Group Policy Template (GPT). When a Group Policy Object (GPO) is created, both components are created simultaneously, linked together by a common GUID (Globally Unique Identifier). The GPC lives in `CN=Policies,CN=System,DC=domain,DC=tld`. The GPT lives in `\\domain.tld\SYSVOL\domain.tld\Policies\{GUID}`. If the two components become out of sync — a common occurrence in poorly maintained environments — Group Policy behaves unpredictably, with some settings applying from stale content and others failing silently.

A GPO is linked to a site, a domain, or an Organizational Unit (OU). When a computer boots or a user logs on, the Group Policy client evaluates which GPOs apply, downloads and processes the relevant GPTs, and applies the settings. This evaluation follows a defined inheritance order: Local Policy is processed first, then Site GPOs, then Domain GPOs, then OU GPOs from the top of the OU hierarchy down to the OU containing the object. Settings configured at a lower level in the hierarchy override conflicting settings from higher levels, unless the higher-level GPO is enforced — in which case it cannot be overridden. Understanding this inheritance model is essential for both administering policy and for assessing whether a specific setting is actually applying to a specific object.

### 7.2.2 WHAT GROUP POLICY CAN DO

Group Policy is not limited to desktop backgrounds and password complexity requirements. The scope of what Group Policy can configure is vast, and most practitioners underestimate it.

**Security settings:** Account policies (password complexity, lockout thresholds, Kerberos ticket lifetime), local policies (user rights assignments, audit policy, security options), the Windows Firewall configuration, software restriction policies, AppLocker rules, credential protection settings (Credential Guard, LSASS protection), and the entire Windows Security configuration baseline. When this book discusses controls like "enforce SMB signing," "enable LDAP signing," "enable Credential Guard," or "configure audit policy" — Group Policy is the delivery mechanism for almost all of them.

**Software deployment:** Windows Installer packages can be assigned to computers (installed at startup) or published to users (available for installation). This makes Group Policy a software distribution platform, which also makes it a malware distribution platform in the hands of an adversary with write access to the right GPO.

**Script execution:** Startup scripts, shutdown scripts, logon scripts, and logoff scripts can all be delivered through Group Policy. Scripts configured in a GPO are stored in the GPT on SYSVOL and execute in the machine or user context depending on their type.

**Registry configuration:** Group Policy Preferences (GPP) allows administrators to configure arbitrary registry values, drive mappings, environment variables, scheduled tasks, services, and local users and groups. It was through GPP that one of Active Directory's most historically significant credential exposures occurred — the `cpassword` vulnerability, covered in Chapter 17.

**Administrative template settings (ADMX):** These are XML-based policy definitions that expose thousands of registry-backed settings for Windows, Office, Internet Explorer, Edge, and any application that ships or supports ADMX templates. Virtually every Windows feature that has a documented Group Policy setting is controlled through an ADMX template.

The breadth of Group Policy's reach is exactly why it is a primary target. A single GPO linked to the domain root, with no domain user filter, applied with enforcement — that GPO's settings reach every computer and user in the domain. An adversary who creates or modifies such a GPO has a direct execution channel to every domain-joined system.

### 7.2.3 GROUP POLICY PROCESSING AND THE CLIENT-SIDE EXTENSIONS

Group Policy processing on the client is handled by a set of Client-Side Extensions (CSEs) — DLLs registered in the registry that each handle a specific category of policy. When the Group Policy client processes a GPO, it passes each section of the policy to the appropriate CSE. The Security extension handles security settings. The Registry extension handles administrative template registry values. The Scripts extension handles startup/shutdown/logon/logoff scripts. The Software Installation extension handles MSI deployment.

CSEs are triggered at two primary events: computer startup (machine policy processing) and user logon (user policy processing). Between these events, Group Policy refreshes in the background approximately every 90 minutes, with a randomized offset of up to 30 minutes to prevent all machines from contacting domain controllers simultaneously. Domain controllers themselves refresh every 5 minutes. Security settings are always reapplied at each refresh, even if the GPO version has not changed. Most other settings are only reprocessed if the GPO version number has incremented — though this behavior can be overridden by enabling "Process even if the Group Policy Objects have not changed."

A significant defense implication follows from this refresh behavior: a GPO-based configuration change, whether made by an administrator or an adversary, will propagate to all affected machines within roughly two hours under default settings. This is both the mechanism that makes Group Policy a powerful management tool and the mechanism that makes it a powerful lateral execution channel.

### 7.2.4 GPO PERMISSIONS AND THE DELEGATION MODEL

Every GPO has a security descriptor, and that security descriptor determines who can read it, who can apply it, who can edit it, and who has full control over it. The default permissions on a new GPO grant Domain Admins and SYSTEM full control, and grant Authenticated Users read access plus Apply Group Policy permission. The Apply Group Policy permission is what causes a GPO to be processed by an object — a computer or user that cannot read a GPO, or that has Deny Apply Group Policy on the GPO's DACL, will not process that GPO even if the GPO is linked to a container that includes the object.

Security filtering, as this permission model is commonly called, is the mechanism administrators use to scope GPOs to specific computers or users within a linked OU. A GPO linked to a domain-root OU but with Authenticated Users removed and a specific security group granted Apply Group Policy will only apply to members of that group.

The delegation model has a critical security implication that many administrators miss: the ability to **link** a GPO to an OU is separate from the ability to **edit** a GPO. An administrator who has the Link GPOs permission on an OU can link any existing GPO — including maliciously configured ones — to that OU. An administrator who has edit rights on a GPO can modify its settings without necessarily having link permissions anywhere. These two permissions are frequently over-granted, creating paths where a principal with limited apparent authority can either modify an existing GPO affecting many systems, or link a new GPO to a high-value OU.

---

## 7.3 SYSVOL: THE FILE SYSTEM THAT CARRIES POLICY

SYSVOL is a shared folder tree that exists on every domain controller. Its contents are replicated among all domain controllers so that every domain controller serves an identical copy of the SYSVOL content to clients. This replication is what allows any domain controller to service Group Policy requests — the client connects to its closest domain controller and retrieves GPTs from SYSVOL without needing to contact any specific server.

### 7.3.1 SYSVOL STRUCTURE

The SYSVOL tree sits in a path defined during domain controller promotion, typically `C:\Windows\SYSVOL`. The actual shared content is under `SYSVOL\domain\`, which is shared as `\\domain.tld\SYSVOL`. Within this tree, two subdirectories carry the critical content.

`Policies\` contains one subdirectory per GPO, named by the GPO's GUID. Within each GPO directory: `Machine\` holds machine-side policy content, `User\` holds user-side policy content, and `GPT.INI` is the version file that the Group Policy client reads to determine whether it needs to download updated content. When an administrator saves changes to a GPO, the version number in both the GPC object in Active Directory and the GPT.INI file on SYSVOL is incremented. The client compares its cached version against the current version and downloads the updated GPT only when the versions differ.

`Scripts\` contains logon and logoff scripts configured through Group Policy. These are often overlooked during security assessments, but logon scripts that execute in the user context have been used in both legitimate administration and in persistence scenarios where an adversary adds content to a script that already exists and is trusted.

### 7.3.2 FRS AND DFSR: THE REPLICATION ENGINES

SYSVOL replication has gone through two distinct engine generations, and the generation an environment runs matters for both operational stability and security assessments.

**File Replication Service (FRS)** was the original SYSVOL replication mechanism, introduced with Windows 2000 Server. FRS is deprecated. Microsoft stopped supporting it with Windows Server 2019, and environments still using FRS represent a legacy posture that carries operational risk. FRS uses a multi-master replication model where changes made on any domain controller propagate to all others, but it has known limitations around collision handling, journal wrapping, and recovery from replication failures. When FRS fails, SYSVOL replication stalls silently in some cases, leaving different domain controllers serving different versions of GPO content — a condition known as a SYSVOL divergence, which produces inconsistent policy application across the environment.

**Distributed File System Replication (DFSR)** is the modern replacement, introduced with Windows Server 2008. DFSR uses a compression-efficient, change-journal-based replication mechanism that handles large file sets more reliably than FRS and provides better recovery mechanisms. The migration from FRS to DFSR uses a specific four-phase process that must be completed in sequence; environments that were partially migrated or that promoted new domain controllers after completing the migration but failed to replicate the DFSR configuration can end up in a hybrid state.

For a security practitioner, the SYSVOL replication engine matters because DFSR provides better audit and monitoring capabilities, and because the migration state of SYSVOL replication is an indicator of overall domain controller hygiene. An environment still on FRS in 2026 has not been maintaining its domain controller infrastructure to a current standard, which correlates with other maintenance gaps worth examining.

### 7.3.3 SYSVOL AS AN ATTACK SURFACE

SYSVOL is readable by all authenticated domain users by design — clients must be able to read GPTs to apply Group Policy. This means that any domain user can browse `\\domain.tld\SYSVOL` and read the content of every GPO, every logon script, and every other file stored there. In environments where SYSVOL contains hard-coded credentials in logon scripts, configuration files, or Group Policy Preferences XML files, this read access becomes a credential exposure affecting every authenticated user in the domain.

SYSVOL content is also executable in the context of the systems and users that process it. A logon script stored in SYSVOL executes in the user's context on every logon. A startup script executes in the SYSTEM context on every reboot. An adversary with write access to SYSVOL — either through compromising a domain controller, through misconfigured SYSVOL share permissions, or through a GPO write permission that includes script content — can use this execution channel to deliver code to any system that processes the associated policy.

---

## 7.4 NTDS.DIT: WHAT IT IS, WHAT IT MEANS, AND WHY EVERYTHING DEPENDS ON IT

This section requires more space than the others in this chapter because it is addressing something that most books about Active Directory assume the reader already understands — but which, in practice, most practitioners understand only superficially. The question of what NTDS.dit actually is, what it contains, how its credential storage works, and why its extraction represents the complete compromise of a domain deserves a complete and careful treatment. That is what follows.

### 7.4.1 THE NAME ITSELF

NTDS.dit stands for **New Technology Directory Services — Directory Information Tree**.

**New Technology Directory Services (NTDS)** is Microsoft's name for the directory service engine underlying Active Directory. The "New Technology" prefix is the same one carried by Windows NT itself, distinguishing the NT-era architecture from the older DOS-based and LAN Manager-era systems it replaced. Directory Services describes the function: a service that maintains a structured directory of network objects.

**Directory Information Tree (DIT)** is a term drawn directly from the X.500 directory standard developed by the International Telecommunication Union (ITU) in the 1980s. In X.500 and its derivatives — including Lightweight Directory Access Protocol (LDAP), which is itself a simplified implementation of X.500 concepts — a Directory Information Tree is the hierarchical structure of entries that makes up the directory, branching from a root through containers and leaf objects. The `.dit` extension tells you precisely what kind of data the file holds: it is the file that *is* the Directory Information Tree, the physical storage container for the entire logical structure of the Active Directory domain.

So in full: **NTDS.dit** = the New Technology Directory Services implementation of a Directory Information Tree. It is the file that *is* Active Directory. Every user account, every computer account, every group, every Group Policy Object link, every permission, every password hash, every Kerberos key, every attribute on every object in the domain — all of it lives in that one file on every domain controller.

### 7.4.2 THE EXTENSIBLE STORAGE ENGINE

NTDS.dit is not a flat file. It is not a proprietary Microsoft-only format. It is a structured database built on the **Extensible Storage Engine (ESE)** — a transactional, record-based database engine that Microsoft has used across multiple products including Exchange Server, Windows Search, Windows Update, Active Directory Lightweight Directory Services (AD LDS), and several other components.

ESE was originally developed by Microsoft as the Jet Blue engine in the early 1990s and has evolved continuously since. It is a B-tree database, meaning records are organized in a balanced tree structure that provides efficient lookup, insertion, and deletion operations. The "extensible" in its name refers to its ability to handle variable-length and variable-schema records, making it suited to a directory that stores many types of objects with different attributes.

The ESE database format organizes data into **tables** — structured collections of records with defined columns — and maintains those tables in **pages** of a fixed size (8 KB by default in NTDS.dit). Related pages are grouped into **spaces**, and multiple spaces form the complete database file. For integrity purposes, ESE uses a write-ahead logging model: before any change is committed to the database file itself, it is first written to a transaction log. If the system crashes mid-write, the transaction log allows the database to be recovered to a consistent state on restart, either by replaying completed transactions or by rolling back incomplete ones.

The files associated with an NTDS.dit database are:

- **NTDS.dit** — the main database file, located in `%SystemRoot%\NTDS\` on every domain controller
- **edb.log** — the current active transaction log, always exactly 10 MB
- **edbXXXXX.log** — filled transaction logs awaiting checkpoint advancement
- **edb.chk** — the checkpoint file recording how far committed transactions have been flushed to the database file
- **res1.log and res2.log** — two pre-allocated 10 MB reserve log files that provide space for a final transaction flush if the disk fills completely, preventing an ungraceful shutdown

Understanding that these files form a unit matters for any forensic, backup, or extraction scenario: a copy of NTDS.dit without the associated transaction logs may be in an inconsistent state, and a modern forensic extraction of the database must either take a consistent snapshot (via VSS) or run ESE's integrity check and recovery tools before the database can be read.

### 7.4.3 THE TABLES INSIDE NTDS.DIT

The ESE database of NTDS.dit contains several tables, but three are directly relevant to security practitioners.

**The Data Table (datatable):** This is the core of the directory. Every Active Directory object — every user, computer, group, GPO, site, subnet, trust, certificate template, and every other directory object — is stored as a record in the data table. Each record has a fixed structure with hundreds of potential columns, one per possible Active Directory attribute, though any given record will only populate the columns relevant to its object class. The data table for a large enterprise domain can contain millions of records and grow to tens of gigabytes.

The most sensitive columns in the data table from a credential perspective are:

- **unicodePwd (column 0x9005a):** Stores the NT hash (and historically the LM hash) of the account's current password, encrypted with the Password Encryption Key (PEK).
- **dbcs-Pwd:** The LM hash, similarly encrypted (present only for older accounts or where LM storage is enabled).
- **supplementalCredentials:** A binary blob containing additional credential material including Kerberos keys (AES128, AES256, DES, RC4 variants), NTLM hash variants, and potentially WDigest hashes. This is where the full Kerberos long-term key material lives.
- **ntPwdHistory and lmPwdHistory:** Stores the encrypted hashes of previous passwords, enforcing the password history policy.
- **unicodePwdBackup:** Used in certain credential roaming and recovery scenarios.

**The Link Table (link_table):** Directory objects frequently reference other objects — a group contains members, a user belongs to groups, an OU contains computers. These relationships are stored as records in the link table rather than in the data table, because a many-to-many relationship (a user in hundreds of groups, a group with thousands of members) cannot be efficiently stored as columns on the parent record. The link table is critical for understanding group membership and the access control relationships that underpin privilege mapping.

**The Security Descriptor Table (sd_table):** Access control is too expensive to store in full on every individual object. Instead, Windows uses a security descriptor deduplication model: unique security descriptors are stored once in the SD table, and objects in the data table reference their descriptor by a hash key. This table is what enables the efficient application of inherited permissions and the storage of ACLs across millions of directory objects.

### 7.4.4 HOW PASSWORDS ARE STORED IN NTDS.DIT

This is the section that matters most to a practitioner trying to understand what extracting NTDS.dit actually gives an attacker, so it deserves explicit detail at each layer of the encryption stack.

**Layer 1 — The raw hash.** A user's password is never stored in plaintext in the directory. When a password is set, Windows computes the NT hash (MD4 of the UTF-16LE encoded password) and, depending on configuration, the LM hash. This is the raw credential material — the NT hash is what enables Pass-the-Hash, and it is what Hashcat operates against in offline cracking.

**Layer 2 — The Password Encryption Key (PEK).** The raw NT hash is not stored as-is in the data table. It is first encrypted with a domain-wide symmetric key called the Password Encryption Key. The PEK is unique per domain, generated when the domain is created, and stored in the directory itself — specifically as an attribute on the `CN=NTDS Settings` object. The PEK is encrypted with the SYSTEM boot key.

**Layer 3 — The SYSTEM boot key (SYSKEY).** The boot key is a 128-bit symmetric key derived from four scrambled registry values in the SYSTEM hive: `JD`, `Skew1`, `GBG`, and `Data`, found under `HKLM\SYSTEM\CurrentControlSet\Control\Lsa`. These four values store portions of the boot key in obfuscated form, and the actual key is reconstructed by a specific combination algorithm. This is the outermost encryption layer — the key that protects the PEK.

**The full decryption chain to recover a password hash:**

```
SYSTEM hive (4 registry values)
        ↓  [reconstruct boot key]
    SYSKEY (128-bit boot key)
        ↓  [decrypt]
    PEK (Password Encryption Key, stored in NTDS.dit)
        ↓  [decrypt]
    Encrypted NT hash (stored in datatable, unicodePwd column)
        ↓  [decrypt]
    Raw NT hash (16 bytes — now usable for PtH or offline cracking)
        ↓  [optional: offline dictionary/brute-force]
    Plaintext password
```

This chain is why an attacker needs **both** NTDS.dit **and** the SYSTEM hive to extract usable credentials. Either file alone is insufficient — NTDS.dit without the SYSTEM hive cannot yield the boot key to decrypt the PEK, and the SYSTEM hive without NTDS.dit has nothing to decrypt. Tools such as Impacket's `secretsdump.py`, the `ntdsutil` command, and various other credential extraction utilities all follow this decryption chain to reconstruct plaintext or hash-form credentials from the database.

### 7.4.5 SUPPLEMENTALCREDENTIALS AND KERBEROS KEY MATERIAL

The `unicodePwd` attribute contains only the NT hash — the RC4 Kerberos key derivation input. The full Kerberos long-term key material, including the AES128 and AES256 keys, lives in the `supplementalCredentials` binary blob alongside several other credential structures.

The `supplementalCredentials` attribute contains a serialized structure with multiple credential packages. The packages relevant to Kerberos are:

**Kerberos-Newer-Keys:** Contains the AES256-CTS-HMAC-SHA1-96 key, the AES128-CTS-HMAC-SHA1-96 key, and the DES keys. These are the long-term Kerberos keys derived from the password using the Kerberos AES string-to-key function — the same keys the Key Distribution Center (KDC) uses to decrypt AS-REQ pre-authentication and to encrypt AS-REP content. When an attacker extracts these AES keys, they can forge AES-encrypted Kerberos tickets, create Golden Tickets with AES encryption (not just RC4), and operate in environments where RC4 has been disabled.

**Primary:Kerberos:** Contains the older DES and RC4 Kerberos keys for backward compatibility.

**Primary:WDigest:** If WDigest authentication is enabled on the domain controller, this package contains a set of MD5-derived password representations in cleartext-equivalent form. WDigest is disabled by default since Windows 8.1/Server 2012 R2 via the `HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest\UseLogonCredential` registry value, but environments that have not enforced this setting or have applications that require WDigest may have cleartext-equivalent credentials recoverable from this package for every account in the domain.

**Primary:CLEARTEXT:** Present only for accounts configured for reversible encryption storage (a policy setting that should essentially never be enabled). If it is present, the password is stored in a recoverable form.

### 7.4.6 THE ESE LOCK AND LIVE DATABASE ACCESS

While the domain controller is running, ESE holds an exclusive lock on NTDS.dit. The file cannot be opened, copied, or read by standard file system tools while Active Directory Domain Services are running — Windows will refuse the operation with a sharing violation error. This lock exists to maintain database consistency; ESE coordinates all reads and writes through its own engine, and direct file system access would bypass the transaction management that keeps the database coherent.

This locking mechanism is why NTDS.dit extraction requires one of three specific approaches:

**Volume Shadow Copy Service (VSS):** VSS creates a point-in-time snapshot of the volume at the block level, capturing the database file in a consistent state without requiring the Active Directory service to be stopped. The snapshot is created nearly instantaneously. Once a VSS snapshot exists, the snapshot volume can be mounted and NTDS.dit can be read from the snapshot because the snapshot is a historical view, not the live database. VSS snapshots are created automatically by Windows Server Backup and other backup products, and can be created manually with the `vssadmin` command or via WMI. The `ntdsutil` command's IFM (Install From Media) function also uses VSS internally.

**Offline extraction:** If the domain controller is stopped or if NTDS.dit is copied from a backup, the ESE lock does not apply. The file can be read directly once removed from the running system context, provided the associated transaction logs are also available.

**DCSync replication:** This approach does not touch NTDS.dit at all. Instead, it uses the directory replication protocol to request specific credential attributes directly from a live domain controller, as if the requesting system were another domain controller synchronizing its replica. DCSync produces the same credential material as physical database extraction but operates entirely over the network without requiring file system access to the domain controller. It is examined in depth in Chapter 26.

### 7.4.7 REPLICATION AND THE DISTRIBUTED NATURE OF NTDS.DIT

Every domain controller in a domain maintains its own complete replica of NTDS.dit. These replicas are kept synchronized through Active Directory replication — the same process examined at the substrate level in Chapter 3. What replication means in the context of NTDS.dit is that the database is not a single file with a single point of failure or a single extraction target. Any domain controller's NTDS.dit contains the complete domain credential store. An attacker who reaches any domain controller — not necessarily the Primary Domain Controller (PDC) Emulator or any specific domain controller — has access to the complete credential database through that controller's replica.

This has important implications for incident response. In a multi-domain-controller environment, determining whether NTDS.dit was accessed or extracted requires examining every domain controller, not just the most prominent one. The replication metadata stored in the database — specifically the Originating DSA (Directory System Agent) and the Update Sequence Number (USN) for each attribute — can be used to understand when changes propagated and through which controllers, which is relevant for understanding the timeline of a compromise that involved directory modifications.

### 7.4.8 NTDS.DIT IN THE CONTEXT OF THE FEDERAL IDENTITY TRUST SYSTEM

In federal and Department of Defense environments, the stakes of NTDS.dit exposure extend beyond the domain itself. A domain that participates in a FICAM-aligned federated architecture — trusting certificates from the Federal Public Key Infrastructure, synchronizing identities to Microsoft Entra ID, federating with mission partners — is a trust anchor for that entire ecosystem. Extraction of NTDS.dit from a domain controller in such an environment provides not only the credentials for every account in that domain but also the Kerberos keys that can be used to forge tickets accepted by every trusting service and partner environment.

The krbtgt account's credential material, stored in NTDS.dit with the same encryption layering as all other accounts, is the key to the entire domain's Kerberos trust. Its AES keys, once extracted, enable Golden Ticket forgery for the lifetime of those keys — and because Golden Tickets are verified against the krbtgt key embedded in the ticket rather than against the directory, they remain valid even if the actual krbtgt password is later reset once (requiring the well-known double-reset procedure to fully invalidate outstanding tickets, examined in Chapter 40).

In short: the extraction of NTDS.dit is not a credential theft incident. It is the complete and total compromise of everything the domain's identity authority vouches for.

---

## 7.5 GROUP POLICY, SYSVOL, AND NTDS.DIT AS CONNECTED ATTACK SURFACE

These three components do not exist in isolation, and the attacks that target them frequently chain across all three. A thorough understanding of the attack surface requires seeing them as a connected system rather than three separate concerns.

Group Policy can be weaponized to deliver code to every domain-joined system — but doing so requires write access to either the GPO object in Active Directory (the GPC) or to the GPT on SYSVOL, and link permissions on the target OU. An adversary seeking this capability is either targeting Active Directory write permissions or targeting SYSVOL write permissions, both of which require significant existing privileges.

SYSVOL can expose credentials through logon scripts, Group Policy Preferences XML, configuration files, and other content that administrators store there for convenience. This exposure requires only authenticated user access to read, making it one of the most accessible credential sources in an Active Directory environment.

NTDS.dit requires domain controller access for physical extraction, or domain-level replication rights for DCSync. It is the highest-value target and the most protected. But it is also the target whose extraction provides the most comprehensive impact — every other identity-related attack in this book produces a subset of what NTDS.dit extraction produces in full.

The defensive architecture for all three follows from understanding their value. Group Policy infrastructure requires the same Tier 0 treatment as domain controllers because GPO write access is functional equivalent to code execution rights across the domain. SYSVOL requires hygiene — no credentials, no sensitive content, no permanent scripts that have outlived their purpose. NTDS.dit and the domain controllers that host it require physical security, network access controls, detailed audit logging, and the monitoring architecture developed in Part III.

---

## 7.6 SUMMARY AND TRANSITION

This chapter has examined Group Policy, SYSVOL, and NTDS.dit as the policy delivery and identity data infrastructure of Active Directory. Group Policy is the configuration authority that flows outward from domain controllers to every system in the domain, carried by the two-part GPO architecture and processed through client-side extensions at startup and logon. SYSVOL is the replicated file system that carries Group Policy Templates and scripts, readable by all authenticated users and writable — critically — by those with GPO edit rights and SYSVOL permissions. NTDS.dit is the Extensible Storage Engine database that is Active Directory itself: every object, every attribute, every credential in the domain, stored in a single file on every domain controller, protected by a layered encryption chain that requires both the database and the SYSTEM hive to unwrap.

The credential storage architecture of NTDS.dit — the NT hash, the PEK, the SYSKEY, the supplementalCredentials blob with its AES Kerberos keys and optional WDigest entries — is the foundation for understanding nearly every credential-based attack in Part II. DCSync, NTDS.dit extraction, Pass-the-Hash, Pass-the-Ticket, Golden Tickets, and Kerberoasting all operate against some portion of what this chapter has described. The tooling changes, the access requirements differ, but the target is always some derivative of what NTDS.dit holds.

The next chapter completes Part I by establishing the assessment and baseline engineering methodology that connects this foundational knowledge to operational practice — teaching how to evaluate an identity trust system against its intended configuration, locate where it has drifted, prioritize what must be corrected, and validate that corrections have taken effect before an adversary discovers what was left open.

---

## ACRONYMS

ACE — Access Control Entry · ACL — Access Control List · AD — Active Directory · AD LDS — Active Directory Lightweight Directory Services · ADMX — Administrative Template XML · AES — Advanced Encryption Standard · CSE — Client-Side Extension · DACL — Discretionary Access Control List · DC — Domain Controller · DFSR — Distributed File System Replication · DIT — Directory Information Tree · ESE — Extensible Storage Engine · FICAM — Federal Identity, Credential, and Access Management · FRS — File Replication Service · GPO — Group Policy Object · GPC — Group Policy Container · GPP — Group Policy Preferences · GPT — Group Policy Template · GUID — Globally Unique Identifier · IFM — Install From Media · ITU — International Telecommunication Union · KDC — Key Distribution Center · LDAP — Lightweight Directory Access Protocol · NTDS — New Technology Directory Services · NTLM — New Technology LAN Manager · OU — Organizational Unit · PDC — Primary Domain Controller · PEK — Password Encryption Key · PtH — Pass-the-Hash · RPC — Remote Procedure Call · SMB — Server Message Block · USN — Update Sequence Number · VSS — Volume Shadow Copy Service · WMI — Windows Management Instrumentation

## REFERENCES

1. Microsoft. Group Policy Overview. Microsoft Learn. https://learn.microsoft.com/windows-server/identity/ad-ds/manage/group-policy/group-policy-overview (accessed July 19, 2026).
2. Microsoft. SYSVOL and Group Policy. Microsoft Learn. https://learn.microsoft.com/windows-server/identity/ad-ds/ (accessed July 19, 2026).
3. Microsoft. Migrate SYSVOL replication to DFS Replication. Microsoft Learn. https://learn.microsoft.com/windows-server/storage/dfs-replication/migrate-sysvol-to-dfsr (accessed July 19, 2026).
4. Microsoft. Active Directory Database Mounting Tool (Snapshot Viewer). Microsoft Learn. https://learn.microsoft.com/windows-server/identity/ad-ds/ (accessed July 19, 2026).
5. Microsoft. Extensible Storage Engine Reference. Microsoft Learn. https://learn.microsoft.com/windows/win32/extensible-storage-engine/ (accessed July 19, 2026).
6. Microsoft. Volume Shadow Copy Service. Microsoft Learn. https://learn.microsoft.com/windows-server/storage/file-server/volume-shadow-copy-service (accessed July 19, 2026).
7. Fortra. Impacket — secretsdump.py. https://github.com/fortra/impacket (accessed July 19, 2026).
8. National Institute of Standards and Technology. Digital Identity Guidelines (SP 800-63-4). July 2025. https://csrc.nist.gov/pubs/sp/800/63/4/final (accessed July 19, 2026).
9. Microsoft. How Credentials Are Protected in Windows. Microsoft Learn. https://learn.microsoft.com/windows-server/security/credentials-protection-and-management/ (accessed July 19, 2026).
