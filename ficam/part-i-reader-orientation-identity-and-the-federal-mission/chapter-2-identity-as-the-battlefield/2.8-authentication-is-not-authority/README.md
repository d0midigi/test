# 2.8 Authentication Is Not Authority

Few distinctions are more important to identity security than the difference between proving an identity and possessing authority.

Authentication establishes that a system is willing to accept a principal as the identity represented by a credential or authentication exchange.

Authority determines what that principal can influence after authentication succeeds.

The two are related but not equivalent.

This distinction appears obvious in theory, yet operational security practices routinely blur it. Stronger authentication is sometimes treated as though it directly reduces excessive privilege. Multifactor authentication is described as protecting an administrator even when the administrator's account remains overprivileged. Passwordless authentication is presented as an identity-security endpoint even when authorization relationships remain poorly governed.

Stronger authentication can make impersonation significantly more difficult.

It does not automatically make the authenticated identity's authority appropriate.
