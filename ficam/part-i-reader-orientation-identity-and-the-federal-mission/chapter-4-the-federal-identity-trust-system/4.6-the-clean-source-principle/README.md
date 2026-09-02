# ✔️ 4.6 The Clean Source Principle

{% hint style="info" %}
Administrative actions inherit risk from their workstations, credentials, software supply chains, and recovery sources.
{% endhint %}

Identity security is often discussed as though trust begins when a user enters a credential and ends when an access-control decision is returned. That view is much too narrow for a federal Active Directory environment. A domain controller may accept only approved administrative identities, require phishing-resistant authentication, enforce hardened Group Policies, and reside behind tightly controlled network boundaries, and the domain can still be lost if those administrators reach it from systems an adversary already owns.

The reason is straightforward: administration is itself a trust relationship.

When one system is allowed to configure, repair, monitor, virtualize, back up, deploy software to, image, attest, or otherwise control another system, the security of the target becomes dependent upon the security of the administrative source. The target may never explicitly identify that source as a trusted identity provider. Operationally, it has granted that source something more consequential - the ability to alter its state.

This produces one of the most important architectural rules in privileged-access design:

> **A system must not be administered from a security context less trustworthy than the system being administered.**

This is the Clean Source Principle.

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

### 4.6.1 Administration Is a Directed Trust Graph

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

### 4.6.2 A System Cannot Be Administered Safely From a Less-Trusted System

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

### 4.6.3 Administrative Dependencies Inherit the Target's Security Tier

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

### 4.6.4 Credential Entry Creates Trust Relationships

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

### 4.6.5 The Hybrid Control Plane Travels in Both Directions

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

### **4.6.6 Software Supply and Deployment Pathways Matter**

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

### 4.6.7 Out-of-Band, Firmware, and Physical Paths Are Administrative Paths

Every control discussed so far operates inside the operating system. Several of the most reliable paths into Tier 0 operate beneath it.

**Baseboard management controllers.** iDRAC, iLO, IPMI, and equivalent BMCs provide power control, virtual media, console redirection, and firmware update capability independent of the host operating system. A BMC on a domain controller host is a platform-control edge into Tier 0 that no amount of Windows hardening addresses. These interfaces frequently carry default credentials, shared credentials across a rack, unpatched firmware, and network placement on a "management" VLAN that half the infrastructure team can reach. CISA Binding Operational Directive 23-02 addresses exposed management interfaces for a reason. NIST SP 800-53 control MA-4 governs nonlocal maintenance, and it applies here even though nobody thinks of a BMC as maintenance tooling.

**KVM-over-IP, serial console servers, and remote console appliances.** Same edge, different vendor. Console access to a domain controller is administrative access to a domain controller.

**The virtualization stack.** A hypervisor administrator can mount the virtual disk of a domain controller and extract `NTDS.dit` and the `SYSTEM` hive offline. They can capture a memory snapshot and recover keys and tickets. They can clone a domain controller into an isolated network and attack it without time pressure. Live-migration networks carry unencrypted memory unless explicitly configured otherwise. Snapshot repositories are backup repositories by another name.

Microsoft's answer to this was the guarded fabric - shielded VMs, virtual TPMs, and the Host Guardian Service providing attestation and key release so that a Tier 0 virtual machine runs only on attested hosts. Windows Server 2025 supports shielded VMs, but the feature is no longer actively developed, with focus shifting toward Azure confidential computing. The Host Guardian Service is deprecated and unsupported on Windows Server 2025; HGS deployments require Windows Server 2022 Datacenter or earlier. Verify the support status for your platform version before committing to it in a design document.

The practical consequence for federal environments is uncomfortable. The platform feature designed to break the hypervisor-to-Tier-0 edge is winding down, which leaves separation as the primary control: run Tier 0 virtual machines on a dedicated cluster with dedicated storage, dedicated management, and dedicated administrators, or run them on physical hardware. Where a dedicated fabric is not affordable, the hypervisor administrators are Tier 0, and their accounts, workstations, and authentication paths must be governed accordingly. There is no third option that survives analysis.

