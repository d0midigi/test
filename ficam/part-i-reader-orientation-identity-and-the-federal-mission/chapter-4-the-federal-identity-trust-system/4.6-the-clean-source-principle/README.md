# ✔️ 4.6 The Clean Source Principle

{% hint style="info" %}
Administrative actions inherit risk from their workstations, credentials, software supply chains, and recovery sources.
{% endhint %}

_**TL;DR** Modern identity systems are deeply interconnected, and every weak dependency creates an attack path - no matter how strong any single platform appears. The Clean Source Principle and BloodHound OpenGraph make these hidden relationships visible, empowering defenders to treat Attack Path Management as an ongoing discipline rather than a one-time project._

### 4.6.1 Introduction to the Active Directory Clean Source Principle (CSP)

Identity security is often discussed as though trust begins when a user enters a credential and ends when an access-control decision is returned. That view is much too narrow for a federal Active Directory environment. A domain controller may accept only approved administrative identities, require phishing-resistant authentication, enforce hardened Group Policies, and reside behind tightly controlled network boundaries, and the domain can still be lost if those administrators reach it from systems an adversary already owns.

The reason is straightforward: administration is itself a trust relationship.

This also proposes a deceptively simple rule: _all security dependencies must be as trustworthy as the object being secured;_ however, this simple rule is violated constantly in modern enterprise environments. These violations are what give rise to attack paths.

When one system is allowed to configure, repair, monitor, virtualize, back up, deploy software to, image, attest, or otherwise control another system, the security of the target becomes dependent upon the security of the administrative source. The target may never explicitly identify that source as a trusted identity provider. Operationally, it has granted that source something more consequential - the ability to alter its state.

This produces one of the most important architectural rules in privileged-access design:

> **A system must not be administered from a security context less trustworthy than the system being administered.**

This is the Clean Source Principle.

<figure><img src="../../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure>

The word _source_ should be interpreted broadly, however. It includes the workstation from which an administrator connects. It also includes management servers, automation platforms, deployment systems, virtualization infrastructure, baseboard management controllers, backup consoles, software repositories, administrative scripts, recovery media, security tooling, credentialed vulnerability scanners, directory synchronization servers, and any other mechanism capable of introducing state into the protected production environment.

This matters most at Tier 0. Active Directory does not remain trustworthy simply because the domain controllers and Group Policy Objects (GPOs) are hardened. The administrative ecosystem surrounding those domain controllers and GPOs must be trustworthy as well. If a lower-trust management system can alter a high-level domain controller, deploy code to it, recover its filesystem, read its memory, retrieve its secrets, issue certificates it will honor, or impersonate an administrator who actively manages it, that management system has already crossed into the identity control plane whether or not anyone formally classified it there.

The clean source principle changes the question from:

_"Is the domain controller secure?"_

to:

_"What must an adversary compromise to cause this domain controller to trust attacker-controlled infrastructure or state?"_

The second question reveals the architecture that absolutely matters.

> #### **Did You Know?**
>
> The clean source principle originated in Microsoft's Privileged Access Workstation and Enhanced Security Administrative Environment (ESAE, informally the "Red Forest") guidance. Microsoft retired the ESAE hardened-forest pattern as a general recommendation in 2020 and folded the underlying principle into the Enterprise Access Model and its privileged access rapid modernization guidance. Federal and DoD documentation lags that change by years. You will still encounter system security plans, contract deliverables, and architecture review boards that reference ESAE as current doctrine or that treat "we built a Red Forest" as the end-state. The forest was never the primary source of control. The clean source principle was, and it survived the pattern that popularized it.

In today’s security discourse, phrases like _“identity is the new perimeter”_ are often repeated as though they capture the whole story. They suggest that if an organization hardens its identity provider, deploys MFA, and centralizes authentication, it will have contained its risk. The reality is far more complicated.

Identities never exist in isolation. They are embedded in a web of devices, platforms, agents, and other identities. These relationships, often hidden, sprawling, and poorly understood, are what adversaries exploit to move through an environment. A system may appear well-secured on its own, but if it inherits trust from another weaker system, it is vulnerable.

Most agencies do not realize the depth of their interconnections. They may invest heavily in hardening one platform, only to leave open attack paths through another. Without visibility into how dependencies actually link together, security leaders and enterprise defenders are left managing fragments of risk rather than the whole picture.

The Clean Source Principle provides a unifying way to understand these risks. Violations of the principle are what make modern attack pathways possible. By examining how dependencies span across platforms and compound through transitive relationships, we can see why conventional strategies fall short, and why graph-based analysis is essential to bring these hidden risks into view. To illustrate this, let’s begin with a simple but powerful case study: how the security of a GitHub repository can be silently chained to platforms its administrators never intended to trust.

### **4.6.2 Case Study: GitHub’s Hidden Dependencies**

Consider a GitHub Enterprise environment hosting an organization’s most sensitive intellectual property. Imagine a private repository containing unreleased source code or proprietary algorithms. At first glance, it appears to be a simple access control problem: secure the repository by tightly managing who has permissions.

For this example, we’ll use **BloodHound’s new OpenGraph capability** to visualize the configuration as we discuss it.

### **4.6.3 The Repository in Isolation**

**The repository appears to stand alone, protected only by the permissions assigned by administrators.**

<figure><img src="../../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

### **4.6.4 Mapping GitHub Access**

Expanding outward reveals the GitHub users and teams who have access. Some accounts may have read permissions, others write, and a few may hold administrative control. The repository is no longer an isolated object; it is part of a web of relationships where each user or team becomes a potential dependency.

<figure><img src="../../../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>

### **4.6.5 Revealing External Identities**

Many of those GitHub accounts authenticate through an external identity provider such as Entra ID via SSO. Once those relationships are revealed, the dependency becomes clear: GitHub’s security is directly tied to the security of Entra.

<figure><img src="../../../.gitbook/assets/image (7).png" alt="" width="563"><figcaption></figcaption></figure>

Here, the Clean Source Principle comes into focus: **GitHub is only as secure as the identity provider it depends on.** If the IdP is compromised, so too are the GitHub accounts federated to it and by extension, the repositories they control.

### **4.6.6 Escalation: Entra Depends on Active Directory**

At this point, we’ve shown that GitHub’s security is chained to Entra’s security through single sign-on. But the chain rarely stops there.

In many enterprises, Entra is not an independent identity system. Entra users are often synchronized from on-premises Active Directory. This means that a compromise of an AD account can cascade upward into Entra, and from there into GitHub.

<figure><img src="../../../.gitbook/assets/image (8).png" alt="" width="563"><figcaption></figcaption></figure>

The picture is now clear:

* GitHub’s security depends on Entra.
* Entra’s security depends on Active Directory.
* Therefore, GitHub’s security also depends on Active Directory.

This is the essence of a **transitive security dependency**. The administrator of the GitHub repository may never think about Active Directory when assigning access, but in practice the security of their most sensitive repository is only as strong as the related Active Directory domain.

### **4.6.7 The Probability Problem: Assume Breach** <a href="#the-probability-problem-assume-breach" id="the-probability-problem-assume-breach"></a>

A thoughtful CISO might still push back: surely compromise of the one specific AD user synced to Entra is unlikely. Unfortunately, the data tells a different story.

In real-world Active Directory Security Assessments (ADSAs) and CORA readiness inspections, by deploying BloodHound Enterprise across hundreds of environments, a striking pattern emerges: in roughly **95% of enterprises**, the Domain Users group has an attack path to Tier Zero. In plain terms, virtually _every_ user in the domain has some path, often short and exploitable, to compromise the entire AD forest.

<figure><img src="https://specterops.io/wp-content/uploads/sites/3/2025/10/image_5ab9b7.png?w=1024" alt=""><figcaption></figcaption></figure>

This means that if attackers can compromise _any_ AD user, they can find a path to _every_ AD user. And because Entra identities are frequently synced from AD, compromise of AD translates directly into control of Entra accounts.

Even more concerning, we often find that **highly privileged Entra accounts are synced from non-privileged AD accounts.** From a Clean Source Principle perspective, this is a glaring violation: a weak, low-value AD account inherits the power to control an administrative identity in Entra. In this scenario, the attacker doesn’t even need to escalate to Tier Zero, compromise of a relatively unprivileged AD user may be enough to seize control of a global administrator in Entra, and from there, access to critical GitHub repositories.

Once inside Entra, the attacker inherits all the relationships we saw earlier. If an Entra user is linked to a GitHub account with write or administrative access to a sensitive repository, the repository is effectively compromised. This is why the **Assume Breach** paradigm matters: defenders must act as though an arbitrary AD user _will_ be compromised at some point. When that assumption holds, the attack path to the GitHub repository is not a remote edge case, it is a certainty waiting to be exploited.

### **4.6.8 Addressing Common Objections**

_**"We're cloud-native. We don't have AD."**_

A small minority of organizations have escaped Active Directory altogether, usually because they were born recently in the cloud era. But even those organizations are not exempt from the Clean Source Principle.

Cloud-native enterprises almost always centralize trust into a single identity provider such as Okta, Entra, or Ping. This creates the same class of dependency problem: GitHub, or any other SaaS platform, is only as secure as the IdP it federates to. From a CIA triad perspective, SSO consolidates availability, integrity, and confidentiality risks into a single point of failure.

Escaping AD does not mean escaping dependencies. It only means that the dependency graph has shifted.

_"We've implemented Zero Trust."_

Zero Trust is another common defense offered by security leaders. The problem is that the term is overloaded, it can mean anything from “we enforce MFA at login” to “we bought a vendor suite marketed as Zero Trust.” In practice, Zero Trust does not eliminate hybrid attack paths, for four reasons.

* **The user access layer is highly interconnected.** At Black Hat, SpecterOps researchers released _JamfHound_, and we are currently developing an Intune extension for OpenGraph. These efforts demonstrate that even in “Zero Trust” environments, device management systems themselves create new webs of trust relationships.
* **Segmentation without visibility is a paper exercise.** Customers who worked with Microsoft to implement Tiered Administration later used BloodHound to validate their approach with troubling results.  First, many attack paths were still present despite these efforts simply due to a lack of visibilty. They were working in the blind.  Second, small user permission modifications here and there combined to further erode the tiers that took over a year to put in place.   &#x20;
* **Identities in transit reconnect what segmentation attempts to divide.** Cloud services must still be accessed from user devices. Sessions cached on those devices can be stolen to bypass MFA and other controls.

The net result: Zero Trust may constrain certain avenues of compromise, but it does not dissolve the transitive dependencies that generate hybrid attack paths.

_"We're migrating away from AD."_

This is another familiar refrain: AD is a legacy anchor, but in 12–18 months, it will be gone. In our experience, this rarely happens. AD’s gravitational pull is too strong, too many applications and devices are entangled with it.

Even for the few agencies that succeed in reducing their AD footprint, the fundamental problem does not disappear. It simply reconstitutes itself in other platforms. Intune, Jamf, Okta, and Ping all step into the same role that AD once played, becoming new hubs of centralized trust.At the end of the day, users will still have devices. Devices will still be compromised through phishing or client-side attacks. And those devices will still bridge access to identity providers. No matter what technology stack governs them, **attack paths are inevitable when dependencies are invisible.**

