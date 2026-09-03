---
icon: rocket-launch
---

# NEW Chapter 7 - FICAM and FISCAM: From Identity Architecture to Audit Assurance

### Abstract

Chapter 7 introduces the slight variations and differences between Federal Identity, Credential, and Access Management (FICAM), which defines how federal identities, credentials, access, federation, and lifecycle governance should operate, and the Federal Information System Controls Audit Manual (FISCAM), which provides a methodology for determining whether supporting controls are properly designed, implemented, and operating effectively. This chapter connects those disciplines through an offensive and defensive identity-security lens. Rahter than treating audit evidence as proof of security, readers learn to challenge the assumptions behind account provisioning, privileged access, separation of duties, authentication, recertification, logging, change management, and deprovisioning. Each control area is examined from the perspective of both the defender engineering the control and the adversary attempting to bypass, misuse, or remain invisible within it using various methods such as Living-Off-The-Land (LOTL), persistence, obfuscation, impersonation, and masquerading. Attack pathways, shadow administrators, stale or dormant identities, lax authentication, excessive privilege, evidence gaps, and control circumvention demonstrate how a technically compliant environment can remain exploitable. The chapter ultimately establishes adversarial control validation as the bridge between identity architecture, audit assurance, continuous monitoring, and defensible federal cybersecurity.

### 7.1 Two Frameworks, One Security Question

Federal identity architecture and federal information-system auditing begin from different professional perspectives. FICAM is concerned with how an agency establishes, manages, authenticates, authorizes, federates, governs, and retires identities and credentials. FISCAM approaches the same environment from the perspective of control assurance: whether information-system controls are appropriately designed, implemented, and operating with enough reliability to support the objectives for which they exist.

The distinction between the two matters.

FICAM should not be reduced to an audit checklist, and FISCAM should not be treated as an identity architecture framework. They both answer fundamentally different questions.

In an operational environment, those questions eventually collide.

An agency may design an identity lifecycle that requires authoritative sponsorship, identity proofing, controlled provisioning, strong authentication, appropriate authorization, periodic review, and timely deprovisioning. Those are intended identity outcomes. The existence of a policy describing those outcomes does not demonstrate that they occur consistently in production.

Likewise, an auditor may determine that access requests are approved, privileged accounts are periodically reviewed, terminated users are sampled for timely removal, and authentication settings are documented. That evidence may establish something meaningful about control operation. It still does not prove that an adversary cannot reach the same authority through a delegated Access Control Entry (ACE), a forgotten service account, a certificate, an unmanaged local administrator relationship, a surviving cloud token, or a system capable of controlling the administrator.

This is where the offensive and defensive perspectives become essential.

The attacker does not ask whether the identity program has a mature lifecycle diagram.

Rather, the attacker asks:&#x20;

_"Where is the trust assumption wrong?"_

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

Chapter 6 established FICAM as an identity architecture and governance discipline rather than a collection of account-management procedures. At this stage, the reader should already understand identity establishment, credentialing, authentication, authorization, federation, lifecycle management, Person Entity, Non-Person Entity (NPE), identity assurance levels, and access gvoernance.

Chappter 7 does not aim to teach those concepts again.

Instead, FICAM becomes the source of security assertions that can be readily tested.

First, let us consider several examples:

* identites should originate from trustworthy authoritative sources;
* credentials should remain correctly bound to the identities to which they were issued;
* access should reflect legitimate mission need;
* privileged authority should remain appropriately constrained;
* federation should extend only the intended trust;
* credentials and access should be revoked when no longer authorized;
* Non-Person Entities (NPEs) should remain attributable to accountable owners; and,
* identity events should produce sufficient evidence for monitoring and investigation.

Each statement describes an intended condition.

The security problem begins when the intended condition andthe technically effective condition diverge.

Suppose an agency's identity process correctly disables a deeparting employee's Active Directory user account within minutes of separation. From a FICAM lifecycle perspective, an important action occurred.

An attacker asks a different set of questions, however.

