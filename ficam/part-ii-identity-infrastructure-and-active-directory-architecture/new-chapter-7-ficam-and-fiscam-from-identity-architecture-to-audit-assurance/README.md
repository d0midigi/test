---
icon: rocket-launch
---

# NEW Chapter 7 - FICAM and FISCAM: From Identity Architecture to Audit Assurance

### Abstract

Chapter 7 introduces the slight variations and differences between Federal Identity, Credential, and Access Management (FICAM), which defines how federal identities, credentials, access, federation, and lifecycle governance should operate, and the Federal Information System Controls Audit Manual (FISCAM), which provides a methodology for determining whether supporting controls are properly designed, implemented, and operating effectively. This chapter connects those disciplines through an offensive and defensive identity-security lens. Rather than treating audit evidence as proof of security, readers learn to challenge the assumptions behind account provisioning, privileged access, separation of duties, authentication, recertification, logging, change management, and deprovisioning. Each control area is examined from the perspective of both the defender engineering the control and the adversary attempting to bypass, misuse, or remain invisible within it using various methods such as Living-Off-The-Land (LOTL), persistence, obfuscation, impersonation, and masquerading. Attack pathways, shadow administrators, stale or dormant identities, lax authentication, excessive privilege, evidence gaps, and control circumvention demonstrate how a technically compliant environment can remain exploitable. The chapter ultimately establishes adversarial control validation as the bridge between identity architecture, audit assurance, continuous monitoring, and defensible federal cybersecurity.

### 7.1 Two Frameworks, One Security Question

Federal identity architecture and federal information-system auditing begin from different professional perspectives. FICAM is concerned with how an agency establishes, manages, authenticates, authorizes, federates, governs, and retires identities and credentials. FISCAM approaches the same environment from the perspective of control assurance: whether information-system controls are appropriately designed, implemented, and operating with enough reliability to support the objectives for which they exist.

The distinction between the two matters.

FICAM should not be reduced to an audit checklist, and FISCAM should not be treated as an identity architecture framework. They both answer fundamentally different questions.

In an operational environment, those questions eventually collide.

An agency may design an identity lifecycle that requires authoritative sponsorship, identity proofing, controlled provisioning, strong authentication, appropriate authorization, periodic review, and timely deprovisioning. Those are intended identity outcomes. The existence of a policy describing those outcomes does not demonstrate that they occur consistently in production.

Likewise, an auditor may determine that access requests are approved, privileged accounts are periodically reviewed, terminated users are sampled for timely removal, and authentication settings are documented. That evidence may establish something meaningful about control operation. It still does not prove that an adversary cannot reach the same authority through a delegated Access Control Entry (ACE), a forgotten service account, a certificate, an unmanaged local administrator relationship, a surviving cloud token, or a system capable of controlling the administrator.

This is where the offensive and defensive perspectives become essential.

The attacker does not ask whether the identity program has a mature lifecycle diagram.

Rather, the attacker asks:

> _"Where is the trust assumption wrong?"_

The defender must learn to as that question **first.**

> #### Did You Know?
>
> FISCAM is not the document most cybersecurity practitioners think it is, because most of them are citing an edition that has been superseded twice.\
> \
> The 2009 manual, GAO-09-232G, organized general controls into five categories - security management, access controls, configuration management, segregation of duties, and contingency planning - and that taxonomy is what circulates in security training material, vendor mappings, and a great many System Security Plans (SSP).\
> \
> GAO issued a revision in September 2024, and a further revision, GAO-26-108633, that is effective beginning with fiscal year and calendar year 2026 audits of federal entity financial statements, and for attestation engagements and performance audits beginning on or after October 1, 2026. The current manual is organized by audit phase rather than control family:
>
> * Section 100 - Introduction
> * Section 200 - Planning
> * Section 300 - Testing
> * Section 400 - Reporting
> * Section 500 - Appendices containing the glossary and the FISCAM Framework.
>
> GAO publishes a crosswalk mapping the 2009 control activities to the current framework, which is the fastest way to translate legacy documentation. GAO also publishes a companion, the Cybersecurity Program Audit Guide (CPAG, GAO-23-104705), aimed at performance audits of cybersecurity programs rather than financial-statement work. For the adversarial validation this chapter describes, CPAG is often the closer fit.\
> \
> If your agency's control documentation still cites FISCAM chapter and control-activity identifiers from 2009, that is a currency finding waiting to be written, and it is worth resolving before an assessor writes it for you.

### 7.1.1 Federal Identity, Credential, and Access Management (FICAM)

Chapter 6 established FICAM as an identity architecture and governance discipline rather than a collection of account-management procedures. At this stage, the reader should already understand identity establishment, credentialing, authentication, authorization, federation, lifecycle management, Person Entity, Non-Person Entity (NPE), identity assurance levels, and access governance.

Chapter 7 does not aim to teach those concepts again.

Instead, FICAM becomes the source of security assertions that can be readily tested.

First, let us consider several examples:

* identities should originate from trustworthy authoritative sources;
* credentials should remain correctly bound to the identities to which they were issued;
* access should reflect legitimate mission need;
* privileged authority should remain appropriately constrained;
* federation should extend only the intended trust;
* credentials and access should be revoked when no longer authorized;
* Non-Person Entities (NPEs) should remain attributable to accountable owners; and,
* identity events should produce sufficient evidence for monitoring and investigation.

Each statement describes an intended condition.

The security problem begins when the intended condition and the technically effective condition diverge.

Suppose an agency's identity process correctly disables a departing employee's Active Directory user account within minutes of separation. From a FICAM lifecycle perspective, an important action occurred.

An attacker asks a different set of questions, however.

> _"Did the identity possess a still-valid authentication certificate?"_
>
> _"Were active cloud sessions and refresh tokens revoked, or only the account disabled?"_
>
> _"Did the user control an application registration, service principal, or workload identity?"_
>
> _"Were privileged group memberships nested through another identity?"_
>
> _"Did the person know a shared service credential?"_
>
> _"Did a local administrator password remain unchanged?"_
>
> _"Did the departing user own automation, scripts, keys, scheduled tasks, or service accounts that continue to operate?"_
>
> _"Was a second account created outside the primary provisioning process?"_
>
> _"Did the person hold a role in a system that does not consume the enterprise directory at all?"_

The attacker's purpose is not to argue that the account was not disabled. It was.

The attacker is testing whether account disablement accomplished the security objective everyone believes it accomplished.

That difference - between control activity and security outcome - is central to this chapter.

### 7.1.2 Federal Information System Controls Audit Manual (FISCAM)

FISCAM provides a disciplined means of examining information-system controls rather than relying on assertion alone. Its importance to this book is not that every identity engineer must become a security assessor. Its importance is that the security professionals benefit enormously from understanding how indpendent security assessors reason about control designs, implementation, evidence, effectiveness, deficiency, and reliance.

That mindset forces uncomfortable questions to arise.

> _What exactly is the control?_
>
> _Who performs it?_
>
> _What population does it affect?_
>
> _How frequently does it operate?_
>
> _What evidence does it produce?_
>
> _Can that evidence be independently corroborated?_
>
> _What happens when the control fails?_
>
> _Who is capable of overriding it?_
>
> _Can the same person both perform the sensitive action and manipulate the evidence demonstrating that the action was appropriate?_

Those are audit questions.

They are also excellent defensive questions as well.

However, inverted, they become excellent offensive questions.

If the security assessor asks:

> _"What evidence demonstrates that all privileged access is approved?"_

The offensive operator asks:

> _"Which privileged pathways are absent from the population used to generate that evidence?"_

If the security assessor asks:

> _"Are terminated accounts disabled within the required period?"_

The attacker asks:

> _"Which authentication artifacts remain userful after the account has been disabled?"_

If the security assessor asks:

> _"Are administrative changes logged?"_

The attacker, in turn, asks:

> _"Which administrative pathway lets me produce the desired state without generating the expected evidence?"_

The technical content changes very little. The perspective, however, changes everything.

Two FISCAM concepts deserve particular attention from security engineers, because both have direct offnesive relevance and neither is intuitive to practitioners who have not worked a security audit.

**Population completeness.** Before a control can be tested, the assessor must first establish what set of items the control is supposed to cover, and must have reason to believe that set is complete. If the population is derived from a query, the query is part of the control. A privileged-access review whose population comes from a script enumerating three named groups is testing membership in three named groups, and the assessor's conclusion can only extend that far. Everything outside the population is, from the audit's perspective, invisible - and from the adversary's perspecitve, available.

**Management override.** Internal control literature treats management override as the residual risk that survives well-designed controls, because the people who operate a control frequently possess the authority to circumvent it. In identity terms, the domain administrator who performs the quarterly access review can also modify the directory the review examines. Where the same authority can both act and shape the evidence of the act, the control's assurance value drops toward zero regardless of how faithfully it is executed.

Both concepts recur throughout this chapter, because both describe the very seam an adversary works.

### 7.1.3 Architecture and Control Assurance Are Different Disciplines

A secure Active Directory architecture can absolutely contain a failed control while everthing continues to operate normally.

A well-operated control can exist inside a weak architecture.

These conditions must not be confused or interchanged.

Suppose any agency implements an excellent quarterly review of Domain Admin membership. Every member has documented justification. Every reviewer signs on time. Every addition and removal traces to an approved request. The control may be operating exactly as designed.

Now suppose a server-management group outside Domain Admins holds `WriteDACL` over an Organizational Unit (OU) containing a privileged service account. That account ultimately controls a management platform that is capable of executing commands on domain controllers.

The Domain Admin review has not failed.

The architecture has exposed an alternate pathway to equivalent authority.

This distinction is critical because organizations sometimes respond to a security finding by strengthening a control that was never addressing the real attack pathway.

More frequent Domain Admin reviews would not remove the delegated `WriteDACL`.

A stronger approval form would not remove it.

An additional signature would not remove it.

The technical edge must be removed, constrained, monitored, or otherwise rendered unable to produce the unwanted authority.

Conversely, architecture can be sound while a control fails operationally.

An agency may have a carefully designed access model requiring managers to approve privileged access for only six months. If expiration dates are never enforced and nobody removes the resulting memberships, the architecture expresses the correct intent while the operational control fails to preserve it.

The defender therefore needs both views:

> _"What should be true?"_
>
> _"What is actually true?"_

The attacker cares almost exclusively about the second.

There is a third question that belongs to neither discipline alone, and it is the one this chapter is built around:

> _What can be made true by someone who is not authorized to make it true?_

### 7.1.4 FICAM Defines Identity Outcomes

For purposes of this chapter, FICAM provides the intended identity state against which technical reality can be examined.

The operative word is _**intended**._

If an identity should be unique, attributable, appropriately proofed, correctly credentialed, granted only necessary access, and removed when its mission relationship ends, each of those characteristics creates something that can be tested.

The defensive engineer can ask:

> _Can I prove the account originated from an authoritative workflow?_
>
> _Can I trace sponsorship?_
>
> _Can I determine every credential currently representing this identity?_
>
> _Can I calculate its effective authority, including indirect paths?_
>
> _Can I identify every system on which that identity has authenticated?_
>
> _Can I determine who can modify the identity?_
>
> _Can I determine who can replace its credential?_
>
> _Can I determine which applications and services continue trusting it?_

Those questions transform identity governance from administrative process into observable security state.

The offensive operator asks nearly identical questions for a different purpose.

> _Which identity lacks a reliable owner?_
>
> _Which account was provisioned outside the normal workflow?_
>
> _Which entitlement survived a role change?_
>
> _Which credential can still represent a disabled identity?_
>
> _Which administrator can be controlled indirectly?_
>
> _Which service account has authority disproportionate to its visibility?_
>
> _Which federation path accepts a weaker assertion than the architecture assumes?_

The defender and attacker are interrogating the same identity environment.

They disagree on what should happen next.

### 7.1.5 FISCAM Tests Whether Supporting Controls Can Be Relied Upon

Control assurance introduces another distinction: a control can exist without being reliable.

A policy requiring account recertification exists.

A script that generates the account-review population exists.

A manager receives the report.

The manager signs it.

The report is archived.

Every visible step can occur exactly as expected.

Now suppose the population-generation script ignores nested group membership.

The control operated.

The evidence exists.

The reviewer completed the task.

The resulting conclusion is wrong.

This is precisely the condition adversarial thinking should expose.

From the attacker's perspective, the interesting question is not whether the review happened. It is whether the review's method creates a blind spot in which useful authority can survive.

From the defender's perspective, control reliability requires more than procedural completion. The defender must understand the technical mechanism generating the evidence and determine whether that mechanism adequately represents the security condition being asserted.

If the control claims to identify privileged users, its population-generation logic must identify privilege.

If it identifies only membership in a small set of named administrative groups, the control is testing group membership - not privilege.

Those are different things.

The gap between them is where shadow administrators live, and §7.4 is devoted to it.

### 7.1.6 Neither Framework Alone Proves the Environment Is Secure

No framework eliminates the need for technical judgment.

FICAM can describe a mature identity architecture without proving that every implementation detail is correct.

