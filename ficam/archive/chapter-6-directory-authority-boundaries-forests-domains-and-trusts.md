# ❌ Chapter 6 - Directory Authority Boundaries, Forests, Domains, and Trusts

### Abstract

Chapter 6 examines the Active Directory structures through which identity authority is organized, separated, shared, and extended across an enterprise. It explains the distinct security significance of forests, domains, organizational units, domain controllers, and trust relationships, emphasizing that these constructs serve different technical and administrative purposes. A forest establishes the broadest Active Directory security boundary because its domains share schema, configuration, and core trust relationships; a domain provides an authentication and administrative boundary within that forest; and an organizational unit provides a scope for object organization, delegated administration, and Group Policy, not an independent security boundary.

The chapter analyzes trusts as configurable relationships rather than binary connections, considering direction, transitivity, authentication scope, selective authentication, administrative ownership, and the authority that can cross a boundary after successful authentication. It examines how cross-domain and cross-forest dependencies can support legitimate federal missions while creating paths through which compromise, misconfiguration, or poorly governed administration may expand.

The chapter applies effective control to directory boundaries: a lower-trust environment need not hold direct domain-administrator membership to influence a higher-trust environment if it can manage a trusted identity, alter a policy, control a synchronization path, administer a shared service, or affect a credential accepted across the boundary. The objective is to design trust relationships that are purposeful, constrained, observable, and recoverable.

### Key Terminology

* **Forest:** The highest-level Active Directory structure, containing one or more domains that share a schema, configuration, and common directory trust framework.
* **Forest root domain:** The first domain created in an Active Directory forest. It establishes the forest namespace but is not inherently the location of all administrative authority.
* **Domain:** An Active Directory administrative and authentication boundary containing directory objects, policies, and domain-specific identity functions.
* **Domain tree:** A set of Active Directory domains within a forest that share a contiguous DNS namespace.
* **Organizational unit (OU):** A directory container used to organize objects, delegate administration, and scope Group Policy. An OU is not an independent authentication or security boundary.
* **Trust relationship:** A configured relationship through which one domain or forest accepts authentication from identities managed by another domain or forest.
* **Trust direction:** The direction in which authentication is accepted across a trust relationship.
* **Transitive trust:** A trust relationship that can extend authentication relationships beyond two directly connected domains, according to the trust configuration.
* **Nontransitive trust:** A trust relationship limited to the two directly connected domains or forests.
* **Selective authentication:** A trust configuration that requires identities from a trusted environment to be explicitly permitted to authenticate to selected computers or services in the trusting environment.
* **Authentication scope:** The set of systems, services, and resources to which an identity may authenticate after crossing a trust boundary.
* **Foreign security principal:** An object used in Active Directory to represent a security principal from a trusted external domain or forest for authorization purposes.
* **Cross-forest access:** Access granted to identities from one forest to resources governed by another forest through an approved trust, federation, provisioning, or other interoperability mechanism.
* **Administrative boundary:** A limit on which identities or teams may manage a defined set of systems, objects, or identity functions.
* **Security boundary:** A limit intended to constrain the spread of authority or compromise. Whether a construct functions as a security boundary depends on its technical configuration and the dependencies surrounding it.

### 6.1 Forests and Domains: Where Directory Authority Begins and Ends

A forest is the broadest native Active Directory boundary for shared directory authority. A domain is a more focused boundary for authentication, administration, and object management. An organizational unit is a container for organization, delegation, and policy scope.

Treating these three constructs as interchangeable is one of the fastest ways to misunderstand an Active Directory environment.

A forest contains one or more domains that share core directory elements, including a common schema and configuration structure. The forest also establishes the overarching trust framework through which its domains can recognize one another. This shared foundation permits organizations to operate a distributed directory while retaining interoperability among domains that serve different geographic locations, business functions, mission organizations, or administrative requirements.

The shared foundation also means that a forest must be defended as an authority system, not as a set of unrelated domains.

A compromise capable of altering forest-level configuration, schema, enterprise authentication conditions, or the administration of core directory services can affect more than the domain where the compromise was first observed. The same is true of systems that can effectively control those functions: privileged administrative workstations, certificate authorities accepted for domain authentication, backup and recovery platforms, synchronization services, endpoint-management systems, and identities able to modify the components on which forest authority depends.

The forest is not simply a naming hierarchy. It is a trust framework.

A domain creates a more specific administrative and authentication context within that framework. It contains users, computers, groups, organizational units, policies, service identities, and domain-specific directory data. A domain can support distinct administration, account policies, replication scope, and operational responsibilities. Domains may be appropriate where the organization needs separate directory namespaces, defined administrative control, specialized operational functions, or a structure aligned to longstanding mission requirements.

A domain is meaningful, but it is not automatically an isolated security enclave.

Domains in the same forest participate in a common directory ecosystem. They share important forest-level dependencies and may have relationships that permit authentication and resource access across domain boundaries. An identity in one domain can become relevant to another domain through group nesting, shared services, cross-domain administration, trusts, certificate use, management platforms, or systems whose operators hold authority in more than one domain.

The defensive question is not merely whether two domains have different names. It is what authority can cross between them and who can change the conditions under which it crosses.

This distinction is particularly important in federal environments, where domain structures may reflect agency components, legacy organizations, mission functions, deployed locations, administrative responsibilities, or different operational eras. A domain boundary may support an important organizational or operational separation. It does not independently prove that a compromise in one domain cannot influence another.

The organization must validate that conclusion through the actual trust, administration, credential, management, and recovery relationships in place.

The forest root domain deserves similar precision. It is the first domain created in the forest and establishes the forest namespace. Its role in the namespace does not mean that every forest-level administrative function should be performed from it or that every privileged account should reside there. The forest root domain is important because of its place in the directory structure, but defenders should not confuse naming centrality with the complete distribution of effective control.

Authority must be mapped, not presumed from labels.

A domain controller represents another form of concentrated authority. It stores and replicates directory information for its domain and provides authentication-related services to clients and dependent systems. It is therefore part of the domain’s core identity infrastructure. Yet domain controllers also depend on forest-wide configuration, network connectivity, DNS, replication topology, privileged administration, policy, backups, certificate services, and recovery processes. The server itself cannot be assessed in isolation from those dependencies.

The same principle applies to administrative groups. A group with a well-known privileged name is consequential because of the authority it grants. But a group need not have a recognizable name to be security-relevant. It may administer a domain controller indirectly, modify a Group Policy Object, control a service identity, manage certificate enrollment, or hold delegated rights over objects that influence more sensitive authority.

Formal hierarchy is useful. Effective control is decisive.

Organizational units fit into this model differently. An OU can organize users, computers, groups, and other objects. It can define the scope of delegated administration. It can determine where Group Policy Objects apply. Those are powerful functions. They do not make the OU a separate authentication boundary, a separate domain, or an independent security enclave.

An identity able to administer an OU may have significant authority over the objects within it. If those objects include privileged accounts, administrative workstations, sensitive service identities, or systems that influence Tier 0 functions, the delegation may create a high-impact pathway. If the OU contains only a tightly defined population of ordinary accounts and the delegated rights are limited to a narrow lifecycle function, the authority may be appropriate.

The security consequence depends on the contents of the OU and the permissions applied to it.

This is why organizational design must avoid mixing objects with substantially different trust levels under the same delegated administrative scope. A help-desk delegation intended to support ordinary users should not extend by inheritance to privileged administrative accounts. An application-support team’s authority over service identities should not include services that administer identity infrastructure. An endpoint-management scope intended for user devices should not silently include privileged-access workstations or domain controllers.

Containers are organizational tools. Their delegated permissions create security relationships.

A defensible directory architecture begins by identifying the boundaries the organization actually needs. Some boundaries support authentication and administration. Some support policy scope. Some support network reachability. Some support mission, classification, organizational, or operational separation. The architecture becomes unsafe when one type of boundary is assumed to provide the protection of another.