_"Did the identity possess a still-valid authentication certificate?"_

_"Were active cloud sessions and refresh tokens revoked, or only the account disabled?"_

_"Did the user control an application registration, service principal, or workload identity?"_

_"Were privileged group memberships nested through another identity?"_

_"Did the person know a shared service credential?"_

_"Did a local administrator password remain unchanged?"_

_"Did the departing user own automation, scripts, keys, scheduled tasks, or service accounts that continue to operate?"_

_"Was a second account created outside the primary provisioning process?"_

_"Did the person hold a role in a system that does not consume the enterprise directory at all?"_

The attacker's purpose is not to argue that the account was not disabled. It was.

The attacker is testing whether account disablement accomplished the security objective everyone believes it accomplished.

That difference - between control activity and security outcome - is central to this chapter.

### 7.1.2 Federal Information System Controls Audit Manual (FISCAM)

FISCAM provides a disciplined means of examining information-system controls rather than relying on assertion alone. Its importance to this book is not that every identity engineer must become a security assessor. Its importance is that the security professionals benefit enormously from understanding how indpendent security assessors reason about control designs, implementation, evidence, effectiveness, deficiency, and reliance.

That mindset forces uncomfortable questions to arise.

_What exactly is the control?_

_Who performs it?_

_What population does it affect?_

_How frequently does it operate?_

_What evidence does it produce?_

_Can that evidence be independently corroborated?_

_What happens when the control fails?_

_Who is capable of overriding it?_

_Can the same person both perform the sensitive action and manipulate the evidence demonstrating that the action was appropriate?_

Those are audit questions.

They are also excellent defensive questions as well.

However, inverted, they become excellent offensive questions.

If the security assessor asks:

> What evidence demonstrates that all privileged access is approved?

The offensive operator asks:

> Which privileged pathways are absent from the population used to generate that evidence?

If the security assessor asks:

> Are terminated accounts disabled within the required period?

The attacker asks:

> Which authentication artifacts remain userful after the account has been disabled?

If the security assessor asks:

> Are administrative changes logged?

The attacker, in turn, asks:

> Which administrative pathway lets me produce the desired state without generating the expected evidence?

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

_"What should be true?"_

_"What is actually true?"_

The attacker cares almost exclusively about the second.

There is a third question that belongs to neither discipline alone, and it is the one this chapter is built around:

_What can be made true by someone who is not authorized to make it true?_

### 7.1.4 FICAM Defines Identity Outcomes

For purposes of this chapter, FICAM provides the intended identity state against which technical reality can be examined.

The operative word is _**intended**._

If an identity should be unique, attributable, appropriately proofed, correctly credentialed, granted only necessary access, and removed when its mission relationship ends, each of those characteristics creates something that can be tested.

The defensive engineer can ask:

_Can I prove the account originated from an authoritative workflow?_

_Can I trace sponsorship?_

_Can I determine every credential currently representing this identity?_

_Can I calculate its effective authority, including indirect paths?_

_Can I identify every system on which that identity has authenticated?_

_Can I determine who can modify the identity?_

_Can I determine who can replace its credential?_

_Can I determine which applications and services continue trusting it?_

Those questions transform identity governance from administrative process into observable security state.

The offensive operator asks nearly identical questions for a different purpose.

_Which identity lacks a reliable owner?_

_Which account was provisioned outside the normal workflow?_

_Which entitlement survived a role change?_

_Which credential can still represent a disabled identity?_

_Which administrator can be controlled indirectly?_

_Which service account has authority disproportionate to its visibility?_

_Which federation path accepts a weaker assertion than the architecture assumes?_

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

| Property     | Question                                      | Failure mode                                   |
| ------------ | --------------------------------------------- | ---------------------------------------------- |
| Completeness | Does the evidence cover the whole population? | Blind spot outside the query                   |
| Accuracy     | Does it reflect the actual technical state?   | Report generated from stale or cached data     |
| Timeliness   | Does it describe the period under review?     | Point-in-time snapshot missing interim changes |





####









vbb