FISCAM can provide rigorous audit methodology without guaranteeing that every exploitable relationship appears inside the selected scope, population, evidence source, or control objective.

This does not diminish either framework. It defines the boundary of what each is intended to accomplish.

Security engineering fails when those boundaries are ignored.

A control can pass and an attack path can remain.

An architecture can conform to the intended model while one delegated permission violates its security assumptions.

An audit can correctly sample a population while the attacker's target exists outside that sample.

A configuration can satisfy the stated requirement while a second protocol bypasses it.

An access review can accurately describe every account it examined while failing to recognize an administrator hidden behind indirect control.

For this reason the book adds a third perspective:

adversarial validation.

The purpose is not to replace FICAM or FISCAM.

The purpose is to apply hostile technical reasoning to the assumptions they expose.

### 7.1.7 The Adversary Tests What the Documentation Assumes

Attackers benefit from differences between documented architecture and operational reality.

That difference may be small.

One account.

One Access Control Entry (ACE).

One certificate.

One service password.

One authentication exception.

One unmanaged endpoint.

One forgotten trust.

One backup administrator.

One application that still accepts NTLM.

One recovery process that can reset a privileged identity without equivalent assurance.

The adversary does not need the entire identity architecture to be defective.

Only one usable path must be defective.

This creates an asymmetry between administrative assurance and offensive operations.

An agency may need evidence that thousands of identities are governed correctly.

An attacker may need only one overlooked identity.

An auditor may reasonably sample a population.

An attacker deliberately searches outside the sample.

A defender may demonstrate that ninety-nine percent of privileged authentication uses phishing-resistant mechanisms.

The attacker asks what the remaining one percent can reach.

The asymmetry is worth stating precisely, because it explains why compliance metrics and security outcomes diverge. Audit assurance is a statement about a population. Exploitation is a statement about an element. A ninety-nine percent result is excellent evidence of program maturity and says nothing at all about whether the remaining element grants Tier 0.

This does not mean sampling, metrics, or compliance evidence are useless. It means defenders must understand what those mechanisms do not prove.

Adversarial thinking is the discipline of searching deliberately for the remainder.

### 7.1.8 The Defender Must Test the Same Assumptions First

The defender's advantage is authorization.

A mature defensive identity program does not wait for an adversary to discover that a control assumption is false. It attacks its own assumptions deliberately, safely, and repeatedly.

That requires a shift in mentality.

Instead of asking:

> Did the control execute?

Ask:

> Can I circumvent the outcome?

Instead of:

> Was the account reviewed?

Ask:

> Can the account reach authority the reviewer never saw?

Instead of:

> Is MFA enabled?

Ask:

> Can the identity authenticate to the same resource through a mechanism that does not invoke MFA?

Instead of:

> Was the terminated account disabled?

Ask:

> Can anything still authenticate as, impersonate, or act with authority derived from that identity?

Instead of:

> Are Domain Admins tightly controlled?

Ask:

> Who can become functionally equivalent to Domain Admin without joining the group?

Instead of:

> Are security events being collected?

Ask:

> What privileged activity could occur without producing the telemetry our detection logic expects?

This is where offensive and defensive identity security converge.

The attacker's mindset supplies the challenge.

The defender's access to architecture, telemetry, administrative authority, and approved testing supplies the opportunity to answer it before the challenge becomes an incident.

The remainder of this chapter treats control assurance adversarially. FICAM provides the intended trust model. FISCAM provides disciplined methods for evaluating the controls supporting that model. Offensive analysis attempts to falsify their assumptions. Defensive engineering uses the results to strengthen the architecture, evidence, telemetry, and control itself.

### That combined process is adversarial identity assurance.

### 7.2 From FICAM Requirement to FISCAM Testable Assertion

An identity requirement becomes operationally useful only when it can be translated into a condition that can be observed and tested.

This translation is where architecture, auditing, offense, and defense meet.

For the remainder of the chapter we will repeatedly use the following chain:

**Identity Requirement → Control Objective → Technical Implementation → Expected Evidence → Audit Test → Adversarial Challenge → Defensive Validation**

```
  FICAM                    FISCAM                   ADVERSARIAL
  (intent)                 (assurance)              (falsification)
     │                        │                          │
     ▼                        ▼                          ▼
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│ Identity │→ │ Control  │→ │Technical │→ │ Expected │→ │  Audit   │→ │Adversary │
│Requirement│  │Objective │  │  Impl.   │  │ Evidence │  │   Test   │  │Challenge │
└──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘  └────┬─────┘
      ▲                                                                     │
      │                        ┌──────────────────┐                         │
      └────────────────────────│    Defensive     │←────────────────────────┘
         feeds back into        │   Validation     │   findings
         the requirement        └──────────────────┘
```

Consider a simple example.

**Identity requirement:** privileged access must be limited to authorized personnel.

That statement is not yet technically testable.

A control objective refines it:

**Control objective:** only personnel with current approval and mission need may possess privileged administrative authority.

Implementation may include privileged groups, role assignments, access workflows, Authentication Policy Silos, Privileged Identity Management, Group Policy, endpoint restrictions, and delegated directory permissions.

Evidence may include approval records, group membership, directory ACLs, activation history, authentication telemetry, and administrative logs.

An auditor can test whether selected privileged assignments were approved and remained appropriate.

The attacker then asks a different question:

_"Can I obtain equivalent authority without appearing in the population being reviewed"?_

The defender completes the process: enumerate effective authority, graph indirect control paths, identify shadow administrators, compare technical state to approvals, and verify that removal of inappropriate access actually severs the path.

That final step converts control evidence into stronger security assurance.

The subsections that follow work each link in the chain.

### **7.2.1 Identity Requirement**

An identity requirement expresses what the agency intends to be true about identities, credentials, and access. It originates in policy, architecture, statute, or directive - HSPD-12, FIPS 201-3, OMB M-19-17, OMB M-22-09, agency identity policy, or the FICAM architecture itself.

Requirements are written in the language of intent, and intent is not testable.

_"Access shall be granted based on least privilege"_ is a requirement.

It cannot be tested, because nothing in the sentence identifies what would count as a violation. Least privilege relative to what baseline? Measured how? Evaluated by whom? Across which authority paths?

The first analytical task is therefore to determine what the requirement is actually asserting about the environment. A useful technique is to force the requirement into a falsifiable form by asking what observation would prove it false.

| Requirement as written                            | Falsifiable form                                                                                                            |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Access shall follow least prvileged               | No identity holds an entitlement not traceable to a current, approved mission need                                          |
| Credentials shall be bound to verified identities | Every credential in the environment maps to an identity that completed proofing at the required assurance level             |
| Privileged access shall be limited                | No identity can reach administrative authority over a Tier 0 system without appearing in the approved privileged population |
| Access shall be removed upon separation           | No authentication artifact associated with a separated identity can produce a successful authorization decision             |
| Identity events shall be auditable                | Every change to an identity's effective authority produces evidence attributable to an accountable actor                    |

The right-hand column is where security engineering begins. Each statement is now something an operator can attempt to disprove.

Note that the falsifiable forms are deliberately absolute. Real environments will not satisfy them completely, and that is the point: the exceptions are the findings.

### 7.2.2 Control Objective

A control objective narrows the requirement to a specific condition that a control is meant to preserve. It answers the question, _"What must reliably occur for this requirement to hold?"_

The translation is not mechanical, and this is where most identity programs lose fidelity. A single requirement usually decomposes into several objectives, and objectives that go unwritten become gaps that no control covers.

Take the requirement that access be removed upon separation. Reasonable objectives include:

* the separation event is detected and communicated to the identity system within a defined period;
* the primary directory account is disabled;
* credentials bound to the identity are revoked, not merely deactivated;
* active sessions and refresh tokens are terminated;
* entitlements held in systems that do not consume the enterprise directory are removed;
* shared or service credentials known to the separated person are rotated; and
* resources owned by the identity are reassigned to an accountable owner.

Most agencies write the second objective and assume the rest.

An assessor testing only the second objective can issue a clean result while five of the seven remain unaddressed. The adversary works the five.

The defensive discipline here is decomposition. For every identity requirement, enumerate the objectives that must all hold, and identify which have an owner, a control, and evidence. Objectives with none of the three are the chapter's recurring subject.

### 7.2.3 Technical Implementation

Implementation is the mechanism that enforces the objective in the actual environment. It is also where the objective's meaning quietly changes.

Consider the objective that only approved personnel may hold privileged authority. Implementations might include:

* membership in named privileged groups;
* role assignments in a privileged identity management platform;
* delegated permissions on directory objects;
* local administrator group membership on servers;
* application-level administrative roles;
* cloud directory roles and administrative units;
* Authentication Policy Silo membership;
* Group Policy user rights assignments; and
* service account permissions and constrained delegation.

Every one of those is a legitimate implementation of privilege. Only the first two are typically enumerated when someone is asked to produce "the list of privileged users."

Three implementation questions carry disproportionate security weight:

**Does the implementation enforce the objective, or does it record it?** A ticket recording approval does not restrict anything. A group membership does. Confusing recording controls with enforcing controls produces documentation that describes an environment nobody is actually constrained by.

**Is the implementation the only path to the outcome?** If administrative authority can be reached through directory delegation, a management platform, or a backup system, then restricting group membership constrains one path of three.

**Can the implementation be modified by the population it governs?** If privileged users can alter the mechanism restricting privileged users, the control is advisory.

That last question is management override expressed technically, and it is the single most productive question to ask about any identity control.

### 7.2.4 Expected Evidence

Evidence is what the control produces to demonstrate that it operated. It is not the same as the security state, and the difference is the source of an entire class of finding.

Evidence has properties that determine how much weight it can bear:

| Property        | Question                                                           | Failure mode                                              |
| --------------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| Completeness    | Does the evidence cover the whole population?                      | Blind spot outside the query                              |
| Accuracy        | Does it reflect the actual technical state?                        | Report generated from stale or cached data                |
| Timeliness      | Does it describe the period under review?                          | Point-in-time snapshot missing interim changes            |
| Attributability | Can each action be tied to an accountable actor?                   | Shared or service account performed the change            |
| Integrity       | Could the subject of the evidence alter it?                        | Log source controlled by the administrator being reviewed |
| Independence    | Was it generated by something outside the control's own operation? | Administrator attests to their own access                 |

The properties compound. A privileged-access report that is complete, accurate, and timely but generated by a script the privileged users can edit fails on integrity, and the other three properties do not compensate.

Evidence integrity deserves particular emphasis in identity work because the subject of the evidence is frequently the person with authority over the evidence source. A domain administrator can clear a security log, modify audit policy, alter a scheduled report, or change the group whose membership the report enumerates. Evidence produced inside the of the authority control plane describes it describes is evidence of limited assurance value, and the fix is architectural rather than procedural: the collection path must terminate somewhere the reviewed population cannot reach.

### 7.2.5 Audit Procedure

The audit procedure is the assessor's method for determining whether the control operated effectively. Typical procedures include inquiry, observation, inspection of documentation, reperformance, and analysis of system-generated data.

Security engineers should understand three characteristics of audit procedures, because each creates a predictable seam.

**Sampling.** Where populations are large, assessors test a sample rather than every item. A well-designed sample supports a conclusion about the population. It does not, and is not intended to, guarantee that every unsampled item is compliant. An adversary who needs exactly one non-compliant item is not constrained by the sample's statistical validity.

**Point-in-time testing.** Many procedures examine state at a moment, or transactions over a defined period. Conditions that exist between test dates, or that are created and removed within a period, may never appear. Privilege that is added Friday and removed Monday satisfies a quarterly review and is entirely sufficient for an adversary.

**Reliance on system-generated information.** When an assessor uses a report from a system, the reliability of that report becomes part of the test. Under FISCAM the assessor is expected to consider whether the data is complete and accurate, which means examining how the report is produced. Security teams should read this as a standing invitation: if you cannot explain how your privileged-user report is generated, neither can the assessor rely on it, nor can you.

The offensive reading of an audit program is straightforward. Every procedure defines a scope, a population, a period, and a source. Everything outside those four is unexamined by construction.

### 7.2.6 Adversarial Challenge

The adversarial challenge attempts to falsify the control's assertion using the environment as it actually exists.

This is not penetration testing in the general sense. It is targeted at a specific claim. The claim is written down, and the challenge either falsifies it or does not.

A structured challenge has four parts:

1. **The assertion.** State exactly what the control claims. Only members of the approved privileged population hold administrative authority over domain controllers.
2. **The falsification hypothesis.** State how the assertion might be false. An identity outside that population can obtain equivalent authority through delegated directory permissions, a management platform, or a backup service account.
3. **The test.** Enumerate effective authority using the same techniques an adversary would, within an authorized scope and rules of engagement.
4. **The result.** Either the assertion held under the test, or it did not, with the specific path documented.

The discipline is in step 1. A challenge against a vaguely stated control produces a vaguely useful finding. A challenge against a precisely stated assertion produces a finding that names the path, the authority it confers, and the control it defeats.