### **4.6.9 The Broader Lesson: Security Dependencies Are Eternal** <a href="#the-broader-lesson-security-dependencies-are-eternal" id="the-broader-lesson-security-dependencies-are-eternal"></a>

The GitHub → Entra → Active Directory example is just one illustration of a larger truth: **modern environments are built on layers of dependency, and those dependencies inevitably leak trust.** Attack paths are not anomalies, they are symptoms of this structural reality.

It helps to think about these dependencies on two levels:

* **Intra-platform dependencies** exist inside a single system.
  * In Active Directory, the relationship between Domain Users and Tier Zero assets creates predictable attack paths.&#x20;
  * In GitHub, team structures and repository permissions can unintentionally grant excessive control.
* **Inter-platform dependencies** span across systems. GitHub federating to Entra, Entra syncing from AD, or Jamf enforcing policies on Mac workstations are all examples. These connections multiply the attack surface, because the security of one platform now inherits the weaknesses of another.

And here lies the uncomfortable insight: **the combination is more dangerous than either system in isolation.** An Active Directory environment riddled with attack paths is dangerous. A GitHub organization with overly broad permissions is dangerous. But when GitHub becomes dependent on AD through Entra, the risk compounds.

The Clean Source Principle tells us that if a dependency is weaker than the object it secures, an attack path exists. Intra-platform and inter-platform dependencies both violate this principle, and adversaries exploit both. What makes inter-platform dependencies especially dangerous is that they are often invisible to the teams who own each platform. A GitHub administrator may never realize their repository’s security hinges on an AD user they’ve never heard of.

The lesson is stark: dependencies are eternal. Active Directory may shrink, Intune or Okta may grow, Jamf may dominate in MacOS environments, but the attack paths will keep re-emerging wherever dependencies are hidden or misaligned. The only way to manage identity risk is to make these dependencies visible, across and within platforms, and to continually validate that the Clean Source Principle is not being violated.

### **4.6.10 OpenGraph as the Future-Proof Strategy** <a href="#opengraph-as-the-future-proof-strategy" id="opengraph-as-the-future-proof-strategy"></a>

BloodHound was originally built to map Active Directory. That model exposed a reality defenders had long suspected but could never fully prove: nearly every AD environment is saturated with attack paths. For years, that visibility alone transformed how enterprises understood identity risk.

But the most critical risks are no longer contained within a single platform. They emerge in the **spaces between platforms**; GitHub federating to Entra, Entra syncing from AD, Jamf enforcing policy on Mac devices, Okta brokering authentication across SaaS. These hybrid paths are what turn isolated weaknesses into enterprise-wide compromise.

This is why we built **BloodHound OpenGraph**. OpenGraph extends BloodHound beyond AD, allowing defenders to model _any_ platform, capture its internal access control model, and then connect it to the systems around it. Whether you are running Intune, Jamf, Ping, Okta, or GitHub Enterprise, the same principle applies: your security is only as strong as the platforms you depend on, and those dependencies can be visualized, queried, and managed in the graph.

The key differentiator is not just the ability to add new platforms, but the ability to see **hybrid attack paths**. Hardening AD alone or tightening GitHub permissions alone is insufficient if the platforms are chained together. The combination is more dangerous than either in isolation. OpenGraph allows defenders to surface those chains, understand their full impact, and prioritize breaking the most dangerous paths first.

Most importantly, OpenGraph is a **future-proof strategy**. The leviathan of today may be Active Directory; tomorrow it may be Intune, Okta, or something yet to emerge. But the problem is eternal: security dependencies accumulate, and attackers will always exploit them. By abstracting the platform and focusing on the relationships between systems, BloodHound ensures defenders will never be left blind to the next identity core.

### 4.6.11 Administration Is a Directed Trust Graph

The clean source principle is easier to apply when it is treated as a graph problem rather than a policy statement.

Draw a node for every system, identity, and artifact in scope. Draw a directed edge from **A** to **B** whenever A can change what B is or what B believes. The edge is what truly matters here, not the label on either node.

Edges take a small number of recognizable forms:

* **Code execution -** A can run code on B, in any security context that matters.
* **Configuration authority -** A can change B's policy, registry, security settings, or applied Group Policy.
* **Secret recovery -** A can read B's credentials, keys, memory, or storage.
* **State restoration -** A can replace B's disk, system state, snapshot, or image.
* **Software supply -** A can change what B installs or executes.
* **Identity issuance -** A can mint, sign, or alter credentials B will accept.
* **Platform control -** A can control the firmware, hypervisor, or hardware beneath B.
* **Human control -** A can direct, coerce, impersonate, or compromise the people who administer B.

Once the edges are drawn, tiering becomes a reachability question. Any node with a directed pathway into a Tier 0 asset is effectively part of Tier 0, whatever its product category, whatever its budget line, whatever the agency's organizational chart says.

```
                     ┌──────────────────────────┐
                     │   TIER 0 CONTROL PLANE   │
                     └──────────────────────────┘
                                  ▲
        ┌────────────┬────────────┼────────────┬────────────┐
        │            │            │            │            │
    code exec    config auth  secret recov  state rest   ident issue
        │            │            │            │            │
   ┌────┴────┐  ┌────┴────┐  ┌────┴────┐  ┌────┴────┐  ┌────┴────┐
   │  MECM/  │  │   GPO   │  │ Backup  │  │Hypervisor│ │ AD CS / │
   │ Deploy  │  │ SYSVOL  │  │  Vault  │  │  / BMC   │ │ Fed IdP │
   └────┬────┘  └────┬────┘  └────┬────┘  └────┬─────┘ └────┬────┘
        │            │            │            │            │
        └────────────┴─────┬──────┴────────────┴────────────┘
                           │
                  ┌────────┴────────┐
                  │  ADMIN ENDPOINT │  ← the source that decides
                  │   (PAW or not)  │     whether any of it holds
                  └────────┬────────┘
                           │
                  ┌────────┴────────┐
                  │ ENDPOINT MGMT / │  ← who manages the PAW?
                  │ IDENTITY / MFA  │     answer that or the
                  └─────────────────┘     chain is decorative
```

A **trust inversion** exists wherever an upstream node retains an edge into a protected asset while receiving weaker protection than the asset it can reach. Trust inversions are the shape attackers look for, because they route around the strongest control instead of confronting it.

Two properties of this graph are worth stating plainly.

**Trust is not transitive in the direction people assume.** Hardening a domain controller does not harden the systems that administer it. Authority flows downward from the source, like a waterfall; assurance does not flow upward from the target.

The graph is larger than the diagram. Network diagrams show packets. Control graphs show authority. A backup agent that never appears on a network diagram because it uses an existing management VLAN still holds a state-restoration edge into every host it protects.

### 4.6.12 A System Cannot Be Administered Safely From a Less-Trusted System

Consider a Domain Admin using an ordinary enterprise workstation to administer a domain controller.

The workstation may have no direct permissions over Active Directory. It may sit in a user-device Organizational Unit (OU), receive workstation security policy, and be managed by an endpoint support team with no formal Tier 0 responsibilities. On an architecture diagram, the separation looks reasonable.

Then the Domain Admin signs into that workstation.

The security relationship has constructively changed.

The workstation now processes the Domain Admin's authenntication material, Kerberos tickets, Remote Desktop connections, PowerShell command history, clipboard contents, administrative scripts, saved MMC consoles, and every other artifact associated with that Domain Admin's privileged activities on the domain. Malware executing with sufficient authority on that workstation does not need to attack the domain controller directly anymore. Rather, it will attack the Domain Admin before the Domain Admin reaches the domain controller.

That inversion is fundamental to credential theft.

The adversary does not move upward by defeating the strongest system first. The more efficient pathway is usually to compromise a weaker system and wait for stronger authority to arrive.

A compromised administrative source can effectively:

* capture credentials before submission, through keystroke captures, credential-provider tampering, sniffing the wire, or a spoofed elevation prompt;
* steal or replay authentication artifacts after successful authentication - Kerberos TGTs and service tickets, NTLM material, access tokens, and cached certificates;
* alter scripts, modules, or administrative commands between authoring and execution;
* modify binaries, PowerShell modules, or DLLs loaded during administration;
* tamper with Remote Desktop, PowerShell Remoting (PSR), browser, or management sessions in flight;
* manipulate DNS, proxy, certificate trust, or connection information presented to the administrator, sending trusted commands to an attacker-controlled destination;
* capture sensitive output returned from the target, including secrets displayed during troubleshooting;
* introduce malicious configuration through legitimate administrator activity;
* register a device, enroll a certificate, or bind an authenticator using the administrator's active session; or,
* use the administrator's existing authority without ever recovering the underlying password.

Strong authentication does not solve this.

A Personal Identity Verification (PIV) card, Common Access Card (CAC), FIDO2 authenticator, or hardware-backed private key makes credential duplication substantially more difficult. None of them guarantee that the operating environment invoking the credential is indeed trustworthy. An adversary who controls the workstation after authentication abuses the authenticated session rather than stealing the hardware-protected secret. The card stays in the reader and works exactly as designed, on the attacker's behalf.

This becomes more important as agencies and commands move toward phishing-resistant authentication under OMB M-22-09. Stronger authenticators close one class of attack. They do not, however, remove the requirement for a trustworthy administrative endpoint. An agency that has completed its phishing-resistant MFA milestone and still administers Tier 0 from general-purpose desktops has changed which attack works, not whether one does.

> #### Warning - Smart Card Required Does Not Mean No Password
>
> Enforcing Smart Card Required for Interactive Logon (SCRIL) on a privileged account does not remove that account's NT hash. Enabling SCRIL causes the directory to generate a random password, and unless expiration is configuraed that hash may never change again. A hash that never rotates is a hash that survives every credential-rotation exercise you run.\
> \
> In a domain at a Windows Server 2016 functional level or higher, enable rolling of expiring NTLM secrets by setting `msDS-ExpirePasswordsOnSmartCardOnlyAccounts` to `TRUE` on the domain object so SCRIL account hashes rotate on the normal password-expiration cycle.
>
>
>
> ```powershell
> # Verify domain functional level first — 2016 (7) or higher required
> (Get-ADDomain).DomainMode
>
> # Enable rolling of expiring NTLM secrets for SCRIL accounts
> Set-ADDomain -Identity (Get-ADDomain).DistinguishedName `
>   -Replace @{ "msDS-ExpirePasswordsOnSmartCardOnlyAccounts" = $true }
>
> # Confirm which privileged accounts are SCRIL-enforced
> Get-ADUser -Filter 'SmartCardLogonRequired -eq $true' `
>   -Properties SmartCardLogonRequired, PasswordLastSet, MemberOf |
>   Where-Object { $_.MemberOf -match 'Domain Admins|Enterprise Admins|Administrators' } |
>   Select-Object SamAccountName, PasswordLastSet
> ```
>
> \
> A `PasswordLastSet` value several years old on a SCRIL-enforced Tier 0 account is a critical finding, not a curiosity.

Several platform controls narrow the endpoint problem without actually solving it:

| Control                     | What it addresses                                                                     | What it does not address                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Credential Guard (VBS)      | Isolates NTLM hashes, Kerberos TGTs, and cached domain credentials from the OS kernel | Live session abuse; anything the logged-on user can already do                                                 |
| Remote Credential Guard     | Keeps credentials on the client during RDP; requests are proxied back                 | A compromised **client** - the attacker rides the session                                                      |
| RDP Restricted Admin Mode   | Prevents credentials from landing on the target                                       | Introduces network-logon-style exposure; the session hash becomes unusable for Pass-the-Hash **to** the target |
| Protected Users Group       | Blocks NTLM, DES, RC4, WDigest, CredSSP delegation; 4-hour-non-renewable TGT          | Compromise of the machine the member logs onto; application compatibility casualties                           |
| Windows LAPS                | Removes shared local administrator passwords across the estate                        | Anything holding read rights on the LAPS attributes on Entra-stored secrets                                    |
| Authentication Policy Silos | Restricts where a Tier 0 account may authenticate from                                | Systems already inside the silo boundary                                                                       |

Read that table as a set of narrowing measures, not as a stack that adds up to assurance. Each one removes a technique. None removes the dependency.

A Privileged Access Workstation (PAW) / Secured Administrative Workstation (SAW) exists for the dependency. Its value does not come from being called a PAW/SAW. The value comes from deliberately reducing the number of people, applications, management systems, browsing sessions, communication tools, software packages, and lower-trust administrative mechanisms capable of influencing the platform from which privileged authority originates.

A PAW/SAW managed by the same unrestricted endpoint-management system as every ordinary workstation fails the clean source test.

A hardened jump host reached from already-compromised endpoints fails it as well.

A PAW/SAW whose administrator checks email, opens a browser to a public site, or joins a video call on the same device has reintroduced the population of untrusted inputs the device existed to exclude.

The label is irrelevant. The dependency graph decides.

### 4.6.13 Administrative Dependencies Inherit the Target's Security Tier

Administrative tiering is frequently misunderstood as a classification applied only to user accounts.

Domain Admin is Tier 0. Server Admin is Tier 0. Workstation Admin is Tier 2.

That is incomplete.

Tiering must follow effective control.

Suppose a software deployment platform can execute arbitrary code as `SYSTEM` on every domain controller. The platform's administrators may not be Domain Admins. Their accounts may never appear in the Domain Admins group. They may hold no permission to open the Active Directory Users and Computers (ADUC) administrative console.

None of that changes what their systems can do, however.

If they can deploy arbitrary code to a domain controller, they can cause code to execute in a security context from which directory credentials, directory state, or domain-level authority can be obtained. The management platform possesses a direct pathway straight into Tier 0 territory.

Architecturally, it is Tier 0.

The following table catalogs the dependencies that most often turn out to hold Tier 0 authority in federal and DoD environments, along with the edge that puts them there.

| Dependency                                                                       | Edge into Tier 0                                                        | Why it is missed                                                      |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Endpoint/configuration management (MECM, Intune, Ansible, Puppet, Salt           | Code execution as `SYSTEM` on DCs                                       | Owned by an operations team, not security                             |
| Virtualization platform and its management server                                | Platform control - disk mount, memory inspection, snapshot              | Treated as "infrastructure," not identity                             |
| Baseboard management controllers (iDRAC, iLO, IPMI, BMC) and KVM-over-IP         | Platform control beneath the OS                                         | Frequently on a "maintenance" VLAN with default or shared credentials |
| Backup platform holding DC system state                                          | State restoration; offline `NTDS.dit` and `SYSTEM` hive                 | Classified by data availability, not authority                        |
| Enterprise Certificate Authority (CA) / AD CS                                    | Identity issuance - certificates the DC will honor                      | PKI treated as a separate discipline                                  |
| Credentialed vulnerability scanning (ACAS/Tenable, SCAP, Nessus, Qualys, Retina) | Stored privilege credentials plus authenticated access to every host    | Owned by compliance; credentials often over-privileged                |
| Endpoint security console (ESS/Trellix ePO/HBSS, EDR / XDR / NDR platforms)      | Remote response actions, arbitrary command executions                   | Its authority is a security feature, so nobody audits it              |
| Patch infrastructure (WSUS, repository shares, update pull/push mirrors)         | Software supply into Tier 0                                             | Unauthenticated HTTP WSUS is still found in production                |
| Privileged access management vault and session broker                            | Secret recovery for every Tier 0 credential it holds                    | Bought as a compensating control, becomes the crown jewel             |
| Third-party AD management and auditing tools                                     | Configuration authority, often via a highly privileged service account  | Service account privilege is set during install and never revisited   |
| Directory synchronization (Entra Connect, Cloud Sync, PTA agents)                | the on-prem/cloud boundarySecret recovery and identity issuance across  | Sits at a boundary that neither team fully owns                       |
| Group Policy and `SYSVOL` write access                                           | Configuration authority and code execution on every host in scope       | Delegation drifts over a decade of OU restructuring                   |
| DNS and authoritative time                                                       | Service location and Kerberos validity                                  | Considered plumbing                                                   |
| Monitoring and log-forwarding agents with remote-execution features              | Code execution                                                          | Installed everywhere by definition                                    |

Two secrets deserve individual attention, because both are recoverable from dependencies in that table and both are routinely omitted from Tier 0 inventories:

**The `krbtgt` account's keys.** Anyone able to read a domain controller's `NTDS.dit` offline - from a backup, a snapshot, a mounted virtual disk, or an unencrypted replica - holds the material required to forge Kerberos tickets for any principal in the domain, indefinitely, until `krbtgt` is reset twice with sufficient 10-hour separation.

**The domain DPAPI backup key.** The domain's DPAPI backup key (`BCKUPKEY`) allows decryption of DPAPI-protected secrets belonging to any domain user in the forest - saved browser credentials, certificates with exportable private keys, scheduled task passwords, and stored RDP credentials. It is recoverable from a domain controller and from a system-state backup of one. Unlike a password, it cannot be rotated without consequence, and most agencies have never rotated it.

Neither secret is protected by hardening the domain controller if a Tier 1 backup platform can read the disk.

The same reasoning extends to any domain-joined system able to reach Tier 0 through the edges described in 4.6.1. This inheritance is exactly why Tier 0 is consistently larger than expected.

An agency may begin with a diagram showing four domain controllers and six Domain Admin accounts. After administrative dependencies are mapped, the trusted core includes virtualization clusters, backup servers and networks, certificate authorities, privileged workstations, management platforms, security and administrative consoles and interfaces, scanning appliances, out-of-band management interfaces, automation accounts, software repositories, and the administrators responsible for each.

That discovery is not a failure of tiering. t is the purpose of the exercise.

The dangerous condition is not that Tier 0 is larger than expected. The dangerous condition is having Tier 0 dependencies nobody recognizes as Tier 0.

Hidden Tier 0 creates ungoverned authority.

Once an administrative dependency has been identified as part of the identity control plane, its security requirements must reflect the authority it carries. That affects who administers it, where those administrators authenticate primarily, which systems may connect to it, how software is introduced, how credentials are stored, which telemetry is collected, how it is assessed under the Risk Management Framework (RMF), and how it is recovered after compromise.

The security tier belongs to the capability, not the product category.

A backup server is not inherently Tier 0.

A backup server capable of restoring `NTDS.dit`, the `SYSTEM` hive, certification authority private keys, or an entire domain controller is.

A hypervisor is not inherently Tier 0.

A hypervisor capable of mounting the disks or inspecting the memory of Tier 0 virtual machines is.

An endpoint security console is not inherently Tier 0.

A console able to run arbitrary commands as `SYSTEM` on domain controllers is.

A vulnerability scanner is not inherently Tier 0.

A scanner storing credentials that authenticate to domain controllers is.

The clean source principle makes these relationships visible because it forces the architect to follow authority backward toward every system capable of originating trusted administrative change.

### 4.6.14 Credential Entry Creates Trust Relationships

Credential placement is one of the most overlooked forms of architectural trust.

When a privileged identity authenticates to a system, that system becomes part of the credential's exposure surface.

This remains true even when the system is not intended to administer the identity infrastructure.

Suppose a Tier 0 administrator signs into a Tier 1 application server to troubleshoot a problem. The administrator intends to perform one task and disconnect five minutes later. From the perspective of the identity architecture, something more significant has occurred: Tier 0 authentication material has entered into a Tier 1 security boundary.

Depending on the authentication method being used, operating-system configuration, remote-management protocol, and platform protections, the destination may gain access to some combination of:

* Kerberos Ticket Granting Tickets (TGT);
* Kerberos service tickets;
* NTLM-derived authentication material;
* access tokens available for impersonation;
* delegated credentials, where delegation is permitted;
* Remote Desktop session artifacts and reconnect state information;
* certificate-backed authentication contexts and cached PKINIT material;
* browser, cloud, or federation session cookies; or,
* other reusable authentication state.

The administrator has effectively told the identity architecture, _"I trust this machine enough to process my Tier 0 identity."_

If the machine is already compromised, the attacker easily inherits that same trust.

This is why privileged-access architecture must examine where credentials _can appear_, not merely where administrators are _supposed to work_.

It also explains the importance of authentication restrictions. Protected Users, Authentication Policies, Authentication Policy Silos, Remote Credential Guard, privileged workstation designs, and tier-specific logon restrictions all address different portions of the same problem: reducing the number of systems effectively allowed to become custodians of high-value authentication material.

The logon-rights matrix is the blunt instrument here, and it works. Three Group Policy Objects, linked to the OUs holding each tier's computer objects, deny the wrong tiers the ability to authenticate:

| GPO linked to                                          | Deny these accounts                                                   | Rights denied                                            |
| ------------------------------------------------------ | --------------------------------------------------------------------- | -------------------------------------------------------- |
| Tier 0 computers (DC OU, Tier 0 server OU, PAW/SAW OU) | Tier 1 and Tier 2 administrative accounts, all standard user accounts | Interactive, Remote Interactive, Network, Batch, Service |
| Tier 1 computers (member server OUs)                   | Tier 0 accounts, Tier 2 administrative accounts                       | Interactive, Remote Interactive, Network, Batch, Service |
| Tier 2 computers (workstation OUs)                     | Tier 0 accounts, Tier 1 administrative accounts                       | Interactive, Remote Interactive, Network, Batch, Service |

Denying Tier 0 accounts on lower-level tiers is the half that gets skipped, and it is also the exact half that stops credential theft. Blocking downward logon is what prevents a Domain Admin from depositing a TGT on a workstation during a "quick" troubleshooting session.

**Authentication Policy Silos** enforce the same boundary in the directory rather than on the endpoint, which means the restriction travels with the account instead of depending on correct GPO scoping:

```powershell
# Create the silo that will contain Tier 0 accounts, hosts, and service accounts
New-ADAuthenticationPolicySilo -Name "Tier0-Silo" `
  -Enforce:$true `
  -Description "Tier 0 control plane — DCs, PAWs, Tier 0 services"

# Policy: Tier 0 users may only obtain a TGT from members of the Tier0-Computers group.
# TGT lifetime is capped at 240 minutes and the TGT is non-renewable.
New-ADAuthenticationPolicy -Name "Tier0-UserPolicy" `
  -Enforce:$true `
  -UserTGTLifetimeMins 240 `
  -UserAllowedToAuthenticateFrom `
    "O:SYG:SYD:(XA;OICI;CR;;;WD;(@USER.ad://ext/AuthenticationSilo == `"Tier0-Silo`"))"

