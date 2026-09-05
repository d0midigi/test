# Network Security Controls

Network Security Controls, Protocols, and Devices

Cyberattacks directed against individual computers, networks, and related interconnected devices happen seamlessly across continents and oceans and the backbone of this interconnectedness lies in our network. Modern computing networks serve as lifelines of modern societies, facilitating communications, commerce, education, information sharing, entertainment, data transfer, plus more. Yet, this very connectivity exposes us to a myriad of threats, rendering our networks vulnerable to a plethora of cyberattacks. From sophisticated cyber espionage campaigns to simple yet devastating Distributed Denial of Service (DDoS) attacks, the landscape of network security is constantly evolving, demanding steadfast vigilance and resilient defenses.

However, that is the nature of network attacks, and they present themselves in many various forms, each exploiting vulnerabilities in the network infrastructure, applications, or user behaviors. These attacks can range from targeted assaults aimed at stealing sensitive information or disrupting services to indiscriminate barrages seeking to overwhelm systems and cause chaos. Whether motivated by financial gain, political intrigue, or sheer malice, these attacks underscore the fragility of the will to protect a network’s most critical resources and the relentless pursuit of adversaries to breach them

This chapter discusses the three most important elements that comprise network security: _**controls, protocols,**_ and _**devices.**_ The chapter will teach you the various network security controls, including authentication, authorization, encryption, and access controls. It also provides the necessary information on the different network security protocols that should be implemented to secure the network. This chapter also discusses the various network security perimeter appliances commonly deployed in networks to defend against possible attacks.

Network Security Controls

Network security controls are used to ensure the confidentiality, integrity, and availability of network services. These security controls are either technical, or administrative safeguards implemented to minimize security risks. To reduce the risk of a network from being compromised, an adequate network security requires implementing a proper combination of network security controls.

These network security controls include:

* Authentication
* Authorization
* Accounting
* Access Control
* Identification
* Cryptography
* Security Policy

These controls help organizations with implementing strategies for addressing network security concerns. The multiple layers of network security controls along with the network should be used to minimize the risks of attack or compromise. The overlapping use of these controls ensures defense in depth network security.

The following terminologies are used to define access control on specific resources:

Subject

A subject can be either a user or a process attempting to access objects. Subjects are the entities that carry out actions within a system.

Object

An object represents a tangible resource that access restrictions apply to. Access controls applied to objects dictate the actions users can perform on them. Examples include files or hardware devices.

Reference Monitor

The reference monitor oversees the enforcement of access control rules. It determines, based on predefined rules, whether a subject is permitted to perform certain actions on an object.

Operation

An operation signifies an action executed by a subject on an object. For instance, a user attempting to delete a file exemplifies an operation, where the user acts as the subject, “delete” is the operation, and the file is the object.

Access control principles deal with restricting or allowing access controls to users or processes. The principle includes the server receiving a request from the user and authenticating the user with the help of an Access Control Instruction (ACI). The server can either allow or deny the user to perform any actions like read, write, access files, etc.

Access controls enable users to gain access to the entire directory, subtree of the directory and other specific set of entries and attribute values in the directory. It is possible to set permission values to a single user or a group of users. The directory and attribute values contain the access control instructions.

Access control function uses an authorization database, maintained by a security admin, to check the authorization details of the requesting user.

General Steps in Access Control:

* **Step 1:** Users have to provide their credentials/identification while logging into the system.
* **Step 2:** The system validates users with the provided credentials/identification such as passwords, fingerprints, etc., with the database.
* **Step 3:** Once the identification of the user is successful, the system provides the user access to use the system.
* **Step 4:** The system then allows the user to perform only those operations or access only those resources for which the user is authorized.

There are three main parts for an access control instruction:

* **Target:** Permissions are set for certain attributes and entities. These attributes and entities are known as _**targets.**_
* **Permission:** Permissions set for the target explain the actions allowed or denied for those targets.
* **Bind Rule:** Specifies the subject to the access control instructions.

Administrative Controls

Administrative controls are management limitations, operational, and accountability procedures, and other controls that ensure the security of an organization. The procedures prescribed in the administrative access control ensure the authorization and authentication of personnel at all levels. The components of an administrative access control are as follows:

Security Policies and Procedures

Policies and procedures determine the method of implementing security practices in an organization. These specify the extent to which the company can accept a risk and specifies the level of actions allowed in the organization.

