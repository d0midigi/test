# 1.4 What the Reader Does Not Need to Know Yet

Advanced Active Directory security can appear unnecessarily difficult when it is first encountered through exploit names rather than underlying mechanisms.

A new reader may encounter terms such as DCSync, DCShadow, Kerberoasting, Resource-Based Constrained Delegation (RBCD), Shadow Credentials, ESC1, Golden Tickets, Golden Certificates, Primary Refresh Tokens, or Golden SAML and conclude that the field consists of hundreds of unrelated tricks that must somehow be memorized.

That conclusion is wrong.

Most advanced identity attacks are consequences of a much smaller set of underlying security principles: authentication, authorization, credential possession, object control, delegation, replication authority, certificate trust, federation trust, identity synchronization, and administrative reachability.

Once those mechanisms are understood, many apparently complex attacks become predictable.

The reader therefore does not need to arrive knowing the offensive vocabulary. The architecture chapters deliberately establish the mechanisms before the attack chapters ask the reader to abuse them.