# Bind the policy to the silo, then assign accounts and computers to the silo
Set-ADAuthenticationPolicySilo -Identity "Tier0-Silo" -UserAuthenticationPolicy "Tier0-UserPolicy"
Grant-ADAuthenticationPolicySiloAccess -Identity "Tier0-Silo" -Account "svc-t0-admin"

# Silos require Kerberos armoring (FAST). Verify it is enabled domain-wide before enforcing,
# or Tier 0 administrators will be locked out of their own control plane.
Get-GPResultantSetOfPolicy -ReportType Xml -Path .\rsop.xml   # inspect KDC armoring settings
```

> #### Warning - Silos Fail Closed
>
> Authentication Policy Silos require Kerberos armoring, knwon as FAST, a Windows Server 2012 R2 or higher domain functional level, and correct membership of both accounts _and_ computers. Enforcing a silo before every Tier 0 host is a member produces an outage in the one part of the environment that has no pathway to recovery except the credentials you just blocked. Deploy in audit mode, review Event IDs 4820, 4821, 4822, and 4823, and enforce only after the audit log is clean. Keep a break-glass account outside the silo, in a safe, on paper.

From an offensive perspective, credential placement turns host compromise into opportunity.

A compromised workstation appears strategically unimportant until a server administrator logs onto it. A compromised management server becomes considerably more valuable when a domain administrator authenticates during a troubleshooting session. An adversary who understands operational behaviors may choose not to move at all. Waiting for privileged credentials to cross an existing trust boundary is quieter and more reliable than attacking Tier 0 directly, and it generates telemetry that looks exactly like administration, because it is administration.

From the defensive perspective, this suggests an inversion of ordinary credential monitoring.

Do not ask only:

_"Where are our privileged accounts?"_

Ask:

_"Where have those accounts authenticated?"_

Those are not the same inventory.

One describes identity ownership.

The other describes identity exposure.

### 4.6.15 The Hybrid Control Plane Travels in Both Directions

Nothing in the preceding sections assumed the control path stays on-premises. In practice it rarely does, and hybrid identity produces the trust inversions that federal environments discover last.

Directory synchronization is the clearest case. The server running Entra Connect or Entra Connect Cloud Sync holds credentials capable of writing to Active Directory, and in password-hash-synchronization deployments it processes hash material for synchronized accounts. Its service account has historically carried directory replication rights. A compromise of that server is a compromise of the entire directory, and a compromise of the entire directory is a compromise of everything downstream in the cloud tenant.

The synchronization server is Tier 0. It is very often built, patched, and administered as Tier 1.

Other hybrid edges worth mapping:

* **Seamless SSO** creates the `AZUREADSSOACC$` computer account, whose Kerberos decryption key is used to validate tokens. That key does not rotate on its own. Possession of it enables forged Kerberos tickets accepted for cloud authentication. Rotate it on a defined schedule or do not deploy the feature.
* **Pass-through Authentication agents** validate cloud sign-ins against on-premises Active Directory. An agent host that an adversary controls sits directly in the authentication path.
* **Federation servers -** AD FS or a third-party IdP - hold token-signing keys that let the holder assert any identity the relying party trusts. This is the Golden SAML path where the point is narrower. The federation server, its configuration database, and its private key store are Tier 0 regardless of which team operates them.
* **Cloud-managed endpoints administering on-premises systems.** If a PAW/SAW is enrolled in a cloud device-management tenant, every administrator of that tenant holds a code-execution edge into the PAW/SAW, and therefore into Tier 0. The tenant's Global Administrators are Tier 0 whether or not they hold a single on-premises permission.
* **Cloud-side password reset and role assignment.** Where writeback or hybrid role assignment is enabled, cloud administrative roles can influence on-premises privileged accounts. Control flows down the pipe in both directions.
* **Cloud-stored secrets.** Windows LAPS can store local administrator passwords in Entra ID. That is a legitimate design. It also means the tenant holds recovery material for on-premises Tier 0 hosts, and tenant read permissions become an on-premises secret-recovery edge.

The federal framing adds one more constraint. A cloud service supporting a Tier 0 control path inherits the authorization requirements of the systems it controls. A synchronization or management service accredited for a lower impact level, or operating under a FedRAMP authorization that does not cover the DoD impact level of the systems it administers, is a clean source violation expressed as an authorization boundary problem. The system security plan will usually describe it as an interconnection. The control graph describes it as an inversion.

State the rule directly:

**A cloud control plane administering an on-premises identity system, and an on-premises system administering a cloud identity plane, are each governed by the clean source principle. The higher-authority side sets the requirement.**

### **4.6.16 Software Supply and Deployment Pathways Matter**

Administrative trust does not require a human login.

Software carries authority into a protected system as effectively as an administrator does.

Consider a domain controller receiving an updated monitoring agent from an enterprise software-deployment platform. The domain controller trusts that package sufficiently to install and execute it under a highly privileged security context. The deployment server therefore holds the ability to introduce executable state into Tier 0.

Where did the package originate?

Who can modify the deployment repository?

Who can alter the package after approval?

Who controls the build pipeline?

Which service account retrieves it?

Can an endpoint-management administrator replace the deployment command without changing the package?

Can the package-signing process be bypassed, or is signature enforcement advisory?

Can a lower-tier administrator change the share permissions from which Tier 0 systems obtain software?

Is the transport authenticated, or is it HTTP to a hostname resolved by a DNS server a lower tier can modify?

Each answer introduces another potential trust dependency.

The clean source principle extends into software supply.

A pristine administrative workstation does not preserve Tier 0 assurance if it installs scripts, modules, binaries, configuration packages, or updates supplied by infrastructure an attacker can modify from a lower security tier.

This is especially consequential for automation.

PowerShell modules, Desired State Configuration, infrastructure-as-code definitions, Group Policy startup and logon scripts, configuration-management agents, endpoint detection and response agents, and administrative tooling execute with enormous authority while receiving input from repositories far removed from the domain controllers themselves. A module installed from a public gallery onto a PAW is a supply edge from the internet into Tier 0, mediated only by whoever last published that module.

`SYSVOL` deserves specific attention because it is a software supply path that most agencies classify as a file share. Any principal able to write to `SYSVOL`, modify a GPO linked to the domain controllers OU, or alter a script referenced by a startup task holds a code-execution edge into every host in scope. GPO delegation drifts across reorganizations; the permission granted to a defunct desktop-support group in 2014 still executes code as `SYSTEM` in 2026.

> #### **Warning - Scripts Are Software**
>
> Administrative scripts stored on a general-purpose file share, retrieved by a scheduled task on a domain controller, and executed under a privileged context are indistinguishable from a supply-chain implant if the share ACL permits lower-tier write access. This pattern is common because it grew organically: someone needed an automated report, the share already existed, and nobody performed an authority analysis on a `.ps1` file. Audit write access to every path referenced by a Tier 0 scheduled task, service, GPO script, or agent configuration.

The relevant security boundary follows the deployment path backward.

For high-value identity infrastructure, agencies and commands should be able to answer:

_Where did this code originate?_

_Who approved it?_

_Who could have changed it between approval and execution?_

_How was its integrity verified, and by what key?_

_Which system delivered it?_

_What identity performed the deployment?_

_What evidence proves the artifact that was approved is the artifact that executed?_

These are identity-security questions, because executable code running under a trusted administrative context exercises that context's authority.

Practical enforcement means signature validation that fails closed rather than warns, application control policies (WDAC or AppLocker in enforcement mode) applied to Tier 0 hosts and PAWs, authenticated transport for every repository serving Tier 0, separate repositories for Tier 0 artifacts, and integrity verification recorded as evidence rather than performed and forgotten. Where the acquisition supports it, software bills of materials and provenance attestation belong in the same evidence package. NIST SP 800-53 Rev. 5 addresses this directly through the `SR` family - SR-3, SR-4, SR-5, SR-6, and SR-11 - alongside CM-5, CM-7, CM-14, SA-10, SA-11, and SI-7.

Software provenance and privileged identity are connected more closely than traditional diagrams show.

### 4.6.17 Out-of-Band, Firmware, and Physical Pathways Are Administrative Pathways

Every control discussed so far operates inside the operating system. Several of the most reliable paths into Tier 0 operate beneath it.

**Baseboard management controllers.** iDRAC, iLO, IPMI, and equivalent BMCs provide power control, virtual media, console redirection, and firmware update capability independent of the host operating system. A BMC on a domain controller host is a platform-control edge into Tier 0 that no amount of Windows hardening addresses. These interfaces frequently carry default credentials, shared credentials across a rack, unpatched firmware, and network placement on a "management" VLAN that half the infrastructure team can reach. CISA Binding Operational Directive 23-02 addresses exposed management interfaces for a reason. NIST SP 800-53 control MA-4 governs nonlocal maintenance, and it applies here even though nobody thinks of a BMC as maintenance tooling.

**KVM-over-IP, serial console servers, and remote console appliances.** Same edge, different vendor. Console access to a domain controller is administrative access to a domain controller.

**The virtualization stack.** A hypervisor administrator can mount the virtual disk of a domain controller and extract `NTDS.dit` and the `SYSTEM` hive offline. They can capture a memory snapshot and recover keys and tickets. They can clone a domain controller into an isolated network and attack it without time pressure. Live-migration networks carry unencrypted memory unless explicitly configured otherwise. Snapshot repositories are backup repositories by another name.

Microsoft's answer to this was the guarded fabric - shielded VMs, virtual TPMs, and the Host Guardian Service providing attestation and key release so that a Tier 0 virtual machine runs only on attested hosts. Windows Server 2025 supports shielded VMs, but the feature is no longer actively developed, with focus shifting toward Azure confidential computing. The Host Guardian Service is deprecated and unsupported on Windows Server 2025; HGS deployments require Windows Server 2022 Datacenter or earlier. Verify the support status for your platform version before committing to it in a design document.

The practical consequence for federal environments is uncomfortable. The platform feature designed to break the hypervisor-to-Tier-0 edge is winding down, which leaves separation as the primary control: run Tier 0 virtual machines on a dedicated cluster with dedicated storage, dedicated management, and dedicated administrators, or run them on physical hardware. Where a dedicated fabric is not affordable, the hypervisor administrators are Tier 0, and their accounts, workstations, and authentication paths must be governed accordingly. There is no third option that survives analysis.

**Firmware and boot integrity.** Secure Boot, measured boot, TPM-backed attestation, and DMA protection determine whether the operating system you hardened is the operating system that booted. Physical or virtual media presented through a BMC bypasses OS-level control entirely. Boot media, PXE infrastructure, and imaging servers are software supply paths.

**Classification and enclave boundaries.** In DoD environments the clean source principle has a security-domain expression: a system in a lower-classification enclave must not administer a system in a higher-classification enclave. Administrative connections crossing a boundary - through a cross-domain solution, a dual-homed management host, a shared KVM, or a shared administrator working both sides from one device - invert trust in exactly the way the principle prohibits. The same rule governs shared administrative tooling across mission enclaves that are otherwise separated.

### 4.6.18 People Are Part of the Source

A control graph that stops at machines is incomplete, because the last edge into every Tier 0 system terminates at a person.

Administrators are dependencies. The systems that authenticate them, the devices they carry, the accounts they use for ordinary work, and the processes that grant and revoke their authority all sit upstream of the identity infrastructure they manage.

Consider the paths that reach an administrator:

* **The second factor's host.** If an administrator's multifactor approval arrives on a personally owned phone running unmanaged applications, that phone is in the Tier 0 control path. Derived PIV credentials on mobile devices - Purebred in the DoD context - move that credential onto a device whose management posture must match the authority it unlocks.
* **The administrator's other identity.** An administrator whose Tier 0 account shares an inbox, a browser profile, a password manager, or a Single Sign-On session with their ordinary user account has merged the two boundaries. Separate accounts on the same device separate very little.
* **Vendor and contractor support access.** Remote support sessions, screen-sharing tools, and vendor jump boxes create temporary administrative edges that outlive the incident that justified them. Support tooling installed for a one-time engagement becomes a permanent code-execution path.
* **The account lifecycle itself.** Whoever can create, modify, or reset a Tier 0 account holds Tier 0 authority. A service desk with password-reset rights over privileged accounts, an identity governance platform with write access to privileged groups, or an HR-driven provisioning workflow feeding privileged group membership are all upstream of the directory.
* **Position sensitivity and investigation level.** Administrative tier should align with position sensitivity determination and investigative requirements. A Tier 0 role held by personnel whose vetting matches a Tier 2 function is a personnel-side trust inversion, and it appears in exactly zero network diagrams.

Two process controls belong in the design rather than the policy appendix:

**Separation of duties, applied to the control plane.** The team that administers the identity infrastructure should not also be the team that approves its changes, audits its logs, and controls its backups. Where staffing makes full separation impractical - a common condition at smaller commands and component agencies - document the compensating control and the detection that substitutes for it.

**Break-glass handling.** Emergency access accounts must be excluded from the authentication restrictions that would otherwise prevent recovery, which makes them the most dangerous credentials in the environment. Split knowledge, sealed and serialized envelopes, physical custody in a safe or GSA-approved container, documented two-person integrity for retrieval, and alerting on any use are minimum handling requirements. An emergency account whose password lives in the same vault that a compromise would take is not an emergency account.

### 4.6.19 Recovery Sources Must Also Be Clean

The clean source principle matters most when an environment is under the greatest pressure: recovery from compromise.

During an ordinary outage the objective is obvious - estore service.

During an identity compromise, restoring service is half the problem.

The recovered environment must also be trustworthy.

Imagine a forest compromise in which an adversary gained Domain Admin authority. The response team isolates the affected domain controllers and restores them from backup. Authentication resumes. DNS responds. Replication appears healthy. Users log in again.

Operationally, the forest is back.

But what exactly was restored?

If the backup already contained attacker-created permissions, malicious certificate templates, unauthorized group membership, modified delegation, `AdminSDHolder` changes, persistence in Group Policy, stolen service credentials, forged certificate authority trust, or compromised `krbtgt` material, the restoration reconstructed the adversary's environment along with the agency's.

Availability has been recovered.

Trust has not.

The specific artifacts that survive a restore, and that must be assumed compromised until proven otherwise:

* **`krbtgt` keys.** Restoring a domain controller from a backup taken before the compromise restores the `krbtgt` keys as they existed at backup time. If the adversary extracted them before that point, the Golden Ticket capability survives the restore. Two resets with replication convergence between them are required, and both must occur in the recovered environment, not before it.
* **The DPAPI domain backup key.** Recoverable from any restored system state. Its compromise persists across password resets.
* **Certificate authority private keys and issued certificates.** A certificate issued to an attacker before containment remains valid until revoked and until the revocation is honored. Certificate-based authentication survives password resets by design.
* **Computer account passwords and service account secrets.** Machine account keys restored from backup are the same keys the adversary may hold.
* **Delegation, ACLs, and GPO content.** Persistence written into the directory is data, and restore operations restore data faithfully.

The recovery source therefore requires its own security pedigree.

A backup used to rebuild Tier 0 must be treated as Tier 0 material. The system storing it, the administrators capable of restoring it, the credentials required to access it, the media on which it resides, and the infrastructure onto which it will be restored all participate in the identity trust system. Immutable or offline copies, independent credentials, and integrity verification performed before restoration are the operative controls; NIST SP 800-53 CP-9 and CP-10 provide the compliance language and, unusually, the compliance language matches the engineering requirement.

The same principle applies to installation media, scripts, automation, hypervisor templates, configuration exports, certificate backups, hardware security module recovery material, Group Policy backups, and privileged-account records.

Recovery can also fail in the opposite direction.

A clean backup may be restored onto a compromised hypervisor.

A trusted domain-controller image may be configured by an untrusted automation server.

A recovered forest may immediately be administered from the same endpoints that participated in the original compromise.

Clean data entering a dirty control path does not remain clean in any meaningful security sense.

This is why forest recovery requires more than technical knowledge of Active Directory restore procedures. It requires a trustworthy recovery environment from which known-good identity infrastructure can be reconstructed without depending on systems whose integrity is uncertain.

The sequence matters.

1. Trusted administrative devices must exist before they are used to rebuild trusted servers.
2. Trusted credentials must exist before they are used to administer those servers.
3. Trusted software, media, and configuration must exist before deployment.
4. Trusted recovery material must be validated before introduction.
5. Directory-level secrets with persistence value - `krbtgt`, DPAPI backup key, CA keys, service account credentials - must be rotated or reissued inside the recovered boundary.
6. Only then can downstream systems begin inheriting trust from the recovered identity infrastructure.

An isolated recovery environment - a clean room, physically or logically separated from production, with its own administrative endpoints, credentials, and media -  is what makes that sequence executable. Agencies that intend to build one during an incident will not build one during an incident.

This creates an uncomfortable but necessary distinction between _service restoration_ and _trust restoration_.

A server is restored when it works again.

An identity authority is restored when there is defensible reason to believe the adversary can no longer control what that authority asserts.

That standard is considerably higher, and it is the standard an authorizing official should be applying before the system returns to operational use.

### 4.6.20 Bootstrapping the First Clean Source

Every clean source chain terminates somewhere, and the terminal node is a problem in its own right. A PAW/SAW must be built by something. That something must be trustworthy. Well, what builds it?

The chain cannot regress forever, so it must terminate in a small set of artifacts whose integrity is established outside the environment being protected:

* **Verified installation media.** Operating system images obtained from the vendor or from an authorized government distribution point, like the General Services Administration (GSA), with cryptographic hashes verified against an independent source rather than against a hash published on the same page as the download.
* **An approved baseline.** DISA Security Technical Implementation Guides (STIGs) and the DoD Secure Host Baseline provide a defined, auditable starting configuration. Baseline provenance matters as much as baselined content - a STIG-compliant image built by an untrusted pipeline is definitely not a clean source.
* **An isolated build process.** Initial Tier 0 assets built offline, or on a network segment that has no inbound administrative pathway from production, using media introduced under controlled, authorized handling.
* **Hardware attestation.** TPM-backed measurements and Secure Boot establish that the platform booted what was installed. Where device health attestation is available, it essentially converts "we built this correctly" into evidence that survives the build.
* **Documented custody.** Who built it, what media, verified how, witnessed by whom. This is the same evidence discipline applied to key ceremonies, and for the same reason.

The bootstrap is a one-time act with permanent consequences. Once the first clean administrative device exists, it can build the second, and the chain becomes self-sustaining. Until it exists, everything downstream of it will inherit the trust posture of whatever entity built it - usually the general-purpose imaging infrastructure the design was meant to escape.

### 4.6.21 Verifying Clean Source

The control graph is testable. Treating clean source as an assertion in a System Security Plan (SSP) rather than a measured property is how trust inversions persist through consecutive assessments.

**Graph analysis.** BloodHound and SharpHound compute attack pathways across directory permissions, session data, and local group membership; the shortest pathways to Domain Admins are a direct answer to _"what can control Tier 0?"_ PingCastle and Purple Knight surface delegation, ACL, and configuration weaknesses with less collection overhead. Microsoft Defender for Identity (MDI), where deployed, reports lateral movement pathways built from observed sessions. Each tool answers part of the larger question. None enumerates BMCs, backup software, or scanning appliances - those require manual mapping against the catalog in 4.6.3.

**Authentication exposure.** The inversion posed in 4.6.4 is a query, not a philosophy. Detect Tier 0 accounts authenticating to hosts outside the Tier 0 boundary as such:

```kql
// Microsoft Sentinel — Tier 0 accounts authenticating outside the Tier 0 host boundary.
// Requires two watchlists: Tier0Accounts (SamAccountName) and Tier0Hosts (Computer).
let tier0Accounts = _GetWatchlist('Tier0Accounts') | project Account = tolower(tostring(SamAccountName));
let tier0Hosts    = _GetWatchlist('Tier0Hosts')    | project Host    = tolower(tostring(Computer));
SecurityEvent
| where TimeGenerated > ago(7d)
| where EventID == 4624                              // successful logon
| where LogonType in (2, 3, 7, 10, 11)               // interactive, network, unlock, RDP, cached
| extend AccountName = tolower(tostring(split(Account, "\\")[1]))
| extend TargetHost  = tolower(tostring(Computer))
| where AccountName in (tier0Accounts)               // a Tier 0 identity ...
| where TargetHost !in (tier0Hosts)                  // ... landing somewhere it should not
| summarize
    Logons      = count(),
    FirstSeen   = min(TimeGenerated),
    LastSeen    = max(TimeGenerated),
    LogonTypes  = make_set(LogonType),
    SourceIPs   = make_set(IpAddress, 25)
  by AccountName, TargetHost
