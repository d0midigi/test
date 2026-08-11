# 5.4 Digital Identity Assurance

Digital identity assurance separates three questions that are frequently compressed into one vague statement that an identity is “high assurance.”

Current NIST guidance intentionally treats them separately.

Identity Assurance Level addresses confidence in the relationship between a subject and the real-world identity being claimed.

Authenticator Assurance Level addresses confidence that the claimant controls the authenticator associated with the subscriber account during authentication.

Federation Assurance Level addresses protections applied when authenticated identity information is conveyed through a federation transaction.

The current NIST SP 800-63-4 suite was finalized on July 31, 2025 and supersedes the Revision 3 suite. Its companion volumes SP 800-63A-4, SP 800-63B-4, and SP 800-63C-4 contain the detailed requirements for identity proofing, authentication, and federation respectively. ([7](https://csrc.nist.gov/pubs/sp/800/63/4/final))

The separation is more than administrative taxonomy.

An identity can be established with strong confidence and authenticated weakly.

A strongly authenticated account may have been inadequately proofed.

Both of those properties may be strong while a federation transaction lacks protections appropriate to the relying application's risk.

The assurance levels therefore describe different parts of the trust chain.
