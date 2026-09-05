# Penetration Testing Methodology

Penetration Testing Methodology

When looking into cyberattacks, one notable observation is the strategic approach taken by hackers. While all pre-attack hacking methodologies may vary between one hacker to the next, one thing remains constant: the goal for breaching security centers around a meticulously thought out plan that ensures that the attack process adheres to some standardized methodology with documented steps. This structured approach leads to predictable and consistent results, especially in terms of the security posture being targeted. By following a structured methodology, you are effectively able to devise testing or attack strategies based on the information you gathered in earlier phase of the hacking lifecycle.

In a detailed penetration test, various security measures are systematically analyzed to identify vulnerabilities and potential points of exploitation. The comprehensive assessment should cover a range of crucial areas including:

**Network Security**

Penetration testers should check for the following things to secure a network:

| <ul><li>Network surveying</li></ul>                                    | <ul><li>Port scanning</li></ul>                                                      |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| <ul><li>Operating System identification (OS Fingerprinting)</li></ul>  | <ul><li>Services identification</li></ul>                                            |
| <ul><li>Vulnerability research, validation, and verification</li></ul> | <ul><li>Application testing and code reviews</li></ul>                               |
| <ul><li>Router and switch testing</li></ul>                            | <ul><li>Firewall testing</li></ul>                                                   |
| <ul><li>Intrusion Detection System (IDS) testing</li></ul>             | <ul><li>Trusted-systems checking</li></ul>                                           |
| <ul><li>Password cracking</li></ul>                                    | <ul><li>Denial of Service (DoS) stress testing</li></ul>                             |
| <ul><li>Containment-measures testing</li></ul>                         | <ul><li>Perimeter and network-edge security testing (public-facing assets)</li></ul> |
| <ul><li>Wireless network perimeter security</li></ul>                  | <ul><li>Database Hardening</li></ul>                                                 |

When conducting network security penetration tests, penetration testers must thoroughly examine key elements to reinforce the network’s defenses and resiliencies against emerging threats and cyberattacks. This includes conducting network surveys, scanning for open ports, identifying systems and services, researching vulnerabilities, and verifying and validating their presence.

Additionally, testers must engage in rigorous application testing, review code for weaknesses, test routers and firewalls, assess IDS/IPS, evaluate trusted systems, and simulate scenarios such as password cracking, DoS attacks, and containment-measures testing. Each step plays a critical role in fortifying the security posture of a client organization.

**Information Security (INFOSEC)**

Penetration testers check the security of sensitive information of the client organization, and includes the following activities:

* Document analysis
  * Examining internal documents to identify sensitive information that might be improperly stored, shared, or protected, potentially leading to information leaks.
* Gathering competitive intelligence
  * Simulating how competitors might gather intelligence via OSINT techniques on the organization to identify weaknesses in information handling that could be exploited.
* Conducting privacy assessments
  * Reviewing the client organization’s practices to ensure compliance with privacy regulations and identifying vulnerabilities in data protection.

**Social Engineering**

To evaluate the client organization’s defenses against social engineering attacks, penetration testers should perform the following:

* Request testing
  * Testing the client organization’s response to various types of information requests to identify how easily sensitive data can be obtained through deceptive means.
* Guided suggestion testing
  * Assessing employees’ susceptibility to subtle suggestions that might lead to security breaches, such as clicking on malicious links or disclosing confidential information.
* Trusted insider testing
  * Evaluating how the organization handles potential threats from trusted insiders, such as employees or partners, who might attempt to exploit their position to gain unauthorized access.

**Wireless Network Security**

To ensure the security of wireless devices and networks, penetration testers should conduct the following tasks:

* Wireless network testing for rogue access points
  * Detecting unauthorized wireless access points that could be used by attackers to enter the network.
* Cordless-communications testing
  * Evaluating the security of cordless communications systems to identify vulnerabilities that could be exploited for unauthorized access or eavesdropping.
* Privacy assessments
  * Ensuring that wireless communication channels are secured, and that sensitive data transmitted over these networks is protected against interception.
* Infrared-systems testing
  * Checking the security of infrared communications systems, which could be targeted by attackers to intercept or manipulate data being transmitted being devices.

**Communications Security (COMSEC)**

The following penetration testing methods are used to assess the security of communications systems within the organization:

* PBX testing
  * Evaluating the security of the organization’s Private Branch Exchange (PBX) system to identify vulnerabilities that could allow unauthorized access, eavesdropping, or toll fraud.
* Voice mail testing
  * Testing the security of voicemail systems to ensure that they are protected against unauthorized access and manipulation.
* Fax review
  * Reviewing fax systems for security weaknesses that could lead to unauthorized interception or tampering with transmitted documents.
* VoIP and modem testing
  * Assessing the security of modems to detect any vulnerabilities that could be exploited for unauthorized network access.

**Physical Security (PHYSEC)**

Security of the organization against physical attacks may be ensured by implementing the following procedures:

* Access controls testing
  * Verifying the effectiveness of access control mechanisms, such as key cards and biometric systems, to prevent unauthorized entry into secure areas.
* Perimeter reviews
  * Assessing the physical perimeter of the facility, including fences, gates, CCTV, and surveillance systems to identify weaknesses that could be exploited.
* Monitoring review
  * Evaluating the effectiveness of security monitoring systems, such as motion detectors and flood lighting to ensure continuous surveillance and deterrence for timely detection of unauthorized activities.
* Alarm-response testing
  * Testing the organization’s alarm systems and response protocols to ensure that security breaches are detected and addressed promptly.
* Location review
  * Reviewing the physical layout and strategic location of sensitive areas to identify potential security risks, such as proximity to public spaces or easily accessible points.