A separate OU does not replace a separate administrative model. A separate domain does not replace constrained trusts and privileged-access design. A separate forest does not eliminate risk if shared administrators, credentials, management platforms, certificate authorities, synchronization services, or recovery systems can influence both forests.

The structure is only the beginning. The relationships determine the security outcome.

The next section examines organizational units and delegation in greater detail, focusing on how an apparently administrative convenience can become an authority pathway when privileged identities, policies, and support functions are not deliberately separated.

### 6.2 Organizational Units and Delegated Administration: Scope Is Not Separation

An organizational unit provides scope. It can organize directory objects, receive Group Policy, and serve as the target of delegated administration. It does not, by itself, establish an independent security boundary.

That distinction is easy to lose in large environments because OUs often carry meaningful names: a command, directorate, installation, application portfolio, user population, server class, or administrative function. The name may describe a real organizational responsibility. The OU may still be subject to the same domain authentication framework, forest dependencies, administrative relationships, and cross-boundary authority pathways as the rest of the environment.

An OU answers practical management questions:

* Which objects should be organized together?
* Which Group Policy Objects should apply to them?
* Which team may perform defined administrative actions over them?
* Which lifecycle process governs their creation, modification, and removal?

It does not independently answer whether the objects within it are protected from identities elsewhere in the domain, whether the OU’s administrators can reach more sensitive objects through another path, or whether the systems within the OU can influence authority outside it.

Scope is useful. Scope is not isolation.

The security importance of an OU comes from the objects it contains and the authority delegated over those objects. A narrowly managed OU containing ordinary user accounts may allow a help-desk group to reset passwords, unlock accounts, or update limited user attributes. That can be appropriate. An OU containing privileged accounts, certificate-service identities, administrative workstations, domain controllers, or high-impact service accounts requires a different administrative model because the same actions may create substantially greater consequence.

The right to reset a password is not intrinsically low risk or high risk. Its risk depends on whose password can be reset.

A support team able to reset an ordinary user’s password may support a legitimate lifecycle function. The same team, if able to reset the password of a privileged administrator or service identity, may be able to assume that identity’s authority. Likewise, the ability to modify group membership may be routine for application access groups and highly consequential for groups that administer sensitive systems or are nested into privileged roles.

Delegation must therefore be evaluated against the authority of the target population, not only the action requested.

#### 6.2.1 OU Design Should Reflect Administrative Trust Levels

An OU structure is most defensible when it separates object populations that require materially different administrative protections.

Ordinary user accounts, privileged user accounts, service identities, administrative workstations, general endpoints, servers, identity infrastructure, and specialized mission systems may each require different Group Policy, ownership, lifecycle processes, monitoring, and delegated administration. Placing these objects in distinct administrative scopes does not guarantee security. It makes it possible to apply distinct controls deliberately.

The opposite design creates authority mixing.

Authority mixing occurs when objects with different trust requirements share a container, delegation model, policy scope, or management process such that lower-trust administration can influence higher-trust objects. A help-desk group may be delegated authority over an OU intended for ordinary user support. Over time, privileged accounts, service accounts, or break-glass identities may be placed in that same OU for convenience. The original delegation now reaches identities that were never meant to be exposed to it.

The directory may continue to function normally. The security model has changed.

This is why OU design should be reviewed whenever an organization adds a new identity class, deploys an application, creates a service account, introduces a new management platform, reorganizes personnel, or changes a mission boundary. A technically convenient location is not always an administratively safe location.

The relevant design question is not, _“Where will this object be easiest to find?”_ It is, _“Which identities, policies, permissions, and administrative workflows will this placement cause to apply?”_

That question includes inheritance. Permissions delegated at an OU can apply to descendant objects. Group Policy linked to an OU can affect computers and users beneath it. A nested OU structure can create layered administrative and policy relationships that are difficult to understand from the object’s immediate location alone.

An object placed in a child OU may inherit exposure from a parent container. An object moved during a reorganization may begin receiving different policy or delegation. A policy link intended for an endpoint population may reach an administrative system if the scope changes. A new delegation assigned to support a routine workflow may affect legacy objects that remain in the container.

OU changes are therefore authority changes when they alter the effective policy or administrative control surrounding an object.

#### 6.2.2 Delegation Must Be Narrow Enough to Defend

Delegation is necessary in a federal enterprise. Central directory administrators cannot process every onboarding request, password reset, computer account operation, application integration, and access change. The question is not whether to delegate. It is whether the delegated authority is limited to a specific function and protected from unintended expansion.

A defensible delegation model identifies:

* the mission or operational function being delegated;
* the accountable owner of that function;
* the group or identity receiving the delegated authority;
* the exact objects, object classes, and attributes within scope;
* the actions permitted and prohibited;
* the source endpoint or automation platform from which the authority may be used;
* the evidence that records changes; and
* the review and removal conditions for the delegation.

This is more than administrative documentation. It is the information required to determine whether a delegated permission can become a path to higher authority.

For example, a support team may need to unlock accounts and reset passwords for a specific user population. Its delegation should not include authority to modify group memberships, alter service attributes, write access-control entries, change object ownership, or manage privileged account containers unless those actions are independently justified and governed. A provisioning workflow may need to create computer accounts in a defined OU. It should not automatically receive broad rights over every descendant object or authority to modify the security descriptors governing the container.

The smallest practical delegation is usually the most explainable and recoverable one.

Broad permissions are often granted because they are easier to implement than a narrow model, especially during integration projects or operational emergencies. Those permissions can persist long after the original need has passed. The organization should treat broad delegation as a risk decision requiring explicit ownership, compensating controls, heightened monitoring, and a plan to reduce or retire the authority.

A delegation that cannot be explained in operational terms should not be treated as normal configuration.

#### 6.2.3 Group Policy Adds Another Dimension of Control

OUs also determine where Group Policy may apply. This makes their design relevant not only to account administration but also to the configuration of endpoints and servers.

A Group Policy Object can configure security settings, operating-system behavior, software deployment, scripts, administrative restrictions, and other controls affecting the systems or users in its scope. The ability to link, modify, or influence a GPO applied to a sensitive OU can therefore create effective control over the systems within that scope.

An OU containing privileged-access workstations should not be treated like an ordinary user-device container. An OU containing domain controllers or other identity infrastructure should have tightly controlled policy administration because changes to those systems can affect authentication, credential exposure, logging, and enterprise authority. A policy-management role intended for general endpoints should not silently extend to high-trust systems through broad linking rights or poorly managed inheritance.

The important question is not simply, _“Who can edit this GPO?”_ It is also, _“Who can cause this GPO to apply here?”_

An identity able to link an existing policy to a sensitive OU, alter inheritance behavior, change an OU’s placement, or modify the scope of a policy can influence system configuration even without owning the policy itself. These relationships must be included in the authority model.

#### 6.2.4 Protected Identities Require Protected Administration

High-value identities should be placed within administrative scopes that reflect their consequence.

This includes privileged user accounts, emergency accounts, service identities with sensitive permissions, accounts used by directory or PKI administrators, and identities associated with recovery functions. The appropriate design varies, but the principle is stable: a lower-trust support process should not be able to alter the credential, group membership, ownership, policy exposure, or lifecycle state of a higher-trust identity merely because both were placed in the same convenient container.

Protection requires more than moving objects into an OU named “Privileged.” The organization must validate the permissions inherited by that OU, the groups allowed to administer it, the GPOs applied to it, the automation workflows that modify objects within it, the synchronization services that write attributes, and the identities capable of changing those relationships.

A protected container with inherited lower-trust delegation is protected in name only.

The same discipline applies to systems. Domain controllers, certificate authorities, privileged-access workstations, identity synchronization servers, and management platforms should be assigned to policy and administrative scopes that prevent broad endpoint-management or user-support processes from influencing their configuration without explicit authorization.

The goal is not to create complexity for its own sake. It is to ensure that the most consequential objects are governed by the most appropriate administrative boundary.

