---
icon: clover
---

# Chapter 79 - NTLM Credential Reuse, Pass-the-Hash, and Remote Authentication Abuse (Offensive)

### Abstract

NTLM allows Windows systems to authenticate a principal without transmitting the underlying password, but that design also means possession of certain password-derived material can sometimes substitute for possession of the password itself. This chapter examines NTLM primarily from the offensive perspective, focusing on hash reuse, Pass-the-Hash, local administrator credential reuse, remote administrative authentication, machine-account material, service accounts, Remote Procedure Call, Server Message Block, Windows Management Instrumentation, service control, Windows Remote Management, Remote Desktop conditions, and the transition from NTLM-derived access into Kerberos or broader Active Directory authority. Particular attention is given to distinguishing Pass-the-Hash from password cracking, NTLM relay, cached credential recovery, and ticket-based attacks. Defensive treatment follows through Windows Local Administrator Password Solution, NTLM restriction, privileged-access isolation, remote User Account Control, firewall and protocol boundaries, phishing-resistant authentication, credential placement reduction, telemetry correlation, and attack-path validation. The chapter establishes that password secrecy alone is insufficient whenever reusable password-equivalent material can authenticate directly.
