# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. Non-Person Entity (NPE) Authentication via Certificate-Based Identities**

Using PKI certificates, smart cards, and PIV/CAC cards for non-human entities (service principals, container workloads, network appliances) to meet FICAM Authenticator Assurance Level 3 (AAL3) requirements.

#### 2. Workload Identity Federation & Shadow Identities

Connecting on-premises Active Directory service objects to cloud workload identities (e.g., Entra ID Workload Identities, AWS IAM Roles), using short-lived tokens to eliminate long-lived explicit credentials.

#### 3. Orphaned Accounts & Entitlement Creep

Security risks associated with stale user, computer, and service objects that retain high-privilege access due to broken Identity Lifecycle (JML) processes.

#### 4. Group Managed Service Account (gMSA) Password Blob Processing

The mechanics of how member hosts query the Group Key Distribution Service (KDS) via RPC (`MS-GKDI`) to generate and rotate account passwords locally without human intervention.
{% endhint %}
