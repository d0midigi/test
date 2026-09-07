---
icon: cc-mastercard
---

# Chapter 84 - Identity Enrollment, Account Recovery, Help-Desk Abuse, and High-Assurance Rebinding (Offensive)

### Abstract

Strong authentication can be defeated without breaking the authenticator if an adversary can manipulate the process used to issue, replace, recover, or rebind it. This chapter examines enrollment and recovery primarily from the offensive perspective, treating help desks, identity-proofing workflows, PIV/CAC issuance, biometric verification, Microsoft Entra authentication-method registration, Temporary Access Pass, FIDO2 and passkey enrollment, Windows Hello for Business provisioning, device registration, certificate reissuance, derived PIV credentials, account recovery, and emergency access as identity attack surfaces. Particular attention is given to attacks that exploit weaker recovery assurance than the authentication mechanism being recovered, allowing an adversary to replace a trusted authenticator without defeating it. Defensive treatment follows through Identity Assurance Level, Authenticator Assurance Level, and Federation Assurance Level continuity; independent verification; privileged recovery boundaries; transaction logging; phishing-resistant enrollment; biometric presentation-attack resistance; recovery-channel restrictions; and post-rebinding validation. The chapter establishes that recovery is not administrative support—it is a new identity-binding decision capable of transferring authentication authority to another principal.