**Firmware and boot integrity.** Secure Boot, measured boot, TPM-backed attestation, and DMA protection determine whether the operating system you hardened is the operating system that booted. Physical or virtual media presented through a BMC bypasses OS-level control entirely. Boot media, PXE infrastructure, and imaging servers are software supply paths.

**Classification and enclave boundaries.** In DoD environments the clean source principle has a security-domain expression: a system in a lower-classification enclave must not administer a system in a higher-classification enclave. Administrative connections crossing a boundary - through a cross-domain solution, a dual-homed management host, a shared KVM, or a shared administrator working both sides from one device - invert trust in exactly the way the principle prohibits. The same rule governs shared administrative tooling across mission enclaves that are otherwise separated.

### 4.6.8 People Are Part of the Source

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

### 4.6.9 Recovery Sources Must Also Be Clean

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

### 4.6.10 Bootstrapping the First Clean Source

Every clean source chain terminates somewhere, and the terminal node is a problem in its own right. A PAW/SAW must be built by something. That something must be trustworthy. Well, what builds it?

The chain cannot regress forever, so it must terminate in a small set of artifacts whose integrity is established outside the environment being protected:

* **Verified installation media.** Operating system images obtained from the vendor or from an authorized government distribution point, like the General Services Administration (GSA), with cryptographic hashes verified against an independent source rather than against a hash published on the same page as the download.
* **An approved baseline.** DISA Security Technical Implementation Guides (STIGs) and the DoD Secure Host Baseline provide a defined, auditable starting configuration. Baseline provenance matters as much as baselined content - a STIG-compliant image built by an untrusted pipeline is definitely not a clean source.
* **An isolated build process.** Initial Tier 0 assets built offline, or on a network segment that has no inbound administrative pathway from production, using media introduced under controlled, authorized handling.
* **Hardware attestation.** TPM-backed measurements and Secure Boot establish that the platform booted what was installed. Where device health attestation is available, it essentially converts "we built this correctly" into evidence that survives the build.
* **Documented custody.** Who built it, what media, verified how, witnessed by whom. This is the same evidence discipline applied to key ceremonies, and for the same reason.

The bootstrap is a one-time act with permanent consequences. Once the first clean administrative device exists, it can build the second, and the chain becomes self-sustaining. Until it exists, everything downstream of it will inherit the trust posture of whatever entity built it - usually the general-purpose imaging infrastructure the design was meant to escape.

### 4.6.11 Verifying Clean Source

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

### 4.6.12 Relevant Event IDs for Hunting

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

### 4.6.13 Common Trust Inversions

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

### 4.6.14 Implementation Sequence and Interim Risk

Clean source is frequently presented as an absolute, which invites the response that it is unaffordable, which produces no change at all. A sequenced approach preserves the principle while acknowledging that most environments start deep in violation of it.

**Phase 1 - Discovery.** Map the control graph. Produce the list of everything holding an edge into Tier 0. Do this before purchasing anything. The output is an inventory, and it is usually the most valuable artifact the exercise produces.

**Phase 2 - Contain credentials.** Deploy the tier-based deny-logon GPOs, place Tier 0 accounts in Protected Users, remove Tier 0 accounts from routine use, and stand up dedicated administrative endpoints (PAW/SAW) for the smallest possible set of Tier 0 operations as feasibly possible. This, in turn, greatly reduces credential attack surface, escalation of privileges, pivoting, and horizontal / vertical lateral movement. Further, this phase also produces the largest reduction in exposure per single dollar.

**Phase 3 - Separate management.** Move Tier 0 assets of shared endpoint management, shared scanning credentials, and shared deployment infrastructure. Give the Tier 0 control plane its own patching, its own repositories, and its own administrators.

**Phase 4 — Secure supply and platform.** Application control on Tier 0 hosts and PAW/SAWs, authenticated repositories, signature enforcement, dedicated virtualization or physical hardware, and BMC isolation with unique credentials.

**Phase 5 — Prove recovery.** Isolated recovery environment, validated media, tested forest recovery including secret rotation, and evidence retained for the authorizing official.

