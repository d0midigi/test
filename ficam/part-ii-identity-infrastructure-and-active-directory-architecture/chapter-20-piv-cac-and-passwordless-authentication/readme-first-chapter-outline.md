# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. Smart Card Required for Interactive Logon (SCRIL)**

Setting the `SMARTCARD_REQUIRED` flag (`userAccountControl` bit `0x40000`), which causes Active Directory to automatically randomize the user's NT hash to a 128-bit secret, effectively mitigating NTLM Pass-the-Hash (PtH) attack vectors.

#### 2. Explicit Certificate Mapping & KB5014754 Hardening

Enforcing strong certificate mapping rules via explicit SIDs (`1.3.6.1.4.1.311.25.2`) or `altSecurityIdentities` attributes to prevent certificate-based account takeover via weak mapping fallbacks.

#### 3. NIST SP 800-157 & FIPS 201-3 Compliance

Implementing Derived PIV Credentials (DPC) on mobile and unmanaged devices to maintain Authenticator Assurance Level 3 (AAL3) under NIST SP 63B without physical smart card readers.

#### 4. CTAP2 & WebAuthn Protocol Mechanics

How Client-to-Authentiator Protocol 2 (CTAP2) coordinates with Trusted Platform Modules (TPM) and external FIDO2 tokens to issue hardware-bound, non-exportable cryptographic assertions for domain logon.
{% endhint %}





