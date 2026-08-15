Figure Specifications



Chapter 1



For production in Lucidchart (Figures 101, 1-2,1-3, 1-4) and Canva (Figures 1-5, 1-6).



Springer manuscript minimum: 300 DPI, exported as high-res PNG, SVG, or PDF



**Figure 1-1. Active Directory as Part of the Federal Identity Trust System**



* **Recommended Tool:** Lucidchart
* **Body Text Reference:** Section 1.1.4
* **Layout:** Hub-and-spoke or conecntirc ring diagram
* **Center Element:** A box labeled "Active Directory Domain / Forest" - this is the hub.



Six surrounding components connected to the center by directional arrows showing trust flow directions.



**1. Certificate Authority / Federal PKI**

\- **Arrow direction:** pointing INWARD toward AD

\- **Arrow label:** "Certificate Trust"

\- **Note:** CA issues credentials the domain accepts



**2. Active Directory Federation Services (AD FS) / Token-Signing Infrastructure**

\- **Arrow direction:** BIDIRECTIONAL

\- **Arrow label:** "SAML assertions / federation trust"

\- **Note:** Federation extends trust outwards to relying parties



**3. Microsoft Entra ID / Synchronization Bridge**

\- **Arrow direction:** BIDIRECTIONAL

\- **Arrow label:** "Synchronized credentials / cloud identity"

\- **Note:** Synchronization flows both directions



**4. Mission Partners / Coalition Access**

\- **Arrow direction:** pointing INWARD

\- **Arrow label:** "Federated authentication"

\- **Note:** External trust flowing into the domain



**5. Authoritative Attribute Sources / Personnel and Clearance Systems**

\- **Arrow direction:** pointing INWARD

\- **Arrow label:** "Identity attributes"

\- **Note:** Attributes flow into the directory



**6. Privileged Access Infrastructure / Tier 0 Systems**

\- **Arrow direction:** INWARD and internal loop

\- **Arrow label:** "Administrative control"

\- **Note:** Governs the domain itself



**Title:** "The Federal Identity Trust System"



**Caption:** Figure 1-1. Active Directory operates at the center of a broader federal identity trust system. Each surrounding component extends, delegates, or depends upon the trust the domain produces.

==========



**FIGURE 1-2. Domain Boundary Versus Identity Trust System Boundary**



* **Recommended Tool:** Lucidchart
* **Body text reference:** Section 1.1.3
* **Layout:** Two concentric boundary shapes - inner nested inside outer.
* **Inner boundary:** (smaller, solid line)

  * **Label:** "Domain / Forest Boundary"
  * **Contents inside:** Domain Controllers, NTDS.dit, Group Policy, Kerberos / NTLM, krbtgt
* **Outer body:** (larger, dashed line)

  * **Label:** "Identity Trust System Boundary"
  * **Contents in the ring between inner and outer:** Certificate Authorities, Federation Services, Cloud Identity Platform, Mission-Partner Trust Relationships, Synchronization Infrastructure, Authoritative Attribute Sources



**Attack path illustration:** A red arrow labeled "Attack paths cross both boundaries" originating outside the outer boundary, passing through a component in the outer ring (e.g., Federation Services), and reaching the inner domain.



**Caption:** Figure 1-2. The domain and forest boundary is nested within the larger identity trust system boundary. Attack pathways frequently originate or traverse components outside the domain before reaching domain assets.

==========



**FIGURE 1-3. Administrative View Versus Attacker-Control Path View**



* **Recommended Tool:** Lucidchart
* **Body text reference:** Section 1.5.2
* **Layout:** Split panel - left and right side by side, clearly divided.
* **Left panel:** labeled "Administrative View"

  * Clean organizational hierarchy / org chart structure
  * **Boxes for:** Domain Admins → Tier 1 Admins → Help Desk → Standard Users → Service Accounts
  * Clean vertical lines connecting levels, orderly, and hierarchical
  * **Color:** Neutral blues or grays



