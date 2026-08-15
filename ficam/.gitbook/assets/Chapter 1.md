Chapter 1.



IDENTITY AS THE BATTLEFIELD: WHY ACTIVE DIRECTORY SECURITY IS A FEDERAL MISSION PROBLEM



ABSTRACT



Active Directory was designed to centralize identity, authentication, authorization, and administrative control across any given enterprise. In federal and military environments, however, those same capabilities concentrate mission risk, because control of the directory's trusted core can become control over the agency's or command's ability to determine who and what should be trusted. Chapter 1 establishes the book's central thesis: the correct unit of analysis is not merely the Active Directory domain, but the broader federal identity trust system in which the domain operates. That system includes directory services, certificate services, federation services, the Federal Public Key Infrastructure (FPKI), Personal Identity Verification (PIV), Common Access Card (CAC) credentials, authoritative attributes, cloud identity, privileged access, mission partners, the Electronic Data Interchange Personal Identifier (EDIPI), a 10-digit identifier the Department of Defense (DoD) issues and uses to protect digital identities, and the governance requirements that bind them. The chapter introduces identity as contested terrain, explains why adversaries follow trust relationships rather than administrative diagrams, presents Assume Breach as the operational starting point for identity security engineering, and frames the Active Directory identity attack lifecycle that structures the offensive chapters in Part II and the defensive mirror in Part III.



KEYWORDS



Active Directory; Identity trust system; Federal identity; FICAM; DoD ICAM; Assume Breach; Identity kill chain; Mission assurance; Zero Trust; Tier 0



KEY TERMS



**Active Directory (AD):** The Microsoft directory service that provides centralized identity, authentication, authorization, and administrative management for Windows domain environments.



**Active Directory Domain Services (AD DS):** The core directory role providing Kerberos-based authentication, Lightweight Directory Access Protocol (LDAP) directory access, Group Policy delivery, and the distributed database of domain identities.



**Identity Trust System:** The complete set of directory, credential, certificate, federation, attribute, cloud identity, and governance components an organization depends on to determine who and what can be trusted.



**Federal Identity, Credential, and Access Management (FICAM):** The United States federal government's enterprise approach to common identity, credential, access, federation, and governance processes.



**Department of Defense Identity, Credential, and Access Management (DoD ICAM):** The Department of Defense's policy, architecture, services, and operational implementation of identity, credential, and access management across classified and unclassified enclaves.



**Identity Plane:** The layer of infrastructure - directories, certificate authorities, federation services, cloud identity platforms, synchronization services - through which trust decisions are made, mandated, and enforced.



**Trust Boundary:** The defined perimeter within which an identity assertion is accepted without re-verification.



**Tier 0:** The set of systems, accounts, and services that control the identity infrastructure itself; compromise of any Tier 0 component implies compromise of all identities and systems that depend on it.



**Privileged Access:** The rights, permissions, and capabilities that allow a principal to administer, modify, or control the identity infrastructure and its dependent systems.



**Assume Breach:** The security engineering posture that treats initial access as an already-accomplished condition and designs detection, containment, and recovery capabilities accordingly.



**Cyber Kill Chain:** The sequential model of adversarial activity from reconnaissance through impact, developed by Lockheed Martin.



**Identity Kill Chain:** An Active Directory-specific adaptation of the kill chain model, tracing adversary progression from passive reconnaissance through domain dominance.



**Attack Pathway:** A chain of linked permissions, trust relationships, credential exposure, or configuration weaknesses that an adversary can traverse from a lower-privilege position to a higher one.



**Mission Assurance:** The confidence that an agency's mission-essential functions can be performed under adversarial conditions.



**Risk Management Framework (RMF):** The National Institute of Standards and Technology (NIST)-defined process for classifying and categorizing information systems, selecting and implementing security control families, assessing their effectiveness, authorizing information systems for operation and production, and monitoring them continuously.



**Zero Trust:** A security model that removes implicit trust from any identity, device, or network location and requires continuous, explicit verification of every access request.



LEARNING OBJECTIVES



Upon completing this chapter, the reader will be able to:



1. Explain why Active Directory security in federal and military environments is an identity trust problem, not merely a domain administration or hardening problem.
2. Describe the identity trust system as the book's primary unit of analysis, and distinguish it from the narrower concept of Active Directory domain.
3. Distinguish between the administrative structure an organization maintains and the adversary control pathways that structure can enable.
4. Explain why adversaries follow trust relationships - credentials, certificates, sessions, delegation paths, and federation assertions - rather than organizational charts or administrative inventories.
5. Describe how Federal Identity, Credential, and Access Management (FICAM) and Department of Defense Identity, Credential, and Access Management (DoD ICAM) change the meaning and stakes of Active Directory security.
6. Explain what Assume Breach means as an identity security engineering model and how it changes assessment, detection, and recovery requirements.
7. Relate the traditional cyber kill chain to an Active Directory identity attack lifecycle, identifying where identity-specific techniques replace or extend the original model.
8. Identify why security findings in federal environments must translate into mission risk, Risk Management Framework (RMF) evidence, and control validation artifacts.



STANDARDS, FRAMEWORKS, AND GUIDANCE COVERED IN THIS CHAPTER



**Federal Identity, Credential, and Access Management (FICAM) Architecture** - The government-wide identity architecture lens informing the book's federal framing.



**DoD ICAM Reference Design and Federation Framework** - The defense-specific identity implementation lens covering classified and unclassified environments, mission partners, and coalition access.



**NIST Risk Management Framework (SP 800-37)** - The control-validation and authorization structure connecting identity security findings to federal accountability.



**Federal Information Security Modernization Act (FISMA)** - The federal security governance foundation establishing accountability for information security programs.



**NIST Special Publications (SP 800-53, SP 800-63-4, SP 800-207)** - The primary federal cybersecurity, digital identity, and Zero Trust guidance layer.



**Federal Information Processing Standards (FIPS 140, FIPS 199, FIPS 200, FIPS 201)** - The federal identity and cryptographic baseline requirements.



**Office of Management and Budget (OMB) and Zero Trust Memoranda** - Federal executive direction on identity governance and Zero Trust adoption.



**Cybersecurity and Infrastructure Security Agency (CISA) Zero Trust Maturity Model** - The federal Zero Trust maturity guidance providing a capability-based progression framework.



**Defense Information Systems Agency (DISA) Secure Technical Implementation Guides (STIGs) and Security Requirements Guides (SRGs)** - The technical configuration and hardening authorities for Active Directory, certificate services, and related infrastructure. 



**MITRE ATT\&CK Framework** - The MITRE ATT\&CK Framework is a globally accessible knowledge base that documents real-world adversary Tactics, Techniques, and Procedures (TTPs) used in cyberattacks. It helps defenders to better understand how attackers operate and improve their threat detection and defense strategies. This framework is used throughout Part II to classify attacker TTPs.



**MITRE D3FEND Framework** - MITRE D3FEND is a framework designed to enhance defensive cybersecurity techniques and provides a structured knowledge base of Tactics, Techniques, and Procedures (TTPs) that agencies can use to protect their information systems and data. It complements the MITRE ATT\&CK Framework, which focuses on offensive tactics used by adversaries. The D3FEND framework is used throughout Part III.



1.1 READING ACTIVE DIRECTORY AS A TRUST SYSTEM



Most technical treatments of Active Directory begin with forests, domains, and Organizational Units (OUs). This one begins somewhere more important: with the question of what Active Directory actually is for.



1.1.1 ACTIVE DIRECTORY IS MORE THAN A DIRECTORY SERVICE



Active Directory is frequently described as a directory service - a database of users, computers, and groups that Windows networks use to manage access. That description is 



accurate; however, it is also dangerously incomplete.



What Active Directory actually provides is not storage. It provides trust. When a workstation authenticates a user through Kerberos, it is trusting the Key Distribution Center's (KDC) assertion that the presented credential is indeed legitimate and validated. When a service grants access based on group membership, it is trusting the directory's representation of that membership. When a federal system accepts a PIV card authentication, it is trusting a chain of certificate authority relationships that ultimately routes back to the Federal Common Policy Certificate Authority (FCPCA). None of those trust decisions are made by the directory alone. They are made by a distributed system of components - directory, Certificate Authority (CA), federation service, cloud identity platform, privileged access infrastructure - in which the directory is one critical participant.



Understanding Active Directory as a trust system, rather than merely as a directory service, changes what a defender monitors, what an assessor evaluates, and what an adversary targets.



1.1.2 THE DIFFERENCE BETWEEN A DOMAIN AND AN IDENTITY TRUST SYSTEM



A domain is a technical boundary: an administrative container, a Kerberos realm, a replication scope. It has real security properties. Domain Controllers (DCs) enforce authentication. Group Policy Objects (GPOs) configure member systems. Trust relationships with other domains are negotiated and mutually governed. These are meaningful boundaries.



But a domain is not an identity trust system.



The identity trust system is larger than any domain by itself. It includes the Certificate Authorities (CAs) that issue credentials the domain accepts. It includes the Active Directory Federation Services (AD FS) that broker cross-boundary assertions. It includes the cloud identity platforms synchronized to on-premises Active Directory through a service accounts with domain replication-equivalent permissions. It includes the mission partners who authenticate through federation agreements and whose trust extends into systems the domain itself does not exclusively control. It includes the authoritative attribute sources - personnel records, clearance databases, role registries - whose data flows into the directory and determines what access each identity can request.



An adversary who understands only the domain misses most of the attack surface. A defender who monitors only the domain misses most of the telemetry. This book's unit of analysis is the identity trust system, not the domain.



1.1.3 WHY THE DOMAIN IS A REAL SECURITY BOUNDARY, BUT NOT THE ONLY ONE



Clarifying the distinction between domain and identity trust system is not an argument that the domain is unimportant. It very much is.



Domain controllers are Tier 0 infrastructure. The `NTDS.dit` database is the authoritative credential store for every account in the domain. The `krbtgt` account's key material is the master trust anchor for all Kerberos authentication in the domain. These facts do not diminish in importance because the identity trust system is larger - they become more important when you recognize that the domain is the authoritative source from which much of the broader trust system derives its assertions.



The point is precision: the domain boundary is a real and important security boundary, but it is not the outermost boundary of the identity trust system. Figure 1-2 shows this distinction visually - the domain and forest boundary nested within the larger identity trust system boundary. A defender who treats it as the outermost boundary will miss attack pathways that begin outside the domain or that use the domain only as a pivot to reach targets in federated, cloud, or mission-partner environments.



1.1.4 HOW TRUST EXTENDS THROUGH FORESTS, DOMAINS, CERTIFICATES, FEDERATION, CLOUD IDENTITY, AND MISSION PARTNERS



Trust in Active Directory environments does not stop at the domain or even at the forest boundary.



Figure 1-1 illustrates the full identity trust system, with the domain at the center and the trust-extending components - certificate authorities, federation services, cloud identity platforms, and mission-partner relationships - surrounding it. It extends outward through multiple channels simultaneously.



Forest trusts carry Kerberos authentication across forest boundaries, governed by Security Identifier (SID) filtering and trust direction. Certificate trust extends to any system that accepts certificates issued by an authority in the Federal Public Key Infrastructure (FPKI). Federation trust reaches Relying Party (RP) applications that accept assertions from an Active Director Federation Services (AD FS) deployment - potentially including systems in other agencies, cloud environments, or mission-partner networks. Cloud identity trust extends from on-premises Active Directory through Microsoft Entra Connect synchronization into cloud tenants where separate governance and administrative roles apply.



Each of these trust extension pathways is legitimate and operationally necessary.



Each is also an attack surface expander.



An adversary who compromises a token-signing key in an Active Directory Federation Services deployment does not need to attack any domain controller directly - the token-signing key provides the ability to generate assertions accepted by every relying party in the federation.



An adversary who compromises a Managed Service Account (MSA) with excessive Entra ID permissions does not need to traverse the on-premises forest - the cloud elevation is already available.



The identity trust system's reach determines the reach of any compromise within it.



1.1.5 WHY IDENTITY TRUST BECOMES MISSION INFRASTRUCTURE IN FEDERAL AND MILITARY ENVIRONMENTS



In a commercial organization, a domain compromise is an Information Technology (IT) crisis. In a federal or military environment, it can become a mission catastrophic crisis that may carry abilities to threaten national security or the well-being of society as a whole.



Federal identity infrastructure is not separable from mission capability in the way that a commercial company's IT systems are separable from its products.



When the authentication infrastructure that validates who can access mission-critical systems is compromised, the agency loses the ability to determine who is authorized, which systems are being accessed legitimately, which administrative actions are clean, and which recovery operations are genuinely safe to execute. That loss of authoritative identity is not a technical problem that carries a technical solution. It is a complete trust collapse that affects mission execution and demands immediate investigation and remediation.



This distinction shapes everything about how identity security must be approached in federal and defense environments. Controls must be engineered not just to prevent attacks but to preserve the ability operate under adversarial conditions. Detection must be designed not just to alert but to produce the evidence and artifact chain required for high-level authorization and recovery decisions.



Recovery must be planned not just for technical restoration, but for the restoration of trusted identity - which is a different and harder problem to tackle.



1.1.6 WHY IDENTITY FAILURE BECOMES MISSION RISK



The governing proposition of this book, stated plainly: **identity failure in federal and military environments is mission risk, not just IT risk.**



When an adversary controls the directory's trusted core, they control who the agency believes is authorized. They can manufacture credentials. They can create endless sessions that appear legitimate. They can grant themselves administrative authority of the highest paramount and that monitoring will interpret as normal. They can do this quietly, persistently, and in ways the leave clean-looking artifacts contained within the logs.



The mission operates on the basis of identity decisions the agency is blindly trusting, and can no longer trust.



That is the problem this book teaches readers to understand, prevent, detect, contain, and recover from.



1.2 WHY ACTIVE DIRECTORY REMAINS CENTRAL TO FEDERAL AND MILITARY ENVIRONMENTS



Before this book argues about why Active Directory security is a mission problem, it should first establish why Active Directory remains the relevant subject. The answer is not simply that it is ubiquitous, though it is. The answer is that it provides capabilities that no current alternative provides at equivalent scale, with equivalent integration depth, for the environments this book serves.



1.2.1 ACTIVE DIRECTORY AS THE OPERATIONAL MAINSTAY OF ENTERPRISE IDENTITY



Active Directory Domain Services (AD DS), commonly referred to as Active Directory (AD), did not emerge into an empty market. Before Microsoft established AD as the predominant identity architecture for Windows enterprise networks, directory services were already at the center of a broader contest over who would control enterprise authentication, authorization, resource discovery, and administrative policy.



Understanding that history is important because many of Active Directory's present-day strengths, limitations, and security assumptions are products of the environment in which it was designed. Ad was created to solve the management and scalability problems of the 1990s. It was not originally designed for today's threat landscape, in which credential theft, remote access, hybrid identity, ransomware, cloud federation, and identity-based lateral movement are routine operational concerns that keep defender's up at night.



1.2.1.1 THE ENTERPRISE DIRECTORY CONTEST



Before Active Directory, many enterprise networks relied on Novell NetWare and Novell Directory Services (NDS). NDS represented a major architectural advance over the server-specific account databases and bindery structures that preceded it. It organized users, systems, groups, and resources within a hierarchical directory tree and provided centralized administration across large, distributed networks. NDS later evolved into Novell eDirectory, a scalable, cross-platform directory that supported X.500 and Lightweight Directory Access protocol (LDAP) standards.



Microsoft's Windows NT domain architecture was more constrained. Windows NT 4.0 relied on a domain-centric account model in which a Primary Domain Controller (PDC) maintained the authoritative domain account database and Backup Domain Controllers (BDCs) received replicated copies. This architecture centralized account administration within a domain, but it did not provide the hierarchical forest, organizational unit, multidomain replication, or policy architecture that would later define Active Directory.



As enterprises expanded, acquired other companies, opened remote offices, and deployed larger numbers of Windows systems, the limitations of flat domain structures became increasingly difficult to manage. Microsoft needed a directory service that was capable of supporting distributed authentication, hierarchical administration, delegated authority, policy-based configuration, and interoperability with emerging Internet standards.



1.2.1.2 THE ORIGINS OF ACTIVE DIRECTORY



Active Directory inherited important architectural concepts and engineering work from the Microsoft Exchange Directory Service. Microsoft has described Active Directory as a direct descendant of the Exchange directory, although the resulting Windows directory became a substantially broader platform for identity, authentication, authorization, replication, policy, and resource management.



Rather than implementing the complete X.500 directory stack as originally defined, Microsoft developed a directory influenced by the X.500 information model and accessible through LDAP. It integrated that directory with Kerberos authentication, Domain Name System (DNS) service location, Windows security identifiers, access control lists, replication, and Group Policy.



Active Directory became generally available with the initial release of Microsoft's Windows 2000 Server on February 17, 2000. It replaced the limitations of the Windows NT domain model with a logical architecture consisting of forests, domains, trees, organizational units, sites, trusts, schemas, global catalogs, and multi-master domain controller replication. Microsoft presented Active Directory as a central component of Windows 2000's policy-based and distributed management architecture.



This was not an improvement to the Windows logon process. It was a fundamental redesign of how Windows enterprises identified security principals, located services, assigned permissions, distributed security policy, and administered systems at scale.



1.2.1.3 HOW MICROSOFT PREVAILED



The outcome of the enterprise directory contest cannot be attributed solely to the technical capabilities of either NDS or Active Directory. NDS was already mature, hierarchical, scalable, and cross-platform. Microsoft's decisive advantage was its ability to integrate Active Directory directly into the Windows Server platform and connect it to the rapidly expanding ecosystem of Windows workstations, servers, applications, and Exchange deployments.



Active Directory was not positioned as an isolated directory product that administrators had to purchase and integrate separately. It became part of the Windows Server operating model. DNS service discovery, Kerberos authentication, LDAP directory access, Windows security identifiers, Group Policy, domain membership, and application integration were designed to operate as components of the same administrative ecosystem.



Microsoft also benefited from application gravity. As enterprises standardized on Windows desktops, Windows Server, Microsoft Office, and Exchange, Active Directory became the natural location for user accounts, computer accounts, security groups, application identities, and administrative policy. Software vendors increasingly designed their products to authenticate against or store configuration information in AD. The more systems that depended on the directory, the more difficult it became to replace.



NetWare's market position consequently declined, although NDS continued to evolve as a separate cross-platform directory product. Active Directory prevailed not because every component was categorically superior, but because Microsoft made the directory inseparable form the broader Windows enterprise platform.



1.2.1.4 THE MODERN OPERATIONAL REALITY



More than twenty-five years after its initial release, Active Directory remains a mature distributed service used as a backend by numerous Microsoft and third-party products. In the federal, Department of Defense (DoD), and critical-infrastructure environments addressed by this book, AD commonly intersects with identity governance, endpoint administration, certificate services, federation, privileged access, application authentication, and hybrid-cloud identity.



Decades of mission and business infrastructure have been constructed around that dependency.



Enterprise certification authorities may use AD DS to publish certificate templates, enrollment information, revocation data, and public key infrastructure objects.



Group Policy Objects (GPOs) use Active Directory and the System Volume (`SYSVOL`) to distribute configuration and security policy.



Privileged roles derive authority from directory group memberships, delegated permissions, access control entries, user rights assignments, and control over trusted systems.



Kerberos authentication depends on domain controllers operating as Key Distribution Centers (KDCs).



Federation services frequently use AD identities and attributes to issue claims to external applications and relying parties.



Hybrid identity services may synchronize users, groups, password-derived information, and other identity attributes from on-premises AD DS into cloud identity platforms.



Applications use LDAP, Kerberos, NT LAN Manager (NTLM), group membership, Service Principal Names (SPNs), and directory attributes to authenticate users and authorized access.



The result is accumulated dependency. Active Directory is no longer one identity product among many. In environments built around it, AD is woven through the technical and administrative fabric of the mission.



1.2.1.5 ACTIVE DIRECTORY AS AN ADVERSARY OBJECTIVE



The same concentration of identity and administrative authority that makes Active Directory operationally valuable also makes it a high-value adversary objective.



Threat actors enumerate Active Directory to discover an identify users, groups, computers, services, trusts, delegated permissions, certificate services, and pathways to privileged access. They target domain credentials to expand access, move laterally, compromise servers, reach sensitive data, and prepare disruptive operations. State-sponsored actors and ransomware operators have been observed extracting the Active Directory database, `NTDS.dit`, to obtain credential material and establish domain-wide control.



It is important to note that Active Directory does not contain just the accounts listed above. It records relationships of authority. It tells an adversary which users administer which systems, which service accounts possess elevated rights, which computers host valuable services, which trusts connect security environments or that lead straight to DA, and which permissions create a route toward Tier 0 infrastructure.



Once an attacker acquires sufficient authority, the directory can become an attack-distribution and persistence platform. The adversary may manipulate group membership, directory permissions, GPOs, service accounts, authentication policy, certificate enrollment, or replication rights. At that point, the attacker is no longer operating only inside the environment. The attacker may be able to change the rules by which the environment decides who and what should be trusted.



