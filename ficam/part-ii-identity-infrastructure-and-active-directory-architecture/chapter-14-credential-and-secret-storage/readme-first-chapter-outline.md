# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. DPAPI Domain Master Keys & Backup Key Extraction**

The cryptographic hierarchy of Domain DPAPI, where the Domain Controller's private backup key (`PvkKey`) can decrypt any domain user's DPAPI Master Keys, exposing browser credentials, WiFi keys, and encrypted files domain-wide.

#### 2. Virtualization-Based Security (VBS) & Credential Guard

The hardware-isolated security architecture (Isolated User Mode / Hypervisor-Enforced Code Integrity) designed to protect LSASS memory secrets and prevent Pass-the-Hash (PtH) / Pass-the-Ticket (PtT) credential dumping.

#### 3. Delegated Managed Service Accounts (dMSA)

Windows Server 2025 dMSA architecture, which binds service account credentials directly to specific machine identities and eliminates static password rot without requiring complex KDS key distribution loops.

#### 4. Primary Refresh Tokens (PRT) & Hybrid Identity Artifacts

Device-bound OAuth/OIDC tokens stored in Cloud AP LSASS plugin memory and protected by TPM keys, serving as the bridge between Active Directory on-premises credentials and Entra ID cloud access.
{% endhint %}

### Key Learning Objectives

* Analyze the cryptographic storage mechanisms used by Active Directory to protect user hashes, Kerberos keys, and DPAPI master keys.
* Execute and Evaluate offensive techniques used to dump domain credentials offline (NTDS extraction) and live over the network (DCSync).
* Architect defensive controls that satisfy FICAM high-assurance credential requirements, drastically reducing credential exposure vectors across the domain lifecycle.
* Deploy telemetry collectors and detection mechanisms capable of alerting on unauthorized credential extraction attempts in near-real-time.