Rules of engagement matter here in a way they do not in ordinary research. Identity infrastructure is the system on which incident response itself depends, and a validation exercise that disrupts authentication has produced an outage rather than an assurance. Authorization, scope boundaries, deconfliction with the operations team, and a documented rollback for any change made during testing are prerequisites, not formalities.

{% hint style="warning" %}
#### Warning - Please Read Before Executing Anything in This Chapter

The offensive validation sections that follow contain the commands a real-world cyber adversary would use, because a chapter that describes attacks without demonstrating them teaches recognition rather than capability. They are written for autrhorized assessment of systems you are responsible for.\
\
Before running any of it: obtain written authorization naming the exact systems with the operations team, and agree on what happens if something breaks. Identity infrastructure is the system incident response itself depends on, so a validation exercise that disrupts authentication has produced an outage ratherthan an assurance.\
\
Several techniques below write to the directory - a permission grant, a key credential, a certificate request. Every write needs a documented rollback recorded before it is made, and then verified after the exercise. An assessment that leaves behind the access it created has effectively manufactured the finding it reported.\
\
On a feederal information system, unauthorized execution of this material is a violation of the Computer Fraud and Abuse Act (CFAA) and of the terms under which you hold your access.\
\
Get the authorization in writing, and signed by ALCON (all parties concerned).
{% endhint %}

### 7.2.7 Defensive Validation

Defensive validation converts an adversarial finding into a durable change in the environment, and then proves the change worked.

The sequence has four steps, and skipping the fourth is the most common failure in federal remediation.

1. **Establish the technical fact.** Not _"the access review may be incomplete,"_ but _"the review population excludes 14 identities holding `GenericAll` on the Tier 0 OU through nested group membership."_
2. **Remove or constrain the path.** Modify the permission, restructure the group, restrict the platform, or bring the authority under the same governance as the population it parallels.
3. **Correct the control that missed it.** If the review's population logic could not see the path, fixing the individual permission leaves the logic still blind. The next fourteen will be equally invisible. This step is what distinguishes remediation from cleanup.
4. **Verify the path is actually gone.** Re-run the enumeration. Confirm the authority no longer resolves. Retain the before-and-after as evidence.

That last step is also what makes the finding defensible to an assessor, an Inspector General (IG), or an Authorizing Official (AO). A closed Plan of Action and Milestones (POA\&M) item supported by a re-run enumeration showing the path removed is materially stronger evidence than a memorandum asserting that remediation occurred.

### 7.2.8 Residual Risk After the Control Passes

A control that operates effectively still leaves residual risk, and naming it honestly is a professional obligation rather than a weakness in the program.

Residual risk in identity controls comes from several recurring sources:

* **Population boundaries.** The control governs what it enumerates. Authority outside the enumeration is ungoverned by construction.
* **Testing intervals.** Between tests, state changes. A quarterly control leaves a quarterly window.
* **Management override.** The authority that operates the control can generally circumvent it.
* **Dependency inheritance.** A control is only as reliable as the systems that administer the systems it protects, which is the clean source problem developed in §4.6 and applied here to control assurance.
* **Evidence integrity.** Where the reviewed population can influence the evidence, the residual risk is the difference between what occurred and what was recorded.
* **Compensating-control drift.** Controls accepted as compensating for a deficiency degrade quietly, because nothing tests a compensating control the way the original control is tested.

The correct treatment is not to eliminate residual risk, which is not possible, but to state it in terms specific enough that an authorizing official can make an informed decision.

Compare two statements of the same condition:

{% hint style="info" %}
**Privileged access is managed in accordance with agency policy. Residual risk is low.**\
\
The quarterly privileged access review enumerates membership in five named groups. It does not enumerate delegated directory permissions, local administrator membership on Tier 0 hosts, or administrative roles in the endpoint management platform. Effective authority reachable outside the reviewed population was measured at 22 identities as of the last enumeration, of which 9 have no current approval record. Residual risk is the authority held by those 9 identities between enumerations.
{% endhint %}

***

**The first is unassessable. The second is a decision an authorizing official can actually make, and it converts an audit result into a risk statement - which is the entire purpose of the chain this section describes.**

***

### 7.3 Account Provisioning and Identity Establishment

Provisioning is where an identity enters the environment, and therefore where every later control inherits its assumptions. If the provisioning process is the authoritative path, then the population of identities is knowable. If it is one of several paths, the population is an estimate.

**The FICAM assertion:** identities originate from authoritative sources, are proofed at the required assurance level, are uniquely attributable to a person or accountable owner, and receive access reflecting legitimate mission need.

**The control objective:** no identity exists in the environment that did not originate from an approved provisioning workflow with a traceable sponsor.

**Typical implementation:** an identity management platform provisions accounts from an authoritative human-resources or personnel-security feed, applies a naming standard, assigns birthright access by role, and records the request, approval, and sponsor.

**Typical evidence:** provisioning tickets, workflow approval records, account creation timestamps, and a reconciliation report comparing directory accounts to the authoritative source.

### 7.3.1 The Adversarial Challenge to Provisioning

The assertion to falsify is that every identity came from the workflow.

Accounts that exist outside an authoritative provisioning path are common in mature federal environments, and they are rarely malicious in origin. They accumulate:

* accounts created directly in the directory during an outage, a migration, or a deployment, and never reconciled;
* service accounts created by application teams under local delegation;
* test, training, and demonstration accounts from projects that ended;
* accounts created by a management platform or application on its own behalf;
* accounts migrated from an acquired or consolidated environment whose provisioning history did not migrate with them;
* contractor accounts provisioned through a separate workflow with different rigor; and
* break-glass and emergency accounts, which by design bypass the workflow.

Each represents an identity whose sponsor, purpose, and approval may be unrecoverable. An adversary looking for a durable foothold prefers exactly this population, because an account with no accountable owner generates no inquiry when it authenticates.

Two provisioning-adjacent weaknesses deserve specific attention.

**Attribute-driven authority.** Where birthright access is derived from attributes - department, job code, location, `extensionAttribute` values - the ability to write those attributes is the ability to grant access without touching a group. A service desk delegated to update user attributes may hold, unintentionally, the authority to move an identity into a privileged role.

**Account creation as a privilege.** The right to create accounts in an OU where privileged groups apply birthright access is functionally the right to create privileged identities. This is enumerable and rarely enumerated.

### **7.3.X Offensive Validation for Provisioning Outside the Workflow**

The assertion is that every identity originated from an approved workflow. Falsifying it means creating one that did not, using delegation the environment already grants.

```powershell
# Enumerate where the current principal can create objects. PowerView, from an
# authorized assessment host. Any OU returned is an identity-creation path.
Import-Module .\PowerView.ps1
Find-InterestingDomainAcl -ResolveGUIDs |
  Where-Object { $_.ActiveDirectoryRights -match 'CreateChild|GenericAll' } |
  Where-Object { $_.IdentityReferenceName -eq $env:USERNAME } |
  Select-Object ObjectDN, ActiveDirectoryRights, IdentityReferenceName

# Same question from Linux, unauthenticated tooling not required — this is a
# normal LDAP read available to any domain user.
ldapsearch -x -H ldap://dc01.agency.local -D 'AGENCY\svc-inventory' -w '<pw>' \
  -b 'DC=agency,DC=local' '(objectClass=organizationalUnit)' nTSecurityDescriptor

# Create the identity through the delegated path. Built-in binary, no tooling.
net user assessment.svc '<complex-pw>' /add /domain

# Or via the directory module, placing it in an OU with birthright group linkage
New-ADUser -Name 'assessment.svc' -SamAccountName 'assessment.svc' `
  -Path 'OU=Service Accounts,DC=agency,DC=local' `
  -AccountPassword (Read-Host -AsSecureString) -Enabled $true `
  -Description 'Inventory sync - AUTHORIZED ASSESSMENT, remove by <date>'
```

The finding is not that an account was created. It is that the account exists with no sponsor, no approval record, and no reconciliation expiration - and that it received access from OU placement without any workflow evaluating whether it should have.

***

_**ATT\&CK: T1136.002 (Create Account: Domain Account), T1078.002 (Valid Accounts: Domain Accounts).**_

***

### 7.3.2 Defensive Validation for Provisioning

The validating question is not _"are accounts approved"_ but _"can I account for every identity in the directory."_

```powershell
# Identities with no recorded sponsor, manager, or description — candidates for
# accounts that entered the environment outside the provisioning workflow.
# Adjust the attribute names to your agency's provisioning schema.
Get-ADUser -Filter * -Properties whenCreated, manager, description, employeeID,
        extensionAttribute1, lastLogonTimestamp, servicePrincipalName, enabled |
  Where-Object {
      -not $_.manager -and -not $_.employeeID -and $_.enabled
  } |
  Select-Object SamAccountName, whenCreated, description,
        @{n='LastLogon';e={[datetime]::FromFileTime($_.lastLogonTimestamp)}},
        @{n='IsServiceAccount';e={[bool]$_.servicePrincipalName}} |
  Sort-Object whenCreated

# Who can create user objects in each OU? Account creation in a privileged OU
# is the authority to create privileged identities.
Get-ADOrganizationalUnit -Filter * | ForEach-Object {
    $ou = $_.DistinguishedName
    (Get-Acl "AD:\$ou").Access |
      Where-Object {
          $_.ActiveDirectoryRights -match 'CreateChild|GenericAll' -and
          $_.IdentityReference -notmatch 'SYSTEM|Domain Admins|Enterprise Admins|BUILTIN\\Administrators'
      } |
      Select-Object @{n='OU';e={$ou}}, IdentityReference, ActiveDirectoryRights
}
```

Reconciliation is the control that makes provisioning assertable. It compares three populations - the authoritative personnel source, the identity management platform's record, and the directory's actual contents - and treats every discrepancy as a finding requiring disposition. An environment that cannot produce that three-way reconciliation cannot claim a knowable identity population, whatever its provisioning workflow looks like on paper.

{% hint style="warning" %}
#### **Warning - Reconciliation Without Disposition Is Theater**

Many agencies generate an exception report and file it. The report is evidence that the control ran. It is not evidence that the exceptions were resolved, and an assessor who traces a sample of exceptions to their disposition will find this quickly. Every unreconciled identity must reach one of three states: matched to an authoritative record, assigned an accountable owner with documented justification, or removed. A fourth state - appearing on the report every quarter for three years - is a finding about the control, not about the account.
{% endhint %}

### 7.4 Privileged Access and Shadow Administrators

This is the control area where the gap between audit population and effective authority is widest, and where adversarial validation delivers the most value per hour spent.

**The FICAM assertion:** privileged authority is constrained to approved personnel with current mission need.

**The control objective:** no identity holds administrative authority over a Tier 0 system without appearing in the approved privileged population.

**Typical implementation:** membership in named privileged groups, role activation through a privileged identity management platform, and periodic review.

**Typical evidence:** group membership exports, activation logs, and signed review records.

### 7.4.1 Privilege Is Not Group Membership

The control objective refers to administrative authority. The implementation and the evidence both refer to group membership. Those are different populations, and the difference is the attack surface.

An identity can reach administrative authority over a domain controller through any of the following without ever appearing in a privileged group:

| Path                      | Mechanism                                                                                                 | Appears in a group export? |
| ------------------------- | --------------------------------------------------------------------------------------------------------- | -------------------------- |
| Directory permissions     | `GenericAll`, `GenericWrite`, `WriteDACL`, `WriteOwner`, `AllExtendedRights` on a privileged object or OU | No                         |
| Group management          | `WriteProperty` on a privileged group's `member` attribute                                                | No                         |
| Password reset            | `User-Force-Change-Password` extended right on a privileged account                                       | No                         |
| GPO modification          | Edit rights on a GPO linked to the domain controllers OU                                                  | No                         |
| Computer object control   | Write access to `msDS-AllowedToActOnBehalfOfOtherIdentity` on a DC                                        | No                         |
| Delegation abuse          | Unconstrained or configured constrained delegation to a Tier 0 service                                    | No                         |
| Certificate services      | Enrollment rights on a template permitting client authentication with a supplied subject                  | No                         |
| Local administrator       | Membership in the local Administrators group on a Tier 0 host                                             | No                         |
| Management platform       | Administrative role in a deployment, backup, virtualization, or scanning platform                         | No                         |
| Service account ownership | Control of an account holding replication or administrative rights                                        | No                         |
| Nested indirection        | Membership in a group nested several levels beneath a privileged group                                    | Sometimes                  |

Every row is a path to equivalent authority. Only the last is even partially visible to the control as most agencies implement it.

A **shadow administrator** is an identity holding one of these paths without appearing in the privileged population. The term matters because it names a specific finding: not "excessive privilege" in the abstract, but an identity whose effective authority exceeds its governed authority.

### 7.4.2 The Adversarial Challenge to Privileged Access

The challenge is to reach Tier 0 authority using an identity that the privileged access review would not have examined.

```powershell
# Non-default principals holding control-class rights over privileged objects.
# Any result is an identity whose effective authority may exceed its governed authority.
$targets = @(
    (Get-ADDomain).DomainControllersContainer,
    (Get-ADGroup 'Domain Admins').DistinguishedName,
    (Get-ADGroup 'Enterprise Admins').DistinguishedName,
    (Get-ADUser -Filter 'SamAccountName -eq "krbtgt"').DistinguishedName
)