**Right panel -** labeled "Attacker Control-Path View"

* Same entities (same boxes, same labels) but connected by permission edges rather than org-chart lines
* Dotted red arrows connecting nodes, labeled with permission types:

  * "`GenericWrite`"
  * "`WriteDACL`"
  * "`ForceChangePassword`"
  * "`AllExtendedRights`"
  * "`GenericAll`"
* Several arrow lead FROM Standard Users or Service Accounts UPWARD to Domain Admins through intermediate nodes - showing the attack pathway
* The graph looks like a web rather than a hierarchy
* **Color:** Red edges on the attack pathways, same neutral boxes.



**Caption:** Figure 1-3. The administrative view describes intended structure. The attacker control-path view reveals the permission relationships that structure enables - pathways invisible to compliance review but clearly visible to enumeration tools.

==========



**FIGURE 1-4. From Cyber Kill Chain to Identity Kill Chain**



* **Recommended Tool:** Lucidchart
* **Body text reference:** Section 1.7.1
* **Layout:** Two parallel vertical columns with stage labels aligned horizontally across both columns
* **Left column header:** "Cyber Kill Chain (Lockheed Martin)"
* **Left column - seven stages top to bottom:**

  * 1\. Reconnaissance
  * 2\. Weaponization
  * 3\. Delivery
  * 4\. Exploitation
  * 5\. Installation
  * 6\. Command and Control
  * 7\. Actions on Objectives



* **Right column header:** "Active Directory Identity Kill Chain"
* **Right column - seven stages aligned with the left:**

  * 1\. Passive Identity Reconnaissance
  * 2\. Active Directory Enumeration
  * 3\. Initial Identity Acquisition
  * 4\. Credential Acquisition
  * 5\. Identity Authority Expansion
  * 6\. Enterprise Identity Mobility
  * 7\. Persistence and Domain Dominance
* **Connecting elements:** Horizontal arrows connecting each left stage to its right equivalent
* **Color treatment:** Color gradient from lighter shads at top (recon) to darker/deeper shades at bottom - indicating escalating privilege and impact as the chain progresses.



**Caption:** Figure 1-4. The traditional cyber kill chain stages map to identity-specific equivalents in Active Directory environments. The identity kill chain reflects credential-based intrusion patterns that do not require malware, exploits, or distinctive command-and-control channels.

==========



**FIGURE 1-5. Identity Trust Failure as Mission Risk**



* **Recommended tool:** Canva
* **Body text reference:** Section 1.10.1
* **Layout:** Central hub with five outward spokes
* **Center node:** "Tier 0 Identity Compromise" - styled with a red warning indicator or red background



**Five outward arrows** leading to mission function boxes:



1. **"Authentication for Sensitive Systems"**
* **Sub-label:** "Who can be trusted to access?"
* **Status indicator:** DEGRADED (red)

**2. "Federation with Mission Partners"**

* **Sub-label:** "Which partner sessions are clean?"
* **Status indicator:** UNTRUSTED (red)

**3. "Cloud Service Access"**

* **Sub-label:** "Which cloud authorizations are valid?"
* **Status indicator:** DEGRADED (red)

**4. "Certificate Trust"**

* **Sub-label:** "Which certificates can be relied upon?"
* **Status indicator:** UNTRUSTED (red)

**5. "Administrative Actions"**

* **Sub-label:** "Which recovery steps are safe?"
* **Status indicator:** DEGRADED (red)



**Footer text** below the entire diagram (one line): "Mission operates on identity decisions it can no longer trust."



**Caption:** Figure1-5. A Tier 0 identity compromise propagates outward to every mission function that depends on the identity trust system. Recovery requires restoring trusted identity, not just rebuilding systems.

=========



**FIGURE 1-6. Book Structure: Architecture, Offense, Defense, and Warfare**



* **Recommended tool:** Canva
* **Body text reference:** Section 1.13.1
* **Layout:** Four horizontal bands stacked vertically, each a different color



