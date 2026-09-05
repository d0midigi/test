# Cybersecurity 101

Cybersecurity 101

ARP Poisoning

ARP Poisoning, also known as ARP Spoofing, is a type of cyberattack carried out over a Local Area Networks (LANs) that involves sending falsified Address Resolution Protocol (ARP) messages onto the network. This attack exploits the lack of authentication in the ARP protocol and is used to associate the attacker’s MAC address with the IP address of another host, such as the default gateway or a specific computer on the network.

Under normal circumstances, when a device wants to communicate with another device on the network, it sends an ARP request to determine the MAC address associated with the desired IP address. The device with that IP address replies with its MAC address.

In ARP poisoning, the attacker sends forged ARP reply messages to a target host (or hosts) on the network. These replies falsely tell the target device(s) that the attacker’s MAC address corresponds to the IP address of another important host on the network, such as the gateway.

As a result, the target device(s) sends data intended for that important host (like the gateway) to the attacker instead. The attacker can then intercept, modify, or block this data before potentially forwarding it to the intended host, thus executing a man-in-the-middle (MiTM) attack.

The attacker can eavesdrop on network traffic, capturing sensitive information such as login credentials and financial data. By intercepting and modifying data, attackers can take over sessions, such as web sessions, to gain unauthorized access to web applications. By disrupting the network communication, the attacker can render network services unavailable. ARP poisoning can lead to network slowdowns and instability due to incorrect ARP mappings.

AS-REP Roasting

AS-REP Roasting is a type of attack targeting Kerberos authentication in Windows Active Directory (AD) environments. This attack exploits a vulnerability in the way Kerberos handles pre-authentication, specifically targeting accounts configured not to require pre-authentication.

In a typical Kerberos setup, when a user logs in, their client requests an _**“Authentication Service Request” (AS-REP)**_ from the Kerberos Key Distribution Center (KDC). Normally, this request includes pre-authentication data, proving the user’s identity by encrypting the timestamp with their password hash. The KDC decrypts this to verify the user’s identity before sending the AS-REP.

Some accounts, however, may be configured without the requirement for pre-authentication. This is sometimes done for backward compatibility or specific configuration scenarios. An attacker can request AS-REP tickets for accounts without pre-authentication. The KDC will return encrypted data that can be cracked offline to reveal the user’s password.

Using tools like GetNPUsers from Impacket, an attacker enumerates user accounts in an AD domain that are set not to require pre-authentication:

GetNPUsers.py \<Domain>/\<User> -no-pass -usersfile users.txt

The tool requests AS-REP tickets for these accounts. The KDC responds with encrypted tickets. The attacker uses password cracking tools like John the Ripper, or Hashcat to crack these tickets and potentially recover users’ passwords.

Asynchronous SQL Injection

Asynchronous SQL injection is a form of SQL injection attack where the malicious SQL commands executed by an attacker don’t produce immediate results.

In traditional SQL injection, the attacker inputs malicious SQL code into an input field (like a search box or login form) to manipulate a database in ways that benefit them, such as accessing unauthorized data.

The results of these actions are typically immediate and directly observable by the attacker, such as retrieving hidden data or altering database content.

In contrast, with asynchronous SQL injection, the effects of the malicious SQL commands might not be immediately visible. These attacks might involve injecting a payload that is executed later or under certain conditions, making detection and prevention more challenging.

For example, the payload might be designed to trigger when a specific event occurs in the database or application, or it might execute in a background process that doesn’t provide direct output to the attacker.

This type of attack requires a more sophisticated approach both in execution and in detection. It’s also more difficult to trace, as the delayed execution can disconnect the cause (injection) from the effect (malicious action), complicating efforts to identify and mitigate the attack.

Authentication

Authentication is a process used in computing and information security to verify the identity of a user, process, or device as a prerequisite to allowing access to resources in a system. It's a critical component of most security strategies, ensuring that only authorized entities can access protected resources such as data, systems, and networks.

Authentication typically involves validating credentials, which can include things like usernames, passwords, digital certificates, or biometric data.

Types of Authentication Factors:

Knowledge Factors: Something the user knows (e.g., password, PIN).

Possession Factors: Something the user has (e.g., security token, smartphone).

Inherence Factors: Something the user is (e.g., biometric verification like fingerprints or facial recognition).

Location Factors: Somewhere the user is (e.g., accessing from a specific location).

Behavior Factors: Something the user does (e.g., typing patterns).

Combining two or more different types of authentication factors significantly increases security. For example, a system may require a password (something the user knows) and a one-time code from a smartphone (something the user has) - known as Multi-Factor Authentication (MFA).

Single Sign-On (SSO) allows user to authenticate once and gain access to multiple systems without being prompted to log in again for each system.

Various protocols facilitate authentication including Kerberos Authentication|Kerberos, Lightweight Directory Access Protocol|LDAP, OAuth, and SAML (Security Assertion Markup Language).

Authentication is a fundamental part of access control systems, determining whether a user should be allowed access to a system or resource. It helps in protecting systems from unauthorized access, thus safeguarding sensitive data and resources. In digital communications and transactions, authentication establishes trust by ensuring that entities involved are who they claim to be.

Authentication, Authorization and Accounting (AAA)

Authentication, Authorization, and Accounting (AAA) is a framework for intelligently controlling access to computer resources, enforcing policies, auditing usage, and providing the information necessary to bill for services. These processes are important for effective network management and security.

Authentication:

Purpose: To verify the identity of a user or device attempting to access a system or network.

