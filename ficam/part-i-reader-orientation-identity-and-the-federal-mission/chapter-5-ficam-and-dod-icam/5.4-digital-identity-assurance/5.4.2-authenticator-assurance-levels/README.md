# 5.4.2 Authenticator Assurance Levels

Authenticator Assurance Level (AAL) concerns the authentication event.

AAL1 establishes basic confidence that the claimant controls an authenticator bound to the subscriber account. The current NIST SP 800-63B-4 permits single-factor or multi-factor mechanisms at AAL1 and recommends making multifactor options available. ([8](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b-4.pdf))

AAL2 provides high confidence in control of one or more authenticators and requires multifactor authentication. The current Revision 4 requirements also require verifiers to offer a phishing-resistant option at AAL2 and specifically require federal agencies to require their staff, contractors, and partners to use phishing-resistant authentication when accessing federal information systems. ([8](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b-4.pdf))

AAL3 raises the requirements further. It requires phishing resistance, replay resistance, authentication intent, public-key cryptography for the relevant cryptographic authenticator, non-exportable private-key material, and hardware-protected isolation of authentication keys. Syncable authenticators are not permitted at AAL3 because the private key must remain non-exportable. ([8](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b-4.pdf))

The resulting architecture has direct implications for federal identity modernization.

AAL is not simply a count of factors.

Two factors do not automatically produce the security characteristics required at higher assurance.

Phishing resistance, authenticator key protection, replay resistance, verifier properties, and the design of the authentication protocol matter.

This is why older diagrams that equate AAL1 with “password,” AAL2 with “two factors,” and AAL3 with “smart card” are useful only as introductory illustrations and become misleading when treated as normative architecture.