**Band 1 - Part 1** (lightest shade, top)

* **Large label:** "PART I - Foundations and Terrain"
* **Sub-label:** "Understand the identity trust system before it is attacked"
* **Left side:** "Chapters 1-8"
* **Right side:** "All Practitioners"



**Band 2 - Part II** (medium shade, warmer/amber color)

* **Large label:** "PART II - The Identity Attack Lifecycle"
* **Sub-label:** "Follow the adversary through seven stages of identity compromise"
* **Left side:** "Chapters 9-26"
* **Right side:** "Red Team / Security Engineers"



**Band 3 - Part III** (medium shade, cooler/blue color)

* **Large label:** "PART III - Defense, Detection, Recovery, and Governance"
* **Sub-label:** "Build, validate, and sustain the defensive mirror"
* **Left side:** "Chapters 27-43"
* **Right side:** "Blue Team / ISSOs / IR Leads"



**Band 4 - Part IV** (darkest shade, bottom)

* **Large label:** "PART IV - Operational Lessons and the Future"
* **Sub-label:** "Synthesize field experience and prepare for what comes next"
* **Left side:** "Chapter 44"
* **Right side:** "Senior Practitioners / Leaders"



**Caption:** Figure 1-6. The book's four parts map to sequential operational phases: understanding the terrain, following the adversary, building the defense, and preparing for the future identity battlespace.

==========



**PRODUCTION NOTES FOR SPRINGER SUBMISSION**



* **Minimum resolution:** 300 DPI for all figures
* **Preferred formats:** SVG (vector, scalable) or high-resolution PNG/PDF
* **Font:** Use a clean sans-serif (Arial, Helvetica, or Calibri) for all labels - avoid decorative fonts
* **Figure numbering:** Figures are numbered sequentially per chapter (Figure 1-1 through Figure 1-6 for Chapter 1)
* **Captions:** Captions go BELOW the figure, not above
* **Color:** Confirm with Apress production contact whether the book prints in color or black and white - it b/w, replace color coding with pattern fills or grayscale gradients
* **Accessibility:** Ensure sufficient contrast between text and background in all figures
* **Lucidchart export:** File > Export > PDF or SVG for best quality
* **Canva export:** Download > PDF Print (for highest quality) or PNG at custom size set to 300 DPI

==============

from pathlib import Path