Personnel Controls and Procedures

Personnel controls determine the methods by which the employees may handle the security principles. Personnel controls specify the steps taken in the case of any non-compliance issue. The change of security determines the steps taken right from the hiring of an employee until the employee leaves or shifts in any other department.

Supervisory Structure

Supervisory structure consists of members that are responsible for the actions performed by the other employees in the organization in the context of security.

Security Awareness and Training

Trains the employee in an organization about the importance of access controls. The training assists the employees to limit the attacks in the network and assists them in detecting and controlling any potential malware outbreak.

Testing

Testing of access controls brings out the weaknesses found in the network after they are implemented since this is technically a change to the network infrastructure. Testing is conducted to make sure all access controls are working properly and evaluate the procedures and policies aligned for the proper functioning of the organization.

Job Rotation

Job rotation improves error detection and fraud disclosure. Job rotation policy along with separation of duties is a good administrative access control; however, job rotation prevents employees to take up multiple roles at a time, which adds overhead to access control system. One needs to be aware of the impact of job rotation on access control systems.

### Separation of Duties

Separation of duties comes into play when a single operation requires more than one person to complete it. When one individual is responsible for completing a task it gives them more power and the security risk is high. Whereas, if the same task is accomplished by a team of people, proper checks and balances are maintained and there is less chance for errors.

**Example:** Having one security administrator for doing actual planning and another team of security administrators implementing and testing will reduce the security risks and increase the chances of finding errors.

Separation of duties can be applied to a single person. For instance, it a user having limited access wants to perform a task requiring administrative privileges. User Account Control (UAC) can give access once the appropriate privileges are supplied.

Information Classification

Implementing access control is impossible without information classification. The information can be classified as: public, private, secret, proprietary, confidential.

Process of Information Classification:

* Understand data classification project goals
* Build data classification policy
* Build data classification process flow and procedures
* Create tools to support the process
* Determine application owners
* Determine data owners and data owner delegates
* Categorize information
* Define the audit process
* Save information in a repository
* Give user training
* Review and update information classification at regular intervals

Investigation

Investigate the logs for all doubtful activities and violations and make a report for further actions. Investigate unexpected information system-related activities. Study the investigations periodically and make changes to access authorizations.

### Physical Access Controls

Appropriate physical access controls can reduce the chances of attacks and risks in an organization. Maintaining physical access controls provides physical protection of the information, buildings, and all other physical assets of an organization.

The physical access controls are categorized into the following:

Prevention Access Controls

They are used to prevent unwanted or unauthorized access to resources. It includes access controls such as fences, locks, biometrics, mantraps, faraday cages, turnstiles, and more.

Deterrence Controls

These are used to discourage the violation of security policies. It includes access controls such as security guards, warning signs, decoy video cameras and surveillance systems, hidden mirrors, etc.

Detection Controls

These are used to detect unauthorized access attempts which include access controls such as CCTV, alarms, flashing/blinking lights, etc.

An access control point can be a physical barrier such as a door or parking gate, where electronic access control is placed; users must enter their credentials before they receive access. Using a PIN for authentication, checks the identity of a user. For example, in an office, the employee must place an access card to the card reader to be able to access the premises.

### Technical Access Controls

Technical access controls the subject’s access to an object. It involves implementing technical access controls for restricting access to devices in an organization to protect the identity of sensitive data.

The components of technical access control include:

System Access Control

System access controls deal with restriction of access to data according to sensitivity of data, clearance level of users, user rights, and permissions.

Network Access Control

Network access control offers different access control mechanisms for network devices like routers, switches, hubs, and so on.

Encryption and Protocols

Encryption and protocols protect the information passing through the network and preserves the privacy and reliability of data.

Auditing

Deals with tracking the activities of the network devices in a network. This mechanism helps in identifying weaknesses in the network.

Firewalls

Firewalls are implemented to filter unwanted traffic and prevent attacks on a network.

Antivirus Software

Antivirus software is installed to prevent the system from potential malware infections.

Types of access control determines how a subject can access an object. The policies for determining the mechanism, uses access control technologies and security.

The types of access controls include:

Discretionary Access Control (DAC)

Discretionary access controls determine the access controls taken by any possessor of an object to decide the access controls of the subjects on those objects. The other name for DAC is a _**need-to-know**_ access models. The decision taken by the owner depends on the following measures:

