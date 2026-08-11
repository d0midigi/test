# 2.3 Identity as the Federal Enterprise Control Plane

Active Directory became strategically important not because it stores user accounts, but because increasingly large portions of the enterprise came to depend on the decisions made through those accounts and the infrastructure surrounding them.

This distinction separates a directory from an identity control plane.

A directory records information. A control plane determines how other systems are allowed to operate.

In a mature Windows enterprise, Active Directory Domain Services (AD DS) participates in decisions that reach far beyond interactive logon. It establishes security principals, maintains group relationships, supports Kerberos authentication, distributes policy, provides service-discovery information, maintains trust relationships, exposes directory attributes to applications, and supplies authorization data that other systems consume. Administrative tools rely on it. File servers rely on it. Application servers rely on it. Remote-management technologies rely on it. Certificate infrastructure may rely on it. Network-access systems may rely on it. Hybrid identity platforms may synchronize from it or write information back into it.

Once those dependencies accumulate, Active Directory ceases to be merely another enterprise service.

It becomes a source of authority.

That authority is distributed across many mechanisms rather than concentrated in a single setting called “trust.” A user's group membership can affect access to thousands of resources. A computer account can establish the identity under which a machine participates in the domain. A Group Policy Object can alter the configuration of every system within its scope. A delegated permission can allow one administrator to control another identity without making that administrator a Domain Admin. A trust can permit principals from another domain or forest to authenticate to resources that honor that trust. A Certification Authority integrated with the directory can issue credentials that applications and Domain Controllers subsequently accept as proof of identity.

The security consequence is cumulative.

Individually, each mechanism solves a legitimate administrative problem. Collectively, they establish the operating model by which the enterprise decides who may act, where they may act, and with what authority.

That is control-plane behavior.