#### 6.2.5 OU Review Is an Ongoing Control

An OU design that was safe when created can become unsafe as the environment changes. New applications may introduce service accounts. An acquisition or reorganization may move users and systems between administrative scopes. A cloud migration may add synchronization attributes and provisioning workflows. A policy-management platform may gain new capabilities. An emergency delegation may remain after the emergency ends.

Periodic review should therefore evaluate not only whether the OU structure remains tidy, but whether the effective administration remains appropriate.

For each consequential OU, the organization should be able to identify its purpose, contained object populations, applied GPOs, delegated permissions, inherited permissions, owners, automation dependencies, and associated management paths. For OUs supporting privileged identities or systems, the review should also determine whether any lower-trust identity can reset credentials, modify memberships, change permissions, alter policy scope, or otherwise influence the protected population.

This review is particularly valuable after incidents. A compromise may reveal that the attacker did not need direct membership in a privileged group because an inherited OU permission, policy-management right, or automation workflow provided an indirect route to authority. The corrective action should address the relationship that enabled the path, not merely the account used to traverse it.

Organizational units are indispensable tools for operating Active Directory at enterprise scale. Their security value depends on the discipline with which they are used. When they separate administrative scopes, constrain delegation, and support distinct policy treatment for distinct trust levels, they strengthen the identity architecture. When they mix authority, conceal inheritance, or substitute for real security boundaries, they create pathways an attacker can use to move from routine administration toward consequential control.

The next section examines trust relationships between domains xand forests: the configurable mechanisms through which an identity recognized in one environment may be accepted in another.

### 6.3 Trust Relationships: Configuring the Movement of Identity

A trust relationship is a configured decision to accept authentication from an identity authority managed elsewhere.

In Active Directory, trusts allow identities from one domain or forest to be recognized by resources in another. They support legitimate requirements: shared services, enterprise applications, reorganizations, acquisitions, mission partnerships, administrative separation, legacy interoperability, and access across domain boundaries. Without some mechanism for cross-boundary identity recognition, many large organizations would be forced to create duplicate accounts, duplicate credentials, or brittle one-off integrations for every shared resource.

Trust is therefore mission-enabling infrastructure.

It is also a security decision with consequences that extend beyond the two domains shown on a diagram.

When a resource accepts authentication from an identity managed in another domain or forest, the resource owner is relying on the other environment’s identity proofing, credential management, authentication controls, privileged administration, monitoring, and compromise response. The trust relationship can be technically valid while still creating a risk that the receiving organization has not fully considered.

The critical question is not, “Do these domains trust each other?” It is:

> _Which identities may authenticate across the boundary, to which systems, under what conditions, and with what resulting authority?_

That question turns trust configuration into an analyzable security relationship.

#### 6.3.1 Trust Direction Describes Who Accepts Authentication

Trust direction is often confusing because the language is counterintuitive. The important operational concept is simple: a trusting domain or forest accepts authentication from identities maintained by a trusted domain or forest.

If Environment A trusts Environment B, then resources in Environment A can be configured to grant access to identities from Environment B. In that relationship, Environment A is relying on Environment B’s identity authority for the principals that cross the boundary.

The direction of trust does not automatically determine the scope of authorization. An identity accepted across a trust does not receive access to every resource in the trusting environment. Resource owners, group memberships, ACLs, application roles, selective-authentication settings, and other controls determine what authority follows successful authentication.

Authentication acceptance and authorization are separate decisions.

This distinction is important because a trust relationship may appear limited while the authorization model behind it is broad. A forest may accept identities from a partner environment only for a single application in principle, yet a broadly assigned group, unmanaged resource ACL, or inherited permission can allow those identities to reach more systems than intended. Conversely, a trust may technically permit cross-boundary authentication while carefully designed authorization controls limit access to a narrow mission function.

The trust is only the beginning of the access path.

#### 6.3.2 Transitivity Extends Relationships Beyond a Direct Connection

A transitive trust can extend authentication relationships beyond two directly connected domains according to the Active Directory trust configuration. In a forest, transitive relationships help domains recognize one another without requiring every pair of domains to be configured independently. This supports scalability and operational coherence within a shared directory framework.

The same convenience can obscure the reach of authority.

A defender evaluating a domain trust must determine whether the relationship is transitive, which additional domains may be involved, and whether the organization’s authorization model permits identities from those domains to reach sensitive resources. A direct connection on a diagram may represent a broader authentication path than its visual simplicity suggests.

A nontransitive trust is limited to the directly connected domains or forests. That narrower relationship can be useful where an organization needs a specific interoperability function without extending broader authentication recognition. It is not automatically secure. The access granted through the direct relationship may still be substantial, and the systems administering the trust can still become authority pathways.

Transitivity determines possible reach. Authorization determines realized consequence.

#### 6.3.3 Trust Scope Must Be Deliberate

A trust relationship should be designed according to the smallest practical identity population, resource set, administrative scope, and operational duration required for the mission function.

This principle applies whether the relationship is between domains within a forest, between separate forests, or between organizations. The broader the accepted identity population and the larger the set of reachable resources, the greater the dependency the trusting environment assumes on the security of the trusted environment.

Selective authentication can help constrain that dependency. It requires identities from the trusted environment to be explicitly permitted to authenticate to selected computers or services in the trusting environment. This provides an additional control point beyond the existence of the trust itself.

Selective authentication does not replace resource authorization. It adds a boundary before the destination system accepts the cross-trust authentication attempt. The destination still needs appropriate ACLs, application roles, group controls, monitoring, and administrative protection. The benefit is that the organization can reduce broad, implicit authentication reachability and make cross-boundary access more deliberate.

A constrained trust is stronger when its technical scope, authorization model, and administrative ownership agree.

An environment may also use other mechanisms to support cross-boundary access: federation, provisioning of separate accounts, application-specific identity brokering, certificates, or cloud identity services. The appropriate choice depends on mission need, assurance requirements, connectivity, ownership, lifecycle management, and recovery capability. The core principle remains the same: the organization should accept only the identity information and authority necessary for the defined purpose.

Interoperability should not become inherited administrative trust.

#### 6.3.4 Foreign Security Principals Represent External Authority Locally

When a domain grants access to a principal from a trusted external domain or forest, Active Directory can represent that principal through a foreign security principal object. This allows the local environment to assign permissions or group membership to an identity whose authoritative account is maintained elsewhere.

The mechanism is operationally useful. It also provides a visible reminder that the local environment has granted authority to an external identity source.

A foreign security principal should be reviewed with the same questions applied to local privileged identities: What resource or role recognizes it? Who approved the access? Which external environment manages the identity? What assurance and lifecycle processes does that environment provide? Who can change the local authorization assignment? How is access reviewed and removed? What happens if the trusted environment reports compromise or cannot provide timely revocation information?

The fact that an identity is external does not make its access less consequential. It makes the dependency more complex.

An external principal may be a partner user, contractor, mission collaborator, shared-service administrator, or identity from another organizational component. The organization must not assume that the external identity’s lifecycle, endpoint controls, credential policies, logging, or incident response processes are identical to its own. The access design should account for the difference rather than treating the trust boundary as invisible.

#### 6.3.5 Trusts Can Create Administrative Dependencies

A trust relationship is not controlled only by the settings visible in the trust configuration interface.

The identities capable of modifying the trust, the domain controllers that enforce it, the DNS and network paths required for cross-boundary authentication, the certificate or federation services supporting the relationship, the groups and ACLs granting access, the administrative workstations used to manage those components, and the monitoring systems recording the activity all influence the effective security of the trust.

An attacker does not necessarily need to alter the trust directly. Compromise of a trusted identity, an administrative endpoint, a synchronization service, or a resource authorization group may be sufficient to expand access across the boundary.

The organization should therefore map the full trust pathway:

* the identity source and credential accepted from the other environment;
* the trust configuration and its direction, transitivity, and authentication scope;
* the destination systems allowed to receive authentication;
* the groups, ACLs, applications, and roles granting authorization;
* the identities and systems capable of changing each stage;
* the network, DNS, certificate, or federation dependencies that support it;
* the evidence retained on both sides of the relationship; and
* the containment and recovery actions required if either environment is compromised.

A trust that cannot be explained across this pathway is not adequately governed.

#### 6.3.6 Federal and Mission-Partner Trust Requires Explicit Ownership

Federal environments frequently require identity interoperability across organizational boundaries. Shared services, joint operations, coalition activity, contractor support, legacy migrations, and interagency applications can all create legitimate pressure to recognize identities managed by another organization.

These relationships should not be treated as ordinary internal trusts with a different name.

The organizations involved may operate under different mission requirements, network conditions, credentialing processes, incident-reporting obligations, administrative models, and recovery capabilities. A cross-boundary trust must therefore include explicit agreements about identity proofing expectations, accepted credentials, authorization scope, system ownership, administrative roles, monitoring, notification, suspension authority, and incident coordination.

Technical configuration is necessary. Operating agreement is equally necessary.

A partner environment may be able to suspend a compromised user identity quickly while the relying organization must remove local group memberships or terminate active sessions. A relying application may detect suspicious use before the external identity provider sees the event. A trust outage may affect mission access across both environments. Recovery requires shared understanding of who acts first, what evidence is exchanged, and which party decides when the relationship may resume.

A trust without an incident and recovery model is an incomplete trust decision.

#### 6.3.7 Monitoring Cross-Boundary Authority

Cross-boundary authentication should be observable at the points where trust is accepted and where authorization is exercised.

The organization should be able to identify the external identity, its source environment, the destination system, the time and method of authentication, the resulting role or access, the source of the authorization assignment, and the administrative changes that established the relationship. It should also be able to distinguish routine mission use from unexpected expansion: new external identities receiving access, existing identities reaching new systems, changes to selective authentication or trust configuration, altered group memberships, unusual privileged activity, or administrative actions from unexpected paths.

Monitoring should also detect loss of visibility. If the organization cannot obtain expected identity, certificate, federation, DNS, or network evidence from a cross-boundary relationship, it may be unable to determine whether the trust remains safe to operate.

The absence of telemetry can itself change the risk decision.

Trust relationships are not binary switches marked secure or insecure. They are configurable pathways through which one environment accepts another environment’s identity authority. Their security depends on the purpose, scope, direction, transitivity, authorization, administration, monitoring, and recovery conditions surrounding them.

The next section examines cross-domain and cross-forest administration, where trust relationships become operational pathways for privileged work and where effective control can cross a boundary even without broad user access.

### 6.4 Cross-Domain and Cross-Forest Administration: When Trust Becomes Control

Cross-boundary access becomes most consequential when it enables administration.

A user from one domain or forest may require access to a shared application, file service, collaboration platform, or mission system managed in another environment. That access can be constrained to a defined resource and role. Cross-domain or cross-forest administration is different. It permits an identity, management platform, service account, or workflow controlled in one environment to alter the configuration, credentials, policies, systems, or authorization decisions of another.

That relationship can be necessary. It must be treated as an authority pathway.

An administrator may manage resources in another domain because the organization operates a centralized service model. A shared directory-services team may support several domains or forests. A PKI team may administer certificate services used across organizational components. A cloud identity platform may synchronize attributes from one environment while writing access-related data into another. A security operations team may need remote visibility and response capability across mission boundaries. A joint operation may require designated administrators to support a shared service under a formal agreement.

The operational justification may be sound. The security question is whether the authority has been constrained to the function required.

The fact that an administrator is trusted to perform work in another environment does not mean the administrator, the administrator’s endpoint, the administrator’s management tools, or the administrator’s home environment should be treated as implicitly trusted for every purpose in the destination environment.

#### 6.4.1 Administrative Access Carries the Security Posture of Its Source

An administrative session crossing a domain or forest boundary carries more than a username. It carries the security posture of the identity, endpoint, credential, management tool, and administrative process from which the session originated.

An administrator using a hardened privileged-access workstation, a dedicated administrative identity, approved strong authentication, a constrained management path, and an accountable change process presents a different risk from an administrator connecting from a general-purpose workstation through an informal remote-access path. Both may be technically able to authenticate across the trust. Only one may satisfy the destination environment’s requirements for privileged administration.

The destination must evaluate the source according to the authority it is being asked to accept.

This is particularly important where environments have different mission consequences, protection requirements, or administrative models. A lower-trust environment should not become a launch point for administration of a higher-trust environment merely because a trust relationship, remote-management path, or shared service makes it technically possible.

A cross-boundary administrative path should therefore identify:

* the administrators and service identities permitted to use it;
* the source endpoints, jump hosts, or management platforms from which it may originate;
* the credentials, authentication methods, and session protections required;
* the target systems and administrative functions within scope;
* the network and protected-communications paths that support the connection;
* the approval, change-management, and emergency-use conditions governing the activity;
* the evidence retained by both source and destination environments; and
* the containment and recovery procedures used if the source environment is suspected of compromise.

These conditions should be defined before an incident, not inferred from access permissions during one.

#### 6.4.3 Shared Administration Can Defeat Intended Separation

Separate domains or forests are sometimes created to support administrative separation. That separation may be weakened if the same people, credentials, workstations, management platforms, certificate authorities, or recovery systems can control all environments without meaningful distinction.

Shared administration is not automatically unsafe. It may be the most practical model for an enterprise service. It does, however, change the boundary’s security meaning.

If one privileged account administers several forests, compromise of that account may affect all of them. If one endpoint-management platform can deploy configuration to systems in several domains, compromise of that platform may cross the intended administrative separation. If one password vault holds secrets for multiple environments, the vault becomes a shared authority concentration point. If one recovery team can restore domain controllers across separate forests, its identities, tools, backups, and procedures require protection proportionate to every environment they can influence.

The separation is only as strong as the independence of the authority paths that cross it.

This principle also applies to service identities. A synchronization account, monitoring account, backup account, deployment account, or identity-governance connector may be granted permissions in more than one domain or forest because it supports a shared function. Such an account can become a bridge of effective control between environments even if no human administrator routinely signs in across the boundary.

The organization must determine whether the shared function requires that breadth of authority and whether the account’s credential, host, administrators, logs, and recovery process are protected accordingly.

#### 6.4.4 Cross-Boundary Groups and Authorization Require Special Care

Authorization across domains and forests is frequently implemented through groups. A resource in one environment may grant access to a group containing identities from another. A local group may include foreign security principals. An application may map external identities or claims to internal roles. A centralized identity-governance platform may assign membership according to authoritative data managed elsewhere.

These mechanisms are useful because they allow the destination environment to define its own authorization rules while accepting selected external identities.

They can also create a false sense of local control.

A destination group may be owned locally, but its members may be managed in an external domain. An external identity may be disabled by its home organization while retaining active sessions or cached authorization in the destination. A synchronization delay or failure may prevent a removal decision from reaching the resource that must enforce it. An administrator in the source environment may be able to alter attributes or memberships that the destination interprets as access eligibility.

The destination organization must understand where the authorization decision truly originates.

If an internal application grants access because an external group or attribute is synchronized into a local directory, then the source environment’s ability to change that group or attribute is part of the application’s authorization boundary. If a local group contains foreign security principals, then the management of the local group and the lifecycle of the external principals both affect access. If a federation assertion carries a role-related claim, then the issuer’s claim policy and the relying application’s mapping rules must both be governed.

No cross-boundary authorization model is complete until it identifies the identity source, the local enforcement point, and the administrators capable of changing either.

#### 6.4.5 Remote Management Tools Can Become Forest Bridges