foreach ($dn in $targets) {
    (Get-Acl "AD:\$dn").Access |
      Where-Object {
          $_.ActiveDirectoryRights -match 'GenericAll|GenericWrite|WriteDacl|WriteOwner|WriteProperty|ExtendedRight' -and
          $_.IdentityReference -notmatch 'NT AUTHORITY\\SYSTEM|BUILTIN\\Administrators|Domain Admins|Enterprise Admins|Account Operators'
      } |
      Select-Object @{n='Object';e={$dn}}, IdentityReference,
                    ActiveDirectoryRights, ObjectType, IsInherited
}

# Resource-based constrained delegation configured against Tier 0 computers
Get-ADComputer -Filter * -Properties msDS-AllowedToActOnBehalfOfOtherIdentity |
  Where-Object { $_.'msDS-AllowedToActOnBehalfOfOtherIdentity' } |
  Select-Object Name, DistinguishedName

# Accounts holding directory replication rights outside expected principals —
# the permission pair that enables directory synchronization abuse
$rootDN = (Get-ADDomain).DistinguishedName
(Get-Acl "AD:\$rootDN").Access |
  Where-Object { $_.ObjectType -in @(
        '1131f6aa-9c07-11d1-f79f-00c04fc2dcd2',   # DS-Replication-Get-Changes
        '1131f6ad-9c07-11d1-f79f-00c04fc2dcd2'    # DS-Replication-Get-Changes-All
  )} |
  Select-Object IdentityReference, ObjectType
```

Graph tooling completes the picture that object-by-object enumeration cannot.&#x20;

Offensive validation: - reaching Tier 0 from outside the reviewed population.

The defensive enumeration above finds permissions. The adversary's question is whether those permissions chain into domain compromise. Path-finding answers it directly.

```cypher
// BloodHound — identities with a control path to Domain Admins that are NOT
// members of any group the privileged access review enumerates.
MATCH (n)-[:MemberOf*0..]->(g:Group)
WHERE g.name IN ['DOMAIN ADMINS@AGENCY.LOCAL','ENTERPRISE ADMINS@AGENCY.LOCAL',
                 'SCHEMA ADMINS@AGENCY.LOCAL','SERVER OPERATORS@AGENCY.LOCAL',
                 'BACKUP OPERATORS@AGENCY.LOCAL']
WITH collect(DISTINCT n) AS reviewed
MATCH p = shortestPath((s)-[*1..]->(t:Group {name:'DOMAIN ADMINS@AGENCY.LOCAL'}))
WHERE NOT s IN reviewed AND s:User
RETURN s.name AS shadow_admin, length(p) AS hops
ORDER BY hops ASC

// Every row is an identity the quarterly review never examined that can
// nonetheless become Domain Admin. This query IS the finding.
```

```powershell
# Collection, from an authorized assessment host
.\SharpHound.exe -c All --zipfilename agency-assessment.zip

# Confirm a specific WriteDACL path is exploitable rather than theoretical.
# Step 1: grant DCSync rights to a controlled principal using the delegated write.
Import-Module .\PowerView.ps1
Add-DomainObjectAcl -TargetIdentity 'DC=agency,DC=local' `
  -PrincipalIdentity 'assessment.svc' -Rights DCSync

# Step 2: demonstrate the authority actually resolves. Impacket, remote, no
# code executed on the domain controller.
secretsdump.py 'AGENCY/assessment.svc:<pw>@dc01.agency.local' -just-dc-user krbtgt

# Step 3: ROLLBACK — remove the ACE. Record before and after.
Remove-DomainObjectAcl -TargetIdentity 'DC=agency,DC=local' `
  -PrincipalIdentity 'assessment.svc' -Rights DCSync
```

Step 2 is what converts an Access Control List (ACL) listing into a finding an authorizing official cannot argue with. A permission is debatable. A `krbtgt` hash retrieved by an account that appeared in no privileged population is not.

***

_**MITRE ATT\&CK Adversarial Tactics, Techniques, and Procedures (TTP)**_

* _**T1098 - Account Manipulation**_
  * _**What it is:** a defense evasion and persistence technique where attackers maliciously modify account credentials, permissions, or configurations to maintain persistent long-term acce ss to a domain network. Instead of provisioning an account from scratch - which might trigger security alarms - attackers may quietly edit existing accounts. This allows them to stay inside the domain network even when their initial entry point is discovered and blocked._
  * _**Parent technique(s):** Account Manipulation (T1098)_
  * _**Target platform(s):** Windows, Linux, macOS, AWS, Azure, GCP, Office 365_
  * _**Primary tactic(s):** Persistence, Defense Evasion_
    * _**Offensive TTPs:**_
      * _**Password resets:** attackers may change the password of an existing, inactive, or administrator account so they can log back in whenever they please._
      * _**Elevating privileges:** they may add compromised accounts to high-privileged groups like Domain Admins in Windows or global admin roles in cloud environments._
* _**T1003.006 - OS Credential Dumping: DCSync**_
  * _**What it is:** a credential dumping subtechnique where attackers target the DCSync feature of Windows networks to steal or harvest password data. Instead of attacking a machine directly, attackers may use a legitimate network protocol to request password data from a domain ctonroller. Because the domain controller believes the request is coming from another legitimate server trying to sync domain data, it willingly hands over password hashes._
  * _**Parent technique(s):** OS Credential Dumping (T1003)_
  * _**Target platform(s):** Windows_
  * _**Primary tactic(s):** Credential Access_
    * _**Offensive TTPs:**_
      * _**Replication requests: a**ttackers may use tools like `mimikatz` to impersonate a domai comtroller and request accout data via the Directory Replication Service Remote Protocol (MS-DRSR)._
      * _**Stealing hashes:** the target server replies by sending cryptographic password hashes for all users in the network domain._
      * _**Domain takevover:** attackers may decrypt these hashes of use them directly to forge Golden Tickets, giving them permanent, undetected access to the entire agency's network._
* _**T1078.002 - Valid Accounts: Domain Accounts Subtechnique**_
  * _**What it is:** a cyberattack sub-technique where adversaries use stolen elgitimate domain account credentials to log into a domain network. Because these credentials work across multiple computers, attacker use them to pivot and move around undetected._
  * _**Parent technique(s):** Valid Accounts (T1078)_
  * _**Target platform(s):** Windows, Linux, macOS, and VMware ESXi_
  * _**Primary tactic(s):** Initial Access, Persistence, Privilege Escalation, and Defense Evasion_
    * _**Offensive TTPs:**_
      * _**Gaining entry:** attackers steal passwords using phishing emails, malware, or credential dumping tools such as `hashcat` or `mimikatz`._
      * _**Belnding in:** they log in using normal user-based or admin accounts so the authorized, administrative use of those tools blends in legitimately._
      * _**Moving around:** they may use the account to jump, pivot, veritcally, or horizontally move laterally from one network segment, or one workstation to another inside the same network._

***

Path-finding tools compute transitive control across permissions, group nesting, session data, and local group membership, answering the question the access review cannot: not _"who is in the group"_ but _"who can reach the group."_

The finding to write is not a list of permissions. It is a comparison of two populations:

```
  Governed privileged population          Effective privileged population
  (what the review examines)              (what enumeration finds)
  ┌────────────────────────┐              ┌────────────────────────┐
  │  Domain Admins      12 │              │  Domain Admins      12 │
  │  Enterprise Admins   3 │              │  Enterprise Admins   3 │
  │  Schema Admins       2 │              │  Schema Admins       2 │
  │  Server Ops          6 │              │  Server Ops          6 │
  │  Backup Ops          4 │              │  Backup Ops          4 │
  └────────────────────────┘              │  ── unreviewed ──      │
         27 identities                    │  ACL-delegated      14 │
                                          │  GPO edit rights     8 │
                                          │  Local admin on DC   5 │
                                          │  Mgmt platform roles 11│
                                          │  Cert template       3 │
                                          └────────────────────────┘
                                                 68 identities

         The delta — 41 identities — is the finding.
```

### 7.4.3 Defensive Validation for Privileged Access

Three changes convert the finding into durable assurance.

**Redefine the population by capability rather than membership.** The review's population-generation logic must enumerate effective authority. If it enumerates groups, it will keep producing clean results while the delta grows.

**Bring the delta under governance.** Every identity in the effective population either enters the approved population with an approval record, or loses the path. There is no third disposition that survives scrutiny.

**Detect new paths rather than re-discovering them quarterly.** Permission changes on privileged objects are logged as directory object modifications, and a standing detection is far cheaper than a quarterly enumeration.

```kql
// Microsoft Sentinel — new control-class permissions granted on Tier 0 objects.
// Requires directory object auditing (SACL) on the privileged OUs and groups.
SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID == 5136                                    // directory object modified
| where AttributeLDAPDisplayName == "nTSecurityDescriptor"  // ACL change
| extend TargetDN = tostring(ObjectDN)
| where TargetDN has_any ("OU=Domain Controllers", "CN=Domain Admins",
                          "CN=Enterprise Admins", "CN=krbtgt")
| project TimeGenerated, SubjectAccount = Account, TargetDN,
          OperationType, ObjectClass, Computer
| order by TimeGenerated desc
```

```spl
index=wineventlog EventCode=5136 Attribute_LDAP_Display_Name="nTSecurityDescriptor"
| search Object_DN="*OU=Domain Controllers*" OR Object_DN="*CN=Domain Admins*"
         OR Object_DN="*CN=Enterprise Admins*" OR Object_DN="*CN=krbtgt*"
| table _time, Account_Name, Object_DN, Operation_Type, Object_Class, ComputerName
| sort - _time
```

> #### **Did You Know?**
>
>

{% hint style="info" %}
#### **Did You Know?**

The distinction between governed and effective privilege has a direct FISCAM expression. Under the manual's treatment of system-generated information, an assessor relying on a report must consider whether that report is complete and accurate for the purpose used. A privileged-user report that enumerates group membership is complete and accurate as a statement about group membership. Used to support a conclusion about privileged access, it is neither.

Security teams sometimes discover that the fastest route to funding an identity-attack-path program is not the security argument at all. It is showing the audit liaison that the agency's privileged
{% endhint %}

***

### 7.5 Separation of Duties

Separation of duties is an internal-control concept that predates information systems by centuries, and it translates imperfectly into identity environments because the thing being separated is authority rather than task.

**The FICAM assertion:** no single identity can complete a sensitive transaction end to end without independent participation.

**The control objective:** conflicting duties are assigned to different identities, and no identity can both perform a sensitive action and conceal or approve it.

**Typical implementation:** role definitions with conflict matrices, workflow approvals requiring a second party, and periodic review of role combinations.

**Typical evidence:** a segregation matrix, role assignment exports, and approval records showing distinct requester and approver.

### 7.5.1 What Separation of Duties Actually Requires

A meaningful separation control has to survive three tests, and identity implementations commonly satisfy the first while failing the second and third.

**Assignment separation.** Two conflicting roles are not assigned to the same identity. This is the test most tooling performs.

**Path separation.** The identity cannot reach the second role indirectly. If a requester can modify the group that defines approvers, the roles are separated on paper and unified in effect.

**Evidence separation.** The identity that performs the action cannot alter the record of it. Where the actor controls the log source, audit policy, or reporting query, separation has failed even if assignment and path are clean.

The third test is where identity infrastructure differs sharply from financial systems. A payables clerk cannot usually rewrite the ledger. A domain administrator can usually rewrite the audit configuration.

Separation combinations worth enumerating in an identity environment:

| Conflicting authorities                                                    | Why it matters                                                 |
| -------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Create accounts + approve access requests                                  | Self-provisioned privilege with a valid-looking approval trail |
| Modify group membership + perform access review                            | The reviewer sets what is reviewed                             |
| Administer the directory + administer the SIEM or audit policy             | Action and evidence in one identity                            |
| Manage certificates + hold enrollment rights on an authentication template | Credential issuance without identity proofing                  |
| Administer backups + administer the systems backed up                      | Restoration as an unlogged change mechanism                    |
| Approve changes + implement changes in production                          | Change control becomes self-certification                      |
| Manage the PAM vault + hold accounts stored in it                          | Retrieval without the approval the vault enforces              |
| Manage the HR feed + manage provisioning                                   | Authoritative source and consumer under one authority          |

### 7.5.2 The Adversarial Challenge to Separation

The challenge is to complete a sensitive transaction end to end using a single identity, or a set of identities under single control.

The productive technique is to work backward from the transaction rather than forward from the matrix. Choose a sensitive outcome - grant Domain Admin, issue an authentication certificate, restore a domain controller, disable audit logging - and enumerate every combination of authority that produces it. Then ask whether any single identity holds a full combination, and whether any identity can acquire the missing piece.

Small teams generate structural conflicts that no matrix will resolve, and this is the norm at component agencies and smaller commands rather than the exception. Where the same four people run the directory, the SIEM, the backups, and the change process, assignment separation is not achievable. The honest treatment is to say so, document what compensates - dual authorization for defined actions, evidence forwarded outside the team's control, review performed by a different organization - and stop asserting a separation that does not exist.

### 7.5.3 Defensive Validation for Separation

The validating question is whether the evidence path escapes the actor's authority.

```powershell
# Identities holding both directory-write authority and audit or log-source control.
# The pairing collapses action and evidence into a single identity.
$dirWriters = @()
$rootDN = (Get-ADDomain).DistinguishedName
(Get-Acl "AD:\$rootDN").Access |
  Where-Object { $_.ActiveDirectoryRights -match 'GenericAll|WriteDacl|WriteProperty' } |
  ForEach-Object { $dirWriters += $_.IdentityReference.Value }

