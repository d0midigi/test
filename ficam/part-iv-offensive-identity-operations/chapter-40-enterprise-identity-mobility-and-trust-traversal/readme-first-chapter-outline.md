# ❗ README FIRST-Chapter Outline

{% hint style="danger" %}
**Crucial Concepts Missing to Consider**

#### 1. SID History Injection & Trust Transitivity Exploitation

Exploiting cross-domain/forest trust relationships by injecting privileged Security Identifiers (e.g., Enterprise Admins SID `S-1-5-21-...-519`) into the `sIDHistory` attribute of a compromised domain user, allowing horizontal and vertical privilege escalation across forest boundaries when SID Filtering is disabled.

#### 2. Selective Authentication & Forest Trust Boundary Weaknesses

Bypassing or abusing Selective Authentication configurations across external and forest trusts, including misconfigured Authentication Policies or over-permissive Local Security Authority (LSA) secret mappings.

#### 3. Cross-Forest Kerberos Ticket Referral Abuse

Crafting inter-realm TGTs (using the inter-realm trust key) to cross Active Directory forest boundaries, highlighting how SID Filtering enforcement, Selective Authentication, and Kerberos Name Canonicalization impact cross-forest identity traversal.

#### 4. Hybrid Trust Traversal (Entra ID B2B & Cross-Tenant Access Policies)

Traversing identity boundaries between on-premises Active Directory forests and multi-tenant Entra ID environments by exploiting misconfigured B2B guest permissions, Cross-Tenant Access Policies (CTAP), and federated trust relationships (AD FS/PingFederate).
{% endhint %}