1.2.1.6 DOMAIN AND FOREST SECURITY BOUNDARIES



This distinction is critical: an Active Directory domain is an authentication, replication, and administrative boundary, but it is not an independent security boundary within a forest. Microsoft identifies the forest - not the individual domain - as the Active Directory security boundary. Domains within the same forest share the schema, configuration partition, global catalog infrastructure, and transitive trust relationships.



Compromise of one domain does not necessarily and automatically prove that every domain in the forest has been compromised; however, it may create viable pathways toward forest-wide control, especially where privileged credentials are reused, administrative tiers overlap, delegation is excessive, domain controllers share infrastructure, or cross-domain permissions are poorly governed.



A misconfiguration is not guaranteed to produce immediate forest compromise. It can, however, create a control pathway through which an attacker moves from an ordinary user, workstation, service account, application server, or subordinate domain toward domain-level or forest-level authority.



Zero Trust Architecture (ZTA) does not eliminate this problem, either. Zero Trust principles require explicit verification, principle of least privilege, separation of duties, resource-centered authorization, continuous evaluation, and an assumption that network location does not establish trust. Those principles must be applied to Active Directory rather than used as a reason to ignore it. A cloud identity platform or Zero Trust policy layer cannot compensate for an on-premises directory whose privileged groups, domain controllers, certificate services, service accounts, or administrative pathways remain exposed.



1.2.1.7 WHY ACTIVE DIRECTORY PERSISTS



Replacing Active Directory is not simply a matter of installing a newer directory product. Complete replacement may require an agency or command to redesign:



User and computer authentication

Application authorization

Service account dependencies

Group-based access models

Kerberos and LDAP integrations

Certificate enrollment and account mapping

Group Policy and endpoint configuration

Administrative delegation

Domain and forest trusts

Federation services

Cloud synchronization

Audit and governance processes

Recovery procedures

Mission applications built around Windows-integrated authentication



Each integration must be identified, re-engineered, tested, accredited, migrated, and maintained without disrupting critical mission operations. In large federal and defense environments, this work can span multiple acquisition, modernization, and authorization cycles.



Some environments will reduce their dependency on AD. Some will adopt cloud-native identity for specific applications or user populations. Many will operate hybrid architectures for years. During that transition, the original directory does not become less important because a second identity control plane has been introduced. In many cases, hybrid integration increases the number of trust relationships that defenders must understand through and through.



Active Directory must therefore be defended as it exists: a mature, deeply integrated, high-consequence identity system whose compromise can affect nearly every resource that relies on it.



1.2.3 ACTIVE DIRECTORY AS THE CONTROL PLANE FOR USERS, COMPUTERS, GROUPS, SERVICES, AND POLICIES



Active Directory is frequently described as an authentication service - a digital strongarm that checks credentials and permits or denies access. Authentication is one of its core functions, but that description captures only a fraction of its true operational role.



Active Directory Domain Services (AD DS) functions as an identity, authorization, and administrative control plane for Windows domain environments. It stores and replicates information about security principals and resources, participates in authentication, supplies authorization data, distributes administrative policy, supports service discovery, and defines relationships of trust. Microsoft describes AD DS as a hierarchical directory containing objects such as user accounts, computer accounts, servers, printers, services, and shared resources.



AD is not literally the operating system of the enterprise network. Network devices, cloud services, local accounts, standalone systems, operational technology, and non-Windows applications may maintain separate control planes. Nevertheless, in a Windows-centered environment, AD often determines who may administer those systems, which credentials applications accept, which policies endpoints receive, and which identities can access mission resources.



1.2.3.1 THE OBJECTS UNDER DIRECTORY CONTROL



Domain users, computers, groups, managed service accounts, service connection points, organizational units, Group Policy metadata, certificate-related objects, and numerous application-defined objects are stored within the Active Directory database.



On a writable domain controller, this database is maintained in the `NTDS.dit` file. Each writable domain controller holds a replica of the directory partition for its domain, while Read-Only Domain Controllers maintain read-only copies subject to replication and credential-caching restrictions. Changes made to directory objects are replicated between applicable domain controllers.



This does not mean that every Windows identity exists in `NTDS.dit`. Local accounts are maintained in the Security Accounts Manager database of the individual computer. Cloud-native identities may exist only within a cloud identity provider. External users may authenticate through federation or other identity systems. The `NTDS.dit` database specifically contains the directory objects and credential-related information managed by that Active Directory domain.



Computer accounts allow domain controllers and other systems to authenticate domain-joined computers. Security groups collect users, computers, service accounts, and other groups into authorization structures. Service accounts provide identities under which applications, scheduled tasks, services, databases, and automated processes operate. Organizational units provide administrative scope for delegation and policy application.



These objects are not passive records. They form relationships that determine access and control.



A user may control a server because of group membership.



A group may control an organizational unit because of a delegated access control entry.



A service account may control an application because it owns the service process and its data.



A computer account may possess rights to retrieve managed passwords or access another system.



An administrator may control thousands of endpoints because the administrator can modify a GPO linked to their organizational units.



The security of the environment depends not only on which objects exist, but also on the relationships between them.



1.2.3.2 THE POWER OF DISTRIBUTED CONFIGURATION AUTHORITY



Group Policy is one of Active Directory’s most powerful administrative mechanisms, but it is not the sole mechanism through which AD exercises control.



A Group Policy Object contains configuration settings that can be applied to users and computers according to their placement within Active Directory sites, domains, and organizational units. Security filtering, inheritance, enforcement, loopback processing, Windows Management Instrumentation filtering, and link order further determine where and how a GPO applies.



GPO metadata is stored in Active Directory, while the associated policy files are maintained within SYSVOL and replicated between domain controllers. Both components must remain available and consistent for normal Group Policy processing.



Through Group Policy, authorized administrators can centrally configure:



Windows Firewall rules

Audit policy

User rights assignments

Security options

Account and lockout settings

Local group membership

Logon and startup scripts

Application control policies

Microsoft Defender settings

Certificate autoenrollment

Administrative templates and registry-based policy

Remote access restrictions

Credential and authentication protections

Windows Update behavior

Software deployment in supported scenarios



Microsoft documents the use of domain GPOs to distribute security baselines, audit settings, domain controller hardening, firewall configuration, user rights, and other security controls.



Group Policy does not automatically govern every device in the enterprise, nor is it a complete endpoint-management or patch-management platform. A GPO applies only where the client supports the relevant policy, falls within its processing scope, can contact the required domain infrastructure, and successfully processes the policy. Other technologies may be responsible for software distribution, vulnerability remediation, mobile device management, configuration compliance, or cloud workload governance.



Nevertheless, the ability to alter a widely linked GPO may provide control over large numbers of users and computers. That makes GPO creation, modification, linking, ownership, and delegation Tier 0 concerns whenever the affected policy can influence privileged accounts, domain controllers, administrative workstations, identity infrastructure, or other critical systems.



1.2.3.3 AUTHORITY BEYOND GROUP POLICY



The Active Directory control plane extends beyond GPOs. Administrative authority is also created and enforced through:



Security group membership

Nested group relationships

Directory access control lists

Object ownership

Delegated permissions

Kerberos ticket issuance

Privilege information contained in authorization data

User rights assignments

Authentication policies and silos

Domain and forest trusts

Service principal names

Password and account policies

Replication permissions

Certificate enrollment permissions

Domain Name System records and service discovery

Control of domain controllers and administrative infrastructure



An identity does not need to be a direct member of Domain Admins to possess domain-impacting authority. A principal may obtain equivalent control by modifying a privileged group, resetting a privileged account’s password, editing a sensitive GPO, controlling a service executed on a domain controller, changing an object’s permissions, granting directory replication rights, or compromising a system from which privileged administrators operate.



Effective privilege is therefore determined by control relationships, not merely by the visible contents of well-known administrative groups.



1.2.3.4 WEAPONIZING THE CONTROL PLANE



When an adversary gains sufficient control over Active Directory, the compromise is no longer limited to credential validation. The attacker may be able to use the agency’s own identity and administrative infrastructure to expand access, distribute changes, establish persistence, and undermine defensive controls.



Depending on the permissions obtained and the protections present, a compromised AD control plane may allow an attacker to:



Add controlled identities to privileged groups

Create new administrative accounts

Reset passwords or change authentication attributes

Modify directory access control lists

Grant replication rights used for DCSync

Alter GPOs to execute scripts, scheduled tasks, or malicious software

Change firewall, audit, logging, or endpoint-security policy

Weaken authentication requirements

Manipulate service accounts or service principal names

Create or modify delegation relationships

Abuse certificate enrollment and certificate authority permissions

Establish persistence through directory objects or permissions

Access systems that trust compromised Kerberos tickets or credentials

Conceal activity by modifying security settings or disrupting telemetry



An attacker with GPO modification rights may attempt to deploy a payload, create a scheduled task, alter local group membership, disable logging, or weaken endpoint defenses across the scope of that policy. This does not guarantee the successful bypass of Endpoint Detection and Response (EDR) controls. Tamper protection, policy enforcement, application control, network segmentation, local protections, and independent monitoring may prevent or detect the change. The critical issue is that Active Directory can provide a centralized mechanism through which the attacker attempts the action at scale.



Service accounts create another significant path. Because services frequently operate continuously and may possess broad access to files, databases, applications, remote systems, or administrative interfaces, compromise of a highly privileged service account can support lateral movement and persistence. The resulting activity may appear consistent with legitimate system operations because the identity is already expected to authenticate between systems.



1.2.3.5 WHY CONTROL-PLANE COMPROMISE IS DIFFERENT



An Active Directory compromise is fundamentally different from an incident confined to an individual application or endpoint because AD supplies trust and administrative authority to other systems.



This does not mean that a workstation compromise is automatically contained. A compromised workstation can expose credentials, sessions, tokens, administrative tools, browser data, or network access that allows an attacker to progress toward the directory. An endpoint may be the initial foothold from which a much larger identity compromise develops.



The distinction lies in the level of authority obtained.



An endpoint compromise initially affects the integrity of that endpoint and any credentials or resources accessible from it.



A domain compromise affects the integrity of domain identities, authentication decisions, administrative groups, policies, and domain-managed resources.



A forest compromise affects the highest Active Directory security boundary and may undermine trust across every domain within that forest.



If an attacker obtains privileged access to a domain controller, Microsoft warns that the attacker can modify, corrupt, or destroy the AD DS database and potentially threaten every account and system managed by the directory. Microsoft further states that after a domain controller compromise, the forest cannot be considered trustworthy unless it is recovered from known-good data and the original paths of compromise are closed.



At that level, ordinary endpoint remediation is insufficient. Reimaging one workstation, deleting one malware binary, or resetting one password does not restore confidence in:



Privileged group membership

Directory permissions

Kerberos secrets

Service account credentials

Group Policy integrity

Certificate-based authentication

Replication rights

Trust configuration

Administrative workstations

Domain controller integrity

Security logs and monitoring configuration



The response must determine whether the adversary merely used Active Directory credentials or obtained the ability to change Active Directory itself. That distinction drives the difference between account containment, domain remediation, and complete forest recovery.



1.2.3.6 THE DIRECTORY AS BOTH INFRASTRUCTURE AND WEAPON



Active Directory is valuable because it centralizes identity and administration. That same centralization creates strategic risk.



Defenders use AD to distribute policy, authenticate users, delegate administration, enforce access, and operate the enterprise.



Attackers seek AD because the directory can provide the same capabilities for hostile purposes.



The directory can tell the defender who should have access.



It can also tell the attacker whose access should be stolen.



It can allow the defender to configure thousands of systems.



It can also allow an attacker with sufficient authority to manipulate those systems at scale.



It can provide the foundation for secure authentication.



It can also provide forged or stolen identities with access to every system that continues to trust the compromised control plane.



For this reason, Active Directory must not be treated as an ordinary application service. It is critical identity infrastructure. Its privileged groups, domain controllers, administrative workstations, service accounts, Group Policy infrastructure, certificate services, federation systems, virtualization platforms, and recovery assets form a connected trust system.



Defending only the directory database is not enough. The entire control path to the directory must be protected.



1.2.4 ACTIVE DIRECTORY'S ROLE IN PRIVILEGED ACCESS AND ADMINISTRATIVE AUTHORITY



Active Directory Domain Services (AD DS) functions as the primary authority plane for privileged access across a Windows domain and forest. It determines which identities can administer domain controllers, modify directory objects, alter security policy, manage authentication infrastructure, and exercise control over other users, computers, services, and administrative groups. In this role, Active Directory does more than store accounts. It defines who holds administrative authority, where that authority applies, and how it is inherited, delegated, or constrained.



The most sensitive forms of authority are concentrated in highly privileged groups and protected by security principals. These include Domain Admins (DA), Enterprise Admins (EA), Schema Admins, the built-in Administrators group, Enterprise Key Admins, Key Admins, and other identities granted equivalent rights through delegated permissions, Access Control Entries (ACEs), or control of privileged systems. Membership in a well-known administrative group is therefore only one indicator of privilege. An identity may possess equivalent or greater control through nested group membership, Discretionary Access Control List (DACL) permissions, Group Policy ownership, directory replication rights, certificate authority administration, service account control, or the ability to modify another privileged identity.



The Protected Users group serves a different purpose altogether. Instead, it applies additional authentication protections to selected accounts by restricting the use of weaker credential and authentication mechanisms. Privileged accounts may be added to Protected Users as part of a broader hardening strategy, but membership alone does not make an account privileged.



Modern privileged-access architectures depend heavily on Active Directory to establish and preserve administrative separation. Tier 0 models, dedicated administrative forests, Privileged Access Workstations (PAWs), authentication silos, and restricted administrative groups all rely on directory-based controls to define trusted identities and enforce where those identities may operate. Their effectiveness, however, also depends on supporting safeguards such as endpoint hardening, network segmentation, secure administrative protocols, certificate protection, multifactor authentication, monitoring, and disciplined account lifecycle management.



Within Active Directory, privileged authority is primarily established and enforced through several interconnected mechanisms:



1. **Security principal and group membership:** Determines which users, computers, managed service accounts, and groups receive administrative rights directly or through nested relationships.

2. Directory permissions and delegation: Access control lists define who may create, modify, delete, or take ownership of directory objects, including users, groups, Organizational Units (OUs), Group Policy Objects (GPOs), and domain-level configuration.

3. Group Policy enforcement: Group Policy Objects (GPOs) apply security settings, user rights assignments, authentication restrictions, local group membership, software controls, and administrative workstation requirements across domain-joined managed systems.

4. Kerberos authentication and ticket issuance: The Key Distribution Center (KDC), operating on domain controllers, issues authentication tickets based on the identity, group membership, account state, and applicable authentication policy of the requesting security principal.

5. Domain and forest trust relationships: Trusts extend authentication and authorization decisions across security boundaries, allowing identities from one domain or forest to access resources within another when permissions and trust configuration permit it.

6. Domain replication and boundary control: Domain controllers replicate privileged identity data, group membership, password-derived secrets, policy configuration, and authorization information. An identity that can manipulate or replicate this data may effectively control the domain even without conventional administrative group membership.



Active Directory therefore represents both the foundation of administrative governance and one of the most consequential security boundaries in a Windows environment. When its privileged groups, delegated permissions, authentication services, or administrative systems are compromised, the result is rarely limited to a single account or endpoint. The compromise may give an adversary the ability to redefine authority itself, create persistent access, impersonate trusted identities, weaken established security controls, and extend control throughout the domain or forest.





***\*\*\****

***1.2.4.1 THE INSEPARABILITY OF DIRECTORY AND PRIVILEGE***



*Privileged-access security cannot be separated from Active Directory security in a Windows domain or forest. The two are not identical, but they are structurally interdependent.*



*Privileged-access security governs how elevated authority is assigned, exercised, constrained, monitored, and revoked, Directory security protects the identities, groups, permissions, authentication secrets, policies, and administrative relationships through which much of that authority is created. A privileged0access program may introduce separate safeguards such as Privileged Administrative Workstations (PAWs), Multi-Factor Authentication (MFA), password vaults, session monitoring, Just-In-Time (JIT) elevation, or approval workflows. Those safeguards can reduce risk, but they cannot compensate for a directory whose underlying authority relationships can be modified by an unauthorized principal.*



*Active Directory Domain Services (AD DS) determines much of the effective privilege within a domain through several interconnected mechanisms:*



* *Security group membership*
* *Nested group relationships*
* *Directory object ownership*
* *Discretionary Access Control Lists (DACLs)*
* *Access Control Entries (ACEs)*
* *Delegated administrative permissions*
* *Group Policy Object (GPO) ownership and modification rights*
* *Domain controller replication permissions*
* *Kerberos authentication secrets*
* *Service account control*
* *Trust configuration*
* *Certificate enrollment and certificate authority permissions*



*Each Active Directory object is protected by a security descriptor containing access control information that identifies which security principals may read, modify, delete, take ownership of, or otherwise control that object. Active Directory delegation is implemented by granting specific rights through ACEs contained within an object's Access Control List (ACL).*



*The relationship between directory control and privileged authority can be represented as follows:*



*\[Active Directory Identity and Control Plane] │ ├── Modify privileged group membership │ └──► Domain, forest, or Tier 0 authority │ ├── Modify object ownership, DACLs, or ACEs │ └──► Delegated control paths and persistence │ ├── Modify privileged accounts or authentication attributes │ └──► Account takeover or impersonation │ ├── Abuse directory replication permissions │ └──► DCSync retrieval of credential material │ └── Compromise the KRBTGT account secret └──► Forged Kerberos Ticket-Granting Tickets and Golden Ticket attacks*



*This diagram illustrates several distinct forms of compromise. They should not be treated as interchangeable.*



*The ability to modify a privileged group produces administrative authority through a legitimate authorization mechanism. The ability to rewrite an ACL creates control over the protected object and may establish an indirect pathway to higher privilege. DCSync abuses directory replication permissions to request password-derived credential material from a domain controller. A Golden Ticket attack requires possession of the `krbtgt` account secret, which allows an adversary to forge Kerberos Ticket Granting Tickets (TGTs).*



*Exposure of the directory database and unauthorized modification of the directory also create different risks.*



*If an adversary exfiltrates the Active Directory database, `NTDS.dit`, together with the cryptographic material required to decrypt protected secrets, the adversary may be able to extract password hashes and other credential material for offline use. The attacker does not necessarily receive immediate write access to the live directory, but the exposed credentials may enable impersonation, privilege escalation, lateral movement, and later domain compromise. MITRE ATT\&CK classifies the extraction of credential material from `NTDS.dit` as Operating System Credential Dumping.*



*If an adversary obtains administrative control of a domain controller, the consequences are more direct. Domain controllers can read and write directory information, participate in authentication, replicate credential data, and distribute authoritative changes to other domain controllers. Microsoft states that after a domain controller compromise, the Active Directory forest cannot be considered trustworthy unless it is recovered from a known-good data and the pathways that enabled the compromise are completely closed.*



*Identity security is therefore not limited to creating accounts, resetting passwords, unlocking users, or disabling identities. Those are identity-administration functions. Directory security must also preserve the integrity of the objects, permissions, secrets, policies, replication mechanisms, and control relationships that determine what each identity is authorized to do.*



*A credential can be perfectly protected while the account remains vulnerable through a delegated password-reset right.*



*A privileged group can be carefully monitored while an overlooked ACL allows an unprivileged principal to modify its membership.*



*A domain administrator's password can remain unknown to the attacker while the attacker controls the administrator's account object, workstation, authentication certificate, service dependency, or group membership.*



*The central security question is therefore not limited to who possesses a privileged credential. The more important question at hand is:*



***Who can create, alter, impersonate, or regain privileged authority?***



***1.2.4.2 THE MANUFACTURE OF ILLEGITIMATE AUTHORITY***



*Active Directory does not distinguish between a legitimate administrative change and a malicious change based on the operator's intent. It evaluates whether the requesting security principal possesses the required rights.*



*An adversary who acquires permissions to modify directory objects, reset passwords, alter ACLs, or change privileged group membership may be able to manufacture administrative authority without obtaining an existing administrator's password.*



*For example, an attacker who controls the membership attribute of the Domain Admins group may add an attacker-controlled account to that group. Once the change has replicated and the account obtains a new access token or Kerberos ticket containing the updated authorization information, the account may exercise the rights associated with its new membership.*



*The attacker has not bypassed the authorization model. The attacker has subverted the mechanism that defines the authorization model.*



*Equivalent escalation pathways can arise when an adversary is able to:*



* *Reset the password of a privileged account*
* *Modify the credentials associated with an account*
* *Change the owner of a privileged directory object*
* *Add an ACE granting control over a protected object*
* *Modify a GPO applied to domain controllers or administrative systems*
* *Alter a service account used by a privileged application*
* *Register or modify a Service Principal Name (SPN)*
* *Change Kerberos delegation settings*
* *Grant directory replication permissions*
* *Modify certificate templates or enrollment permissions*
* *Alter attributes synchronized to a cloud identity platform*
* *Take control of a workstation used by privileged administrators*



*These pathways demonstrate why administrative authority cannot be measured solely by enumerating members of Domain Admins, Enterprise Admins, or other well-known groups. Effective privilege includes every direct and indirect control relationship through which a principal can influence a privileged identity, system, policy, or secret.*