# Compare against principals holding "Manage auditing and security log" (SeSecurityPrivilege)
# on domain controllers — exported from the Default Domain Controllers Policy.
secedit /export /cfg $env:TEMP\dcpol.inf /areas USER_RIGHTS | Out-Null
$auditManagers = (Select-String -Path "$env:TEMP\dcpol.inf" -Pattern 'SeSecurityPrivilege').Line

Write-Host "Directory writers:" ($dirWriters | Sort-Object -Unique)
Write-Host "Audit log managers:" $auditManagers
# Any principal appearing in both lists is a separation-of-duties finding.
```

Where separation cannot be achieved by assignment, it can often be achieved by architecture. Forwarding security events to a collector the administrative population cannot modify converts an unachievable assignment control into an achievable evidence control. That substitution is worth documenting explicitly, because an assessor who sees "separation of duties: not achievable, compensated by independent evidence collection" can test the compensating control, whereas an assessor who sees an aspirational matrix will test the matrix and find it false.

***

### 7.6 Authentication Assurance and Alternate Paths

**The FICAM assertion:** authentication occurs at the assurance level appropriate to the risk of the resource, using credentials bound to a proofed identity.

**The control objective:** no identity can obtain access to a protected resource through an authentication mechanism weaker than the one the architecture requires.

**Typical implementation:** PIV or CAC required for interactive logon, phishing-resistant multifactor for cloud and remote access, conditional access policies, and legacy protocol restrictions.

**Typical evidence:** authentication policy configuration, conditional access policy exports, and sign-in telemetry showing method distribution.

### 7.6.1 The Alternate Path Problem

Authentication controls fail through alternates rather than through defeat. The configured path holds; a second path exists that the control never contemplated.

The recurring alternates in a federal Active Directory environment:

* **NTLM where Kerberos was assumed.** Applications, appliances, scanners, and legacy services frequently negotiate NTLM. An identity enforced to smart card for interactive logon may still authenticate to a service using derived material.
* **Legacy protocols in hybrid environments.** Basic authentication endpoints, older mail protocols, and legacy client access paths bypass modern conditional access by predating it.
* **Certificate-based authentication.** A certificate issued to an identity authenticates that identity. Where enrollment rights are broad or template configuration permits a requester-supplied subject, certificate issuance becomes an authentication bypass, and the resulting authentication looks entirely legitimate in telemetry.
* **Service accounts and workload identities.** These typically authenticate with a secret and are frequently excluded from multifactor requirements by necessity.
* **Break-glass and exception accounts.** Excluded from the policy by design, and often from the monitoring as well.
* **Delegation.** A service permitted to act on behalf of a user authenticates as that user without the user's credential.
* **Session and token reuse.** A stolen session cookie or refresh token produces authorized access without a fresh authentication event.
* **Policy scope gaps.** A conditional access policy scoped to a group covers the group's members. Identities outside it are unconstrained, and nothing in the policy announces its own scope limitation.

### 7.6.2 The Adversarial Challenge to Authentication

The assertion to falsify is that the strong path is the only path.

The method is enumeration of what actually authenticated, rather than inspection of what policy requires. Sign-in telemetry answers questions that policy exports cannot.

```kql
// Successful authentications by Tier 0 identities that did not use a
// phishing-resistant method, including service and legacy paths.
let tier0 = _GetWatchlist('Tier0Accounts') | project UPN = tolower(tostring(UserPrincipalName));
SigninLogs
| where TimeGenerated > ago(30d)
| where ResultType == 0                                  // successful only
| extend Method = tostring(AuthenticationDetails)
| where tolower(UserPrincipalName) in (tier0)
| where Method !has "certificate" and Method !has "FIDO" and Method !has "Windows Hello"
| summarize Attempts = count(),
            Apps = make_set(AppDisplayName, 20),
            Methods = make_set(Method, 10),
            IPs = dcount(IPAddress)
    by UserPrincipalName, ClientAppUsed
| order by Attempts desc
```

```spl
index=wineventlog EventCode=4776
| stats count AS ntlm_auths values(Workstation) AS sources BY Logon_Account
| lookup tier0_accounts.csv account AS Logon_Account OUTPUT tier0_account
| where isnotnull(tier0_account)
| sort - ntlm_auths
```

Event 4776 is the domain controller's record of NTLM credential validation. A privileged account generating 4776 events is authenticating through a path that smart card enforcement does not govern, and the volume tells you whether it is an occasional application or a standing dependency.

> #### **Warning - Certificate Templates Are Authentication Policy**
>
> An enterprise certificate authority that issues client-authentication certificates is an identity provider. Where a template permits the requester to supply the subject, allows enrollment by broad groups, or does not require manager approval, the authority to enroll is the authority to authenticate as another identity. This produces a successful, policy-compliant, phishing-resistant authentication event for an identity the requester does not own.
>
> Authentication assurance therefore cannot be assessed from authentication configuration alone. The certificate template configuration is part of the authentication control, and it is administered by a different team in most agencies.

### 7.6.3 Defensive Validation for Authentication

Validation means proving that the alternates are closed, monitored, or accepted.

Enumerate every authentication path into each protected resource, not every policy applied to it. For each path, record the assurance level it actually achieves, whether it is required for an operational reason, and what detection covers it. Paths that are neither required nor closed are findings. Paths that are required - a legacy mission application, a scanning appliance - become documented exceptions with compensating detection, which is a defensible position, unlike an undocumented alternate that nobody enumerated.

***

### 7.7 Access Recertification and Dormant Identity

**The FICAM assertion:** access remains appropriate over time, and identities no longer requiring access do not retain it.

**The control objective:** entitlements are periodically confirmed as necessary by an accountable reviewer, and unnecessary entitlements are removed.

**Typical implementation:** a recertification campaign generating reviewer worklists, with removal actions on non-confirmation.

**Typical evidence:** campaign completion records, reviewer decisions, and removal tickets.

### 7.7.1 Why Recertification Underperforms

Recertification is among the most consistently executed and least effective identity controls in federal environments, for reasons that are structural rather than a matter of diligence.

**Reviewers approve what they do not understand.** A manager presented with sixty entitlements named after applications and groups they have never heard of will approve all sixty. The control records a decision. It does not record comprehension.

**Bulk approval defeats the purpose.** Where the interface offers "approve all," completion metrics improve and assurance does not.

**The population inherits the same blind spot as the privileged review.** If the campaign enumerates group membership, it recertifies group membership.

**Removal is frequently not performed.** Non-confirmation generates a ticket. The ticket may be worked, deferred, or closed as a false positive by the same team that would have to break something to act on it.

**Role accumulation is invisible to the interface.** An identity that moved through four positions in eight years holds entitlements from all four. Each looked reasonable at the moment it was granted, and the reviewer sees each in isolation.

The audit result and the security state diverge quietly. Campaign completion is measurable, reportable, and satisfying. Effective authority is none of those things and is what the adversary uses.

### 7.7.2 Dormant and Stale Identity

A dormant identity is an account that exists and retains authority while nobody is watching it, which makes it the highest-value persistence target in the environment.

Categories worth enumerating separately, because they have different owners and different remediation:

* accounts that have never authenticated since creation;
* accounts with no authentication in a defined period, still enabled;
* accounts whose password has not changed beyond the policy interval, indicating exclusion from expiration;
* accounts with `PasswordNeverExpires` set;
* service accounts whose owning application was decommissioned;
* computer objects for hosts no longer in service, which retain their machine account and any delegation configured on them; and
* accounts disabled but not removed, retaining group membership and certificates.

```powershell
# Dormant and stale identity enumeration with the attributes that determine risk.
$cutoff = (Get-Date).AddDays(-90)
Get-ADUser -Filter 'Enabled -eq $true' -Properties lastLogonTimestamp, passwordLastSet,
        PasswordNeverExpires, whenCreated, memberOf, servicePrincipalName,
        'msDS-KeyCredentialLink', description |
  Select-Object SamAccountName, description, whenCreated, PasswordNeverExpires,
      @{n='LastLogon';e={ if ($_.lastLogonTimestamp) {[datetime]::FromFileTime($_.lastLogonTimestamp)} }},
      @{n='PwdAgeDays';e={ if ($_.passwordLastSet) {[int]((Get-Date) - $_.passwordLastSet).TotalDays} }},
      @{n='PrivGroups';e={ ($_.memberOf | Where-Object { $_ -match 'Admin|Operator|Backup' }) -join '; ' }},
      @{n='IsSvc';e={ [bool]$_.servicePrincipalName }},
      @{n='HasKeyCred';e={ [bool]$_.'msDS-KeyCredentialLink' }} |
  Where-Object { -not $_.LastLogon -or $_.LastLogon -lt $cutoff } |
  Sort-Object PwdAgeDays -Descending

# Disabled accounts retaining privileged group membership — disabled is not removed
Get-ADUser -Filter 'Enabled -eq $false' -Properties memberOf |
  Where-Object { $_.memberOf -match 'Domain Admins|Enterprise Admins|Server Operators|Backup Operators' } |
  Select-Object SamAccountName, @{n='Groups';e={ $_.memberOf -join '; ' }}
```

The `msDS-KeyCredentialLink` attribute is included deliberately. A key credential written to a dormant account provides certificate-based authentication for that account without any password, and it does not appear in any review that examines group membership or password age.

### 7.7.3 Defensive Validation for Recertification

Three changes materially improve this control.

**Present authority, not entitlement names.** A reviewer shown "this identity can approve payments up to $250,000" makes a different decision than a reviewer shown "member of `APP-FIN-PROD-APPR-L3`." Where the platform cannot translate, a curated description field is a cheap substitute.

**Measure removal, not completion.** The meaningful metric is entitlements removed as a proportion of entitlements reviewed, tracked over successive campaigns. A campaign that removes nothing across four cycles is either governing a perfect environment or not governing at all.

### **Test the population against enumeration.** Once per year, compare the campaign's population to an independent enumeration of effective authority. The delta is the control's blind spot, expressed as a number an authorizing official can weigh.

### 7.8 Logging, Evidence, and the Observability Gap

**The FICAM assertion:** identity events produce sufficient evidence for monitoring, investigation, and accountability.

**The control objective:** every change to an identity's effective authority, and every use of privileged authority, produces attributable evidence retained for the required period and available to those who need it.

**Typical implementation:** audit policy on domain controllers and Tier 0 hosts, event forwarding to a collector, SIEM ingestion, retention configuration, and detection content.

**Typical evidence:** audit policy configuration, log source inventories, retention settings, and detection rule documentation.

### 7.8.1 The Gap Between Logged and Observable

Four distinct failures hide behind "logging is enabled," and they are worth separating because each has a different fix.

**Generation.** The event was never produced, because the audit subcategory was not enabled or the object had no system access control list. Directory object modification (5136) requires both an enabled subcategory and a SACL on the object. Most agencies enable the subcategory and never set the SACL, which produces a configuration that looks correct and generates nothing.

**Collection.** The event was produced and never left the host. Forwarding gaps, agent failures, and hosts outside the collection scope are ordinary. A domain controller that stopped forwarding three weeks ago will not announce itself.

**Retention.** The event was collected and aged out before anyone looked. Identity compromises are frequently discovered long after the initial access, which makes retention a detection capability rather than a compliance parameter.

**Interpretation.** The event was generated, collected, retained, and means nothing to the analyst because it lacks context. Event 4662 with a GUID in the properties field is technically a record of a directory access. Without the GUID resolved to `DS-Replication-Get-Changes-All`, it is noise.

Only the fourth is a detection-engineering problem. The first three are assurance problems, and an audit that inspects audit policy configuration will detect none of them.

### 7.8.2 The Adversarial Challenge to Evidence

The challenge is to perform a privileged action that produces no evidence, insufficient evidence, or evidence attributable to the wrong actor.

Recurring techniques, each of which is ordinary administration performed with intent:

* **Act through a service account.** The action is logged and attributed to an identity with no human owner. Attribution is technically present and practically absent.
* **Act on a host outside collection.** A management server, an appliance, or a lab system administered from the same directory but not forwarding events.
* **Modify the collection.** Audit policy, SACLs, forwarding subscriptions, and SIEM ingestion filters are all administratively modifiable by the population being observed.
* **Use an authorized path that generates expected telemetry.** A change made through the approved management platform produces exactly the events the detection expects to see and blends into thousands of legitimate ones.
* **Exploit the retention boundary.** Establish access, wait beyond the retention period, then act. The evidence of initial access no longer exists when the later action is investigated.
* **Time the action to reporting cadence.** Grant, use, and remove authority between two review dates.

The last two are why point-in-time controls and retention parameters are security decisions rather than compliance settings.

### 7.8.3 Defensive Validation for Evidence

The validating exercise is a generation test, and it is inexpensive: perform a known privileged action under authorization, then confirm the event was generated, collected, retained, and interpretable.

```powershell
# Verify the audit subcategories that identity detection depends on are actually enabled.
# A subcategory set to "No Auditing" silently defeats every downstream detection.
$required = @(
  'Directory Service Changes',
  'Directory Service Access',
  'Kerberos Authentication Service',
  'Kerberos Service Ticket Operations',
  'Credential Validation',
  'Security Group Management',
  'User Account Management',
  'Sensitive Privilege Use',
  'Audit Policy Change'
)
auditpol /get /category:* | ForEach-Object {
    foreach ($r in $required) {
        if ($_ -match [regex]::Escape($r)) {
            $state = ($_ -split '\s{2,}')[-1].Trim()
            [pscustomobject]@{
                Subcategory = $r
                State       = $state
                Finding     = if ($state -match 'No Auditing') { 'GAP' } else { 'ok' }
            }
        }
    }
} | Sort-Object Finding -Descending

