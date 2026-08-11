# 5.9 Federation Governance

Federation creates one of the most powerful capabilities in modern identity architecture: the ability to accept an identity without locally administering the process through which that identity authenticates.

That capability enables interagency collaboration, mission-partner access, cloud services, Software-as-a-Service applications, and many forms of enterprise Single Sign-On.

It also creates deliberate dependency on another authority.

The security of federation therefore rests not only on cryptography but on governance.

A relying party must know which identity provider it trusts, which assertions it accepts, which attributes are meaningful, which assurance is required, how signing keys are protected, how trust is renewed, and how the relationship can be terminated during an incident.

NIST SP 800-63C-4 defines current federation assurance requirements, while the FICAM Architecture treats federation as a distinct enterprise capability for accepting identities, credentials, and attributes managed elsewhere. ([1](https://www.idmanagement.gov/arch/))