***1.2.4.3 DCSYNC AND THE ACQUISITION OF CREDENTIAL AUTHORITY***



*A DCSync attack does not modify the Active Directory database by itself. Instead, it abuses the directory replication protocol.*



*A principal with the necessary replication permissions can impersonate the behavior of a domain controller and request replicated account data from another domain controller. This may expose password hashes and other credential material, including the secret associated with the `krbtgt` account. MITRE ATT\&CK classifies DCSync as the `T1003.006` sub-technique of Operating System Credential Dumping.*



*DCSync is therefore best understood as a credential-acquisition mechanism enabled by excessive or compromised directory replication authority.*



*The attack does not eliminate authentication. It obtains material that may later be used to impersonate accounts, authenticate with stolen password hashes, crack passwords offline, or forge Kerberos tickets.*



***1.2.4.4 GOLDEN TICKETS AND FORGED AUTHENTICATION AUTHORITY***



*The `krbtgt` account is used by the Kerberos Key Distribution Center (KDC) to protect domain TGTs. If an adversary obtains the relevant `krbtgt` secret, the attacker may generate forged TGTs known as Golden Tickets.*



*A forged TGT can contain manipulated identity and authorization information. The adversary may claim membership in privilege groups and request access to Kerberos-protected services as a chosen domain identity. Because the ticket appears to be protected with a valid domain secret, systems relying on Kerberos may accept it unless other controls detect or prevent its use.*



*Golden Tickets do not bypass every security control in the enterprise. They apply to the affected Active Directory domain and to resources that trust that domain's Kerberos authentication. Application-specific authorization, network segmentation, certificate requirements, cloud-native controls, device compliance, and other independent controls may still restrict access.*



*Golden Tickets are also not inherently undetectable. Detection may be difficult, particularly when forged tickets imitate normal ticketing properties, but defenders can identify anomalies involving ticket lifetimes, encryption types, account behaviors, authorization data, logon events, and Ticket Granting Service (TGS) requests that lack expected preceding authentication activity.*



*The persistence is likewise not permanent. Proper incident response can invalidate forged tickets by resetting the `krbtgt` password twice, allowing replication to complete between resets, remediating compromised accounts and domain controllers, and closing the original control pathway.*



*The danger lies in the adversary's ability to convert compromised directory authority into new authentication material that appears legitimate to systems still trusting the affected domain.*



***1.2.4.5 THE DUAL NATURE OF THE DIRECTORY***



*Active Directory is a dual-use administrative platform.*



*Defenders use it to create accounts, assign permissions, distribute policy, authenticate systems, delegate administration, and enforce operational standards.*



*Adversaries target the same mechanisms to create accounts, grant permissions, distribute malicious configuration, impersonate users, establish persistence, and weaken security controls.*



*This does not make Active Directory the sole source of administrative privilege across the entire enterprise. Local accounts, cloud roles, application permissions, virtualization platforms, network-management systems, public key infrastructure, and operational technology may each maintain separate forms of authority.*



*Within an Active Directory domain, however, AD DS is the central authority for domain identities, groups, Kerberos authentication, directory permissions, and domain-based administrative delegation. Its control relationships frequently extend into other systems that trust domain identities or groups.*



*This dual-use property is broader than Living Off the Land (LoTL).*



*Living Off the Land generally describes an adversary's use of legitimate administrative tools, binaries, scripts, protocols, or other administrative capabilities already present in the environment. An attacker might use PowerShell, Windows Management Instrumentation (WMI), Remote Service Management, Group Policy, native directory-management tools, or other approved utilities that are signed and trusted by Microsoft and other reputable vendors to perform malicious activity.*



*Not every Active Directory attack is a LoTL technique. Golden Ticket creation normally requires specialized capabilities to forge Kerberos tickets. DCSync requires implementation of the directory replication protocol; however, the authority being abused is often legitimate authority that the environment was designed to honor.*



*The problem is not that Active Directory contains malicious functions. The problem is that its legitimate functions become malicious when exercised by an unauthorized or compromised principal.*



*Defending the directory therefore requires more than blocking known attack tools and vectors. It requires defenders to:*



* *Protect the control pathways that grant administrative authority*
* *Restrict who can modify privileged groups and objects in the domain*
* *Review delegated permissions and ACL inheritance*
* *Secure domain controllers and administrative workstations (or Tier 0 assets)*
* *Protect replication permissions*
* *Monitor changes to privileged identities and policies*
* *Reduce standing administrative access*
* *Separate administrative and standard user identities*
* *Protect Kerberos, service account, and certificate secrets*
* *Detect abnormal use of legitimate administrative mechanisms*
* *Maintain tested domain and forest recovery procedures and run through them periodically to ensure their efficiency*



*The directory is not inherently the adversary's playground. It becomes on when the adversary gain control over the identities, permissions, systems, or secrets through which the directory operates.*



1.2.5 ACTIVE DIRECTORY'S ROLE IN HYBRID IDENTITY AND CLOUD TRUST



*Modern federal and defense environments rarely operate exclusively within isolated data centers or entirely within cloud-native platforms. Most maintain combinations of on-premises Active Directory, Microsoft Entra ID, cloud applications, federal credentialing systems, federation services, legacy mission applications, and externally managed identity providers.*



*These architectures are commonly described as hybrid identity environments. The term does not mean that Active Directory and Microsoft Entra ID become one unified directory. They remain separate identity and authorization systems connected through synchronization channels, provisioning, authentication, federation, certificate validation, and administrative workflows.*



*The security of the hybrid enterprise depends on understanding exactly what crosses those wires.*



***1.2.5.1 THE ILLUSION OF CLOUD ISOLATION***



*Moving an application or workload into the cloud does not automatically isolate it from on-premises identity compromise.*



*Isolation depends on how the cloud resource authenticates users, receives identity attributes, assigns roles, evaluates devices, and trusts external Identity Providers (IdPs). If cloud accounts, passwords, groups, authentication decisions, or authorization attributes remain derived form on-premises AD DS, then the cloud environment remains a material dependency on the on-premised control plane.*



*The opposite claim would also be inaccurate. On-premises Active Directory is not always the ultimate trust anchor for Microsoft Entra ID or cloud services. Cloud-only users, clout-native devices, workload identities, managed identities, cloud role assignments, and applications using independent identity providers may operate without an on-premises AD dependency.*



*The correct principal is narrower:*



***Cloud migration does not sever identity trust unless the identity dependencies themselves are redesigned or moved.***



*A hybrid identity architecture may contain several different connection models:*



***POSSIBLE HYBRID IDENTITY PATHWAYS DIAGRAM***


*\[On-Premises AD DS]*

&#x20;       *│*

&#x20;       *├── Object and attribute synchronization*

&#x20;       *│       └──► \[Microsoft Entra Connect or Entra Cloud Sync]*

&#x20;       *│                     └──► \[Microsoft Entra ID]*

&#x20;       *│*

&#x20;       *├── Password Hash Synchronization*

&#x20;       *│       └──► Hash-of-hash representation used for cloud authentication*

&#x20;       *│*

&#x20;       *├── Pass-through Authentication*

&#x20;       *│       └──► Cloud sign-in validated through on-premises agents*

&#x20;       *│*

&#x20;       *└── Federation*

&#x20;               *└──► \[AD FS or Third-Party Identity Provider]*

&#x20;                             *└──► Signed token accepted by cloud service*





*\[PIV / CAC / Enterprise or Federal PKI Certificate]*

&#x20;       *│*

&#x20;       *├──► AD FS certificate authentication*

&#x20;       *│         └──► Federated token*

&#x20;       *│*

&#x20;       *└──► Microsoft Entra Certificate-Based Authentication*

&#x20;                 *└──► Direct cloud authentication*



*These pathways are alternatives and may be combined differently by each agency or command. They should not be depicted as one mandatory architecture.*



***1.2.5.2 MICROSOFT ENTRA CONNECT AND DIRECTORY SYNCHRONIZATION***



*Microsoft Entra Connect Sync can synchronize selected users, groups, contacts, and attributes from on-premises AD DS into Microsoft Entra ID. Synchronized cloud objects may retain an on-premises source of authority for specific attributes, meaning that changes to those values must originate form the connected on-premises directory rather than from the cloud object itself.*



*Password Hash Synchronization (PHS) is an optional sign-in method. When enabled, Microsoft Entra Connect obtains the on-premises hash and performs additional processing before transmitting a resulting hash representation to Microsoft Entra ID over Transport Layer Security (TLS). Microsoft describes the synchronized value as a hash of the original Active Directory hash. The plaintext password is not transmitted or stored by the synchronization process.*



*Password synchronization is not present in every hybrid environment. Other sign-in architectures include Pass-through Authentication (PTA), federation, certificate0based authentication, or combinations designed for resilience and migration.*



*The Microsoft Entra Connect server is nevertheless a highly sensitive control-plane asset. Microsoft states that the server contains critical identity data and must be treated as a Tier 0 component. Compromise of the server or its administrative accounts may allow an attacker to manipulate synchronization, alter attribute flows, affect the source of authority for synchronized objects, or misuse connector permissions.*



*Microsoft Entra Cloud Sync introduces a different agent-based provisioning architecture but is provisioning agents are also treated as control-plane assets because they connect on-premises AD DS to the cloud identity service.*



***1.2.5.3 ACTIVE DIRECTORY FEDERATION SERVICES (AD FS)***



*Active Directory Federation Services (AD FS) provides federation capabilities by authenticating users and issuing signed security tokens containing identity and authorization claims.*



*In AD FS, federation means establishing a trust relationship between two separate security domains or agencies so users can log in once to access applications across organizational boundaries. To federate means to link separate identity and resource systems using a federated trust so that an external application trusts an agency's internal authentication without sharing user databases or passwords.*



***1.2.5.4 HOW FEDERATION WORKS***



*When an agency federates its systems using AD FS, it acts as an Identity Provider (IdP) that verifies a user's credentials against an on-premises directory. Instead of passing the actual password to an external or cloud application, the federation server generates a secure digital token containing signed claims about the user's identity. The external application or resource provider receives this token, checks its validity against the established trust, and grants access.*



*The AD FS token-signing certificate is therefore a critical trust asset. Its private key allows AD FS to prove that a token originated from the trusted federation service. Microsoft states that token-signing certificates protect against alteration or counterfeiting of security tokens.*



*If an adversary compromises the token-signing certificate or gains equivalent control over the federation service, the attacker may forge Security Assertion Markup Language (SAML) tokens. This technique is commonly called Golden SAML (pronounced as "SAH-MUL").*



*A forged SAML token can contain attacker-selected identity, attribute, permission, and lifetime claims. It may be accepted by services that trust the compromised federation issuer. MITRE ATT\&CK classifies this behavior as `T1606.002`, Forge Web Credentials: SAML Tokens.*



*Golden SAML does not automatically compromise every cloud service, tenant, or subscription. Its reach depends highly on a few factors listed below:*



* *Which relying parties trust the compromised issuer*
* *Which claims those relying parties accept*
* *How cloud and application roles are assigned*
* *Whether authorization is independently evaluated*
* *The audience and scope restrictions applied to the token*
* *Whether additional device, network, or workload controls exist*
* *Whether the forged activity is detected and contained*



*A forged token may bypass the normal authentication event, including authentication performed with Multi-Factor Authentication (MFA), because the relying party is validating a signed assertion rather than repeating the underlying authentication process. That possibility does not mean all MFA technologies or all cloud controls are universally bypassed. The effect depends on the federation and authorization design. CISA warns that an attacker who obtains an AD FS token-signing certificate may be able to forge tokens accepted by SAML-dependent services.*



***1.2.5.5 FEDERAL PKI, PIV, AND CAC AUTHENTICATION***



*Federal Public Key Infrastructure (FPKI), Personal Identity Verification (PIV), and Common Access Card (CAC) authentication must be represented separately from directory synchronization.*



*FPKI is not rooted in an agency’s on-premises Active Directory database. It is a federal certificate trust framework consisting of certificate authorities, policies, trust anchors, and validation mechanisms.*



*Active Directory may still participate in the authentication and authorization process. For example, an agency may:*



*Map a PIV or CAC certificate to an AD account*

*Use AD FS to authenticate a smart card user and issue a federated token*

*Publish certificate information or trust configuration through directory services*

*Use directory groups and attributes to authorize the authenticated user*

*Synchronize selected identity attributes into Microsoft Entra ID*



*Microsoft Entra Certificate-Based Authentication (CBA) also allows users to authenticate directly to Microsoft Entra ID with trusted X.509 certificates. This can remove the requirement to redirect the user to AD FS for certificate authentication.*



*Certificate authentication contains two separate decisions:*



*Whether the certificate is valid and chains to a trusted issuing authority.*

*Whether the certificate is correctly bound to the intended user account.*



*A valid certificate must not be treated as sufficient by itself. The platform must securely associate certificate fields with the correct identity and determine whether the certificate satisfies single-factor or multifactor authentication requirements.*



*Weak or mutable certificate-to-user bindings can create hybrid risk. Microsoft warns that where certificate username binding depends on synchronized attributes, an administrator who can modify the relevant on-premises attributes or synchronization mappings may affect how a certificate is associated with a Microsoft Entra identity. Microsoft recommends higher-affinity bindings to establish stronger assurance that a particular certificate belongs to a particular user.*



*A certificate-mapping weakness does not directly assign a cloud administrative role to a certificate. Role assignment remains a separate authorization function. However, if the mapping causes the certificate holder to authenticate as an already privileged cloud identity, the result may be privileged cloud access.*



***1.2.5.6 HOW ON-PREMISES COMPROMISE CAN REACH THE CLOUD***



*On-premises domain dominance can create several routes toward cloud compromise, but propagation is neither automatic nor unlimited.*



*Potential pathways include:*



*Resetting or controlling passwords for synchronized users*

*Modifying synchronized group membership*

*Altering attributes used for cloud authorization or certificate binding*

*Compromising the Microsoft Entra Connect server*

*Abusing synchronization connector permissions*

*Manipulating object-matching or source-of-authority behavior*

*Compromising PTA agents*

*Compromising AD FS servers or token-signing certificates*

*Taking over accounts that hold both on-premises and cloud privileges*

*Exploiting password reuse across control planes*

*Compromising administrators who manage both environments*

*Abusing writeback capabilities where those features are enabled*

*Modifying on-premises systems that cloud administrators use for privileged access*



*The overall damage impact depends on the architecture.*



*An agency using cloud-only privileged administrators, phishing-resistant authentication, separate administrative workstations, independent cloud role governance, managed authentication, and restricted synchronization may significantly reduce the ability of an on-premises compromise to reach the cloud.*



*An agency that synchronizes privileged accounts, federates all authentication through AD FS, allows the same administrators to control both environments, and operates its synchronization infrastructure as an ordinary member server may create a direct control path between the on-premises forest and the cloud tenant.*



*Hybrid identity security must therefore be evaluated as a graph of specific trust and control relationships, not as a general assumption that one environment always controls the other.*



***1.2.5.7** DEFENDING THE HYBRID ENTERPRISE*



*Securing cloud assets is not impossible when on-premises Active Directory is vulnerable. Cloud-native controls can still provide meaningful segmentation, detection, independent authentication, and authorization.*



*It is equally incorrect, however, to treat cloud controls as adequate protection while ignoring a connected on-premises identity system that remains capable of altering users, attributes, passwords, certificates, federation claims, or administrative workflows.*



*A defensible hybrid architecture should:*



*Treat synchronization and provisioning systems as control-plane assets*

*Restrict administration of Entra Connect, Cloud Sync, PTA, and AD FS*

*Separate on-premises and cloud privileged identities where practicable*

*Avoid synchronizing highly privileged accounts unless specifically required*

*Use dedicated privileged access workstations*

*Protect federation token-signing keys*

*Prefer strong certificate-to-user bindings*

*Monitor changes to synchronized identity attributes*

*Monitor federation configuration and signing-certificate changes*

*Establish cloud-only emergency access accounts*

*Apply independent cloud role governance*

*Use Conditional Access and phishing-resistant authentication*

*Review writeback and synchronization scope*

*Eliminate unnecessary federation and legacy authentication dependencies*

*Test hybrid identity incident-response and recovery procedures*



*Zero Trust Architecture (ZTA) does not require defenders to declare either the cloud or the internal network inherently trusted. It requires explicit evaluation of identity, device, resource, context, and risk.*



*In a hybrid environment, that principle must be applied to every bridge between Active Directory and the cloud.*



*The on-premises directory and the cloud identity platform are separate control planes. The connections between them determine whether compromise of one can become compromise of the other.*



**1.2.5.8 THE FAR-REACHING IMPACTS OF A SUCCESSFUL FEDERAL COMPROMISE**



Because these environments are deeply intertwined with one another, the security perimeter is only as strong as its weakest link. A compromise of the on-premises directory does not stop at the local firewall or perimeter edge router - it propagates directly into the cloud through these synchronized pipelines.



If an adversary is able to achieve domain dominance on-premises, they can easily pivot to cloud workloads and take over from there. By targeting the sync server, extracting the encryption keys used by Entra Connect, or executing an AD FS Golden SAML attack, threat actors can forge administrative tokens. This allows them to bypass Multi-Factor Authentication (MFA) and gain unauthorized access to every cloud service and application that trusts the compromised federation - the full scope of which depends on the relying party trust configuration of that specific AD FS deployment.



What is more is that a single misconfiguration in certificate-to-identity mapping can completely disrupt cloud-based authentication. This allows actors to map an unprivileged on-premises certificate to a highly privileged cloud role.



**1.2.5.9 DEFENDING THE HYBRID ENTERPRISE**



Ultimately, Active Directory's role in hybrid identity makes its structural integrity vital to the entire enterprise. Its defenses are directly tied to cloud-based mission functions.



Securing cloud assets is impossible if the underlying on-premises directory remains vulnerable. It is quite pointless, to be honest. To achieve a true Zero Trust architecture, agencies and security teams must realize that the on-premises directory controls the cloud in most cases. It must, therefore, be defended with the same level of strict vigilance and rigor as the core cloud control plane itself.



**1.2.6 ACTIVE DIRECTORY'S ROLE IN MISSION-PARTNER AND CROSS-BOUNDARY ACCESS**



Federal and military missions routinely require access across agency, command, contractor, coalition, and mission-partner boundaries.



A contractor may need access to an agency application.



A military service may need to consume an identity assertion issued by another component.



A coalition partner may require access to a shared mission environment.



A federal agency may need to accept a PIV credential issued by another agency.



These scenarios require more than authentication. They require the receiving environment to determine whether an externally established identity, authenticator, attribute, or assertion is sufficiently trustworthy for access to a specific resource.



The Federal Identity, Credential, and Access Management (FICAM) Architecture defines federation as the technology, policies, standards, and processes that allow an agency to accept digital identities, attributes, and credentials managed by other agencies.



**1.2.6.1 CROSS-BOUNDARY TRUST IS NOT A SINGLE TECHNOLOGY**



Cross-boundary access can be implemented through several architectures, including:



Active Directory forest trusts

Selective authentication across forest boundaries

AD FS federation

Microsoft Entra external identities

SAML federation

OpenID Connect federation

OAuth authorization

PIV or CAC certificate authentication

Federal PKI trust

Agency-operated federation hubs

Mission-partner identity providers

Application-specific credential acceptance

Identity-provider and relying-party trust agreements



Active Directory may be central to some of these architectures, but it is not always the root identity authority.



A cloud-native identity provider may authenticate the mission partner directly.



A federal credential service provider may issue and manage the credential.



A federation hub may broker assertions between agencies.



A PIV or CAC certificate may be validated through FPKI trust without the issuing user existing in the receiving agency’s Active Directory.



The precise role of AD DS depends on the architecture.



**1.2.6.2 ACTIVE DIRECTORY’S ROLE IN THE TRUST CHAIN**



In a Windows-centered federal environment, Active Directory may act as:



The authoritative source for workforce users and groups

The authentication backend for an identity provider

The repository for attributes used in federation claims

The source of authorization groups consumed by applications

The platform supporting AD FS

The destination for externally authenticated users

The directory used to map PIV or CAC certificates to local accounts

The basis for a direct forest trust

The administrative control plane for systems exposed to mission partners



A typical federated access path can be represented as follows:



\[Mission-Partner User and Authenticator]

&#x20;                   │

&#x20;                   ▼

\[Credential Service Provider / Identity Provider]

&#x20;                   │

&#x20;                   │  Signed identity assertion

&#x20;                   ▼

\[Federation Trust, Metadata, and Signing Keys]

&#x20;                   │

&#x20;                   ▼

\[Agency Relying Party or Federation Broker]

&#x20;                   │

&#x20;                   │  Claims evaluated against local policy

&#x20;                   ▼

\[Authorized Application or Mission Resource]



In this model, the partner identity provider authenticates the user and issues an assertion. The agency Relying Party (RP) verifies the assertion’s signature, validates its issuer, audience, lifetime, and other protocol requirements, and then evaluates the supplied attributes or claims against local authorization policy.