* Environment review
  * Assessing the environmental controls in place, such as temperature, humidity, and fire suppression systems, to ensure that they adequately protect sensitive equipment and data from damage.

**Penetration Testing Methodologies**

The success of any penetration test largely depends on the formal, or modified, methodology used to design it. A well-structured methodology provides you with a systematic approach, ensuring the test is consistent, accurate, and efficient; however, this doesn’t mean that the framework should be overly restrictive.

There are two key types of penetration testing methodologies:

1. **Proprietary Methodologies**
2. **Open-Source and Public Methodologies**

**Proprietary Methodologies**

Many organizations that specialize in penetration testing and network security services have developed their own methodologies (modified). These are typically kept confidential to maintain a competitive edge. Examples of proprietary methodologies include:

* IBM
* ISS Foundstone
* EC-Council LPT

**Open-Source and Public Methodologies**

There are numerous publicly available methodologies that are well-documented and widely accepted within the security community. These include:

* **OWASP (Open Web Application Security Project):** OWASP focuses on improving the security of software by providing a set of tools, documentation, and methodologies specifically designed for web applications. It includes resources like the OWASP Top Ten, which identifies the most critical security risks to web applications, and various guides for secure development and testing.
* **OSSTMM (Open-Source Security Testing Methodology Manual):** OSSTMM provides a comprehensive framework for security testing and analysis. It covers various types of security assessments, including network, physical, and human security. The methodology is designed to achieve measurable and repeatable security metrics, ensuring a high level of consistency and accuracy in testing.
* **NIST SP 800-115 (National Institute of Standards and Technology Special Publication):** NIST SP 800-115 is a guide to conducting information security assessments, including penetration testing, security audits, and vulnerability assessments. It provides detailed steps and best practices for planning, executing, and reporting on security assessments, ensuring that organizations follow a standardized approach.
* **PTES (Penetration Testing Execution Standard):** PTES outlines a structured process for conducting penetration tests, covering everything from pre-engagement interactions to post-engagement reporting. It is designed to ensure that penetration tests are thorough, standardized, and repeatable, providing a clear roadmap for both testers and clients.
* **SANS (SysAdmin, Audit, Network, and Security) Testing Methodology):** The SANS Testing Methodology provides guidelines for various types of security testing, including penetration testing, vulnerability assessments, and incident response. It is part of a broader set of resources offered by SANS, a leading organization in cybersecurity education and research.
* **CHECK (UK Government's IT Security Penetration Testing Methodology):** CHECK is a methodology used by certified penetration testers in the UK to assess the security of government systems. It is designed to identify vulnerabilities that could lead to unauthorized access to sensitive information, ensuring that systems comply with UK government security standards.
* **WASC-TC (Web Application Security Consortium Threat Classification):** WASC-TC is a methodology for classifying web application vulnerabilities. It provides a standardized way to identify, categorize, and address security threats specific to web applications, helping organizations prioritize their security efforts based on the severity and impact of potential vulnerabilities.

These methodologies provide a structured approach to penetration testing and security assessments, ensuring thorough and consistent results.

Routine testing is crucial in preventing security incidents before they happen. Regular testing of network security in areas such as system configurations, operations, and administration ensures that all systems are properly configured and equipped with the necessary security measures.

Key Areas of Focus:

* **Initial Testing of Significant Equipment:** Begin by testing critical systems that are publicly accessible, such as:
  * Firewalls
  * Web Servers
  * E-mail Servers

Adhere to warning instructions properly when testing. Certain types of testing, like network scanning, vulnerability testing, and penetration testing, require strict adherence to warning instructions. Since these tests can mimic the signs of an attack, they must be conducted in a coordinated manner with the full knowledge and permission of appropriate officials.

Security Policy and Risk Management

The organization’s security policy should guide all testing procedures to meet specific needs and requirements. Incorporating security testing into risk management procedures helps identify and reduce vulnerabilities.

Expertise in Security Testing

Only trained professionals who specialize in system and network operations should perform security testing. Given the complexity of system administration, organizations need an adequate number of skilled administrators to manage both system administration and security testing effectively.

Patching and Vulnerability Management

Keeping all systems up-to-date with the latest patches is essential. Security testing may reveal the need to patch multiple systems, and applying these patches promptly can significantly reduce vulnerability exposure.

Complementing Vulnerability Testing

While vulnerability testing may sometimes produce false positives or miss certain issues, penetration testing serves as a valuable complement. It can uncover hidden vulnerabilities that might otherwise go undetected, providing a more comprehensive assessment of the system's security.

**Operational Strategies for Security Testing**

The primary goal of performing a security test is to maximize the benefit to the organization. For an operational perspective, penetration testing is crucial in shaping information security strategies. It identifies vulnerabilities, assesses their potential impact, and measures their likelihood, allowing these risks to be managed proactively.

**Operational and Maintenance Phases**

During these phases, the types and frequencies of penetration tests are determined through a prioritization process, which takes into account the following factors:

* **Security Category of the Information System:** Understanding the sensitivity and criticality of the information system guides the prioritization of tests.
* **Costs of Conducting Tests:** Evaluating the costs associated with each type of test helps in making informed decisions about resource allocation.
* **Benefit to the Organization’s Systems:** Assessing how each test type benefits the organization’s system ensures that testing efforts align with business objectives.

**Implementation Phase**

Deciding what to test during this phase involves evaluating all systems within the organization. The senior IT manager plays a crucial role in the prioritization process, ensuring that assets are appropriately tested based on their importance and risk profile. This approach ensures that testing is both comprehensive and aligned with the organization’s overall security strategy.
