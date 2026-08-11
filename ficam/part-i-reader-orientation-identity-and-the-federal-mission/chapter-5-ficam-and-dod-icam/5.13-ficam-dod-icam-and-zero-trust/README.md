# 5.13 FICAM, DoD ICAM, and Zero Trust

FICAM, DoD ICAM, and Zero Trust are closely related enough that they are often discussed together and different enough that combining them into one concept creates confusion.

FICAM provides an enterprise identity architecture and governance model.

DoD ICAM adapts and extends identity, credential, access, federation, and related capabilities to Department of Defense mission requirements.

Zero Trust changes the assumptions under which access is granted and maintained.

The three intersect, but none replaces the others.

A Zero Trust policy engine still needs identity.

It needs to know which principal is requesting access, what authenticator established that principal, what attributes are trustworthy, what device is involved, what privilege the principal possesses, and what resource is being requested.

ICAM supplies significant portions of that information and the governance required to maintain it.

Zero Trust then refuses to treat successful authentication, network location, or previous access as sufficient reason to grant unrestricted continuing trust.

The result is not “FICAM with more MFA.”

It is a change in how identity evidence is consumed.
