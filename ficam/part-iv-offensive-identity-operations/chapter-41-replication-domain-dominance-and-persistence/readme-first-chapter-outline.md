# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Concepts Missing to Consider**

#### 1. DCSync & Directory Replication Service Remote Protocol (MS-DRSR) Abuse

Bypassing traditional filesystem host controls by invoking `DSGetNCChanges` via RPC to request password hashes (including `krbtgt` and historical NTLM/AES keys) directly from Domain Controllers as an authorized replication principal (`Replicating Directory Changes` rights).

#### 2. DCShadow & Rogue Domain Controller Injection

Temporarily registering an attacker-controlled workstation or server as a rogue Domain Controller using LDAP schema modifications (`classSchema`/`attributeSchema`) and RPC call bindings (`RPC_C_AUTHN_GSS_NEGOTIATE`) to push persistent, stealthy attribute changes (e.g., SID History, AdminSDHolder DACLs) without triggering standard object modification event logs.

#### 3. Dual-Rotation `krbtgt` Key Lifecycle Mechanics

Managing the technical lifecycle and dual-rotation process for the Kerberos Ticket Granting Service Account (`krbtgt`) password to completely invalidate historical Golden Tickets while accounting for ticket lifetime buffers (`maxTicketAge`) and preventing enterprise pre-authentication failures.

#### 4. LSASS Memory Patching for In-Memory Persistence (Skeleton Key)

&#x20;Patching the LSASS process memory space on live Domain Controllers to insert master password validation handles (e.g., Skeleton Key attacks) that allow arbitrary logon while preserving valid user authentication streams without modifying `NTDS.dit` on disk.
{% endhint %}

