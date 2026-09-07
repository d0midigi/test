---
icon: gem
---

# Chapter 80 - Domain Controller Persistence, Authentication Backdoors, and Credential-Validation Subversion (Offensive)

### Abstract

Once an adversary reaches a domain controller, persistence no longer has to resemble a conventional backdoor. The attacker may instead target the systems that decide whether credentials are valid, which authentication packages are trusted, which secrets survive password changes, and which identities can authenticate independently of ordinary Active Directory administration. This chapter examines domain-controller persistence primarily from the offensive perspective, focusing on Directory Services Restore Mode credentials, Security Support Providers, Local Security Authority packages, password-filter and notification packages, credential-provider manipulation, authentication-process tampering, Skeleton Key–style backdoors, Kerberos and NTLM validation paths, machine-account authority, registry-based security-package loading, and persistent access that survives account remediation. Particular attention is given to persistence that manipulates authentication infrastructure rather than simply adding privileged accounts. Defensive treatment follows through domain-controller isolation, LSA protection, code integrity, registry and module baselining, credential rotation, DSRM governance, memory and authentication telemetry, forensic validation, and complete trust reconstitution. Domain recovery is incomplete whenever an adversary may still influence the mechanism that decides who is allowed to authenticate.