NIST Special Publication (SP) 800-63C-4 describes federation as a model in which an Identity Provider (IdP) supplies authentication attributes and, when applicable, subscriber attributes to separately administered relying parties.



The receiving agency is not simply trusting an Active Directory account. It is trusting a chain of technical and governance decisions:



The identity-proofing process used for the individual

The credential or authenticator issued to that individual

The partner’s identity lifecycle controls

The authentication method used for the session

The security of the partner IdP

The protection of federation signing keys

The accuracy of the asserted attributes

The federation protocol and configuration

The legal or operational trust agreement

The receiving application’s authorization policy



Active Directory may support several of these decisions, but it does not independently guarantee all of them.



**1.2.6.3 FEDERATION ASSURANCE AND LOCAL AUTHORIZATION**



A valid federated assertion does not automatically justify access to every resource.



Federation establishes that the relying party is willing to accept specific identity and authentication information from a trusted issuer. The relying party must still decide what the asserted identity may access.



Under the NIST digital identity model, the Federation Assurance Level (FAL) addresses protections applied to federation transactions and assertions. The Authentication Assurance Level (AAL) addresses confidence in the authentication process, while the Identity Assurance Level (IAL) addresses confidence in the identity-proofing process.



The agency must determine whether the identity, authentication, federation, and attribute assurances are sufficient for the sensitivity of the requested resource.



A coalition partner’s valid assertion might permit access to one shared application but not another.



A contractor identity may be accepted only while the contract, sponsorship, investigation, training, and account lifecycle remain valid.



An external PIV certificate may strongly authenticate the holder but still require local authorization based on mission role, citizenship, clearance, need to know, device posture, or resource-specific policy.



Federation reduces the need to create and independently maintain credentials for every external user. It does not eliminate the receiving agency’s responsibility to enforce authorization.



**1.2.6.4 THE SECURITY CONSEQUENCES OF CROSS-BOUNDARY TRUST**



Every federation relationship extends the effective attack surface beyond the systems directly operated by the relying agency.



If a trusted partner IdP is compromised, an adversary may be able to issue fraudulent assertions.



If a federation signing key is compromised, an adversary may be able to forge apparently valid tokens.



If attribute mappings are inaccurate, an external identity may receive excessive authorization.



If deprovisioning is delayed, a former employee or contractor may retain access after the underlying mission need has ended.



If trust metadata or issuer configuration is altered, the relying party may accept assertions from an unauthorized source.



If the receiving application accepts broad group or role claims without local validation, compromise of the partner’s group-management process may become compromise of the receiving application’s authorization model.



The impact is not necessarily reciprocal or enterprise-wide. A properly scoped federation restricts assertions by audience, relying party, attribute, application, session, and authorization policy. A compromised partner should not automatically receive administrative access to every system.



The overall damage impact depends on how much authority the federation grants.



**1.2.6.5 ACTIVE DIRECTORY FOREST TRUSTS**



Direct Active Directory forest trusts create a different form of cross-boundary access from token-based federation.



A forest trust allows security principals from one forest to authenticate and potentially access resources in another forest when the trusting environment grants the necessary permissions. Active Directory supports claims and authorization across forest trust boundaries, but access still depends on trust direction, authentication scope, name and identity filtering, resource permissions, and other configuration.



A forest trust should not be interpreted as unrestricted access between forests. It establishes an authentication path. Authorization must still be granted.



Poorly configured trusts can nevertheless create serious control paths. Risk increases when agencies or mission partners use:



Two-way trusts without a documented requirement

Forest-wide authentication where selective authentication would suffice

Shared administrative accounts

Privileged group nesting across forests

Weak Security Identifier filtering

Excessive resource permissions

Unmanaged legacy trusts

Overlapping administrative infrastructure

Shared service accounts

Unmonitored cross-forest authentication



Trust architecture must therefore be evaluated from both perspectives: what the trust was designed to enable and what an adversary could reach if either side were compromised.



**1.2.6.6 DEFENDING MISSION-PARTNER ACCESS**



Mission-partner access should be governed as a constrained trust relationship rather than as a general extension of the internal directory.



Agencies and commands should:



Define the identity provider and relying party responsibilities

Document the federation agreement

Establish required IAL, AAL, and FAL values

Limit accepted issuers and token audiences

Protect federation signing and encryption keys

Validate certificate chains and revocation status

Restrict accepted claims and attributes

Map external identities to least-privilege local roles

Apply application-specific authorization

Use selective authentication where appropriate

Monitor cross-boundary authentication

Review partner identity lifecycle and deprovisioning

Establish incident-notification requirements

Define emergency trust-revocation procedures

Test the ability to suspend or terminate federation

Avoid transitive trust assumptions not required by the mission

Revalidate access when mission, contract, sponsorship, or role conditions change



FICAM guidance emphasizes that federation involves accepting identities, attributes, and credentials managed by other agencies and that external federation requires governance and technical agreements.



Active Directory’s role in mission-partner access is therefore consequential but not universal.



Where AD DS supplies the identities, attributes, federation infrastructure, administrative groups, or receiving systems involved in the trust relationship, its compromise may affect external partners as well as the local agency.



Where the federation relies on cloud-native identity providers, federal credentials, or external federation brokers, the trust chain may not begin in Active Directory at all.



The correct security principle is broader:



Cross-boundary access is only as trustworthy as the complete chain of identity proofing, credential issuance, authentication, assertion protection, attribute integrity, authorization, lifecycle management, and governance supporting it.



Active Directory may form a critical part of that chain. It must never be mistaken for the entire chain.



**1.2.7 WHY LEGACY DOMAINS REMAIN OPERATIONALLY CRITICAL**



Some of the Active Directory domains this book is concerned with are not new. They were built in the early 2000s, expanded through acquisitions and command mergers, and have accumulated almost two decades or more, of technical debt. Domain functional levels that could be raised haven't been. Not ever. Schema extensions installed for a retired application remain. Trust relationships established for a decommissioned mission still exist, and have become "part of the norm." Service accounts created for a system that was replaced 15 years ago still authenticate and are unnecessarily chatty on the domain.



These legacy and deprecated conditions, are sadly, not unusual. They literally are what a modern normal operating environment looks like for much of the federal and defense identity infrastructure. This book is written for that environment, not for a clean greenfield deployment that nobody actually operates.



1.3 THE FEDERAL IDENTITY TRUST PROBLEM



Federal identity governance differs from commercial identity governance in ways that are not merely procedural. The differences are architectural, operational, and, in some cases, existential - they determine whether mission-essential functions can continue to operate under adversarial conditions.



1.3.1 WHY FEDERAL IDENTITY IS NOT ONLY A MICROSOFT ARCHITECTURE PROBLEM



The frameworks governing federal identity do not begin with Active Directory. They begin with legislation: FISMA, which establishes the federal security accountability structure. They continue with executive direction: HSPD-12, which mandated a common identification standard for federal employees and contractors. They incorporate NIST standards: SP 800-63-4, which defines digital identity assurance requirements; FIPS 201, which defines the PIV standard; SP 800-53, which defines the security control catalog. They culminate in executive memoranda: M-19-17 on ICAM and M-22-09 on Zero Trust, which set the current operational direction.



Active Directory is one technical component within this governance framework. Knowing how to administer Active Directory is not the same as understanding how it must be configured, monitored, and operated within the obligations this framework imposes. This book addresses both.



1.3.2 FICAM AS THE US FEDERAL GOVERNMENT-WIDE IDENTITY ARCHITECTURE LENS



Federal Identity, Credential, and Access Management (FICAM) is not a vendor-specific product, not a Microsoft service, and not a synonym for Active Directory. It is the United States federal government's enterprise approach to the processes of digital human-person entity and Non-Person entity (NPE) identity management, credential management, access management, federation, and the governance that conjoins these identity proofing components as one cohesive unit.



FICAM defines how federal identities, whether that be a human, a device such as a smartphone or a digital assistant, an application, a service, or a process, are proofed, how credentials are issued and bound to those identities, how access is provisioned and governed, how federation relationships are established and terminated, and how all of this is measured and validated over time. Active Directory may support several of these functions, but it is one technical component within an architecture that encompasses the entire federal identity lifecycle.



Reading this book through the FICAM lens means asking, for every technical subject: *what federal identity function does this support, and what does it mean for the federal identity trust system when this function fails?*



1.3.3 DoD ICAM AS THE DEFENSE IMPLEMENTATION LENS



Department of Defense Identity, Credential, and Access Management (DoD ICAM) applies the FICAM framework to an environment with requirements that civilian agencies do not uniformly share: classified and unclassified network boundaries, Common Access Card (CAC) credentials bound to an EDIPI for personnel, non-person entity governance at the scale of global military organization, coalition, and mission-partner access requirements, and the operational availability obligations of a warfighting organization.



DoD ICAM introduces concepts that shape how identity security is understood in defense environments: the Defense Information Systems Agency (DISA) as the technical standards authority; Secure Technical Implementation Guides (STIGs) and Security Requirements Guides (SRGs) as the baseline configuration requirements; the DoD Federation Hub as the broker for cross-component trust; the Secret Fabric as the classified counterpart to unclassified enterprise identity components; and the operational context in which identity failures are not IT disruption but potential effects on mission command.



1.3.4 HOW IDENTITY GOVERNANCE CONNECTS PEOPLE, DEVICES, SERVICES, ATTRIBUTES, CREDENTIALS, AND ACCESS



Federal identity governance addresses more than just human entities. It addresses the complete population of principals that interact with federal information systems and the complete set of attributes that govern what those principals can access and what they cannot.



People are credentialed through identity proofing processes that establish who they are before any credential is issued. Devices are registered and enrolled through processes that establish what they are and whether they are authorized to participate in the identity system. Services are registered as non-person entities with their own sets of credentials and privileges. Attributes - organizational affiliation, clearance level, role, citizenship, PIV status - determine what access each identity can request and under what conditions. The governance framework that connects these elements is not a convenience, a luxury, or an advantage - it is the sole mechanism through which the federal government's access decisions become defensible, auditable, and recoverable.



1.3.5 PERSON ENTITIES AND NON-PERSON ENTITIES (NPE) AS FEDERAL IDENTITY SUBJECTS



One of the most practically important distinctions in federal identity governance is the one between person entities and non-person entities (NPEs). Person entities are human users: federal employees, military personnel, contractors, coalition partners. Non-person entities are everything else: service accounts, application identities, device accounts, workload identities, automated processes.



The significance of this distinction for Active Directory security is direct. The PIV and Common Access Card (CAC) mandates that drive strong authentication requirements in federal environments apply to person entities. Non-person entities cannot physically carry a smartcard. They authenticate through other mechanisms - Kerberos service tickets, certificates, password hashes, Application Programming Interface (API) keys - and they are frequently the weakest credentials in an environment because they are the ones the strong-authentication mandates structurally cannot reach.



Attackers know this fact very well. The service account with an old password from 2003 and a Service Principal Name (SPN) registration is not protected by PIV alone. The synchronization account with replication-equivalent permissions is not protected by phishing-resistant Multi-Factor Authentication (MFA). Non-person entity governance is simply not optional; it is the very gap through which identity compromises most commonly enter.



1.3.6 AUTHORITATIVE ATTRIBUTES AND THE PROBLEM OF TRUSTING IDENTITY DATA



Access decisions if a federal environment are only as good as the attributes that inform them. An authorization decision based on a stale clearance attribute, an outdated organizational affiliation, or a group membership that was never revoked after a role change is not a good authorization decision. Period. It is a correct authorization based on incorrect or incomplete data - which, in and of itself, is a major security failure that to many look just like normal operations.



Authoritative attributes are attributes that are sourced from the System of Record (SOR) for that data element: the personnel system for employment status, the security clearance database for security background and clearance management, the credentialing system for PIV issuance status. When attributes in the directory reflect what the authoritative source says, access decisions are grounded in accurate data. When they drift - through delayed synchronization, through manual overrides that were never corrected, through role changes that were never reflected in group membership - access decisions become unreliable, and the identity trust system is silently unforgiving and degraded.



1.3.7 CREDENTIAL ISSUANCE, CREDENTIAL BINDING, AND ACCESS AUTHORIZATION AS A TRUST CHAIN



Federal identity operates as a trust chain. Identity proofing establishes who the principal is with sufficient confidence for the assurance level required. A credential is issued to the proofed identity, bound to it cryptographically and administratively via EDIPI. Authentication with that credential proves, to the relying system, that the credential holder or claimant is how the credential was originally issued to. Access authorization uses the authenticated identity, with its associated attributes, to decide what the principal is permitted to do.



Each link in this chain can fail. Proofing can be inadequate. Credentials can be stolen, spoofed, or forged. Authentication can be bypassed or replayed. Attributes can be stale or incorrect. Access controls can easily be misconfigured. And each failure looks, from the outside, like successful operation - because the protocols are completing normally, just with the wrong inputs.



This is why identity security requires smart engineering for the failure modes of each link in the identity trust chain, not just for the normal case.



1.3.8 WHY IDENTITY GOVERNANCE MUST BE TESTED AGAINST REAL ATTACK PATHWAYS



Identity governance documents and compliance artifacts can describe a correct and complete trust chain without that chain actually functioning as documented or as originally intended. Controls that are present on paper may not be implemented correctly. Attribute synchronization that is configured may not be running as expected. Certificate mapping that is specific may not be enforced by all relying systems.



The only way to know for sure whether the trust chain functions as documented is to test it against the potential attack pathways that would exploit those failure modes. This is not a claim that red team assessments replace governance - governance provides the intended state that testing is measured against. It is a claim that governance without attack-pathway analysis and validation is not sufficient enough to provide the assurance federal mission systems mandate and require.



1.4 IDENTITY AS THE BATTLEFIELD



Modern adversaries - nation-state threat actors, Advanced Persistent Threat (APT) groups, state-sponsored security professionals, intelligence agencies, and the full range of actors targeting federal and defense networks - have concluded what many defenders have not yet fully absorbed: identity is the most efficient attack surface in today's modern enterprise. Not because endpoints are safe and secured. Not because networks are hardened to their fullest extent. It is because identity is literally the key to everything.



1.4.1 WHY MODERN ADVERSARIES TARGET IDENTITY BEFORE INFORMATION SYSTEMS



A sophisticated adversary does not need to exploit some vulnerability, deploy nasty malware, or leverage the use of an expensive zero-day in a system to access it. They need only one valid credential.



Valid credentials produce valid authentication. Valid authentication produces authorized sessions. Authorized sessions operate within the normal permission set of the account, generating logs that look like normal administrative operational noise, traversing controls that check for valid credentials rather than for malicious intent, and leaving artifacts that are difficult to distinguish from legitimate ones. The adversary who operates with stolen credentials is not actually inside the perimeter just yet - from the system's perspective, they are the authorized user standing at the front door.



This is not a theoretical vulnerability. It is the operational reality of advanced persistent threat intrusions into federal and defense networks. Credential theft, credential abuse, privilege escalation through trust relationships, and persistence through identity manipulation are the dominant techniques because they work - quietly, persistently, and with significant resistance to detection and eviction.



The phrase "crown jewels" gets used so often in Active Directory security discussions that it stops meaning anything at some point. Ask most practitioners what Active Directory's crown jewels are and you will get the same list: the `NTDS.dit` database, the `krbtgt` account, Domain Administrator credentials, the Key Distribution Center (KDC). Reasonable answers. Also incomplete in a way that matters operationally.



None of those is the crown jewel, honestly. Each of them are only a consequence of it.



Before an adversary can steal the `NTDS.dit`, they need to be in the network first.



Before they can forge a Kerberos ticket, they need to be in an authenticated session first.



Before they can abuse a Domain Administrator account, they need a foothold first - and that foothold does not even have to be a privileged one. It does not have to belong to a named administrator or a sensitive service account. It can be any credential for any domain principal: a contractor account that was never deprovisioned, a shared mailbox, a forgotten service account with a password that is crackable in under two minutes with a decent cracking rig, fast GPU, and thorough wordlist. Any of those gets the adversary through the door. 



And what is that credential tied to? A digital identity.



The `NTDS.dit` exists to store digital identities. The KDC exists to authenticate them. Privileged accounts derive their power from the directory's representation of their identity. Strip away all the identity talk and none of those assets holds any operational value. Give an adversary a single valid one - at any privilege level - and the enumeration begins, the attack-pathway graph materializes, and every technique in Part II of this book becomes real.



Every other crown jewel in this list has identity as its prerequisite.



The 2015 Office of Personnel Management (OPM) breach made this concrete for anyone who still needed proof. The adversary's entry point was not a zero-day exploit. It was not a privileged account obtained through some sophisticated escalation chain. It was a single valid credential belonging to a contractor at a third-party firm. From there, the real enumeration begin, the lateral movement followed, and the records of approximately 21.5 million individuals (including myself) - background investigations, fingerprint data, SF-86 (Standard DoD Form 86) with sensitive personally identifiable information (PII) and associative information - left the building over an extended period before anyone noticed. Digital identity was the front door. The `NTDS.dit`, the privileged accounts, the mission data - those were what waited on the other side of it.



1.4.2 WHY CREDENTIALS, TOKENS, CERTIFICATES, AND SESSIONS ARE OPERATIONAL ACCESS POINTS



A Kerberos Ticket Granting Ticket (TGT) is not a piece of useless information. It is **access**. An attacker who holds a valid TGT for a privileged account does not need to authenticate over-and-over - the ticket grants them access to services within its validity window like a VIP, and within an environment where the `krbtgt` key has not been rotated (which is rarely), that window may be much longer than the nominal ticket lifetime (which is 10 hours by default).



A stolen token-signing key is not a cryptographic secret. It is the ability to impersonate any identity in the federation. A stolen certificate with a private key is not just a plain file - it is the authentication capability of the account to which the trusted certificate maps. A session cookie in a web surfing session is not a small string - it is an active authenticated session that can be hijacked from any network position where it is accessible.



Defenders who think about credentials as data to be protected miss the entire point. Credentials are operational capabilities. Their theft is not a disclosure event - it is a capability transfer form the authorized identity to the adversary, and only that.



1.4.3 WHY ADMINISTRATIVE RIGHTS ARE OFTEN LESS IMPORTANT THAN CONTROL PATHWAYS



Conventional security thinking focuses on privileged accounts: Domain Admins, Enterprise Admins, Schema Admins, Local Administrators. These are real targets, but they are not the only ones, and focusing on them to the exclusion of control pathways is a significant defensive blind spot.



A control pathway is any chain of permissions, trust relationships, or configuration conditions that allows a principal to affect a higher-privilege identity or system - regardless of whether the starting point is labeled "administrative." An account with `GenericWrite` permission on a user object can set that user's SPN and Kerberoast it to death. An account with `AllExtendedRights` on a computer object can configure resource-based constrained delegation to allow itself to authenticate as any user to that computer. None of these starting permissions is labeled "privileged." All of them produce pathways to privileged outcomes.



Adversaries find and follow these control pathways. Defenders who inventory administrative accounts but do not analyze control pathways will miss the paths adversaries repeatedly use.



1.4.4 WHY ATTACKERS PREFER TRUST ABUSE OVER EXPLOITATIVE NOISE



A zero-day exploit leaves artifacts, and is messy to clean up. It often triggers EDR (Endpoint Detection and Response) alerts. It requires that the adversary keep the exploit operational and maintain their initial access channel. It is noisy, plain, and simple.



Trust abuse is quiet. When an adversary uses a valid credential obtained through phishing, smishing, quishing, vishing, spearphishing, whaling, or water-holing, the Kerberos ticket request looks like a normal ticket request. The logon event looks like a normal logon. The file access looks like normal file access. The privileged action - if the account had the right - looks like authorized administration.



Advanced adversaries strongly prefer trust abuse over exploitation for exactly this reason. The techniques this book examines are effective not despite being complicated but because they leverage the environment's own legitimate trust mechanisms. Understanding these technique is therefore not primary an intellectual exercise in futility - it is what actually enables defender to properly recognize trust abuse in telemetry that is otherwise indistinguishable from the untrained eye.



1.4.5 WHY IDENTITY ATTACKS OFTEN APPEAR AS NORMAL AUTHENTICATION ACTIVITIES



This point deserves its own emphasis because it is the one most likely to be underestimated.



A Kerberoasting attack produces Windows Security log Event ID 4769 (*a Kerberos service ticket was requested*). Normal Kerberos operations produce Event ID 4769 constantly. The attack is only distinguishable from legitimate activity only by the specific combination of logged attributes (if set to log that specific Event ID) - which account requested, which service principal was sued, what encryption type, how many requests in what time window, at what time of day. Without a properly tuned detection rule that sniffs and hunts looking for exactly those attributes, the attack is plainly invisible.



A DCSync attack produces Event ID 4662 (*an operation was performed on an object*) on the domain controller. Legitimate directory replication produces Event ID 4662 every time replication propagates the domain which is roughly every 90 minutes by default, or unless forced via the `gpupdate /force` command. The attack is distinguishable from replication only by the source IP address and the requesting account identity, and only if those are set up properly to be monitored and triggered by detection rule events.



