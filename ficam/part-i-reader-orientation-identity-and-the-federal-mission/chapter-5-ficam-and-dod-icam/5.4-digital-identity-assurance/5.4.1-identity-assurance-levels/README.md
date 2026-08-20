# 5.4.1 Identity Assurance Levels

Identity Assurance Level (IAL) concerns confidence that the identity represented by the subscriber account corresponds to the actual subject being enrolled.

The current NIST model has three levels, but the 2025 requirements should not be reduced to the older shorthand that IAL1 simply means “self-asserted,” IAL2 means “remote proofing,” and IAL3 means “in-person proofing.” Revision 4 materially changes and expands the proofing model.

IAL1 now contains defined evidence, validation, verification, fraud-resistance, and enrollment requirements. NIST describes it as supporting multiple proofing types and as being designed to limit highly scalable enrollment attacks, synthetic identities, and attacks using compromised personal information. ([6](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a-4.pdf))

IAL2 increases evidentiary and verification rigor and is designed to address both scaled and targeted impersonation, basic evidence falsification, evidence theft, and social-engineering threats. Importantly, IAL2 can be achieved through remote or on-site processes and includes multiple verification pathways, including non-biometric, biometric, and digital-evidence approaches. ([6](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a-4.pdf))

IAL3 adds still greater rigor, including an on-site attended proofing session involving a trained proofing agent and collection of at least one biometric characteristic. NIST positions IAL3 to resist more sophisticated evidence falsification, theft, repudiation, and advanced social-engineering attacks. ([6](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a-4.pdf))

For federal Active Directory security, the most important point is what IAL does not mean.

IAL does not describe the privilege of the account.

It does not determine how the user authenticates during every later logon.

It does not establish whether the account should be a Domain Admin.

It describes confidence in the proofed identity relationship.

Those other security properties belong elsewhere.
