# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Concepts Missing to Consider**

#### 1. Foreign Security Principals (FSPs)

Objects created in a local domain's `CN=ForeignSecurityPrincipals` container to represent users or groups from a trusted external domain when added to local domain groups.

#### 2. SID History Abuse & SID Filtering Bypasses

Injecting extra SIDs (like RID 512 Domain Admins) into the `sIDHistory` attribute during migration or cross-trust Kerberos ticket forging (Extra SIDs / Golden Tickets over trusts).

#### 3. Kerberos PAC Validation & CVE-2022-37969 / CVE-2022-38023

Microsoft signatures and hard limits on Kerberos Privilege Attribute Certificate (PAC) validation across forest and realm trusts to prevent cross-domain privilege escalation.

#### 4. Linux Keytab Exposure & Service Ticket Theft

Security risks surrounding unencrypted keytab file storage (`/etc/krb5.keytab`) on Linux endpoints joined via SSSD or Samba, enabling offline Kerberos hash extraction.
{% endhint %}