identity attacks hide in the normal traffic of the underlying identity system on purpose as it enables slow-and-low security detection evasion for the attacker. Defending against them requires a full and thorough understanding of what "normal" looks like well enough to recognize what simply is not.



1.4.6 WHY DEFENDERS MUST PROTECT TRUST-BASED DECISIONS, NOT ONLY ENDPOINTS



The defensive instinct is to harden and patch endpoints until blue in the face - enable endpoint detection and response, restrict local administrative rights, disable unused services and network protocols, deploy separate VACLs (Virtual Access Control Lists) for isolated VLANs (Virtual Local Area Networks). These are necessary controls; however, they are not sufficient controls for identity security.



The trust decisions that matter in Active Directory environments are not made on endpoints. They are made in the Kerberos authentication protocol's exchanges on domain controllers. They are made in certificate issuance decisions by Certificate Authorities (CAs). They are made in role assignment and Role-Based Access Control (RBAC) decisions by cloud identity administrators. They are made in claim rule processing by federation services. Protecting trust decisions means protecting the systems and configurations that govern those decisions - the domain controllers, the certificate authority and public key infrastructure, the federation service, the cloud tenant roles, and the synchronization mechanisms that connect them.



An endpoint compromise that escalates to a domain controller is a fundamentally different event than an endpoint compromise that does not. Identity security focuses on preventing that escalation, detecting it when it occurs, and recovering the trust infrastructure when it is compromised.



1.4.7 IDENTITY AS CONTESTED TERRAIN IN FEDERAL AND MILITARY ENVIRONMENTS



The framing of this section's title - identity as the battlefield - is not rhetorical. In federal and military environments, adversaries have specifically targeted identity infrastructure as a precondition for persistent access to mission-critical systems.



The objective is not data exfiltration in the conventional sense. It is the establishment of a foothold in the identity control plane that survives detection of individual intrusions, survives password resets, survives system reimaging and continuous reboots, and provides the ability to regenerate access as needed. An adversary who controls the directory, who holds the `krbtgt` key material, who has modified the AdminSDHolder descriptor to establish persistence, or who has placed a trust in the federation infrastructure has established a presence that does not disappear when a compromised endpoint is rebuilt and re-deployed to the already breached production domain network.



Identity infrastructure is where persistence lives and thrives in sophisticated intrusions. Defending it requires a thorough understanding of this concept.



1.5 HOW TO THINK LIKE AN ATTACKER WITHOUT ABANDONING THE DEFENDER'S MISSION



One of the central arguments of this book is that defenders (not just in federal environments) but as a whole need to think the way attackers think. This argument requires careful framing, because thinking like an attacker does not mean becoming one. It means developing the analytical capability to see the identity trust system the way an adversary sees it - through the perspective of the adversary - as a map of relationships, permissions, and trust pathways rather than as an administrative inventory of objects.



1.5.1 ATTACKER THINKING AS A DEFENSIVE SKILL SET



Attacker thinking is not about memorizing offensive tools or techniques. It is a cognitive posture that as asks different questions than defensive administration typically asks.



The administrator asks: "What should this account be able to do?" The attacker asks: "What can this account actually do, and what does that enable?" The administrator asks: "Is this configuration compliant with policy?" The attacker asks: "What attack paths does this configuration create, regardless of whether it is compliant?" The administrator asks: "Are our logs capturing what they should?" The attacker asks: "What can I do that these logs cannot see?"



Defenders who can switch between these cognitive postures can find the gaps that compliance-only thinking misses. That is the defensive value of attacker thinking.



1.5.2 HOW ATTACKERS READ AND BLUEPRINT A TARGETED ENVIRONMENT



Before an adversary executes an attack, they map the environment. They enumerate the directory to understand its structure: how many domains, what trust relationships, which accounts hold SPNs, which computers have unconstrained delegation configured, which certificate templates are available for enrollment. They query for group memberships to identify privileged accounts. They analyze access control lists to find unexpected permission relationships. They look for paths from their initial access point to higher-privilege targets.



This enumeration process produces what offensive practitioners call a blueprint — a map of the environment's attack surface from the adversary's perspective. Figure 1-3 contrasts the administrative view and the attacker control-path view of the same environment, showing how the same directory data produces two very different pictures depending on the analytical lens applied. The tools that generate this blueprint (BloodHound, SharpHound, Adalanche, PowerView) analyze the same data that exists in every Active Directory environment. The data is not secret. The question is whether defenders have analyzed it first.



1.5.3 WHY ATTACKERS ASK "WHAT CAN THIS IDENTITY CONTROL, ACCESS, MODIFY, OR IMPERSONATE?"



The central attacker question about any identity is not "what is this account?" but "what can this account do?" The answer to the second question is often very different from the answer to the first.



1.5.3.1 ACCESS VERSUS CONTROL



Access is the ability to read or use a resource. Control is the ability to affect who can access it, how it is configured, or what it does. These are different, and control is far more dangerous than access alone. An account with read access to a sensitive file is a confidentiality concern. An account with write access to the security descriptor of a privileged group is a potential domain compromise waiting for someone to notice.



1.5.3.2 READ, WRITE, RESET, ENROLL, REPLICATE, DELEGATE, AND IMPERSONATE RIGHTS



Active Directory access control is granular. An account may have rights to read certain attributes and not others, to write certain object classes and not others, to reset passwords for objects within a specific Organizational Unit, to enroll for certificates from specific templates, to request replication of the directory database, to delegate Kerberos authentication on behalf of users, or to act as another identity entirely.



Each of these rights is a potential attack vector when held by the wrong account or when combined with other rights that extend its impact.



1.5.3.3 WHY LOW-PRIVILEGE IDENTITIES CAN STILL CREATE HIGH-IMPACT PATHWAYS



An account that is not a member of any privileged group is not necessarily without privilege. If that account has GenericWrite on a computer object configured for Resource-Based Constrained Delegation, it can potentially leverage that write access into authentication as any user to that computer. If it has Write access to a certificate template with permissive enrollment flags, it may be able to enroll for a certificate authenticating as a domain administrator. If it has ownership of a group that contains privileged accounts, it can modify the group's membership.



None of these capabilities appears in a group membership report. All of them appear in an access control analysis.



1.5.3.4 WHY ATTACKERS VALUE DOWNSTREAM AUTHORITY MORE THAN JOB TITLES



An adversary compromising an environment does not care whether a target account belongs to a person with an impressive title. They care whether the account has permissions that lead somewhere useful. The accounts with the most interesting attack pathways are frequently not the most visible privileged accounts — they are intermediate accounts, service accounts, or overlooked accounts with unexpected permissions that provide stepping stones toward higher privilege.



1.5.3.5 HOW SMALL RIGHTS BECOME CONTROL PATHWAYS



Individual permissions that appear limited can combine with other conditions to create significant control pathways. The WriteSPN right on a user object enables setting a Service Principal Name, making the account Kerberoastable. The AllExtendedRights permission on a user enables resetting the account's password. The WriteProperty right on specific attributes of a computer object can enable Shadow Credentials attacks. The ForceChangePassword right enables password reset without knowing the current password.



Each of these rights, in isolation, might not appear alarming. Combined with the right target account — a Domain Administrator, an account with Tier 0 access, a privileged service account — they produce a control pathway from a low-privilege position to domain compromise.



1.5.3.6 HOW DEFENDERS TRANSLATE IDENTITY CONTROL INTO MISSION RISK



The defender's obligation is to translate what they find in access control analysis into terms that mission owners and authorizing officials can act on. "An account with GenericWrite permission on the Domain Admins group exists" is a technical finding. "Any compromise of the service account running the helpdesk application could allow an attacker to add themselves to Domain Admins and control every system in the environment" is a mission risk statement.



Making this translation consistently — from technical finding to attack pathway to mission consequence — is one of the core skills this book is designed to develop.



1.5.4 WHY ATTACKERS SCOUT FOR ATTACK PATHWAYS AND NOT JUST VULNERABILITIES



The conventional vulnerability model focuses on discrete weaknesses in software: unpatched CVEs, misconfigured services, weak protocols. These are real and important. But in Active Directory environments, the most impactful attack paths are frequently not CVE-based at all. They are permission-based, trust-relationship-based, and configuration-based — and they exist in environments that are fully patched and scanner-compliant.



An adversary who has one foothold in a domain with no unpatched vulnerabilities may still have a path to domain administrator through trust abuse, credential theft, and permission exploitation. Defenders who rely only on vulnerability scanning will not find these paths. Attack-pathway analysis finds them.



1.5.5 WHY ATTACKERS CHAIN WEAKNESSES ACROSS IDENTITY SYSTEMS



Advanced adversaries do not exploit one weakness at a time. They chain them. A low-privilege domain account is used to enumerate certificate templates. A misconfigured template is exploited to obtain a certificate authenticating as a high-privilege account. That certificate is used to obtain a Kerberos TGT through PKINIT. The TGT is used to request service tickets for sensitive services. A service account credential from one of those tickets is cracked offline and used to log into a server that has an Active Directory Federation Services configuration backup. The federation configuration backup yields the token-signing private key. The token-signing key is used to issue assertions to cloud services accessed by mission partners.



No single link in that chain is catastrophic in isolation. The chain as a whole is a complete identity trust system compromise. Defenders who analyze weaknesses individually will not see it coming. Defenders who analyze the system — its trust relationships, its permission chains, its federation configuration — will.



1.5.6 HOW DEFENDERS USE ATTACKER THINKING TO VALIDATE CONTROLS



Attacker thinking does not require performing actual attacks. It requires asking attacker questions about the defensive controls that are in place. For every control: what does this prevent, under what conditions does it fail, and how would an adversary attempt to bypass it?



A Protected Users group prevents NTLM authentication for its members. An adversary who needs to authenticate from a non-Kerberos context or who targets an account not in Protected Users is not stopped. Knowing this allows a defender to ensure that all Tier 0 accounts are in Protected Users, that non-Kerberos authentication is monitored, and that the remaining accounts not covered by Protected Users have compensating controls.



This analysis — systematically asking how each control fails — is control validation from an adversarial perspective. It produces more honest assurance than compliance checking alone.



1.5.7 THE ETHICAL AND AUTHORIZED BOUNDARY OF OFFENSIVE THINKING



Thinking like an attacker does not authorize acting like one. In federal and defense environments, all offensive activity — penetration testing, red team exercises, vulnerability assessment — requires explicit authorization under documented Rules of Engagement, legal review, and appropriate oversight structures.



This book discusses offensive techniques because understanding them is essential for defense. It does not authorize their use outside the context of properly authorized security assessments. Readers who intend to apply offensive techniques in operational environments must ensure that those activities are conducted under appropriate authorization. That obligation is not a disclaimer — it is a professional and legal requirement that federal security practitioners must internalize.



1.5.8 WHY FEDERAL DEFENDERS MUST TRANSLATE ATTACK PATHWAYS INTO MISSION RISK



The final obligation of attacker thinking, in federal and defense contexts, is translation. Finding attack pathways is analytically useful. Communicating them in ways that inform mission decisions is operationally essential.



Mission owners, commanding officers, and authorizing officials are not required to understand PKINIT or Kerberoasting. They are required to understand risk. The defender's obligation is to produce finding descriptions that tell the relevant decision-maker: what is exposed, what an adversary could do with that exposure, what mission functions are at risk, and what corrective action would close the gap. This translation — from technical finding to mission risk to governance decision — is developed throughout this book.



1.6 ASSUME BREACH AS THE STARTING POINT FOR IDENTITY SECURITY ENGINEERING



Assume Breach is not a philosophy of despair. It is a design principle.



1.6.1 WHAT IT MEANS TO ASSUME BREACH



To Assume Breach is to begin security engineering from the premise that an adversary has already achieved, or will achieve, initial access to the environment — and to design detection, containment, and recovery capabilities accordingly.



This premise does not mean the organization has failed or that prevention is irrelevant. It means that in environments that are targeted by sophisticated, persistent adversaries — which includes every federal and defense organization this book addresses — prevention alone is insufficient. No preventive control portfolio has achieved a 100 percent prevention rate against advanced persistent threats, and no organization that relies exclusively on prevention is prepared for the moment it fails.



Assume Breach is the answer to the question: what happens after prevention fails?



1.6.2 WHAT ASSUME BREACH DOES NOT MEAN



Assume Breach does not mean abandoning preventive controls. It does not mean accepting that compromise is inevitable and not worth preventing. It does not mean that Tier 0 protections, strong authentication requirements, certificate hygiene, and federation governance are unnecessary.



Preventive controls reduce the frequency and severity of breaches. Detection reduces the dwell time — the duration between initial access and discovery — during which adversaries conduct their operations. Containment limits the blast radius of a compromise that has occurred. Recovery restores trusted operation. All four functions are necessary. Assume Breach simply makes explicit that detection, containment, and recovery must be designed with the same rigor as prevention, rather than treated as afterthoughts.



1.6.3 WHY PREVENTIVE CONTROLS ALONE ARE NOT ENOUGH



Preventive controls are bounded by what is known. They protect against known attack patterns, known vulnerabilities, and known threat actor techniques. They are implemented at the boundary of known-good and known-bad, and they fail when an adversary operates in the space that is neither.



In an Active Directory environment, that space is large. Trust relationship abuse does not look like a known attack pattern — it looks like normal Kerberos traffic. Legitimate credential theft does not look like malware — it uses built-in Windows capabilities. Persistence through identity infrastructure modification does not look like system compromise — it looks like administrative changes. Preventive controls that key on known-bad signatures will not see these techniques.



Detection that understands the identity trust system and knows what normal looks like within it has a fundamentally better chance of recognizing these techniques. Assume Breach is what drives investment in that detection capability.



1.6.4 WHY IDENTITY SECURITY MUST BE VALIDATED AFTER INITIAL ACCESS IS ASSUMED



Once an adversary has initial access to an environment — even as a low-privilege domain user — the question is not whether the authentication controls prevented their entry. It is what they can reach from where they are.



Assume Breach testing — sometimes called red team or adversary emulation — answers that question by starting from an authorized point of initial access and determining what attack pathways exist from there. In identity security, this means: starting from a low-privilege domain account, what certificate templates are exploitable? What service accounts are Kerberoastable? What access control lists create unexpected control pathways? What trust relationships extend beyond the domain? What federation configurations expose token-signing material?



These questions are answered not by vulnerability scanning but by operating the way an adversary would operate, within an authorized testing context.



1.6.5 HOW ASSUME BREACH CHANGES ACTIVE DIRECTORY ASSESSMENTS



A traditional Active Directory security assessment asks: are the recommended configurations in place? Is SMB signing enforced? Is NTLM restricted? Is LAPS deployed? Are privileged accounts in Protected Users? These questions are necessary and important.



An Assume Breach assessment adds: given what is configured, what can an adversary do? It starts from an authorized initial access position and attempts to find pathways to higher privilege. It tests whether the controls that should prevent escalation actually prevent it, under realistic attack conditions and with realistic attack techniques.



The two approaches are complementary. Configuration assessment tells you what controls are in place. Assume Breach assessment tells you whether those controls are sufficient given the actual attack surface of the environment.



1.6.6 HOW ASSUME BREACH CHANGES LOGGING AND DETECTION REQUIREMENTS



If an adversary will achieve initial access, the organization needs to detect them during the time between initial access and impact. That time — dwell time — is determined by how quickly the organization can recognize that an adversary is present and operating.



Assume Breach makes detection requirements explicit: every significant attack technique should produce a detectable signal in a properly configured logging and monitoring environment. If a technique does not produce a detectable signal, that is a detection engineering gap. If it produces a signal but no one is looking at it, that is a coverage gap. If it produces a signal that no one can interpret, that is a skills gap.



Detection engineering under Assume Breach means designing telemetry collection, correlation rules, and analyst workflows around the assumption that an adversary is operating in the environment right now.



1.6.7 HOW ASSUME BREACH CHANGES RECOVERY AND RESTORATION PLANNING



Recovery planning under Assume Breach must account for the possibility that the identity trust infrastructure itself is compromised. If an adversary has modified AdminSDHolder to establish persistence, recovery requires identifying and remediating those changes before restoring normal operations. If krbtgt keys have been exposed, a double-reset is required and must be sequenced correctly. If a certificate authority's private key has been stolen, the CA must be revoked and reissued.



Identity trust restoration is not the same as system restoration. A server can be rebuilt from a clean image. The trust relationships, permission configurations, and governance artifacts that make an identity trust system trustworthy take longer to validate and restore. Assume Breach planning accounts for this.



1.6.8 ASSUME BREACH AND MISSION ASSURANCE



For a federal agency or military command, Assume Breach has a mission-specific dimension. Mission assurance requires that mission-essential functions can continue to operate under adversarial conditions. That means the identity infrastructure supporting those functions must be designed to degrade gracefully — to continue providing authentication and authorization for mission-critical systems even when portions of the infrastructure are compromised or unavailable.



Assume Breach does not guarantee mission assurance. It is the engineering posture that makes mission assurance achievable: by understanding what failure modes exist, designing detection that finds adversaries during their dwell time, building containment that limits blast radius, and planning recovery that can restore trusted identity infrastructure rather than merely rebuilding systems.



1.7 FROM CYBER KILL CHAIN TO IDENTITY KILL CHAIN



The Lockheed Martin Cyber Kill Chain, introduced in 2011, provided a common language for understanding adversary progression: Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command and Control, Actions on Objectives. This model was enormously valuable for organizing thinking about intrusion detection and response. It is also, for the purposes of Active Directory identity security, incomplete.



1.7.1 WHY TRADITIONAL KILL CHAIN MODELS NEED IDENTITY-SPECIFIC TRANSLATION



The traditional kill chain was designed to describe malware-centric intrusions. The adversary delivers a malicious payload, exploits a vulnerability, installs an agent, and operates through a command-and-control channel. This model captures an important and real class of intrusion.



It does not well capture the intrusion pattern that dominates advanced persistent threat activity against federal and defense networks: credential-based lateral movement through a legitimate identity infrastructure, with no malware, no exploits, and no command-and-control channel that differs from normal domain traffic.



An adversary who phishes a low-privilege user's credentials, uses those credentials to enumerate the directory, identifies a misconfigured certificate template, exploits it to obtain a high-privilege certificate, authenticates as a domain administrator, performs DCSync to extract the krbtgt key, and creates a Golden Ticket — this adversary has never executed malware, never exploited a CVE, and never created a network connection that looks different from normal Active Directory traffic. The traditional kill chain does not give defenders a framework for identifying or interrupting this progression.



The identity kill chain does. Figure 1-4 maps the traditional cyber kill chain stages to their identity kill chain equivalents, and Table 1-4 later in this chapter provides the detailed stage-by-stage correspondence.



1.7.2 RECONNAISSANCE AS IDENTITY EXPOSURE DISCOVERY



In the identity kill chain, reconnaissance is not external scanning of the organization's perimeter. It is the discovery of identity exposure: public-facing federation metadata that reveals the organization's identity provider configuration, certificate transparency logs that reveal issued certificates and their subjects, DNS records that reveal Active Directory domain structure, LinkedIn profiles that reveal organizational membership and role titles, and any other external information that allows an adversary to develop hypotheses about the identity trust system before gaining access to it.



1.7.3 ENUMERATION AS TRUST RELATIONSHIP DISCOVERY



Once inside the domain — with any valid credential — the adversary's next objective is to understand the trust relationships that structure the environment. Which accounts have SPNs? Which computers have unconstrained delegation configured? What certificate templates are available? What trusts exist with other forests or domains? What cloud services are accessible through federated authentication? What service accounts hold permissions that create control pathways?



This is not a passive information-gathering exercise. It is the adversary constructing a blueprint of the attack surface from inside the environment, using tools and queries that are functionally identical to what a legitimate administrator uses for inventory and management.



1.7.4 INITIAL IDENTITY ACQUISITION AS THE FIRST TRUST BREAK



Initial identity acquisition is the moment the adversary acquires a valid credential that allows them to authenticate to the domain. It may come through phishing a human user's credentials, through credential stuffing against a publicly accessible authentication endpoint, through MFA fatigue attacks on enrolled multi-factor authentication, or through any other technique that produces a valid session or credential.



This is the first trust break: the adversary is now operating with a credential that the identity system treats as legitimate.



1.7.5 CREDENTIAL ACQUISITION AS ACCESS MATERIAL COLLECTION



Credential acquisition is the systematic collection of access material: NT hashes from LSASS memory, Kerberos tickets from memory, service account credentials through Kerberoasting, cached credentials from offline storage, certificate private keys from certificate stores, refresh tokens and Primary Refresh Tokens from cloud sessions. The objective is to accumulate credential material that can be used to authenticate as higher-privilege identities.



1.7.6 IDENTITY AUTHORITY EXPANSION AS PRIVILEGE GROWTH



Identity authority expansion is the progression from initial access to higher privilege through permission abuse, trust relationship exploitation, and delegation abuse. It includes ACL exploitation, certificate-based privilege escalation, delegation attack paths, and any other technique that converts lower-privilege access into higher-privilege access within the identity trust system.



1.7.7 ENTERPRISE IDENTITY MOBILITY AS MOVEMENT THROUGH ESTABLISHED TRUST CHAINS



