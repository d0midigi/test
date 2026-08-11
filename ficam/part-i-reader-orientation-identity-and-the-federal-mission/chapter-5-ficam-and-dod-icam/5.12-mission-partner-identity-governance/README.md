# 5.12 Mission-Partner Identity Governance

Mission-partner identity represents one of the clearest demonstrations that identity trust and administrative ownership are not the same thing.

A mission partner may need access to a DoD resource while remaining an identity governed by another organization. The user may belong to another military service, federal agency, allied nation, coalition organization, contractor, or external mission entity. Requiring every partner to abandon their originating identity and become a fully local account would create enormous duplication and lifecycle problems.

Federation and related trust mechanisms provide a better model.

The originating organization remains authoritative for the identity it owns.

The relying DoD environment determines what that identity may do locally.

This sounds simple at the architectural level.

Operationally, it creates one of the most governance-intensive relationships in ICAM because neither party independently controls the entire trust chain.