Cross-boundary administration rarely occurs through directory tools alone. It may depend on endpoint-management systems, remote-support platforms, vulnerability scanners, backup and recovery tools, monitoring agents, automation frameworks, cloud administration portals, configuration-management services, or privileged-access management platforms.

These tools are often introduced to reduce operational cost and improve consistency. Their authority must be evaluated according to their reach.

A tool that can authenticate to systems in multiple forests, deploy agents, execute scripts, retrieve credentials, alter local administrators, modify firewall rules, or reconfigure services may create an administrative bridge between those forests. The tool may not appear in a domain trust diagram. Its compromise can nevertheless provide the means to traverse the authority boundary the diagram suggests.

The relevant question is not whether the tool is formally part of Active Directory. It is whether the tool can change the conditions under which Active Directory authority is exercised.

A shared management tool should therefore be assessed for its administrative identities, source infrastructure, network reachability, supported actions, credential stores, logging, tenant or forest separation, software-update process, backup practices, and incident-recovery plan. If it can influence more than one high-trust environment, it requires a security model proportionate to the combined consequence.

The same principle applies to cloud-connected administration. A cloud control plane, synchronization service, or identity-governance platform may provide centralized management across on-premises domains and forests. It can improve visibility and lifecycle discipline. It can also become a high-value authority concentration point if its service identities, write permissions, federation relationships, or administrator roles can alter sensitive on-premises identity functions.

Centralization is not inherently dangerous. Unexamined central authority is.

#### 6.4.6 Cross-Boundary Incident Response Requires Coordinated Authority

When compromise affects a cross-domain or cross-forest administrative pathway, technical containment must be coordinated with the organizations that own the relevant identity sources, targets, and network boundaries.

One team may control the compromised administrator account. Another may own the destination domain controller or application. A third may operate the privileged-access workstation, certificate authority, management platform, or network gateway used in the session. The organization must be prepared to decide who can disable access, isolate systems, revoke credentials, inspect logs, suspend a trust, validate replication, and authorize restoration.

Delays in those decisions can allow an attacker to preserve authority across the boundary.

The incident process should therefore establish contact paths, decision authority, evidence-sharing procedures, and predefined containment options for high-value cross-boundary relationships. These may include suspension of specific accounts, removal of foreign-principal access, termination of privileged sessions, restriction of management paths, isolation of a shared platform, temporary disabling of synchronization, or, when necessary, suspension of a trust or federation relationship.

The scope must match the evidence. A single compromised external account may require targeted removal of access. Evidence that a source environment’s privileged administration or credential issuance capability is compromised may require the destination to treat a broader set of external identities or assertions as untrusted until the relationship can be revalidated.

Cross-boundary recovery is complete only when both sides can account for the authority that was accepted and the conditions under which it will be accepted again.

#### 6.4.7 The Operating Standard for Administrative Trust

A trust relationship can support authentication. Cross-boundary administration grants the ability to change trust.

That distinction should drive the design. Routine interoperability should not automatically create administrative reachability. Administrative reachability should not automatically permit shared privileged identities. Shared privileged identities should not automatically be usable from shared endpoints or management platforms. And no cross-boundary path should exist without an accountable owner, protected source, narrowly defined target scope, evidence of use, and recovery procedure.

The strongest administrative boundary is not the one with the most elaborate diagram. It is the one in which every path capable of crossing from one authority system into another is known, necessary, constrained, monitored, and revocable.

The next section examines identity dependencies that extend beyond native trust configuration—including shared credentials, certificates, synchronization, policy management, and recovery services—and explains why these dependencies can weaken a directory boundary even when formal trusts appear tightly controlled.

### 6.5 Shared Services and Hidden Dependencies: Authority Beyond the Trust Configuration <a href="#id-65-shared-services-and-hidden-dependencies-authority-beyond-the-trust-configuration" id="id-65-shared-services-and-hidden-dependencies-authority-beyond-the-trust-configuration"></a>

A forest or domain boundary can be technically well configured and still be weakened by services that operate across it.

Trust relationships are visible because Active Directory represents them explicitly. Shared administrative dependencies are often less visible. They may exist in certificate services, synchronization platforms, endpoint-management systems, privileged-access tools, backup infrastructure, monitoring agents, credential vaults, identity-governance workflows, shared DNS services, cloud control planes, or recovery procedures. These components can create cross-boundary authority even when the formal trust configuration is narrow.

A defender who reviews only domains, forests, and trust objects sees only part of the environment.

The broader question is this:

> _Which shared identities, systems, services, or recovery capabilities can alter authority in more than one environment?_

The answer identifies the dependencies that can turn nominal separation into operational interdependence.

#### 6.5.1 Shared Credentials Create Shared Risk <a href="#shared-credentials-create-shared-risk" id="shared-credentials-create-shared-risk"></a>

A credential should represent a defined identity and a defined purpose. When the same credential is used across several domains, forests, enclaves, applications, or management platforms, compromise of that credential can create access beyond the location where it was first exposed.

The most obvious example is a privileged account used to administer multiple environments. The account may be convenient for a centralized operations team, but it becomes a single point of authority across every environment that accepts it. If an attacker compromises the administrator’s endpoint, credential, token, session, or management workflow, the attacker may inherit the same cross-boundary reach.

The same condition can arise with service identities.

A backup account may be able to access recovery material in several forests. A monitoring account may query or administer systems across multiple domains. An automation credential may deploy configuration to several environments. A synchronization account may read identity data from one domain and write it into another. A shared password-vault identity may retrieve secrets for several administrative boundaries.

The credential is not merely a convenience. It is an authority bridge.

This does not mean every shared service identity must be prohibited. Federal enterprises often require centrally managed services. It means that the organization must assess the credential according to the combined consequence of every environment it can affect. Its storage, authentication method, source hosts, administrative owners, permitted network paths, monitoring, rotation, and recovery procedures should reflect that combined authority.

A credential that can cross several boundaries should not be protected according to the least sensitive one.

#### 6.5.2 Certificate Trust Can Extend Beyond Directory Trust <a href="#certificate-trust-can-extend-beyond-directory-trust" id="certificate-trust-can-extend-beyond-directory-trust"></a>

Certificate-based authentication can create identity dependencies that do not appear in a conventional domain-trust diagram.

A system may accept a certificate issued by an enterprise certificate authority, a Federal PKI participant, a partner organization, or another trusted certificate hierarchy. The certificate can establish an authentication relationship independently of whether the user’s home account resides in the same domain or forest as the relying service. If the relying service maps certificate information to a local identity, role, or authorization decision, the certificate issuer and enrollment process become part of the access boundary.

This can be mission-enabling. It can also become a hidden route to authority.

A certificate authority capable of issuing certificates accepted for privileged access in several environments holds influence over each of those environments. A template or enrollment process that allows an inappropriate identity to obtain such a certificate can create cross-boundary consequences. A compromised private key can be used wherever the credential is accepted. A failed revocation mechanism can allow a credential to remain usable after the organization believes access has been removed.

The organization must therefore identify which certificate authorities are trusted by each environment, what credential uses are permitted, which identities can administer the relevant certificate services, and how certificate trust is suspended or re-established after compromise.

A trust boundary is only as strong as the credential authorities it accepts.

#### 6.5.3 Synchronization Can Move Authority Without Interactive Logon <a href="#synchronization-can-move-authority-without-interactive-logon" id="synchronization-can-move-authority-without-interactive-logon"></a>

Identity synchronization is often designed to reduce administrative burden. It can provision accounts, align attributes, update memberships, support cloud access, synchronize identities between directories, and automate lifecycle changes based on authoritative records.

Those functions can also move authority across boundaries without an administrator interactively logging on to either environment.

A synchronization service may read account data from one domain, transform it according to business rules, and write it into another directory, cloud tenant, application, or identity-governance platform. If the destination treats the synchronized data as authoritative for access, the source system and synchronization workflow become part of the destination’s authorization model.

The critical question is not only whether synchronization is working. It is what the synchronization process is allowed to change.

