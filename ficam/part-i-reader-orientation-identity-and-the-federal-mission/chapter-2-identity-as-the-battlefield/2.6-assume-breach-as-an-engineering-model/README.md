# 2.6 Assume Breach as an Engineering Model

Assume breach is sometimes reduced to a defensive slogan: operate as though an attacker is already inside the environment. That interpretation is directionally correct but incomplete. Used properly, assume breach is an engineering model for removing security assumptions that cannot be guaranteed throughout the life of an enterprise.

The model does not assert that every workstation is compromised, every administrator is malicious, or every credential has already been stolen. It recognizes instead that some preventative controls will eventually fail and that the architecture should remain defensible after that failure occurs.

This distinction is particularly important in identity infrastructure.

A security model based primarily on preventing initial compromise can appear strong until an attacker obtains one legitimate credential. If that credential immediately exposes broad network access, unrestricted authentication, excessive directory visibility, privileged sessions, reusable credentials, weak administrative boundaries, or transitive control paths into Tier 0, then much of the environment's security depended on the assumption that the first credential would never be compromised.

That is not a resilient identity architecture.

Assume breach begins from a more difficult premise: an ordinary identity will eventually be compromised. A workstation will eventually become hostile. A session token will eventually be stolen. A password will eventually be phished. An application credential will eventually leak. A trusted internal network position will eventually be occupied by an adversary.

The security architecture is then evaluated according to what happens next.

If compromise of one user remains largely confined to that user's legitimate authority, the architecture has contained the failure. If the same user can enumerate sensitive administrative relationships, reach privileged management interfaces, capture reusable credentials, modify more powerful identities, or traverse an indirect path toward directory control, the initial compromise has exposed a larger architectural weakness.

Assume breach therefore changes the unit of analysis from prevention alone to containment of authority.
