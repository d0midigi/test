# 5.5 Federal Credentials

Federal credentials occupy a distinctive position in the identity trust system because they connect an established identity to an authentication mechanism that can be recognized beyond a single application or local account database. In the federal model, the credential is not merely a convenient container for a username. It is part of a controlled trust chain in which identity proofing, issuance, cryptographic binding, lifecycle management, validation, and revocation determine whether a relying system should accept the credential as evidence of identity.

This distinction becomes particularly important when federal credentials interact with Active Directory.

A Windows domain account and the credential used to authenticate that account are related but separate security objects. The account exists within the directory and carries directory-specific state such as group membership, authorization relationships, logon restrictions, and object permissions. The credential provides one mechanism through which the person represented by that account can demonstrate control of an authenticator. Federal smart-card authentication joins those two systems through certificate-based authentication and account mapping rather than by turning the card itself into an Active Directory account.

That separation has important defensive consequences.

An agency can issue a cryptographically strong credential while maintaining an overprivileged directory account. Conversely, an appropriately governed account can still be exposed if certificate mapping, revocation processing, credential issuance, or authenticator lifecycle controls are weak. The security of the resulting authentication therefore depends on both sides of the relationship: the federal credentialing infrastructure that establishes the authenticator and the relying identity system that determines what authority the authenticated principal receives.

FICAM treats credentials as a distinct architectural function for precisely this reason. Current federal guidance recognizes agency-issued PIV and Common Access Card credentials, cryptographic key pairs, derived credentials, and other authentication mechanisms as credentials associated with enterprise identities rather than as the identity itself. ([1](https://www.idmanagement.gov/arch/))
