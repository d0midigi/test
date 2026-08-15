Why Did I Write this Book?



I needed this book 20 years ago when I started my first role as a help desk technican with the Department of Defense. 6 months later, I was promoted to the Network Security Operations (NetSecOps) administering three networks on a flat novell domain at the time: a DMZ, one NIPRNet and one SIPRNet. Fast forward 20  years into the future, and here I sit, and as I type this there are still zero books available for beginners starting out in the cybersecurity world on the federal side of things. Federal Identity, Credential, and Access management functions very much the same as traditional Identity d Access Management (IAM) in commercial Active Directory domains; however, there are some pretty major and critical nuances that make the two security models differ from one another. Besides the fact that you will be managing an regular Active Directory domain build from Microsoft for the government vice commercial sectors, the policies, procedures, mandates, to Operational Orders (OPORD), Presidential Executive Orders, Fragmented Order (FRAGO), and Warning Orders (WARNORD) to IAVA/IAVB and IAVT, to Gold Disk and DISA STIGs and SRGs. Other than a handful of published articles from government agencies online in regard to FICAM domains, there's really no options for people who are starting out the same way I did.



A specialized book on Active Directory (AD) domains within Federal Identity, Credential, and Access Management (FICAM) networks is critically needed because existing literature focuses on commercial Active Directory environments, neglecting the rigid regulatory, architectural, and operational constraints of federal information systems. FICAM-based AD is not merely about user, group, and computer management; it is a phishing-resistant, PKI-centric, high-information assurance framework (PIV/CAC cards), often utilizing Active Directory federated identities, which requires entirely different offensive and defensive strategies comopared to standard commercially available Active Directory.



A book dedicated to FICAM-enabled Active Directory (AD) and federal networks would be a "Holy Grail" resource because most industry training assumes a private sector environment. In corporate AD, the focus is often on covenience and "good enough" security; however, in federal AD, the environment is governed by Zero Trust Network Architecture (ZTNA), mandatory Smart Card with Personal Identity Verfication (PIV) through the use of Common Access Cards CACs) and OCSP responders through the use of a third-party software, like Tumbleweed, with security enforcements from all military branches to include Air Force, Army, and Navy, the CNSSI, CNSS, CMMC, and NIST 800-53 security controls.



The benefit of such a book stems from the fact that current offensive and defensive "playbooks" often break when they hit a TIC 3.0 (Trusted Internet Connection) or a FICAM (Federal Identity, Credential, and Access Management) compliant boundary.



The impetus for this book stems from a critical, systemic vulnerability within the federal cybersecurity workforce: the "knowledge gap" between commercial enterprise Active Directory (AD) administration and the rigorous, mandate-driven reality of Federal Identity, Credential, and Access Management (FICAM). While the private sector focuses on "Identity and Access Management" (IAM) as a business facilitator, the federal government treats Identity as a weaponized system. This book was written because, as stated above, there is no consolidated field manual that prepares an incoming Cyber Mission Force (CMF) operator or a civilian contractor for the specific architectural complexities of a FICAM-compliant Active Directory environment.



