# 2.4 Identity as an Attack Surface

An attack surface is often described as the collection of systems, interfaces, services, and vulnerabilities available to an adversary.

Identity expands that definition considerably.

The identity attack surface includes not only software that can be exploited, but relationships that can be abused.

A password is part of the identity attack surface because possession may enable authentication.

A service ticket is part of the attack surface because its cryptographic protection may reveal information useful for recovering a service account password.

A directory permission is part of the attack surface because it may allow unauthorized modification of an identity object.

A certificate template is part of the attack surface because its enrollment and subject-name rules may permit unintended identity representation.

A trust relationship is part of the attack surface because it determines which external principals are accepted.

A synchronization service is part of the attack surface because it can move identity state between environments.

An administrator's workstation is part of the attack surface because privileged credentials and sessions may pass through it.

The important shift is that none of these conditions must contain a traditional software vulnerability.

The attack surface may exist entirely within legitimate functionality.
