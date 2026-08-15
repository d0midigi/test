# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### 1. GPO Modification Control Paths (`WriteDACL` / `GenericAll` / `gPCFileSysPath`)

How granting modification rights over a GPO container in Active Directory or its underlying file structure in `SYSVOL` allows an attacker to achieve instant, silent remote code execution on every computer or user processing that policy.

#### 2. SYSVOL Vulnerabilities & Legacy Passwords (`cpassword` / MS14-025)

The legacy Group Policy Preferences (GPP) mechanism that stored AES-encrypted passwords in XML files inside `SYSVOL` with a publicly known static decryption key.

#### 3. Loopback Processing Modes (Merge vs. Replace)

How Group Policy Loopback Processing alters policy application when users log on to specific high-security hosts (e.g., Jump boxes, Terminal Servers) and the corresponding security risks when misconfigured.

#### 4. Group Policy Object Delegation & Delegation Abuse

How non-default GPO creator permissions (`Group Policy Creator Owners`) and local administrative rights can be abused to create cross-tier GPO persistence.
{% endhint %}
