# 6.1 Risk Management Framework

RMF is a decision architecture, not a documentation process.

It connects controls to systems, missions, threats, dependencies, and consequences. NIST organizes RMF into seven steps: Prepare, Categorize, Select, Implement, Assess, Authorize, and Monitor. It integrates security and privacy risk management throughout the system life cycle.

This model fits identity security particularly well. Identity infrastructure rarely belongs conceptually to one application. Domain Controllers, PKI, federation, privileged-access platforms, synchronization services, and administrative workstations can serve many authorization boundaries.

Their authority is relational. A technically healthy forest can retain dangerous delegated control. A sound PKI can permit unintended authentication authority. A hardened privileged-access platform can still depend on a lower-tier management plane.

RMF gives these conditions a place as risk. Its value depends on the analysis supporting it.

If an authorization boundary omits an identity dependency, its controls may be evaluated elsewhere. They may not be evaluated at all. If an assessment verifies MFA but ignores alternate authentication, its evidence can overstate assurance.

RMF becomes shallow only when the technical analysis is shallow.
