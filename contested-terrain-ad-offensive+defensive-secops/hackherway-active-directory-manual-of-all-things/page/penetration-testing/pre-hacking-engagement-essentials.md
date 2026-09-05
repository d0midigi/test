# Pre Hacking Engagement Essentials

### Pre-Hacking Engagement Essentials:

### Key Documents and Agreements in Ethical Hacking

**Objectives**

**After completing this section, you will be able to:**

* **Explain the need for penetration testing, stages of penetration testing, and client requirements**
* **Describe the rules of behavior and risks associated with ethical hacking, penetration testing, and red teaming**
* **Read and understand the various legal agreements involved in ethical hacking and other types of security assessments and engagements**

**Key Terms**

* **Complete-knowledge test** a type of penetration test in which the testing team is given complete knowledge about the target organization’s network and security systems
* **Confidentiality agreement** a type of agreement that states that the information provided by the target organization will be treated as confidential and proprietary; this agreement also covers key aspects of negligence and liability for many potential issues
* **DMZ (demilitarized zone)** an area that is open to all network traffic, beyond the protection of the firewall and proxies
* **HIPAA (Health Insurance Portability and Accountability Act of 1996)** an act that mandates that all health and human-services organizations incorporate security standards to protect Electronic Protected Health Information (ePHI)
* **Negligence claims** a claim made against a testing firm asserting that the firm failed to exercise minimum required protective measures regarding or care of the target organization’s electronic information systems and other electronic information assets
* **Nondisclosure agreement (NDA)** a document that protects an organization’s confidential information during business dealing with customers, suppliers, employees, and the press
* **Partial-knowledge test** a type of penetration test in which the target organization provides basic information to the testing team in order to save time and expenses; the information provided to the team may include policy and network topology documents, assets, inventory, and other valuable information
* **Rules of behavior** an agreement that details the internal and external aspects surrounding the testing procedure
* **Zero-knowledge test** a type of penetration test in which the testing team has no information and will have to start from scratch

Introduction to Client Prospects and Legal Agreements

This section focuses on client prospects and legal agreements. It deals with the various legal issues involved in ethical hacking and penetration testing, the stages of ethical hacking, and client requirements for penetration testing and various security assessments alike.

**Why Organizations Need Penetration Testing**

In today’s modern digital landscape, where a company’s operational foundation heavily relies on its information strategy, ensuring a secure network is paramount for every organization. Protecting corporate data from threats such as misconfiguration, exploits, harmful updates, backdoors, remote access trojans (RATs), insider threats, and other potential risks is essential.

Ethical hacking plays a critical role in uncovering vulnerabilities and weaknesses within the targeted network. It not only aids in identifying these vulnerabilities but also evaluates the network’s strengths, weaknesses, threats, and defense mechanisms. A standard security assessment, audit, evaluation, or inspection encompass several key steps (these are listed in no particular order):

* Assembling a testing team composed of trustworthy, transparent, and ethical skilled security professionals and security practitioners alike.
* Identifying and setting up a demilitarized zone (DMZ), an exposed area beyond the fireall and proxy protections, for testing purpose, or to segment publicly-facing web servers, such as VPNs or FTP servers from the internal DMZ and internal LAN.
* Assessing which systems and data are most susceptible to compromise.
* Evaluating the feasibility of penetrating and accessing database servers.

By clearly defining the scope of an ethical hacking engagement, or penetration testing event, organizations can:

* Pinpoint critical areas requiring testing.
* Address any legal considerations.
* Conduct impartial assessments of the production network, thereby enhancing both the systems and administrative practices.

While a penetration testing team can be internal or external, outsourcing this task to an independent third-party is often preferred. This approach ensures an objective evaluation of the network’s security measures, assisting the internal IT team in identifying and mitigating vulnerabilities. Demonstrating the network’s vulnerabilities to the in-house team is vital, especially considering legal mandates like HIPAA, which necessitate regular penetration testing to safeguard sensitive personally identifiable information (PII).

Penetration testing helps organizations comply with HIPAA, the _**Health Insurance Portability and Accountability Act of 1996.**_ HIPAA mandates that all health and human services organizations implement strict security measures and implementations to protect _**Electronic Personal Health Information (ePHI).**_ This includes designing an informational architecture that safeguards personal health information wherever ePHI is created, received, stored, maintained, or transmitted.

To meet HIPAA requirements, health organizations must maintain systems that protect sensitive personal information from unforeseen threats and hazards. The HIPAA Privacy Rule does not restrict the reasonable use of ePHI but ensures that employees respect and adhere to the privacy and security policies set forth by HIPAA. Compliance with HIPAA helps secure personal health information and ensures that the organization’s practices align with regulated requirements and legal standards.

**Security Assessment Stages**

Before initiating any type of security assessment whether it be a penetration test, an ethical hacking engagement, or a red team security assessment, it’s most important to fully realize and understand a client’s expectations and goals of the test. The planning phase should always align closely with these requirements. To effectively prepare for any security assessment, consider the following steps and implement into your proposed attack strategy to dodge unforeseen events and CYA (cover your ass).

* **Service Checklist:** Offer the client a detailed list of services you can, intend to, or will provide included within the type of security assessment you are tasked to perform.
* **Legal Documentation:** Draft essential documents, such as contracts, Non-Disclosure Agreements (NDAs), and a “Get Out of Jail Free Card” agreement. Also, prepare any additional legal paperwork addressing concerns discussed during the negotiation round.
* **Agreement Signing:** Schedule a tentative meeting with representatives from both sides to formally sign the agreement and the legally binding contract.
* **Adjustments Post-Agreement:** Should there be any changes to the terms and conditions post-contract signing, draft mutual _**Memos of Understanding (MOUs)**_. Ensure these are signed by team leads, system and network owners, and authorized experts prior to commencing the test.

