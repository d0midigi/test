# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. Primary Group ID  (primaryGroupID) Masking & Enumeration Evasion**

Modifying a principals' `primaryGroupID` attribute (e.g., setting it to `514` for Domain Admins) removes the account from the standard `member` / `memberOf` linked-attribute list, effectively hiding privileged group membership from standard LDAP query filters.

#### 2. Dynamic Access Control (DAC) & Conditional ACEs

Implementing ABAC in AD via user/resource claims, Central Access Policies (CAPs), Central Access Rules (CARs), and Callback/Conditional Access Control Entries evaluated during Kerberos authentication.

#### 3. Security Descriptor Propagator (SDProp) & AdminSDHolder Mechanics

The background process that periodically overwrites the security descriptors of protected high-privileged accounts and groups with the DACL from the `AdminSDHolder` container, invalidating explicit ACL modifications or persistence mechanisms.

#### 4. Token Bloat & Kerberos PAC Truncation

Deep group nesting architectures (AGDLP/AGUDLP) pushing Kerberos authorization data (PAC) beyond default HTTP/RPC buffer sizes (`MaxTokenSize`), causing unexpected authentication failures or silent PAC truncation.
{% endhint %}
