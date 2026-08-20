# 5.4.3 Federation Assurance Levels

Federation Assurance Level (FAL) applies when identity and authentication information is conveyed between separately administered parties through federation.

At FAL1, the current NIST requirements establish baseline protections such as signed assertions, audience restriction, and replay protection. ([9](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63c-4.pdf))

FAL2 adds stronger protections against attacks such as assertion injection, requires the federation transaction to be initiated by the relying party, restricts the assertion to a single relying party, and requires a pre-established trust agreement. ([9](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63c-4.pdf))

FAL3 provides the strongest federation assurance and requires the relying party to verify that the subscriber controls an additional bound authenticator rather than relying solely on possession of the assertion. NIST explicitly positions that added subscriber authentication as protection even in scenarios involving compromise of the identity provider. ([9](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63c-4.pdf))

This becomes extremely important in federal federation.

A signed assertion is not equivalent to an inherently trustworthy assertion.

Its trustworthiness depends on the issuer, signing infrastructure, federation protocol, relying-party validation, audience restrictions, replay protections, key management, and the conditions under which the assertion was created.

Federation assurance exists because passing identity across a boundary introduces risks that do not exist in exactly the same form when authentication and resource access occur inside one system.
