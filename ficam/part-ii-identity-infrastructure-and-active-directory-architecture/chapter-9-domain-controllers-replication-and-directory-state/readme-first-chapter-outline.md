# ❗ README FIRST-Chapter Outline

{% hint style="info" %}
_These are just ideas for what this chapter can provide. If I find that the previous chapter is making this chapter move in a different direction than what is listed below, I will make adjustments to reflect direction. They are not mandatory for inclusion although they will help to strengthen the overall context of chapter concepts._
{% endhint %}

{% hint style="danger" %}
**Crucial Missing Concepts to Consider**

#### **1. Confidential Attributes & RODC Filtered Attribute Sets (FAS):**

Attributes marked with `SEARCH_FLAGS = 128 (0X80)` (Confidential) or added to the Read-Only Domain Controller (RODC) Filtered Attribute Set to prevent secret exposure to non-privileged users or branch offices.

#### 2. Schema Poisoning & Stealth Persistence:

Modifying existing `attributeSchema` or `classSchema` definitions (or adding rogue attributes) to hide payload data, establish backdoors, or bypass auditing tools.

#### 3. Global Catalog Partial Attribute Set (PAS):

The subset of attributes replicated forest-wide to Global Catalog servers (`isMemberOfPartialAttributeSet = TRUE`), impacting cross-domain search performance and identity exposure.

#### 4. Replication Metadata & State Verification:

Mechanics of `msDS-ReplAttributeMetaData`, Update Sequence Numbers (USN), and `invocationID` used to verify firectory state integrity and detect USN Rollback or covert object manipulation.
{% endhint %}
