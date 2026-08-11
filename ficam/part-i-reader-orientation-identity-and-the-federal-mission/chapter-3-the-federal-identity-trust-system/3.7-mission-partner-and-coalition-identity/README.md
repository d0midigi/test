# 3.7 Mission-Partner and Coalition Identity

Federal and military missions rarely occur within a single administrative enterprise.

Operations may require collaboration among military departments, combatant commands, defense agencies, civilian agencies, coalition partners, contractors, and other authorized external entities. The technical challenge is enabling those partners to access the resources they need without requiring every participating environment to surrender control of its own identities.

Mission-partner identity exists to solve that problem.

At its best, the model allows one party to remain authoritative for the identities it owns while another party makes local access decisions based on trusted information about those identities.

This is a fundamentally different model from creating local accounts for every external user and manually maintaining them forever.

It can also be significantly more secure.

Federation, certificate trust, external identity, and controlled partner-access architectures can reduce duplicate credentials, improve lifecycle management, and allow access to reflect authoritative changes made by the identity-owning organization.

But the architecture introduces a dependency: local authorization now depends partly on identity state originating elsewhere.
