# ❌ Chapter 5 - Authentication, Authorization, and the Exercise of Trust

### Abstract

Chapter 5 examines how Active Directory converts an identity claim into an authenticated session and an authorization decision. It distinguishes authentication—the validation that a claimant controls an accepted credential—from authorization—the determination of what that authenticated identity may access, administer, or affect. The chapter explains why these functions must be analyzed together but governed separately: a strong authentication event does not justify excessive access, and a correctly assigned role does not compensate for a compromised credential or administrative session. It introduces the principal Active Directory mechanisms through which trust is exercised, including security principals, security identifiers, access tokens, groups, access-control lists, access-control entries, Kerberos, Lightweight Directory Access Protocol, service identities, and privileged roles. It also addresses the relationship between directory authorization and external decision points such as application roles, cloud services, certificate-based authentication, conditional access, and federation. The chapter applies the book’s effective-control model to authentication and authorization pathways, showing how delegated permissions, nested groups, service-account rights, token contents, and administrative access can create authority beyond a principal’s visible job role. Throughout, it emphasizes evidence, least privilege, protected administration, and recovery: defenders must be able to determine not only whether an identity authenticated successfully, but what authority it received, why it received it, and how that authority can be withdrawn after compromise.

### Key Terminology

* **Security principal:** An identity that can be authenticated and assigned permissions, such as a user, computer, group, service account, or managed service identity.
* **Security Identifier (SID):** A unique identifier used by Windows and Active Directory to represent a security principal in authorization decisions.
* **Authentication:** The process of validating that a claimant controls an accepted credential associated with an identity.
* **Authorization:** The process of determining what an authenticated identity is permitted to access, administer, or perform.
* **Access token:** A Windows data structure created for a security principal after authentication that contains identity and authorization information used in access checks.
* **Kerberos:** The primary authentication protocol used in Active Directory domains to establish authenticated sessions and issue tickets for access to services.
* **Key Distribution Center (KDC):** The domain-controller service that performs Kerberos authentication functions and issues Kerberos tickets.
* **Ticket-Granting Ticket (TGT):** A Kerberos ticket that allows an authenticated principal to request service tickets from the KDC.
* **Service ticket:** A Kerberos ticket issued to permit an authenticated principal to access a specific service.
* **Lightweight Directory Access Protocol (LDAP):** A protocol used to query and modify directory information, including Active Directory objects and attributes.
* **Group:** A directory object used to organize security principals and assign access through collective membership.
* **Nested group membership:** A relationship in which one group is a member of another group, allowing authority to be inherited indirectly.
* **Access-control list (ACL):** A collection of access-control entries associated with an object or resource that defines which principals may perform specified actions.
* **Access-control entry (ACE):** An individual rule within an ACL that grants, denies, or audits a specified permission for a principal.
* **Delegation:** The assignment of authority that permits one identity or group to administer defined objects, services, or functions without receiving unrestricted administrative privilege.
* **Service account:** An identity used by an application, service, task, or automation process to authenticate and perform work.
* **Managed service account:** A service identity whose password or credential lifecycle is managed by Active Directory or an associated service-management mechanism.
* **Privileged role:** A role, group membership, permission set, or administrative relationship capable of materially affecting sensitive systems or identity authority.

### 5.1 Authentication Establishes a Claim; Authorization Grants Consequence

Authentication establishes that a system accepts a claimant as an identity. Authorization determines what that identity is permitted to do after acceptance.

The distinction is basic, but identity incidents repeatedly demonstrate how easily it is blurred. An administrator may state that a user “has access” when the real question is whether the user authenticated successfully, whether the user’s group memberships were evaluated correctly, whether an application accepted an external identity assertion, whether a device or session condition was required, and which permissions the resulting identity actually received.

Each stage is a separate decision. Together, they create operational authority.

In an Active Directory environment, authentication commonly begins when a user, computer, service, or application presents a credential associated with a security principal. The domain’s authentication services validate that claim according to the credential type, the configured protocol, the identity record, and the conditions of the request. The resulting session can then be used to obtain access to network services, applications, files, management interfaces, and other protected resources.

Successful authentication does not, by itself, grant unlimited access. It establishes a basis on which authorization decisions may be made.

Those decisions can occur in several places. Windows may evaluate the identity’s access token against the access-control list on a file, registry key, service, or other securable object. An application may evaluate Active Directory group membership against an internal role model. A cloud service may evaluate an identity claim, device condition, assigned role, and session risk. A management platform may accept a privileged identity while separately determining whether the administrator is authorized to perform a specific action.

The directory is central to many of these decisions because it stores and distributes identities, group memberships, permissions, service attributes, and relationships that other systems consume. It is not always the final decision point.

That distinction matters for defense. Resetting an Active Directory password may invalidate one authentication mechanism while leaving an issued certificate, an active cloud session, a service token, an application-managed entitlement, or another credential pathway unaffected. Removing a user from one directory group may not remove access if the application relies on a separate role assignment or if nested memberships continue to grant equivalent authority.

Containment must follow the actual access path, not the first identity object responders find.

A useful way to analyze any access decision is to separate four questions:

1. **Who or what is making the claim?**\
   The claimant may be a person, device, application, service, automation process, or external identity provider acting through an assertion.
2. **What credential or evidence supports the claim?**\
   The evidence may be a password, smart card, certificate, Kerberos ticket, cryptographic key, token, federation assertion, or managed service credential.
3. **Which authority validates the claim?**\
   The validating authority may be an Active Directory domain controller, certificate authority, cloud identity provider, federation service, application identity store, or another trusted component.
4. **What authority follows from successful validation?**\
   The result may be limited access to one resource, broad membership in a role, local administrative control, the ability to change policy, or effective control over another identity system.

The first three questions concern authentication. The fourth concerns authorization and consequence.

An attacker may seek to compromise any point in this chain. Theft of a credential can allow impersonation of the claimant. Compromise of the validating authority can allow false claims to be accepted. Manipulation of group membership, permissions, application roles, or policy can expand the authority that follows legitimate authentication. Compromise of a privileged endpoint can allow an attacker to act within an already authenticated session.

This is why strong authentication is essential but cannot carry identity defense alone.

A CAC or PIV credential can provide a strong basis for proving control of an identity. Kerberos can provide mutual authentication and ticket-based access to domain resources. Certificate validation can establish cryptographic trust. Multifactor authentication can reduce the value of a stolen password. None of these mechanisms alone establishes whether the resulting access is appropriate, limited, observable, or recoverable.

The authorization model must remain subject to the same discipline as credential management.

A group grants authority because a resource owner, system administrator, or application has been configured to recognize that group. An access-control entry grants authority because the object owner or delegated administrator has allowed it. A privileged role grants authority because a management system accepts it. An application role grants authority because the application interprets an identity attribute, group, or assertion in a particular way.

Every authorization mechanism represents a decision about trust.

The defender’s responsibility is to determine whether those decisions reflect current mission need and whether lower-trust identities can influence them. A user who is not a member of a visibly privileged group may still control a group that is nested into one. A service account may lack broad directory rights while possessing access to an application that can alter sensitive authorization data. An endpoint-management platform may not authenticate as a domain administrator but may be able to deploy a policy that affects the workstation of one.

Formal role names are useful. Effective control remains the governing measure.

The next sections examine the specific mechanisms through which Active Directory performs these functions. They begin with security principals, security identifiers, and access tokens—the core structures through which Windows represents identity and carries authorization information into an access decision.

### 5.2 Security Principals, SIDs, and Access Tokens: How Windows Represents Authority

Windows does not make authorization decisions primarily from a username. It makes them from the security identifiers and authorization data associated with the authenticated security principal.

A security principal is an entity that the operating system or a directory can authenticate and assign permissions. In an Active Directory environment, common security principals include users, computers, security groups, service accounts, managed service accounts, and, in some contexts, application or workload identities. Each principal represents a potential actor in the environment: a person signing in, a computer establishing a domain relationship, a service performing work, or a group receiving collective authority.

The visible name of a principal is useful to people. The Security Identifier, or SID, is what gives the principal durable meaning to Windows authorization.

A SID is a unique identifier assigned to a security principal. When an administrator grants a group permission to a file share, a directory object, a service, or another securable resource, the system records the relevant SID in the associated access-control information. When a user’s name changes, the SID generally continues to represent the same underlying principal. This allows an organization to rename accounts, reorganize teams, or apply naming conventions without requiring every resource permission to be recreated.

The same persistence creates an important defensive requirement: identity governance must track more than names.

An account with a familiar name may have been deleted and recreated as a different principal. A renamed group may retain permissions whose original purpose is no longer apparent. A migrated identity may carry historical relationships that require review. An access-control entry may display an unresolved SID when the associated account or domain is no longer available, yet that entry can still represent a meaningful authorization condition in the environment.

The defender must be able to connect the human-readable identity, the SID, the authority assigned to that SID, and the lifecycle history that explains why the authority exists.

This is especially important in mature federal enterprises, where domains may have been consolidated, systems migrated, contractors replaced, applications inherited, or mission organizations reorganized over many years. A permission that appears obscure may be an expected legacy dependency. It may also be unreviewed authority preserved long after the system, organization, or access requirement that created it has changed.