Process: This can involve checking credentials like usernames and passwords, biometric data, tokens, or other authentication factors.

Goal: Ensure that users or devices are indeed who or what they claim to be.

Authorization:

Purpose: To determine what an authenticated user or device is permitted to do.

Process: Once a user is authenticated, the system checks what access rights and privileges they have. This could include access to files, databases, services, or other network resources.

Goal: Make sure users or devices have the appropriate permissions to perform certain actions or access certain data.

Accounting:

Purpose: To track the activities of users and devices on a network.

Process: Records are kept of what actions were taken, when they were taken, which resources were used, for how long, etc. This data can include time logs, data usage, performed activities, and more.

Goal: Provide a way to audit and bill for resource usage, as well as a means to monitor and analyze usage patterns for security and administrative purposes.

AAA is implemented through various protocols and systems, such as RADIUS (Remote Authentication Dial-In User Service) and TACACS+ (Terminal Access Controller Access-Control System Plus).

These protocols help manage AAA for networked computing environments and are essential for enforcing security policies, controlling access to resources, auditing usage, and ensuring that only authorized users and devices can access network resources and perform actions according to their permissions.

AAA is a cornerstone of network management and security, especially in large-scale and enterprise environments.

Authorization

Authorization

Authorization, in the context of computer security and information systems, is the process of granting or denying rights and privileges to a user, program, or process to access resources in a system. It is a critical component of access control and is often closely linked with authentication. While authentication verifies the identity of a user or entity, authorization determines what an authenticated user or entity is allowed to do.

Authorization involves defining and enforcing policies that determine what actions users can perform on a system, such as read, write, delete, or execute permissions on files, databases, or applications.

In many systems, authorization is managed through Role-Based Access Control (RBAC)|RBAC, where permissions are assigned based on roles within an organization, and users are granted roles that provide appropriate access. Authorization involves managing the privileges assigned to users or groups, ensuring they have the necessary access to perform their roles efficiently but not more than what is required.

This security principle dictates that users and programs should have the minimum levels of access - or permissions - necessary to perform their tasks. This minimizes the risk of unauthorized access. Authorization is enforced through policies set by the system or network administrators. These policies are implemented and enforced through security mechanisms in the operating system, applications, or in the network.

Examples of authorization:

A user attempting to access a file may be authenticated through a username and password but can only read or modify the file if their role or user account has been granted those specific permissions.

In an enterprise setting, an employee in the finance department may have access to financial software and documents that are not accessible to someone in the marketing department.

In a web application, a user may be authenticated to log in but will only be authorized to access certain features or data based on their user type or subscription level.

Authy

Authy

Authy is a Multi-Factor Authentication (MFA)|two-factor authentication (2FA) app that provides an additional layer of security for online accounts beyond just usernames and passwords. It's similar to Google Authenticator but comes with several features that distinguish it. Authy is designed to generate Time-based One-Time Password (TOTP)|time-based one-time passwords (TOTPs) for 2FA, enhancing the security of user accounts on various online platforms.

One of the standout features of Authy is its ability to sync across multiple devices. This means you can access your 2FA tokens from your smartphone, tablet, or desktop, which is convenient if you lose access to one of your devices. Authy allows users to back up their 2FA accounts in the cloud. If you change or lose your device, you can easily recover your accounts on a new device after verifying your identity.

Like Google Authenticator, Authy generates TOTPs offline, making it usable even in areas without internet connectivity. In addition to generating TOTPs, Authy also supports push authentication – a simple approve or deny prompt for logging in, adding ease of use. You can use Authy to manage 2FA tokens for various services, including social media, cloud storage, email, and online banking.

The process is:

When setting up 2FA for an online account, if you choose to use an authenticator app, you can opt for Authy.

You typically scan a QR code provided by the service to add your account to Authy. This process securely transfers the shared secret key used to generate the TOTPs.

For logging in to your account, after entering your password, you'll be prompted to enter the 6-digit code from Authy.

Open Authy to view the code, which refreshes every 30 seconds.

Authy enhances account security by requiring a second form of verification, protecting against password theft and unauthorized access. The ability to sync across devices and back up your accounts reduces the risk of being locked out of your accounts if you lose access to your primary device.

While the multi-device feature and cloud backups add convenience, some users might have concerns about the implications of cloud-based storage for sensitive 2FA data. The security of your Authy app depends on the security of your devices and your cloud account.

Bind Shell

Bind Shell

A bind shell is a type of shell used in cybersecurity contexts, particularly in the exploitation of vulnerable systems. It refers to a technique where a shell (command interpreter) is bound to a specific port on the target machine, allowing an attacker to remotely access it.

In a bind shell scenario, an attacker exploits a vulnerability in a target system to execute arbitrary code. This code sets up a command shell (like bash, cmd.exe) that listens on a specified network port.

Once the shell is bound to a port, the attacker can connect to this port over the network. This connection provides access to the command shell of the target system, allowing the attacker to execute commands as if they were locally logged into the system.

Unlike a Reverse Shell, where the target system initiates a connection to the attacker’s machine, a bind shell opens a listening port on the target system, which the attacker then connects to. Bind shells are often used in penetration testing and exploitation scenarios to demonstrate the impact of a vulnerability that allows remote code execution.

Bind shells are considered a security threat, as they allow unauthorized access to a system. They can bypass Firewall|firewalls and other security measures if outbound traffic is less restricted than inbound traffic.

Bind shells can be scripted in various languages (like Python, Perl, PHP) or set up using tools like Netcat.
