# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Concepts Missing to Consider**

#### **1. Golden SAML & AD FS Key Theft**

Stealing the private key of the AD FS Token-Signing Certificate (`TokenSigningCert`) from on-premises Active Directory to forge SAML assertions, bypassing CAC/PIV MFA, and achieving persistent cloud access across GCC High/Azure Government tenants.

#### 2. Azure Government & DoD Cloud Boundaries (GCC High, IL4/IL5/IL6)

Technical mechanics, endpoint isolation, and FICAM alignment differences distinguishing commercial Entra ID from Microsoft Government and DoD Impact Level (IL4/IL5/IL6) clouds.

#### 3. Pass-the-PRT & Cloud JWT Exploitation

Extracting Primary Refresh Tokens (PRT) and session keys from LSASS/Cloud AP on hybrid endpoints to bypass Conditional Access, device compliance mandates, and CAC/PIV MFA.

#### 4. Entra Connect Account Abuse (MSOL\_ / ADSync)

Decrypting local `ADSync` database credentials to compromise the high-privilege `MSOL_` service account, allowing direct account takeover, password injection, or directory manipulation between on-premises AD and cloud tenants.


{% endhint %}