# Confirm a SACL exists on privileged objects — without it, 5136 is never generated
$dn = (Get-ADGroup 'Domain Admins').DistinguishedName
(Get-Acl "AD:\$dn" -Audit).Audit |
  Select-Object IdentityReference, ActiveDirectoryRights, AuditFlags
```

```kql
// Silent log sources — Tier 0 hosts that have stopped reporting.
// A collection gap produces no alert on its own; this query is the alert.
let expected = _GetWatchlist('Tier0Hosts') | project Computer = tolower(tostring(Computer));
let reporting = SecurityEvent
    | where TimeGenerated > ago(24h)
    | summarize LastEvent = max(TimeGenerated) by Computer = tolower(Computer);
expected
| join kind=leftouter reporting on Computer
| extend Status = iff(isnull(LastEvent), "SILENT — no events in 24h", "reporting")
| where Status startswith "SILENT"
| project Computer, Status
```

Two architectural requirements make this control assertable rather than aspirational. Events must reach a collector the reviewed population cannot modify, which is the evidence-separation test from §7.5 applied to telemetry. And retention for identity-relevant events must be set from the realistic detection interval for identity compromise rather than from the shortest period that satisfies a policy minimum.

***

### 7.9 Change Management and Configuration Drift

**The FICAM assertion:** the identity architecture in production reflects the architecture that was designed, approved, and authorized.

**The control objective:** changes to identity infrastructure are requested, reviewed, approved, implemented, and documented, and unauthorized changes are detected.

**Typical implementation:** a change advisory process, ticketing, maintenance windows, and post-implementation review.

**Typical evidence:** change records with approvals and implementation notes.

### 7.9.1 Changes That Escape the Process

Identity configuration drifts through paths the change process was not designed to see. The process governs projects. Authority changes through operations.

| Change                                         | Governed by change management?     | Effect on authority                          |
| ---------------------------------------------- | ---------------------------------- | -------------------------------------------- |
| Adding a user to a privileged group            | Rarely — treated as access request | Direct privilege grant                       |
| Delegating permissions on an OU                | Rarely — treated as administration | Shadow administrator creation                |
| Editing a GPO linked to Tier 0                 | Sometimes                          | Code execution scope change                  |
| Publishing or modifying a certificate template | Rarely — PKI team process          | Authentication path change                   |
| Modifying a conditional access policy          | Sometimes                          | Authentication assurance change              |
| Adding a service principal or app registration | Rarely                             | New non-person identity with consented scope |
| Configuring delegation on a computer object    | Rarely                             | Impersonation path creation                  |
| Changing audit policy                          | Rarely                             | Evidence generation change                   |
| Emergency change during an incident            | By exception                       | Anything, with retroactive documentation     |

The pattern is consistent. Changes that create or alter authority are usually classified as access administration or routine operations, while changes that alter service are classified as changes. The classification tracks operational risk rather than security risk, and identity authority is the casualty.

Emergency changes deserve separate treatment. Every mature process permits them, and every adversary who understands the process knows that an emergency change is a change with retroactive documentation, performed under time pressure, reviewed by people who want the incident to end. The control is not the emergency procedure. The control is whether emergency changes are reconciled afterward with the same rigor as planned ones, and whether anyone measures how many there are.

### 7.9.2 The Adversarial Challenge to Change Management

The challenge is to alter identity authority in a way the change process will never see, in a form indistinguishable from routine administration.

The productive question is which authority-affecting changes are classified as something other than a change, because that classification is the bypass. It requires no technical sophistication and produces no anomalous telemetry.

### 7.9.3 Defensive Validation Through Drift Detection

Change management is assured by reconciliation: comparing the environment's current state to its approved state and investigating every difference.

```powershell
# Baseline-and-compare for Tier 0 authority state. Run on a schedule; diff the output.
# Any difference is either an approved change or a finding — there is no third category.
$baseline = @{
    PrivilegedMembers = foreach ($g in 'Domain Admins','Enterprise Admins','Schema Admins',
                                       'Server Operators','Backup Operators','Account Operators') {
        Get-ADGroupMember -Identity $g -Recursive |
          Select-Object @{n='Group';e={$g}}, SamAccountName, objectClass
    }
    DCOUPermissions   = (Get-Acl "AD:\$((Get-ADDomain).DomainControllersContainer)").Access |
          Where-Object { -not $_.IsInherited } |
          Select-Object IdentityReference, ActiveDirectoryRights, ObjectType
    LinkedGPOs        = (Get-GPInheritance -Target (Get-ADDomain).DomainControllersContainer).GpoLinks |
          Select-Object DisplayName, GpoId, Enabled, Enforced
    DelegatedComputers = Get-ADComputer -Filter * -Properties TrustedForDelegation,
                                 'msDS-AllowedToDelegateTo','msDS-AllowedToActOnBehalfOfOtherIdentity' |
          Where-Object { $_.TrustedForDelegation -or $_.'msDS-AllowedToDelegateTo' -or
                         $_.'msDS-AllowedToActOnBehalfOfOtherIdentity' } |
          Select-Object Name, TrustedForDelegation, 'msDS-AllowedToDelegateTo'
}
$stamp = Get-Date -Format 'yyyyMMdd-HHmm'
$baseline | ConvertTo-Json -Depth 6 | Out-File ".\tier0-baseline-$stamp.json"

# Compare to the prior capture:
#   Compare-Object (Get-Content .\tier0-baseline-PRIOR.json) (Get-Content .\tier0-baseline-$stamp.json)
```

The reconciliation control has one requirement that agencies routinely omit: every detected difference must be dispositioned to an approved change record or investigated as unauthorized. A drift report with no disposition workflow is the reconciliation-theater failure from §7.3 in a different control area.

***

### 7.10 Deprovisioning and Residual Access

**The FICAM assertion:** access is removed when the mission relationship supporting it ends.

**The control objective:** no authentication artifact or entitlement associated with a separated identity can produce a successful authorization decision.

**Typical implementation:** an automated disable action triggered by the authoritative personnel feed, followed by scheduled deletion.

**Typical evidence:** separation records matched against account status, with elapsed-time metrics.

### 7.10.1 Disabled Is Not Removed

Account disablement is a fast, measurable, well-instrumented control that addresses one authentication path. The artifacts that survive it are the residual access.

| Artifact                                             | Survives disable?                                | Why                                                                                                  |
| ---------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Issued authentication certificate                    | Yes, until revoked and the revocation is honored | Certificate validity is independent of account state, and revocation checking is not always enforced |
| Active cloud session / refresh token                 | Yes, until revoked or expired                    | Token lifetime is independent of directory state                                                     |
| Key credential (`msDS-KeyCredentialLink`)            | Yes                                              | Provides certificate-based authentication for the account                                            |
| Shared or service credential known to the person     | Yes                                              | No account to disable                                                                                |
| Local administrator password on endpoints            | Yes                                              | Not directory-managed unless LAPS is deployed                                                        |
| Application-local account                            | Yes                                              | Application does not consume the enterprise directory                                                |
| Owned application registration or service principal  | Yes                                              | The workload identity is separate from the person                                                    |
| SSH key or API token deployed to systems             | Yes                                              | Not represented in the directory                                                                     |
| Group membership                                     | Retained on the disabled object                  | Restored intact if the account is re-enabled                                                         |
| Mailbox delegation and shared access                 | Frequently retained                              | Delegation is a separate object property                                                             |
| Scheduled tasks and services running as the identity | Depends                                          | May continue with cached credentials until restart                                                   |

A separated identity whose account was disabled in four minutes may retain seven of those eleven. The metric that the agency reports - mean time to disable - is accurate and describes one row of the table.

### 7.10.2 The Adversarial Challenge to Deprovisioning

The challenge is to authenticate, or exercise authority, as or on behalf of an identity whose account has been correctly disabled.

The most durable technique requires no post-separation access at all: establish the residual artifact before separation. A certificate enrolled, a key credential written, an application registration created, or a service account whose credential is known, all established while access is legitimate, survive a deprovisioning process that examines account state.

This is the insider variant, and it is the reason deprovisioning validation must look at artifacts rather than accounts.

### 7.10.3 Defensive Validation for Deprovisioning

Validation means enumerating artifacts for a sample of separated identities and confirming that none can produce a successful authorization decision.

```powershell
# For a separated identity, enumerate the artifacts that survive account disablement.
param([string]$SamAccountName)

$u = Get-ADUser $SamAccountName -Properties memberOf, 'msDS-KeyCredentialLink',
        servicePrincipalName, userCertificate, Enabled, whenChanged, lastLogonTimestamp

[pscustomobject]@{
    Account            = $u.SamAccountName
    Enabled            = $u.Enabled
    GroupsRetained     = ($u.memberOf | Measure-Object).Count
    KeyCredentials     = ($u.'msDS-KeyCredentialLink' | Measure-Object).Count
    SPNsRegistered     = ($u.servicePrincipalName | Measure-Object).Count
    CertsOnObject      = ($u.userCertificate | Measure-Object).Count
    LastDirChange      = $u.whenChanged
}

# Certificates issued to the identity that remain unrevoked (run on the CA)
certutil -view -restrict "RequesterName=$env:USERDOMAIN\$SamAccountName,Disposition=20" `
         -out "RequestID,RequesterName,NotAfter,CertificateTemplate"
```

The deprovisioning control should be restated as a checklist of artifact classes rather than an account action, with an owner for each class. Certificates belong to the PKI team, tokens to the cloud identity team, local credentials to the endpoint team, application accounts to the application owners. An agency that has assigned all of them can assert deprovisioning. An agency that has assigned only the directory account can assert that the directory account was disabled, which is true and much narrower than the assertion usually made from it.

> #### **Warning - The Metric Measures the Easy Path**
>
> Mean time to disable is the most commonly reported deprovisioning metric in federal identity programs, and it measures the fastest, most automated, least residual of the artifact classes. Reporting it as evidence of deprovisioning effectiveness is not dishonest, but it invites a conclusion the measurement does not support. If the program reports one number, the more defensible one is the proportion of artifact classes with an assigned owner and a verification step.

***

### 7.11 Living Off the Land, Masquerading, and Evidence Obfuscation

The preceding sections examined control areas. This section examines the techniques that cut across all of them, because a control's assurance value depends heavily on whether the activity it is meant to catch looks different from the activity it is meant to permit.

For identity infrastructure, the answer is usually that it does not.

### 7.11.1 Living Off the Land (LOTL)

Living off the land describes the use of tooling already present and authorized in the environment rather than introduced malware. In an identity context the technique is unusually effective, because administration of a directory is performed with tools whose entire purpose is to modify identity and authority.

An adversary holding administrative authority needs nothing that a support technician does not already use:

* directory management consoles and their command-line equivalents;
* the built-in PowerShell modules for directory, group policy, and certificate administration;
* remote management protocols already permitted between administrative and target systems;
* the endpoint management platform's own software distribution capability;
* scheduled task infrastructure;
* the backup platform's restore capability; and
* certificate enrollment through the approved enterprise process.

None of that produces a malicious file for an endpoint product to detect. All of it produces telemetry indistinguishable in form from legitimate administration.

The control implication is specific. Detection cannot rest on the tool. It must rest on the relationship between actor, action, target, and context - which identity performed which change against which object from which source at what time, and whether that combination is consistent with the actor's governed authority.

That is a harder detection to build and the only one that works against an adversary using the same tools as the administrators.

### 7.11.2 Masquerading and Impersonation

Masquerading is the adversary making activity appear to originate from a legitimate identity, process, or system. Impersonation is exercising authority as another identity. Both defeat attribution, which is what most identity evidence ultimately rests on.

The identity-specific forms:

