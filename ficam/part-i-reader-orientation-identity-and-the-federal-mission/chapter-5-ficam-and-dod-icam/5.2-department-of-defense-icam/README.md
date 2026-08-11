# 5.2 Department of Defense ICAM

DoD ICAM operates within the broader federal identity framework while addressing the Department's distinct mission, scale, organizational structure, classification environments, operational constraints, and mission-partner requirements.

The DoD Enterprise ICAM Reference Design does not define one monolithic identity service that every system must consume in exactly the same manner. It provides architecture guidance for capabilities that can exist at the DoD enterprise, Component, Community of Interest, or local level. It also recognizes that mission-partner identity functions may be performed externally and that local ICAM services may remain necessary where enterprise services cannot satisfy mission requirements.

That architecture is significant because DoD identity cannot be reduced to Active Directory consolidation.

The problem is not simply how many forests should exist.

It is how authoritative identity, credentials, attributes, authentication, authorization, federation, and lifecycle state can remain interoperable across a department whose missions cannot always depend on one network, one directory, one classification, or one administrative authority.

The reference design explicitly encourages enterprise services where they provide appropriate mission support but retains Component and local responsibility where enterprise services do not meet operational needs. It also places responsibility on mission owners to ensure that ICAM is implemented securely and identifies threat-representative cybersecurity testing as part of validating secure ICAM implementation.

That last point is especially important to _Contested Terrain_.

ICAM is not complete because the architecture diagram looks correct.

Its trust assumptions must survive adversarial validation.