A SID is not evidence that access remains justified. It is evidence that a principal was once assigned authority.

#### 5.2.1 Security Principals Carry Different Kinds of Risk

Not all security principals represent the same kind of authority.

A user account commonly represents an individual person. Its lifecycle should be associated with proofing, sponsorship, assignment, credential issuance, access approval, periodic review, and termination or reassignment. A computer account represents a domain-joined device and participates in domain authentication, policy processing, and machine-level access decisions. A service account represents a noninteractive function performed by an application, service, task, or automation process. A group represents a collective authorization mechanism whose membership can affect many users or systems at once.

Each identity type should have a distinct ownership and monitoring model.

A user account may require review when the individual changes roles. A computer account may require review when the device is rebuilt, moved to another enclave, loses management support, or is decommissioned. A service account may require review when the application changes, the credential is rotated, the hosting platform is replaced, or the account receives new permissions. A group may require review whenever its scope, nesting, owners, membership-management process, or recognized resources change.

Treating all of these as ordinary “accounts” obscures their different authority pathways.

A service account illustrates the point. It may never support an interactive human logon, but it can still authenticate to databases, web services, file shares, management interfaces, certificate services, cloud applications, or directory resources. It may hold a password, certificate, managed credential, cryptographic key, or secret stored in a configuration system. The service account’s effective authority depends on what it can access and on who can influence its credential, configuration, host, or execution context.

A service account without a named human owner is not autonomous. It is an unaccountable authority relationship.

Computer accounts require similar attention. A domain-joined system establishes a machine identity with the domain and may receive policy, access resources, perform service operations, or host credentials used by people and applications. If the system is a privileged administrative workstation, domain controller, identity synchronization server, certificate authority, or management platform, compromise of its computer identity or operating environment may have consequences far beyond those of an ordinary endpoint.

The risk follows the authority exercised through the principal, not the type of object displayed in the directory console.

#### 5.2.2 Groups Convert Membership Into Collective Authority

Groups allow organizations to manage authorization at scale. Rather than granting a separate permission to every individual account, a resource owner can grant authority to a group and manage membership according to the role, mission, or function represented by that group.

This is necessary for enterprise operation. It is also a major source of indirect authority.

When a user becomes a member of a group, the resulting access may extend to many resources that recognize the group’s SID. The user may not know every system that evaluates that membership. The group owner may not know every permission assigned to the group. An application owner may not know that the group is nested within another group that grants broader authority. These gaps make it possible for a seemingly modest membership change to alter effective control in ways that are not visible from a single system.

Nested groups amplify that effect.

A group can be a member of another group, allowing authority to be inherited through several relationships. This supports scalable role design, but it also requires careful analysis. A user may not belong directly to a highly privileged group while still receiving equivalent authority through one or more nested memberships. Likewise, a principal able to modify the membership of a lower-level group may be able to influence a higher-level authorization decision indirectly.

The relevant question is not only, “Who belongs to this privileged group?” It is also, “Which groups, identities, permissions, and administrative relationships can cause a principal to become effectively represented in this group’s authority?”

That question is central to Tier 0 analysis.

A group does not need an obviously privileged name to be consequential. It may grant local administrative rights on a management server, modification rights over a Group Policy Object, access to a certificate-enrollment function, use of a privileged remote-access platform, or control over a service account. Each relationship can become part of an authority pathway toward a more sensitive identity system.

Group review should therefore consider four dimensions:

* the identities and groups that are members;
* the resources and permissions that recognize the group;
* the identities and groups allowed to modify its membership or attributes; and
* the nested relationships through which its authority is inherited or extended.

A group that cannot be explained across those four dimensions is not adequately governed.

#### 5.2.3 The Access Token Carries Authority Into the Session

After successful authentication, Windows creates an access token for the resulting session. The access token contains information used by the operating system to evaluate authorization decisions, including the SID of the authenticated principal, applicable group SIDs, privileges, integrity-related information, and other context relevant to access checks.

The token is the operational representation of authority during the session.

When a user or process attempts to access a protected object, Windows compares the information in the access token with the object’s access-control list. If the token contains a SID granted the required permission, and no applicable restriction prevents the action, the system can permit access. If the token does not satisfy the access-control requirements, access is denied.

This process explains why group membership matters only when the resulting authorization information is recognized in the session and by the destination resource. It also explains why containment actions can require more than changing a directory object.

Removing a user from a group changes the directory’s current membership state. Existing sessions may retain authorization context until they are ended, refreshed, or otherwise re-evaluated according to the relevant service and session behavior. Active application sessions, issued tokens, cached credentials, remote connections, and service processes may each have their own lifecycle. A defender responding to a suspected compromise must consider not only what the directory now says, but also which active sessions or credentials may continue to represent prior authority.

Revocation is an operational process, not just a directory edit.

For privileged activity, this reality reinforces the value of short-lived, controlled administrative sessions; separate privileged identities; hardened administrative endpoints; explicit session termination during containment; and logging that allows the organization to determine where a principal has authenticated and what authority may still be active.

The objective is to reduce the interval during which a change in authorization state leaves prior authority usable.

#### 5.2.4 Authorization Is Distributed Beyond the Token

The Windows access token is a foundational authorization mechanism, but it is not the only one. Applications may maintain internal roles. Cloud services may evaluate tokens and claims independently of Windows resource access. Network devices, databases, certificate services, endpoint-management platforms, and mission applications may use their own authorization models while relying on Active Directory groups, certificates, or federated assertions as input.

A successful Windows logon therefore does not fully describe a user’s authority, and a group review does not necessarily capture every entitlement.

The defender must identify where the decision is actually made. Does the resource evaluate a Windows token and an ACL? Does the application map an Active Directory group to a local role? Does it accept a federated claim? Does it rely on a certificate subject, an attribute, a cloud role, or an internal authorization database? Which administrators can alter that mapping? Which logs record the decision and its associated changes?

These questions prevent a common containment error: removing access in one authority system while leaving an equivalent path active in another.

A user removed from a directory group may retain an application-managed role. A cloud account may retain a session or role assignment independent of on-premises group membership. A service identity may retain a certificate usable for authentication after a password change. An application may continue using cached authorization data until its own refresh process occurs.

The identity trust system must be understood as a set of connected decision points, not a single directory lookup.

Security principals, SIDs, groups, and access tokens provide the structures through which Windows represents and applies authority. The next section examines access-control lists, access-control entries, and delegated administration: the mechanisms through which that authority is assigned, constrained, and too often expanded without adequate visibility.

### 5.3 Access Control, Delegation, and the Hidden Paths to Authority

Authorization is often visible at its final point of enforcement: a user can open a file, administer a server, modify a directory object, approve an action, or access an application. The path that produced that authority is often less visible.

In Windows and Active Directory environments, that path is commonly expressed through access-control lists, access-control entries, inheritance, object ownership, group membership, delegated administration, and the systems capable of modifying those relationships. These mechanisms are necessary for enterprise operation. They allow an organization to distribute administrative work without giving every administrator unrestricted control of the domain or forest.

They also create some of the most important hidden paths to authority.

An access-control list, or ACL, is associated with a securable object and contains the rules that govern access to that object. An access-control entry, or ACE, is an individual rule within the ACL. It identifies a security principal and specifies permissions that may be granted, denied, or audited. The object may be a file, folder, registry key, service, printer, directory object, certificate template, Group Policy Object, application resource, or another component capable of enforcing access control.

The mechanism is straightforward. The consequences may not be.

A permission assigned directly to a user can be relatively easy to identify. A permission inherited through several containers, granted to a group nested inside another group, delegated over a collection of directory objects, or exercised through an application or service account can be much harder to recognize. The resulting authority may not appear in a simple privileged-group review even though it permits an identity to alter a more sensitive principal, policy, credential, or system.

This is why access control must be evaluated as a relationship, not as a collection of isolated permission entries.

#### 5.3.1 Access-Control Lists Express Administrative Authority

In Active Directory, ACLs govern more than ordinary data access. They can determine who may create, modify, delete, reset, move, protect, or otherwise influence directory objects and their attributes.

Those permissions may apply to a specific user, computer, group, organizational unit, Group Policy Object, certificate-related object, or broader category of directory object. They may be inherited by descendant objects. They may grant broad control or narrowly scoped rights. They may be assigned directly, through groups, through delegated administration, or through ownership relationships.

The operational value is clear. A help-desk team may need authority to reset passwords for a defined user population. A server-management group may need to create and maintain computer accounts in a particular organizational unit. An application team may need the ability to update attributes associated with a service. A PKI team may need authority over certificate templates or enrollment configuration. A security team may need read access to investigate objects without receiving the ability to change them.

The security risk arises when the permission scope exceeds the mission function.

A group granted authority to reset passwords may be appropriately constrained to ordinary user accounts. The same authority becomes materially more sensitive if the group can reset passwords for service accounts, privileged administrators, accounts with elevated directory rights, or identities used to manage sensitive systems. A team granted authority to manage computer objects may require careful limits if the affected objects participate in privileged administration, certificate services, synchronization, or other high-impact functions.

