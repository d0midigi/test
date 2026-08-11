# 3.2 The Domain Versus the Identity Trust System

The Active Directory domain is a real and meaningful security structure.

It is simply not always the largest structure that matters.

A domain contains security principals, directory objects, policy, computer accounts, authentication relationships, and administrative authority. Domain Controllers maintain authoritative directory state and participate directly in authentication. Compromise of domain-level authority can therefore have severe consequences.

The analytical mistake occurs when the domain boundary is assumed to contain every system capable of influencing that authority.

It often does not.

A Certification Authority can issue a credential that Active Directory later accepts.

A federation service can issue a token that another application trusts.

A personnel system can supply attributes that determine how an identity is provisioned.

A synchronization engine can move identity state from one directory to another.

A virtualization administrator can potentially control the execution environment of a Domain Controller without holding any directory privilege.

A backup operator may possess the ability to restore sensitive directory data.

These systems exist around the domain while still influencing the domain's trust state.

The distinction between the domain and the identity trust system is therefore not semantic. It determines whether security analysis captures the actual sources of authority.