Enterprise identity mobility is lateral movement conducted through the identity trust system rather than through network exploitation. The adversary passes the hash, passes the ticket, relays NTLM credentials, or uses stolen certificates to authenticate to additional systems — operating through the domain's own authentication infrastructure rather than through attack channels that differ from normal traffic.



1.7.8 PERSISTENCE AS LONG-TERM CONTROL OF IDENTITY INFRASTRUCTURE



Persistence in an identity-centric intrusion is achieved not through malware but through modifications to the identity infrastructure itself: AdminSDHolder modifications that survive attribute synchronization, SID History injections that provide persistent cross-domain access, malicious certificates with long validity periods, rogue federation trusts, krbtgt key material that enables Golden Ticket generation indefinitely, and DCShadow modifications that avoid normal replication detection.



1.7.9 DOMAIN DOMINANCE AS STRATEGIC TRUST COLLAPSE



Domain dominance is the state in which the adversary controls the identity trust system. They hold the krbtgt key material. They have modified the directory to ensure persistent access. They can generate credentials for any identity. They can suppress or manipulate the telemetry that defenders would use to detect them. From this position, every subsequent operation occurs through the legitimate identity infrastructure, making detection and eviction extremely difficult.



1.7.10 WHY THE IDENTITY KILL CHAIN STRUCTURES PART II



Part II of this book is organized around the identity kill chain: passive reconnaissance, active enumeration, initial identity acquisition, credential acquisition, identity authority expansion, enterprise identity mobility, and persistence and domain dominance. This organization is not arbitrary — it reflects how sophisticated adversaries actually operate against Active Directory environments, and it ensures that the offensive techniques this book examines are understood as part of a coherent operational progression rather than as isolated tricks.



1.8 THE ACTIVE DIRECTORY ATTACK LIFECYCLE USED IN THIS BOOK



Table 1-4, presented later in this chapter, maps the traditional cyber kill chain stages to their identity kill chain equivalents. The following sections describe the seven stages of the Active Directory identity attack lifecycle that structure Part II.



1.8.1 STAGE 1 — PASSIVE RECONNAISSANCE



The adversary collects identity exposure information from external sources without touching the target environment directly: federation metadata endpoints, certificate transparency logs, DNS records, OSINT on organizational structure and personnel, public GitHub repositories that may contain credentials or configuration artifacts, cloud tenant discovery through DNS or Microsoft login pages.



1.8.2 STAGE 2 — ACTIVE ENUMERATION



With initial access established, the adversary enumerates the directory: all users, all computers, all groups, all trust relationships, all Service Principal Names, all Group Policy Objects, all Access Control Lists, all certificate templates, all delegation configurations, and all attack pathways connecting the initial access position to higher-privilege targets.



1.8.3 STAGE 3 — INITIAL IDENTITY ACQUISITION



The adversary acquires the first valid domain credential through any available technique: password spraying, credential stuffing, phishing, MFA fatigue, OAuth consent abuse, or exploitation of exposed authentication endpoints. The result is a valid credential that allows authentication as a domain principal.



1.8.4 STAGE 4 — CREDENTIAL ACQUISITION



The adversary systematically collects credential material: Kerberoasting service account tickets, extracting cached credentials, dumping LSASS, obtaining NT hashes through methods appropriate to their access level, stealing certificate private keys, and acquiring cloud tokens through any available path.



1.8.5 STAGE 5 — IDENTITY AUTHORITY EXPANSION



The adversary escalates privilege through the identity trust system: exploiting Access Control List misconfigurations, abusing delegation, exploiting certificate templates, leveraging shadow credentials, or any other technique that converts lower-privilege access into higher-privilege access within the domain or connected identity systems.



1.8.6 STAGE 6 — ENTERPRISE IDENTITY MOBILITY



The adversary moves laterally through the enterprise using credential material and trust relationships: Pass-the-Hash, Pass-the-Ticket, NTLM relay, certificate-based authentication to additional systems, cross-domain and cross-forest traversal through established trust relationships, and cloud pivot through hybrid identity synchronization or federated access.



1.8.7 STAGE 7 — PERSISTENCE AND DOMAIN DOMINANCE



The adversary establishes durable control of the identity trust system: krbtgt key extraction for Golden Ticket generation, AdminSDHolder modification for persistent ACL control, DCSync capability for ongoing credential harvest, token-signing key theft for federation persistence, and any other technique that ensures continued access through the identity infrastructure rather than through vulnerable endpoints that may be remediated.



1.8.8 WHY THE LIFECYCLE IS NOT LINEAR IN REAL-WORLD INTRUSIONS



The seven-stage lifecycle is an analytical framework, not a rigid sequence. Real-world adversaries iterate: they may reach Stage 5 and discover they need additional Stage 2 enumeration to find the next escalation path. They may achieve Stage 7 domain dominance and return to Stage 1 passive reconnaissance to understand what the identity trust system can reach beyond the initial domain. They may operate at multiple stages simultaneously, with different team members handling different functions.



The lifecycle is presented sequentially because sequential presentation best supports learning. It should be understood operationally as a map of the attack surface, not a recipe that adversaries follow in strict order.



1.8.9 HOW DEFENSIVE SECURITY ENGINEERING MIRRORS THE ATTACK LIFECYCLE



Part III of this book mirrors the attack lifecycle from the defensive perspective. Each stage of the attack has a corresponding defensive chapter that examines detection, hardening, and recovery for the techniques that stage employs. The defensive mirror is not a section-by-section rebuttal — it is an integrated defensive engineering framework that addresses the attack lifecycle as a complete problem.



1.9 THE DEFENDER'S PROBLEM: SEEING WHAT THE ATTACKER SEES



Defensive identity security fails in predictable ways. Understanding those failure modes is the starting point for building defenses that actually work.



1.9.1 WHY ADMINISTRATIVE VISIBILITY IS NOT THE SAME AS ATTACK-PATH VISIBILITY



An Active Directory administrator can tell you every group membership in the domain, every account's last password reset, every computer's patch level, and every Group Policy Object's configuration. What they typically cannot tell you, without specific analysis tools and deliberate effort, is the attack-path graph: the map of which accounts can affect which other accounts through the domain's permission structure.



Administrative visibility is object-level. Attack-path visibility is relationship-level. An object-level inventory tells you what exists. A relationship-level analysis tells you what can affect what. Both are necessary. Most organizations have invested heavily in the first and inconsistently in the second.



1.9.2 WHY INVENTORY DOES NOT EQUAL VISIBILITY AND CONTROL



An asset inventory that says a service account exists is not the same as visibility into what that account can do. An account inventory that says no unauthorized accounts exist is not the same as control over all permission relationships in the domain. An access control list that says a group is configured correctly is not the same as assurance that every member of every nested group within that group has appropriate access.



These are not arguments for abandoning inventory — they are arguments for extending it into the relationship and permission space that inventory alone does not cover.



1.9.3 WHY COMPLIANCE DOES NOT AUTOMATICALLY EQUAL SECURITY



A system can meet every applicable STIG requirement, pass every IAVA check, have clean continuous monitoring outputs, and still have control pathways that allow an adversary with initial access to escalate to domain administrator.



Compliance measures the presence of controls. It does not measure their effectiveness against real attack techniques. An organization that conflates compliance with security has substituted a process for an outcome. This book does not suggest that compliance is unimportant — it is required and it provides a necessary baseline. But it does insist that compliance is the floor, not the ceiling, of identity security.



1.9.4 WHY LOGGING DOES NOT AUTOMATICALLY EQUAL DETECTION



Event logs that are collected but never analyzed are not detection. Alerts that fire on known signatures but miss identity-based attack techniques that produce only normal-appearing authentication events are not detection. A Security Information and Event Management platform that ingests millions of events per day but has no tuned rules for Kerberoasting, DCSync, or NTLM relay is not detection.



Detection requires telemetry that captures the right events, correlation rules that identify the right patterns in that telemetry, analyst capacity to investigate what the rules surface, and institutional knowledge of what normal looks like. All of these requirements must be met simultaneously. Any gap in the chain breaks the detection capability.



1.9.5 WHY HARDENING DOES NOT AUTOMATICALLY EQUAL RESILIENCE



A hardened system is a system that has been configured to reduce its attack surface. A resilient system is one that can continue operating, detect adversarial activity, contain damage, and recover under adversarial conditions. Hardening contributes to resilience but does not produce it alone.



An environment with every STIG applied and every recommended control in place, but with no incident response plan, no recovery procedures for identity trust compromise, and no tested backup capability for domain controllers and certificate authorities, is hardened but not resilient. Resilience requires hardening plus detection plus response plus recovery — all designed and tested together.



1.9.6 WHY RECOVERY PLANS MUST ASSUME IDENTITY TRUST MAY BE CORRUPTED



Standard disaster recovery procedures focus on data restoration and service restoration. Identity trust recovery is a different problem. Restoring a domain controller from backup restores the directory state to the backup point. If an adversary compromised the directory before the backup was taken, restoring from that backup restores the adversary's modifications as well.



Recovery planning for identity trust compromise must account for this: how to determine what modifications the adversary made, how to validate that the restored state is clean, how to reset krbtgt keys correctly so that existing forged tickets are invalidated, how to revoke compromised certificates, and how to rebuild federation trust after token-signing key compromise. These procedures must be documented, tested, and exercised before they are needed.



1.9.7 WHY DEFENDERS NEED SECURITY ENGINEERING, DETECTION, GOVERNANCE, AND RECOVERY TOGETHER



None of the four defensive functions — security engineering, detection, governance, and recovery — is sufficient alone.



Security engineering without detection leaves the organization blind to what bypasses its controls. Detection without security engineering generates so much noise from low-hanging fruit that the signal of sophisticated attacks is buried. Governance without attack-pathway awareness approves configurations that are compliant but exploitable. Recovery without governance produces clean systems that are rebuilt into the same vulnerable configurations.



The four functions are a system. This book treats them as one.



1.10 FEDERAL MISSION RISK AND THE IDENTITY CONTROL PLANE



Identity compromise is not an IT event with IT consequences. In federal and military environments, it is a mission event with mission consequences. This section maps the components of the identity control plane to the mission functions they support — so that when those components are compromised, the mission impact is legible.



1.10.1 IDENTITY COMPROMISE AS A MISSION-IMPACT EVENT



When the identity trust system is compromised in a meaningful way — not a single account password exposed, but a Tier 0 compromise that puts the adversary in control of the directory's authoritative functions — the organization faces a specific set of mission-level problems.



It cannot confidently determine which accounts are clean and which have been modified. It cannot confidently determine which authentication events are legitimate and which are adversary operations. It cannot confidently determine which administrative actions are safe to execute and which would be executed in an environment the adversary still controls. It cannot confidently determine which logs have been tampered with and which accurately reflect what occurred.



These are not IT problems. They are decision-support problems, mission command problems, and operational risk problems. Figure 1-5 illustrates how a Tier 0 identity compromise propagates outward to the mission functions that depend on the identity trust system — authentication for sensitive systems, federation with mission partners, cloud service access, and certificate trust for encrypted communications.



1.10.2 PRIVILEGED ACCESS AS OPERATIONAL AUTHORITY



In federal and defense environments, privileged administrative access to identity infrastructure is a form of operational authority. The individual who can modify group memberships, reset passwords for any account, create authentication bypasses, or modify Group Policy controls for an enterprise of thousands of systems holds operational authority over those systems — the ability to affect who can use them, what they can do, and how they behave.



Treating privileged access as an IT management convenience rather than as operational authority is a governance failure. Privileged access to Tier 0 identity infrastructure should be controlled with the same rigor applied to operational authority in the mission context — restricted, monitored, time-limited, and accountable.



1.10.3 FEDERATION TRUST AS MISSION PARTNER DEPENDENCY



When a federal agency or military command has federation relationships with mission partners — other agencies, coalition partners, contractors, cloud services — those relationships are mission dependencies. The mission functions that depend on cross-boundary authentication to partner systems cannot execute if the federation trust is compromised or unavailable.



A compromised token-signing key does not just expose the organization's own relying parties. It potentially exposes every mission partner that trusts the federation. A broken federation configuration does not just prevent internal users from accessing cloud services. It prevents mission partner personnel from accessing the shared systems they depend on for joint operations.



Federation trust is mission infrastructure. Its security is a mission security concern.



1.10.4 CLOUD IDENTITY AS AN EXTENSION OF ENTERPRISE TRUST



Federal adoption of cloud services has extended the enterprise trust boundary into cloud tenants that operate under different administrative models, different monitoring capabilities, and different incident response procedures than on-premises infrastructure. The identities synchronized to cloud tenants, the Service Principals that operate in those tenants, the Conditional Access policies that govern cloud access, and the Managed Identities that authenticate cloud workloads are all extensions of enterprise identity — and all are attack surface.



Cloud identity compromise in a federal environment is not a cloud provider's problem to solve. It is the organization's problem, governed by the same RMF authorities, FISMA obligations, and STIG requirements that govern on-premises identity infrastructure.



1.10.5 CERTIFICATE TRUST AS CRYPTOGRAPHIC AUTHORITY



Every certificate accepted by a federal system as the basis for an authentication decision embeds a trust assertion: "this certificate was issued by a certificate authority we trust, to the identity it claims, for the purpose it asserts." When that assertion fails — because the certificate authority was compromised, because the certificate was issued in error, because the certificate maps to the wrong identity — the authentication decision based on it is wrong.



Certificate trust is cryptographic authority. A certificate authority with an unprotected private key, or certificate templates with exploitable issuance rules, is a compromise of cryptographic authority. The corrective action — revoking the CA, reissuing the hierarchy, retiring exploitable templates — is not a technical cleanup. It is a restoration of cryptographic authority.



1.10.6 GROUP POLICY AS ENTERPRISE CONFIGURATION AUTHORITY



Group Policy reaches every domain-joined system in the enterprise. A GPO linked at the domain root with enforcement can configure every workstation, server, and device in the environment simultaneously. This is enterprise configuration authority: the ability to define, at scale, how every domain-joined system behaves.



An adversary who gains write access to Group Policy Objects and link permissions at the domain level does not need to compromise individual endpoints. They can configure the endpoints they want to reach through the same mechanism the organization uses for legitimate configuration management. A malicious GPO is not malware — it is an administrative action that happens to deliver malicious content.



1.10.7 DIRECTORY DATA AS AUTHORITATIVE IDENTITY MEMORY



The Active Directory database — `NTDS.dit` — is the organization's authoritative identity memory. Every identity that has ever existed in the domain, every credential that has ever been set, every group membership, every delegation configuration, every permission assignment — the history of all of these is embedded in the directory database and its associated transaction logs.



When that database is exposed — through DCSync, through `NTDS.dit` extraction, through Shadow Copy theft — the adversary does not only obtain current credentials. They obtain the history of the identity infrastructure: historical password hashes, historical group memberships, replication metadata that can be used to understand how the directory has changed over time. This information supports not just immediate credential use but long-term strategic analysis of the environment.



1.10.8 WHY IDENTITY RISK MUST BE EXPRESSED IN MISSION TERMS



Table 1-5, presented later in this chapter, maps identity security findings to the federal evidence outputs they should produce. The underlying principle is that identity security findings are not self-interpreting. A finding that says "unconstrained delegation is configured on a server that authenticates domain controllers" is a technical fact. A finding that says "this configuration allows any adversary who compromises this server to obtain Kerberos tickets for domain controller accounts, enabling full domain compromise within the Kerberos ticket lifetime" is an impact statement. A finding that says "this condition, if exploited, would allow an adversary to forge authentication for any user in the domain, including those authorized for classified systems" is a mission risk statement.



Federal practitioners — ISSOs, security control assessors, authorizing officials — need mission risk statements, not just technical facts. This book is designed to help practitioners make that translation.



1.11 GOVERNANCE, AUTHORIZATION, AND EVIDENCE IN IDENTITY SECURITY



Identity security findings in federal environments do not exist in isolation. They exist within a governance structure that determines what action they require, who must act, how the action is documented, and how the organization demonstrates to its authorizing official that the risk has been addressed.



1.11.1 WHY FEDERAL IDENTITY SECURITY MUST PRODUCE EVIDENCE



In a commercial organization, a security finding might produce a remediation task, an updated configuration, and a note in a ticket system. In a federal organization, a finding must produce evidence: evidence that the finding was identified, that its risk was assessed, that remediation action was taken, that the remediation was validated, and that the residual risk was accepted by the appropriate authority or eliminated through additional controls.



This evidence requirement is not bureaucratic overhead. It is accountability: the mechanism by which the organization demonstrates to itself and to its oversight authorities that its security posture is known, managed, and appropriate for the systems and data it protects.



1.11.2 RISK MANAGEMENT FRAMEWORK AS THE CONTROL-VALIDATION STRUCTURE



The Risk Management Framework (RMF), defined by NIST Special Publication 800-37, is the six-step process through which federal systems are secured, assessed, authorized, and monitored: Categorize, Select, Implement, Assess, Authorize, Monitor. For identity security, the RMF context is specific: the identity infrastructure supporting a system is part of the authorization boundary, its security controls must be selected and implemented based on the system's categorization, and continuous monitoring must validate that those controls remain effective.



An identity security finding that connects to a specific NIST SP 800-53 control — IA-2 (Identification and Authentication), AC-2 (Account Management), AU-12 (Audit Record Generation) — can be presented as a control deficiency within the RMF process. That presentation tells the authorizing official precisely where the gap is, what policy requires, and what must be done to close it.



1.11.3 FISMA AS THE FEDERAL SECURITY ACCOUNTABILITY FOUNDATION



The Federal Information Security Modernization Act of 2014 establishes the accountability framework within which federal information security programs operate. FISMA requires each agency to develop, document, and implement an agency-wide program for information security, including for identity infrastructure. The head of each agency is accountable for implementation. The Chief Information Security Officer is accountable for oversight. System owners and ISSOs are accountable for implementation at the system level.



Identity security is not separable from FISMA compliance. An identity system that is not authorized to operate, or that operates outside its authorization boundary, or that has identity-related control deficiencies that are not documented in Plans of Action and Milestones (POA\&Ms), is a FISMA accountability problem, not just a technical problem.



1.11.4 STIGS AND SRGS AS TECHNICAL CONFIGURATION EVIDENCE



DISA Security Technical Implementation Guides (STIGs) and Security Requirements Guides (SRGs) are the technical configuration standards for federal systems, including Active Directory, Active Directory Certificate Services, and Windows Server. STIG compliance — assessed through automated checking tools, manual verification, and authorized exception documentation — provides the evidentiary basis for the Implement step of the RMF and produces artifacts that support authorization decisions.



STIGs are a floor, not a ceiling. STIG compliance establishes that a system meets baseline configuration requirements. It does not establish that the system is secure against advanced identity-based attacks. The combination of STIG compliance and attack-pathway analysis provides a more complete security posture assessment than either alone.



1.11.5 INFORMATION ASSURANCE VULNERABILITY ALERT AS OPERATIONAL VULNERABILITY-RESPONSE DRIVERS



DISA Information Assurance Vulnerability Alerts (IAVAs) are mandatory responses to significant vulnerabilities affecting DoD systems. IAVAs related to identity infrastructure — Kerberos vulnerabilities, NTLM authentication weaknesses, Active Directory privilege escalation paths, certificate validation failures — require documented response within specified timelines. Tracking and responding to IAVAs in the identity infrastructure is an operational requirement that connects technical vulnerability management to authorization evidence.



1.11.6 EMASS AS THE AUTHORIZATION EVIDENCE REPOSITORY



The Enterprise Mission Assurance Support Service (eMASS) is the DoD's primary system of record for RMF artifacts: system categorizations, security plans, control implementation statements, assessment results, POA\&Ms, and authorization decisions. For identity security findings, eMASS is the destination for the evidence that demonstrates control implementation and validates remediation. Understanding how to translate identity security findings into eMASS artifacts — control assessments, POA\&M entries, continuous monitoring results — is a practical skill that this book addresses through assessment questions in later chapters.



1.11.7 PLANS OF ACTION AND MILESTONES AS THE RISK-TRACKING ACCOUNTABILITY MECHANISM



A Plan of Action and Milestones (POA\&M) is a document that tracks security weaknesses that have been identified but not yet fully remediated, the plan for remediation, the resources required, and the timeline for completion. Identity security findings that cannot be immediately remediated — because of operational constraints, resource limitations, or technical complexity — must be documented in POA\&Ms to be tracked and managed within the RMF process.



A POA\&M is not a license to accept risk indefinitely. It is a structured commitment to addressing identified risk within a defined timeline, with accountability for that commitment resting with the system owner and the Information System Security Officer.



1.11.8 CONTINUOUS MONITORING AS IDENTITY SECURITY SUSTAINMENT



Authorization is not a one-time event. It is a continuous process of maintaining knowledge of the security posture of authorized systems and acting when that posture degrades. For identity infrastructure, continuous monitoring means ongoing collection and analysis of security-relevant events from domain controllers, certificate authorities, federation services, and cloud identity platforms; ongoing assessment of configuration drift against established baselines; and ongoing review of privileged access and account management.