Where a phase cannot be completed, the gap belongs in the Plan of Action and Milestones (POA\&M)  with the dependency named explicitly. _"Tier 0 hosts are managed by the enterprise endpoint management system, which is administered by personnel outside the Tier 0 boundary"_ is an accurate, assessable, and fundable statement. _"Privileged access management is implemented in accordance with agency policy"_ is none of those things.

Interim compensating controls that carry real weight while a phase is outstanding: monitoring every action the over-privileged dependency takes against Tier 0, requiring change approval for its deployments to Tier 0 targets, restricting its Tier 0 scope to an enumerated host list, and alerting on any expansion of that list. These do not satisfy the principle. They make its violation visible, which is the next best thing.

### 4.6.15 MITRE ATT\&CK & D3FEND Framework and Control Mapping

<table><thead><tr><th>Clean source requirement</th><th>NIST SP 800-53 Rev. 5</th><th width="177.5714111328125">Other authorities</th><th width="149">ATT&#x26;CK</th><th>D3FEND</th></tr></thead><tbody><tr><td>Privileged access originates from dedicated, hardened endpoints</td><td>AC-6(1), AC-6(2), AC-6(5), AC-17, AC-19</td><td>DoD ZT (User and Device pillars); DISA Windows STIGs</td><td>T1078.002, T1021.001</td><td>Credential Hardening, Execution Isolation</td></tr><tr><td>Credentials restricted to appropriate boundaries</td><td>IA-2, IA-5, AC-3, AC-6(10)</td><td>OMB M-22-09; DoDI 8520.03; NIST SP 800-63 AAL3</td><td>T1550.002, T1550.003, T1003</td><td>Credential Transmission Scoping</td></tr><tr><td>Administrative dependencies tiered by capability</td><td>CA-3, PM-5, RA-3, SA-8</td><td>NIST SP 800-207; DoDI 8510.01</td><td>T1072, T1078</td><td>Asset Inventory, Network Mapping</td></tr><tr><td>Software supply integrity into Tier 0</td><td>CM-5, CM-7, CM-14, SA-10, SA-11, SI-7, SR-3, SR-4, SR-5, SR-6, SR-11</td><td>NIST SP 800-161r1; EO 14028 §4</td><td>T1195, T1072, T1554</td><td>Executable Allowlisting, File Integrity Monitoring</td></tr><tr><td>Out-of-band and platform paths governed</td><td>MA-4, PE-3, SC-7, SI-7(9)</td><td>CISA BOD 23-02; platform STIGs</td><td>T1542, T1200</td><td>Platform Monitoring, Firmware Verification</td></tr><tr><td>Recovery sources trustworthy and validated</td><td>CP-9, CP-10, CP-2, SI-7(1)</td><td>NSA/CISA/ACSC AD compromise guidance (2024)</td><td>T1490, T1078.002</td><td>Backup Integrity, System Restoration</td></tr><tr><td>Personnel and lifecycle authority aligned to tier</td><td>AC-2, AC-5, PS-2, PS-3, PS-7</td><td>DoD 8140 workforce framework</td><td>T1078, T1098</td><td>Account Locking, Authorization Event Thresholding</td></tr></tbody></table>

Adjust the D3FEND column to the specific technique identifiers used elsewhere in the book so this table matches the crosswalk in the appendix rather than duplicating it.

### 4.6.16 Field Note - Follow the Administrative Pathway Backward

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

### 4.6.17 Chapter Summary

The clean source principle is therefore not a workstation-hardening recommendation. It is a method for discovering the true perimeter of administrative authority. Applied correctly, it exposes hidden Tier 0 systems, unsafe credential placements, untrusted deployment chains and pipelines, out-of-band control pathways, hybrid identity inversions, and recovery dependencies that ordinary identity diagrams fail to show.

For federal and Department of Defense environments, this carries direct mission significance. Identity systems determine which people, devices, services, and workloads the enterprise accepts as legitimate. If the systems administering those identity authorities cannot themselves be trusted, neither can the decisions produced by the identity infrastructure they effectively control.

The security boundary does not end at the domain controller, the Certificate Authority (CA), or the Identity Provider (IdP).

It ends at the least-trusted system still capable of changing them.

### 4.6.18 Chapter Concepts Review