The permission name alone does not determine its risk. The target of the permission does.

A right that is appropriate over one organizational unit may be unsafe over another. An ability to modify a group may be low consequence when the group controls a routine application role and high consequence when the group grants local administration to privileged workstations or indirect control over Tier 0 systems. An ability to modify an attribute may appear narrow but become significant when that attribute affects authentication, service identity, delegation, certificate issuance, or synchronization.

Defenders must therefore ask two questions together:

> _What can this principal modify?_

> _What authority follows from the modification?_

The first question identifies the direct permission. The second identifies effective control.

#### 5.3.2 Delegation Is Necessary; Unbounded Delegation Is Dangerous

Delegation allows an organization to distribute defined administrative responsibilities without granting broad domain or forest administration. It is a necessary design pattern in large environments. Central identity teams cannot perform every password reset, computer join, group update, account lifecycle action, application integration, or local support function across the enterprise.

The objective of delegation is controlled administration.

A well-designed delegation model ties authority to a defined mission function, limits it to the objects and attributes required for that function, assigns accountable ownership, preserves evidence of changes, and prevents the delegated principal from influencing identities or systems outside the intended scope.

An unsafe delegation model does the opposite. It grants broad authority for convenience, relies on poorly understood inheritance, permits administration across mixed-trust object populations, leaves ownership unclear, or allows lower-trust identities to influence higher-trust authority indirectly.

The distinction is not academic. A delegated right may be the difference between a constrained support role and a pathway to enterprise compromise.

For example, an organization may delegate management of an organizational unit containing ordinary user accounts. That delegation can be defensible when the unit’s scope, object types, administrative tasks, and protected identities are carefully controlled. The same delegation becomes risky if privileged accounts, service accounts, administrative groups, or sensitive computer objects reside in the same container and inherit the same administrative exposure.

Administrative convenience can create authority mixing.

This is one reason privileged identities and systems require deliberate placement and protection. Their security boundary should not depend solely on a naming convention or a group label. The organization must ensure that the organizational units, ACLs, management workflows, and inheritance structures surrounding those identities do not permit lower-trust administrators to change the conditions under which privileged access is granted.

A privileged account placed in an ordinary user container may inherit ordinary user administration. A sensitive service identity placed with application accounts may be exposed to a team whose authority was intended only for routine lifecycle support. A Group Policy Object linked to a privileged system population may be modifiable by a group whose broader endpoint-management role was never intended to reach Tier 0.

The directory structure matters because it can carry administration along with organization.

#### 5.2.3 Inheritance Makes Authority Easy to Apply—and Easy to Misunderstand

Inheritance allows permissions assigned to a parent object or container to apply to child objects. It reduces repetitive configuration and supports consistent administration across a defined scope. It can also make an authority pathway difficult to identify because the resulting permission may not be visibly assigned on the affected object itself.

An administrator reviewing a sensitive account may see no direct permission granting another group control. The authority may instead be inherited from an organizational unit, a parent container, a delegated administration group, or a permission assigned to a broader class of objects. The affected principal may also be protected from inheritance in some respects while remaining exposed through another relationship.

This complexity does not make inheritance inherently unsafe. It makes casual assumptions unsafe.

A security review must identify the effective permissions on consequential objects, the source of those permissions, the groups and identities receiving them, the scope over which they apply, and the administrative purpose that justifies them. The review must also determine whether the same effect can be achieved through ownership, group-management rights, policy administration, service control, or another indirect mechanism.

The concern is not whether an ACL looks clean in one console. The concern is whether a lower-trust principal can cause a higher-trust object to change.

A directory object can be altered in more ways than by a broad “full control” permission. A principal may have authority over a specific attribute, permission to reset a password, ability to modify group membership, authority to alter an object’s security descriptor, control of the object owner, or access to an administrative tool that performs those actions through another identity. Each relationship should be evaluated according to the result it permits.

Narrow permissions can produce broad consequences.

#### 5.2.4 Object Ownership Is Authority That Requires Review

Object ownership is often overlooked in routine access reviews. Yet an owner can hold meaningful influence over the security configuration of an object, depending on the object type, platform behavior, and associated permissions.

In practical terms, ownership can become a route by which a principal changes access control over an object and then grants additional authority. The exact implications must be evaluated in context, but the defensive principle is consistent: ownership of a sensitive object is not a cosmetic attribute. It is an administrative relationship.

Organizations should identify the owners of consequential directory objects, Group Policy Objects, certificate templates, privileged groups, service identities, and other authority-bearing resources. They should be able to explain why that owner holds the relationship, whether the ownership is current, who can change it, and what monitoring records its modification.

An object with an unknown, departed, inactive, or inappropriate owner is a governance problem even if its visible permissions appear correct.

Ownership review becomes particularly important after migrations, reorganizations, incident remediation, application retirement, and emergency changes. These events can leave behind technical relationships that remain valid in the directory while losing their operational justification.

#### 5.2.5 Group Management Is Often Delegated Privilege Management

The ability to change group membership is itself an authorization function. A principal permitted to add members to a group can influence every resource that recognizes that group. If the group is nested into another group, grants local administration, controls an application role, or receives delegated directory rights, the authority may be far greater than the group name suggests.

For this reason, the organization should treat high-impact group management as privileged administration even when the person making the change is not a member of a visibly privileged group.

A help-desk function may legitimately manage membership in a routine access group. That function should not automatically extend to groups that grant elevated access, influence sensitive systems, control administrative endpoints, or provide a pathway to Tier 0. The distinction must be reflected in the delegation model, approval workflow, logging, and review process.

The security review should identify not only who belongs to a privileged group, but also:

* who can add or remove members;
* who can modify the group’s attributes or ownership;
* which groups can be nested within it;
* which groups it is nested within;
* which automation processes can alter membership; and
* which systems consume the group for authorization.

A group may be well governed at the membership level while remaining vulnerable through an overlooked administrative permission or automated workflow. Conversely, a carefully restricted group can be undermined if an application, synchronization process, or management platform can modify the underlying identity attributes that determine membership.

Authority must be reviewed at the point where it can be changed.

#### 5.2.6 Delegation Requires Evidence and Validation

Delegated administration is defensible only when the organization can establish that it is purposeful, bounded, observable, and recoverable.

Purposeful means that the delegated right supports a defined mission or operational function. Bounded means that the scope does not extend beyond the objects, attributes, systems, and time period required for that function. Observable means that the organization can identify who exercised the right, from which administrative system, against which object, and with what result. Recoverable means that the organization can remove or reverse the delegated authority and validate that the affected systems now recognize the corrected state.

These conditions should be assessed whenever a new delegation is proposed and periodically for existing delegations.

The analysis should not stop with a statement that a team _“needs access.”_ It should identify the precise action required, the object population affected, the identity or group receiving the authority, the source endpoint or management system from which it will be used, the approval authority, the events that record its use, and the review process that determines whether the delegation remains necessary.

This level of specificity is not bureaucracy. It is the difference between controlled delegation and an untracked path to authority.

During an incident, delegated permissions deserve immediate attention because they can provide persistence that is less conspicuous than a new privileged-group membership. An attacker who gains the ability to alter a group, reset a sensitive account password, modify a policy object, change an access-control entry, or control an automation identity may retain a durable route back into the environment without creating an obvious new administrative account.

Defenders must therefore examine whether the attacker could have changed the relationships through which authority is granted—not only the accounts that visibly hold that authority.

Access control and delegation are where an organization’s identity design becomes operational. They determine whether administrative power is narrowly assigned or quietly accumulated, whether authority is visible or inherited invisibly, and whether compromise of one identity can influence another.

The next section examines Kerberos, the core Active Directory authentication service through which identity claims become tickets, sessions, and access to domain resources.

### 5.4 Kerberos: Authentication Tickets and the Duration of Trust

Kerberos is the primary authentication protocol used in Active Directory domains to establish authenticated sessions and permit access to domain resources.

Its purpose is to allow a user, computer, service, or other security principal to prove its identity to trusted services without repeatedly transmitting a reusable password across the network. Instead, Kerberos relies on tickets issued by a domain controller acting as the Key Distribution Center, or KDC. Those tickets represent time-bounded evidence that the KDC has authenticated the principal and, where appropriate, authorized access to a requested service.

For defenders, Kerberos is not simply a background protocol supporting logon. It is a central mechanism through which the directory turns identity into usable authority.

The process begins when a principal authenticates to the domain. The KDC validates the authentication request and issues a Ticket-Granting Ticket, commonly called a TGT. The TGT allows the authenticated principal to request additional tickets for particular services without performing the full authentication process again for every resource.

When the principal needs to access a service, it requests a service ticket for that destination. The KDC evaluates the request and issues a ticket associated with the service identity. The client presents that service ticket to the destination, which can validate the ticket and make its own authorization decision about the requested access.

This structure separates several related functions:

* the initial validation of the claimant;
* the KDC’s issuance of time-limited ticketing authority;
* the issuance of a ticket for a defined service;
* the service’s validation of the ticket; and
* the service’s authorization decision after authentication succeeds.