The curret training landscape for ethical hackers and offensive and defensive specialists is saturated with "General Corporate" AD content. These resources teach you how to exploit NTLM relaying or remediate weak passwords through the use of MFA; however, in a federal environment goverend by Presidential Executive Order 14028 (Improving the Nation's Cybersecurity), such "low-hanging fruit" is largely threoretical. When a new hire enters an agency, they are often blindsided by the shift from username/password paradigms to mandatory identity proofing and PIV/CAC-enforced NTLM-disabled environments.



This book serves as the bridge between theoretical hacking and operational federal reality.



To understand why this resource is more than necessary, one must look at the unique "Command, Communications, and Control (C3) structure of federal networks and domains. Our infrastructure is not merely managed; it is directed through a hierarchy or a chain of operational directives.



Federal cybersecurity specialists do not operate in a vacuum. We are goverend by:



* **Presidential Executive Orders (EOs):** Specifically EO 14028, which mandated the shift toward Zero Trust Network Architecture (ZTNA) and centralized FICAM governance.
* **Warning Orders (WARNORDs):** These are the preliminary notices of upcoming shifts in security posture - such as the transition from a FISMA security model to the Risk Management Framework for DoD (NIST SP 800-37 and 800-207) standards that allow security teams to begin resource allocation before a final directive is issued.
* **Operational Orders (OPORDs):** These provide the specific "Who, What, Where, and Why" for large-scale security deployments, such as the mandatory rollout of Derived Credentials for mobile endpoints.
* **Fragmentary Orders (FRAGOs):** In the federal space, a FRAGO might be issued from higher Commands mid-operation to mandate a change configuration on the fly in response to a new Zero Day threat released in the wild, such as an emergency directive from CISA - except, it's DISA on the federal side, Defense Infrastructure Security Agency and the United States Cyber Command (USCYBERCOM).



From an offensive perspective, the Red Teamer arriving from the private sector is often ineffective in a FICAM environment. Traditional lateral movement tools break quickly when they encounter strict PKI (Public Key Infrastructure) requirements and TIC 3.0 (Trusted Internet Connection) and Global Information Grid (GIG) boundaries. This book provides the first dedicated look at attacking the "Identity Provider" (IdP) and exploiting the trust reltionships between federal forests - the only way to maintain persistence in a true Zero Trust environment.



Defensively, this book moves beyond the "Compliance is Security" fallacy. while we adhere to DISA STIss (Security Technical Implementation Guides) and NIST SP 800-53 security controls, those are merely the baseline. A true "Govie" defender must understand how to operationalize FICAM to create a "Defense in Depth" security posture that can ultimately withstand an Advanced Persistent Threat (APT).



I wrote this book to stop the "Tribal Knowledge" cycle. For too long, the secrets of defending and auditing federal AD domains and networks have stayed locked in the minds of senior GS-15s and long-term contractors. By codifying these "Operational Orders" and "Tactical Procedures" into a structured curriculum, we ensure that the next generation of federal defenders is ready to protect the nation's most sensitive data on Day One when i is time to report for duty.



(NEED TO ADD HOW I IMPART WHAT I'VE LEARNED AND ADD A SHARPER CLOSER).



This next section provides the technical and regulatory "why" behind the shift in Federal Active Directory. We will first examine the mechanics of the PIV-enforced authentication flow and then look at the DISA directives that dictate its implementation.



\## Architectural Breakdown: The PIV-Enforced Login Flow



In a FICAM-compliant federal Active Directory environment, the traditional "Username and Password" (something you know) is superseded by Mandatory Smart Card Redirection (something you have). For an ethical hacker, this represents a massive shift in the attack surface.



\### The Pre-Auth Discovery



* **The Client Request:** The workstation detects a Smart Card insertion via the PC/SC (Personal Computer/Smart Card) interface.
* **UPN Mapping:** The User Principal Name (UPN) is read from the Subject Alternative Name (SAN) field of the X.509 certificate on the PIV card.



\### The PKINIT Process (Kerberos Extension)



* **AS-REQ (Authentication Service Request):** Unlike a standard login, the client sends an AS-REQ that includes a digital signature created by the PIV card’s private key.
* **The KDC Validation:** The Domain Controller (acting as the Key Distribution Center) validates the certificate against the Enterprise Trusted Root Store and checks the CRL (Certificate Revocation List) or OCSP (Online Certificate Status Protocol) responder to ensure the card isn't revoked.



\### PAC (Privilege Attribute Certificate) Generation



* Once validated, the KDC issues a Ticket Granting Ticket (TGT).



**Note of importance: Critical Detail:**

In a high-security Federal AD, the TGT is flagged as having been authenticated via HW-MFA. Many federal applications are configured to reject any TGT that does not carry this specific "strong authentication" attribute.



\## DISA Directives: The Strategic "Move Orders"



While the architecture defines the how, CISA (Cybersecurity and Infrastructure Security Agency) defines the when and must. These directives act as the federal government's "Grand Strategy" for AD security.



\## Binding Operational Directive (BOD) 23-01



* **The Mission:** Mandatory asset inventory and vulnerability detection.
* **The AD Link:** This directive forces agencies to identify every "shadow" AD forest or orphaned trust relationship that hasn't been migrated to FICAM standards.
* **Offensive Reality:** For a pentester, these "non-migrated" pockets are the primary entry point into an otherwise hardened network.



DISA Zero Trust Maturity Model (Version 2.0)



* **The Identity Pillar:** CISA has moved the goalposts. It is no longer enough to have MFA; the goal is Phishing-Resistant MFA (FIDO2 or PIV).
* **The AD Impact:** Traditional "Internal" trusts are being replaced by Federated Identity. Instead of a Forest Trust (which allows lateral movement), agencies are moving toward SAML/OIDC-based connections where the AD never actually "talks" to the other forest.



Emergency Directive (ED) 24-03 (and its Predecessors)



* **The Focus:** Mitigation of credential theft via "Living Off The Land" (LOTL) techniques.
* **The Requirement:** Agencies are now under strict mandated and compliance-driven FRAGOs to disable NTLM wherever possible and enforce Credential Guard.
* **The Defensive Shift:** Federal defenders are now being graded on their ability to hunt for "Silver Ticket" attacks that attempt to bypass the PIV requirement by forging the Kerberos PAC.



\## Tactical Intersection: What This Means for You



When you combine a PIV-enforced login with DISA directives, the result is an environment where:



* Credential Dumping (Mimikatz) is largely mitigated because there are no cleartext passwords in memory.
* Lateral Movement requires the physical redirection of a smart card or the compromise of the Root CA (Certificate Authority).
* Persistence is achieved not through a backdoor, but through the illicit "issuance" of a rogue certificate.



**NOTE:** While CISA (Department of Homeland Security (DHS)) issues directives for the *Federal Civilian Executive Branch (FECB),* the Department of Defense (DoD) and the Intelligence Community (IC) march to the beat of a different drum.



In the federal word of *DoDIN (DoD Information Network)* operations, your authority comes from the United States Cyber Command (USCYBERCOM) and the technical implementation standards are dictated by DISA.



\## The Command Hierarchy: USCYBERCOM and DISA



In a federal textbook, we must distinguish between "Guidance" (CISA) and "Orders" (Cyber Command). When you are operating on a DoD NIPRNet, the Non-Classified Internet Protocol Router Network or SIPRNet, the Secure Internet Protocol Router Network, you aren't looking for a random blog post; you are looking for a *Task Order (TASKORD)* or a *Cyber Operations Directive (COD).*



\### USCYBERCOM: The Operational Authority



USCYBERCOM issues the Executive Orders (EOs) that strategically move the entire force.



* **TASKORDs (Tasking Orders):** These are the mandatory "marching orders." For example, if a new vulnerability hits Active Directory, the USCYBERCOM will issue en masse a TASKORD with a specific *suspense date* (deadline). Failure to comply isn't just a security risk in and of itself; it is a complete failure of a Command directed by a four-star General.
* **OPORDs (Operational Orders):** These define how the *Cyber Mission Force (CMF)* will defend the FICAM AD environment during a specific window or defined mission.
* **FRAGOs (Fragmentary Orders):** These are used to pivot. If the Red Force (adversary) changes tactics against a FICAM infrastructure, a FRAGO will be issued to immediately adjust the defensive posture across all *Combatant Commands (COCOMs).*



\### DISA: The Technical Architect



If the USCYBERCOM gives the orders to "Fortify the Gates," DISA provides the blueprints to accurately carry the mission forward.



* **STIGs (Security Technical Implementation Guides):** This is the "Bible" for any Federal FICAM AD admin. In later chapters, we will address how to automate STIG compliance using *SCAP*, the *Security Content Automation Protocol.*
* **SRGs (Security Requirements Guides):** These are the higher-level "Strategic" versions of STIGs that define how FICAM should behave at the architectural level before the first Domain Controller is even promoted.
* **CCIs (Control Correlation Identifiers):** These are the bridge between the technical setting in AD and the NIST SP 800-53 security controls that are required for a Command's *ATO (Authority to Operate).*



\## The FICAM Kill Chain in a DISA-Governed Active Directory Environment



From an offensive and defensive perspective, the DISA/USCYBERCOM relationship changes the "Game Board' entirely.



\### The Defensive "Govie" Reality



Defenders in this space don't just "check logs." They operate within the *JRSS (Joint Regional Security Stacks)* or the newer *Thunderdome (Zero Trust) architecture.*



* **HBSS (Host Based Security System):** You aren't just looking at Active Directory logs via the Windows Event Viewer; you are monitoring the McAfee/Trellix events via the ePolicy Orchestrator (ePO) dashboard that trigger when someone or something tries to touch the `lsass.exe` process on a Domain Controller.
* **ACAS (Assured Compliance Assessment Solution):** This is the Tenable/Nessus implementation used to report *Cyber Readiness* up the chain to CYBERCOM.



\### The Offensive Ethical Hacker Reality



If you are a Red Teamer on a DoD contract, your "Rules of Engagement" (ROE) are governed by the *Staff Judge Advocate (SJA)* and the *Current Operations (CUOPS)* cell.



* **Bypassing the STIG:** Your job is to find the one setting the previous admin may have missed - the "Non-STIG'd" legacy server that still allows for NTLM fallback and DNS fallback to LLMNR/NBT-NS protocols.
* **The Gold Ticket in a PIV World:** PIV is **mandatory**, a 'Gold Ticket" (forging a TGT) is only useful if you can also forge the PKI attributes that tell the service "yes, this user actually swiped a card."



\## The DoD Network Tiers: NIPR, SIPR, and Beyond



The federal government's Active Directory (AD) landscape is divided into specialized network enclaves, each with its own Rules of Engagement and technical mandates. In the Department of Defense (DoD), this is known as the *DoD Information Network (DoDIN)*, where the digital backbone is treated as a weaponized system.



Operating on a federal network requires an immediate understanding of which "wire" you are operating on. In the DoD, these are largely separated by classification and physical network isolation.



\### NIPRNet (Non-Classified Internet Protocol Router Network)



* **The Mission:** Used for unclassified but sensitive data (*Controlled Unclassified Information - CUI*).
* **Active Directory Environment:** This is where the *Common Access Card (CAC)* is the primary identity token. It is connected to the public Internet through a series of TIC 3.0 compliant gateways.
* **Offensive Perspective:** Penetration testers, ethical hackers, and defenders focus on the massive attack surface of millions of users, looking for SAML/OIDC federation vulnerabilities that could potentially lead to lateral movement from a contractor enclave into the main internal DoD fabric.



\### SIPRNet (Secret Internet Protocol Router Network)



The Secret Internet Protocol Router Network (SIPRNet) is a secure, private network used by the U.S. Department of Defense and Department of State to transmit classified, or *Secret Compartmentalized Information (SCI)* up to the Secret level. It acts as a classified version of the Internet, providing secure email, web services, and data for military and diplomatic operations.



Some key facts about the SIPRNet include:



* **Purpose:** It supports national security by providing a secured environment for military intelligence, situational reports and assessments, an diplomatic communications to be transmitted via a *TACLANE.*
* **Access:** It is utilized by millions of U.S. officials, military personnel, and specifically cleared users.
* **Access Levels:** While primarily for the U.S., it is accessible to select members of the Five Eyes intelligence alliance (Australia, Canada, UK, New Zealand).
* **Security:** Unlike the open internet, it requires specific hardware tokens (smartcards) for access.
* **Distinction:** It is separate from the NIPRNet (Non-Classified Internet Protocol Router Network) and JWICS (Joint Worldwide Intelligence Communications System), which handles top-secret data.
* **Naming Convention:** Files and websites on this network often use the "`.sgov.gov`" or "`.smil.mil`" domain.



https://image4.slideserve.com/9210464/example-of-siprnet-at-user-l.jpg





\## Enter TACLANE: Accessing Classified SIPRNet to Retrieve Official Government Communications: WARNORDS, FRAGOs and Other Official Security Communique



A TACLANE is a low-cost, key agile, In-Line Network Encryptor (INE) that provides confidentiality, data integrity, and end-to-end authentication to protect data of all classification levels. TACLANEs can be shared with an enclave or users and can support the use of a single workstation for access.



TACLANE (KG-175) inline network encryptors interact directly with defense information systems on SIPRNet by providing Type 1 encryption for all classified data at rest and in transit, acting as the secure gateway that enables network enterprise defenders - such as ACAS (Assured Compliance Assessment Solution) and *CSSP (Cybersecurity Service Provider) GOTS (Government-Off-The-Shelf)* appliances - to monitor and protect DoD network traffic. They operate at the boundary between unencrypted (plaintext) and encrypted (ciphertext) domains, allowing for secure monitoring and compliance scanning, and document and communications retrieval across the entire SIPRNet enclave.



https://jproc.ca/crypto/kg175\_dual.jpg

