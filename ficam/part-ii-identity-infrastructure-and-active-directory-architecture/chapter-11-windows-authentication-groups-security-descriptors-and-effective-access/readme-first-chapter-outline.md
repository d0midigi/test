# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. LDAP Channel Binding & NTLM Relay Vulnerabilities**

The operational distinction between LDAP Signing (integrity) and LDAP Channel Binding Tokens (CBT / EPA). Unsigned or un-bound LDAP requests enable NTLM Relay attacks to elevate privileges or modify directory bojects without valid Kerberos tickets.

#### 2. Authentication Coercion Primitives

Protocol abuse vectors in RPC interfaces - such as Mapper (EPMAP), and MS-RPRN (`PrinterBug`) - the force Domain Controllers to initiate outbound NTLM authentication to attacker-controlled targets.

#### 3. RPC Dynamic Port Allocation & Firewall Traversal

Mechanics of the RPC Endpoint Mapper (EPMAP) mapping fixed port 135 to dynamic high-port ranges (`49152-65535`) ,creating perimeter firewall challenges and cross-segment visibility blind spots.

#### 4. SAMR/LSARPC Reconnaissance Restrictions

Migrating anonymous or low-privileged diretory enumeration via policy controls like `RestrictRemoteSAM` to prevent SAMR/LSARPC user and SID mapping.
{% endhint %}
