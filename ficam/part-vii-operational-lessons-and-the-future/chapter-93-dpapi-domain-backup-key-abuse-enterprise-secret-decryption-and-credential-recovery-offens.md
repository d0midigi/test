---
icon: dice-d20
---

# Chapter 93 - DPAPI Domain Backup Key Abuse, Enterprise Secret Decryption, and Credential Recovery (Offensive)

### Abstract

Windows Data Protection Application Programming Interface (DPAPI) protects credentials, browser secrets, private keys, application tokens, wireless profiles, and other sensitive material by binding encryption to user or machine identity. In a domain, however, recovery mechanisms introduce an enterprise-level dependency: domain backup keys can allow authorized recovery of user DPAPI material when ordinary user-derived protection is unavailable. This chapter examines DPAPI primarily from the offensive perspective, progressing from master-key discovery and user-context decryption through domain backup key identification, domain-controller recovery authority, credential-store targeting, browser and application secret recovery, certificate private-key exposure, scheduled-task and service credentials, and offline decryption of collected profiles. Particular attention is given to the difference between stealing one user’s master key and obtaining domain-level recovery material capable of affecting many users. Defensive treatment follows through domain-controller protection, backup-key custody, Credential Guard, credential minimization, certificate-key protection, browser-policy reduction, secret rotation, forensic scoping, and domain recovery.