| order by LastSeen desc
```

Kusto Query Language (`kql`)

```splunk
index=wineventlog EventCode=4624 LogonType IN (2,3,7,10,11)
| eval account=lower(mvindex(split(Account_Name,"\\"),-1))
| eval host=lower(ComputerName)
| lookup tier0_accounts.csv account OUTPUT tier0_account
| lookup tier0_hosts.csv host OUTPUT tier0_host
| where isnotnull(tier0_account) AND isnull(tier0_host)
| stats count AS logons
        values(LogonType) AS logon_types
        values(Source_Network_Address) AS src_ips
        min(_time) AS first_seen
        max(_time) AS last_seen
        BY account, host
| convert ctime(first_seen) ctime(last_seen)
| sort - last_seen
```

Splunk Query Language (`spl`)

### 4.6.22 Relevant Event IDs for Hunting

* 4624 - logon, with logon type;
* 4648 - explicit credential use - the "runas" trail that reveals tiering violations;
* 4672 - special privileges assigned, a proxy for privileged logon;
* 4768 and 4769 - Kerberos TGT and service ticket requests, with encryption type;
* 4776 - NTLM authentication attempt;
* 4964 - special group logon;
* 4820 - 4823 - Kerberos armoring and authentication policy failures; and,
* 5136 - directory object modification, for delegation and GPO changes.

Delegation and supply-path audit. Enumerate who holds write authority over the domain objects and file pathways that constitute Tier 0 supply.

```powershell
# Non-default principals holding write-class rights on the Domain Controllers OU
$dcOU = (Get-ADDomain).DomainControllersContainer
$acl  = Get-Acl -Path "AD:\$dcOU"
$acl.Access |
  Where-Object {
    $_.ActiveDirectoryRights -match 'WriteProperty|GenericAll|GenericWrite|WriteDacl|WriteOwner' -and
    $_.IdentityReference -notmatch 'BUILTIN\\Administrators|NT AUTHORITY\\SYSTEM|Enterprise Admins|Domain Admins'
  } |
  Select-Object IdentityReference, ActiveDirectoryRights, ObjectType, InheritanceType