A successful Kerberos exchange establishes an authenticated basis for access. It does not eliminate the need for authorization controls at the resource.

A user may receive a valid service ticket for an application and still be denied a sensitive action because the application’s role model does not grant it. Conversely, a highly privileged user may authenticate correctly but should not be able to reach an administrative resource from an unapproved device, session, or network path if the environment is designed to constrain privileged operations appropriately.

Kerberos establishes trust in identity. The surrounding architecture determines the consequence of that trust.

#### 5.4.1 The KDC Is an Authority-Bearing Function

In an Active Directory domain, the KDC function operates on domain controllers. This gives domain controllers a central role in authentication: they validate principals, issue Kerberos tickets, and provide the ticketing authority on which many domain-integrated services depend.

The KDC must therefore be protected according to the authority it conveys.

A compromise affecting the integrity of a domain controller can affect more than the accounts stored in the directory database. It can affect the organization’s ability to rely on Kerberos authentication itself. If an attacker can influence the credentials, ticketing keys, policies, or administrative functions associated with the KDC, the attacker may be able to create, obtain, or misuse trusted authentication material in ways that are difficult to distinguish from ordinary domain activity.

This is why domain controllers belong at the center of the Tier 0 boundary. Their importance is not based only on their server role. They participate directly in establishing the authenticated sessions through which users, services, and administrators reach the rest of the enterprise.

The same reasoning applies to systems and identities capable of effectively controlling domain controllers. A management platform that can deploy configuration to a domain controller, an administrative workstation from which privileged sessions are established, a backup system holding recovery material, or an identity with delegated rights over critical directory functions may not operate the KDC directly. Yet each can influence the conditions under which Kerberos trust is created.

Effective control remains the appropriate security measure.

#### 5.4.2 Service Principal Names Bind Services to Identity

Kerberos relies on service identities to determine which service a ticket is intended to reach. In Active Directory, this relationship is represented through Service Principal Names, or SPNs.

An SPN associates a service instance with the account under which that service operates. It gives the KDC a way to identify the service principal for which a service ticket should be issued. The service may operate under a computer account, a dedicated service account, a managed service account, or another account structure appropriate to its design.

The technical purpose is service identification. The security consequence is that SPN administration can affect authentication authority.

An incorrectly configured SPN can produce failed authentication, duplicate-identity conditions, unexpected service behavior, or reliance on alternate authentication methods. A service identity that is poorly governed can become a credential-management risk. An identity permitted to alter a high-value service’s SPNs, credentials, or configuration may be able to influence how clients obtain and present authentication tickets for that service.

Service identities should therefore be treated as authority-bearing objects, particularly when they support administrative platforms, directory-connected applications, databases containing sensitive data, certificate services, synchronization systems, or services used by privileged operators.

The organization should be able to answer basic questions for every consequential service identity:

* What service does this identity represent?
* Which hosts use it?
* Which SPNs are associated with it?
* Which systems accept tickets issued for it?
* Who can modify its credentials, attributes, SPNs, or permissions?
* Where does it authenticate, and what authority follows?
* How is its credential rotated, monitored, suspended, and recovered?

An account that cannot be explained across those questions is not simply difficult to administer. It is an unbounded trust dependency.

#### 5.4.3 Tickets Are Time-Bounded, Not Automatically Harmless

Kerberos tickets are designed to be valid for defined periods rather than indefinitely. This limits the need for repeated authentication while providing a mechanism for periodic renewal and re-evaluation. It also creates an operational reality that matters during containment: authority already represented in an active ticket or session may continue for some time after a directory change is made.

Disabling an account, removing group membership, resetting a password, or changing a permission can be essential response actions. Their effect on active access depends on the service, the type of session, the ticket lifecycle, the client behavior, the destination’s authorization model, and whether existing connections remain active.

The principle is broader than any one Kerberos setting:

> _Revoking future authority does not always terminate authority that has already been issued._

This is why identity incident response must account for active sessions and not only for directory state. Responders may need to identify where a compromised identity authenticated, which administrative or application sessions remain active, which service tickets could still be valid, and what additional actions are needed to terminate or constrain access at the affected endpoints and services.

The purpose is not to assume that every ticket remains dangerous after every account change. The purpose is to avoid declaring containment complete based solely on a directory update whose operational consequences have not been validated.

This is especially important for privileged identities. A privileged administrator may have active sessions to domain controllers, management systems, cloud portals, certificate services, network devices, or mission applications. If the associated endpoint or session is compromised, changing the account’s directory attributes without addressing the active session can leave the attacker in possession of already established authority.

Privileged access should therefore be designed to limit session duration, isolate administrative activity, record high-impact sessions, and provide tested procedures for ending or re-establishing them during an incident.

#### 5.4.4 Kerberos Depends on Time, DNS, and Network Integrity

Kerberos authentication depends on conditions beyond the KDC and the credential. Time synchronization, DNS-based service location, network connectivity, domain-controller reachability, and service configuration all influence whether the protocol can function correctly.

Time is especially important because Kerberos tickets include validity information intended to limit replay and misuse. Significant disagreement among system clocks can prevent normal authentication or produce misleading operational symptoms. A time problem may appear to users as an access failure while affecting administrators as a broader inability to establish trusted sessions.

Time synchronization is therefore not merely a server-maintenance concern. It is a dependency of authentication assurance.

DNS is equally significant. Clients use service-location records to find appropriate domain controllers and KDCs. Incorrect, unavailable, or manipulated DNS information can prevent ticket acquisition, direct clients toward unintended services, or create dependencies on remote domain controllers during an outage or degraded condition. The DNS and site-design principles discussed in Chapter 3 therefore have direct consequences for Kerberos availability and observability.

Network segmentation must also be designed with authentication in mind. A boundary that prevents unnecessary access to domain controllers can reduce exposure. A boundary that inadvertently blocks required authentication, ticketing, service-discovery, or time-synchronization paths can impair mission operations and drive users or administrators toward unsafe workarounds.

The objective is deliberate, observable connectivity—not maximum reachability and not accidental isolation.

#### 5.4.5 Delegation Requires Explicit Trust Boundaries

Kerberos supports delegation patterns that allow a service to act on behalf of a user under defined conditions. These patterns can enable legitimate multi-tier applications, service workflows, and integrated authentication scenarios. They can also create high-impact authority pathways when the delegation relationship is broader than its mission purpose or poorly governed.

The central security issue is not whether delegation exists. It is what authority the delegated service may exercise, on whose behalf, toward which resources, and under what technical and administrative constraints.

A service that can act on behalf of users to a limited, defined backend may be performing a necessary mission function. A service that can use delegated authority broadly across sensitive resources may become a valuable target because compromise of the service could allow an attacker to extend a user’s authority beyond the system initially compromised.

Delegation design should therefore identify the service owner, the supported mission workflow, the identities involved, the destinations permitted, the administrative identities capable of changing the configuration, the evidence produced by use of the delegation path, and the recovery actions required if the service is compromised.

Delegation is not a binary feature to enable or disable casually. It is a trust relationship that must be bounded according to consequence.

This is particularly important when a service bridges trust zones. A web application, identity gateway, management platform, or automation service may receive requests from a lower-trust user population and then contact a higher-trust backend. The service becomes an enforcement point. Its credential protection, code integrity, administrative control, logging, and network placement must be evaluated according to the authority it can carry across the boundary.

A service that bridges trust boundaries should be protected as part of the more consequential boundary.

#### 5.4.6 Kerberos Visibility and Detection

Kerberos activity is common in an Active Directory environment. Many ticket requests are routine and necessary. A useful detection program does not attempt to treat every ticketing event as suspicious. It focuses on context that may indicate a change in authority, unusual use of credentials, or access inconsistent with the identity’s normal role.

High-value investigative questions include:

* Which identity requested the ticket, and from which endpoint?
* Which domain controller issued it?
* Which service identity and destination were involved?
* Was the request consistent with the identity’s expected function?
* Did the same identity recently receive elevated group membership, a new certificate, or a modified delegation relationship?
* Did the activity originate from an unmanaged, unexpected, or lower-trust administrative endpoint?
* Is the request part of a sequence that moves toward privileged services or identity infrastructure?

The organization should correlate Kerberos evidence with directory changes, service-account events, endpoint telemetry, DNS activity, privileged-session records, and application logs. A ticket request is often meaningful only when interpreted alongside the authority relationship that made the request possible.

For example, a service ticket for a management system may be expected from a designated privileged-access workstation during an approved maintenance period. The same request from a general-purpose endpoint, following an unusual group change or service-account modification, merits a different investigation even if the authentication itself succeeded according to protocol.

The protocol can validate a credential. It cannot determine whether the resulting use of authority is legitimate.

#### 5.4.7 Recovery of Kerberos Trust

When an incident affects high-privilege Kerberos authority, recovery must address more than the first compromised account. The organization must determine whether ticketing keys, privileged credentials, service identities, delegation relationships, active sessions, authentication policies, domain-controller integrity, or supporting infrastructure may have been affected.

