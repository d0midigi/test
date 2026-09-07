---
icon: hexagon-nodes
---

# Chapter 67 - Authentication Coercion, Credential Relay, and Protocol Pivoting Across Federal Identity Environments (Offensive)

### Abstract

Authentication relay operations exploit a fundamental weakness in identity trust: a valid authentication exchange may be accepted by a service other than the one the principal intended to access. This chapter examines offensive identity operations built around authentication coercion, NTLM capture and relay, protocol negotiation, SMB, LDAP, LDAPS, HTTP, WebDAV, Active Directory Certificate Services, machine-account authentication, name-resolution manipulation, and the chaining of relayed authority into privilege escalation or persistence. The offensive discussion leads with target selection, coercion opportunities, relay feasibility, signing and channel-protection conditions, authenticated-action selection, and movement from a single forced authentication into consequential directory authority. Defensive treatment follows each attack surface through protocol hardening, Extended Protection for Authentication, SMB and LDAP signing, channel binding, NTLM reduction, certificate enrollment protection, network controls, telemetry, and attack-path validation. The chapter emphasizes that relay is not simply credential theft: it is the unauthorized redirection of legitimate authentication authority into an attacker-selected security context.
