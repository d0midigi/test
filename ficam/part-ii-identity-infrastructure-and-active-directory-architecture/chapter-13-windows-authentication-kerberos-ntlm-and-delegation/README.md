---
icon: windows
---

# Chapter 13 - Windows Authentication, Kerberos, NTLM, and Delegation

### Abstract

Windows authentication converts credentials into security contexts that Active Directory and Windows systems can trust. This chapter examines the Local Security Authority (LSA), LSASS, Security Support Provider Interface (SSPI), local and domain logon, machine authentication, Netlogon, NTLM, Kerberos, the Key Distribution Center (KDC), ticket-granting tickets, service tickets, preauthentication, service principal names, delegation, PKINIT, smart-card authentication, authentication policies, and Protected Users. Offensive analysis examines password-derived authentication, pass-the-hash, ticket theft and replay, Kerberoasting, AS-REP roasting, forged Kerberos tickets, delegation abuse, NTLM relay, and downgrade paths. Defensive analysis focuses on phishing-resistant authentication, Kerberos hardening, NTLM reduction, encryption policy, delegation control, authentication silos, privileged-session isolation, telemetry, and incident response. The chapter emphasizes that authentication strength depends not only on the credential presented, but also on the protocol, endpoint, cryptographic material, delegation path, and security context through which that identity is accepted.