The appropriate recovery scope depends on evidence and effective control. It may involve resetting credentials, ending sessions, reviewing service accounts, validating SPNs and delegation settings, rebuilding affected endpoints, verifying domain-controller trustworthiness, and increasing monitoring for reuse of compromised identity material.

The key question is not, _“Are Kerberos services running?”_ It is, _“Can the organization again trust the authority through which Kerberos tickets are issued and used?”_

Kerberos provides a resilient and efficient foundation for domain authentication. It also concentrates trust in the KDC, service identities, ticketing relationships, and administrative systems that support them. The next section examines LDAP and directory access: the mechanisms through which identities, applications, and administrators query and modify the directory information underlying those authentication and authorization decisions.

### 5.5 LDAP and Directory Access: Reading and Changing the Source of Authority

Lightweight Directory Access Protocol, or LDAP, is one of the primary mechanisms through which users, systems, applications, and administrative tools read and modify Active Directory information.

That information includes far more than names and email addresses. Active Directory stores user and computer objects, group memberships, organizational units, service-related attributes, access-control information, authentication-relevant data, policy relationships, and administrative configuration. LDAP is therefore not simply a directory-query protocol. It is a means of interacting with the information from which many authentication, authorization, and administrative decisions are derived.

A request to read directory information can be routine and necessary. Applications use directory queries to find users, groups, devices, and attributes. Domain services use directory information to support authentication and authorization. Administrative tools use LDAP to locate objects, review configuration, and perform approved changes. Security teams may query the directory to investigate identity relationships, verify permissions, or identify systems affected by an incident.

The security significance depends on the access requested and the authority of the identity making the request.

A read-only query may reveal information that helps an attacker understand the environment: identity naming conventions, group relationships, service accounts, computer objects, organizational structure, certificate-related attributes, and administrative dependencies. A write operation may create, alter, or remove directory information that changes effective authority. The protocol is the same; the consequence is not.

LDAP should therefore be analyzed as both a **visibility mechanism** and an **authority mechanism**.

#### 5.5.1 Directory Queries Reveal the Shape of the Environment

Active Directory is designed to be discoverable enough for authorized systems and users to function. A user needs to find a printer, a file server, a group, a colleague, or a service. An application may need to locate users matching an approved attribute or determine whether an account belongs to a group. An administrator may need to identify which computers reside in an organizational unit or which accounts are subject to a particular policy.

This legitimate discoverability creates an operational challenge for defenders. Identity information that appears harmless in isolation can reveal meaningful relationships when assembled: which accounts are privileged, which groups control sensitive systems, which service identities support key applications, which organizational units receive delegated administration, and which objects may be connected through ownership or permissions.

The defensive objective is not to make the directory unusable through indiscriminate restriction. It is to understand what information is available to which identities, what mission function justifies that availability, and what unusual query behavior may indicate an attempt to map authority pathways.

The context of directory access matters more than the fact that an LDAP query occurred.

A directory-services administrator performing a targeted query from a privileged administrative endpoint during approved maintenance may be acting normally. A standard user account performing broad, repeated searches for administrative groups, service accounts, delegation attributes, or high-value computer objects from an atypical endpoint presents a different investigative context. The query itself may be technically permitted. Its scope, timing, source, identity, and relationship to other activity determine whether it warrants attention.

This is consistent with the book’s larger visibility model. An attacker seeks enough information to identify one viable route to greater authority. The defender must be able to recognize when ordinary directory access begins to resemble systematic discovery of the identity control plane.

#### 5.5.2 LDAP Write Access Is Administrative Authority

The greater risk arises when an identity can modify directory information.

LDAP write operations can create accounts, change attributes, modify group memberships, update service-related information, alter organizational-unit contents, change access-control entries, and perform other actions that affect how the directory represents trust. The exact authority exercised depends on the object, the attribute, the access-control model, the administrative tool, and the identity or service account performing the operation.

An LDAP write is therefore not inherently suspicious. Directory administration depends on approved writes. The security question is whether the identity performing the write was authorized to make that change and whether the resulting change expanded effective control beyond its intended purpose.

A help-desk group may have a legitimate need to update selected attributes or reset passwords for a limited population. An application workflow may require the ability to provision accounts in a defined organizational unit. An identity-governance platform may update group memberships based on approved lifecycle events. A synchronization service may write authoritative attributes from one environment into another.

Each of these functions can be necessary. Each also represents an authority relationship that must be bounded, monitored, and recoverable.

The organization should be able to explain, for every consequential LDAP write path:

* which identity, service, or workflow performs the update;
* which objects and attributes it may alter;
* what source information or approval authorizes the change;
* what technical controls constrain the scope;
* what evidence records the operation; and
* how the organization reverses or validates the change if it is later found to be incorrect or unauthorized.

A directory write without a clear answer to those questions is not routine administration. It is ungoverned authority.

#### 5.5.3 Attributes Can Carry More Consequence Than Their Names Suggest

Some directory attributes have an obvious security meaning. Group membership, account status, password-related data, security descriptors, and service identities naturally attract attention. Other attributes may appear operational or application-specific while still influencing authentication, authorization, delegation, synchronization, certificate enrollment, or service behavior.

The defender must avoid judging an attribute solely by its name.

An attribute may be used by an application to assign a role. It may be consumed by a synchronization service to determine whether an account is provisioned or granted access in another environment. It may influence a certificate-enrollment workflow, identify a service principal, control where a policy applies, or establish an administrative relationship in a management platform. A modification that appears minor in Active Directory Users and Computers may have a substantial consequence in a dependent system.

This is why identity-change reviews require application and service context. Directory engineers can identify the object and attribute that changed. Mission and application owners may be needed to explain what the change means downstream. Security teams must connect both views to determine whether effective authority has expanded.

The object is not the whole decision. The systems that consume its attributes are part of the authority pathway.

#### 5.5.4 LDAP Security Depends on Authentication, Encryption, and Source Control

Directory access should be protected according to the sensitivity of the information and operations involved. An identity system cannot rely on unauthenticated or weakly protected directory communication for consequential administrative functions. Authentication of the client, protection of the connection, validation of the destination, and restriction of administrative sources all contribute to a trustworthy LDAP operating model.

For ordinary operations, the organization must determine which applications, services, users, and endpoints require directory access; whether they use approved authentication methods; whether sensitive queries or writes are protected in transit; and whether the directory services they contact are the intended authorities.

For privileged operations, the standard should be higher. Administrative directory changes should originate from managed, monitored endpoints and approved management paths. Service identities used for directory integration should have narrowly scoped permissions and protected credentials. Applications should not receive broad directory-write authority merely because a specific provisioning or lookup function is convenient to implement through a powerful account.

The guiding design principle is simple: grant the smallest practical directory authority to the smallest practical set of identities, from the most controlled practical sources.

This principle reduces the consequence of a compromised application, workstation, automation process, or service account. It also makes monitoring more useful. A directory write from a narrowly designated identity and management path is easier to recognize as expected or unexpected than a write that could originate from dozens of broadly privileged systems.

#### 5.5.5 LDAP, Application Integration, and Hidden Dependencies

Many applications depend on LDAP without being recognized as identity infrastructure. They may query the directory for user attributes, determine access from group membership, synchronize account information, search for services, or update objects as part of an automated workflow. Over time, these integrations can accumulate into a complex dependency structure in which an application team, database administrator, service account, or software component can affect directory information that other systems treat as authoritative.

The result can be an architectural inversion.

A lower-trust application environment may receive directory-write access because it needs to update a user attribute. If that attribute drives access provisioning, group membership, certificate eligibility, synchronization behavior, or an application role in another system, compromise of the application can become a route to broader authority. The directory permission may look narrowly scoped. The consuming systems determine whether its consequence is narrow.

These relationships should be documented before integration, not reconstructed after compromise. The organization should identify the source system, destination objects and attributes, service identity, permissions, authentication method, encryption requirements, network path, ownership, logging, exception process, and recovery actions associated with every sensitive directory integration.

An integration that cannot be described as an authority pathway cannot be defended as one.

#### 5.5.6 Monitoring Directory Access Without Drowning in Activity

LDAP activity can be frequent in an enterprise environment. Domain services, applications, endpoint tools, identity platforms, and administrative consoles may generate large volumes of directory queries and updates. Effective monitoring does not require treating ordinary directory use as suspicious by default.

It requires prioritizing the events that alter or reveal consequential authority.

High-value monitoring should focus on changes to privileged groups, security descriptors, object ownership, delegated permissions, service identities, certificate-related attributes, Group Policy relationships, synchronization-related objects, account controls, and other elements that can create or expand effective control. It should also identify unusual patterns of broad directory discovery, particularly when they originate from identities or endpoints that do not normally perform such work.

The relevant evidence includes the initiating identity, source system, authentication context, directory target, attribute or permission affected, time of activity, resulting state, and whether the action aligns with approved workflow. Where an automated service performs the action, the organization must also be able to trace the workflow owner and source data that caused the service to act.

A record that says an object changed is useful. A record that establishes **who caused the change, from where, through what authority, and with what consequence** is operationally meaningful.