The continuous monitoring outputs for identity infrastructure — event logs, configuration assessment results, privileged access reviews, certificate inventory reviews — are both operational security inputs and RMF evidence outputs.



1.11.9 WHY GOVERNANCE MUST BE INFORMED BY ATTACK PATHWAYS



Governance processes that are not informed by attack-pathway awareness will consistently underestimate risk. An account management review that checks for accounts without recent logons does not identify service accounts with Kerberoastable SPNs and old passwords. An access review that checks for privileged group memberships does not identify control pathways that provide privileged outcomes without privileged group membership. A configuration assessment that checks STIG settings does not identify certificate templates with exploitable issuance rules.



Governance informed by attack-pathway awareness adds these questions to its standard inventory: What can an adversary with this account do? What does this misconfiguration enable? What control pathways lead from this configuration to a privileged outcome? That augmented governance provides a more complete and more actionable picture of identity security risk.



1.12 THE BOOK'S OPERATING MODEL



This book follows a specific sequence in how it presents each subject. Understanding the sequence helps the reader anticipate why each chapter appears where it does.



1.12.1 ARCHITECTURE BEFORE ATTACK



Part I establishes the architecture — forests, domains, trusts, protocols, certificate services, federation, hybrid identity, policy delivery, and directory data — before Part II examines how each architectural element is attacked. This is not simply pedagogical sequencing. It is the premise of the book: you cannot defend what you do not understand, and you cannot understand attack pathways without first understanding the architecture those pathways traverse.



1.12.2 PROTOCOLS BEFORE EXPLOITATION



The authentication protocols — Kerberos, NTLM, LDAP, the Kerberos extensions that enable PIV/CAC authentication — are examined in Part I before the techniques that exploit them are examined in Part II. Kerberoasting is not comprehensible without understanding the Kerberos TGS-REQ/TGS-REP exchange. Pass-the-Hash is not comprehensible without understanding how the NT hash functions as authentication material. Golden Tickets are not comprehensible without understanding the krbtgt key's role in the Kerberos AS-REP.



1.12.3 IDENTITY GOVERNANCE BEFORE AUTHORIZATION CLAIMS



The FICAM and DoD ICAM frameworks, the assurance level model, the credential and federation governance requirements, and the RMF evidence structure are established in Part I before the governance evidence requirements are applied in Part III's defensive chapters. Governance is not a concluding afterthought — it is the framework within which all technical identity security work occurs.



1.12.4 ASSESSMENT BEFORE OFFENSIVE VALIDATION



The baseline engineering and assessment methodology established in the final chapter of Part I provides the starting state against which offensive validation in Part II is measured. Assessment tells you what the controls say. Offensive validation tells you whether they work.



1.12.5 OFFENSIVE TRADECRAFT BEFORE DEFENSIVE ENGINEERING



Part II precedes Part III because defensive engineering without understanding offensive tradecraft is incomplete. A detection rule that does not account for the specific telemetry signature of a Kerberoasting attack will not detect it. A hardening control that does not address the specific precondition for a Golden Ticket attack will not prevent it. Offense before defense is not only pedagogical preference — it is the sequence that produces the most effective defense.



1.12.6 DETECTION BEFORE RESPONSE



Detection engineering — building the telemetry and correlation capability to identify adversary activity — is developed in Part III before incident response procedures. A response that is not informed by what detection can see will miss the attack paths it is intended to interrupt.



1.12.7 RECOVERY BEFORE TRUST RESTORATION



Recovery from identity compromise — the technical procedures for containing and remediating specific attack techniques — is addressed in Part III before trust restoration. Technical recovery establishes that the adversary has been evicted and the vulnerable conditions remediated. Trust restoration — the process of demonstrating to stakeholders, authorizing officials, and mission partners that the identity infrastructure can be relied upon again — follows from technical recovery.



1.12.8 FUTURE WARFARE AFTER CURRENT-STATE ENGINEERING



Part IV addresses the future of identity-centric defense and warfare after the current-state engineering, attack, detection, and recovery techniques have been established in Parts I through III. Future-oriented content without current-state grounding is speculation. Grounded future-oriented content — built on a thorough understanding of how identity trust systems work and fail today — is analysis.



1.13 HOW THIS BOOK IS ORGANIZED

1.13.1 PART I — FOUNDATIONS AND TERRAIN



Part I establishes the conceptual and technical foundation for everything that follows. Figure 1-6 maps the book's four parts to the operational mission phases they support. It examines Active Directory architecture, the networking and protocol substrate, federal identity governance, authentication protocols in depth, enterprise identity services including certificate authorities and federation, policy delivery and the directory data store, cross-domain directory services, and the assessment and baseline engineering methodology that connects foundational knowledge to operational practice.



1.13.2 PART II — THE ACTIVE DIRECTORY IDENTITY ATTACK LIFECYCLE



Part II follows the adversary through the seven-stage identity attack lifecycle: passive reconnaissance, active enumeration, initial identity acquisition, credential acquisition, identity authority expansion, enterprise identity mobility, and persistence and domain dominance. Each stage is examined through the specific techniques adversaries use, the tooling that implements those techniques, the specific telemetry each technique produces, and the initial detection signals each generates.



1.13.3 PART III — DEFENSE, DETECTION, RECOVERY, AND GOVERNANCE



Part III mirrors Part II from the defensive perspective. It examines privilege isolation and Tier 0 architecture, hardening of the exploited attack surfaces, detection engineering for each attack category, identity forensics and incident response, recovery procedures for each class of compromise, and the governance and evidence structure that connects technical security to federal authorization requirements.



1.13.4 PART IV — OPERATIONAL LESSONS AND THE FUTURE OF IDENTITY-CENTRIC DEFENSE AND WARFARE



Part IV synthesizes the operational lessons from the preceding parts, examines the field conditions — service account sprawl, documentation drift, STIG checkbox culture, SOC-to-identity-team disconnects — that create the gaps adversaries exploit, and looks ahead to the identity battlespace as it is being shaped by artificial intelligence-assisted attack and defense, machine identity governance at scale, passkey and FIDO2 adoption, and Zero Trust modernization.



1.13.5 HOW CHAPTER-LEVEL MITRE ATT\&CK FRAMEWORK MAPPINGS WILL BE USED



Each chapter in Part II maps its techniques to MITRE ATT\&CK technique identifiers. This mapping serves two functions: it connects the techniques described in this book to the broader adversary-behavior taxonomy used by the security community for threat intelligence sharing and detection rule development, and it provides a reference that allows practitioners to locate additional information about each technique within the ATT\&CK knowledge base.



1.13.6 HOW CHAPTER-LEVEL STANDARDS AND GUIDANCE SECTIONS WILL BE USED



Each chapter identifies the federal standards, frameworks, and guidance that apply to the subjects covered. This section tells the reader which NIST Special Publications, DISA STIGs, OMB memoranda, or DoD instructions govern the configuration, monitoring, or evidence requirements for the chapter's subject — connecting technical content to the governance framework within which federal practitioners must operate.



1.13.7 HOW OFFENSIVE AND DEFENSIVE CONCEPTS WILL BE PAIRED



Each attack chapter in Part II has a corresponding defense chapter in Part III that addresses detection, hardening, and recovery for the same attack techniques. This pairing is not simply organizational — it reflects the analytical approach of the book: every offensive technique is a defensive engineering problem, and every defensive control is a response to a specific offensive technique.



1.13.8 HOW ATTACKER AND DEFENDER PERSPECTIVES WILL BE USED



Beginning with Part II, each chapter opens with a brief attacker journal entry — a first-person perspective from the relevant attacker archetype — that grounds the chapter's technical content in operational reality. Part III chapters open with the corresponding defender perspective. These journal entries are not fiction. They are distillations of the practitioner experience that informs this book, presented in a form that makes the operational stakes of each technique concrete before the technical analysis begins.



1.14 WHAT THIS BOOK IS ABOUT AND WHAT IT IS NOT

1.14.1 THIS BOOK IS AN IDENTITY SECURITY ENGINEERING REFERENCE



Identity security engineering is the practice of designing, implementing, assessing, and validating security controls for identity infrastructure — not as a compliance exercise but as a defense against real adversary techniques. This book is a reference for that practice: it establishes the technical foundation, maps the attack surface, develops the defensive engineering requirements, and connects both to the federal governance framework that makes security decisions accountable.



1.14.2 THIS BOOK IS AN OFFENSIVE AND DEFENSIVE ACTIVE DIRECTORY SECURITY GUIDE



For practitioners who conduct Active Directory security assessments, red team exercises, or penetration tests: this book provides the attack technique knowledge, operational context, and telemetry signatures needed to conduct and interpret those assessments in federal and defense environments, with the federal governance context that makes findings actionable.



For practitioners who defend Active Directory environments: this book provides the attack knowledge needed to build effective defenses, the detection engineering guidance needed to build telemetry that finds adversaries, and the recovery procedures needed to restore trusted identity infrastructure after compromise.



1.14.3 THIS BOOK IS A FEDERAL AND MILITARY IDENTITY TRUST ANALYSIS HANDBOOK



For ISSOs, security control assessors, authorizing officials, and governance practitioners: this book provides the technical depth needed to evaluate identity security findings, translate them into mission risk terms, connect them to RMF control structures, and produce the evidence that authorization decisions require. The assessment questions at the end of each Part I chapter, and the governance integration throughout Part III, are designed specifically for this audience.



1.14.4 THIS BOOK IS NOT ANOTHER ACTIVE DIRECTORY ADMINISTRATION MANUAL



There are excellent books that teach Active Directory administration: how to deploy domain controllers, how to configure sites and replication, how to manage Group Policy, how to troubleshoot Kerberos authentication problems. This book does not replicate that material. It assumes working knowledge of Active Directory administration and builds security engineering capability on top of that foundation.



1.14.5 THIS BOOK IS NOT ANOTHER ACTIVE DIRECTORY PENETRATION TESTING PLAYBOOK



There are books and courses that provide hands-on guidance for Active Directory penetration testing — step-by-step instructions for running specific tools against specific targets. This book covers offensive techniques in depth, but it does so in the context of understanding the underlying mechanisms, the federal governance implications, the defensive countermeasures, and the evidence requirements that make the technique relevant to practitioners across the red team, blue team, and governance spectrum.



1.14.6 THIS BOOK IS NOT ANOTHER ACTIVE DIRECTORY SECURITY COMPLIANCE CHECKLIST



Compliance checklists are necessary and useful. This book is not one. The analytical approach throughout this book — from architecture through attack lifecycle through defense engineering through recovery — is designed to produce security assurance that goes beyond compliance: the demonstrated ability to defend, detect, contain, and recover from sophisticated adversarial activity targeting the federal identity trust system.



1.14.7 WHY THOSE BOUNDARIES AND DISTINCTIONS MATTER



Every book represents a choice about what to include and what to defer to other resources. The boundaries described above reflect a deliberate choice to fill the gap this author identified in the existing literature: a book that treats Active Directory and its connected identity services as a federal mission-critical identity trust system, and that examines offense, defense, governance, and recovery as an integrated discipline — rather than as separate books for separate audiences.



1.15 SUMMARY AND TRANSITION

1.15.1 KEY CONCEPTS REVIEWED



Chapter 1 has established the conceptual foundation for the entire book. The key propositions established here inform every chapter that follows.



1.15.2 ACTIVE DIRECTORY AS IDENTITY TRUST INFRASTRUCTURE



Active Directory is not merely a directory service. It is one participant in a federal identity trust system that extends through certificate authorities, federation services, cloud identity platforms, authoritative attribute sources, and mission-partner relationships. The correct unit of analysis for federal and defense identity security is not the domain — it is the identity trust system.



1.15.3 IDENTITY AS THE BATTLEFIELD



Modern adversaries targeting federal and defense networks focus on identity before systems, credentials before exploits, and trust abuse before noisy attacks. They prefer techniques that operate through the environment's own legitimate mechanisms — Kerberos, certificate authentication, federation assertions — because those techniques are quiet, persistent, and difficult to distinguish from normal operation. Defending against them requires understanding them.



1.15.4 ASSUME BREACH AS AN ENGINEERING MODEL



Assume Breach is the design posture that produces effective detection, containment, and recovery capabilities. It does not abandon prevention — it extends security engineering to account for the moment prevention fails, and designs the detection, containment, and recovery functions that limit the impact of that failure.



1.15.5 FROM CYBER KILL CHAIN TO IDENTITY KILL CHAIN



The traditional cyber kill chain does not adequately describe credential-based intrusions into Active Directory environments. The identity kill chain — passive reconnaissance, active enumeration, initial identity acquisition, credential acquisition, identity authority expansion, enterprise identity mobility, persistence and domain dominance — provides the framework that structures Part II of this book and informs the defensive design in Part III.



1.15.6 FEDERAL GOVERNANCE AS A SECURITY REQUIREMENT



Federal identity security findings must produce evidence: control assessment results, POA\&M entries, continuous monitoring outputs, and mission risk statements that authorizing officials can act on. The RMF, FISMA, STIGs, IAVAs, eMASS, and continuous monitoring are not separate from identity security — they are the governance structure that makes identity security decisions accountable.



1.15.7 WHY CHAPTER 2 MOVES INTO THE ARCHITECTURE OF AUTHORITY



Chapter 1 has established why identity trust matters and what it means for the identity trust system to fail. Chapter 2 examines the architecture that gives the identity trust system its shape: the forests, domains, trusts, schema, Organizational Units, domain controllers, and administrative boundaries that organize Active Directory's authority. Where Chapter 1 explains why identity trust matters, Chapter 2 explains how Active Directory organizes and concentrates that trust — and why the architecture itself is the map that both adversaries and defenders must be able to read.



INCLUDED FIGURES



Figure 1-1. Active Directory As Part of the Federal Identity Trust System \[Diagram to be produced: Active Directory domain at center; surrounding components include Certificate Authority / FPKI, Active Directory Federation Services / Token-Signing Infrastructure, Microsoft Entra ID / Synchronization Bridge, Mission Partners / Coalition Access, Authoritative Attribute Sources, and Privileged Access Infrastructure. Arrows show trust flow direction.]



Figure 1-2. Domain Boundary Versus Identity Trust System Boundary \[Diagram to be produced: Inner boundary labeled "Domain / Forest" containing domain controllers, `NTDS.dit`, Group Policy, Kerberos; outer boundary labeled "Identity Trust System" containing certificate authorities, federation services, cloud identity, mission-partner relationships, and synchronization infrastructure. Attack paths crossing both boundaries illustrated.]



Figure 1-3. Administrative View Versus Attacker Control-Path View \[Diagram to be produced: Left panel shows organizational chart / administrative hierarchy. Right panel shows same environment as a permission graph with control pathways highlighted — GenericWrite, WriteDACL, ForceChangePassword edges connecting low-privilege nodes to high-privilege targets.]



Figure 1-4. From Cyber Kill Chain to Identity Kill Chain \[Diagram to be produced: Two parallel chains. Left: traditional Lockheed Martin Kill Chain stages. Right: Identity Kill Chain equivalents — Passive Reconnaissance, Active Enumeration, Initial Identity Acquisition, Credential Acquisition, Identity Authority Expansion, Enterprise Identity Mobility, Persistence and Domain Dominance.]



Figure 1-5. Identity Trust Failure as Mission Risk \[Diagram to be produced: Identity trust system with a compromise point indicated; arrows show how compromise propagates to mission-essential functions — authentication for classified systems, federation with mission partners, cloud service access, certificate trust for encrypted communications.]



Figure 1-6. Book Structure: Architecture, Offense, Defense, Recovery, and Warfare \[Diagram to be produced: Four-part book structure mapped to mission phases — Part I (Understand the Terrain), Part II (Follow the Adversary), Part III (Build and Validate the Defense), Part IV (Prepare for What Comes Next).]



INCLUDED TABLES



Table 1-1 Active Directory component roles in the overall identity trust system



AD Component	Identity Function	Trust Produced	Tier Level	Attack Surface

Domain Controllers	Authentication authority; ticket issuance; directory enforcement	Kerberos authentication trust for all domain principals	Tier 0	Credential exposure; DCSync; replication abuse

`NTDS.dit` Database	Authoritative identity data store; credential storage	Source of record for all domain identities and credentials	Tier 0	`NTDS.dit` extraction; DCSync; VSS abuse

Group Policy / SYSVOL	Configuration authority for all domain-joined systems	Enterprise configuration trust	Tier 0 (policy objects); Tier 1 (delivery)	Malicious GPO; SYSVOL credential exposure; logon script abuse

Active Directory Certificate Services	Certificate issuance and enrollment for domain identities	Cryptographic identity binding; PIV/CAC authentication	Tier 0	ESC1–ESC16 template abuse; CA key exposure

Active Directory Federation Services	Cross-boundary identity assertion; claims-based authentication	Federation trust to relying parties and mission partners	Tier 0	Token-signing key theft (Golden SAML); DKM exposure

krbtgt Account	KDC signing identity; TGT encryption key	Kerberos domain-wide authentication trust	Tier 0	Golden Ticket; key material exposure

Privileged Groups	Administrative authority delegation	Administrative access to domain resources	Tier 0 (DA/EA); Tier 1	Group membership abuse; SID History; AdminSDHolder

Trust Relationships	Cross-domain and cross-forest authentication	Inter-organizational identity assertion	Tier 1	SID filtering bypass; trust exploitation; lateral traversal

Synchronization / Entra Connect	On-premises to cloud identity bridge	Hybrid identity trust	Tier 0	Sync account DCSync equivalent; writeback abuse



Table 1-2 Domain-centric view versus identity trust system view



Dimension	Domain-Centric View	Identity Trust System View

Primary security boundary	Forest or domain	The complete trust-extending infrastructure

Key assets to protect	Domain controllers and `NTDS.dit`	Domain controllers, CAs, federation services, cloud identity, sync accounts

Authentication scope	On-premises Kerberos and NTLM	Kerberos + certificates + federation tokens + cloud tokens + hybrid

Credential types	NT hashes and Kerberos tickets	NT hashes, tickets, certificates, tokens, PRTs, refresh tokens, API keys

Attack surface	Domain membership and group rights	Permission graphs, trust chains, certificate templates, federation configs, cloud roles

Compliance reference	STIG for Active Directory	STIGs + FICAM + RMF + FPKI policy + DoD ICAM + OMB memoranda

Mission dependency	On-premises domain availability	Cross-boundary federation, cloud access, mission partner authentication, classified fabric access

Recovery scope	Domain controller restoration	Directory restoration + CA re-issuance + federation trust repair + cloud identity recovery



Table 1-3 Attacker questions versus defender questions



Topic	Attacker Question	Defender Question

Account inventory	What accounts have SPNs, old passwords, or excessive permissions?	Do all accounts have appropriate group memberships and recent password resets?

Permission relationships	What control pathways lead from this account to domain admin?	Are all privileged permissions assigned per the least-privilege policy?

Certificate templates	Which templates allow me to request a certificate as any user?	Are all templates reviewed for enrollment permissions and EKU combinations?

Federation configuration	Can I extract the token-signing key through the DKM container?	Is the DKM container access-restricted and audited?

Trust relationships	What does this forest trust enable me to reach?	Are trust relationships documented with current business justification?

Cloud configuration	What cloud roles or Service Principal permissions can I escalate through?	Are all cloud roles governed by PIM and reviewed quarterly?

Detection capability	What operations can I perform that leave no distinctive log signature?	What attack techniques do we have no detection rule for?

Recovery posture	Can I persist through a domain controller rebuild?	Do we have recovery procedures for identity trust compromise, tested and current?



Table 1-4 Traditional cyber kill chain versus Active Directory identity kill chain



Stage	Traditional Cyber Kill Chain	Active Directory Identity Kill Chain

1	Reconnaissance	Passive Identity Reconnaissance — external exposure, federation metadata, DNS, certificate transparency

2	Weaponization	Active Enumeration — domain objects, trusts, SPNs, ACLs, templates, delegation, cloud

3	Delivery	Initial Identity Acquisition — spraying, phishing, MFA fatigue, OAuth abuse

4	Exploitation	Credential Acquisition — Kerberoasting, LSASS, cached creds, certificate theft, token theft

5	Installation	Identity Authority Expansion — ACL abuse, delegation exploitation, ESC paths, cloud role abuse

6	Command and Control	Enterprise Identity Mobility — PtH, PtT, NTLM relay, cross-domain traversal, cloud pivot

7	Actions on Objectives	Persistence and Domain Dominance — DCSync, DCShadow, Golden Ticket, Golden SAML, AdminSDHolder



Table 1-5 Identity security findings and federal evidence outputs



Finding Type	Technical Description	Mission Risk Statement	RMF Control	Evidence Output

Kerberoastable service accounts	Service accounts with SPNs and human-set passwords permit offline credential recovery	Adversary with initial access can silently obtain service account credentials and authenticate to dependent systems	IA-5 (Authenticator Management)	POA\&M entry; gMSA migration plan; AES enforcement evidence

Unconstrained delegation	Servers configured for unconstrained delegation store TGTs for authenticating users	Domain controller authentication to delegating servers exposes DC credentials to adversary on that server	SC-8 (Transmission Confidentiality)	POA\&M entry; delegation audit results; remediation evidence