# Principals able to modify GPOs linked to the Domain Controllers OU
Get-GPInheritance -Target $dcOU | Select-Object -ExpandProperty GpoLinks | ForEach-Object {
    $gpo = Get-GPO -Guid $_.GpoId
    [pscustomobject]@{
        GPO        = $gpo.DisplayName
        Editors    = (Get-GPPermission -Guid $gpo.Id -All |
                      Where-Object { $_.Permission -match 'GpoEdit|GpoEditDeleteModifySecurity' } |
                      ForEach-Object { $_.Trustee.Name }) -join '; '
    }
}

# Accounts with unconstrained delegation — every one is a credential-capture edge
Get-ADObject -LDAPFilter '(userAccountControl:1.2.840.113556.1.4.803:=524288)' `
  -Properties samAccountName, objectClass |
  Select-Object samAccountName, objectClass
```

**Assessment questions that produce evidence rather than assurances:**

1. Show the list of every account and system that can execute code on a domain controller. Not the list of Domain Admins - the list of everything with that edge.
2. For each item on that list, show its patch status, its administrative source, and where its administrators authenticate.
3. Show 30 days of Tier 0 authentication events landing on non-Tier 0 hosts and territory.
4. Show the ACL on every file pathway referenced by a Tier 0 scheduled task, service, or GPO script.
5. Show the credentials configured in the vulnerability scanner, the backup platform, and the endpoint management console, and the tier of each.
6. Show who can access the BMC of each domain controller host, and how they authenticate to it.
7. Demonstrate a domain controller restore into an isolated environment, and identify who could have altered the backup.

An environment that cannot produce these artifacts has not implemented the clean source principle regardless of what the control implementation statement says.

### 4.6.23 Common Trust Inversions

The same failures recur across federal and military enterprises. Each entry below is an inversion - an upstream node less protected than what it controls.

| Pattern                                                       | The inversion                                                                  |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| PAW/SAWs enrolled in the general endpoint management system   | Tier 2 management holds code execution on Tier 0 devices                       |
| Jump host reachable from ordinary user desktops               | The hardened host inherits the trust level of its callers                      |
| Hypervisor administrators outside Tier 0                      | Platform control without Tier 0 governance                                     |
| Backup service account in Domain Admins                       | Convenience purchase of a permanent Tier 0 edge                                |
| Credentialed scanning with a Domain Admin account             | A single appliance holds the highest credential in the entire forest           |
| EDR/MDR/NDR/XDR console operated by a Tier 1 team             | Arbitrary `SYSTEM` execution on DCs, delegated downward                        |
| Entra Connect server built as a member server                 | Directory-write authority on a Tier 1 baseline                                 |
| Service desk holds reset rights over privileged accounts      | Account lifecycle control without tier alignment                               |
| Tier 0 admin account has a mailbox and browses the web        | The administrative identity acquires an internet and web server attack surface |
| DC host BMC on the general management VLAN                    | Below-OS access with above-OS consequences                                     |
| Break-glass credentials stored in the PAM vault               | Recovery depends on the system a compromise would take                         |
| ESAE forest built, the administered from production endpoints | The architecture exists; the principle was never applied                       |
| "Tier 0" defined as a group membership list                   | Tiering applied to accounts rather than to capability                          |

The final row is the most common of all, and it is why this section leads with the graph rather than with the group.

### 4.6.24 Implementation Sequence and Interim Risk

Clean source is frequently presented as an absolute, which invites the response that it is unaffordable, which produces no change at all. A sequenced approach preserves the principle while acknowledging that most environments start deep in violation of it.

**Phase 1 - Discovery.** Map the control graph. Produce the list of everything holding an edge into Tier 0. Do this before purchasing anything. The output is an inventory, and it is usually the most valuable artifact the exercise produces.

**Phase 2 - Contain credentials.** Deploy the tier-based deny-logon GPOs, place Tier 0 accounts in Protected Users, remove Tier 0 accounts from routine use, and stand up dedicated administrative endpoints (PAW/SAW) for the smallest possible set of Tier 0 operations as feasibly possible. This, in turn, greatly reduces credential attack surface, escalation of privileges, pivoting, and horizontal / vertical lateral movement. Further, this phase also produces the largest reduction in exposure per single dollar.

**Phase 3 - Separate management.** Move Tier 0 assets of shared endpoint management, shared scanning credentials, and shared deployment infrastructure. Give the Tier 0 control plane its own patching, its own repositories, and its own administrators.

**Phase 4 - Secure supply and platform.** Application control on Tier 0 hosts and PAW/SAWs, authenticated repositories, signature enforcement, dedicated virtualization or physical hardware, and BMC isolation with unique credentials.

**Phase 5 - Prove recovery.** Isolated recovery environment, validated media, tested forest recovery including secret rotation, and evidence retained for the authorizing official.

Where a phase cannot be completed, the gap belongs in the Plan of Action and Milestones (POA\&M)  with the dependency named explicitly. _"Tier 0 hosts are managed by the enterprise endpoint management system, which is administered by personnel outside the Tier 0 boundary"_ is an accurate, assessable, and fundable statement. _"Privileged access management is implemented in accordance with agency policy"_ is none of those things.

Interim compensating controls that carry real weight while a phase is outstanding: monitoring every action the over-privileged dependency takes against Tier 0, requiring change approval for its deployments to Tier 0 targets, restricting its Tier 0 scope to an enumerated host list, and alerting on any expansion of that list. These do not satisfy the principle. They make its violation visible, which is the next best thing.

### 4.6.25 MITRE ATT\&CK & D3FEND Framework and Control Mapping

<table><thead><tr><th>Clean source requirement</th><th>NIST SP 800-53 Rev. 5</th><th width="177.5714111328125">Other authorities</th><th width="149">ATT&#x26;CK</th><th>D3FEND</th></tr></thead><tbody><tr><td>Privileged access originates from dedicated, hardened endpoints</td><td>AC-6(1), AC-6(2), AC-6(5), AC-17, AC-19</td><td>DoD ZT (User and Device pillars); DISA Windows STIGs</td><td>T1078.002, T1021.001</td><td>Credential Hardening, Execution Isolation</td></tr><tr><td>Credentials restricted to appropriate boundaries</td><td>IA-2, IA-5, AC-3, AC-6(10)</td><td>OMB M-22-09; DoDI 8520.03; NIST SP 800-63 AAL3</td><td>T1550.002, T1550.003, T1003</td><td>Credential Transmission Scoping</td></tr><tr><td>Administrative dependencies tiered by capability</td><td>CA-3, PM-5, RA-3, SA-8</td><td>NIST SP 800-207; DoDI 8510.01</td><td>T1072, T1078</td><td>Asset Inventory, Network Mapping</td></tr><tr><td>Software supply integrity into Tier 0</td><td>CM-5, CM-7, CM-14, SA-10, SA-11, SI-7, SR-3, SR-4, SR-5, SR-6, SR-11</td><td>NIST SP 800-161r1; EO 14028 §4</td><td>T1195, T1072, T1554</td><td>Executable Allowlisting, File Integrity Monitoring</td></tr><tr><td>Out-of-band and platform paths governed</td><td>MA-4, PE-3, SC-7, SI-7(9)</td><td>CISA BOD 23-02; platform STIGs</td><td>T1542, T1200</td><td>Platform Monitoring, Firmware Verification</td></tr><tr><td>Recovery sources trustworthy and validated</td><td>CP-9, CP-10, CP-2, SI-7(1)</td><td>NSA/CISA/ACSC AD compromise guidance (2024)</td><td>T1490, T1078.002</td><td>Backup Integrity, System Restoration</td></tr><tr><td>Personnel and lifecycle authority aligned to tier</td><td>AC-2, AC-5, PS-2, PS-3, PS-7</td><td>DoD 8140 workforce framework</td><td>T1078, T1098</td><td>Account Locking, Authorization Event Thresholding</td></tr></tbody></table>

Adjust the D3FEND column to the specific technique identifiers used elsewhere in the book so this table matches the crosswalk in the appendix rather than duplicating it.

### 4.6.26 Field Note - Follow the Administrative Pathway Backward

When evaluating a high-value identity system, begin with the system and work backward.

Do not stop at the administrators listed in the access-control documentation.

Ask what can control the administrators.

Then ask what control those systems.

Continue until the pathway reaches components whose compromise cannot alter the original target.

For a domain controller, the pathway may look similar to this:

```
Domain Controller
  ← Privileged Administration
    ← Privileged Access Workstation
      ← PAW Management Infrastructure
        ← Software Deployment Platform
          ← Administrative Repository
            ← Build or Package Authority
```

Another pathway:

```
Domain Controller
  ← Virtual Machine
    ← Hypervisor
      ← Virtualization Management Platform
        ← Virtualization Administrator
          ← Administrator's Workstation
```

Another:

```
Domain Controller
  ← System-State Backup
    ← Backup Platform
      ← Backup Administrator
        ← Backup Vendor Support Tooling
```

And the one most often missing from the diagram entirely:

```
Domain Controller
  ← Host Hardware
    ← Baseboard Management Controller
      ← Management Network
        ← Whoever Can Reach It
```

If any upstream node is less protected than the domain controller while retaining the ability to influence its state, the architecture contains a trust inversion.

Attackers look for those exact inversions because they provide a route around the strongest defenses.

Defenders should find them first.

> ### Sidebar - The Professional: Patience Is A Control Bypass
>
> _I never went at the domain controllers. Why would I? They were the one thing that team actually watched._\
> _I took a build server. Not a glamorous one - a box that pushed agent updates and had been running the same service account since a migration nobody documented. It could write to a share. The share fed a scheduled task. The task ran on four machines, and one of them mattered._\
> _Then I waited._\
> _Eleven days. On the twelfth, someone with real authority connected to troubleshoot a certificate problem, and every control they had bought that year became decoration, because the environment they trusted was already mine. It had been mine. I didn't crack anything. I didn't need to spend wads of cash on an expensive zero-day from the dark web or vanilla-net hacker forum. I needed them to keep doing their jobs the way they always had._\
> _That is the part defenders underestimate. I am not fighting your strongest control. I am standing behind it, holding the door._

### 4.6.27 Adopting the CSP as an Attack Pathway Management Routine Discipline

The clean source principle is therefore not a workstation-hardening recommendation. It is a method for discovering the true perimeter of administrative authority. Applied correctly, it exposes hidden Tier 0 systems, unsafe credential placements, untrusted deployment chains and pipelines, out-of-band control pathways, hybrid identity inversions, and recovery dependencies that ordinary identity diagrams fail to show.