#### 5.5.7 Recovery Requires Reviewing the Directory State, Not Just the Server

When compromise affects an identity with meaningful LDAP write authority, recovery must account for the possibility that the attacker altered directory state in ways that persist after the original account or endpoint is remediated.

The investigation should consider the scope of the identity’s permitted writes, the objects and attributes it accessed, the administrative tools or automation paths available to it, and the downstream systems that consume the affected information. The organization may need to review group memberships, delegated rights, access-control entries, ownership changes, service attributes, policy relationships, synchronization behavior, certificate-related configuration, and application mappings.

The appropriate scope follows the authority held by the compromised identity.

A low-impact account with limited attribute-update rights does not automatically justify forest-wide review. An identity or platform capable of altering privileged objects, directory permissions, policy scope, synchronization, or certificate enrollment may require a much broader trust assessment. The organization must determine not only whether the change can be reversed, but whether it had time to propagate, be consumed by another service, or establish a second pathway to authority.

LDAP provides the interface through which Active Directory becomes useful to users, applications, administrators, and security teams. It also provides a route through which directory authority can be observed, exercised, and altered. The next section examines service identities and nonhuman access, where authentication and authorization decisions often become persistent, automated, and less visible than those associated with an individual user.

### 5.6 Service Identities and Nonhuman Authority

Service identities are often the least visible and most consequential accounts in an Active Directory environment.

A human account is usually associated with a person, a job function, a supervisor, a sponsor, a credential, and an expected pattern of interactive use. A service identity may represent an application, scheduled task, database connection, synchronization engine, web service, automation workflow, monitoring platform, backup process, management agent, or machine-to-machine integration. It may run continuously, authenticate without a person present, hold access to multiple systems, and persist long after the people who created it have moved to other roles.

That makes nonhuman identity a distinct security problem.

A service identity is not simply a technical account with a password. It is an authorization decision embodied in an automated process. The account exists because a system needs to act. Its permissions determine what that system can cause to happen. Its credentials, certificates, keys, or tokens determine how the system establishes that authority. Its host, configuration, administrators, scripts, and supporting platforms determine who can influence it.

The security question is therefore not merely whether the account has a strong password. It is:

> _What authority does this service identity exercise, and who can cause it to exercise that authority differently?_

That question places service identities directly within the effective-control model.

#### 5.6.1 Nonhuman Identities Accumulate Authority Differently

Service identities often receive broad permissions because they are created to solve an operational problem quickly. An application cannot reach a database, so its service account is granted additional access. A synchronization platform cannot update an attribute, so its connector account receives wider directory permissions. A management tool cannot complete a deployment, so its automation identity is granted local administration across more servers. A scheduled task needs access after hours, so it is configured to run under an account with standing privilege.

Each decision may be understandable in isolation. Over time, the resulting account can hold authority far beyond the narrow function that originally justified it.

This accumulation is especially dangerous because service identities may not be reviewed with the same regularity as human accounts. They may not appear in ordinary access-certification campaigns. Their owners may be unclear. Their credentials may be embedded in scripts, configuration files, scheduled tasks, deployment systems, application settings, password vaults, backups, or documentation. Their activity may be treated as normal background traffic even when the account accesses highly sensitive systems.

A service identity can therefore become both a persistence mechanism and an escalation pathway.

The attacker does not need to compromise the service identity directly if the attacker can compromise the application host, management platform, credential store, configuration-management process, or administrator capable of changing the service’s credentials or behavior. Control of those dependencies can provide effective control over the service identity.

A low-trust application server that stores a credential for a highly privileged service account is not simply an application server. It is a route to the authority held by that account.

#### 5.6.2 Ownership Must Be Explicit

Every consequential service identity should have a named technical owner and a named mission owner.

The technical owner is responsible for the account’s configuration, credential lifecycle, monitoring, hosting environment, and operational support. The mission owner is responsible for explaining why the service exists, what function it supports, what access it requires, and when that access should be reviewed or removed. In some environments, a system owner or risk owner will hold an additional responsibility for accepting the consequences of an exception or elevated permission.

These roles may be assigned to the same person in a small environment. They should still be distinguishable.

Without a mission owner, no one is responsible for determining whether the service remains necessary. Without a technical owner, no one is responsible for protecting its credential, reviewing its configuration, or responding when its behavior changes. Without a clear risk owner, broad permissions may persist because every team assumes another team approved them.

An unowned service identity is not a neutral administrative defect. It is ungoverned standing authority.

A defensible service-identity record should establish, at minimum, the service represented, the application or mission function supported, the systems on which it runs, the authentication methods it uses, the resources it accesses, the permissions it holds, the groups to which it belongs, the identities and systems that can modify it, the source location of its credentials, its credential-rotation process, its expected activity pattern, and its retirement condition.

The required detail should reflect consequence. A low-impact service used for a narrowly scoped internal function does not need the same governance burden as an identity that can alter directory objects, enroll for certificates, administer servers, access sensitive mission data, or synchronize authorization information across environments. The higher the possible authority, the more complete the ownership and evidence model should be.

#### 5.6.3 Managed Service Accounts Reduce Some Risk, Not All Risk

Managed service accounts and group Managed Service Accounts can reduce the operational risk associated with manually maintained service-account passwords. They are designed to support service identities whose password lifecycle is managed through Active Directory rather than handled manually by an administrator or embedded in a script.

That capability can improve credential hygiene. It reduces the need for administrators to know, distribute, store, or rotate a static service password manually. It can also reduce the likelihood that an old password remains in configuration files or is reused across several services.

It does not eliminate the need to govern authority.

A managed service account can still hold excessive permissions. It can still be assigned to a service running on an inadequately protected host. It can still authenticate to sensitive resources. It can still be subject to misuse by an attacker who controls the host or process authorized to use it. The identities and systems allowed to retrieve or use the managed credential must be treated as part of the service identity’s security boundary.

Credential management is necessary. Least privilege, source control, monitoring, and recovery remain necessary as well.

The same reasoning applies to certificates, keys, tokens, and cloud-managed identities used by nonhuman services. A stronger authentication mechanism may reduce one category of credential-exposure risk. It does not independently establish that the service should retain its authority or that the systems capable of using the credential are appropriately protected.

#### 5.6.4 Service Accounts Should Not Become Administrative Shortcuts

A recurring design failure occurs when a service identity is used to bypass the controls expected for human administrators.

A service may be granted broad directory rights because automated provisioning is easier than implementing a narrow delegation model. An application may run with local administrator rights because individual required permissions were not identified. An automation account may be shared across teams because it is difficult to separate operational responsibilities. A management tool may use a privileged service identity from many hosts because maintaining designated administration paths is inconvenient.

These choices can make an environment easier to operate in the short term. They make it harder to defend over time.

A highly privileged service identity is particularly dangerous when it is used interactively, shared among personnel, permitted to authenticate from general-purpose systems, or exempted from normal monitoring because its activity is assumed to be automated. Those conditions blur the boundary between machine authority and human authority. They make attribution difficult, increase credential exposure, and provide an attacker with a trusted mechanism for operating across the environment.

Service identities should perform services. They should not become substitute administrator accounts.

Where a service requires high-impact authority, the organization should isolate the service’s execution environment, restrict where and how the identity can be used, protect the administrative interfaces capable of changing it, and monitor its activity according to the authority it holds. The service should be granted only the permissions necessary for its defined function, and its use should be distinguishable from interactive administration.

#### 5.6.5 Monitoring Nonhuman Authority

Service-account activity is often high volume and repetitive. That does not make it unimportant. It means that monitoring must establish an expected behavioral model.

The organization should understand where a service identity normally authenticates, which systems it contacts, which protocols and services it uses, what times or operational conditions drive its activity, and what administrative changes are expected during maintenance. Deviations from that model can reveal a compromised credential, altered configuration, unauthorized use from a new host, a change in service scope, or an attempt to use the identity for interactive or lateral movement activity.

High-value indicators include authentication from an unexpected endpoint; use outside the defined application or maintenance context; changes to group membership, delegated rights, certificates, or credentials; modifications to the account’s service-principal information; new administrative rights; access to systems outside the documented service dependency; and changes to the host or automation workflow that executes the account.

The signal is not that a service account authenticated. The signal is that it authenticated, changed, or was used in a way inconsistent with its defined authority.

Monitoring must also cover the systems that administer the identity. A service-account credential stored in a password vault, deployment platform, source-control system, automation server, or application configuration is exposed to the administrative control of those systems. If an attacker gains control of a platform that can retrieve, replace, or execute the credential, the attacker may not need to alter the directory account at all.

The evidence model must therefore connect service-account use to service-account control.

#### 5.6.6 Containment and Recovery of Service Identity Compromise

When a service identity is suspected of compromise, responders must determine more than whether its password or key should be rotated. They must identify what authority the identity held, where it was used, which systems stored or accessed its credential, whether the attacker could have changed its permissions or configuration, and whether the service may have been used to create another route to authority.

Rotation is necessary when a secret may be exposed. It is not sufficient if the attacker retains control of the host, service configuration, management platform, or delegation path through which the identity operates.

