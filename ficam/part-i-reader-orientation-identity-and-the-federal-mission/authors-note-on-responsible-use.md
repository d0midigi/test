# Author's Note on Responsible Use



The offensive material presented throughout _Contested Terrain_ serves a simple purpose: identity infrastructure cannot be defended effectively when defenders do not understand how an adversary may attempt to manipulate it.

Active Directory, certificate services, federation, cloud identity, privileged-access systems, and the broader Federal Identity, Credential, and Access Management (FICAM) ecosystem are all built upon trust. That trust is expressed through credentials, permissions, attributes, certificates, authentication protocols, group memberships, delegation, administrative authority, and the relationships between, around, inside, and outside of systems. When those relationships are misunderstood, overextended, poorly governed, or inadequately monitored, they can become the same pathway an adversary may use to move through your environment.

The offensive techniques in this book are not presented as tricks to memorize or commands to reproduce indiscriminately. They are presented as a way to understand where, why, and how trust can fail.

Throughout my career, some of the most consequential security weaknesses I have encountered were neither dramatic software vulnerabilities nor malicious insiders misusing government-issued systems. They were ordinary configurations that had accumulated extraordinary authority. Service accounts appear frequently in this book for that reason. One of the first significant weaknesses I identified nearly two decades ago involved an IIS service account and, later, an Apache Tomcat service account that had been granted far more access than the mission required. The problem was not that the accounts existed. The problem was that its authority had expanded beyond anyone's comfort level - and beyond anyone's apparent view.

The same pattern appears in other forms: a legacy trust that remains long after its original mission purpose has disappeared; a Group Policy Object whose delegated permissions were never revisited; an administrative credential used across security tiers that no one can fully account for; or a synchronization service granted broad write authority during an integration effort and never reduced afterward.

Then there are the familiar institutional patterns: _“That is just the way it has always been done here,”_ and _“No one wants to touch it.”_ Those statements often signal that a configuration has outlived its documented purpose, its ownership, or its original risk decision. They do not establish that the condition remains safe. In identity infrastructure, an unexamined legacy dependency can retain authority long after the mission need that created it has disappeared.

These conditions must be understood.

Anyone adopting an attacker mindset—whether as an ethical hacker, security engineer, system administrator, incident responder, red team operator, or blue team defender—must learn to think before acting. As the saying goes, “A sword fight is like a game of chess; you must think first, before you move.” In identity security, that means anticipating the adversary’s next move before the adversary has fully developed it.

This is what I refer to as **critically creative thinking**.

Critically creative thinking means questioning assumptions, examining a condition from multiple perspectives, and resisting the bias that comes from accepting the first explanation that appears reasonable. It requires the practitioner to remain impartial long enough to understand both the defender’s intended design and the adversary’s likely interpretation of that design. It also requires creativity: looking at relationships, dependencies, and consequences from angles that others may overlook.

An adversary does not care whether a weakness originated in a sophisticated design decision, an emergency workaround, a legacy migration, a compliance exception, or a configuration that simply escaped review. The adversary cares about what the condition permits now.

Defenders must learn to think the same way.

That is why this book places offensive and defensive security beside one another. Understanding how to enumerate a permission should improve the reader’s ability to govern that permission. Understanding how Kerberos can be abused should improve the reader’s ability to engineer, monitor, and recover Kerberos. Understanding certificate-based escalation should change the way certificate templates and Certification Authorities are reviewed. Understanding paths into Tier 0 should influence how privileged administration, virtualization, backup, identity synchronization, and management infrastructure are designed.

The ability to perform a technique, however, does not create authorization to use it.

The procedures, tools, attack paths, and adversary-emulation methods discussed in _Contested Terrain_ are intended only for authorized security assessments, approved red- and purple-team operations, controlled laboratory environments, defensive validation, professional training, and legitimate security research. They must never be used against systems, identities, networks, applications, tenants, or infrastructure for which explicit authorization has not been granted.

This responsibility carries particular weight in federal and Department of Defense environments. Identity infrastructure may support mission-essential systems, classified and unclassified enclaves, coalition partners, contractors, external agencies, cloud services, cross-domain capabilities, and personnel whose ability to authenticate is itself operationally significant. An action that appears limited to one account or one server can propagate through directory replication, Group Policy, certificate trust, federation, synchronization, or another administrative dependency far beyond the immediate target.

Professional offensive security therefore requires more than technical capability. It requires judgment.

There will be situations throughout this book in which the technically complete version of an attack is appropriate in a laboratory but unnecessary—or inappropriate—in production. Demonstrating that an account possesses directory-replication rights may establish risk without extracting an entire domain’s credential material. Demonstrating control over a Group Policy Object may establish a path to domain-controller execution without deploying payloads to production domain controllers. Identifying a vulnerable certificate template may establish the possibility of identity impersonation without unnecessarily issuing a privileged certificate from a production Certification Authority.

Knowing when sufficient evidence has been obtained is part of the discipline.

The objective of offensive security is not to prove how much damage can be caused after the security consequence has already been established. The objective is to identify where trust can be subverted, demonstrate the condition convincingly, preserve meaningful evidence, and enable the environment to become more resilient.

Learn the offensive tradecraft in this book deeply. Build the laboratory. Intentionally break trust relationships in a controlled environment. Examine the tickets, tokens, permissions, certificates, credentials, and directory changes that result. Study the evidence from the defender’s perspective. Rebuild the environment. Harden it. Attempt the same authorized test again and determine whether the path is actually gone.