* **Service account use.** Activity attributed to a non-person identity with no owner is attributed to nobody in practice.
* **Delegation.** A service configured to act on behalf of users generates authentication and access events attributed to those users.
* **Certificate-based impersonation.** A certificate obtained through a permissive template produces authentication events for an identity the adversary does not own, at a high assurance level, through the approved path.
* **Naming.** An account named to resemble a service, a host, or an administrative convention passes visual review indefinitely. A group whose name matches the organization's standard is not questioned.
* **Process and path masquerading.** Renaming or relocating a binary to resemble a system component defeats analyst pattern recognition and simple detections.
* **Session hijacking.** Using an existing authenticated session produces no new authentication event at all.

The defensive countermeasure is not better naming conventions. It is ensuring that every identity capable of exercising meaningful authority has an accountable owner, and that authority exercised by non-person identities is scoped narrowly enough that its misuse is detectable as an anomaly against a narrow baseline.

### 7.11.3 Obfuscation and Evidence Manipulation

Obfuscation targets the interpretation stage of §7.8. The event is generated and collected and does not mean what an analyst would need it to mean.

Techniques range from trivial to structural:

* command-line obfuscation that defeats string-matching detections;
* encoding and indirection that hide intent from a log record;
* performing an action in many small steps, each individually unremarkable;
* generating a high volume of benign activity of the same type;
* operating during periods of high legitimate change, such as a migration or an incident;
* modifying audit configuration before the action and restoring it afterward; and
* clearing or truncating logs, which is detectable but only if the detection exists and someone acts on it.

Two events deserve standing detections in any identity environment, because both indicate an attempt to manipulate the evidence layer itself: 1102, the clearing of the security audit log, and 4719, a change to system audit policy. Neither is common in normal operations, both are trivially alertable, and their absence from a detection catalog is a reasonable proxy for the maturity of the whole program.

```kql
// Evidence-layer tampering on Tier 0 hosts. Low volume, high signal.
let tier0 = _GetWatchlist('Tier0Hosts') | project Computer = tolower(tostring(Computer));
SecurityEvent
| where TimeGenerated > ago(90d)
| where EventID in (1102, 4719, 4739, 4907)   // log cleared, audit policy change,
                                              // domain policy change, SACL change
| where tolower(Computer) in (tier0)
| project TimeGenerated, EventID, Activity, Computer, Account, SubjectUserName
| order by TimeGenerated desc
```

### 7.11.4 What This Means for Control Assurance

Every technique in this section is available to an adversary who has obtained administrative authority, and none of them is defeated by the control being well designed or faithfully executed.

That produces the chapter's sharpest conclusion. Once an adversary holds administrative authority over identity infrastructure, the controls governing that infrastructure lose most of their assurance value, because the adversary now sits inside the population the control governs and the evidence path the control depends on.

Control assurance therefore protects against the accumulation of authority, not against its use. The entire weight of the program falls on the earlier stages: provisioning, privilege containment, authentication assurance, and the clean source dependencies of §4.6.

This is also why evidence separation is not a bureaucratic nicety. It is the one control property that retains value after administrative compromise, and only if the evidence path terminates outside the compromised authority.

***

### 7.12 Adversarial Control Validation as a Program

Individual challenges produce findings. A program produces assurance, and the difference is repeatability.

A defensible adversarial control validation program has six components.

1. **A control register with stated assertions.** Every identity control written as a falsifiable assertion in the form developed in §7.2.1. Controls whose assertion cannot be stated are the first finding.
2. **A validation calendar.** Each assertion tested on a defined interval, with intervals set by the authority at stake rather than by convenience. Tier 0 privilege enumeration belongs on a shorter cycle than application entitlement review.
3. **Authorized methodology.** Documented scope, rules of engagement, approved tooling, deconfliction with operations, and rollback for any change made during testing. This is what separates validation from an unauthorized assessment, and it is what allows the program to survive its first disruptive result.
4. **Findings written as paths.** A finding names the identity, the path, the authority obtained, the control that did not see it, and the population boundary that excluded it. "Excessive privilege observed" is not a finding.
5. **Remediation that corrects the control.** The four-step sequence from §7.2.7, with the third step - correcting the population logic that missed the path - treated as mandatory rather than optional.
6. **Evidence retained for reuse.** Before-and-after enumerations supporting POA\&M closure, assessment responses, and continuous monitoring reporting. Work performed once should answer the same question for the security team, the assessor, and the authorizing official.

The program's output belongs in continuous monitoring rather than in an annual cycle. Under the Risk Management Framework, ongoing assessment of control effectiveness is already the expectation; adversarial validation is a method for satisfying it with technical evidence rather than reattestation.

| Control area         | Assertion to falsify                                                      | Suggested interval                                           |
| -------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Provisioning         | Every identity originated from an approved workflow                       | Quarterly reconciliation, continuous exception alerting      |
| Privileged access    | No identity reaches Tier 0 outside the governed population                | Monthly enumeration, continuous ACL-change detection         |
| Separation of duties | No identity completes a sensitive transaction alone                       | Semiannual, plus on reorganization                           |
| Authentication       | No path weaker than the required assurance level reaches the resource     | Monthly telemetry review                                     |
| Recertification      | The campaign population equals effective authority                        | Annual comparison against enumeration                        |
| Logging              | Privileged action produces attributable, retained, interpretable evidence | Quarterly generation test, continuous silent-source alerting |
| Change management    | Production state matches approved state                                   | Weekly drift capture, continuous Tier 0 change alerting      |
| Deprovisioning       | No artifact of a separated identity authorizes access                     | Quarterly artifact sampling                                  |

***

### Field Note — Read the Control's Population Before You Read the Control

When you are handed an identity control to evaluate, do not begin with the control description. Begin with the question of what set of things the control examines, and how that set is produced.

Ask for the query.

Not the policy. Not the procedure. The actual query, script, report definition, or platform configuration that generates the population the control operates against.

Then ask four questions about it.

1. _What does it enumerate?_
2. _What could hold this authority that it does not enumerate?_
3. _Who can modify it?_
4. _When was it last compared to an independent enumeration?_

In most federal environments the fourth question has no answer, and the second has a long one.

This technique works because nearly every identity control failure this chapter describes is a population failure wearing a different costume. The access review that misses shadow administrators, the recertification campaign that recertifies group names, the deprovisioning metric that measures one artifact class, the drift report with no disposition, the audit policy enabled without a SACL - each is a control operating faithfully against a population that does not represent the security condition being asserted.

The control is not lying. It is answering a narrower question than the one being asked of its result.

Find the query. The query is the control.

***

> ### **Sidebar — The Auditor and the Adversary**
>
> _Two people examined the same environment in the same month. Neither have met the other._
>
> **The auditor:** I requested the privileged user listing and received it within a day, which is better than most engagements. Twenty-seven identities across five groups. I selected a sample of eight, traced each to an approved request, and confirmed the approvals were current and appropriately authorized. I reperformed the population query to satisfy myself it ran as described. My conclusion was that the control was operating effectively, and I documented it that way, because within the scope of what I tested, it was.
>
> **The adversary:** I never looked at those five groups. Groups are where they watch. I looked for who could write to them, and found a service account belonging to an inventory tool that had been granted permissions on the OU during a 2019 deployment. Nobody had touched it since. It was not in anyone's listing because it was not in anyone's group. I used it once, took what I needed, and left it exactly as I found it.
>
> Both accounts of the environment are accurate. The auditor tested the control and reported the result correctly. The adversary tested the assumption underneath the control and found it false.
>
> The gap between them is not incompetence on either side. It is the difference between a population and an environment - and closing it is the reason this chapter exists.

***

### Chapter 7 Summary

FICAM describes what a federal identity environment should be. FISCAM provides a disciplined methodology for determining whether the controls supporting it are designed appropriately, implemented as described, and operating effectively. Both are necessary, and neither answers the question an adversary asks.

This chapter has argued that identity control assertions should be treated as hypotheses rather than conclusions. A requirement becomes a control objective, an objective becomes an implementation, an implementation produces evidence, an assessor tests that evidence, and an adversary attempts to obtain the same authority the control was meant to constrain - outside the population the evidence describes.

Across every control area the same structure recurred. Provisioning governs identities it can account for. Privileged access governs the membership it enumerates rather than the authority it intends. Separation of duties separates assignments while paths and evidence remain unified. Authentication controls hold on the configured path while alternates persist. Recertification measures completion where removal is the objective. Logging is configured where generation, collection, retention, and interpretation each fail separately. Change management governs projects while authority changes through operations. Deprovisioning disables accounts while artifacts survive.

In each case the control is not defective. It is narrower than the assertion drawn from it, and the adversary works the difference.

Adversarial control validation closes that gap by stating each assertion in falsifiable form, testing it with the techniques an adversary would use, correcting both the finding and the control logic that missed it, and retaining the result as evidence. Applied continuously, it converts compliance activity into security assurance and gives an authorizing official something to weigh other than an attestation.

The control is the query. The assurance is what survives an attempt to falsify it.

### **Chapter 7 Key Concepts Review**

* FICAM defines intended identity outcomes; FISCAM evaluates whether supporting controls can be relied upon. Neither, alone, proves an environment is secure.
* A control activity is not a security outcome. Account disablement is an activity; the removal of all authority derived from the identity is the outcome.
* Every identity control operates against a population. The population is produced by a query, and everything outside it is ungoverned by construction.
* Audit assurance is a statement about a population; exploitation is a statement about an element. A ninety-nine percent result says nothing about what the remaining element can reach.
* Privilege is effective authority, not group membership. The difference between the two populations is where shadow administrators exist.
* Management override is the residual risk that survives good control design, because the population operating a control frequently has authority over the control and its evidence.
* Separation of duties requires assignment separation, path separation, and evidence separation. Most identity implementations achieve only the first.
* Authentication controls fail through alternates rather than defeat. Certificate templates, legacy protocols, delegation, and policy scope gaps are authentication policy whether or not they are administered by the identity team.
* Logging fails at four independent stages - generation, collection, retention, interpretation - and inspecting audit policy configuration detects only the first.
* Living-off-the-land, masquerading, and obfuscation are effective against identity controls because administration of a directory uses the same tools as its abuse.
* Once an adversary holds administrative authority over identity infrastructure, control assurance retains value only where the evidence path terminates outside that authority.
* Adversarial control validation states each assertion in falsifiable form, tests it, corrects both the path and the control logic that missed it, and retains the result as reusable evidence.

### **Key Terminology**

Adversarial identity assurance · control assertion · falsifiable form · population completeness · management override · effective authority · governed population · shadow administrator · residual access · artifact class · evidence separation · alternate authentication path · drift reconciliation · generation test · control register

### **Chapter 7 Review Questions**

Answers are found in the subsection noted after each question.

1. Explain the difference between a control activity and a security outcome, using account disablement as the example. (§7.1.1, §7.10.1)
2. State the seven-stage chain from identity requirement to defensive validation, and explain what each stage adds. (§7.2)
3. Rewrite the requirement "access shall follow least privilege" in falsifiable form, and explain why the original cannot be tested. (§7.2.1)
4. Define population completeness and management override, and explain why each has offensive relevance. (§7.1.2)
5. Name six paths by which an identity can hold administrative authority over a domain controller without appearing in a privileged group. (§7.4.1)
6. A quarterly privileged access review is executed faithfully and produces a clean result. Explain how a shadow administrator can persist through it indefinitely. (§7.4.1, §7.4.2)
7. Distinguish assignment separation, path separation, and evidence separation. Which is most often absent in identity environments, and why? (§7.5.1)
8. An account is enforced to smart card for interactive logon. Name three ways it may still authenticate through a weaker path. (§7.6.1)
9. Explain why a certificate template is part of the authentication control even though it is administered by the PKI team. (§7.6.2)
10. Name the four independent stages at which logging fails, and state which of them an inspection of audit policy configuration would detect. (§7.8.1)
11. Why does event 5136 frequently fail to appear even when the corresponding audit subcategory is enabled? (§7.8.1, §7.8.3)
12. List five artifacts associated with a separated identity that survive account disablement. (§7.10.1)
13. Explain why mean time to disable is an accurate metric that invites an unsupported conclusion. (§7.10.3)
14. Why are living-off-the-land techniques unusually effective against identity infrastructure specifically? (§7.11.1)
15. Explain the chapter's conclusion that control assurance protects against the accumulation of authority rather than its use. (§7.11.4)

***

### **Applied Exercise - Northgate Agency**

Northgate Agency's identity program reports the following to its authorizing official.

Privileged access is reviewed quarterly. The review population is generated by a PowerShell script maintained by the directory team, which enumerates members of Domain Admins, Enterprise Admins, Schema Admins, Server Operators, and Backup Operators. Last quarter's review covered 31 identities, all approved, and was signed on time.

All privileged accounts are enforced to smart card for interactive logon. Multifactor is required for cloud access through a conditional access policy scoped to the group `CAP-MFA-Required`, which is populated by a nightly job from the HR feed. Service accounts are excluded by an exception group.

Security events are collected from all domain controllers to the agency SIEM with 90-day retention. The directory team administers both the domain controllers and the SIEM ingestion configuration. Audit policy was configured during the 2021 accreditation and has not been changed since.