Containment may require disabling the account, rotating its credential or certificate, ending active sessions, restricting use to approved hosts, reviewing the service’s permissions and group memberships, validating its SPNs or related configuration, rebuilding affected execution environments, and inspecting downstream systems for changes made under the service identity’s authority. The proper scope depends on what the account could affect.

The recovery goal is not simply to make the application function again. It is to restore the application’s required function without reintroducing an untrusted authority pathway.

This may require redesign. A service that cannot operate without broad standing privilege, shared credentials, unclear ownership, or unrestricted administrative reachability is not merely difficult to support. It is signaling an identity architecture problem.

Service identities demonstrate why authentication and authorization cannot be analyzed only through the actions of individual users. In a modern enterprise, automated systems increasingly create, modify, synchronize, approve, and enforce identity decisions. Their credentials and permissions are mission-enabling, but they also concentrate authority in places that ordinary account reviews can miss.

The next section examines privileged administration, where human and nonhuman authority converge through the systems, sessions, and roles capable of changing the identity control plane.

### 5.7 Privileged Administration: Where Authority Becomes Action

Privileged administration is the point at which identity authority becomes a change in the environment.

A directory permission, administrative role, certificate template, service credential, group membership, or management-platform entitlement has consequence only when an identity uses it to alter a system, configuration, credential, policy, or access decision. Privileged administration is therefore not limited to members of a familiar administrative group. It includes every person, account, endpoint, service, tool, and workflow capable of making a material change to the identity control plane.

This is why privileged access must be defined by effective control.

A domain administrator clearly holds privileged authority. So does an identity capable of modifying the membership of a group that administers domain controllers. So may an endpoint-management platform able to deploy configuration to privileged workstations, a certificate administrator able to alter an authentication-capable template, a synchronization service able to write sensitive attributes, or an automation identity able to modify Group Policy.

The visible role is important. The resulting control is what matters.

#### 5.7.1 Privileged Administration Is a System, Not an Account Category

Organizations often begin privileged-access management by identifying a set of accounts designated as administrators. That is necessary, but incomplete. A privileged-access system includes at least five connected elements:

* the identity authorized to perform the action;
* the endpoint from which the identity acts;
* the management tool, service, or workflow used;
* the target component whose state can be changed; and
* the evidence demonstrating what occurred.

Weakness in any element can undermine the others.

An administrator may use a dedicated account with strong authentication, yet operate from an endpoint exposed to general web activity, email, removable media, or unmanaged software. A hardened privileged-access workstation may be used appropriately, yet connect through an overly broad management platform capable of reaching systems outside its approved scope. A change may be technically approved and correctly implemented, yet inadequately logged, leaving the organization unable to establish whether the action was legitimate or whether a similar unauthorized action occurred later.

Privileged access is trustworthy only when the entire path is controlled.

This requirement is especially important because attackers often seek to use legitimate administrative mechanisms rather than deploy visibly unusual tools. A compromised administrator session can create accounts, modify groups, change policy, alter certificates, reconfigure services, deploy software, disable monitoring, or create persistence through functions the environment already trusts. The resulting actions may be syntactically valid and may use ordinary management protocols.

The defender must distinguish valid administration from authorized administration.

That distinction depends on context: who performed the action, from which source endpoint, through which approved path, against which target, under what approval or change authority, and with what resulting effect on identity authority.

#### 5.7.2 Separate Privileged Identities From Ordinary User Activity

A privileged identity should not be used casually for ordinary productivity work.

When the same account is used for email, web browsing, collaboration, document editing, and high-impact administration, compromise of any lower-trust activity can expose the authority needed to control the environment. The user may authenticate successfully with multifactor authentication and still become vulnerable to session theft, malicious content, endpoint compromise, or manipulation of the administrative tools used after authentication.

The purpose of separate privileged identities is not administrative formality. It is containment.

An identity used for routine work should carry only the authority required for routine work. An identity used for privileged administration should be restricted to the systems, tools, sessions, and functions required for administration. Where the consequence warrants it, the privileged identity should operate only from dedicated administrative endpoints and through controlled management paths.

This separation reduces the number of opportunities for lower-trust activity to reach high-trust credentials or sessions. It also improves detection. An administrative logon from a designated privileged-access workstation is easier to evaluate than a privileged logon that could originate from any endpoint in the enterprise.

The same discipline applies to emergency authority. Break-glass accounts may require elevated rights to support continuity of operations or incident response. Their credentials, conditions of use, management paths, logging, and post-use review should be more tightly governed, not less. Emergency access is justified by the need to restore mission capability under abnormal conditions. It should not become an unmanaged alternative to the standard privileged-access model.

#### 5.7.3 Administrative Endpoints Define a Security Boundary

A privileged-access workstation, jump host, or designated management server is not merely a convenient place to install administrative tools. It is a boundary protecting the sessions, credentials, and actions through which sensitive authority is exercised.

The endpoint should be protected according to what it can do, not according to its hardware type or operating-system version. If it can administer domain controllers, certificate authorities, identity synchronization services, privileged groups, Group Policy, or recovery systems, its exposure to lower-trust activity must be constrained accordingly.

This commonly requires a more restrictive operating model than that used for ordinary workstations. The administrator should not use the endpoint for routine browsing, personal email, unapproved software, or activities unrelated to the administrative function. Network access should be limited to the management paths and identity services required. Administrative tools should be controlled and maintained. Logging and endpoint telemetry should support attribution and investigation. The endpoint itself should be included in the recovery scope when privileged credentials or sessions may have been exposed.

A privileged workstation is part of the authority it carries.

The same principle applies to jump hosts and management platforms. A jump host can reduce direct reachability to sensitive systems when it is dedicated, hardened, monitored, and restricted to approved administrative activity. It becomes an authority concentration point when it is broadly accessible, shared across incompatible trust levels, poorly monitored, or used as a general-purpose remote desktop server.

A management platform should be evaluated by its effective control. A system able to deploy software, execute scripts, alter configuration, retrieve secrets, change policy, manage local administrators, or create remote sessions on sensitive systems may belong within the same security boundary as those systems. Its compromise can provide a route to the authority it manages.

#### 5.7.4 Just-in-Time (JIT) Access Reduces Standing Authority

Standing privilege creates opportunity. The longer an identity retains elevated access, the more time an attacker has to discover, steal, misuse, or inherit that authority.

Just-in-time access reduces this exposure by granting elevated authority only for a defined task, scope, and duration. The exact implementation can vary. It may involve time-bounded group membership, an approved elevation workflow, a privileged-access management system, a task-specific administrative role, or another controlled process. The governing principle is that consequential authority should not persist longer than the mission requires.

Time limitation does not remove the need for monitoring or protected administration. An attacker who compromises a valid administrative session can still act during the approved window. But time-bounded elevation can reduce the volume of standing privilege, improve the visibility of exceptional activity, and create a clearer connection among the requested task, approving authority, administrative session, and resulting change.

The organization should avoid treating just-in-time access as a technical feature without governance. The workflow must establish who requested elevation, what authority was requested, why it was needed, how long it remained active, from which endpoint it could be used, what actions occurred, and whether the authority was removed as intended.

Temporary privilege that cannot be accounted for is simply privilege with an uncertain expiration.

#### 5.7.5 Privileged Actions Require Protected Evidence

The most consequential identity changes should be attributable.

The organization should be able to associate a modification to a privileged group, a delegated permission, a policy object, a certificate template, a synchronization setting, a domain controller, or a recovery configuration with the initiating identity, source endpoint, management tool or automation workflow, target object, approval basis, and resulting state.

This does not mean that every change must require a manual approval ticket before it can occur. Automated maintenance and emergency response may require rapid action. It means that high-impact actions must leave evidence sufficient to reconstruct the decision and determine whether it was authorized.

The evidence should not reside solely on the component being changed. A compromised domain controller, management server, or privileged endpoint may not retain trustworthy local records. Centralized and protected collection of identity, endpoint, administrative-session, and change-management evidence strengthens the organization’s ability to investigate and recover when a privileged pathway is suspected of compromise.

A record of the final configuration is useful. A record of how authority changed is more valuable.

#### 5.7.6 Privileged Administration Must Be Recoverable

A privileged-access design is incomplete if the organization cannot operate it during an outage or an incident.

Normal management paths may fail. A privileged workstation may be unavailable. Network segmentation may prevent access to an affected enclave. A certificate or identity provider may be impaired. The organization may need controlled emergency access to contain compromise, recover a domain controller, revoke an unsafe credential, restore a policy, or validate the integrity of an authority-bearing service.

Those alternatives must be designed before the emergency.

Recovery authority should be limited to designated personnel, protected from ordinary use, tested regularly, and subject to clear logging and post-use review. Recovery identities and credentials should not share the same exposure paths as the systems they are intended to recover. Backup access, break-glass credentials, alternate administrative endpoints, and out-of-band communications each require their own ownership, protection, and validation.

The recovery question is not whether an administrator can regain access. It is whether the organization can restore trusted administrative control without depending on an authority pathway that may already be compromised.

#### 5.7.7 The Administrative Path Is the Attack Surface

