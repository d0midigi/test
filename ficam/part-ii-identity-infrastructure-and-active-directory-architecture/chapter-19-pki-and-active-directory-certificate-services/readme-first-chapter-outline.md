# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Concepts Missing to Consider**

#### 1. ESC1–ESC13 Misconfiguration Taxonomy

The definitive offensive framework (originally defined by SpecterOps and continuously expanded) detailing specific template, permission, and issuance misconfigurations that lead to immediate domain compromise or persistent backdoors via AD CS.

#### 2. PKINIT and Schannel Authentication Mechanics

How Active Directory maps X.509 client certificates to security principals during Kerberos Public Key Cryptography for Initial Authentication (PKINIT) or TLS Schannel binds, converting certificate control into full Ticket-Granting Tickets (TGTs).

#### 3. AD CS Shadow Credentials & Certificate-Based Persistence

Injecting rogue certificates, forging long-lived client certificates, or manipulating user `altSecurityIdentities` attributes to maintain persistent, undetected access across Tier 0 objects.

#### 4. Certificate Authority Role Rights & ACL Abuse

Exploiting delegated CA management rights (such as `Manage CA` or `Manage Certificates`) to approve pending requests, reconfigure templates remotely, or issue arbitrary certificates without template-level privileges.
{% endhint %}