Access recertification runs annually, achieving 100 percent reviewer completion for the last three cycles, with 4 entitlements removed across all three.

Separation upon employee departure averages 3.2 minutes from HR feed to account disable, which the program reports as its headline identity metric.

16. For each of the five statements above, write the assertion the program is making and the narrower assertion the evidence actually supports.
17. Identify at least six specific attack paths or residual exposures this program would not detect.
18. Which single change would most improve the assurance value of the program, and why?
19. The agency asks you to write the residual risk statement for privileged access in a form the authorizing official can act on. Draft it.

**Answer Key - Applied Exercise**

**16.** **Privileged access:** asserts that privileged authority is governed; supports only that membership in five named groups was approved (§7.4.1). **Authentication:** asserts phishing-resistant authentication for privileged identities; supports only that interactive logon requires smart card for enforced accounts, and that cloud MFA applies to members of one group with a documented exclusion set (§7.6.1). **Logging:** asserts identity events are auditable; supports only that events reaching the SIEM from domain controllers are retained 90 days, with generation unverified since 2021 and the evidence path inside the reviewed population's authority (§7.8.1, §7.5.1). **Recertification:** asserts access remains appropriate; supports only that reviewers completed the interface (§7.7.1). Deprovisioning: asserts access is removed on separation; supports only that the directory account is disabled quickly (§7.10.1).

**17.** **Six or more of:** (a) shadow administrators holding delegated ACL rights, GPO edit rights, local administrator on Tier 0 hosts, or management platform roles, none of which the script enumerates; (b) certificate templates permitting requester-supplied subjects, an authentication path outside the smart card control; (c) identities absent from `CAP-MFA-Required` because the nightly job did not add them, plus everything in the service account exception group; (d) NTLM authentication by privileged accounts, ungoverned by smart card enforcement; (e) audit subcategories or SACLs that were never enabled, or that have drifted since 2021, producing silent gaps no configuration review would catch; (f) the directory team's control over both the action and the SIEM ingestion, collapsing evidence separation; (g) residual artifacts on separated identities - certificates, key credentials, tokens, application registrations, local credentials - none measured by the 3.2-minute metric; (h) authority granted and removed between annual recertification cycles.

**18.** Redefining the privileged population by effective authority rather than group membership (§7.4.3). It is the change with the widest downstream effect: it corrects the privileged access review, supplies the correct population for recertification comparison, exposes the shadow administrators that every other control inherits as a blind spot, and converts the program's largest unsupported assertion into a measurable one. Moving SIEM ingestion outside the directory team's authority is the strongest second change, because it is the only one that retains value after administrative compromise (§7.11.4).

**19.** **A defensible form:** The quarterly privileged access review enumerates membership in five named groups. It does not enumerate delegated directory permissions, GPO edit rights on objects linked to Tier 0, local administrator membership on Tier 0 hosts, administrative roles in the endpoint management and backup platforms, or certificate templates permitting client authentication with a requester-supplied subject. An independent enumeration performed on \[`date`] identified `N` identities holding administrative authority over Tier 0 outside the reviewed population, of which `M` have no current approval record. Residual risk is the authority held by those `M` identities, exercisable without appearing in any control population, between enumerations. Recommended treatment: redefine the review population by effective authority and re-baseline; interim compensating control is continuous alerting on permission changes to Tier 0 objects. (§7.2.8, §7.4.3)

***

### References

Running list for the chapter references page. Verify currency at publication — several of these revised within the last two years.

**Federal Audit and Internal Control**

1. U.S. Government Accountability Office. _Federal Information System Controls Audit Manual (FISCAM)_. GAO-26-108633. 2026 revision; effective beginning with fiscal year and calendar year 2026 audits of federal entity financial statements, and for attestation engagements and performance audits beginning on or after October 1, 2026. Supersedes the September 2024 revision (GAO-24-107026) and GAO-09-232G (2009). [https://www.gao.gov/fiscam](https://www.gao.gov/fiscam)
2. U.S. Government Accountability Office. _FISCAM Framework Crosswalk from 2009 to 2026_ (supplemental Excel workbook). Accompanies GAO-26-108633. [https://www.gao.gov/fiscam](https://www.gao.gov/fiscam)
3. U.S. Government Accountability Office. _Cybersecurity Program Audit Guide (CPAG)_. GAO-23-104705. September 2023. [https://www.gao.gov/cpag](https://www.gao.gov/cpag)
4. U.S. Government Accountability Office. _Standards for Internal Control in the Federal Government_ ("Green Book"). Issued May 15, 2025. [https://www.gao.gov/greenbook](https://www.gao.gov/greenbook)
5. U.S. Government Accountability Office. _Government Auditing Standards_ ("Yellow Book"). [https://www.gao.gov/yellowbook](https://www.gao.gov/yellowbook)
6. U.S. Government Accountability Office and Council of the Inspectors General on Integrity and Efficiency. _Financial Audit Manual (FAM)_, Volume 1. Issued June 29, 2026. [https://www.gao.gov/financial-audit-manual](https://www.gao.gov/financial-audit-manual)

**Federal Identity Policy and Architecture**

7. Homeland Security Presidential Directive 12 (HSPD-12), _Policy for a Common Identification Standard for Federal Employees and Contractors_. August 27, 2004.
8. Office of Management and Budget. Memorandum M-19-17, _Enabling Mission Delivery through Improved Identity, Credential, and Access Management_. May 21, 2019. (Rescinds and replaces M-11-11 and M-04-04.)
9. Office of Management and Budget. Memorandum M-22-09, _Moving the U.S. Government Toward Zero Trust Cybersecurity Principles_. January 26, 2022.
10. Executive Order 14028, _Improving the Nation's Cybersecurity_. May 12, 2021.
11. General Services Administration. _Federal Identity, Credential, and Access Management (FICAM) Architecture_ and associated playbooks. [https://playbooks.idmanagement.gov](https://playbooks.idmanagement.gov)
12. National Institute of Standards and Technology. _FIPS 201-3, Personal Identity Verification (PIV) of Federal Employees and Contractors_. January 2022.

**NIST Guidance**

13. NIST SP 800-53, Rev. 5, _Security and Privacy Controls for Information Systems and Organizations_. Control families referenced in this chapter: AC-2, AC-3, AC-5, AC-6, AC-17, AU-2, AU-3, AU-6, AU-9, AU-11, AU-12, CA-2, CA-7, CM-3, CM-5, IA-2, IA-5, IA-8, PS-4, PS-5, SI-4.
14. NIST SP 800-53A, Rev. 5, _Assessing Security and Privacy Controls in Information Systems and Organizations_.
15. NIST SP 800-37, Rev. 2, _Risk Management Framework for Information Systems and Organizations_.
16. NIST SP 800-63 series, _Digital Identity Guidelines_ (identity assurance, authenticator assurance, and federation assurance levels). Confirm the current revision at publication.
17. NIST SP 800-92, _Guide to Computer Security Log Management_. Confirm revision status at publication.
18. NIST SP 800-137, _Information Security Continuous Monitoring (ISCM) for Federal Information Systems and Organizations_.
19. NIST SP 800-207, _Zero Trust Architecture_. August 2020.
20. NIST SP 800-157, _Guidelines for Derived PIV Credentials_.

**Department of Defense**

21. DoD Instruction 8500.01, _Cybersecurity_.
22. DoD Instruction 8510.01, _Risk Management Framework for DoD Systems_.
23. DoD Instruction 8520.02, _Public Key Infrastructure (PKI) and Public Key (PK) Enabling_.
24. DoD Instruction 8520.03, _Identity Authentication for Information Systems_.
25. DoD, _Zero Trust Strategy_. November 2022, and _Zero Trust Reference Architecture_.
26. Committee on National Security Systems Instruction (CNSSI) No. 1253, _Security Categorization and Control Selection for National Security Systems_.
27. Defense Information Systems Agency. Security Technical Implementation Guides (STIGs) for Windows Server, Active Directory Domain, and Active Directory Forest. [https://public.cyber.mil/stigs/](https://public.cyber.mil/stigs/)

**Threat and Technique References**

28. MITRE ATT\&CK. Techniques referenced in this chapter include T1078 (Valid Accounts) and T1078.002 (Domain Accounts), T1098 (Account Manipulation) and T1098.001, T1136 (Create Account), T1207 (Rogue Domain Controller), T1484.001 (Group Policy Modification), T1550 (Use Alternate Authentication Material), T1556 (Modify Authentication Process), T1562.002 (Impair Defenses: Disable Windows Event Logging), T1070.001 (Indicator Removal: Clear Windows Event Logs), T1036 (Masquerading), T1218 (System Binary Proxy Execution), and T1649 (Steal or Forge Authentication Certificates). [https://attack.mitre.org](https://attack.mitre.org)
29. MITRE D3FEND. [https://d3fend.mitre.org](https://d3fend.mitre.org)
30. Australian Signals Directorate's Australian Cyber Security Centre, with NSA, CISA, and international partners. _Detecting and Mitigating Active Directory Compromises_. September 2024.
31. Cybersecurity and Infrastructure Security Agency. Binding Operational Directive 23-02, _Mitigating the Risk from Internet-Exposed Management Interfaces_. June 2023.

**Cross-References Within This Volume**

32. Chapter 4, §4.6, "The Clean Source Principle" — administrative dependency inheritance, trust inversion, and evidence-path integrity as applied to control assurance in §7.2.8 and §7.11.4.
33. Chapter 6 — FICAM architecture, assurance levels, Person and Non-Person Entities, and federation, assumed as prerequisite knowledge throughout this chapter.

\[XREF: confirm chapter numbers for the AD CS / certificate services treatment referenced in §7.6.2 and the Golden SAML / federation treatment referenced in §7.6.1]

"use strict";!function(){let e="remote\_reload\_attempted:",t=document.documentElement.dataset.buildTimestamp??"",n=0,i=0,o=!1,r=!1;function a(){r=!0,o=!1,clearTimeout(i),document.removeEventListener("visibilitychange",l),window.\_\_CLIENT\_HEALTH\_\_={disabled:!0},window.dispatchEvent(new Event("clienthealth"))}function c(){return"hidden"===document.visibilityState?72e5:18e5}function l(){if(clearTimeout(i),r)return;let e=Math.min(c(),n+c()-Date.now());e>0?i=window.setTimeout(l,e):d()}function d(){if(r||(n=Date.now(),l(),o))return;let i=function(e){let t=document.cookie.match(new RegExp("(?:^|; )"+e+"=(\[^;]\*)"));if(!t)return"";try{return decodeURIComponent(t\[1])}catch{return t\[1]\}}("anthropic-device-id").replace(/\[^\x20-\x7E]/g,"").trim();fetch("/edge-api/client-health/check?"+new URLSearchParams({platform:"web",bundle:t,locale:navigator.language||"en-US"}).toString(),{cache:"no-store",credentials:"omit",headers:i?{"anthropic-device-id":i}:{\}}).then(e=>410===e.status?(a(),null):e.ok?e.json():null).then(t=>{if(r||!t||"object"!=typeof t)return;window.\_\_CLIENT\_HEALTH\_\_=t,window.dispatchEvent(new Event("clienthealth"));let n=t.control;if(!n)return;if("lockout"===n.type){try{sessionStorage.setItem("client\_health\_lockout",JSON.stringify({message:n.message,cta:n.cta}))}catch{}let e=window.location;return void e.replace("/health/update-required?returnTo="+encodeURIComponent(e.pathname+e.search))}if("load-shed"===n.type){let e=window.location,t=n.retryAfter;return void e.replace("/health/unavailable?returnTo="+encodeURIComponent(e.pathname+e.search)+("number"==typeof t&\&t>0?"\&t="+t:""))}if("reload"!==n.type)return;let i=n.id;if("string"==typeof i&&/^\[A-Za-z0-9\_-]{1,64}$/.test(i)){try{if(null!==sessionStorage.getItem(e+i))return}catch{return}o=!0,u(i,0)\}}).catch(()=>{})}function u(t,n){r||n>=30?o=!1:fetch("/edge-api/client-health/reload-request",{cache:"no-store",credentials:"omit"}).then(n=>{if(410!==n.status){if(!n.ok)throw new Error;try{sessionStorage.setItem(e+t,String(Date.now()))}catch{return void(o=!1)}location.reload()}else a()}).catch(()=>{setTimeout(()=>u(t,n+1),6e4)})}document.addEventListener("visibilitychange",l),i=window.setTimeout(d,5e3)}()(function(){function c(){var b=a.contentDocument||(a.contentWindow&\&a.contentWindow.document);if(b){var d=b.createElement('script');d.nonce='xBMcwCl/OY44bKLr4ZgWNw==';d.innerHTML="window.\_\_CF$cv$params={r:'a34de9585e975397',t:'MTc4ODM2Njc1NA=='};var a=document.createElement('script');a.nonce='xBMcwCl/OY44bKLr4ZgWNw==';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')\[0].appendChild(a);";b.getElementsByTagName('head')\[0].appendChild(d)\}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())\}}\}})();



####









vbb
