# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
#### Crucial Missing Concepts to Consider

#### 1.Enterprise Access Model (EAM) & Clean Source Principle

Microsoft's modern replacement for the legacy 3-Tier model, organizing system boundaries into Control Plane, Management Plane, and User Plane, anchored by the Clean Source Principle (where security controls must match or exceed the security of the asset being managed).

#### 2. AdminSDHolder & SDProp Mechanics

The automated Active Directory background process (`SDProp`) that runs every 60 minutes to enforce strict, un-inherited Access Control Lists (ACLs) onto protected administrative objects based on the `AdminSDHolder` container template.

#### 3. DCSync & Directory Replication Service (MS-DRSR)

Exploiting the `DS-Replication-Get-Changes` and `DS-Replication-Get-Changes-All` extended rights to request user and computer password hashes directly from a Domain Controller over RPC without executing code on the DC itself.

1. Shadow Credentials (`msDS-KeyCredentialLink`): Exploiting Key Credential provisioning (Public Key Cryptography for Initial Authentication) by injecting raw public keys into an object's `msDS-KeyCredentialLink` attribute to take over Tier 0 accounts without changing their passwords.
{% endhint %}