For federal and Department of Defense environments, this carries direct mission significance. Identity systems determine which people, devices, services, and workloads the enterprise accepts as legitimate. If the systems administering those identity authorities cannot themselves be trusted, neither can the decisions produced by the identity infrastructure they effectively control.

The security boundary does not end at the domain controller, the Certificate Authority (CA), or the Identity Provider (IdP).

It ends at the least-trusted system still capable of changing them.

### **4.6.28 From Principle to Practice** <a href="#conclusion-from-principle-to-practice" id="conclusion-from-principle-to-practice"></a>

The Clean Source Principle gives us a simple but powerful lens: security dependencies must be as trustworthy as the objects they secure. When that rule is violated, attack paths emerge. Our exploration of GitHub, Entra, and Active Directory shows how easily these violations occur, and how they compound across platforms.

The lesson is clear: you cannot treat identity risk as a one-time project or as a siloed control. Dependencies are structural. They evolve as your platforms evolve, and they re-emerge wherever trust is concentrated. Hardening alone will never be enough, and you cannot even see these security dependencies without the visibility that BloodHound provides.

This is why **Attack Path Management must be treated as a practice.** Like vulnerability management or detection engineering, it is not a box to check, it is a discipline that requires visibility, prioritization, and continual validation. Our Attack Path Management maturity model makes this explicit: organizations must progress from simply seeing attack paths, to understanding their dependencies, to actively constraining and removing them as part of routine operations.

BloodHound OpenGraph provides the foundation for this practice. It surfaces both intra- and inter-platform dependencies, reveals hybrid attack paths that no human could model alone, and ensures that as the identity ecosystem shifts, defenders are never blind to the new leviathan.

The time to build this practice is now. Attackers are already exploiting hybrid paths; every dependency you fail to see is one they will. By adopting Attack Path Management as a routine discipline, agencies and commands can finally get ahead of this structural problem, cut off entire classes of attack, and take control of their own identity risk.

### 4.6.29 Section 4.6 Key Concepts Review

* Administration is a trust relationship. When one system can configure, repair, deploy to, virtualize, backup, restore, or attest another, the target's security then depends on the source caller's.
* A system must not be administered from a security context less trustworthy than the system being administered. That is the Clean Source Principle in one sentence.
* Model the environment as a directed control graph. Draw an edge wherever A can change B is or what B believes, then treat tiering as a question of reachability.
* Tier follows effective control, not group membership, job title, or product category. A backup platform that can restore the `NTDS.dit` file is Tier 0 regardless of what the asset inventory calls it.
* The hazard is not a large Tier 0. The hazard is a Tier 0 dependency nobody has recognized as one.
* Authentication places reusable credential material on the destination host. Ask where privileged accounts _have authenticated_, not only where they are _supposed to work_.
* Strong authentication defeat credential duplication, not session abuse. Phishing-resistant MFA does not remove the requirement for a trustworthy administrative endpoint.
* Software, firmware, out-of-band interfaces, and hybrid synchronization all carry authority into Tier 0 without a human login. Each is an administrative pathway.
* People are nodes in the graph. The device holding the second factor, the administrator's ordinary identity, and whoever can reset a privileged account all sit upstream of the root directory.
* Recovery has its own pedigree. A restore that reinstates adversarial persistence has recovered availability and not trust.
* The chain must terminate in artifacts verified outside the environment being protected, or everything downstream inherits the trust posture of whatever or whoever built it.
* The security boundary ends at the least-trusted system still capable of changing the identity authority.

### 4.6.30 Terms Introduced

Clean source principle · control graph · control edge · trust inversion · hidden Tier 0 · credential placement · administrative dependency · inheritance · service restoration versus trust restoration · clean source bootstrap

### 4.6.31 Section 4.6 Basic Review Questions

_Answers are found in the subsection noted after each question._

1. State the clean source principle in one sentence, and explain why the security of a domain controller can depend on a system that holds no directory permissions at all. (§4.6)
2. Name four of the eight control-edge types, and give an example of a product or platform that typically holds each one over a domain controller. (§4.6.1)
3. Define a trust inversion. Why is an inversion more useful to an attacker than a vulnerability or a zero-day in the target itself? (§4.6.1)
4. A domain administrator authenticates with a PIV card to a Tier 1 server that is already compromised. Explain what the adversary can do despite the card never leaving the card reader. (§4.6.2)
5. An account is configured with `Smart Card Required for Interactive Logon`. Why does it still have an NT hash, what makes that hash so dangerous, and what setting causes it to rotate? (§4.6.2)
6. A backup server holds no privileged group memberships and its administrators cannot open the Active Directory Users and Computers (ADUC) administrative console. Explain why it may still be Tier 0. (§4.6.3)
7. Name two secrets that are recoverable from a domain controller system-state ackup and that survive a full password reset of every privileged account. (§4.6.3, §4.6.9)
8. Deny-logon policy is applied so that Tiers 1 and 2 accounts cannot log on to Tier 0 systems. Whivh half of the control is missing, and what attack does the missing half prevent? (§4.6.4)
9. Why is the directory synchronization server a Tier 0 asset, and name two other hybrid components that hold an identity-issuance edge. (§4.6.5)
10. Explain how write access to a file share can be equivalent to code execution on a domain controller. (§4.6.6)
11. A domain controller that is fully STIG-compliant, patched, and hardened can still be authenticated to by an attacker. Describe two ways an adversary can read its `NTDS.dit` without authenticating to Windows at all. (§4.6.7)
12. Distinguish service restoration from trust restoration. Give two artifacts that a successful restore can reinstate on the adversary's behalf. (§4.6.9)
13. Every clean source depends on a cleaner source. Explain how the chain terminates without regressing forever. (§4.6.10)
14. Why is "Tier 0 consists of the members of the Domain Admins, Enterprise Admins, and Schema Admins groups" an inadequate definition? (§4.6.3, §4.6.12)

### 4.6.32 Deep-Dive Review Questions (Q\&A)

_Use these open-ended and scenario-based questions for review or self-study to better help you apply these concepts critically._

**Q1: Define the Clean Source Principle (CSP) using the concept of security dependencies.**

* **Answer:** CSP dictates that an object's security is only as strong as the security of all its dependencies. A "security dependency" exists if an entity can control, modify, or compromise another entity. Under CSP, highly trusted systems (e.g., Tier 0 assets like Domain Controllers) must only have security dependencies that are _equally or more trusted_ than themselves. If a Tier 0 asset relies on a lower-security system (e.g., a standard workstation), that lower system becomes a hidden backdoor into the core identity infrastructure.

**Q2: Scenario: An Active Directory administrator routinely logs into a standard receptionist workstation using their Domain Admin account to troubleshoot a local software issue. Explain how this violates the Clean Source Principle.**

* **Answer:** This violates CSP because it creates a reverse security dependency where a Tier 0 asset (Domain Admin credentials) relies on the integrity of a Tier 2 asset (the receptionist’s workstation). If the workstation is infected with malware, an attacker can use tools to extract the Domain Admin’s credentials or Kerberos tickets straight from memory. The administrator has effectively allowed a lower-trust system to dictate the security of the highest-trust system in the organization.

**Q3: What role do Secure Administrative Workstations (SAWs) or Privileged Access Workstations (PAWs) play in upholding CSP?**

* **Answer:** Secure Admin Workstations (SAWs) or PAWs serve as the _only_ "clean source" from which privileged administrative actions can be initiated. By enforcing a rule where directory administration can only happen from hardened, internet-restricted, and strictly monitored devices, organizations ensure that the administrative session is not exposed to common vectors like phishing or web-based malware. This isolates Tier 0 administrative tasks from lower-trust user environments.

**Q4: How does a Tiered Administration Model align with the Clean Source Principle?**

*   **Answer:** The Microsoft Tiered Administration Model splits an environment into strict security boundaries:

    * **Tier 0:** Identity systems (Domain Controllers, PKI, identity management tools).
    * **Tier 1:** Enterprise servers, cloud applications, and databases.
    * **Tier 2:** End-user devices (workstations, laptops, printers).

    This aligns with CSP by strictly banning credentials and administrative access from mixing across tiers. High-tier accounts are blocked from logging into lower-tier assets, preventing lateral movement and credential theft from weaker sources.

### 4.6.33 Section 4.6 Question & Answer (Q\&A) Review

_Answers are found at the end of this section._

1. **What is the fundamental objective of the Clean Source Principle?**

* [ ] A. To ensure that all user accounts are periodically audited and purged if inactive for over 90 days.
* [ ] B. To guarantee that administrative tools, operatingsystems, and deployment media used for Tier 0 assets originate from a known, trusted, and uncompromised state.
* [ ] C. To automatically clea and sanitize the Active Directory database (`NTDS.dit`) of dangling SIDs and orphaned domain objects.
* [ ] D. To restrict standard users from accessing domain controllers via network shares.<br>

2. **In the framework of the Clean Source Principle, why are downstream security dependencies (such as third-party software repositories or master virtual machine images) considered critical vectors of compromise?**

* [ ] A. They increase the replication traffic between domain controllers across Wide Area Network (WAN) links.
* [ ] B. They cause Kerberos Ticket Granting Service (TGS) request failures due to mismatched encryption types.
* [ ] C. They prevent Active Directory from validating LDAP bindings against external identity providers.
* [ ] D. They can introduce supply-chain vulnerabilities or hidden modifications that bypass local security boundaries during initial deployment.<br>

3. **How does the Clean Source Principle apply when deploying management tools or Group Policy Objects (GPOs) from Tier 1 (Server Administration) to Tier 0 (Enterprise Administration)?**

* [ ] A. Tier 0 assets must never rely on trust tools, management stations, or configurations managed by a lower tier (Tier 1 or Tier 2), as a compromise in a lower tier invalidates the higher tier.
* [ ] B. Tier 1 assets are allowed to manage Tier 0 assets as long as multi-factor authentication is enforced.
* [ ] C. Tier 0 and Tier 1 can share the same administrative sign-on credentials to streamline operational efficiency.
* [ ] D. Tier 1 resources can override Tier 0 Access Control Lists (ALCs) if authorized by a Domain Admin.<br>

4. **If an organization fails to enforce the Clean Source Principle on standard IT workstations used by helpdesk staff, how does this directly facilitate lateral movement by an attacker?**

* [ ] A. It forces domain controllers to disable Server Message Block (SMB) signing, exposing them to NTLM relay attacks.
* [ ] B. It allows attackers to spoof DNS records and redirect replication traffic to a rogue domain controller.
* [ ] C. It enables attackers who compromise a lower-privilege machine to harvest privileged credentials (e.g., via memory dumping or keyloggers) used during administrative sessions on that machine.
* [ ] D. It causes the Key Distribution Center (KDC) to issue over-privileged golden tickets automatically.<br>

5. **What makes a Privileged Access Workstation / Secure Administrative Workstation (PAW/SAW) a direct implementation of the Clean Source Principle for Tier 0 administrators?**