A connector permitted to update contact information may present limited risk. A connector able to create accounts, modify group membership, write role-related attributes, manage service identities, alter authentication-related settings, or provision access to privileged systems holds materially greater authority. The same is true of the service identities, management systems, and administrators capable of changing the synchronization rules.

A synchronization boundary should therefore be documented as an authority pathway: source data, transformation logic, service identity, destination permissions, approval process, monitoring, exception handling, and recovery procedures.

When any part of that pathway is compromised, the organization must determine whether the attacker could have changed not only identity data, but the rules through which authority is propagated.

#### 6.5.4 Shared Management Platforms Can Override Formal Separation <a href="#shared-management-platforms-can-override-formal-separation" id="shared-management-platforms-can-override-formal-separation"></a>

Management platforms often have broader reach than the administrators who use them recognize.

An endpoint-management platform may deploy software and configuration to systems in several domains. A remote-support tool may establish sessions to systems across organizational boundaries. A vulnerability-management platform may run privileged scans or deploy agents. A backup system may access directory databases, system state, certificates, and privileged recovery material. A monitoring platform may hold credentials capable of querying sensitive systems or responding to alerts automatically.

Each tool may have a legitimate function. Its cross-boundary authority must be explicit.

A platform that can modify systems in multiple forests is not neutral supporting infrastructure. It is a shared administrative dependency. If it can deploy software to privileged-access workstations, domain controllers, certificate authorities, or synchronization servers, it may hold effective control over the identity systems those assets support.

The organization should determine whether the platform’s reach is truly required, whether separate instances or management boundaries are appropriate for materially different trust levels, and whether the platform’s administrators, update mechanisms, agents, credentials, network paths, and recovery capabilities are protected accordingly.

Centralized administration can reduce cost and improve consistency. It can also concentrate compromise risk.

#### 6.5.5 Backups and Recovery Services Carry Authority Forward in Time <a href="#backups-and-recovery-services-carry-authority-forward-in-time" id="backups-and-recovery-services-carry-authority-forward-in-time"></a>

Recovery systems create a special form of dependency because they can reintroduce authority after the original system has changed.

A backup platform may contain directory data, system-state information, Group Policy content, certificate material, configuration records, privileged credentials, recovery keys, or other artifacts necessary to restore identity infrastructure. A recovery operator may be able to access those materials across multiple environments. A restoration process may be capable of returning a domain controller, certificate authority, privileged workstation, or management server to an earlier state.

That capability is essential. It must be governed as privileged authority.

A backup that contains the information needed to restore identity services can become a source of compromise if it is accessed, altered, encrypted, destroyed, or restored without adequate validation. A recovery operator who can restore several forests may represent effective control over all of them. A shared recovery vault may defeat administrative separation if the same identities can retrieve sensitive backup material across environments.

The security boundary must account for authority over historical state as well as current state.

Recovery planning should identify which people and systems can access identity backups, which environments the backups represent, how backup integrity is verified, how recovery credentials are protected, what approvals govern restoration, and how restored systems are validated before they are allowed to resume authority. Recovery must not become an unmonitored path through which an unsafe configuration, compromised credential, or stale privilege is returned to service.

#### 6.5.6 Shared Monitoring and Logging Require Careful Design <a href="#shared-monitoring-and-logging-require-careful-design" id="shared-monitoring-and-logging-require-careful-design"></a>

Centralized monitoring can improve detection by making cross-boundary patterns visible. It can also create dependency on a system that collects evidence from several environments.

A security platform capable of receiving logs, running response actions, deploying agents, accessing identity data, or initiating containment can become highly consequential. If it has only passive visibility, its authority may be limited. If it can disable accounts, alter network controls, isolate endpoints, rotate credentials, or modify policy, its role changes from observation to active administration.

The organization must understand that difference.

A shared monitoring platform should have carefully scoped permissions, protected administrative access, clear separation of duties, and evidence showing which analysts or automation workflows invoked response actions. Its failure must also be planned for. If central logging becomes unavailable, each environment needs a way to retain enough local evidence to support incident response and re-establish trustworthy operation.

Visibility is valuable, but a central visibility platform should not become an unexamined central control plane.

#### 6.5.7 Dependency Mapping Reveals the Real Boundary <a href="#dependency-mapping-reveals-the-real-boundary" id="dependency-mapping-reveals-the-real-boundary"></a>

The practical result is that a directory boundary must be mapped through dependencies, not inferred from architecture labels.

For every forest, domain, enclave, or mission environment, the organization should identify the shared services that can influence identity authority: certificate issuers, synchronization platforms, management tools, credential stores, administrative workstations, backup systems, recovery teams, logging services, cloud control planes, DNS infrastructure, network paths, and automation workflows.

The review should then ask:

* Which environments does this component influence?
* What identities, credentials, or privileges allow it to act?
* Can it read, modify, issue, deploy, restore, or revoke identity-related authority?
* Which lower-trust systems can affect it?
* What evidence records its actions?
* How is its authority constrained during normal operations?
* How is its authority suspended, investigated, and restored after compromise?

These questions expose whether a formal boundary is reinforced by operational independence or weakened by shared control.

The objective is not to prohibit shared services categorically. The objective is to make their authority deliberate. A shared service can be appropriate when it is mission-necessary, protected according to its highest consequence, monitored across its full scope, and supported by coordinated incident and recovery procedures.

A hidden dependency becomes dangerous when the organization discovers it only after compromise has already crossed the boundary.

The next section examines how to design and validate directory boundaries as operational controls: defining what trust may cross, limiting who can administer it, collecting evidence of use, and preparing to suspend or restore the relationship when conditions change.

### 6.6 Designing Defensible Directory Boundaries

A directory boundary is only truly defensible when the agency or command can explain what authority may cross it, who can change that authority, how its use is observed, and how it can be withdrawn when trust is no longer warranted.

This is a higher-standard than confirming that a domain, forest, firewall rule, or trust object exists. Technical boundaries are necessary because they provide the mechanisms through which separation can be implemented. Their security value depends on the operational decisions surrounding them.

A separate forest may provide meaningful separation from another forest. That separation is weakened if the same privileged account administers both, if a shared management platform can deploy configuration into both, if a common certificate authority can issue privileged authentication credentials for both, or if the same recovery system can restore their identity infrastructure without distinct controls.

A restrictive trust may limit which external identities can authenticate. That restriction is weakened if broadly managed groups grant access after authentication, if a synchronization process can add foreign identities to privileged ones, or if an external administrator can influence the destination through a shared service account.

The technical boundary must be reinforced by the authority model around it.

#### 6.6.1 Define the Mission Function Before the Trust Mechanism

The first design question is not, _"Which trust type should be configured?"_ It is, _"What mission function requires this identity relationship?"_

An environment may need to provide a partner population access to one application. It may need centralized support for a defined management service. It may need to synchronize a limited attribute set for lifecycle processing. It may need a recovery team to operate during a continuity event. Each requirement calls for a different relationship, different scope, and different controls.

Starting with the mission function prevents a common design failure that is often overlooked: establishing a broad technical trust because it is convenient, then attempting to constrain the resulting authority after access has already expanded.

A well-defined requirement should identify the identities involved, the destination resources, the permitted actions, the expected duration, the assurance requirements, the administrative owners, the network conditions, the monitoring expectations, and the conditions under which the relationship must be suspended or removed.

The design can then select the narrowest practical mechanism.

In some cases, a local account or separately provisioned identity may be more appropriate than accepting a broad external population. In others, a federated assertion may be preferable to a native directory trust. A limited synchronization process may be appropriate where direct administrative access is not. A selective-authentication configuration may be necessary where a standard trust would create too much reachability.

The right mechanism is the one that satisfies the mission without creating unnecessary authority.

#### 6.6.2 Constrain Identity Population, Resource Scope, and Administration Separately <a href="#constrain-identity-population-resource-scope-and-administration-separately" id="constrain-identity-population-resource-scope-and-administration-separately"></a>

