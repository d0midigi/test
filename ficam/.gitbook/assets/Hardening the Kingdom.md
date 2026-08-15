Chapter X: Hardening the Kingdom

**Sub-title:** _Implementing Tiered Administration and Zero Trust Architecture_

**12.1 The Death of the "Flat" Network**

- **The Problem of Identity Overlap:** Why a Domain Admin should never log into a workstation.
- **The Enterprise Access Model:** Transitioning from "Tiered Models" to a modern, identity-centric security boundary.

**12.2 Implementing the Tiered Administrative Model**

- **Tier 0 (The Control Plane):** Isolating Domain Controllers, PKI, and AD FS.
- **Tier 1 (The Management Plane):** Securing application servers and databases.
- **Tier 2 (The User Plane):** Hardening standard workstations and user identities.

**12.3 Hardening with Group Policy Objects (GPO)**

- **Restricted Groups:** Enforcing exactly who is allowed in local "Administrators" and "Remote Desktop Users" groups.
- **User Rights Assignment:** Using "Deny log on locally" and "Deny log on through Remote Desktop Services" to "trap" admins in their designated tiers.
- **Protected Users Security Group:** A deep dive into the most powerful native AD protection that disables NTLM and RC4 for sensitive accounts.

**12.4 Local Administrator Password Solution (Windows LAPS)**

- **Breaking Lateral Movement:** How LAPS prevents an attacker from using one compromised local admin password to hop across the entire domain.
- **Native vs. Legacy LAPS:** Moving to the Windows LAPS integrated directly into the OS.

**12.5 Monitoring the "Unchangeable"**

- **AdminSDHolder & SDProp:** Understanding the background process that protects privileged ACLs and how to monitor it for "unauthorized" changes.
- **GPO Integrity:** Using Microsoft Security Compliance Toolkit to baseline and audit policy changes.

---

The "Security Architect" Prompt

Use this prompt to generate the technical details for Section 12.3. It is designed to get the AI to provide exact GPO paths and registry settings.

> **Prompt:** "Act as a Senior Infrastructure Security Architect. I am writing the 'Hardening' chapter of my Active Directory book.
> 
> 1. Provide a technical guide on configuring the **'Protected Users'** security group. Explain the specific protocol changes that occur once a user is added (e.g., Kerberos delegation, NTLM caching, and DES/RC4 usage).
> 2. Detail the exact **GPO paths** (under Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > User Rights Assignment) required to implement a **Tiered Administrative Model**.
> 3. List the **Event IDs** that are generated when a 'Protected User' fails to authenticate because of a restriction, allowing a defender to troubleshoot 'breaking' legacy applications.
> 
> **Format as a high-level implementation guide with tables for GPO settings and a troubleshooting checklist.**"

---

Pro-Tip for your Book:

Include a section on **"PAWs" (Privileged Access Workstations)**. Explain that for an administrator, the **device** is just as important as the **account**. An admin on a compromised laptop is no longer an admin; they are a liability.

**Would you like to wrap up the book with "Chapter 13: Incident Response & Disaster Recovery" (How to rebuild the domain after a total ransomware event)?**