* [ ] A. It automatically wipes and reinstalls its operating system every 24 hours using a local recovery partition.
* [ ] B. It runs an immutable, strictly controlled operating system with no internet borwsing or general email access, ensi=uring the environment remains untainted by external threats.
* [ ] C. It uses biometric authentication that bypasses Active Directory's Kerberos verification completely.
* [ ] D. It encrypts the NTDS.dit file locally on the workstation to prevent offline cracking.

***

### 4.6.34 Applied Exercise - Meridian Component

Meridian Component operates a single-domain forest with four domain controllers for redundancy. Its architecture documentation records the following.

{% hint style="info" %}
The domain controllers run as virtual machines (VMs) on the general-purpose Hyper-V cluster, administered by the server operations team. That cluster's hosts are Dell servers whose iDRAC interfaces sit on a management Virtual Local Area Network (VLAN) that is reachable from the operations team's standard desktops, using a shared credential documented in the team's runbook.\
\
Six Domain Admin accounts exist. Their holders connect through a hardened jump host, reaching it via Remote Desktop Protocol (RDP) from their ordinary enterprise user workstations. Two privileged access workstations (PAW/SAW) were procured last year and enrolled in the enterprise endpoint management system alongside all 4,000 user devices.\
\
Backups are handled by an enterprise platform whose agent runs under a service account added to Domain Admins during the 2019 installation (it is current 2026). Assured Compliance Assessment Scanner (ACAS) credentialed scanning uses a separate account holding local administrator rights on all servers, including the domain controllers. Entra Connect runs on a member server built from the standard server image and patched on the server team's monthly cycle.\
\
The Backup & Disaster Recovery Plan (BDRP) calls for restoring domain controllers from the most recent system-state backup, verifying replication, and returning the forest to complete functional service.
{% endhint %}

15. Draw the control graph for one domain controller. Identify every node holding an edge into it and label the edge type.
16. Identify at least six trust inversions in this environment. For each, state which upstream node is less protected than the asset it can reach.
17. Which single change would remove the most inversions for the least cost, and why?
18. The BDRP is executed after a confirmed Domain Admin compromise. State what the restored forest still contains, and what steps are missing.

### 4.6.35 Answer Key - Meridian Component Applied Exercise

> 15. **At minimum:** the Hyper-V cluster and its management platform (platform control); the iDRAC interfaces and anyone who can reach the management VLAN (platform control); the enterprise endpoint management system (code execution, via the PAW/SAWs and any managed Tier 0 host); the jump host and the ordinary user workstations upstream of it (human control, credential placement); the backup platform and its service account (state restoration, secret recovery); the ACAS scanner and its stored credentials (secret recovery, code execution); Entra Connect (secret recovery, identity issuance); and the server operations, backup, scanning, and endpoint teams as human nodes upstream of each.

> 16. **Six or more of:** (a) domain controllers on a shared hypervisor administered by a Tier 1 team - platform control without Tier0governance; (b) iDRAC on a reachable VLAN with a shared credential - below-OS access from ordinary desktops; (c) the jump host reached from unmanaged user workstations - the hardened host inherits its callers' trust posture/level; (d) PAW/SAWs enrolled in the enterprise endpoint management system - Tier 2 management holding code execution on Tier 0 devices; (e) the backup service account in Domain Admins - a permanent Tier 0 edge purchased for installation convenience; (f) ACAS credentials with local administrator rights on domain controllers - one appliance storing credentials that yield Tier 0; (g) Entra Connect on a Tier 1 baseline and patching cycle while holding directory-write authority.

> 17. Credential containment, per §4.6.13 - deny-logon policy in both directions plus dedicated administrative endpoints not managed by the enterprise system. It is policy rather than procurement, it removes inversions (c), (d), and much of the exposure created by (e) and (f), and it does not depend on finding a separate hypervisor cluster. Removing the backup service account from Domain Admins is the single cheapest individual fix and should accompany it.

> 18. The restored forest contains whatever persistence existed at backup time: attacker-created ACLs and delegation, modified GPO content, `AdminSDHolder` changes, unauthorized group membership, and issued certificates. It also restores the `krbtgt` keys as they existed at backup, so any previously extracted key material remains valid for ticket forgery, and the domain DPAPI backup key is unchanged.\
>     \
>     **Missing Steps:**
>
> * establishing trusted administrative devices and credentials before the rebuild;
> * validating the backup's integrity and the trustworthiness of the hypervisor receiving it;
> * double-resetting `krbtgt` inside the recovered boundary with replication convergence between resets;
> * reviewing and reissuing certificates;
> * rotating service and computer account secrets.
>
> The plan restores availability and asserts nothing about trust.

***

### 4.6.36 Answer Key for Questions & Answers (Q\&A) Review

1. **What is the fundamental objective of the Active Directory "Clean Source Principle"?**

{% hint style="danger" %}
A. To ensure that all user accounts are periodically audited and purged if inactive for over 90 days.\
\
Incorrect. Inactive account management is part of lifecycle hygiene, but the Clean Source Principle specifically targets the integrity of security tools, deployment media, and operational environments rather than account inactivity lifecycles.
{% endhint %}

{% hint style="success" %}
**B. To guarantee that administrative tools, operating systems, and deployment media used for Tier 0 assets originate from a known, trusted, and uncompromised state.**\
\
**Correct!** The Clean Source Principle dictates that nothing used to manage, build, or deploy high-privilege assets can be trusted if it has passed through or originated from an untrusted or contaminated environment.
{% endhint %}

{% hint style="danger" %}
C. To automatically clean and sanitize the Active Directory database (`NTDS.dit`) of dangling SIDs and domain orphaned objects.\
\
Incorrect. Sanitizing the `NTDS.dit` database relates to garbage collection and metadata cleanup, not the architectural philosophy of sourcing trusted administrative components.
{% endhint %}

{% hint style="danger" %}
D. To restrict standard users from accessing domain controllers via network shares.\
\
Incorrect. Restricting network access is a general hardening measure (access control), whereas the Clean Source Principle focuses on the integrity of the origin of administrative tools and systems.
{% endhint %}

***

2. **In the framework of the Clean Source Principle, why are downstream security dependencies (such as third-party software repositories or master virtual machine images) considered critical vectors of compromise?**

{% hint style="danger" %}
A. They increase the replication traffic between domain controllers across Wide Area Network (WAN) links.\
\
Incorrect. WAN replication traffic is an infrastructure/topology concern and does not directly relate to the conceptual security compromise vectors addressed by the Clean Source Principle.
{% endhint %}

{% hint style="danger" %}
B. They cause Kerberos ticket-granting service (TGS) request failures due to mismatched encryption types.\
\
Incorrect. Kerberos encryption mismatches are configuration or functional issues, not a core vector of compromise under the Clean Source framework.
{% endhint %}

{% hint style="danger" %}
C. They prevent Active Directory from validating LDAP bindings against external identity providers.\
\
Incorrect. LDAP binding validation issues stem from protocol or trust configurations, rather than the integrity of source assets and dependencies.
{% endhint %}

{% hint style="success" %}
**D. They can introduce supply-chain vulnerabilities or hidden modifications that bypass local security boundaries during initial deployment.**\
\
**Correct!** If a dependency or base blueprint used to construct systems is tainted upstream, all downstream builds inherit that compromise, rendering local security controls ineffective.
{% endhint %}

***

3. **How does the Clean Source Principle apply when deploying management tools or group policy objects (GPOs) from Tier 1 (Server Administration) to Tier 0 (Enterprise Administration)?**

{% hint style="success" %}
**A. Tier 0 assets must never rely on or trust tools, management stations, or configurations managed by a lower tier (Tier 1 or Tier 2), as a compromise in a lower tier invalidates the higher tier.**\
\
**Correct!** Tiering relies on unidirectional trust. A lower tier cannot be a "clean source" for a higher tier because any breach at Tier 1 or Tier 2 would automatically compromise Tier 0.
{% endhint %}

{% hint style="danger" %}
B. Tier 1 assets are allowed to manage Tier 0 assets as long as multi-factor authentication is enforced.\
\
Incorrect. MFA mitigates credential theft, but it does not alter the architectural reality that trusting a lower tier violates the isolation required by the Clean Source and Tiering principles.
{% endhint %}

{% hint style="danger" %}
C. Tier 0 and Tier 1 can share the same administrative sign-on credentials to streamline operational efficiency.\
\
Incorrect. Sharing credentials across tiers completely destroys the tiering boundary, allowing a Tier 1 compromise to instantly translate into Enterprise Admin control.
{% endhint %}

{% hint style="danger" %}
D. Tier 1 resources can override Tier 0 access control lists if authorized by a Domain Admin.\
\
Incorrect. Tier 0 represents the absolute top of the enterprise security boundary; lower tiers cannot override or manage Tier 0 components.
{% endhint %}

***

4. **If an organization fails to enforce the Clean Source Principle on standard IT workstations used by helpdesk staff, how does this directly facilitate lateral movement by an attacker?**

{% hint style="danger" %}
A. It forces domain controllers to disable SMB signing, exposing them to NTLM relay attacks.\
\
Incorrect. Workstation management hygiene does not dynamically alter domain controller SMB signing configurations.
{% endhint %}

{% hint style="danger" %}
B. It allows attackers to spoof DNS records and redirect replication traffic to a rogue domain controller.\
\
Incorrect. DNS security relies on zone protection, secure dynamic updates, and proper access controls on DNS servers, not the cleanliness of a helpdesk workstation source.
{% endhint %}

{% hint style="success" %}
**C. It enables attackers who compromise a lower-privilege machine to harvest privileged credentials (e.g., via memory dumping or keyloggers) used during administrative sessions on that machine.**\
\
**Correct!** Logging into an unclean or compromised workstation exposes administrative credentials to memory scrapers, allowing attackers to escalate privilege and move laterally.
{% endhint %}

{% hint style="danger" %}
D. It causes the Key Distribution Center (KDC) to issue over-privileged golden tickets automatically.\
\
Incorrect. Golden tickets require compromise of the krbtgt account hash, which is independent of helpdesk workstation configurations.
{% endhint %}

***

5. **What makes a Privileged Access Workstation (PAW) a direct implementation of the Clean Source Principle for Tier 0 administrators?**

{% hint style="danger" %}
A. It automatically wipes and reinstalls its operating system every 24 hours using a local recovery partition.\
\
Incorrect. While dynamic rebuilding is a great security practice, PAWs achieve their clean source status through hardware isolation, strict lockdown, and preventing general usage, not necessarily a 24-hour wipe cycle.
{% endhint %}

{% hint style="success" %}
**B. It runs an immutable, strictly controlled operating system with no internet browsing or general email access, ensuring the environment remains untainted by external threats.**\
\
**Correct!** PAW/SAWs implement the Clean Source Principle by separating day-to-day productivity tasks (where compromise typically occurs) from high-privilege management tasks.
{% endhint %}

{% hint style="danger" %}
C. It uses biometric authentication that bypasses Active Directory's Kerberos verification completely.\
\
Incorrect. PAW/SAWs still utilize secure authentication protocols like Kerberos or smart cards; they do not bypass AD authentication.
{% endhint %}

{% hint style="danger" %}
D. It encrypts the NTDS.dit file locally on the workstation to prevent offline cracking.\
\
Incorrect. The NTDS.dit database resides on domain controllers, not locally on a Privileged Access Workstation.
{% endhint %}