**Understanding Client Requirements**

Ensuring a thorough understanding of your client’s needs is pivotal to tailoring your security assessment strategy accurately.

* **Scope Identification:** Determine the components to be assessed, including:
  * Servers
  * Workstations
  * Network infrastructure (routers, firewalls)
  * Cabling
  * Databases and software applications
  * Physical security measures
* **Sector Selection:** Choose specific areas for testing and inform relevant users and administrators.
* **Checklist Creation:** Compile a checklist outlining the testing prerequisites.
* **Timing:** Establish the timeline and preferred testing hours.
* **Emergency Planning:** Formulate an emergency response plan.
* **Backup Procedures:** Confirm that all critical data is backed up securely before proceeding.
* **Reporting Format:** Decide on the report’s structure and content.
* **Stakeholder Identification:** Determine who will participate in the review and distribution of reports and documentation.

**Testing Requirements Checklist**

The following checklist is provided to give you a general idea of items you should consider including to provide your client a clear idea of the services you expect to provide them. This list should be given to the client or customer prior to initiating any ethical hacking activities.

* _Do you have any established security-related policies and procedures?_
  * _If yes, do you want them to be reviewed?_
* _Do you want a review of the physical security of your servers and network infrastructure to be performed?_
* _How many Internet domains do you have? Are there any subdomains?_
* _How many Internet hosts do you have?_
* _Do you want your Internet presence to be mapped? Otherwise, you can provide us with a detailed diagram of your Internet presence, including addresses, host OS types, and software in use on the hosts? We will also need addresses in use on both sides of the hosts if they connect to both the Internet and the internal local area network (LAN)._
* _Do you want the security of your routers and network appliances to be reviewed?_
  * _If yes, how many routers and network appliance exist on the network?_
* _Do you want a security review of the workstations on the network to be performed? If yes, what operating systems are the workstations running?_
  * _If yes, how many workstations would you like to be tested?_
* _Five or fewer servers of each type (Windows, UNIX, Linux, Novell, Linux, RedHat, Oracle, AIX, HP-UX will be assessed; do you want more to be reviewed?_
  * _If yes, how many of each?_
* _Do you want denial-of-service (DoS) stress testing to be conducted? This testing can have adverse effects on the systems tested. We can arrange to perform this testing during nonproduction hours._
* _Do you want other sites to be visited to perform assessments on systems?_

By following these preparatory steps, penetration testers can ensure a comprehensive and effective testing process that meets the client’s specific needs and objectives.

Before you dive into the thrilling world of ethical hacking – where you’ll simulate real-world cyber and physical attack scenarios to expose vulnerabilities, identify threats, and uncover weaknesses – it’s absolutely essential to establish a solid foundation built on key documents and agreements. These crucial documents include Non-Disclosure Agreements (NDAs), Authorization Letters (often referred to as _“get out of jail free card”),_ Scope/Statement of Work (SOW), and Rules of Engagement (RoE), among others. These documents not only protect you and your team legally but also ensure that the security assessment is structured, ethical, and aligned with the client’s expectations.

Before you even consider hacking into any organizational assets, you must have all of your “ducks in a row.” This means you must have these critical documents on hand at all times. These documents can literally make or break your life and your engagement – they can be the major difference between your freedom and prison time. Furthermore, these documents must be fully completed, with all necessary written signatures from all parties concerned and involved in the engagement. They need to be accurate, free of errors, up-to-date, and reflective of the client’s goals, objectives, mission, and scope. Most importantly, you should always carry these documents with you whenever you’re conducting any part of an ethical hacking security assessment as they can be the difference between a successful engagement and legal complications.

Consider the following real-world example highlighting the importance of proper documentation and communication:

### Case Study: Red Teamers Arrested During Authorized Penetration Test

A real-world example involves Gary DeMercurio and Justin Wynn from Coalfire, who were arrested while conducting an authorized red team exercise at the Dallas County Courthouse in Iowa. Their scope included testing the physical security of the courthouse by attempting to breach external security perimeters after business hours. While upper management, the IT department, and the red team were all aware of the planned simulation, they failed to inform local law enforcement about the exercise. Although their activities were sanctioned by the State of Iowa's judicial branch, miscommunication with local law enforcement led to their arrest.

### Key Takeaways

* **Always Carry Authorization Documents:** Just as you would always carry your driver's license while driving or your passport when traveling internationally, you must have all relevant authorization documents with you during a penetration test. These documents serve as immediate proof of your legitimate activities and can prevent misunderstandings with law enforcement or security personnel.
* **Ensure Comprehensive Communication:** **Ensure Comprehensive Communication:** It's critical to inform all stakeholders, including security teams and other relevant staff, about the planned activities. Proper communication helps prevent unnecessary panic and legal issues during the engagement.

This case underscores the necessity of thorough preparation and communication to avoid severe consequences, even when operating within the bounds of an authorized engagement.

Establishing and maintaining proper documentation is a fundamental aspect of ethical hacking engagements. These documents validate your actions, define the scope and rules of your assessment, and protect all parties involved. Always ensure that you have all necessary paperwork completed, accurate, and readily accessible throughout the duration of your engagement. This practice will help you conduct effective, ethical, and legally sound security assessments, contributing to the overall security posture of the organizations you serve.

_(**Source:**_ [_https://www.infosecinstitute.com/podcast/red-teamers-arrested-conducting-a-penetration-test/_](https://www.infosecinstitute.com/podcast/red-teamers-arrested-conducting-a-penetration-test/)_)_