Boundary design often fails because organizations constrain only one part of the relationship.

A trust may limit the identities permitted to authenticate but leave the destination resource scope overly broad. A carefully scoped application role may be protected by a broad administrative group that can change the role mapping. A network boundary may restrict ordinary client traffic while allowing a shared management platform unrestricted access to identity infrastructure. A service account may have narrow destination permissions but be usable from many poorly controlled hosts.

Defensible design constrains three dimensions independently:

1. **Identity population:** Which users, service identities, devices, applications, or external authorities may present an identity across the boundary?
2. **Resource and action scope:** Which destination systems accept that identity, and what authorization follows successful authentication?
3. **Administrative scope:** Which people, services, endpoints, and workflows can create, modify, approve, or recover the relationship?

A boundary is only as strong as its least constrained dimension.

For example, selective authentication can limit which destination systems accept users from a trusted environment. That is valuable. The organization must also limit which local groups grant those users access, who may modify those groups, where the external users’ authentication originates, and what monitoring identifies their use. Otherwise, the environment has constrained the first connection while leaving the authority granted after connection poorly governed.

The same logic applies to administration. A cross-forest management relationship may be restricted to a small team, but the destination remains exposed if that team’s privileged endpoint, password vault, automation platform, or recovery credential is broadly accessible in the source environment.

#### 6.6.3 Protect the Source of Privileged Authority <a href="#protect-the-source-of-privileged-authority" id="protect-the-source-of-privileged-authority"></a>

The security of a boundary depends heavily on the source from which privileged authority originates.

An administrator crossing into a higher-trust environment should use an identity dedicated to that function, a protected administrative endpoint, an approved and constrained management path, and credentials appropriate to the sensitivity of the destination. The source endpoint should not be exposed to the same activities, software, and network reachability as an ordinary productivity device. The management tools and service accounts used on that endpoint should be limited to the intended administrative scope.

This is not an argument that every administrative function requires a separate physical workstation or a new forest. It is an argument that the protection of the source must match the consequence of the destination.

A higher-trust environment should not depend on a lower-trust administrative source unless the organization has deliberately accepted, constrained, and monitored that dependency. If a shared platform must support several trust levels, its design should identify how those levels are separated in administration, credentials, network paths, logging, and recovery.

The attacker’s path frequently begins at the source. Protecting the destination alone is insufficient when an attacker can arrive through a trusted administrator, service identity, or management system.

#### 6.6.4 Make Boundary Changes Observable <a href="#make-boundary-changes-observable" id="make-boundary-changes-observable"></a>

A boundary that cannot be observed cannot be reliably governed.

The organization should retain evidence of changes to trust configuration, selective-authentication settings, cross-boundary groups, foreign security-principal assignments, certificate trust stores, federation settings, synchronization rules, network paths, privileged-access roles, service-account permissions, and recovery procedures.

The evidence should establish not only that a configuration changed, but also:

* which identity or automation process initiated the change;
* which source endpoint or management system was used;
* what approval, change request, or emergency authority supported it;
* which environments, identities, or resources were affected;
* whether the change expanded or reduced effective control; and
* whether the intended state was validated after implementation.

This standard is especially important for changes that appear routine. Adding an external principal to a group, allowing a service account to authenticate across a boundary, modifying a DNS record used for service location, or updating a synchronization rule may be operationally ordinary. Any of these actions can create a durable authority pathway if it affects a sensitive destination.

The organization does not need a crisis response for every change. It needs enough evidence to recognize which changes deserve one.

#### 6.6.5 Design Withdrawal and Suspension Before Normal Operations Begin <a href="#design-withdrawal-and-suspension-before-normal-operations-begin" id="design-withdrawal-and-suspension-before-normal-operations-begin"></a>

Every trust relationship should have a planned withdrawal path.

The relationship may need to be suspended because a partner identity authority is compromised, a certificate issuer can no longer be trusted, a synchronization service is malfunctioning, a shared management platform is under investigation, a mission requirement ends, or the destination discovers that the access model has expanded beyond its approved scope.

Suspension must be more deliberate than deleting a visible account.

The organization should know which authentication paths, active sessions, group memberships, certificates, service credentials, tokens, cached authorizations, replication dependencies, and application roles may remain after the primary relationship is disabled. It should know who has authority to suspend the relationship, which mission services will be affected, how users and partners will be notified, where evidence will be preserved, and what validation is required before the relationship may be restored.

A trust relationship that cannot be suspended safely is an unmanaged dependency.

This is particularly important in federal and mission-partner operations, where the pressure to preserve access can be substantial. A mission may depend on a shared service, coalition relationship, remote-support arrangement, or cross-organization credential. Those needs do not remove the requirement to contain a compromised authority. They make recovery planning more important because the organization must balance access continuity with the credibility of its identity decisions.

#### 6.6.6 Validate the Boundary Under Assumed Compromise <a href="#validate-the-boundary-under-assumed-compromise" id="validate-the-boundary-under-assumed-compromise"></a>

A boundary should not be accepted solely because the documented design appears correct. It should be tested against realistic failure conditions.

The organization should validate whether a lower-trust identity can affect a higher-trust system through delegated permissions, group nesting, policy management, certificates, synchronization, shared services, administrative endpoints, recovery infrastructure, or undocumented network routes. It should validate whether a compromised source environment can use an approved management pathway in an unintended way. It should verify that revocation, suspension, logging, and recovery processes function across the relevant boundary.

The objective is not to prove that every boundary can be defeated. Every complex environment contains operational constraints and residual risk. The objective is to identify where authority is broader than intended and determine whether the appropriate response is to remove the pathway, narrow it, protect it more strongly, monitor it more closely, or formally accept and manage the remaining risk.

A boundary is an operational control only when it performs as designed under pressure.

#### 6.6.7 Directory Boundaries as Living Security Decisions <a href="#directory-boundaries-as-living-security-decisions" id="directory-boundaries-as-living-security-decisions"></a>

Forests, domains, OUs, trusts, certificates, groups, synchronization services, management platforms, and recovery systems are not static pieces of architecture. They are continuing decisions about who may influence whom.

Those decisions change whenever an identity is provisioned, a group is nested, a delegation is added, a service account is granted access, a certificate issuer is trusted, a policy is linked, a management tool gains reachability, a backup process is expanded, or a partner relationship is approved.

The defender’s responsibility is to preserve a model of those changes that is detailed enough to expose effective control but practical enough to operate. That model should identify the authority boundaries that matter, the dependencies that weaken or reinforce them, the evidence that demonstrates their use, and the recovery actions required when an assumption of trust proves unsafe.

The security objective is not isolation for its own sake. Federal missions require cooperation, shared services, interoperability, and controlled access across organizational and technical boundaries. The objective is disciplined trust: authority granted for a defined purpose, limited to the necessary scope, protected according to its consequence, visible when it is exercised, and removable when conditions change.

The next section concludes the chapter by connecting forests, domains, organizational units, trusts, and shared dependencies to the defender’s central task: determining where authority can travel before an attacker demonstrates the answer.

### 6.7 Mapping Authority Before It Moves

The purpose of a directory-boundary design is not to make the environment difficult to understand. It is to make authority difficult to expand without authorization, evidence, and consequence.

Forests, domains, organizational units, trusts, groups, certificates, synchronization services, management platforms, and recovery systems all exist to support legitimate operations. They allow organizations to divide responsibility, provide access across missions, manage identity at scale, maintain availability, and recover from disruption. Their security significance emerges from the relationships among them.

An attacker does not need to respect the labels assigned to those relationships.

A forest boundary may appear separate while a shared administrative workstation can manage both forests. A domain may appear independently administered while a centralized endpoint-management platform can deploy configuration to its domain controllers. An organizational unit may appear to protect privileged accounts while inherited delegation permits a lower-trust support group to reset their credentials. A trust may appear limited while a broadly nested group grants the trusted identity access to sensitive systems. A certificate authority may not appear on the directory diagram at all while remaining capable of issuing a credential accepted for privileged authentication.