Then carry that reasoning into authorized operational environments.

The value of understanding how identity infrastructure can be compromised is not in knowing how to take control of it.

It is in recognizing the path before an actual adversary does.

\
\
<br>

<br>

<br>

<br>

\
<br>

<br>

<br>

<br>

\
<br>

\
\
\
<br>





\======================================

The offensive material presented throughout _Contested Terrain_ is included for a simple reason: identity infrastructure cannot be defended effectively if defenders do not understand how an adversary will attempt to manipulate it.

Active Directory, certificate services, federation, cloud identity, privileged-access systems, and the broader Federal Identity, Credential, and Access Management (FICAM) ecosystem are built on trust. That trust is expressed through credentials, permissions, attributes, certificates, authentication protocols, group membership, delegation, administrative authority, and relationships between systems. When those relationships are misunderstood, overextended, poorly governed, or inadequately monitored, they can become the same pathways an adversary uses to move through an environment.

The offensive techniques in this book are therefore not presented as tricks to memorize or commands to reproduce indiscriminately. They are presented as a method of understanding where trust can fail.

Throughout my career, some of the most consequential security weaknesses I have encountered were not dramatic software vulnerabilities, or personnel who were behaving in an unethical manner within their government issued PC or laptop. They were ordinary configurations that had accumulated extraordinary authority: you may see me refer to a "service account" in many of my examples, and that is because that was the first weakness I identified (an IIS service, and later an Apache Tomcat service) in the current DoD structure almost twenty years ago; however, a service account that had been granted too much access for comfortablility. A legacy trust that remained long after its original purpose disappeared; a Group Policy Object whose delegated permissions were never revisited, too an administrative credential that was used across security tiers that no one could account for.

It must be understood.

What also must be understood if adapting the attacker mentality as an ethical hacker, security professional, whatever hat you may wear, because as the great saying from The Lord from The Wu Tang and Shaolin: "a sword fight is like a game of chess; you must think first, before you move." This means you have to be anticipating your opponent, or the attacker in this context, next move before they even contemplate it themselves. This is what I refer to as critically creative thinking. It is thinking to where one questions everything. It is thinking where one looks at the event from all sides of the angle; it also means someone who can maintain neutrality (e.g., deflect bias), remain impartial to "both sides of a story." Creative because it means looking at it from other angles your opponent wouldn't think to look, or notice. It means being self-efficient in that a lot of times, sometimes the fix is a DIY. It's about being inventive, self-sufficient, curious, and motivated because an adversary does not care whether that condition originated from a sophisticated design decision, an emergency workaround, a migration performed years earlier, or a configuration that simply escaped review. The attacker cares about what the condition permits now.

You must learn to think the same way.

That is why this book deliberately places offensive and defensive security beside one another. Understanding how to enumerate a permission should improve the reader’s ability to govern that permission. Understanding how Kerberos can be abused should improve the reader’s ability to engineer and monitor Kerberos. Understanding certificate-based escalation should change the way certificate templates and Certification Authorities are reviewed. Understanding attack paths into Tier 0 should influence how privileged administration, virtualization, backup, identity synchronization, and management infrastructure are designed.

The ability to perform a technique, however, does not create authorization to use it.

The procedures, tools, attack paths, and adversary-emulation methods discussed in _Contested Terrain_ are intended for authorized security assessments, approved red and purple team operations, controlled laboratory environments, defensive validation, professional training, and legitimate security research. They should never be used against systems, identities, networks, applications, tenants, or infrastructure for which explicit authorization has not been granted.

This responsibility becomes particularly important in federal and Department of Defense environments. Identity infrastructure may support mission-essential systems, classified and unclassified enclaves, coalition partners, contractors, external agencies, cloud services, cross-domain capabilities, and personnel whose ability to authenticate is itself operationally significant. An action that appears limited to one account or one server may propagate through directory replication, Group Policy, certificate trust, federation, synchronization, or another administrative dependency far beyond the immediate target.

Professional offensive security therefore requires more than technical capability. It requires judgment.

There will be situations throughout this book where the technically complete version of an attack is appropriate in a laboratory but unnecessary or inappropriate in production. Demonstrating that an account possesses directory replication rights may establish the risk without extracting an entire domain’s credential material. Demonstrating control over a Group Policy Object may establish a path to Domain Controller execution without actually deploying payloads to production Domain Controllers. Identifying a vulnerable certificate template may establish the possibility of identity impersonation without unnecessarily issuing a privileged certificate from a production Certification Authority.

Knowing when sufficient evidence has been obtained is part of the discipline.

The objective of offensive security is not to prove how much damage can be caused after the security consequence has already been established. The objective is to identify where trust can be subverted, demonstrate the condition convincingly, preserve meaningful evidence, and enable the environment to be made more resilient.

So learn the offensive tradecraft in this book deeply. Build the laboratory. Break the trust relationships intentionally. Examine the tickets, tokens, permissions, certificates, credentials, and directory changes that result. Study the evidence from the defender’s perspective. Rebuild the environment. Harden it. Attempt the same attack again and determine whether the path is actually gone.

Then carry that reasoning into authorized operational environments.

The value of understanding how identity infrastructure can be compromised is not in knowing how to take control of it.

It is in recognizing the path before an actual adversary does.
