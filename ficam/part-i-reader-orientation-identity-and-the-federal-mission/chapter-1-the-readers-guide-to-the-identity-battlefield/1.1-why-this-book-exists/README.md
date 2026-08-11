# 1.1 Why This Book Exists

### 1.1 Why This Book Exists

There is no shortage of Active Directory documentation.

There are books explaining how to create domains, manage users, configure Group Policy Objects (GPOs), administer Domain Controllers (DCs), troubleshoot Domain Name System (DNS), and operate Windows enterprise environments. There are countless penetration testing books that fully explain Kerberoasting, credential dumping, relay attacks, lateral movement, privilege escalation, and persistence. There are federal publications explaining risk management, digital identity, security controls, credential assurance, Zero Trust, and authorization requirements.

All of those bodies of knowledge are useful and have contributed greatly to the knowledge bases of offensive and defensive realms within the cybersecurity domains.

The problem is that practitioners are often expected to connect these components on their own.

An Active Directory administrator may understand how to delegate control over an Organizational Unit (OU) without understanding how that delegation becomes an attack-path edge.

An ethical hacker or penetration tester may know how to accurately identify `GenericAll` or `WriteDACL` permissions without understanding why the affected identity relationship may have dire consequences beyond the domain being tested.

An Information Systems Security Officer (ISSO) may understand a security-control requirement without understanding how several individually compliant identity configurations can combine into a viable privilege-escalation pathway.

A Security or Network Operations Center (SOC/NOC) analyst may receive an alert involving unusual Kerberos service-ticket activity without understanding the directory architecture that makes the event one of great significance.

An identity engineer may understand Personal Identity Verification (PIV), Common Access Card (CAC), federation, or authentication assurance while having limited exposure to the techniques an adversary can use after obtaining a legitimate foothold.

A red team operator may know exactly how to reach Domain Admin but have little reason to think about what the compromise means to an Authorizing Official (AO), mission owner, FICAM program, authorization boundary, or interconnected mission partner.

The technical problem is not that any one of these practitioners lacks expertise.

The problem is that identity compromise crosses all of their disciplines.

That is the gap this book is designed to address.