report = r"""# Chapter 1 Full Technical, Structural, and Editorial Review



\## Manuscript Reviewed



\*\*Chapter:\*\* Identity as the Battlefield: Why Active Directory Security Is a Federal Mission Problem  

\*\*Source file:\*\* `Chapter 1.md`  

\*\*Approximate length:\*\* 25,082 words  

\*\*Review scope:\*\* Technical accuracy, Active Directory architecture, offensive and defensive security, federal and Department of Defense identity framing, Risk Management Framework alignment, chapter structure, consistency, terminology, tone, grammar, tables, case studies, exercises, and references.



\---



\# 1. Overall Verdict



Chapter 1 has a strong thesis, a credible differentiator, and the correct conceptual center of gravity:



> Active Directory security in a federal or defense environment cannot be evaluated only at the domain boundary. It must be evaluated as part of a larger identity trust system that includes directory services, certificate services, federation, cloud identity, authoritative attributes, privileged access, and mission-partner trust.



That thesis is clear, useful, and sufficiently distinct to support the rest of the book.



The chapter is \*\*not publication-ready yet\*\*. The deficiencies are repairable, but they require more than a grammar pass. The current manuscript contains:



\- Several publication-blocking technical inaccuracies

\- Conflicting statements about domains, forests, and security boundaries

\- An incorrect Risk Management Framework step count

\- Incorrect Kerberos, Active Directory replication, DCSync, and Group Policy statements

\- Overstated hybrid identity and federation claims

\- Uncorrected earlier versions of Sections 1.2.4 through 1.2.6

\- A reversed attack-lifecycle sequence

\- Incorrect or weak NIST SP 800-53 control mappings

\- Repeated thesis statements that materially inflate the chapter

\- Numbering gaps and inconsistent manuscript formatting

\- Numerous line-level grammatical and typographical errors

\- A reference base that is too small for the number of historical, technical, federal, and incident-specific claims



The chapter should be revised in controlled passes. It should \*\*not\*\* be regenerated from scratch. The central argument, chapter progression, several analytical sections, and the federal mission framing should be preserved.



\---



\# 2. What Is Working Well



\## 2.1 The central thesis is strong



The strongest contribution is the distinction between:



\- Active Directory as a domain and forest technology

\- The broader identity trust system in which Active Directory operates



This is the book's clearest differentiator. It successfully connects traditional Active Directory security with:



\- Federal Identity, Credential, and Access Management

\- Department of Defense Identity, Credential, and Access Management

\- Public key infrastructure

\- Federation

\- Cloud identity

\- Privileged access

\- Mission-partner access

\- Governance and authorization evidence



That integration should remain the chapter's primary organizing argument.



\## 2.2 The chapter follows a rational conceptual progression



The main progression is sound:



1\. Active Directory as a trust system

2\. Federal and defense identity context

3\. Identity as adversarial terrain

4\. Attacker thinking as a defensive capability

5\. Assume Breach

6\. Identity-specific attack lifecycle

7\. Defender visibility

8\. Mission risk

9\. Governance and evidence

10\. Book operating model and transition



The problem is not the sequence. The problem is repetition between adjacent sections and the amount of planning material appended after the narrative chapter.



\## 2.3 Several sections should be retained with targeted edits



The following sections are conceptually strong:



\- \*\*1.1.1 Active Directory Is More Than a Directory Service\*\*

\- \*\*1.1.2 The Difference Between a Domain and an Identity Trust System\*\*

\- \*\*1.3.8 Why Identity Governance Must Be Tested Against Real Attack Pathways\*\*

\- \*\*1.5.3 Access Versus Control\*\*

\- \*\*1.5.4 Why Attackers Scout for Attack Pathways and Not Just Vulnerabilities\*\*

\- \*\*1.6 Assume Breach as the Starting Point for Identity Security Engineering\*\*

\- \*\*1.9 The Defender's Problem: Seeing What the Attacker Sees\*\*

\- \*\*1.10 Federal Mission Risk and the Identity Control Plane\*\*

\- \*\*1.11 Governance, Authorization, and Evidence in Identity Security\*\*

\- \*\*The practical exercises\*\*



These sections require precision edits and some compression, not replacement.



\## 2.4 The chapter appropriately refuses to separate offense, defense, and governance



The manuscript correctly argues that federal identity assurance cannot be established by configuration compliance alone. Attack-path analysis, detection validation, recovery readiness, and evidence production belong in the same operational model.



That is a defensible and valuable position. It should remain, but the claim should not be repeated in five or six separate sections.



\---



\# 3. Publication-Blocking Technical Corrections



\## 3.1 Correct the Risk Management Framework from six steps to seven



\*\*Location:\*\* Section 1.11.2, approximately line 2039



The manuscript states that NIST Special Publication 800-37 Revision 2 defines a six-step process:



> Categorize, Select, Implement, Assess, Authorize, Monitor



That is incorrect. Revision 2 added \*\*Prepare\*\* as the first step. The seven steps are:



1\. Prepare

2\. Categorize

3\. Select

4\. Implement

5\. Assess

6\. Authorize

7\. Monitor



This must be corrected everywhere the Risk Management Framework process is described.



\---



\## 3.2 Correct the DCSync and Active Directory replication explanation



\*\*Location:\*\* Section 1.4.5, approximately line 1279



The current paragraph contains three separate errors:



1\. Active Directory replication does not generally occur “roughly every 90 minutes.”

2\. `gpupdate /force` does not force Active Directory replication.

3\. Event ID 4662 is not automatically generated for every replication operation in every environment.



The 90-minute interval is associated with ordinary background Group Policy refresh on member systems, not domain controller directory replication.



For Active Directory replication:



\- Intrasite change notification begins after a default delay of approximately 15 seconds.

\- Intersite replication follows the configured site-link schedule and interval, commonly 180 minutes by default unless changed.

\- `gpupdate /force` reapplies Group Policy settings. It does not initiate directory replication.

\- Event ID 4662 requires the applicable audit policy and System Access Control List configuration.

\- DCSync detection should not be described as depending only on source IP address and account identity. Detection can include replication-right GUIDs, non-domain-controller replication behavior, Directory Replication Service Remote Protocol traffic, account baselines, host roles, and correlated directory telemetry.



This paragraph requires complete replacement.



\---



\## 3.3 Separate stolen Ticket-Granting Tickets from Golden Tickets



\*\*Location:\*\* Section 1.4.2, approximately line 1223



The manuscript implies that a stolen valid Ticket-Granting Ticket can remain useful far beyond its normal lifetime merely because the `KRBTGT` password has not been rotated.



That conflates two different conditions:



\- A stolen, legitimately issued Ticket-Granting Ticket is constrained by its ticket lifetime and renewal policy.

\- A forged Golden Ticket is created using compromised `KRBTGT` key material and can be generated with attacker-selected attributes and lifetimes.



The default maximum user Ticket-Granting Ticket lifetime is commonly 10 hours, with a default maximum renewal period of seven days. The age of the `KRBTGT` password does not automatically extend an already issued legitimate ticket.



Replace the current explanation with a distinction between:



\- Ticket theft

\- Ticket renewal

\- Forged Ticket-Granting Tickets

\- `KRBTGT` key compromise

\- `KRBTGT` double reset during recovery



\---



\## 3.4 Remove the claim that `NTDS.dit` is a complete historical ledger



\*\*Location:\*\* Section 1.10.7, approximately lines 1995–1999



The manuscript states that `NTDS.dit` contains:



\- Every identity that has ever existed

\- Every credential that has ever been set

\- Every historical group membership

\- The full history of every delegation and permission assignment



It then states that DCSync or `NTDS.dit` extraction yields historical password hashes and historical group memberships.



This is materially inaccurate.



Active Directory maintains replication metadata, deleted-object states for defined retention periods, and configured password history. It does not preserve a permanent, complete historical ledger of every object state and every credential ever used. Deleted objects lose many attributes and linked values, are later recycled or garbage-collected, and password history is limited by policy.



Revise the section to describe `NTDS.dit` as the authoritative current directory database containing:



\- Current directory objects and attributes

\- Password-derived secrets and configured password history

\- Replication metadata

\- Deleted-object information subject to deletion lifecycle and retention

\- Security descriptors and other data retained according to schema and directory behavior



Do not claim that DCSync returns a complete historical record of the domain.



\---



\## 3.5 Correct the attack-lifecycle sequence



\*\*Locations:\*\*



\- Section 1.8.2, approximately lines 1739–1743

\- Section 1.8.3, approximately lines 1747–1751

\- Table 1-4, approximately lines 2493–2505



Stage 2 states:



> With initial access established, the adversary enumerates the directory...



Stage 3 is then:



> Initial Identity Acquisition



This sequence is internally impossible. Authenticated internal directory enumeration cannot depend on initial access when initial identity acquisition occurs in the next stage.



Use one of these structures:



\### Recommended sequence



1\. Passive Identity Reconnaissance

2\. Initial Identity Acquisition

3\. Active Internal Discovery and Enumeration

4\. Credential Acquisition

5\. Identity Authority Expansion

6\. Enterprise Identity Mobility

7\. Persistence and Domain Dominance



\### Alternative



Retain active enumeration as Stage 2 only if it is explicitly limited to unauthenticated or externally reachable enumeration, then introduce authenticated directory enumeration after initial credential acquisition.



The current table also forces identity stages into traditional Cyber Kill Chain stages such as Weaponization and Delivery even when the mapping is weak. Present the two models as an analytical comparison, not a strict one-to-one equivalence.



\---



\## 3.6 Harmonize domain and forest boundary terminology



\*\*Locations:\*\*



\- Section 1.1.2

\- Section 1.1.3

\- Section 1.2.1, “Domain and Forest Security Boundaries”

\- Table 1-2

\- Case Study 1-3



The chapter alternates among these positions:



\- The domain is a security boundary.

\- The forest is the Active Directory security boundary.

\- The identity trust system is the outer security boundary.



These statements are not equivalent.



Use the following terminology consistently:



\- A \*\*domain\*\* is an authentication, policy, administrative, and replication scope.

\- A \*\*forest\*\* is the primary Active Directory Domain Services security boundary.

\- A \*\*trust relationship\*\* connects otherwise distinct administrative or security domains under explicit conditions.

\- The \*\*identity trust system\*\* is the book's unit of analysis. It is not necessarily one formal security boundary. It contains multiple control planes, trust boundaries, issuers, relying parties, and governance authorities.



Rename Section 1.1.3 to avoid stating that the domain is an independent security boundary inside a forest. A better title is:



> WHY THE DOMAIN IS A REAL AUTHENTICATION AND ADMINISTRATIVE SCOPE, BUT NOT THE OUTERMOST TRUST BOUNDARY



\---



\## 3.7 Replace the uploaded versions of Sections 1.2.4 through 1.2.6



\*\*Location:\*\* Approximately lines 850–1027



The uploaded file still contains the earlier versions of:



\- The Inseparability of Directory and Privilege

\- Active Directory's Role in Hybrid Identity and Cloud Trust

\- Active Directory's Role in Mission-Partner and Cross-Boundary Access



These versions include claims already identified as inaccurate:



\- Privileged-access security and directory security are “the same entity.”

\- DCSync and Golden Tickets bypass authentication entirely.

\- Adversary access is undetectable and permanent.

\- Active Directory is the sole source of legitimate administrative privilege.

\- On-premises Active Directory is always the ultimate cloud trust anchor.

\- On-premises compromise automatically propagates into the cloud.

\- Domain dominance easily produces total control of all subscriptions.

\- Federal Public Key Infrastructure is anchored to on-premises directory infrastructure.

\- All mission-partner federation begins in Active Directory.



Replace these sections with the revised versions created during the preceding review. Do not attempt to preserve the old paragraphs through minor copyediting.



\---



\## 3.8 Correct the Protected Users guidance



\*\*Locations:\*\*



\- Section 1.5.6, approximately line 1459

\- Case Study 1-2, approximately line 2631



The manuscript says all Tier 0 accounts should be members of Protected Users and faults a Kerberoastable service account for having “no Protected Users.”



That is unsafe and incorrect as written.



Microsoft explicitly warns that:



\- Service accounts should not be members of Protected Users.

\- Computer accounts should not be members of Protected Users.

\- Highly privileged human accounts should be tested before broad membership changes because authentication restrictions can create lockout or operational failure.



Revise the guidance:



\- Consider Protected Users for compatible privileged \*\*human\*\* accounts after testing.

\- Use authentication policies and silos, account restrictions, dedicated administrative systems, and Kerberos-only designs where appropriate.

\- For services, prefer group Managed Service Accounts where supported, strong randomly generated secrets where not, least privilege, restricted logon scope, and monitored Service Principal Names.



Remove “no Protected Users” from the service-account deficiency in Case Study 1-2.



\---



\## 3.9 Correct the Office of Personnel Management case terminology and scope



\*\*Location:\*\* Section 1.4.1, approximately line 1215



Corrections required:



\- `SF-86` means \*\*Standard Form 86\*\*, Questionnaire for National Security Positions. It is not “Standard DoD Form 86.”

\- Distinguish the approximately 21.5 million background-investigation records from the separate approximately 4.2 million personnel-record incident.

\- Fingerprint data affected a subset of the background-investigation population, not necessarily all 21.5 million.

\- The compromised contractor credential account should be described carefully. Avoid implying that one credential alone explains the full intrusion chain unless the supporting source establishes that sequence.

\- “Including myself” is acceptable only if the author intentionally wants a first-person memoir element. Otherwise, move it into a clearly identified author note or attacker/defender journal.



\---



\## 3.10 Correct Resource-Based Constrained Delegation permission claims



\*\*Locations:\*\*



\- Section 1.4.3, approximately line 1243

\- Section 1.5.3.3, approximately line 1387

\- Section 1.5.3.5, approximately line 1407



The manuscript states that `AllExtendedRights` on a computer object permits Resource-Based Constrained Delegation configuration. That is not the correct general permission statement.



Resource-Based Constrained Delegation abuse normally depends on the ability to modify `msDS-AllowedToActOnBehalfOfOtherIdentity`, commonly through:



\- `GenericAll`

\- `GenericWrite`

\- Applicable `WriteProperty`

\- Ownership or `WriteDACL` used to grant the necessary write right



Similarly:



\- “Write access to a certificate template” is too vague. Exploitability depends on the exact template and certification authority permissions and configuration.

\- Shadow Credentials should identify write access to `msDS-KeyCredentialLink` and state applicable environmental prerequisites.



These rights should be described at attribute and object-control level, not through broad permission labels alone.



\---



\## 3.11 Remove categorical claims about valid credentials



\*\*Locations:\*\* Sections 1.4.1 and 1.4.4



Statements such as “they need only one valid credential” and “any credential gets the adversary through the door” are rhetorically effective but technically overbroad.



A credential may be:



\- Disabled

\- Expired

\- Restricted by logon conditions

\- Limited to an application

\- Denied network logon

\- Bound to a compliant device

\- Constrained by Conditional Access

\- Unable to reach the domain

\- Monitored and immediately blocked



Use:



> A usable credential for a reachable identity service can provide a lower-noise initial access path than exploitation and may expose additional identity relationships from which the adversary can expand authority.



This preserves the point without claiming universal success.



\---



\## 3.12 Remove categorical claims that zero-days are noisy



\*\*Location:\*\* Section 1.4.4



The current text says zero-day exploitation is noisy, messy, and likely to trigger Endpoint Detection and Response.



That is not reliably true. Some exploitation chains are noisy. Others are specifically designed for stealth and may not trigger existing detection.



Replace the contrast with:



> Identity abuse often has lower behavioral distinctiveness because the adversary uses valid protocols, credentials, sessions, and administrative interfaces. Exploitation and identity abuse can both be stealthy or noisy depending on the technique, implementation, telemetry, and defensive controls.



\---



\## 3.13 Correct the Kerberoasting and DCSync detection claims



\*\*Location:\*\* Section 1.4.5



Kerberoasting is not “plainly invisible” without one precisely tuned rule. Defenders can use:



\- Event ID 4769 characteristics

\- Encryption-type analysis

\- Request volume and service distribution

\- Account and host baselines

\- Decoy Service Principal Names

\- Directory reconnaissance telemetry

\- Endpoint and network signals

\- Correlation with logon and process activity



DCSync detection is not limited to source IP and requesting account. Detection may also include:



\- Directory replication rights and control access GUIDs

\- Replication requests from non-domain-controller hosts

\- Directory Replication Service Remote Protocol traffic

\- Named pipe and remote procedure call telemetry

\- Account role and behavior

\- Event ID 4662 when correctly audited

\- Changes granting replication rights



Rewrite the section as a discussion of \*\*low-distinctiveness behavior\*\*, not invisible behavior.



\---



\## 3.14 Correct the endpoint trust-decision statement



\*\*Location:\*\* Section 1.4.6



The manuscript says:



> The trust decisions that matter in Active Directory environments are not made on endpoints.



That is incorrect. Endpoints and applications make or enforce many consequential decisions, including:



\- Local authorization

\- Cached interactive logon

\- Token evaluation

\- Device compliance

\- Local group membership

\- Application session acceptance

\- Certificate validation

\- Credential storage and use

\- Enforcement of access-control policy



Use:



> Many enterprise identity assertions originate from domain controllers, certificate authorities, federation services, and cloud identity providers, while authorization and enforcement occur across endpoints, applications, services, and network resources.



\---



\## 3.15 Qualify Group Policy scope



\*\*Locations:\*\*



\- Section 1.10.6

\- Section 1.2.3

\- Table 1-1



The manuscript says Group Policy reaches every domain-joined system and that a domain-root enforced policy can configure every device simultaneously.



Group Policy scope depends on:



\- Site, domain, and Organizational Unit links

\- User and computer scope

\- Security filtering

\- Windows Management Instrumentation filters

\- Block inheritance and enforcement

\- Client-side extension support

\- Network and domain controller reachability

\- Successful policy processing

\- Loopback processing

\- Platform support



Use “can affect a broad population of in-scope domain-joined Windows users and computers” rather than “every system.”



\---



\## 3.16 Correct Federal Public Key Infrastructure and PIV/CAC relationships



\*\*Locations:\*\*



\- Section 1.1.1

\- Section 1.2.5

\- Section 1.3.7

\- Table 1-1



The manuscript repeatedly collapses four distinct concepts:



1\. Federal Public Key Infrastructure trust

2\. Personal Identity Verification credentials

3\. Common Access Card credentials

4\. Enterprise Active Directory Certificate Services



Required corrections:



\- Federal Public Key Infrastructure is not anchored to an agency's on-premises Active Directory.

\- Enterprise Active Directory Certificate Services does not generally issue federal Personal Identity Verification or Common Access Card credentials.

\- A federal certificate trust path is not always accurately described as routing directly to the Federal Common Policy Certificate Authority.

\- Personal Identity Verification and Common Access Card are related but not interchangeable.

\- Electronic Data Interchange Personal Identifier is a Department of Defense identifier and should not be presented as the universal credential-binding mechanism for all federal Personal Identity Verification credentials.

\- Certificate validation and certificate-to-account mapping are distinct operations.



Chapter 1 should establish these distinctions early because later Active Directory Certificate Services and federation chapters will depend on them.



\---



\## 3.17 Correct the Managed Service Account/cloud-role example



\*\*Location:\*\* Section 1.1.4



The statement that a Managed Service Account with excessive Microsoft Entra ID permissions can directly elevate in the cloud is unclear and likely misclassified.



Use the correct identity type:



\- A synchronized service account

\- A service principal

\- A managed identity

\- A workload identity

\- An application registration

\- An account operating the synchronization or federation service



Do not use “Managed Service Account” when the actual concern is cloud application or workload authority.



\---



\## 3.18 Correct the Active Directory Federation Services incident-response absolutes



\*\*Location:\*\* Case Study 1-3



The case study states that:



\- The token-signing certificate always must be rotated twice.

\- Every relying party must update trust metadata.

\- A Hardware Security Module is always required.



These may be appropriate controls or response steps in a specific architecture, but they are not universal statements.



The correct response depends on:



\- Whether automatic certificate rollover is enabled

\- Whether relying parties consume federation metadata automatically

\- Whether the old signing certificate remains trusted

\- Whether the service uses token-signing certificates stored in software or hardware

\- The incident-response procedure being followed

\- Partner notification and trust-revocation requirements

\- Whether the adversary obtained the private key, service control, or both



Write the case study as a defined scenario with stated architecture assumptions, or use conditional language.



\---



\# 4. Federal and Department of Defense Framing Corrections



\## 4.1 Correct framework names



\- “Cybersecurity Infrastructure Security Agency” must be