These are not exceptions to the architecture. They are the architecture that matters under compromise.

The defender must therefore maintain an authority map rather than relying only on an inventory or a static topology diagram. An inventory identifies components: forests, domains, domain controllers, groups, OUs, certificate authorities, synchronization servers, management tools, and administrative workstations. An authority map identifies relationships: which components can create, modify, authenticate, authorize, manage, recover, or observe one another.

That map should answer several practical questions.

First, where does identity authority originate? The answer may include domain controllers, certificate authorities, identity providers, personnel and sponsorship processes, application role stores, cloud identity platforms, and other authoritative sources. Each source should be associated with the specific trust decision it governs.

Second, where is that authority enforced? A directory may authenticate a user, but an application may decide the user’s role. A certificate authority may issue a credential, but a relying service decides whether to accept it. A synchronization service may write an attribute, but an application or cloud platform may turn that attribute into access. The authority map must identify both the source and the enforcement point.

Third, who can alter the relationship between the source and the enforcement point? This question exposes effective control. An identity that can change an authorization group, certificate template, synchronization rule, application mapping, Group Policy Object, trust configuration, or management-platform setting may influence access without directly appearing in the final authorization decision.

Fourth, from where can those changes be made? Privileged authority is exercised through endpoints, management tools, network paths, service identities, automation workflows, credential stores, and recovery capabilities. A directory administrator may be properly assigned a role but still represent a security risk if that role can be used from an ordinary endpoint or through a broadly administered management platform.

Finally, how can the organization withdraw and restore the relationship? Every authority pathway requires a credible containment and recovery model. The organization must know how to suspend access, terminate active sessions, revoke credentials, remove delegated rights, halt synchronization, isolate management systems, validate replication, preserve evidence, and determine when a relationship can safely resume.

A boundary that can grant authority but cannot safely remove it is incomplete.

#### 6.7.1 Mapping Must Include Intended and Unintended Paths

The obvious authority relationships are usually documented. Domain administrators administer domain controllers. PKI administrators manage certificate services. Endpoint teams manage endpoints. Application owners control application roles. Identity governance platforms provision accounts and groups. Backup teams maintain recovery capability.

The more difficult paths are indirect.

A help-desk group may control password resets for an OU containing an account with privileged access. A support team may manage a policy object linked to an administrative workstation population. A cloud connector may write an attribute consumed by a sensitive application. A vulnerability-management platform may hold credentials capable of reaching domain controllers. A backup service may contain recovery material for several forests. A certificate template may permit enrollment for a credential that a relying system maps to an elevated identity.

Each of these is an authority pathway because it can alter the conditions under which a more sensitive system makes a trust decision.

The purpose of mapping is not to imply that every relationship is unacceptable. Many are necessary. The purpose is to make their consequence visible so that the organization can decide whether the relationship is appropriately scoped, protected, monitored, and recoverable.

A useful authority map distinguishes three categories of relationship:

* **Direct authority:** The principal can immediately administer, authenticate as, configure, or otherwise control the target.
* **Delegated authority:** The principal can perform defined actions over the target or a defined set of related objects.
* **Effective authority:** The principal can influence another identity, system, credential, policy, or process that can in turn affect the target.

This distinction prevents the organization from treating a privileged-group roster as its complete Tier 0 model. Direct authority is important, but attackers frequently seek delegated and effective authority because those paths are less visible and may be less closely monitored.

#### 6.7.2 The Map Must Be Operationally Useful

An authority map should support decisions, not become a static documentation exercise.

During normal operations, it should inform access reviews, system integration, change approval, privileged-access design, control assessment, monitoring priorities, and contingency planning. Before a new application receives directory-write access, the map should help determine which attributes it can change and what downstream systems consume them. Before a management platform is allowed to reach a protected enclave, the map should identify whether that access creates effective control over identity infrastructure. Before a trust or federation relationship is approved, the map should show which credential authorities, groups, endpoints, and recovery processes become part of the dependency.

During an incident, the map should support scope decisions. If a privileged endpoint is compromised, responders need to identify which identities used it, which systems those identities administered, which management paths they could reach, and which credentials or sessions may require containment. If a synchronization service is suspected of compromise, responders need to identify its source data, destination permissions, attribute mappings, and dependent applications. If a certificate authority is affected, responders need to identify where its certificates are accepted and which issued credentials may need review or revocation.

The authority map turns a broad question—“What might this compromise affect?”—into a defensible investigation model.

#### 6.7.3 Ownership Must Follow the Map

Every material authority pathway should have accountable ownership.

The owner may not be a single person. A cross-boundary relationship can involve a mission owner, system owner, directory-services team, PKI team, application owner, network operator, security office, and risk-acceptance authority. But the organization must be able to identify who owns the purpose of the relationship, who operates its technical components, who monitors it, who can approve changes, and who has authority to suspend or restore it.

This ownership is especially important for shared services. A centralized management platform may be operated by one team while affecting multiple mission environments. A certificate authority may be managed by a PKI team while issuing credentials relied on by applications owned elsewhere. A synchronization service may be operated centrally while writing identity information into a destination controlled by another organization.

The technical owner cannot make all of the mission decisions. The mission owner cannot safely make decisions without understanding the technical pathway. Both must be connected through an operating model that recognizes the shared authority.

An unexplained relationship is difficult to defend. An unowned relationship is difficult to recover.

#### 6.7.4 Boundary Validation Is a Continuing Discipline

Authority maps decay when they are not tested.

Organizations change domains, migrate applications, adopt cloud services, replace management platforms, modify credential policies, reorganize personnel, retire servers, create exceptions, and respond to emergencies. Each event can alter a relationship that was previously safe. A new automation workflow may receive broader permissions than intended. A group may become nested into a more privileged role. A policy link may expand to a sensitive OU. A shared service may gain reachability into another forest. A recovery process may add a new administrator without corresponding monitoring or review.

Periodic validation should therefore test the relationships that matter most.

The organization should verify that lower-trust identities cannot modify privileged accounts, groups, policies, certificates, management systems, or recovery capabilities through overlooked delegation or inheritance. It should test whether privileged administration occurs only through approved endpoints and network paths. It should confirm that cross-domain and cross-forest access remains restricted to the intended identity population and resource scope. It should validate that evidence of material changes is retained and that emergency suspension procedures function as designed.

Validation is not a one-time proof that the environment is secure. It is a means of detecting where normal operational change has widened authority beyond its intended boundary.

The strongest result of validation is not a finding. It is an engineering decision: remove an unnecessary trust, narrow a delegation, separate a management path, isolate a service identity, strengthen a credential boundary, improve evidence collection, redesign recovery access, or formally accept a mission-required risk with controls proportionate to its consequence.

#### 6.7.5 The Chapter’s Central Conclusion

Directory boundaries are not defined only by the objects visible in Active Directory Users and Computers. They are defined by the full set of relationships through which authority can travel.

A forest provides a broad directory trust framework. A domain organizes authentication and administration within that framework. An OU scopes delegation and policy. A trust permits one environment to accept an identity managed by another. A group converts membership into authorization. A certificate can establish credential-based trust across a boundary. A synchronization service can move identity data between systems. A management platform can exercise control without appearing in a directory trust diagram. A backup system can restore authority long after the original configuration changed.

Each component is legitimate in the right design. Each can become a route to expanded control when its authority is broader than its mission purpose, when its dependencies are poorly understood, or when its use cannot be observed and withdrawn.

The defender’s responsibility is to identify those routes before an attacker does.

This chapter has established the structures through which Active Directory organizes and extends authority: forests, domains, OUs, trusts, shared services, and administrative dependencies. The next chapter examines Group Policy and configuration control, where directory authority is translated into changes in the operating systems, endpoints, and services that enforce the enterprise’s security posture.
