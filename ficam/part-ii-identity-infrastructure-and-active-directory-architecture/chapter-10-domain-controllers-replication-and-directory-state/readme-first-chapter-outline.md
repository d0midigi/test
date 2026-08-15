# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. Directory Replication Service (DRS) Remote Protocol Abuse**

The `DSGetNCChanges` RPC interface used by DCSync operations to impersonate a Domain Controller and extract secrets over the wire without executing code on a DC.

#### 2. Offline Database Extraction via Volume Shadow Copy (VSS)

Intercepting the `NTDS.dit` file and `SYSTEM` registry hive from live storage volumes or system backups to decrypt domain secrets offline.

#### 3. RODC Password Replication Policy (PRP) Misconfigurations

Unintentionally allowing high-privileged accounts (e.g., Domain Admins, service accounts) to cache credentials on Read-Only Domain Controllers deployed in untrusted branch environments.

#### 4. Directory Services Restore Mode (DSRM) Persistence

Exploiting local DSRM administrative account credentials or modifying registry logon behavior to maintain persistence on Domain Controllers.
{% endhint %}
