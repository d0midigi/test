# 5.6 Identity Governance

Identity governance determines the rules through which enterprise identities are created, maintained, related to authoritative sources, reviewed, and eventually removed.

This is broader than account administration.

Account administration is one implementation function within the governance model.

A technically efficient provisioning system can create accounts within seconds. Identity governance determines whether the account should have been created at all, what authoritative identity it represents, who owns the relationship, how its state will change over time, and what causes the identity to cease being valid.

Current FICAM architecture and lifecycle guidance places identity management and governance across creation, proofing, provisioning, maintenance, aggregation, and deactivation rather than limiting the function to account creation. ([1](https://www.idmanagement.gov/arch/))

This perspective is particularly useful in Active Directory because directories accumulate state very easily.

Creating an object is simple.

Determining whether that object remains appropriate five years later is much harder.