Exploitable certificate templates	Templates with enrollee-supplied subject and client authentication EKU permit identity impersonation	Any enrolled user can obtain a certificate authenticating as any domain identity including administrators	IA-5, SC-17	POA\&M entry; template audit results; template remediation evidence

Excessive federated trust scope	Relying party trusts accept overly broad claim sets or insufficiently filtered identity assertions	Federation trust extends attack surface to mission partners and cloud services beyond the local domain	SC-28, IA-8	Federation agreement review; claim rule audit; POA\&M

Stale privileged accounts	Dormant domain administrator accounts with recent password age	Stolen credential for dormant high-privilege account provides domain administrator access with reduced detection likelihood	AC-2 (Account Management)	Account review results; deprovisioning records; POA\&M



Table 1-6 Book parts and the operational purpose they serve



Part	Title	Operational Purpose	Primary Audience

I	Foundations and Terrain	Establish architecture, protocol, governance, and assessment knowledge as the prerequisite for offense and defense	All practitioners; ISSOs; engineers new to the subject

II	The Active Directory Identity Attack Lifecycle	Develop adversary-perspective analytical capability by examining each stage of the identity attack lifecycle in operational detail	Red team; penetration testers; security engineers; threat hunters

III	Defense, Detection, Recovery, and Governance	Develop defensive engineering, detection, incident response, and governance evidence capabilities aligned to the attack lifecycle	Blue team; ISSOs; security engineers; incident responders; authorizing officials

IV	Operational Lessons and the Future	Synthesize field lessons, address organizational conditions that enable persistent risk, and examine the future identity battlespace	Senior practitioners; security leaders; program managers; assessors

INCLUDED CASE STUDIES

Case Study 1-1. When a Domain Compromise Becomes a Mission Trust Failure



Scenario



In a large federal enterprise environment, an intrusion was discovered during incident response. The initial compromise had occurred several weeks before detection. The adversary had entered through a phishing campaign targeting service desk personnel, obtained credentials for a domain user account through credential theft, and used that foothold to enumerate the directory and identify a misconfigured delegation path that eventually yielded domain controller access.



By the time the intrusion was detected, the adversary had obtained the krbtgt key material. Golden Tickets had been issued. The specific accounts used were not immediately known.



Identity Trust Failure



The failure was not, primarily, technical. The domain controller was patched. The initial account was not privileged. The adversary's path to domain compromise used a delegation configuration that existed in the environment for a legitimate but since-retired operational purpose, and a certificate template with permissive enrollment permissions that had never been reviewed since its creation.



The identity trust failure was this: once the krbtgt key material was known to the adversary, the organization could no longer confidently determine which authentication events were legitimate. Any account could be impersonated. Any service could be accessed. Administrative actions taken during the response window could not be fully trusted.



Why It Mattered



The environment supported mission-critical identity dependencies: other components authenticated through federation agreements with this domain. Those partners could not be fully confident that their federated sessions were not being observed or replayed. Incident response required coordinating with those partners, notifying them of the trust compromise, and temporarily restricting federation access — which affected mission operations that depended on cross-boundary authentication.



The recovery timeline was measured not in hours of system restoration but in days of identity trust validation: krbtgt double-reset, domain controller validation, certificate template audit, delegation configuration review, federation partner notification, and staged reauthorization of federated access.



Attacker View



The adversary saw a standard Windows domain with legacy configuration artifacts: a delegation setting nobody had reviewed, a certificate template with broad enrollment permissions, a service account whose SPN made it roastable. None of these required a zero-day. The environment was patched and STIG-compliant. The attack path was entirely through the identity trust system.



Defender View



The defender should have validated not just the configuration of individual controls but the attack-path implications of combinations: that the delegation configuration plus the certificate template plus the service account created a pathway from initial access to domain dominance without any exploit. That validation requires attack-pathway analysis that compliance checking alone does not perform.



Lesson Learned



Domain compromise is not a technical event followed by a technical recovery. When the identity trust system is compromised at the Tier 0 level, the organization loses the ability to trust its own authentication infrastructure. Recovery must address that trust loss systematically, not just patch the technical gap that enabled entry. Mission dependencies on that identity infrastructure amplify the impact — and must be part of both the recovery plan and the initial risk assessment.



Case Study 1-2. When Compliance Evidence Failed to Reveal an Attack Path



Scenario



During an authorized assessment of a defense environment, the team reviewed the system's authorization package. The package was recent. STIG compliance was documented at over 95 percent. Privileged group memberships had been reviewed six months prior. Continuous monitoring was in place. The authorization was current.



The assessment team was then asked to evaluate whether the environment was actually secure against identity-based attack paths — not whether it was compliant, but whether compliance translated to security.



Identity Trust Failure



Within two hours of beginning enumeration from a low-privilege domain account, the team identified:



A service account with a registered SPN, a password last set four years ago, and no protected users or AES enforcement applied. The account was Kerberoastable. Its password was in a standard wordlist.



An account with GenericWrite permission on a computer object that was part of the domain controller management tier. The permission was an inheritance artifact from a Group Policy application that had since been changed, but the ACL had not been cleaned up.



A certificate template with the CT\_FLAG\_ENROLLEE\_SUPPLIES\_SUBJECT flag set, a Client Authentication EKU, and Authenticated Users in the enrollment rights. The template had been created years before and never reviewed.



None of these findings appeared in the compliance documentation. The service account password age check was looking for accounts over 90 days — not specifically for service accounts with SPNs. The ACL review had checked privileged group membership, not inheritance artifacts on computer objects. The certificate template had never been included in the scope of any configuration review.



Why It Mattered



The authorization was current and accurate — as a compliance document. As a security assurance document, it was incomplete. The attack paths it missed were not exotic. They were the standard paths that any competent adversary would identify within hours of initial access.



The difference between the compliance picture and the security picture was not a failure of the people who conducted the compliance review. It was a failure of the review methodology: compliance processes that check for known-good configurations without analyzing the attack-path implications of what they find will consistently miss control pathways that compliance settings do not directly govern.



Attacker View



The adversary sees a compliant environment and begins enumerating it anyway, because compliance does not close attack pathways. Within a short enumeration window, the three findings above create a reliable path from low-privilege initial access to domain administrator through the certificate template, and to the management tier through the ACL inheritance. The path required no exploits, no CVEs, and no techniques that would appear unusual in the log data.



Defender View



The assessment questions the defender should have been asking: Is every service account with a registered SPN using a group Managed Service Account or enforcing AES with a strong random password? Is every ACL entry on Tier 0 objects traceable to a current, documented authorization? Is every certificate template enrollment permission reviewed and owned? The answers to these questions produce a security picture that the STIG compliance questions do not.



Lesson Learned



Compliance evidence that does not include attack-pathway analysis describes what controls are present, not whether those controls are sufficient. The governance obligation in federal environments is not only to document control implementation but to validate that implemented controls actually prevent, detect, or contain the attack techniques they are designed to address. That validation requires the analytical posture this book is designed to develop.



Case Study 1-3. When Federation Extended the Blast Radius Beyond the Domain



Scenario



In a command environment with federated access requirements, incident responders were called to investigate anomalous activity on a system that appeared, from initial indicators, to be limited to a single domain. The investigation began as a standard domain compromise response.



As the investigation progressed, it became clear that the scope of the compromise was not limited to the local domain. The adversary had obtained the token-signing certificate's private key from the Active Directory Federation Services deployment. Using that key, they had issued assertions for multiple identities — including identities that existed only in the federation, with no corresponding local domain account — and had accessed relying-party applications in a partner environment through those assertions.



Identity Trust Failure



The local domain was not the full attack surface. The Active Directory Federation Services deployment that served the domain was connected to mission partner systems through federation agreements. The token-signing key that was compromised was the trust anchor for all of those relationships simultaneously.



The technical compromise was the token-signing private key. The identity trust failure was federation-wide: every relying party that trusted this federation, and every identity that could be asserted through it, was within the adversary's reach — not just the identities in the local domain.



Why It Mattered



The incident response had to expand beyond the local domain immediately upon discovery of the federation compromise. Partner organizations had to be notified. Federated sessions had to be revoked or treated as suspect. The token-signing certificate had to be rotated — twice, because a single rotation leaves the old certificate valid through the rollover window — and every relying party had to update its trust metadata.



The blast radius of the compromise was not determined by how many accounts existed in the local domain. It was determined by how many systems and partners trusted the federation. The federation extended that radius significantly beyond what a traditional domain-only analysis would have anticipated.



Attacker View



The adversary targeted the federation infrastructure specifically because it provided leverage beyond the local domain. The token-signing key was more valuable than any individual account credential — it provided the ability to authenticate as any identity the federation could assert, to any partner system that trusted it, without leaving authentication artifacts in the local domain's event logs.



Defender View



The defender should have treated the Active Directory Federation Services token-signing key with Tier 0 rigor: protected by a Hardware Security Module, with the DKM container access-restricted and audited, and with a documented incident response procedure that included the two-rotation requirement and partner notification protocol. The assessment of federation security should have included validation that these controls were in place before an incident required them.



Lesson Learned



The domain is a real boundary. It is not the whole identity trust system. Federation relationships extend the identity trust boundary to every relying party that trusts the federation, and the blast radius of a federation infrastructure compromise is determined by the scope of those relationships — not by the size or complexity of the local domain. Identity security assessment must include the federation infrastructure as a first-class security target, not as an afterthought to domain security.



INCLUDED LABS AND EXERCISES

Exercise 1-1. Draw the Identity Trust System Around a Domain



Objective: Develop the analytical habit of mapping the complete identity trust system rather than treating the domain as the full scope of analysis.



Instructions: Select an Active Directory environment you have authorized access to assess. Starting from the domain, map outward to identify every component that participates in the identity trust system: certificate authorities and their chains of trust, federation service configurations and their relying parties, cloud identity synchronization relationships, mission-partner or cross-organization trust relationships, and authoritative attribute sources. Document the trust direction for each relationship. Identify which components are Tier 0.



Discussion Questions:



How many components outside the domain participate in the identity trust system?

Which of those components, if compromised, would affect authentication inside the domain?

Which trust relationships have documented business justification and governance?

Where is the identity trust boundary actually located, and how does it compare to the administrative domain boundary?

Exercise 1-2. Translate an Administrative Diagram Into an Attacker Control-Pathway Diagram



Objective: Develop the ability to read an administrative structure as an attack surface.



Instructions: Obtain or create an administrative diagram for an Active Directory environment: the organizational unit structure, the privileged group memberships, the service accounts and their SPNs. Using BloodHound, Adalanche, or a manual ACL review, produce a permission-graph analysis of the same environment. Identify the control pathways that the permission graph reveals and that the administrative diagram does not show.



Discussion Questions:



How many control pathways from unprivileged positions to Tier 0 targets exist in the environment?

Which of those pathways are the result of explicit configuration decisions, and which are inheritance artifacts?

Which pathways would not appear in a compliance review of privileged group membership?

How would you prioritize remediation across the identified pathways?

Exercise 1-3. Build an Assume-Breach Question Set for an Active Directory Environment



Objective: Apply the Assume Breach posture to identity security assessment.



Instructions: Working from the premise that an adversary has established a low-privilege foothold in the domain as an authenticated domain user (but not a privileged account), develop a question set that maps the attack surface from that starting position: Which service accounts are Kerberoastable? Which certificate templates allow exploitation from this access level? Which ACLs on high-value objects can be reached from this position? What does the adversary see in the first enumeration pass? What detection rules would fire during that enumeration?



Discussion Questions:



How quickly can the attack surface be mapped from an initial foothold?

Which findings are detectable in the current logging configuration, and which are not?

Which controls, if implemented, would close the most significant pathways?

How do the findings compare to the organization's current compliance documentation?

Exercise 1-4. Map a Simple Identity Attack Pathway to Mission Risk



Objective: Practice the translation from technical finding to mission risk statement.



Instructions: Identify one specific technical finding in an Active Directory environment — a Kerberoastable service account, a misconfigured certificate template, an unconstrained delegation configuration, or an excessive ACL entry. Write three descriptions of the same finding:



A technical description (what the finding is, technically)

An attack pathway description (what an adversary can do with this finding, step by step)

A mission risk statement (what mission functions are at risk, and what the impact would be if exploited)



Discussion Questions:



What information is present in the mission risk statement that is absent from the technical description?

How does the mission risk statement change the urgency of remediation compared to a purely technical description?

Which description is most useful for an ISSO preparing a POA\&M entry? For a system owner briefing? For an authorizing official decision?

Exercise 1-5. Identify Which Evidence Would Support an RMF Identity Finding



Objective: Connect identity security findings to the federal governance evidence structure.



Instructions: Select three identity security findings of different types — one related to credential management, one related to access control, one related to audit logging. For each finding, identify: the specific NIST SP 800-53 control it violates or weakens, what evidence would be required to document the finding in an RMF assessment, what remediation evidence would be required to close the finding, and what a POA\&M entry for the finding would contain.



Discussion Questions:



How does the RMF evidence requirement change the way you document a finding?

Which types of identity security findings are most difficult to document within the RMF control structure, and why?

How does the governance accountability structure change the prioritization of remediation?

MITRE ATT\&CK FRAMEWORK COVERAGE IN THIS CHAPTER



This chapter introduces the MITRE ATT\&CK framework as the adversary-behavior mapping layer used throughout the book. No specific ATT\&CK techniques are applied in this chapter; it functions as conceptual preparation for technique-level mapping beginning in Chapter 9 (Passive Identity Reconnaissance) and continuing through all Part II chapters.



The following ATT\&CK tactic categories are introduced conceptually in this chapter as components of the identity kill chain: Reconnaissance (TA0043), Discovery (TA0007), Credential Access (TA0006), Privilege Escalation (TA0004), Lateral Movement (TA0008), Persistence (TA0003), Defense Evasion (TA0005), and Impact (TA0040).



LESSONS LEARNED AND KEY TAKEAWAYS

Active Directory security is identity trust security. The domain is the center, not the boundary, of the federal identity trust system.

The domain is necessary but not sufficient as the primary unit of analysis. Certificate authorities, federation services, cloud identity platforms, synchronization bridges, and mission-partner relationships all participate in the identity trust system and all require security engineering.

Attackers follow trust relationships. The attack paths that matter in advanced intrusions into federal and defense networks do not require exploits — they require understanding of how trust flows through credentials, certificates, federation assertions, and delegation configurations.

Assume Breach changes how identity systems are assessed. Prevention is necessary but not sufficient. Detection, containment, and recovery must be engineered with the same rigor as preventive controls.

Federal identity security must produce evidence and artifacts. Findings must connect to RMF control structures, produce POA\&M entries where needed, and generate evidence that authorizing officials can act on.

Governance without attack-pathway awareness is incomplete governance. Compliance-only assessment misses control pathways that compliance settings do not directly govern. Attack-pathway analysis is required to produce complete security assurance.

Defense must mirror the identity attack lifecycle. Effective defensive engineering addresses each stage of the attack lifecycle — passive reconnaissance through domain dominance — with detection, hardening, and recovery capabilities designed around real adversary techniques.

RECOMMENDED READING

1.19.1 Federal Identity, Credential, and Access Management Guidance

General Services Administration. FICAM Architecture. IDManagement.gov. https://www.idmanagement.gov/arch/

OMB Memorandum M-19-17: Enabling Mission Delivery through Improved Identity, Credential, and Access Management.

1.19.2 Department of Defense Identity, Credential, and Access Management Guidance

DoD ICAM Reference Design and Federation Framework (current edition — confirm at time of reading).

DISA Cloud Computing Security Requirements Guide (SRG) and relevant STIGs for Active Directory.

1.19.3 Risk Management Framework Guidance

NIST Special Publication 800-37 Revision 2: Risk Management Framework for Information Systems and Organizations.

NIST Special Publication 800-53 Revision 5: Security and Privacy Controls for Information Systems and Organizations.

1.19.4 NIST Digital Identity Guidance

NIST Special Publication 800-63-4: Digital Identity Guidelines (July 2025).

NIST Special Publication 800-63A-4, 800-63B-4, 800-63C-4: Identity Proofing, Authentication, and Federation companion volumes.

1.19.5 Zero Trust Guidance

OMB Memorandum M-22-09: Moving the U.S. Government Toward Zero Trust Cybersecurity Principles.

CISA Zero Trust Maturity Model (current version).

NIST Special Publication 800-207: Zero Trust Architecture.

1.19.6 MITRE ATT\&CK Framework

MITRE ATT\&CK for Enterprise. https://attack.mitre.org/

1.19.7 MITRE D3FEND Framework

MITRE D3FEND. https://d3fend.mitre.org/

1.19.8 Active Directory Security References

Schroeder, W., Christensen, L. Certified Pre-Owned: Abusing Active Directory Certificate Services. SpecterOps, 2021.

Microsoft. Securing Privileged Access. Microsoft Learn (current version).

INTRODUCTION TO CHAPTER 2



Chapter 2 moves from the idea of the identity trust system into the architecture that gives it shape. It examines forests, domains, trusts, schema, Organizational Units, domain controllers, and administrative boundaries as structures of authority — showing how Active Directory organizes trust, where that trust concentrates into risk, and why architectural understanding is the prerequisite for the offensive and defensive analysis that follows. Where this chapter explains why identity trust matters, Chapter 2 explains how Active Directory organizes and concentrates that trust, and why the architecture is the map that both adversaries and defenders must be able to read.



ACRONYMS



ACL — Access Control List · AD — Active Directory · AD CS — Active Directory Certificate Services · AD DS — Active Directory Domain Services · AD FS — Active Directory Federation Services · ATT\&CK — Adversarial Tactics, Techniques, and Common Knowledge · CAC — Common Access Card · CISA — Cybersecurity and Infrastructure Security Agency · CVE — Common Vulnerabilities and Exposures · DA — Domain Administrator · DISA — Defense Information Systems Agency · DoD — Department of Defense · DoD ICAM — Department of Defense Identity, Credential, and Access Management · EA — Enterprise Administrator · eMASS — Enterprise Mission Assurance Support Service · EKU — Extended Key Usage · FICAM — Federal Identity, Credential, and Access Management · FIPS — Federal Information Processing Standards · FISMA — Federal Information Security Modernization Act · FPKI — Federal Public Key Infrastructure · gMSA — group Managed Service Account · HSPD-12 — Homeland Security Presidential Directive 12 · IAVA — Information Assurance Vulnerability Alert · ISSO — Information System Security Officer · KDC — Key Distribution Center · LDAP — Lightweight Directory Access Protocol · LSASS — Local Security Authority Subsystem Service · MFA — Multi-Factor Authentication · NIST — National Institute of Standards and Technology · NPE — Non-Person Entity · NTDS — New Technology Directory Services · NTLM — New Technology LAN Manager · OMB — Office of Management and Budget · PIV — Personal Identity Verification · POA\&M — Plan of Action and Milestones · PRT — Primary Refresh Token · RMF — Risk Management Framework · SID — Security Identifier · SIEM — Security Information and Event Management · SP — Special Publication · SPN — Service Principal Name · SRG — Security Requirements Guide · STIG — Security Technical Implementation Guide · TGT — Ticket Granting Ticket · VSS — Volume Shadow Copy Service



REFERENCES

General Services Administration. FICAM Architecture. IDManagement.gov. https://www.idmanagement.gov/arch/ (accessed July 26, 2026).

National Institute of Standards and Technology. Risk Management Framework for Information Systems and Organizations (SP 800-37 Rev 2). 2018. https://csrc.nist.gov/pubs/sp/800/37/r2/final (accessed July 26, 2026).

National Institute of Standards and Technology. Digital Identity Guidelines (SP 800-63-4). July 2025. https://csrc.nist.gov/pubs/sp/800/63/4/final (accessed July 26, 2026).

National Institute of Standards and Technology. Zero Trust Architecture (SP 800-207). 2020. https://csrc.nist.gov/pubs/sp/800/207/final (accessed July 26, 2026).

Office of Management and Budget. Enabling Mission Delivery through Improved Identity, Credential, and Access Management (M-19-17). March 2019.

Office of Management and Budget. Moving the U.S. Government Toward Zero Trust Cybersecurity Principles (M-22-09). January 2022.

MITRE Corporation. ATT\&CK for Enterprise. https://attack.mitre.org/ (accessed July 26, 2026).

MITRE Corporation. D3FEND. https://d3fend.mitre.org/ (accessed July 26, 2026).

Microsoft. Securing Privileged Access. Microsoft Learn. https://learn.microsoft.com/security/privileged-access-workstations/ (accessed July 26, 2026).

Schroeder, W., Christensen, L. Certified Pre-Owned: Abusing Active Directory Certificate Services. SpecterOps Blog. 2021. https://posts.specterops.io/certified-pre-owned-d95910965cd2 (accessed July 26, 2026).

CISA. Zero Trust Maturity Model. https://www.cisa.gov/zero-trust-maturity-model (accessed July 26, 2026).

Department of Defense. DoD ICAM Reference Design and Federation Framework. (Confirm current edition and date at manuscript submission.)

