# 2.5 Trust Rather Than Network Location

The word trust is used so broadly in cybersecurity that it can become imprecise.

Within identity security, trust should be treated as an operational condition: one system accepts another system, principal, credential, assertion, or authority strongly enough to allow that acceptance to influence an access decision.

This definition is intentionally practical.

A Domain Controller trusts cryptographic material associated with domain authentication.

A resource server trusts authorization information associated with an authenticated principal.

A relying party trusts a federation service to make identity assertions.

A certificate consumer trusts certificates chaining to an accepted trust anchor under the conditions required for the intended use.

A domain may trust identities from another domain through an Active Directory trust relationship.

A cloud application may trust an identity provider to authenticate a user it never authenticates directly.

None of these trust decisions requires the participating systems to share the same network.

That is one of the defining differences between network-centric and identity-centric security.
