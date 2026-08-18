---
icon: lock-a
---

# Chapter 20 - PIV, CAC, and Passwordless Authentication

### Abstract

Federal Identity, Credential, and Access Management (FICAM) frameworks mandate hardware-backed, phishing-resistant multi-factor authentication (MFA) to achieve Authenticator Assurance Level 3 (AAL3) under NIST SP 800-63B. Smart cards—specifically Personal Identity Verification (PIV) and Common Access Cards (CAC)—form the backbone of public sector authentication, relying on Kerberos PKINIT to issue Kerberos Ticket Granting Tickets (TGTs) without cleartext password exposure. As organizations modernize, passwordless architectures like Windows Hello for Business (WHfB), FIDO2 security keys, and Entra Kerberos extend these hardware-bound cryptographic guarantees across hybrid, cloud, and remote endpoint environments.

This chapter provides a detailed technical breakdown of smart cards, PKINIT exchanges, and modern passwordless authentication models. It examines PIV/CAC certificate-to-account mapping, TPM key protection, derived credentials, and Windows Hello for Business deployment models (Key Trust, Certificate Trust, and Cloud Kerberos Trust). By analyzing adversary exposure surfaces—such as weak certificate mapping exploitation, PIN brute-forcing, and shadow credential injection—alongside defensive controls (SCRIL enforcement, strong mapping policies, and TPM-bound trust enforcement), this chapter equips security architects to deploy unbreachable, passwordless identity boundaries.

##