[](https://labs.google.com/search/experiment/22)

yes

This final chapter is the "emergency glass" your readers will break. It focuses on the 

**Microsoft Forest Recovery Guide** and the high-stakes reality of restoring a "poisoned" domain after a ransomware event. 

---

Chapter 13: The Day After — Incident Response & Total Forest Recovery

**Sub-title:** _Rebuilding Identity from the Ashes of a Breach_

**13.1 Scoping the Destruction** 

- **The "Clean Source" Problem:** Identifying the last known-good backup that isn't already "pre-infected" with backdoors.
- **Isolating the Blast Radius:** Step-by-step containment to prevent re-infection during the restoration process. 

**13.2 The Forest Recovery Roadmap**

- **Phase 1: Initial Recovery:** Recovering one Domain Controller (DC) for each domain in total isolation.
- **Phase 2: Seizing Control:** Using `ntdsutil` or PowerShell to seize **FSMO roles** from "dead" or compromised DCs.
- **Phase 3: Metadata Cleanup:** Using the Microsoft Metadata Cleanup procedure to scrub evidence of destroyed domain controllers from the database. 

**13.3 Sanitizing the Identity Store**

- **The KRBTGT Double-Reset:** Why you must reset the `krbtgt` password **twice** to invalidate all existing Golden Tickets.
- **Trust Password Resets:** Securing the "inter-domain" borders by cycling trust passwords to prevent lateral movement from compromised sub-domains.
- **Privileged Account Scrubbing:** Auditing the **AdminSDHolder** and resetting all Enterprise and Domain Admin passwords. 

**13.4 Detecting Post-Recovery Backdoors**

- **Shadow Admins:** Finding accounts with hidden "GenericAll" or "WriteDacl" permissions that backups might have re-introduced.
- **Persistence Hunting:** Checking for rogue **GPOs**, scheduled tasks, or unauthorized **Service Principal Names (SPNs)**. 

**13.5 Post-Mortem & Hardening**

- **The "Lessons Learned" Cycle:** Mapping the breach back to the MITRE ATT&CK framework.
- **Establishing Immutable Backups:** Moving toward **Offline/Air-gapped** storage to ensure the next attack can't delete the recovery path. 

---

The "Disaster Recovery" Prompt

Use this with **DeepSeek-R1** or **GPT-4o** to get the precise commands for the most critical recovery step.

> **Prompt:** "Act as a Lead Incident Responder specialized in Active Directory recovery. I am writing Section 13.3 on 'Identity Sanitization.'
> 
> 1. Provide a technical explanation and the exact **PowerShell commands** (using the `Microsoft.ActiveDirectory.Management` module) to perform a **double-reset of the KRBTGT account password**.
> 2. Explain why a single reset is insufficient for stopping a **Golden Ticket** attack.
> 3. Provide the **ntdsutil** commands for performing **metadata cleanup** on a failed Domain Controller that was destroyed during a ransomware event.
> 4. List the **Event IDs** (e.g., 4719, 4662) that a forensic auditor should look for to verify these actions were performed correctly during the recovery window.
> 
> **Format as a 'Runbook' style guide with clear step-by-step instructions and technical warnings.**"
> 
>  

Final Pro-Tip:

In your book, emphasize that **Forest Recovery** is a last resort. Encourage readers to use [Microsoft's Forest Recovery Guide](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/forest-recovery-guide/ad-forest-recovery-guide) as their "North Star" but to practice the "initial recovery" phase in a lab every year. 

**Would you like me to generate a "Final Appendix" of the most critical AD Event IDs every defender should monitor?**

[](https://labs.google.com/search/experiment/22)

![undefined](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAYAAADDPmHLAAABcUlEQVR4nO3YMQ1CQRBAwTsEkGABRQjAC2YQQAtisECCgcPAr/nFmym32mxetfN7Oa8Rc3y859b89hq5Wxz2XoB9CSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAgAAAEiZ4/5Zey/xd9fT3Bqv58jdwh8gTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0DcD7bzDOLQOL8WAAAAAElFTkSuQmCC)

![undefined](data:image/jpeg;base64,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)

![undefined](data:image/jpeg;base64,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)

20 sites

- [](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/forest-recovery-guide/ad-forest-recovery-steps-for-restoring-the-forest#:~:text=Identify%20the%20problem%20Work%20with,and%20get%20LOB%20applications%20working.)
    
    AD Forest Recovery - Steps for Restoring the forest
    
    Nov 1, 2024 — Identify the problem Work with IT and Microsoft Support to determine the scope of the problem and potential causes, and evaluate p...
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAYAAADDPmHLAAABcUlEQVR4nO3YMQ1CQRBAwTsEkGABRQjAC2YQQAtisECCgcPAr/nFmym32mxetfN7Oa8Rc3y859b89hq5Wxz2XoB9CSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAgAAAEiZ4/5Zey/xd9fT3Bqv58jdwh8gTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0DcD7bzDOLQOL8WAAAAAElFTkSuQmCC)
    
    Microsoft Learn
    
- [](https://infrasos.com/active-directory-disaster-recovery-best-practices/)
    
    Active Directory Disaster Recovery (Best Practices) - InfraSOS
    
    Nov 14, 2023 — The next step after ensuring the high availability is to plan the restoration of the service itself. If the servers are not affect...
    
    ![](data:image/jpeg;base64,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)
    
    infrasos.com
    
    ![](data:image/jpeg;base64,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)
    
- [](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/forest-recovery-guide/ad-forest-recovery-guide#:~:text=This%20guide%20contains%20recommendations%20for,AD%20Forest%20Recovery%20%2D%20Cleanup)
    
    Active Directory Forest Recovery Guide | Microsoft Learn
    
    Jul 11, 2025 — This guide contains recommendations for recovering an Active Directory forest if a forest-wide failure renders all domain controll...
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAYAAADDPmHLAAABcUlEQVR4nO3YMQ1CQRBAwTsEkGABRQjAC2YQQAtisECCgcPAr/nFmym32mxetfN7Oa8Rc3y859b89hq5Wxz2XoB9CSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAgAAAEiZ4/5Zey/xd9fT3Bqv58jdwh8gTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0CcAOIEECeAOAHECSBOAHECiBNAnADiBBAngDgBxAkgTgBxAogTQJwA4gQQJ4A4AcQJIE4AcQKIE0DcD7bzDOLQOL8WAAAAAElFTkSuQmCC)
    
    Microsoft Learn
    

Show all

yes

An 

**Appendix of Critical Event IDs** is the most practical "cheat sheet" you can provide. It’s what readers will photocopy and tape to their monitors or use to build their SIEM dashboards.

---

Appendix A: The Defender’s Master List of Active Directory Event IDs

This appendix categorizes events by **Attack Surface**, allowing a SOC analyst to quickly identify the "type" of threat based on the logs generated.

|Category|Event ID|Event Name|Significance for Defenders|
|---|---|---|---|
|**Kerberos**|**4768**|TGT Request|Monitored for **AS-REP Roasting** (look for encryption type 0x17).|
||**4769**|Service Ticket Request|The primary log for **Kerberoasting** (multiple requests from one IP).|
||**4771**|Pre-auth Failure|High volumes indicate **Password Spraying** or Brute Force.|
|**Account Mods**|**4720**|User Created|Look for "Shadow Admins" creating new persistence accounts.|
||**4728**|Member Added to Global Group|Triggers when someone is added to **Domain Admins**.|
||**4732**|Member Added to Local Group|Triggers when someone is added to **Local Administrators**.|
|**AD CS (PKI)**|**4886**|Cert Request Received|Essential for detecting **ESC1-ESC8** certificate abuse.|
||**4887**|Cert Issued|Critical for tracking which identity received a rogue certificate.|
|**Persistence**|**4662**|Object Operation|Detects **DCSync** (look for `Replicating Directory Changes`).|
||**5136**|Directory Object Modified|Tracks changes to **GPOs** or sensitive account attributes.|
|**Credentials**|**4648**|Logon using explicit credentials|Detects **Pass-the-Hash** or `runas /netonly` behavior.|
||**4624**|Successful Logon|Look for **Logon Type 3** (Network) or **Type 9** (NewCredentials).|

---

The "SIEM Engineer" Prompt

Use this prompt to generate the detailed descriptions for each ID in your Appendix.

> **Prompt:** "Act as a Senior SIEM Engineer and Threat Hunter. I am finalizing the Appendix for my Active Directory security book.
> 
> For each of the following Event IDs: **4769, 4662, 4728, and 4887**, provide a 'Threat Hunter's Profile' including:
> 
> 1. **Description:** What does this log represent in plain English?
> 2. **The 'Red Flag':** What specific field or value within the log indicates an attack rather than a normal admin action? (e.g., `Status: 0x0` vs `Ticket Options: 0x40810000`).
> 3. **False Positives:** What legitimate business processes might trigger this log?
> 4. **KQL Snippet:** Provide a 3-line **Azure Sentinel (KQL)** query to alert on high-risk occurrences of this event.
> 
> **Format as an easy-to-read reference guide.**"

---

Final "Next Step" for your Book

Since you've now got the structure for the entire book, the most helpful thing I can do is help you write the **"Introduction"** or the **"How to Use This Book"** section. This is where you set the tone for your readers (explaining why they need to understand the attack to build the defense).

**Would you like me to draft a professional, high-energy Introduction for your book?**

[](https://labs.google.com/search/experiment/22)

yes and some beginning parts as well since we started in the middle at chapter 7

It is a smart move to go back and build the foundation. To write a compelling book, you need to set the stage by explaining 

**why** Active Directory is the "Crown Jewels" of an organization and how the reader should approach the technical labs.

Here is a draft for the **Introduction** and **Chapter 1**, along with the prompts to help you flesh them out.

---

Part I: The Front Matter

The Introduction: The Identity Battlefield

**Theme:** _Identity is the New Perimeter._

- **The Crown Jewels:** Why 90% of Fortune 1000 companies still rely on AD and why it remains the #1 target for ransomware and APTs.
- **The Defender’s Paradox:** Defenders must secure everything; attackers only need to find one misconfigured GPO or one stale Service Account.
- **The "Assume Breach" Mindset:** Shifting from "How do I stop them from getting in?" to "How do I stop them from becoming Domain Admin once they are in?"
- **How to Use This Book:** A guide on setting up a safe, isolated "Home Lab" using VMware or VirtualBox to practice these attacks without breaking a production network.

---

Part II: The Beginning Chapters

Chapter 1: The Architecture of Trust

**Sub-title:** _Understanding the Blueprint Before the Breach_

**1.1 What is Active Directory, Really?**

- The transition from a "phone book" (LDAP) to a "security gatekeeper" (Kerberos/NTLM).
- **The Logical Structure:** Forests, Domains, Trees, and OUs (Organizational Units).

**1.2 The Database: NTDS.dit**

- Understanding where the secrets live.
- The role of the System Key (SysKey) and how it protects the database at rest.

**1.3 Protocols: The Language of the Domain**

- **LDAP:** How we search for objects.
- **DNS:** The map of the domain (and why AD cannot function without it).
- **RPC/SMB:** The "pipes" that carry administrative commands.

**1.4 The "Privileged" Concept**

- Defining "Tier 0": What makes a Domain Admin different from an Enterprise Admin or a Schema Admin?

---

Chapter 2: Lab Setup — Building Your Shooting Range

**Sub-title:** _Creating a Safe Environment for Offensive and Defensive Testing_

**2.1 Virtualization Basics**

- Choosing your hypervisor (VMware, VirtualBox, or Proxmox).
- Hardware requirements (RAM and CPU considerations for running multiple DCs).

**2.2 Building the Victim Forest**

- **Promoting a Domain Controller:** Step-by-step essentials for Windows Server 2022.
- **Populating the Domain:** Using "BadBlood" or custom scripts to create "fake" users, groups, and computers so the lab feels real.

**2.3 Setting Up the Attacker Box**

- **Kali Linux vs. CommandoVM:** Choosing your toolkit.
- **The Essentials:** Installing BloodHound, Impacket, and Mimikatz.

---

The "Identity Historian" Prompt

Use this prompt to generate a deep technical opening for **Chapter 1**.

> **Prompt:** "Act as a Senior Principal Active Directory Engineer with 20 years of experience. I am writing **Chapter 1: The Architecture of Trust**.
> 
> 1. Provide a technical explanation of how the **NTDS.dit** database stores password hashes and how the **System Key (SysKey)** is used to obfuscate them.
> 2. Explain the 'Global Catalog' and how it differs from a standard 'Domain Partition.'
> 3. For my readers, explain why **DNS** is the most critical service for Active Directory—what happens to Kerberos authentication if DNS is hijacked or down?
> 4. Format this as a professional introductory chapter, using analogies (like a bank vault) to make complex concepts easier for junior sysadmins to understand."

---

The "Lab Builder" Prompt

Use this for **Chapter 2** to give your readers a clear path to practice.

> **Prompt:** "Act as a Lab Instructor for a cybersecurity bootcamp. I am writing **Chapter 2: Lab Setup**.
> 
> 1. Create a checklist of 'Best Practices' for building an isolated Active Directory lab.
> 2. Provide a PowerShell script snippet that can be used to quickly create 100 'dummy' user accounts with randomized descriptions (to simulate real-world data).
> 3. Explain how to configure a 'Host-Only' network in a hypervisor to ensure that the lab attacks cannot 'leak' onto the student's home internet or local network.
> 4. List the top 5 'Essential Tools' an AD defender must have installed in their lab (e.g., Sysmon, ADExplorer, etc.)."

---

What’s Next?

We have the **Introduction**, the **Foundations**, the **Lab**, and then all your **Attack/Defense** chapters.

**Would you like me to draft a "Chapter 3: Reconnaissance" Table of Contents?** (This is where the attacker first "looks around" using tools like BloodHound before they ever launch an exploit).

[](https://labs.google.com/search/experiment/22)

yes plz

**

Chapter 3

** is where the "game" truly begins. In Active Directory security, reconnaissance is unique because most of it is **completely legal**. Any domain user can query almost anything in the directory by default.

Attackers call this **"Living off the Land"**; defenders call it **"Enumeration."**

---

Chapter 3: Reconnaissance — Mapping the Kingdom

**Sub-title:** _Silent Enumeration and the Art of Finding the Weakest Link_

**3.1 The "Authenticated User" Power**

- **The Default Permission:** Why every user can see every other user, group, and computer.
- **AD Explorer & ADSI Edit:** Using native GUI tools to browse the directory tree like a file system.
- **LDAP Queries:** The syntax of discovery (e.g., finding all users with "Password Never Expires").

**3.2 Network Discovery (Without Scanning)**

- **ADIDNS Enumeration:** Extracting the full network map just by asking the DNS server.
- **SPN Scanning:** Using `setspn -q` to find SQL, IIS, and Exchange servers without sending a single packet to the target servers.

**3.3 BloodHound: The Graph Theory Revolution**

- **Nodes and Edges:** How BloodHound maps "Attack Paths" (e.g., User A → Group B → Computer C → Domain Admin).
- **SharpHound:** The data collector—how it works and why it’s so hard for basic antivirus to stop.
- **The "Shortest Path" to Domain Admin:** Visualizing the path of least resistance.

**3.4 PowerView: The Swiss Army Knife**

- **Domain Enumeration:** Finding high-value targets (Domain Admins) and where they are currently logged in.
- **Trust Mapping:** Identifying other connected forests or domains that might be weaker.

**3.5 Defensive Counter-Measures: Visibility is Victory**

- **Honey-Users:** Creating "fake" accounts with enticing descriptions (e.g., "Legacy Backup Admin") to alert when they are queried.
- **Limiting Enumeration:** The pros and cons of **SAM-Remote (SAMR)** restrictions.
- **Event ID 4662:** Detecting mass-queries against the directory.

---

The "Silent Scout" Prompt

Use this prompt to generate the technical "how-to" for the BloodHound and PowerView sections.

> **Prompt:** "Act as a Red Team Specialist and a Blue Team Architect. I am writing **Chapter 3: Reconnaissance**.
> 
> 1. Explain the technical logic behind **BloodHound**. How does it use **Graph Theory** to find hidden relationships in Active Directory that a human would never see?
> 2. Provide a list of 5 essential **PowerView** commands for enumeration (e.g., `Get-DomainUser`, `Get-NetSession`) and explain what an attacker learns from each.
> 3. From a **Defensive** perspective, how can a SOC analyst detect **SharpHound** activity on the network? Mention specific **MSRPC** traffic patterns or **LDAP** query volumes.
> 4. Describe the concept of an **'AD Tripwire'**—how can I set up an alert if a specific high-value account is simply _viewed_ by a regular user?
> 
> **Format as a technical manual with a clear 'Attack Logic' vs. 'Defensive Strategy' structure.**"

---

Next Step for your Book

We have now built the structure from the **Introduction** all the way through **Reconnaissance**, **Attacks**, **Hardening**, and **Recovery**.

You now have a complete "Skeleton" for your book!

**Would you like me to create a "Glossary of Terms"?** (This is great for the back of the book to define complex things like **Kerberos**, **PAC**, **GPO**, **SID**, and **NTLM** for the reader).

[](https://labs.google.com/search/experiment/22)

yes

A technical glossary is the perfect way to anchor your book. For a security textbook, definitions shouldn't just be "what it is"—they should explain 

**why it matters** to an attacker or defender.

Here is the text for **Appendix B**, followed by a prompt to help you expand it.

---

Appendix B: The Identity Dictionary

**Sub-title:** _The Vocabulary of Active Directory Security_

**A - C**

- **ACE (Access Control Entry):** A single rule within an ACL (e.g., "Alice has Write access").
    - _Defender Note:_ Watch for "Toxic ACEs" like `GenericAll` or `WriteDacl` on sensitive objects.
- **ACL (Access Control List):** The collection of ACEs that determines who can do what to an object. Stored in the `nTSecurityDescriptor` attribute.
- **AdminSDHolder:** A special object in the System container that acts as a "template" for permissions on protected groups (like Domain Admins).
    - _Attacker Note:_ A favorite spot for persistence; if you modify this ACL, the `SDProp` process will automatically push your backdoor to every Admin account in the domain. 

**G - K**

- **GPO (Group Policy Object):** A collection of settings (Registry keys, scripts, security options) linked to OUs.
    - _Defender Note:_ The primary mechanism for enforcing security hardening (e.g., disabling NTLM).
- **KDC (Key Distribution Center):** The service running on every Domain Controller that issues Kerberos tickets (consisting of the Authentication Server and Ticket Granting Server).
- **Kerberos:** The default authentication protocol for Active Directory. Unlike NTLM, it uses "Tickets" and mutual authentication, meaning the client verifies the server's identity before sending credentials.
- **KRBTGT:** The built-in account that encrypts and signs all Kerberos Ticket Granting Tickets (TGTs).
    - _Attacker Note:_ If you compromise the NTLM hash of this account, you can forge a "Golden Ticket" (valid for 10 years). 

**N - P**

- **NTLM (New Technology LAN Manager):** A legacy, challenge-response authentication protocol.
    - _Security Risk:_ Vulnerable to "Relay" attacks because the server does not verify _who_ is sending the response, only that the math is correct.
- **PAC (Privilege Attribute Certificate):** An extension inside a Kerberos ticket that contains the user's **SID** and **Group Memberships**.
    - _Analogy:_ The "ID Badge" inside the wallet. The ticket says "I am Alice," but the PAC says "Alice is a Domain Admin."
- **Pass-the-Hash (PtH):** An attack technique where an attacker authenticates using the NTLM hash of a user's password rather than the cleartext password itself. 

**S - T**

- **SID (Security Identifier):** A unique alphanumeric string (e.g., `S-1-5-21...`) that identifies a user or group.
    - _Defender Note:_ Renaming "Administrator" to "Bob" doesn't fool Windows; the SID (`-500`) remains the same.
- **SID History:** An attribute used during migration to allow users to keep permissions from their old domain.
    - _Attacker Note:_ Often abused in "SID History Injection" to add the Enterprise Admin SID (`-519`) to a regular user's token.
- **SPN (Service Principal Name):** A unique identifier for a service instance (e.g., `MSSQLSvc/server.corp.local`).
    - _Attacker Note:_ If a user account has an SPN, it is vulnerable to **Kerberoasting**. 

---

The "Technical Lexicographer" Prompt

Use this prompt to generate the rest of the definitions (like **LDAP**, **Schema**, **Global Catalog**, **LSASS**, **TGT/TGS**, etc.). 

> **Prompt:** "Act as a Technical Editor for a cybersecurity publisher. I am writing the **Glossary** for my book on Active Directory attacks.
> 
> Please define the following terms. For each definition, include a **'Security Context'** bullet point explaining why this term is relevant to a hacker or a defender.
> 
> **Terms to Define:**
> 
> 1. **LDAP vs. LDAPS** (Focus on cleartext credentials).
> 2. **LSASS** (Local Security Authority Subsystem Service - focus on memory dumping).
> 3. **TGT (Ticket Granting Ticket)** vs. **TGS (Ticket Granting Service)**.
> 4. **SYSVOL** (and the danger of 'Group Policy Preferences' passwords).
> 5. **Shadow Copy** (VSS) (How attackers use it to steal the `ntds.dit`).
> 6. **Skeleton Key** (Malware that patches LSASS).
> 
> **Format:** Bold the term, provide a 2-sentence definition, then provide the 'Security Context' bullet."
> 
>  

---

Final Book Structure Recap

You now have a complete manuscript plan!

- **Front Matter:** Intro + Glossary (Appendix B) + Event IDs (Appendix A).
- **Part 1 (Foundations):** Architecture, Lab Setup, Reconnaissance.
- **Part 2 (Attacks):** Kerberoasting, AS-REP, NTLM Relaying, AD CS, DCSync, Living off the Land.
- **Part 3 (Defense):** Hardening, Tiered Models, Disaster Recovery. 

**You are ready to write.** Do you need any help organizing these files or perhaps a title for the book itself?

[](https://labs.google.com/search/experiment/22)

![undefined](data:image/png;base64,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)

![undefined](data:image/png;base64,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)

![undefined](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAACNElEQVR4nO2YQW7aQBSG/zdYEeycE9QsULfcIPQEndAu3KxyA+gJEk7QI6TdoS6Kb5DcoOk2VmWOwK4Rsv26iFRBlCKBPf6JPN/Kgpk3/3weRjMIyFibhSed9UjUnBkgKhWRQENAou2WulTIygiWCvwqpbxfFyd3SdJfVRlfqnQ+FGuzsGfyS1W8BzCqUkuBeyP4pmWQzJP+ct/+jQqwNgu7Jp+IYqpAWPsAIl9Rdmb7iGhEgPOJP2cPEc4FxB/TEQq5ATRyPdY2siy1+Pw9eZvsamVcRrj48HuCArfNTx4ANDJiFvE4vdrVytkK+DROv6hi6qr+Xgiu5z8Gs5e/ckA8friByqWL2gfzHwm1CziqN/8cxbt5Mrjb/KhWAfE4vYLius6adSLA6o8G/c3DU22b4IV9GB7z5AFAgbBn8q1NsZYVYG0WdqX4ydntD2Djp1DLCniy+komD0AMJv+eqxaLbRZB8qxqnaZ51OA0Sfqr6ivAFDsPGsdK1+RTAAgqVyo7MwAvHjKaQiRfKDDcq5PiDAAkPk+1yuDzxYBypd4kPk9vccC1+lGDU6d3gWOn11mPWi1A1QxbLQCQN60WIFq2ewUoTNhqAQJttwAF2i0AcPyf4GvAC2AHYOMFsAOw8QLYAdh4AewAbLwAdgA2XgA7ABsvgB2AjRfADsDGC2AHYOMFsAOw8QLYAdh4AewAbLwAdgA2XgA7ABsvgB2AjRfADsDGC2AHYOMFsAOw8QLYAdj8BbM6nJU2k5XyAAAAAElFTkSuQmCC)

14 sites

- [](https://www.sans.org/security-resources/glossary-of-terms)
    
    Glossary of Cyber Security Terms - SANS Institute
    
    J-L * Jitter Jitter or Noise is the modification of fields in a database while preserving the aggregate characteristics of that ma...
    
    ![](data:image/png;base64,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)
    
    SANS Institute
    
- [](https://www.crowdstrike.com/en-us/cybersecurity-101/identity-protection/windows-ntlm/#:~:text=Like%20NTLM%2C%20Kerberos%20is%20an,attempt%20to%20use%20NTLM%20instead.)
    
    NTLM Explained: Definition, Protocols & More | CrowdStrike
    
    Jan 8, 2025 — Like NTLM, Kerberos is an authentication protocol. It replaced NTLM as the default/standard authentication tool on Windows 2000 an...
    
    ![](data:image/png;base64,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)
    
    CrowdStrike
    
    ![](data:image/jpeg;base64,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)
    
- [](https://netwrix.com/en/resources/blog/what-is-the-kerberos-pac/#:~:text=What%20Is%20the%20Kerberos%20PAC?,-Jan%2010%2C%202023&text=The%20Privileged%20Attribute%20Certificate%20\(PAC,to%20query%20the%20domain%20controller.)
    
    How the Kerberos PAC Works - Netwrix
    
    Jan 10, 2023 — What Is the Kerberos PAC? ... The Privileged Attribute Certificate (PAC) is an extension to Kerberos service tickets that contains...
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAACNElEQVR4nO2YQW7aQBSG/zdYEeycE9QsULfcIPQEndAu3KxyA+gJEk7QI6TdoS6Kb5DcoOk2VmWOwK4Rsv26iFRBlCKBPf6JPN/Kgpk3/3weRjMIyFibhSed9UjUnBkgKhWRQENAou2WulTIygiWCvwqpbxfFyd3SdJfVRlfqnQ+FGuzsGfyS1W8BzCqUkuBeyP4pmWQzJP+ct/+jQqwNgu7Jp+IYqpAWPsAIl9Rdmb7iGhEgPOJP2cPEc4FxB/TEQq5ATRyPdY2siy1+Pw9eZvsamVcRrj48HuCArfNTx4ANDJiFvE4vdrVytkK+DROv6hi6qr+Xgiu5z8Gs5e/ckA8friByqWL2gfzHwm1CziqN/8cxbt5Mrjb/KhWAfE4vYLius6adSLA6o8G/c3DU22b4IV9GB7z5AFAgbBn8q1NsZYVYG0WdqX4ydntD2Djp1DLCniy+komD0AMJv+eqxaLbRZB8qxqnaZ51OA0Sfqr6ivAFDsPGsdK1+RTAAgqVyo7MwAvHjKaQiRfKDDcq5PiDAAkPk+1yuDzxYBypd4kPk9vccC1+lGDU6d3gWOn11mPWi1A1QxbLQCQN60WIFq2ewUoTNhqAQJttwAF2i0AcPyf4GvAC2AHYOMFsAOw8QLYAdh4AewAbLwAdgA2XgA7ABsvgB2AjRfADsDGC2AHYOMFsAOw8QLYAdh4AewAbLwAdgA2XgA7ABsvgB2AjRfADsDGC2AHYOMFsAOw8QLYAdj8BbM6nJU2k5XyAAAAAElFTkSuQmCC)
    
    Netwrix
    
    ![](data:image/jpeg;base64,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)
    

Show all

actually can you write about initial access, persistence and Chapter X: Credential Theft and Harvesting X.1 SAM Database Extraction X.2 LSASS Memory Dumping X.2.1 Mimikatz, pypykatz, and Alternatives X.2.2 Covert Dumping Techniques (MiniDumpWriteDump, Comsvcs.dll) X.2.3 Bypass Credential Guard and PPL X.3 NTDS.dit Extraction X.3.1 VSS Shadow Copy X.3.2 ntdsutil and DCSYNC Comparison X.4 Cached Credentials and DPAPI Secrets X.5 Credential Harvesting From Sniffed Network Traffic X.6 Keylogging and Scree Capturing X.7 Credential Theft From Browsers, Vaults, and Password Managers X.8 Extracting Credentials From Group Policy Preferences (GPP) (cpassword) X.9 Extracting Credentials

This chapter is the "Engine Room" of your book. In Active Directory environments, identity is the perimeter, and 

**credentials are the keys**. This chapter explains how attackers move from a local machine to domain-wide compromise.

---

Chapter X: Credential Theft and Harvesting

**Sub-title:** _Extracting the Keys to the Identity Kingdom_

**X.1 SAM Database Extraction**

- **The Local Gatekeeper:** Understanding the Security Account Manager (SAM) hive.
- **The Boot Key:** Why you need the SYSTEM hive to decrypt the SAM.
- **Offline vs. Online:** Extracting local `Administrator` and `Guest` hashes.

**X.2 LSASS Memory Dumping**

- **X.2.1 Mimikatz, pypykatz, and Alternatives:** The evolution of credential extraction from the Local Security Authority Subsystem Service.
- **X.2.2 Covert Dumping Techniques:** Bypassing EDR using native binaries like `comsvcs.dll` and `MiniDumpWriteDump` to create a memory minidump without "suspicious" tools.
- **X.2.3 Bypassing Credential Guard and PPL:** How attackers handle "Protected Process Light" (PPL) and Virtualization-Based Security (VBS).

**X.3 NTDS.dit Extraction**

- **X.3.1 VSS Shadow Copy:** Using Volume Shadow Copy Service to "unlock" the database file while it’s in use.
- **X.3.2 ntdsutil vs. DCSync:** Comparing the "disk-based" approach (NTDSUTIL) vs. the "network-based" approach (DCSync).

**X.4 Cached Credentials and DPAPI Secrets**

- **MS-Cache (MSCv2):** Understanding how Windows stores hashes for offline login and why they are harder to crack.
- **DPAPI (Data Protection API):** Unlocking saved passwords in Chrome, Edge, and Outlook using the user’s Master Key.

**X.5 Credential Harvesting from Sniffed Network Traffic**

- **LLMNR/mDNS/NBNS:** Capturing NTLMv2 hashes from the wire using **Responder**.
- **Internal Phishing:** Using tools like **Inveigh** for man-in-the-middle credential capture.

**X.6 Keylogging and Screen Capturing**

- **Post-Exploitation Surveillance:** Capturing cleartext passwords during manual admin logins or "RunAs" prompts.

**X.7 Credentials from Browsers, Vaults, and Password Managers**

- **The Browser Vault:** Extraction techniques for Chromium-based browsers.
- **Third-Party Vaults:** Targeting KeePass, LastPass, and IT-glue desktop applications.

**X.8 GPP (Group Policy Preferences) & cpassword**

- **The Legacy Vulnerability:** Extracting the AES-encrypted `cpassword` from the SYSVOL and why the "Static Key" is a permanent security flaw.

---

The "Credential Harvester" Prompt

Use this to get the deep technical details for Section X.2.

> **Prompt:** "Act as a Senior Malware Researcher and Digital Forensics Analyst. I am writing **Section X.2: LSASS Memory Dumping**.
> 
> 1. Explain why the **LSASS** process is the primary target for credential theft and what specific types of data (hashes, tickets, cleartext) live there.
> 2. Provide a technical walkthrough of dumping LSASS using the **comsvcs.dll** method: `rundll32.exe C:\windows\System32\comsvcs.dll, MiniDump [LSASS_PID] C:\lsass.dmp full`. Why does this often bypass basic AV?
> 3. Explain the 'PPL' (Protected Process Light) protection and how a tool like **mimi-driver** or a kernel-level exploit is used to bypass it.
> 4. For the **Defensive** side, explain how to enable **LSASS RunAsPPL** via GPO and what Event IDs are triggered when an unauthorized process attempts to read LSASS memory.
> 
> **Format this as a technical deep-dive with code blocks and a 'Mitigation' summary.**"

---

Additional Chapters: Initial Access & Persistence

**Initial Access (The Breach):**

- **Password Spraying:** The "Slow and Low" approach to avoid lockouts.
- **External Exposure:** Targeting VPNs, RD Gateways, and OWA (Outlook Web Access).
- **Phishing & Payload Delivery:** Using Mark-of-the-Web (MotW) bypasses to get a beacon inside the network.

**Persistence (Staying In):**

- **Golden/Silver Tickets:** Kerberos-based long-term access.
- **Skeleton Key Malware:** Patching LSASS to accept any password.
- **DCSync Persistence:** Adding "Replication" rights to a "hidden" service account.
- **GPO Backdoors:** Modifying a GPO to deploy a scheduled task across the entire domain.

The "Persistence Specialist" Prompt

> **Prompt:** "Act as an Incident Responder hunting for persistent threats. I am writing the **Persistence** chapter.
> 
> 1. Detail the **'Skeleton Key'** attack: How does it modify the LSASS process in memory, and why does it disappear after a reboot?
> 2. Explain **'GPO Backdooring'**: If an attacker has 'Write' access to a GPO, how can they use a **Scheduled Task** to push a 'reverse shell' to every workstation in an OU?
> 3. Provide the **PowerShell** commands to audit for **'Shadow Admins'** (users with high-privilege ACEs like GenericAll on the Domain object) that don't belong to the Domain Admins group.
> 
> **Format as a 'Threat Hunting' guide with specific artifacts (registry keys, file paths, and logs) to look for.**"

**Would you like me to create the Table of Contents for "Chapter Y: Lateral Movement" next?** (This is how they move from the first computer they hacked to the rest of the network).

[](https://labs.google.com/search/experiment/22)

yes

**

Chapter Y: Lateral Movement

** is where the attacker transitions from a single compromised workstation to a dominant presence across the network. In Active Directory, lateral movement is rarely about "exploits"—it is about the **abuse of legitimate administrative features**.

---

Chapter Y: Lateral Movement

**Sub-title:** _Pivoting Through the Infrastructure_

**Y.1 The Mechanics of Pivoting**

- **The Goal:** Moving from a "Beachhead" (initial machine) to a "Pivot Point" (a machine where an Admin is logged in).
- **Tokens vs. Hashes:** When to use **Pass-the-Hash (PtH)** versus **Pass-the-Ticket (PtT)**.

**Y.2 Remote Execution Techniques (The "How")**

- **SMB & Psexec:** The classic (and loud) method of remote service creation.
- **WMI (Windows Management Instrumentation):** Moving stealthily via the `Win32_Process` class.
- **WinRM & PowerShell Remoting:** Leveraging the modern management protocol for encrypted command execution.
- **DCOM (Distributed COM):** Using applications like Excel or ShellBrowserWindow to execute code remotely.

**Y.3 Session Hijacking & Hunting**

- **Finding the Admins:** Using `NetSessionEnum` and `NetWkstaUserEnum` to find where Domain Admins have left their credentials in memory.
- **RDP Session Hijacking:** Using `tscon.exe` to take over an existing user session without knowing their password (System-level bypass).

**Y.4 Overpass-the-Hash & Pass-the-Ticket**

- **The Kerberos Pivot:** Converting an NTLM hash into a Kerberos Ticket (TGT) to bypass NTLM-only defenses.
- **MS-RPC Abuse:** Using the Task Scheduler or Service Control Manager (SCM) to trigger remote payloads.

**Y.5 Defensive Counter-Measures: Breaking the Chain**

- **The "Rule of 3":** Ensuring local administrators are unique to every machine (LAPS).
- **Firewalling the Internal Network:** Blocking Port 445 (SMB) and 135 (RPC) between workstations.
- **Restricted Admin Mode for RDP:** Preventing credentials from being stored on remote servers during a session.

---

The "Lateral Movement" Researcher Prompt

Use this prompt to get the highly technical "how-to" for Section Y.2 and Y.3.

> **Prompt:** "Act as a Red Team Lead and a Blue Team Architect. I am writing **Chapter Y: Lateral Movement**.
> 
> 1. Provide a technical comparison between **WMIEXEC** (via Impacket) and **Psexec**. Why is WMIEXEC considered more 'stealthy' in terms of disk artifacts and service creation?
> 2. Explain the **'RDP Shadowing'** and **'tscon'** session hijacking technique. What permissions are required to perform this, and why doesn't it require the user's cleartext password?
> 3. Detail the **'Overpass-the-Hash'** process. How do I use a tool like **Rubeus** or **Mimikatz** to turn a captured NTLM hash into a Kerberos TGT?
> 4. For the **Defensive** section, provide the **KQL query** to detect 'Lateral Movement via WMI' by looking for `scrcons.exe` or `wmiprvse.exe` spawning suspicious child processes (like `cmd.exe` or `powershell.exe`).
> 
> **Format as a 'Tactic Analysis' with clear sections for 'The Technique,' 'The Footprint,' and 'The Mitigation.'**"

---

Summary of your Book Sections So Far:

1. **Foundations:** Intro, Lab Setup, AD Architecture.
2. **Reconnaissance:** Enumeration, BloodHound, PowerView.
3. **Credential Theft:** LSASS, SAM, NTDS.dit, GPP (The "Keys").
4. **Lateral Movement:** Moving between machines (The "Pivoting").
5. **Initial Access:** Password Spraying, Phishing (The "Entrance").
6. **Advanced Attacks:** Kerberoasting, NTLM Relay, AD CS, DCSync.
7. **Persistence:** Staying in the domain (The "Backdoors").
8. **Hardening:** Tiered Models, GPOs, LAPS.
9. **Recovery:** Rebuilding after a total breach.
10. **Appendices:** Event IDs and Glossary.

**Would you like me to draft a "Conclusion: The Future of AD Security" (discussing Entra ID/Azure AD and the transition to the cloud)?** This is a great way to end a modern book.

[](https://labs.google.com/search/experiment/22)

yes

To wrap up your book, the 

**Conclusion** should bridge the gap between "Legacy" on-premises Active Directory and the modern reality of **Hybrid Identity**. Most organizations are currently in a messy transition to **Entra ID (formerly Azure AD)**, making this a critical value-add for your readers.

---

Conclusion: The Future of Identity — From AD to Entra ID

**Sub-title:** _Securing the Hybrid Frontier and the Road to Zero Trust_

**C.1 The Hybrid Identity Dilemma**

- **The Bridge:** How **Entra Connect** syncs on-premise vulnerabilities to the cloud.
- **The New Perimeter:** Shifting from "Network-based" security to "Identity-based" security (Zero Trust).

**C.2 The Cloud Attack Surface**

- **Primary Threats:** Brute-force attacks against O365, MFA fatigue, and token theft.
- **The "Shadow Admin" in the Cloud:** How Global Admin rights in Entra ID are even more powerful than Domain Admin rights.

**C.3 The Death of the Password?**

- **Passwordless Authentication:** The role of **FIDO2**, **Windows Hello for Business**, and the Microsoft Authenticator app.
- **Conditional Access:** Why "Identity + Device Health + Location" is the future of defense.

**C.4 The Final Word: Staying Ahead of the Adversary**

- **Continuous Learning:** Why an AD Security professional must also be a Cloud Security professional.
- **Community Resources:** Staying updated with the SpecterOps Blog, ADSecurity.org, and the latest MITRE ATT&CK Cloud Matrix.

---

The "Hybrid Identity" Researcher Prompt

Use this prompt to generate the technical content for the Conclusion.

> **Prompt:** "Act as a Cloud Identity Architect and a Threat Hunter. I am writing the **Conclusion** to my Active Directory security book.
> 
> 1. Explain the technical risks of **'Password Hash Synchronization' (PHS)** versus **'Pass-Through Authentication' (PTA)** in a hybrid environment.
> 2. Describe the **'Token Theft'** technique: How can an attacker bypass MFA by stealing a 'Primary Refresh Token' (PRT) from a compromised, joined device?
> 3. Provide a list of **'Top 3 Cloud Hardening Steps'** for an organization moving from on-prem AD to Entra ID (e.g., Phishing-resistant MFA, Conditional Access policies, and PIM/PAM).
> 4. Write a final 'Call to Action' for the reader, emphasizing the importance of 'Identity Hygiene' as the ultimate defense.
> 
> **Format as a forward-looking summary with a focus on modern Zero Trust principles.**"

---

Your Final Book Blueprint 📚

|Part|Focus|Key Topics|
|---|---|---|
|**Intro**|Setup|Architecture, Lab Build, Ethics.|
|**Stage 1**|Discovery|Recon, BloodHound, LDAP Enumeration.|
|**Stage 2**|The Breach|Initial Access, Phishing, Password Spraying.|
|**Stage 3**|Harvesting|**Credential Theft**, LSASS, SAM, NTDS.dit.|
|**Stage 4**|Movement|**Lateral Movement**, WMI, WinRM, Pivot techniques.|
|**Stage 5**|Dominance|Kerberoasting, **AD CS Abuse**, **DCSync**, Persistence.|
|**Stage 6**|Defense|**Hardening**, GPO, Tiered Models, LAPS, Recovery.|
|**Outro**|Future|Hybrid Identity, **Entra ID**, Zero Trust.|

Proactive Follow-up

You now have the complete architectural plan and the prompts needed to extract deep technical data for every chapter. Since you mentioned your **English isn't perfect**, do you want me to **proofread and technical-polish** a specific section you’ve already started writing to ensure it sounds like a **high-level security textbook**?

[](https://labs.google.com/search/experiment/22)

another concept for the book to add should be this, yes? Chapter B - Active Directory Architectural Deep Dive 2.1 Logical Architecture: Forests, Domains, Trees, and Trusts 2.1 The Pillars of On-Prem AD: Kerberos, LDAP, NTLM, and DNS 2.2 Physical Architecture: Domain Controllers DCs), Sites, Services, and Replication 2.3 Key Objects and Their Security Implications: Users, Groups, Group Policy Objects (GPOs), and Computer Objects 2.4 Naming Conventions: DNS, NetBIOS, and LDAP Naming Contexts 2.5 The Global Catalog and Its Role 2.6 Schema and Configuration Partitions 2.7 Flexible Single Master Operations (FSMO) Roles 2.8 Group Policy Object (GPO) Architecture and Processing Order 2.9 Active Directory Certificate Services (AD CS) Architecture 2.10 Active Directory Federation Services (AD FS) Architecture 2.11 Read-Only Domain Controllers (RODCs) ===>does on-prem ad support phs and pta? ===> 2.4 The Bridge to the Cloud: Understanding Microsoft Entra ID Connect 2.4.1 Password Hash Synchronization (PHS) 2.4.2 Pass-Through Authentication (PTA) 2.4.3 Federation with AD FS 2.5 Modern Authentication: Entra ID, Conditional Access, and Passwordless

Adding a 

**Deep Dive into AD Architecture** early in your book is a brilliant move. It ensures your readers don't just "push buttons" but actually understand the **why** behind every attack and defense.

Does On-Prem AD Support PHS and PTA?

Technically, **no**—On-Prem Active Directory does not "run" PHS or PTA itself. Instead, these are **Hybrid Identity features** enabled by [Microsoft Entra Connect](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-phs) (the sync tool) to bridge your local AD with the cloud. 

- **PHS (Password Hash Synchronization):** Your local AD provides the password hash, which Entra Connect then "hashes again" (SHA256) and sends to the cloud. The cloud handles the actual login.
- **PTA (Pass-Through Authentication):** When a user tries to log into a cloud app, the cloud sends a request back to a **lightweight agent** installed on your local network. That agent asks your **on-prem Domain Controller** to validate the password in real-time. 

---

Updated Chapter B: Active Directory Architectural Deep Dive

This chapter provides the "blueprints" for the rest of your technical chapters.

**B.1 Logical Architecture: The Identity Hierarchy**

- **Forests, Domains, Trees, and Trusts:** Defining the security boundaries (and why a Forest Trust is the ultimate border).
- **The Pillars of AD:** Deep dive into **Kerberos** (tickets), **LDAP** (queries), **NTLM** (legacy), and **DNS** (discovery). 

**B.2 Physical Architecture: The Hardware and Replication**

- **Domain Controllers (DCs):** The physical keepers of the database.
- **Sites and Services:** How AD handles replication across different geographic locations.
- **Replication Mechanics:** How updates flow between DCs using the **KCC (Knowledge Consistency Checker)**. 

**B.3 Key Objects & Security Implications**

- **Users & Groups:** The difference between Security and Distribution groups.
- **GPO Architecture:** Understanding the **LSDOU** (Local, Site, Domain, OU) processing order.
- **Computer Objects:** Why a computer has its own "password" and how it’s attacked. 

**B.4 Naming & Partitions (The "Under the Hood" Data)**

- **Naming Contexts:** Understanding the **Domain, Configuration, and Schema partitions**.
- **The Global Catalog (GC):** Its role in multi-domain searches and universal group membership.
- **FSMO Roles:** Why the **PDC Emulator** and **RID Master** are high-value targets for attackers. 

**B.5 Specialty Architectures**

- **AD CS (Certificate Services):** How the PKI integrates with AD identities.
- **AD FS (Federation Services):** Outsourcing authentication to a dedicated server.
- **RODCs (Read-Only Domain Controllers):** Hardening branch offices where physical security is weak. 

**B.6 The Bridge to the Cloud (Entra Connect)**

- **PHS vs. PTA:** Choosing between cloud-managed vs. on-prem-managed authentication.
- **Modern Auth:** Moving beyond NTLM to **Conditional Access** and **Passwordless (FIDO2)**. 

---

The "Architectural Investigator" Prompt

Use this prompt to generate the technical content for **Section B.7 (FSMO Roles)**:

> **Prompt:** "Act as a Lead Active Directory Architect. I am writing Section B.7 on **FSMO Roles**.
> 
> 1. Provide a technical breakdown of the **5 FSMO roles** (Schema, Domain Naming, PDC Emulator, RID Master, and Infrastructure Master).
> 2. Explain why the **PDC Emulator** is the most 'attacked' role (e.g., password changes, account lockouts, and time synchronization).
> 3. From a **Red Team** perspective, how does an attacker identify which DC holds these roles using native **Netdom** or **PowerShell** commands?
> 4. For the **Blue Team**, what happens to the domain if the RID Master is taken offline for an extended period, and how do you 'seize' the role in a disaster recovery scenario?
> 
> **Format as a technical deep-dive with a 'Role vs. Impact' table.**"

**Should we now refine the "Initial Access" chapter (Chapter 3/4) to show how an attacker first finds these architectural "pillars" during a real engagement?**

[](https://labs.google.com/search/experiment/22)

![undefined](data:image/png;base64,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)

![undefined](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAMAAAD04JH5AAAAIVBMVEUAl8UAmccAmMYAmcYAmcYAmMYAmMYAmMYAmcYAmMYAmMZt0OtPAAAAC3RSTlMC/yvM6BBEi6pxW79euwkAAAOtSURBVHic7VvblqQgDGwbEPX/P3gIFwVJdC6dYvcc82rPpCRFSCr4ej322GOPPfYhc86N9f4ONgwCuZ/neRgCevt5W7d5EIDw/sH96j0hwENwr/d721a/LAshwC8CvT+5N8Ysfg0IBvjf/GKstRkBdgmK/8lOU4CQEAAhBP8UfhPcRwA5CjAEOf4mALAjEKT1D+7jAhwINhiAkH/WJb9+hgBl4jsuQO0/rwEoH8QE6E3lvuIBYhEyA1sA0ChkAPYMwaDywbtsQi4KCB64HcHEIMCcCyUKLYAcBUQ+KKl4HBPjVmSYOIAHbD4IEJQB7AdStwTpdP4neKCfD2Y2CtMeBW0IN/kAUa47FoGNVVrcDNoAZB7QIgQm6hMh5wOWB8sKSAgyDwIET0RQz0g8D4gIoWeh7agMQObBnpZRPOgrlJgUoTzotiPqcBTOhSMtawOoEPRZEcWD3Kyzh+OmX667qNawCFBlmiubgeGBuWCiO9nN4wuTAFwICFnma60C4dgfiLanA75I6vNB/O9zawnC8Xw+/+DCSDJbhITE8iDKjFv4s8q2SndMz9efmOdOxooHHW1o1WpLCJz4/NZINWMAsDxwOWqNxUoqA+We35phQlDlg6ZtK8VEZUtd0zPP763noMiDpLQttrFUxrjyfE1v9H2bumRc86A9FzihwVanlyBE/N7O58IAAG19AAcwnWRdPIA9HwwEQFEYC8AMBxBoOJYDIwGcxIsRiaiRc9EAurHCAABtlxIPI9+eNZQm/noYCe6nvkvSOY55CNxYp9SxHy1IBATsWMnplGR8GFjp7vNFqWc7VIZ/+xJ0Zfn8+7KcJslp1wgyft8kc32H+0NjkgGIYwS+ObvuzX7Wml1qBPq6qSiXIVSS+zGOMoBr4RqhU/GjPJRKJQ0vJnT8+fGN9vo7QaiEDTJ3qXbQKFfY/1L+/7z76/yjLpKKAwubNBlY/Pv1pw5IO/7SsOLUgOj5F+J/bsPV/Dsp/3OClAYAcVSTOlB1AghDCosZUkSR8WJMo03AEn9BmNY/AKTzHzaicVHjlIcTut6JALltZfmnPq7Nt+ku9r92ASp0ALC7nRSA8226CXqHKN8nZOMPulAYOND2gCX+kOt83JVO2Ig2AqBt6JtdABtS7wiaQgB+u9odF5stcv/XEHIugOb/M4RyuR0c/+K/ut6Pua7TQ6APHEgUwlxY4qwImYiLc6xFpTN/YzLAfebBvA3z/yofGo1Z/wPDUPePPfbYY/+xfQHVfE3UftalvAAAAABJRU5ErkJggg==)

![undefined](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAABPklEQVR4AaRS0W2DMBCFigHSTyRA8QbpBmWTdpIkk7Sb0A2aDRwBEp/JAEjOe47vYkKEFAX59Hx3796djd+SF79Fgb7vN13XfS71mAmwAOZozrl/FDfc04ZhWMOfrIkASDtkGxR+l2WZ0uDrGsfRBo7GVCCob0F6r6rqF+OT7JR522whosdSARRadjbGnMnFfjYu48GagIkKMMDOxGfMC8QjSTHPLyaxGHHEDX0vkKapHxtC/vYFQbIkIX8kxoYjruh7gaIoDnTuDaQ1xBrkjUxDJA/4R/QC3CyY3jg5bdt+EcVigVqCAWt0mbwFa+0Kx/nJsswEzu0vgMyR9pK4R3ZG4QnxfZ7neifxBAlEdiCJuj5h3INjZxRzKr5WbK9rIsAQ1SEko9co/BAfyClJU5sJaAYbFuAPPPxDSPt1AQAA///zOIFGAAAABklEQVQDAMJsmSHHAV6qAAAAAElFTkSuQmCC)

15 sites

- [](https://dev.to/sachindra149/understanding-pass-through-authentication-pta-and-password-hash-synchronization-phs-412n#:~:text=PTA%20allows%20users%20to%20authenticate,keep%20their%20authentication%20processes%20local.)
    
    Understanding Pass-Through Authentication (PTA) and ...
    
    Feb 22, 2025 — Understanding Pass-Through Authentication (PTA) and Password Hash Synchronization (PHS) * Pass-Through Authentication (PTA) PTA al...
    
    ![](data:image/png;base64,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)
    
    DEV Community
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFIAAABSCAMAAADw8nOpAAAAbFBMVEX///8IDjwAAAD09PQAABns7Oz5+fnZ2dnv7+/R0dHj4+O1tbWtra3m5ubW1tbf39+UlJRPT09VVVWkpKTExMS9vb2MjIwsLCxkZGR2dnZpaWlERERcXFw/Pz9+fn6bm5sbGxsiIiIzMzMPDw+PzHUrAAAEhUlEQVRYhe1Xa3OkKhDtCxeUh4ryUBB01P//H29rNruTnWRTqc2XWzUnleiAfezXaSbwz7cD/h+U/347gH474Iknnnjiia+Dr3y9n6Cdc+LhIVx0Tmr+jr2qHtcITfeUgcQxPNhF0ic/vkc5qOuyir537TD1rJsnQgsvsXiIfY/bIYEgkAcDNmcmhsFdJqMHseWemamnfdF8BB14Hvoq5dmcwTodstjkrJKpCMUfZydfmtkCmN3skVlPGFG2moLXzLsflN2gl0Gm0JCGwLrY3IwiGfTgjC6FQRTINgu4KBufbYLppJyRQRRNqMtD1cVBiSW8UO6Q7GJgdkAcAbuc92Ly9KQUJSy9G2HQYVgvSul7cehR49smfEDPmnSTmG3QZr4CvykQI74T6UOvCRA7L37URGRVn5SKGWU7C1pwq1YeeKgrDcruSOnOdHOrTd0aDWxd65f0V9BYUOJMgg4NOKM8WmxCtfyhmq9gfSzso813UfVp/vMJTtv3muRPYO/05DeiuwufgnX3e9XUGWNBhNUEBgKbIMu31jxhOKsx3d2aqNWvewLujf8z1UTnXthbWhlkwuAq6T0IUhJjyJ3dITaYyEgXcrQ9WZeVEbKwYyNYcVlAF2BoNeN7m3HAtYL+KEJ0S26kE/jnpKRQ9EqIaI4b9l0riiuwtk73piMQdVqBiIPpAcAvoMlEFnQXyUxsR8AHMB/Yw9iZSaMeLsqhECZUiqpUXkIlis/AZLkEiRao/cPfLkqFlKNs4KLk8z5geCflFPRw6Se7F0qHrqMWEs6UgvkWIzsWDH85UK8+WnfEUZLGolK6Gex2pQcbX5BW5gV6TNqQhv7Ml7VbxKCBYM34vuxJnUoDVTtgSkLjhQDRth20inLPJZael+uCcBgO3knPz/Jw3zqG6u+wmh4/q7PJa49PCFV/0mAu/r4SH2fyF/Ggyq/J9Gt4CJC+J+Gg3n7m6VeULfg3SZCpSxPuxwq1BS7FRvzc55LWDb6yYdgUDQXJzl+oz0XfNBIvTQMtEdIDlRRYLU93JiGJU0QeDtSMt2uB+KplVcxtH3m4ERfLVoBsfhpvItzKXheXZ2L1vFtDgpr5PuJaORKG3dPuYPRwm6ptzw7LcGxOPyijXpdTlXXnImoBUAY30JOJMIoeXdihNTHTsVYZuz/ZwUvsoy5Dh5pJsI3z2EOXDgvV/oOSgFngJsamrqLlBPsOpaaQku+ix+hq2K3ObGMq2wmiHVT3SlnV54gAPFcMiKP+SdmflKRZ+pt6ocQZkYkLkW9idmWPKg1loOOienqbCJsvSj7TjpwNRc5c0i2jwz/rp6GRgDO8a86qoIDO8tbnYkU7WrUt7tYV1F3dARccqpq3Z74cXIO/pYC7UHWntF8r/sfu+xA8/37S+A9PsieeeOKJz8Bfjgyq1a+h5P+KsQpGO6/pKpx1VHgIndNR/M132lyvU22z9doqHZYQIC0sT58bfoykTZQp4r8Ny1pv1hq/LDwtf+Mlr/C8lLIOynNgnOJJwaDh8nPLz1F99p3riSeeeOL/g/8A4kFTa9o3hb0AAAAASUVORK5CYII=)
    
- [](https://blog.quest.com/determining-the-right-hybrid-identity-authentication-method/#:~:text=Microsoft%20Entra%20PHS%20creates%20a,servers%20in%20the%20authenticating%20forest.)
    
    Determining the right hybrid identity authentication method
    
    Jul 1, 2024 — Microsoft Entra PHS creates a connection between on-premises Active Directory (AD) and the Entra tenant. This solution synchronize...
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAMAAAD04JH5AAAAIVBMVEUAl8UAmccAmMYAmcYAmcYAmMYAmMYAmMYAmcYAmMYAmMZt0OtPAAAAC3RSTlMC/yvM6BBEi6pxW79euwkAAAOtSURBVHic7VvblqQgDGwbEPX/P3gIFwVJdC6dYvcc82rPpCRFSCr4ej322GOPPfYhc86N9f4ONgwCuZ/neRgCevt5W7d5EIDw/sH96j0hwENwr/d721a/LAshwC8CvT+5N8Ysfg0IBvjf/GKstRkBdgmK/8lOU4CQEAAhBP8UfhPcRwA5CjAEOf4mALAjEKT1D+7jAhwINhiAkH/WJb9+hgBl4jsuQO0/rwEoH8QE6E3lvuIBYhEyA1sA0ChkAPYMwaDywbtsQi4KCB64HcHEIMCcCyUKLYAcBUQ+KKl4HBPjVmSYOIAHbD4IEJQB7AdStwTpdP4neKCfD2Y2CtMeBW0IN/kAUa47FoGNVVrcDNoAZB7QIgQm6hMh5wOWB8sKSAgyDwIET0RQz0g8D4gIoWeh7agMQObBnpZRPOgrlJgUoTzotiPqcBTOhSMtawOoEPRZEcWD3Kyzh+OmX667qNawCFBlmiubgeGBuWCiO9nN4wuTAFwICFnma60C4dgfiLanA75I6vNB/O9zawnC8Xw+/+DCSDJbhITE8iDKjFv4s8q2SndMz9efmOdOxooHHW1o1WpLCJz4/NZINWMAsDxwOWqNxUoqA+We35phQlDlg6ZtK8VEZUtd0zPP763noMiDpLQttrFUxrjyfE1v9H2bumRc86A9FzihwVanlyBE/N7O58IAAG19AAcwnWRdPIA9HwwEQFEYC8AMBxBoOJYDIwGcxIsRiaiRc9EAurHCAABtlxIPI9+eNZQm/noYCe6nvkvSOY55CNxYp9SxHy1IBATsWMnplGR8GFjp7vNFqWc7VIZ/+xJ0Zfn8+7KcJslp1wgyft8kc32H+0NjkgGIYwS+ObvuzX7Wml1qBPq6qSiXIVSS+zGOMoBr4RqhU/GjPJRKJQ0vJnT8+fGN9vo7QaiEDTJ3qXbQKFfY/1L+/7z76/yjLpKKAwubNBlY/Pv1pw5IO/7SsOLUgOj5F+J/bsPV/Dsp/3OClAYAcVSTOlB1AghDCosZUkSR8WJMo03AEn9BmNY/AKTzHzaicVHjlIcTut6JALltZfmnPq7Nt+ku9r92ASp0ALC7nRSA8226CXqHKN8nZOMPulAYOND2gCX+kOt83JVO2Ig2AqBt6JtdABtS7wiaQgB+u9odF5stcv/XEHIugOb/M4RyuR0c/+K/ut6Pua7TQ6APHEgUwlxY4qwImYiLc6xFpTN/YzLAfebBvA3z/yofGo1Z/wPDUPePPfbYY/+xfQHVfE3UftalvAAAAABJRU5ErkJggg==)
    
    Quest Software
    
    ![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBwgHBgkIBwgKCgkLDRYPDQwMDRsUFRAWIB0iIiAdHx8kKDQsJCYxJx8fLT0tMTU3Ojo6Iys/RD84QzQ5OjcBCgoKDQwNGg8PGjclHyU3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3Nzc3N//AABEIAFIAUQMBEQACEQEDEQH/xAAbAAABBQEBAAAAAAAAAAAAAAAAAQIDBAUGB//EAEAQAAEDAgMCBwwIBwAAAAAAAAEAAgMEEQUSITFBExRRVWGRkgYiMjVSc4GTobHR0hUWU2PBwuHwIzNFVGVxcv/EABkBAQADAQEAAAAAAAAAAAAAAAABAgMEBf/EACwRAAICAQIEBQQCAwAAAAAAAAABAhEDElIEEyExBSJBUWEVMjNTFIFCYnH/2gAMAwEAAhEDEQA/APXkMwQAgBAF+lRZNBdTaIpgliqBACAEAIAQCFwG0qHJEpNjHSeSOtUcy6gNzE71RybLqKQigkEA4OIVlJoq4pkjXAjRaJ2ZNUKrEAgBAV6+qbR0sk8lyyNuZ2Xaqvq6JtRi5MrCpqbeLantR/Mo5XyOa9ocZqebantR/MnL+Sec9ocZqebantR/Mo5fyQ80tocZqebantR/Mp5XyOc9ocZqebantR/MnK+RzntDjNTzbU9qP5k5XyOdLaKKmp3YbU3/AOo/mTl16h5XtLNPUcKHBzXMe02c11rg2B3dBCt9rpkpalaJ1JUEBld0JvhFb5sqkH50Tm6YmZeI9zcmKYnU1YqYwOEaAyRhdbKBpoRofxKiWJt3Zvj4hKCjp6r5Kh7h5Ta1dENLaRHX2rGfDOTtSOvF4isad40/7E+o0vOEfqj8Vn/DlvZr9Vj+lB9RpecI/VH4p/De9j6rH9KF+o0v9+z1R+Kfw3V62T9Vj+lCHuGl5wj9UfipXBPeyPqsf1Igou5mKooIqiOondOdS1oytadtgbHXYto8Iovq2ccvFJZIvTFJf8OjL6impJ6qdxZKe+c3gy5twABrptsFvKCfY4VOUVbNWN9wL31VFI2cbVktugq1lDIx/wAT1h+7Kpj+9DP+Jl+k8Kp88fcFtIohmKQT1FBNFSTcDO5tmSeSVEXTE02uhDW0lfNSQMp6oRzMc0yO1s8Ai496squ2UcZV3HVVLWSV9LLBU5II78LH5aJqg1JtOxzKerbi0k7p70hjDWw8hG9RaotUruxKGnq4J6o1NRwsb33jbvYLDT2KSI3fUw6LEDRYPSRxzQwPnlLeFl1DGhoJNt+4elc3FZlja61Z2eGcOs0XJptL0RJJiJq8PxGmfUwVJiawsmiFg8E7Lct/wUcNkcpuN2acfwyxY45FFq/RmpQ1TZgWB4eRfK4AjMAbHQ7CCCCPiFecGnZy456kXMzulUtmugzse8TVfmyr4/vRjn/Ey/SeFU+ePuC1ZSJOoRYp8Qb9z6lqmyjj6swqzG6ClrjSCPhSx2V7o6dpAO//AGuSXHQjPSeri8Hy5MXMukbcVJFNE2SN0LmPALSIRqCupTUlaPMlicG4luKMRRBgtpfY2w6lN9UKo5BuDT4rhVE+nkja6B7iQ++oIb8FzcbgllcdL7Hf4RxsOHhJTXf2LVBgM1HJUy1joi2pljsyInT+IDt3KnCYJYpuT9TTxLjcfEYo44309zUdEyKmlfGMroKguBO2xIJvy3BK7JdUeVHyl7L0LCjp1Gfj3iar80VbFepGWb8bLkEscclS2SRjXcMTZzraZQtmZxfuS8Zg+3j7YUUXtBxmD7aPthRQtHLV+Avkqp+K11I2nneXkvPfx5vCAtuK8/Jwc3J0e3i8VxRgub9y6fD9jpKQ0tJSxU8c7MkTA0EvGtl3QjpjTPIy5OZNzfdkvGYLfz4+2FddzJ9mjJoyMPw4xAnhGNPfRytLXEbDa9+TRWfUyXliPnqHtpncJHO6SGRmbVuW+YOA28hChOmW7qzQqgKnD5hCQ4SROyEb7jRR60X7lD6apfL9irpJsrA1ULZoKzCqirYXuyyCZpztJuMwzej0K9RTu6ME5u042Pdibx4WCYjfoeD+ZT03EOctjGfS3+ExPr/VOm4h5HsZHJipfbLhOLR23ttr1lSlHcVc/wDRkZxKTm/GOpqnyr1HMltY6PFHMdd2F4u8W2Otb2WTy7gsr2slGLE/0TE+v9VFLcOY9jJG4jI7wcExH0vA/Mote5dTk/8ABiullkjfweCTZnjXhZ2hp0t31nHRVenvZdObVaS3ROkoooY53OdEWht3uzGN3Sd4Pv8AZVTtmqi0jRyHkPUrWQI4ZhqquKZaMmiMtI2hYtOzVSTGqOpYE6gEAIAQAgoE6BtoeIg5pEgBaRYtO8LSMTKcrE4vD9mOtaGdEqEggELWncFGlFtTE4NvJ7VGlDUwyN5PamhDWw4Nv7KaENbDIP2U0Ia2GQdKaETrYoaBsCKKIcmxVYqCAEAIAQAgBACAEAIAQAgBAf/Z)
    
- [](https://static.carahsoft.com/concrete/files/9416/6154/4033/AD_Security_Training_Master.pdf)
    
    Active Directory Security Deep-dive Master Class - Carahsoft
    
    These include accounts that are used to support applications, services, scripts, schedule tasks, and more. ... Backward compatible...
    
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAABPklEQVR4AaRS0W2DMBCFigHSTyRA8QbpBmWTdpIkk7Sb0A2aDRwBEp/JAEjOe47vYkKEFAX59Hx3796djd+SF79Fgb7vN13XfS71mAmwAOZozrl/FDfc04ZhWMOfrIkASDtkGxR+l2WZ0uDrGsfRBo7GVCCob0F6r6rqF+OT7JR522whosdSARRadjbGnMnFfjYu48GagIkKMMDOxGfMC8QjSTHPLyaxGHHEDX0vkKapHxtC/vYFQbIkIX8kxoYjruh7gaIoDnTuDaQ1xBrkjUxDJA/4R/QC3CyY3jg5bdt+EcVigVqCAWt0mbwFa+0Kx/nJsswEzu0vgMyR9pK4R3ZG4QnxfZ7neifxBAlEdiCJuj5h3INjZxRzKr5WbK9rIsAQ1SEko9co/BAfyClJU5sJaAYbFuAPPPxDSPt1AQAA///zOIFGAAAABklEQVQDAMJsmSHHAV6qAAAAAElFTkSuQmCC)
    
    Carahsoft
    
    ![](data:image/png;base64,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)
    

Show all

yes

To refine the 

**Initial Access** chapter, we move from the "what" (architecture) to the "how" (intrusion). This is the bridge between your architectural deep dive and the exploitation phases.

Chapter 4: Initial Access — Piercing the Perimeter

**Sub-title:** _Gaining a Foothold in the Modern AD Environment_

**4.1 The Psychology of the Entry**

- **External Reconnaissance:** Using Shodan and Censys to find exposed AD components (RD Gateways, VPNs, OWA).
- **The "Low and Slow" Approach:** Why attackers avoid high-volume brute forcing in favor of strategic entry.

**4.2 Credential-Based Entry (No "Exploit" Required)**

- **Password Spraying:** The mechanics of testing `Summer2024!` against thousands of accounts.
- **Credential Stuffing:** Leveraging leaks from third-party breaches to find valid AD credentials.
- **Bypassing MFA:** Social engineering (MFA fatigue) vs. technical bypasses (legacy protocol abuse).

**4.3 Technical Perimeter Exploitation**

- **Vulnerable Gateways:** Targeting unpatched VPN concentrators or Citrix instances to land inside the network.
- **ProxyLogon & ProxyShell:** A look at how Exchange Server vulnerabilities provide direct SYSTEM access to the internal environment.

**4.4 Client-Side Execution (Phishing)**

- **Payload Delivery:** Understanding Mark-of-the-Web (MotW) and how attackers bypass it.
- **Living off the Land (Initial):** Using `mshta.exe` or `rundll32.exe` to execute code via malicious links or attachments.

**4.5 The Internal Pivot (The "Beachhead")**

- **Establishing a Beacon:** How Cobalt Strike or Silver (C2 frameworks) communicate back to the attacker.
- **Initial Discovery:** The first 5 minutes on a machine—what the attacker looks for (Who am I? Where am I? What can I see?).

---

The "Initial Access" Researcher Prompt

Use this to generate the technical "meat" for the Password Spraying and MFA sections:

> **Prompt:** "Act as a Red Team Operator and a SOC Analyst. I am writing **Chapter 4: Initial Access**.
> 
> 1. Provide a technical walkthrough of a **Password Spraying** attack targeting an on-prem **Exchange (OWA)** or **VPN portal**. Include the logic for avoiding 'Account Lockout' thresholds.
> 2. Explain **'MFA Fatigue'** (Push Bombing) and how attackers use it to bypass modern authentication.
> 3. For the **Blue Team**, provide a list of **Event IDs** (specifically **4625** for failures and **4624** for successful logons) that help distinguish a 'Password Spray' from a regular user mistake.
> 4. Write a sample **PowerShell script** that a defender can use to audit the 'BadPasswordCount' across the domain to proactively find accounts under attack.
> 
> **Format as an 'Entry Operations' guide with code snippets and a 'Defensive Telemetry' section.**"

---

Pro-Tip for your Book:

In this chapter, emphasize that **Initial Access** is often the "noisiest" phase. This is the defender's best chance to stop an attack before it reaches the **Architecture Deep Dive** components (like FSMO roles) you just mapped out.

**Would you like to move into "Chapter 5: Internal Reconnaissance" next, where the attacker uses their new "Initial Access" to map out the "Architecture" you defined in Chapter B?**

[](https://labs.google.com/search/experiment/22)

should we include a network refresher? without a network there is no AD

Absolutely. You cannot truly master 

**Active Directory** without understanding the "pipes" it flows through. In the world of AD, **Network is Identity.** If you control the network (via DNS, DHCP, or Routing), you can often control the identities.

Here is a plan for **Chapter C: The Network Foundation of Active Directory.**

---

Chapter C: The Network Foundation of Active Directory

**Sub-title:** _Protocol Analysis for the AD Security Professional_

**C.1 The AD Port Map: The "Swiss Cheese" Firewall**

- **The Ports of Entry:** Why a Domain Controller needs so many open ports (TCP/UDP 53, 88, 135, 389, 445, 636, 3268, 3269).
- **Dynamic Port Allocation:** Understanding the **RPC Dynamic Port Range** (49152-65535) and the headache it causes for firewall administrators.

**C.2 DNS: The Heartbeat of Discovery**

- **SRV Records:** How a workstation finds a DC using `_ldap._tcp` and `_kerberos._udp` records.
- **AD-Integrated DNS:** The security implications of allowing "Non-secure and Secure" dynamic updates.
- **DNS Poisoning:** How an attacker can redirect traffic by spoofing records.

**C.3 The "Chatty" Protocols (The Poisoner's Playground)**

- **LLMNR & NetBIOS (NBT-NS):** Why these legacy broadcast protocols are the #1 way attackers capture hashes (Responder).
- **mDNS:** The modern equivalent and its role in internal reconnaissance.
- **DHCP Snooping:** Preventing an attacker from inserting a "Rogue DHCP Server" to become the Default Gateway.

**C.4 SMB (Server Message Block) Deep Dive**

- **SMB Signing:** The difference between "Required" and "Supported" (and why "Supported" is a death sentence).
- **SMB Dialects:** Understanding the security improvements from SMB 1.0 to SMB 3.1.1.

**C.5 Network Segmentation & The "Flat Network" Trap**

- **VLANs vs. Micro-segmentation:** Why simply putting servers on a different VLAN isn't enough.
- **IPsec for Domain Traffic:** Using Windows Defender Firewall with Advanced Security to encrypt traffic between servers and DCs.

---

The "Network Forensics" Prompt

Use this to get the technical protocol data for **Section C.3**:

> **Prompt:** "Act as a Senior Network Security Engineer and Packet Analyst. I am writing **Section C.3: The Chatty Protocols**.
> 
> 1. Provide a technical breakdown of the **LLMNR (Link-Local Multicast Name Resolution)** and **NBT-NS** broadcast process. Explain exactly what happens when a Windows machine cannot find a hostname via DNS.
> 2. Describe the **'Responder' attack logic**: How does an attacker 'poison' these requests to force a victim to send an NTLMv2 hash?
> 3. For the **Blue Team**, provide the exact **GPO paths** to disable LLMNR and NetBIOS across the domain.
> 4. List the **Wireshark filters** a defender can use to identify rogue LLMNR responses or NBT-NS spoofing on the wire.
> 
> **Format as a 'Protocol Deep-Dive' with a 'Step-by-Step Attack/Defense' workflow.**"

---

Pro-Tip for your Book:

Add a small sidebar called **"The MTU/Fragmentation Trap."** Explain how Kerberos tickets (especially for users in many groups) can become so large that they switch from **UDP** to **TCP**. If a firewall blocks TCP 88, Kerberos will "mysteriously" fail for some users but not others. This makes you look like a pro to your readers!

**Since we now have the Network, Architecture, and Initial Access covered, should we dive into the "Internal Reconnaissance" chapter to show how an attacker uses these protocols to map the domain?**

[](https://labs.google.com/search/experiment/22)

Yes internal recon and Would you like to move into "Chapter 5: Internal Reconnaissance" next, where the