The most important lesson of privileged administration is that authority is exercised through paths, not titles alone.

A privileged group membership matters because it can be used from an endpoint, through a tool, over a network path, against a target, within a session. Each point can constrain or expose the authority. An attacker who cannot compromise the administrator directly may seek the endpoint, the management platform, the service account, the credential vault, the automation workflow, the policy object, or the network route that enables the administrator’s work.

Defenders must protect the full path.

The appropriate design is not a single privileged-access product or a static list of administrator accounts. It is an operating model in which high-impact authority is narrowly assigned, exercised from protected systems, available only through deliberate management paths, monitored as it is used, and recoverable when the ordinary control plane is no longer trustworthy.

Authentication establishes the claim. Authorization grants consequence. Privileged administration changes the conditions under which both are decided.

The next section brings these mechanisms together by examining authorization boundaries, effective control, and the evidence required to determine whether authority has expanded beyond its intended mission purpose.

### 5.8 Authorization Boundaries and Effective Control

Authorization boundaries determine where an identity’s authority should end. Effective control reveals where that authority may continue through indirect relationships.

The difference between the two is the difference between a defensible access model and an environment that appears least privileged while retaining hidden routes to escalation.

An authorization boundary may be expressed through a group, an access-control list, an application role, a network rule, an administrative scope, a certificate policy, a cloud assignment, or a managed-service permission. Each mechanism can limit what an identity is permitted to do directly. But the boundary is meaningful only if the identity cannot use another relationship to alter, bypass, or inherit the same authority.

A user who lacks membership in a privileged group may still be able to modify the group’s membership. A service account that cannot administer a domain controller may be able to control a management platform that can. An endpoint-management operator may not hold directory rights but may be able to deploy configuration to the workstation used by a directory administrator. An application identity may have narrowly scoped directory-write permissions while those attributes determine access in another system. A certificate administrator may not appear in a domain-administration group but may be able to issue credentials accepted for privileged authentication.

Each condition crosses the visible authorization boundary through an authority pathway.

This is why least privilege cannot be measured only by counting privileged accounts or removing users from well-known administrative groups. Those measures are useful. They do not establish whether the organization has controlled the relationships through which less visible authority can be converted into more consequential control.

The governing question remains:

> _Can this identity, system, service, or administrative process cause a higher-trust authority to change?_

If the answer is yes, the relationship belongs within the security analysis of the higher-trust authority.

#### 5.8.1 Direct Privilege and Effective Control

Direct privilege is comparatively easy to identify. A principal may belong to a privileged group, hold a defined role, possess an access-control entry granting administrative rights, or be assigned a role in a management platform. The permission is visible and can usually be reviewed through directory, application, or platform administration tools.

Effective control is broader. It includes the ability to obtain, alter, or exercise direct privilege through another identity, object, system, process, or dependency.

A principal has effective control over a privileged account if it can reset that account’s password, alter its authentication material, change its group memberships, modify the policy applied to its workstation, access the endpoint where it uses credentials, or control a service that acts on its behalf. A principal has effective control over a certificate authority if it can administer the authority, modify a template or enrollment policy, alter the underlying host, access its signing keys, or manage the identities that perform those functions. A platform has effective control over a domain controller if it can deploy software, execute commands, alter policy, recover the server, or change the configuration through which the controller performs identity functions.

Effective control is not always equivalent to full control. The consequence depends on the specific mechanism, target, conditions, and protections present. But it must be assessed as potentially consequential because attackers seek exactly these indirect paths.

The organization should not require an attacker to reach a formal administrator title before recognizing a Tier 0 concern.

#### 5.8.2 Tier 0 Is Defined by Influence Over Trust

Tier 0 is often described through a list of obvious directory assets: domain controllers, forest-level administrative groups, privileged directory accounts, and certain identity services. Those assets belong in Tier 0 because their compromise can directly affect enterprise identity authority.

The list is necessary. It is not complete.

Tier 0 must include the people, identities, devices, services, platforms, and recovery capabilities that can materially influence those core assets. A privileged-access workstation used to manage domain controllers is part of the Tier 0 boundary while it carries that administrative authority. A certificate authority capable of issuing credentials accepted for privileged authentication has Tier 0 significance. A synchronization service that can modify sensitive group memberships or identity attributes belongs in the Tier 0 analysis. A backup platform containing directory recovery material, a credential-management system capable of retrieving privileged secrets, or an endpoint-management tool that can modify domain-controller configuration may also hold effective control.

The tier is defined by what the component can cause, not merely by the label assigned to it.

This does not mean every supporting system must be administered identically to a domain controller. Risk decisions remain proportionate to actual authority. It means that the organization must not exclude a component from high-trust analysis merely because it is categorized as a backup service, endpoint tool, application server, network-management platform, or workstation rather than as a directory server.

If compromise of the component can alter the organization’s identity authority, then the component is part of the identity security boundary.

#### 5.8.3 Boundaries Must Be Tested, Not Assumed

An authorization design may look correct in documentation while failing in the operating environment.

A group may appear restricted while being modifiable through an inherited access-control entry. An application role may appear separate from directory privileges while depending on a synchronization attribute writable by a lower-trust service. A privileged workstation may appear isolated while its management agent accepts commands from a broadly administered platform. A certificate-enrollment policy may appear constrained while a related template, delegated permission, or enrollment workflow permits a different route to obtain equivalent authority.

These conditions are not reliably discovered through policy statements alone.

The organization must validate its authorization boundaries through technical review, access analysis, configuration assessment, controlled testing, and authorized adversary emulation. The purpose is not to demonstrate compromise theatrically. It is to establish whether the architecture behaves as intended when an identity, service, or endpoint is assumed to be compromised.

A useful validation asks whether an ordinary identity can influence privileged authority through paths that are not obvious from formal role membership. It asks whether a delegated administrator can reach sensitive objects outside the intended scope. It asks whether a management platform can become a bridge from a lower-trust network to a higher-trust identity system. It asks whether a compromised service identity can alter directory, certificate, policy, or application decisions beyond its documented mission function.

The result should produce an engineering decision: remove the path, narrow the delegation, isolate the management system, strengthen the source boundary, improve monitoring, or document and govern the residual risk.

Testing without remediation identifies exposure. Validation after remediation establishes control.

#### 5.8.4 Authorization Must Be Observable

An authorization boundary is stronger when the organization can observe attempted and successful crossings.

Visibility should answer who requested or exercised access, what identity and credential were used, which target or authority was affected, which administrative path was involved, what decision was made, and whether the result aligned with an approved function. The required evidence varies by system, but the objective remains consistent: material changes in authority must be attributable and reviewable.

For a sensitive directory action, the organization should be able to identify the changed object, attribute, permission, or membership; the initiating identity; the source administrative endpoint or automation service; the resulting access effect; and the approval or workflow that justified it. For a certificate-based path, it should be able to connect enrollment, issuance, credential use, relying-party access, and revocation status. For an application role, it should be able to identify the source of the authorization attribute, the administrator or workflow that changed it, and the entitlement granted downstream.

Evidence should follow the authority pathway.

This is especially important for indirect control because no single platform may record the entire relationship. A directory log might record a group change. An endpoint log may identify the source of the administrative session. A certificate authority log may show a credential issued afterward. An application log may show the resulting access. The organization’s monitoring design must preserve enough connected evidence to determine whether these events represent normal operations or an expansion of effective authority.

#### 5.8.5 Withdrawal of Authority Must Be Designed

Every authorization mechanism needs a credible removal path.

It is not enough to know how authority is granted. The organization must know how it is suspended, revoked, removed, or revalidated when a person changes roles, a contract ends, a service is retired, a credential is compromised, an application is replaced, or an incident creates uncertainty about the trust relationship.

The withdrawal process must account for the full path by which authority is exercised. Removing a directory group membership may not remove an active application session. Disabling an account may not revoke a certificate, cloud token, or federated assertion already accepted elsewhere. Rotating a service-account secret may not address an attacker’s control of the host where the new secret will be used. Rebuilding a privileged workstation may not address the management platform that can reconfigure it.

Revocation should be evaluated according to the identities, credentials, sessions, authorization stores, and dependent systems that participate in the relevant access decision.

This is not an argument for treating every access change as an enterprise incident. It is an argument for knowing the scope of the decision before declaring it complete.

#### 5.8.6 The Chapter’s Operating Standard

Authentication validates a claim. Authorization assigns consequence. Access control and delegation distribute administrative authority. Kerberos, LDAP, service identities, certificates, tokens, groups, and applications carry that authority through the environment. Privileged administration changes the configuration from which future identity decisions will be made.

Together, these mechanisms form the operational center of the identity trust system.

The defender’s standard is therefore higher than confirming that users can sign in and administrators can perform their work. The organization must be able to establish that authority is granted for a defined purpose, constrained to the necessary scope, exercised from protected paths, observable when it changes, and withdrawable when trust is no longer warranted.

When it cannot meet that standard, the environment may still function. It cannot reliably claim that its identity authority remains under control.

The next chapter examines the directory relationships through which that authority is organized and expanded across domains, forests, trusts, policy scopes, and administrative boundaries.
