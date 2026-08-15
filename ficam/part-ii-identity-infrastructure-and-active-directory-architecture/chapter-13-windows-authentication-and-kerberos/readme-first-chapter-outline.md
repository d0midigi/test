# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. AS-REP Roasting (DONT\_REQ\_PREAUTH)**

Accounts configured without Kerberos pre-authentication allow unauthenticated callers to request AS-REP responses containing encrypted ticket data and crack passwords offline.

#### 2. Golden & Silver Ticket Crafting

Forging Ticket Granting Tickets using the domain `krbtgt` hash (Golden) or forging Service Tickets using service account hashes (Silver) to bypass authentication and inject arbitrary PAC claims.

#### 3. Kerberos Armoring (FAST)

Flexible Authentication Secure Tunneling (`FAST`) protects pre-authentication exchanges against offline password cracking and AS-REP roasting vectors using an armored TLS-like channel.

#### 4. Pass-the-Hash (PtH) & Pass-the-Ticket (PtT)

Reusing NTLM hashes or Kerberos tickets extracted from LSASS memory to authenticate without kowing cleartext credentials.
{% endhint %}