* **File and data ownership:** Determines the access policies of the user.
* **Access rights and permissions:** Setting access privileges to other subjects by the possessor.

The owner can provide or deny access either to any particular user or a group of users. The attributes of a DAC include:

* The owner of an object can transfer the ownership to another user.
* Access control prevents multiple unauthorized attempts to access an object.
* Prevents unauthorized users to view details like file size, file name, directory, path etc.
* The DAC uses access control lists to identify and authorized users.
* **Disadvantages:**
  * It requires to maintain the access control list and access permissions for the users.
* Examples of DAC include UNIX, Linux, and Windows access control.

Mandatory Access Control (MAC)

The mandatory access controls determine the usage and access policies of the users. Users can access a resource only if that particular user has the access rights to that resource. MAC finds its application in the data marked as highly confidential. The network administrators impose MAC, depending on the operating system and security kernel.

* There are two techniques to implement MAC:
  * **Rule-Based Access Control (RBAC):** Rule-based MAC specifies whether to allow or deny access to an object depending upon the levels of trust between the subject and the object.
  * **Lattice-Based Access Control:** The lattice-based access control defines the complex controls required for multiple subjects and objects.
* The advantages and disadvantages of MAC include:
  * MAC provides a high level of security as the network administrators determine the appropriate access controls.
  * The MAC policies minimize the chances of errors.
  * The operating system, depending on the MAC, marks and label the incoming data, thereby creating an external application control policy.
* Examples of MAC include SE Linux, trusted Solaris.

Role-Based Access Control (RBAC)

In role-based access control, the access permissions are available based on the access policies determined by the system. The access permissions are out of user control which means that users cannot amend the access policies created by the system. The rules for determining the role-based access controls are:

* **Role Assignment:** Assigning a certain role to a user that enables them to perform a transaction.
* **Role Authorization:** User needs to perform a role authorization to achieve that role.
* **Transaction Authorization:** Transaction authorization allows users to execute only those transactions for which they are authorized.

Identification

Identification deals with confirming the identity of a user, process, or device accessing the network. User identification is the most common technique used in authenticating the users in the network and applications. Users have a unique user ID which helps in identifying them.

The authentication process includes verifying a user ID and a password. Users need to provide both the credentials to gain access to the network. The network administrators provide access controls and permissions to various other services depending on the user IDs.

**Example:** Username, Account Number, etc.

Authentication

Authentication refers to verifying the credentials provided by the user while attempting to connect to a network. Both wired and wireless networks perform authentication of users before allowing them to access the resources in the network. A typical user authentication consists of a user ID and a password. The other forms of authentication are authenticating a website using a digital certificate, comparing the product and the label associated with it. The factors associated with the process of authentication are:

* **Knowledge factors:** The knowledge factors refer to the mandatory entities that a user should know while trying to log into a system or network. For example, usernames and passwords.
* **Possession factors:** The possession factors refer to the entities that a user should hold while performing logging. For example: One-time password token, Employee IDs, cards and badges.
* **Inherence factors;** The inherence factors, mostly apply to the biometric factors that the users use for authentication. For example: retina scan, fingerprint scans, etc.

Common authentication methods include:

* Passwords
* Biometrics
* Token management
* Authorization

Authorization

Authorization refers to the process of providing permission to access the resources or perform an action on the network. Network administrators can decide the access permissions of users on a multi-user system. They even decide the user privileges. The mechanism of authorization can allow the network administrator to create access permissions for users as well as verify the access permissions created for each user. In logical terms, authorization succeeds authentication. But the type of authentication required for authorization varies; however, there are cases that do not require any authorization of the users requesting for a service. For example, no user authorization is needed when a user tries to access a web page from the Internet.

Accounting

User accounting refers to tracking the actions performed by the user on a network. This includes verifying the files accessed by the user, functions like alteration or modification of the files or data.

In password authentication, users need to provide usernames and the passwords to prove their identity to a system, application, or network. The username and password are then matched against the list of authorized users in the database/Windows Active Directory. Once matched, users can access the system.

The user password should follow standard password creation practices, including a mixture of alphabet letters, numbers, and special characters, having a length greater than 8 characters (small passwords are easily guessed).

Password authentication is vulnerable to brute-force attacks (a person trying possible combinations of characters to guess the password or capture packets using a protocol “sniffer” while sending across the network as plaintext).
