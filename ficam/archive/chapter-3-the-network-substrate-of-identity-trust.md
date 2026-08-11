# ❌ Chapter 3 - The Network Substrate of Identity Trust

### Abstract

Chapter 3 explains the network substrate that allows Active Directory to function as a distributed identity and authority service. Authentication, authorization, directory updates, policy processing, administrative access, logging, and recovery depend on network services that are often treated as background infrastructure. In practice, Domain Name System (DNS) directs clients and services toward identity resources; Active Directory sites influence service location and replication behaviors; replication carries directory changes among domain controllers, and Remote Procedure Call (RPC) supports critical management and directory operations.

The chapter examines these dependencies as security protperties rather than only performance or availability concerns. It analyzes how name resolution, site topology, replication schedules, firewall policy, routing, protected enclaves, and administrative connectivity shape normal operations and failure conditions. Particular attention is given to FICAM environments, where misssion separation, constrained connectivity, and protected communications can affect the availability and observability of identity services. The chapter distinguishes necessary segmentation from architectural isolation that prevents timely authentication, replication, monitoring, or recovery. It frames DNS records, site links, replication partners, and remote-management pathways as trust-relevant dependencies whose compromise, misconfigurations, or unavailability can alter the agency or command's control of its directory. Readers learn to model those dependencies and preserve evidence and recovery options when the network substrate becomes contested terrain.

### Key Terminology

* **Domain Name System (DNS):** The distributed naming service that translates names into network information and enables clients to locate domain controllers, services, and other domain-based resources.
* **Active Directory-Integrated DNS:** DNS zones stored in and replicated through Active Directory, allowing DNS data to follow directory replication and access-control models.
* **Service (SRV) Record:** A DNS record that identifies the location of a service, including domain controllers and Kerberos services used by Active Directory domain-joined clients.
* **Active Directory Site:** A logical representation of one or more well-connected IP subnets used to guide client service location and directory replication.
* **Subnet:** A defined range of Internet Protocol (IP) addresses associated with an Active Directory site so that clients can locate nearby domain-based services.
* **Site Link:** An Active Directory object representing connectivity between sites and used to influence inter-site replication behaviors.
* **Directory replication:** The process through which domain controllers exchange directory changes and converge on a consistent view of Active Directory information.
* **Knowledge Consistency Checker (KCC):** The Active Directory component that generates and maintains much of the replication topology between domain controllers.
* `SYSVOL`: The replicated domain controller share that stores Group Policy Objects (GPOs) and logon scripts required for consistent policy processing.
* **Remote Procedure Call (RPC):** A communications mechanism used by Windows and Active Directory services for many management, directory, and domain replication functions.
* **Service location:** The process through which a client identifies an appropriate domain controller or other service, generally using DNS records, site information, and network reachability.
* **Network segmentation:** The deliberate separation of networks or systems to constrain connectivity, reduce exposure, and enforce trust-based boundaries.
* **Protected enclave:** A network or operational environment separated according to mission, classification, organizational ownership, or security requirements.
* **Replication convergence:** The condition in which directory changes have successfully propagated to the domain controllers expected to receive them.

### 3.1 The Network Is Part of the Identity Control Plane

Active Directory cannot make trustworthy identity decisions if clients, domain controllers, certificate services, management systems, and logging infrastructure cannot reliably find and communicate with one another.

That dependence is easy to overlook because networking is often treated as a supporting service rather than as part of identity architecture. A directory diagram may show domains, domain controllers, organizational units, trusts, and administrative groups, while a separate network diagram shows subnets, routers, firewalls, encrypted links, and protected enclaves. In operation, those diagrams describe the same system. Identity authority depends on communications pathways. When those pathways are unavailable, misdirected, poorly protected, or inadequately understood, the agency or command's ability to authenticate users, enforce policies, replicate changes, detect compromise, and recover from failure is affected.

The network is therefore part of the identity control plane.

This does not mean every network device becomes a Tier 0 asset. It means that the network services and pathways required to effectively locate, reach, administer, replicate, and monitor identity authorities must be evaluated according to the consequences of their failure or manipulation. A domain controller that cannot be located through DNS may be operationally unavailable even when the server is deemed healthy. A domain controller that cannot effectively replicate may continue to provide authentication while holding outdated information about accounts, groups, passwords, policies, or permissions. A management workstation that cannot reach its intended administrative target may encourage unsafe workarounds. A logging system that cannot receive events may leave the organization unable to determine whether authority changed during an outage or suspected compromise.

Network failures are therefore not always separate from identity failures. They can create them, conceal them, or make their efforts harder to contain.

DNS is the first example. Users and administrators often think of DNS as the services that translates a familiar server name into an IP address. In an Active Directory environment, it performs a broader role. Clients use DNS to locate domain controllers, Kerberos services, Lightweight Directory Access Protocol (LDAP) services, Global Catalog Servers (GCS), and other domain functions. Active Directory uses DNS service records to publish the availability and location of those functions. A client does not ordinarily select a domain controller from a static list. It asks DNS to identify a domain controller capable of serving the relevant domain and, when site information is properly configured, one that is appropriate to the client's network location.

The availability and integrity of DNS affects the availability and integrity of service locations.

A poorly configured DNS environment can cause clients to contact distant or unintended domain controllers, create authentication delays, increase dependency on constrained links, or prevent systems from locating required services altogether. In a more serious condition, an unauthorized or incorrect DNS change can redirect a client or service toward an unintended destination. The defensive significance is not limited to whether a hostname resolves. The relevant question is whether the agency or command can establish that identity-dependent services are being located through authorized, accurate, and observable naming information parameters.

In an Active Directory-integrated DNS environment, DNS and directory replication are also connected. DNS zones may be stored within Active Directory and replicated among domain controllers. This design can simplify administration and align DNS access controls with directory security. It also means that changes to DNS data may be changes to directory-held identity dependencies. An agency or command that reviews directory permissions without considering who can create, alter, or secure DNS records has an incomplete view of its authoritative pathways.

Active Directory sites provide the enxt layer of network-aware identity behaviors. A site represents one or more well-connected IP subnets. It is not simply a physical building, a geographic region, or an organziational label. Its main purpise is to help clients located suitable services and to help domain controllers within that site before relying on a remote one. This reduces unnecessary use of wide-area or constrained connectivity and supports more predictable authentication and policy behaviors.

Site design has a security consequence because it directly influences where identity traffic travels and which authorities clients rely upon.

A site configuration that does not reflect actual network connectivity can cause clients to authenticate across unexpected links, depend on remote infrastructure, or bypass the service-location behavior the agency or command intended. In a federal environment, the consequences may extend beyond performance. A mission-separated enclave, a remote location, a protected connection, or a disconnected operational condition may require deliberate decisions about which domain controllers, certificate services, management tools, and logging systems remain reachable. A site topology that assumes unrestricted connectivity may fail at the moment the agency or command needs controlled identity operations most.

Replication carries directory authority across that topology. When a change occurs on a writable domain controller - such as the creation of an account, modification of a group, reset of a password, update to an access-control entry, or change to a Group Policy Object (GPO) - the change must replicate to the relevant domain controllers. Until replication converges, different domain controllers may hold different views of directory information. This is a normal property of distributed system architecture, not automatically evidence of compromise. It becomes a defensive concern when the agency or command cannot determine whether replication is delayed, incomplete, misdirected, or inconsistent with the approved topology.

The same principle applies to `SYSVOL`. Group Policy Objects and related policy content must be available consistently to the systems expected to process them. A directory change may be replicated while the related policy content has not yet reached a particular domain controller, or the reverse may occur. The defender must understand that policy authority depends on more than the visible Group Policy Console (GPC). It depends on the directory objects, file replication mechanism, domain controller health, network pathways, and endpoints processing that together determine what configuration is ultimately applied.

The next sections examine these dependencies in detail. They begin with DNS and service location, then move through sites, replication, RPC, segmentation, and the recovery implications of a network substrate that is inseperable from identity trust.

### 3.2 DNS and Service Location: Finding Authority

DNS is the mechanism through which an Active Directory client beings to locate authority. Before a user receives a Kerberos ticket, before a computer applies Group Policy, and before an administrator connects to a domain service, the requesting system must identify where the relevant service is available.

This is why DNS should not be treated as a generic network utility that sits outside identity security. In an Active Directory environment, DNS provides the naming and service-location information that directs clients toward domain controllers, Kerberos Key Distribution Centers (KDC), LDAP services, Global Catalog Servers (GCS), certificate services, and other identity-dependent resources. If that information is unavailable, inaccurate, manipulated, or unreachable, the identity function depending on it may fail or may be directed through an unintended pathway.

The basic process is straightforward. A client attempting to use domain services queries DNS for records associated with its domain. Active Directory publishes service records, commonly called SRV records, that identify systems offering particular functions. These records allow a client to discover, for example, a domain controller capable of providing Kerberos authentication or LDAP directory access. When Active Directory sites and subnets are correctly configured, the client can use this information to prefer a suitable service within its local site before contacting a remote domain controller.

The client is not simply asking, _“What is the address of the domain controller?”_ It is asking, _“Which authorized system provides the identity service I need, for this domain and from this network location?”_

This distinction gives DNS its identity-security significance.

A static list of server addresses may appear simpler, but it cannot provide the flexibility required by a distributed directory. Domain controllers may be added, removed, rebuilt, promoted, demoted, or temporarily unavailable. Services may be distributed across sites. A resilient identity environment needs clients to discover an appropriate authority dynamically. DNS makes that possible, but it also becomes a dependency that must be governed with the same care given to other authority-bearing components.

The first security requirement is availability. If clients cannot resolve the names or service records needed to locate identity infrastructure, they may be unable to authenticate, change passwords, apply policy, locate management services, validate certificates, or use applications that depend on directory queries. The consequences depend on the systems involved and on their caching behavior. Some users may continue operating for a period with existing sessions or cached credentials. Others may be prevented from accessing services immediately. Administrators may find themselves unable to reach the systems needed to diagnose the problem.

Availability is only the beginning.

The second requirement is integrity. A client that receives an incorrect answer may contact an unintended system. In ordinary operations, this can produce slow authentication, failed logons, certificate-validation problems, or unnecessary traffic across constrained links. In a security incident, unauthorized changes to DNS data can affect how clients discover services, which systems they attempt to contact, and where administrators direct privileged activity.

Not every incorrect DNS record is an attack. Stale records, failed dynamic updates, incomplete cleanup after server retirement, misconfigured forwarders, duplicate names, and inconsistent zone replication can all produce operational failures. The defensive point is that accidental and malicious changes can have similar effects on service location. The organization must preserve sufficient evidence to distinguish normal administration, configuration error, service degradation, and unauthorized modification.

That evidence includes more than DNS query logs. It includes the identity that changed the record, the administrative system used to make the change, the affected zone and record type, the replication path of the change, the systems that subsequently resolved or used the record, and the operational purpose the record was intended to serve. A high-value DNS change is not merely a data update. It may alter the route by which clients find identity authority.

DNS permissions must therefore be thoroughly analyzed as authoritative relationships.

In Active Directory–integrated DNS, zones can be stored within the directory and replicated through Active Directory replication. This design supports centralized management and can align DNS administration with directory access control. It also means that the ability to modify DNS zones or records may be granted through directory permissions, group membership, delegated administration, or control of a system that performs dynamic updates.

A team reviewing privileged directory groups may miss a principal that has no broad administrative role but can alter records in a zone used for critical identity services. Conversely, a DNS administrator may understand the operational importance of a zone without recognizing that its delegated permissions create a route into the identity control plane. The security review must bring those views together.

Dynamic DNS (DDNS) introduces a further operational consideration. Active Directory clients and domain controllers can register and update records automatically as their network information changes. This is necessary for normal service operation in many environments. It also requires careful ownership and update controls. The organization must know which systems are expected to register which records, how stale registrations are removed, which accounts perform updates, and how administrators will detect records created or changed outside normal behavior.

The goal is not to eliminate dynamic updates. The goal is to ensure that dynamic registration does not become unmanaged authority over service location.

DNS also intersects with administrative safety. Engineers under outage pressure may bypass intended naming and service-discovery processes by adding temporary host-file entries, using direct IP addresses, changing local resolver settings, or pointing systems toward an alternate DNS server. These actions can be reasonable emergency measures when controlled, documented, and removed after recovery. They become dangerous when they persist as undocumented operational exceptions or when they route privileged activity around the evidence and controls the organization relies upon.

An administrator who connects to a domain controller by IP address may still reach the intended server. But the organization loses part of the assurance that comes from controlled naming, expected service discovery, certificate validation, and auditable connection patterns. The issue is not that direct addressing is inherently malicious. It is that identity operations conducted through exceptions must remain accountable.

Federal and mission-separated environments add complexity because DNS design often reflects boundaries that are not visible in a single forest diagram. Different enclaves may use distinct zones, forwarding arrangements, resolver paths, administrative ownership models, or connectivity constraints. A protected boundary may permit certain identity services while restricting others. A disconnected or degraded condition may require local resolution and local domain services to continue operating. An external or partner service may need carefully limited name resolution without being permitted broad visibility into internal identity infrastructure.

These requirements make DNS architecture a matter of mission resilience as well as security.

The defender should be able to answer several operational questions before an incident occurs. _Which DNS zones support domain-controller discovery, certificate validation, administrative management, and mission applications? Which identities and systems can create, modify, or delete records in those zones? Which records are dynamically registered, and what normal behavior should that produce? Which clients and servers depend on cross-boundary resolution or forwarding? Which DNS logs are retained, protected, and correlated with directory changes? Finally, if a DNS authority is suspected of compromise, which identity services must be treated as potentially affected?_

Those questions transform DNS from a background service into an observable element of the identity trust system.

The next section examines Active Directory sites and subnets, which add location awareness to service discovery and determine how the directory adapts identity operations to the network paths available.

### 3.3 Active Directory Sites and Subnets: Locating Trust Across the Enterprise

An Active Directory site is a logical representation of network connectivity, not a synonym for a building, command, installation, region, or organizational unit.

That distinction is fundamental. Sites exist so that clients can locate appropriate directory services and so that domain controllers can replicate directory changes in a manner consistent with the network paths available to them. A site may correspond closely to a physical location, but it does not have to. A single installation may contain multiple sites if its networks have materially different connectivity characteristics. Several geographically separate locations may belong to one site if they are connected by reliable, high-bandwidth, low-latency infrastructure. The design decision should reflect communication reality rather than organizational naming convention.

For identity operations, this matters because Active Directory uses site information to make decisions about where authentication, directory queries, policy processing, and replication should occur.

A client determines its site by comparing its IP address to the subnets defined in Active Directory. When the client’s subnet is correctly associated with a site, the client can use DNS service-location records to prefer domain controllers and related services in that site. This reduces unnecessary dependence on remote infrastructure and helps ensure that authentication and directory activity follow the connectivity model the organization intended.

A missing subnet association may cause a client to be treated as outside a known site. An incorrectly assigned subnet may cause the client to prefer a remote domain controller when a local one is available, or to use a service across a constrained or protected connection. Overlapping, outdated, or poorly maintained subnet definitions can make service location inconsistent and difficult to troubleshoot. In a distributed enterprise, the resulting symptoms may appear as slow logons, delayed Group Policy processing, inconsistent authentication behavior, unexpected cross-site traffic, or avoidable failures during degraded connectivity.

Those are operational problems. They can also become security problems.

A client that normally authenticates within a controlled enclave but is redirected toward a remote service may cross a boundary the architecture was intended to limit. A remote-management session may depend on a path that is unavailable during an incident, encouraging administrators to bypass normal procedures. A system that cannot locate its expected domain controller may fall back to cached credentials or retain an older view of group membership and policy. A monitoring system may continue receiving some events while missing activity from another site whose connectivity has degraded.

The defender must understand not only whether the network is reachable, but whether identity traffic is following the intended path.

Federal environments make this especially important because the logical boundaries relevant to identity do not always align neatly with commercial branch-office design. A site may represent a deployed location, a data center, a mission enclave, a remote command element, a separated administrative network, or a set of networks operating under constrained communications. Connectivity may be shaped by bandwidth limitations, approved routing paths, protected communications equipment, mission conditions, classification boundaries, or planned disconnected operations.

The site topology must reflect those conditions without pretending that a network boundary is automatically an identity boundary.

A separate site does not create a separate domain. It does not prevent an identity from authenticating across sites when connectivity and authorization permit it. It does not independently establish a security classification boundary or enforce administrative separation. It influences service location and replication behavior. Security architects must avoid giving sites more meaning than the technology provides, while still recognizing that site design affects the practical behavior of a distributed identity system.

This distinction is important during both design and incident response.

During design, teams sometimes create sites according to organizational charts rather than actual network conditions. A site named for a command, agency component, business unit, or classification label may imply a security boundary that Active Directory itself does not enforce. Conversely, a technically appropriate site design may be misread by nontechnical stakeholders as a statement about organizational authority. Both errors create risk because they obscure where control is actually exercised.

During an incident, responders may assume that an affected domain controller serves only the clients physically nearest to it. That assumption may be false. Service location can change when a local domain controller is unavailable, when subnet information is incorrect, when DNS records are stale, or when clients fall back to remote services. An event affecting one site can therefore have consequences beyond its apparent geographic or organizational scope.

Site design must be analyzed alongside domain-controller placement.

A site containing no domain controller may be appropriate when reliable connectivity to another site is available and the operational consequences of dependency are understood. A site supporting mission-critical or disconnected operations may require local domain services, local DNS capability, locally available policy content, and a recovery plan that accounts for periods of limited reachability. The correct design depends on mission requirements, network conditions, availability objectives, and the authority held by the systems involved.

The security question is not whether every location needs its own domain controller. It is whether the organization has deliberately determined where identity authority must remain available and what happens when that authority cannot be reached.

This leads to a critical design tradeoff. Placing a writable domain controller in a remote or less protected location can improve local availability and reduce dependency on constrained connectivity. It also places a copy of directory authority in that location. The organization must then protect the server, its administrative interfaces, its physical environment, its backup and recovery processes, and the identities capable of managing it. Placing no local domain controller reduces that local concentration of authority but increases reliance on network paths and remote services.

Neither choice is inherently correct. The decision must be proportionate to mission need and the consequences of compromise.

Read-Only Domain Controllers (RODCs) may be appropriate in some scenarios because they can support local authentication and directory-service availability while limiting certain forms of writable directory exposure. They do not eliminate the need for careful design. The organization must still determine which credentials may be cached, which administrators can manage the system, what replication it receives, what local services depend on it, and how compromise would be detected and handled. A read-only role changes the risk profile; it does not remove the component from the identity architecture.

Sites also influence the replication topology through site links. A site link represents a connection between sites and provides Active Directory with information used to determine how intersite replication should occur. Site-link configuration can reflect expected connectivity, relative cost, scheduling, and availability. In principle, this allows the directory to favor reliable and efficient paths while controlling replication over limited links.

In practice, site-link configuration is often inherited, poorly documented, or treated as an availability setting rather than an authority decision.

That approach is insufficient. Directory replication carries changes to accounts, group memberships, passwords, permissions, policies, and other identity data. The timing and path of replication affect how quickly a security-relevant change becomes visible across the environment. A disabled account, revoked access path, emergency group-membership change, or remediation action may not have the same immediate effect at every domain controller while replication is incomplete.

This does not mean that every replication delay is a security incident. It means that defenders must know the expected convergence behavior for their environment and recognize when an incident requires verification that a change has reached the intended authorities.

A containment action is not complete merely because it was performed on one management console. The organization must confirm that the relevant directory and policy changes have replicated where they must take effect.

This requirement becomes more consequential across constrained links and protected enclaves. An organization may intentionally limit intersite replication because of bandwidth, mission availability, or network-security considerations. Those decisions can be appropriate. They must, however, be paired with procedures that address urgent security changes. If a compromise requires disabling an account, changing a privileged group, updating a policy, or revoking an administrative relationship, responders need to know which domain controllers and systems may continue operating with prior information and for how long.

The same reasoning applies to recovery. Restoring a domain controller, repairing a replication path, or rebuilding an isolated site is not simply a server-maintenance task. It requires an understanding of which directory data is authoritative, which changes must converge, which policy content must become available, and whether the restored system could introduce stale or untrusted information into the broader environment.

The defender’s visibility requirement is therefore broader than a replication-health dashboard. It includes the ability to answer:

* Which subnets belong to each site, and are those assignments current?
* Which domain controllers, DNS services, Global Catalog services, and administrative systems serve each site?
* Which clients depend on remote identity services?
* Which site links carry replication between identity authorities?
* What delays, outages, or restrictions are expected on those links?
* Which mission functions are affected if a site loses directory-service reachability?
* How are urgent security changes verified across all relevant sites?
* What recovery actions are required before a repaired site can again be trusted?

These questions establish whether the organization has designed its topology around actual identity dependencies or simply accepted the behavior that accumulated over time.

Active Directory sites and subnets are often described as performance features. They are better understood as location-aware controls over where identity services are discovered and how directory authority is distributed. When accurately designed and carefully maintained, they help the environment continue functioning predictably across distance, constrained connectivity, and mission separation. When neglected, they create hidden dependencies that become visible only during an outage, an incident, or an attempted recovery.

The next section examines replication itself: the mechanism by which Active Directory distributes identity authority and the conditions under which inconsistent, delayed, or untrusted replication can become a security concern.

### 3.4 Directory Replication: Distributing Identity Authority

### 3.4 Directory Replication: Distributing Identity Authority

Directory replication is the process that allows multiple domain controllers to maintain a consistent view of Active Directory identity information.

Without replication, a domain controller would represent only a local and potentially incomplete source of authority. An account created on one server would not be known to another. A password reset performed at one location would not necessarily be recognized elsewhere. Group memberships, access-control entries, computer objects, service identities, Group Policy links, and administrative delegations could diverge permanently among the systems expected to make the same identity decisions.

Replication makes the directory a distributed authority system.

That capability provides resilience and availability. Multiple domain controllers can authenticate users, process directory requests, and support dependent services without relying on a single server. It also creates a requirement for disciplined operations. A security-relevant directory change is not operationally complete when it has been made on one domain controller. It is complete when the change has converged across the domain controllers that must recognize and enforce it.

This distinction matters most during incidents.

If an account is disabled in response to suspected compromise, responders must determine whether the disablement has replicated to the domain controllers serving the affected population. If an emergency group-membership change removes privileged access, the organization must confirm that the updated membership is visible where authentication and authorization decisions will occur. If a delegated permission is removed, administrators must verify that the relevant directory replicas, policy-processing systems, and management tools have received the corrected information.

A change that has not converged may leave an attacker with a limited period in which earlier authority remains usable.

Active Directory is designed to manage normal propagation delays. Intrasite replication generally assumes reliable, high-speed connectivity among domain controllers within the same site. Intersite replication is designed for connections that may be slower, more constrained, or less consistently available. Site links, schedules, costs, topology, network reachability, and domain-controller health all influence how quickly changes move through the environment.

The existence of delay is not itself a defect. Distributed identity systems require organizations to understand the difference between expected replication behavior and a condition that threatens trust.

A defender should be able to distinguish among several operational states. The first is **normal convergence**, in which approved directory changes propagate within the organization’s expected timeframe. The second is **delayed convergence**, in which replication remains functional but does not meet the expected timing for the systems involved. The third is **replication failure**, in which one or more domain controllers cannot exchange needed changes. The fourth is **replication uncertainty**, in which the organization cannot establish whether a sensitive change has reached all relevant authorities.

The fourth state is especially dangerous during containment and recovery. An organization may know that an emergency action was taken but lack confidence that all domain controllers recognize it. In that condition, the issue is no longer simply directory health. It is uncertainty about where effective authority continues to exist.

Replication carries more than user and computer accounts. It distributes the objects and attributes that define directory behavior: groups, organizational units, service principal information, password-related changes, access-control entries, trust-related data, policy links, and many forms of administrative configuration. Because those objects can alter authentication, authorization, and administration, replication becomes part of the mechanism through which authority is extended across the enterprise.

A domain controller that receives a new privileged-group membership has received a change in authorization authority. A domain controller that receives an updated access-control entry may now recognize a different administrative relationship. A domain controller that receives a revised policy link may participate in distributing a changed configuration to endpoints. The technology is performing its intended function, but the security effect depends on whether the underlying change was authorized and whether the organization can recognize its propagation.

This is why replication monitoring cannot be limited to an availability metric.

A healthy replication dashboard can demonstrate that domain controllers are communicating. It cannot, by itself, establish that the replicated changes are legitimate, correctly scoped, or consistent with approved administrative intent. Conversely, a replication failure can become a security issue even when no malicious action occurred, because it can prevent containment changes from reaching the systems that must enforce them.

The operational objective is both **integrity** and **convergence**: approved changes must reach the appropriate domain controllers, while unauthorized or untrusted changes must be identified, contained, and prevented from becoming durable enterprise authority.

This objective has important implications for administrative practice. Emergency changes to identity infrastructure should include a validation step appropriate to their impact. An administrator who disables an account, removes a privileged membership, changes a policy assignment, or modifies a sensitive permission must not assume that saving the change in a management console means the enterprise has reached the intended state. The response procedure should identify the affected scope, the domain controllers expected to receive the update, the monitoring evidence that confirms propagation, and the fallback action if replication is unavailable.

The same discipline applies to planned changes. Routine administration becomes easier to defend when the organization can establish who made a change, what authority the change created or removed, how it moved through the directory, and whether it produced the intended result. Those records support troubleshooting, audit, incident investigation, and recovery.

Replication also complicates rollback.

A directory change that has propagated broadly cannot always be treated like a local configuration edit. Reversing it requires the organization to understand which state is authoritative, whether related objects or permissions changed at the same time, whether dependent systems have acted on the change, and whether a corrective action will itself converge as intended. In a sensitive incident, a poorly understood rollback can reintroduce an unsafe condition, overwrite legitimate changes, or make it harder to determine the sequence of events.

Recovery must therefore be planned around trusted state, not only service restoration.

This is particularly important when a domain controller is rebuilt, restored, isolated, or returned to service after suspected compromise. The organization must determine whether the system’s directory data, system configuration, credentials, policy content, and administrative history remain trustworthy. A server that appears operationally healthy may still be unsuitable for return to the replication topology if the organization cannot establish confidence in the state it will exchange with its peers.

The relevant question is not only, “Can this domain controller replicate?” It is also, “Should this domain controller be permitted to replicate?”

That question separates routine availability recovery from identity-trust recovery.

SYSVOL requires the same attention. Domain controllers replicate directory data and also maintain replicated policy content used by Group Policy and related functions. A Group Policy Object includes both directory-based information and associated file content. The two must remain available and consistent enough for clients and administrators to receive the expected policy behavior. If the directory portion of a policy change is present but the associated content is not, or if policy content is inconsistent among domain controllers, the organization may observe confusing and uneven results across endpoints.

For defenders, this means that policy remediation must be validated at more than one layer. Removing an unsafe configuration from a policy-management console is not sufficient if clients continue receiving stale policy content, if another domain controller has not converged, or if the attacker’s change affected a separate administrative pathway. Policy is authority expressed through configuration; its distribution must be treated accordingly.

Replication also has a visibility dimension. The organization should retain and protect evidence sufficient to answer which systems participated in a sensitive change, when replication began and completed, where it failed, and whether an unexpected domain controller or network path was involved. This evidence supports incident reconstruction, but it also supports decision-making during an active event. Responders cannot safely scope a containment action if they do not know which authorities have received it.

A mature operating model therefore treats replication as part of the identity incident process. Security teams, directory administrators, network operators, and mission owners need shared procedures for urgent identity changes. Those procedures should establish who can authorize the action, how its propagation is verified, what systems may retain prior state during a delay, and what additional controls are necessary while convergence remains incomplete.

In a large or mission-separated environment, replication may be constrained deliberately. A remote or protected site may have limited connectivity. An enclave may rely on planned synchronization windows. A disconnected operation may have locally available identity services that cannot immediately receive enterprise changes. Such constraints can be mission-appropriate. They must be accompanied by explicit decisions about risk: which accounts may authenticate locally, how emergency revocations are handled, what evidence remains available, and when a locally operated domain controller must be reviewed before reconnecting to broader authority.

The goal is not instantaneous replication under every condition. The goal is to know what the directory believes at each location, how quickly that belief can change, and what that means for access and containment.

Directory replication is often described as a technical process running quietly between servers. In operational reality, it is the mechanism through which identity authority becomes shared. Its health, timing, integrity, and recoverability determine whether the organization can apply trust decisions consistently across the environment.

The next section examines RPC and administrative connectivity: the communications mechanisms that allow directory services, management tools, and recovery operations to act across the network substrate.

### 3.5 RPC and Administrative Connectivity: Exercising Authority Across the Network

### 3.5 RPC and Administrative Connectivity: Exercising Authority Across the Network

Remote Procedure Call, commonly called RPC, is one of the communications mechanisms through which Windows and Active Directory systems perform administrative, directory, and replication functions across the network.

For defenders, the important point is not that every administrator must understand the internal implementation of RPC. The important point is that identity authority often depends on communications paths that are broader and more dynamic than a simple “server-to-server” firewall rule suggests. Domain controllers, management consoles, administrative workstations, directory tools, replication services, and supporting Windows components may rely on RPC to request information, perform changes, coordinate services, or administer remote systems.

When those paths are unavailable, poorly governed, or unnecessarily exposed, the effect can extend beyond operational inconvenience. The organization may lose the ability to perform emergency identity actions, validate replication, manage domain controllers, investigate a suspected compromise, or restore a trusted configuration.

RPC is therefore part of the administrative substrate of identity trust.

A common misunderstanding is to think of remote administration as a single protocol operating through a single predictable network port. In practice, Windows administrative functions may begin by contacting a well-known service endpoint and then establish communications through negotiated service ports. Firewalls, network-security devices, routing controls, host-based protections, and protected enclave boundaries must accommodate the required communication pattern for approved operations while still limiting unnecessary reachability.

That creates a design problem with direct security implications.

If connectivity is too permissive, a broader population of systems may be able to reach services that should be available only to tightly controlled administrative endpoints. If connectivity is too restrictive, administrators may be unable to manage domain controllers, perform replication diagnostics, restore services, apply emergency changes, or use the tools required during an incident. The proper solution is not unrestricted access and not indiscriminate blocking. It is deliberate, documented connectivity from authorized management systems to the identity infrastructure they are responsible for operating.

The source of an administrative connection matters as much as its destination.

An administrator connecting to a domain controller from a hardened, dedicated privileged-access workstation operates within a different risk boundary than an administrator connecting from an ordinary workstation used for email, web access, collaboration, and general productivity. Both connections may use valid credentials and approved administrative tools. The difference is the likelihood that the originating endpoint has been exposed to lower-trust activity, credential theft, malicious content, or unauthorized software.

The management session carries the authority of the administrator into the target system. If the source endpoint is compromised, the connection may become a route through which an attacker can observe, hijack, or misuse that authority.

This is why privileged administrative endpoints are part of the identity control plane. They are not interchangeable with ordinary workstations simply because they run the same operating system or can reach the same network. Their security posture must reflect the authority exercised from them.

Administrative connectivity should therefore be designed around three questions. First, which systems genuinely require the ability to administer domain controllers, certificate services, identity synchronization services, Group Policy, privileged groups, and other authority-bearing components? Second, which identities are authorized to perform those functions? Third, from which managed and monitored endpoints may those identities exercise that authority?

The answers should be narrow.

A broad enterprise-management platform may provide valuable operational capability, but it can also become a powerful authority pathway if it can deploy software, execute scripts, alter configuration, or create remote sessions on sensitive systems. The same principle applies to remote-support tools, endpoint-management platforms, vulnerability-management tools, backup systems, monitoring agents, automation frameworks, and orchestration services. Their intended purpose may be legitimate. Their effective authority must be evaluated according to what they can cause a high-trust system to do.

An administrative tool does not need membership in a privileged directory group to create a Tier 0 concern. If it can influence a system or identity that holds Tier 0 authority, it belongs in the Tier 0 security analysis.

Federal and mission-separated environments make this issue more complex because the necessary administrative path may cross several controls: segmented networks, controlled routing, boundary firewalls, protected communications equipment, jump hosts, remote-access gateways, and separately governed enclaves. Each control can reduce exposure. Each can also become a dependency during an incident.

The objective is not to remove every boundary between an administrator and a managed system. The objective is to ensure that the approved path remains available, observable, and recoverable without creating a less protected alternate path.

A recurring operational failure occurs when approved management connectivity is difficult to use during ordinary conditions. Administrators then develop workarounds: temporary firewall exceptions that become permanent, alternate remote-management tools, shared local administrator accounts, direct access from ordinary endpoints, unmonitored jump hosts, or informal network routes. These practices may resolve an immediate availability problem while quietly expanding the number of pathways through which identity authority can be reached.

The result is architectural drift.

Architectural drift is not always visible in a network diagram or a privileged-group review. It appears in the difference between the approved management model and the actual paths people use to complete their work. Defenders must periodically test whether high-impact administrative tasks can be performed through the intended systems, with the intended identities, under the intended controls. If routine operations depend on exceptions, the formal architecture is no longer the architecture that matters.

Visibility is central to this problem. The organization should be able to associate a sensitive administrative action with an identity, a source endpoint, a target system, an approved management path, and an outcome. A log showing that a directory object changed is valuable. It is more valuable when the organization can determine whether the change originated from an authorized privileged-access workstation, through an approved administrative session, by an identity assigned that role, and within an expected change window.

That context distinguishes accountable administration from activity that merely resembles it.

Administrative connectivity also affects incident containment. During a suspected identity compromise, responders may need to disable accounts, remove permissions, isolate systems, alter policy, inspect directory state, revoke certificates, or validate replication. If the organization cannot reach its authority-bearing systems through trusted management paths, it may be forced into hurried decisions from less secure endpoints or through improvised network changes. Those actions can expand the incident, impair evidence collection, and make later recovery harder to defend.

Resilience requires planned alternatives, but alternatives must remain inside the trust model.

A break-glass administrative process may be necessary for continuity of operations. So may an emergency management path when normal connectivity is unavailable. Such capabilities should be tightly controlled, documented, monitored, periodically tested, and designed so that their use creates a clear record. An emergency path is not a justification for unmanaged standing access. It is a recovery capability whose authority and conditions of use must be explicit before a crisis occurs.

The same discipline applies to firewall policy. Rules that permit administrative and identity-service communication should be based on defined sources, destinations, service requirements, and mission purpose. They should be reviewed when systems are added, retired, moved between enclaves, or assigned new authority. The purpose is not only to reduce the attack surface. It is to preserve an intelligible model of which systems can exercise or support administrative control.

A firewall rule can be an authority relationship expressed as network policy.

When a lower-trust management system is allowed to communicate with a higher-trust identity component, the organization should understand what that connection enables. Does it allow monitoring only, or configuration changes? Does it permit remote administration, file transfer, policy deployment, or credential use? Which service account, certificate, or administrator authenticates across the path? Can the connection be initiated in both directions? What logs show that it was used? What happens if the management system is compromised?

These questions connect network design to effective control.

RPC and administrative connectivity are often relegated to implementation details because they are difficult to explain without diagrams, firewall rules, and platform-specific settings. Their operational significance is more direct: they determine whether authorized personnel can safely exercise identity authority and whether unauthorized personnel can reach the same functions through a less protected route.

The next section examines network segmentation and protected enclaves, where those connectivity decisions become explicit boundaries between different levels of mission, operational, and identity trust.

### 3.6 Network Segmentation and Protected Enclaves: Boundaries That Must Hold

### 3.6 Network Segmentation and Protected Enclaves: Boundaries That Must Hold

Network segmentation is the deliberate use of technical boundaries to limit which systems may communicate, which services may cross between them, and how compromise can move through an environment.

In identity operations, segmentation is often discussed as a firewall or routing concern. That description is incomplete. A boundary affects identity when it determines where an identity can authenticate, which directory services it can reach, where a credential may be used, which administrative systems can manage a resource, how policy is distributed, and what evidence can be collected when activity crosses from one environment into another.

Segmentation is therefore not separate from identity architecture. It is one of the mechanisms through which the organization defines and enforces trust boundaries.

A well-designed boundary does not merely prevent arbitrary traffic. It expresses a decision about authority. A user network should not have the same ability to reach domain controllers as a dedicated privileged-administration network. A general-purpose endpoint-management platform should not automatically have unrestricted management access to systems that support enterprise directory authority. A development environment should not be able to influence a production identity service simply because the same administrative convenience is desired in both places.

The goal is not to make every network segment inaccessible to every other segment. Mission systems require communication. Authentication requires clients to reach directory services. Domain controllers require carefully controlled replication. Management teams require paths to the systems they administer. Logging systems require the ability to collect evidence. Certificate services, synchronization platforms, application servers, and endpoints may require specific identity-related communications to function.

The question is whether each path exists for a defined purpose and whether its authority consequences are understood.

A segmentation boundary is effective only when the organization can describe what crosses it. This includes more than network packets. It includes identities, credentials, authentication requests, directory queries, certificate validation traffic, replication changes, policy content, management sessions, remote commands, event records, backups, and recovery actions. A path that permits an administrator to manage a domain controller may also permit an attacker who compromises that administrator’s source system to attempt the same action. A path that allows a synchronization service to write attributes across an environment may also allow a compromised synchronization component to expand authority in its destination.

The boundary must be evaluated according to what the allowed communication enables.

This is especially important when network segmentation is mistaken for identity separation. Placing systems in different subnets, VLANs, sites, or firewall zones does not automatically prevent identities from crossing between them. If an account is recognized by a domain controller reachable across the boundary, and if authorization permits access to the destination resource, the network segmentation may limit the route without changing the underlying identity relationship.

Likewise, a separate Active Directory site does not establish a separate security boundary. A site influences service location and replication behavior. It does not, by itself, prevent authentication, administration, or trust relationships across sites. A separate domain or forest may create stronger administrative and authentication boundaries, but even those boundaries depend on the configuration of trusts, credentials, privileged access, synchronization, management systems, and cross-environment permissions.

The defender must distinguish carefully between boundaries that organize traffic and boundaries that constrain authority.

Federal environments often require multiple overlapping boundaries. An organization may separate systems by mission function, sensitivity, organizational ownership, geographic deployment, classification, operational availability, or connection to an external partner. NIPRNet, SIPRNet, JWICS, mission systems, coalition environments, cloud services, development environments, administrative networks, and remote operational sites may each impose different constraints on connectivity and identity use.

These are not simply larger versions of a commercial network with more firewall rules. They can represent distinct operating conditions in which the organization must decide which identities are recognized, which credentials are accepted, which administrative paths are permitted, which services remain available during degraded connectivity, and how evidence is retained and reviewed.

A boundary between enclaves should therefore be treated as an identity decision as well as a network decision.

For example, a mission requirement may call for limited access to a shared service across an organizational or mission boundary. The appropriate design question is not only whether the required ports can be opened. It is whether the destination should accept the originating identity directly, whether a separate identity should be provisioned, whether a brokered or federated assertion is appropriate, what authorization should follow successful authentication, which administrators can alter the relationship, and how the organization will detect or revoke inappropriate access.

The answers determine whether the connection is a narrowly bounded interoperability function or an unexamined authority pathway.

Protected communications equipment can reinforce such boundaries by limiting or securing approved connectivity between locations or enclaves. In classified environments, TACLANE encryptors and related protected-network architectures may be essential to maintaining approved communications paths. Those technologies do not authenticate users, authorize access, or administer directory objects. They nonetheless influence whether domain controllers can replicate, whether certificate validation can occur, whether administrators can reach management systems, whether logs can leave an enclave, and whether recovery procedures will function during degraded conditions.

The identity architecture must account for these dependencies without confusing network protection with identity assurance.

A secure communications path does not make every identity action crossing that path appropriate. Conversely, a strong identity control cannot fulfill its purpose if the necessary communications path is unavailable when the control must be exercised. Resilient design requires both: protected connectivity and deliberate identity authority.

Segmentation also changes incident response. During a suspected compromise, isolating a network segment may be necessary to prevent lateral movement or stop an attacker from reaching additional systems. But isolation can also interrupt authentication, replication, policy delivery, event forwarding, certificate validation, administrative access, and backup operations. A containment action that protects one system may leave another operating with stale identity data or without the ability to receive emergency revocations.

The correct response is not to avoid isolation. It is to understand the identity dependencies before isolation becomes necessary.

For each high-value enclave or identity boundary, responders should know which domain controllers and DNS services support it; which credentials and directory objects are required for continued operations; which management and recovery paths remain available; what directory or policy changes may fail to converge while it is isolated; and what evidence must be collected locally if centralized logging is interrupted. Those decisions should be made as part of architecture and continuity planning, not improvised during an intrusion.

A boundary also needs accountable ownership. Network teams may operate the firewall rules and routing policies. Directory teams may operate the authentication services. Application teams may control the resources being accessed. Security teams may monitor the resulting activity. The boundary will remain weak if no one is responsible for determining whether the total relationship still reflects mission need.

Ownership requires periodic review of the complete path: source identities, source systems, network controls, destination services, authorization rules, administrative privileges, logging, and recovery dependencies.

This review should look for two recurring conditions. The first is **excessive reachability**, in which a boundary permits more systems, identities, protocols, or administrative actions than its purpose requires. The second is **unsafe dependency**, in which a higher-trust function relies on a lower-trust component, network path, or administrative process without sufficient protection, monitoring, or recovery capability.

Both conditions create opportunities for an attacker to convert a local compromise into broader authority.

Segmentation becomes valuable when it forces a compromise to encounter another meaningful control: a distinct credential boundary, a hardened administrative endpoint, a restricted management path, a separate authorization decision, an inspectable broker, or a monitored transition between environments. A boundary that can be crossed with the same credential, from the same unmanaged endpoint, through broadly permissive connectivity, provides less protection than its diagram suggests.

The purpose of segmentation is not to create impressive diagrams. It is to make authority more difficult to expand, easier to observe, and more feasible to contain.

The next section examines how DNS, sites, replication, administrative connectivity, and enclave boundaries must be considered together during outages, compromise, and recovery.

### 3.7 Resilience, Recovery, and the Networked Identity Environment

### 3.7 Resilience, Recovery, and the Networked Identity Environment

An identity service is not resilient merely because its servers remain powered on. It is resilient when authorized users and systems can continue to make trustworthy identity decisions during disruption, and when administrators can restore those decisions without introducing unverified authority into the environment.

For Active Directory, that resilience depends on more than domain-controller redundancy. It depends on DNS availability, accurate service-location information, site and subnet design, replication health, SYSVOL consistency, administrative connectivity, protected management paths, event collection, backup access, and the network conditions required to use each of them. A failure in any one dependency can change what the organization is able to authenticate, authorize, observe, administer, or recover.

This is why continuity planning for identity infrastructure cannot be reduced to a list of replacement servers.

A domain controller may be available while clients cannot locate it because DNS is unavailable or incorrect. DNS may be available while the domain controller cannot replicate a security-critical change because intersite connectivity has failed. Replication may be functional while SYSVOL content is inconsistent, producing different Group Policy results across the environment. Domain services may continue to authenticate users while the administrative network required to perform emergency containment is unreachable. Central logging may be unavailable while local identity services continue operating, leaving the organization unable to determine what changes occurred during the disruption.

Each condition produces a different form of degraded trust.

The organization must distinguish between **service availability** and **trust availability**. Service availability asks whether a component is operating and reachable. Trust availability asks whether the organization can rely on the identity decisions that component is making. A domain controller that continues to issue authentication responses while it holds stale group membership, has not received an emergency account disablement, or cannot be verified against the expected replication state may be available as a service but uncertain as an authority.

That distinction should govern incident decisions.

During an outage, teams are often under pressure to restore connectivity quickly. During a suspected compromise, they are under pressure to isolate affected systems quickly. Both impulses are understandable. Neither should bypass the question of what authority will be restored, isolated, or permitted to replicate as a consequence.

Restoring a network link may allow needed authentication and replication to resume. It may also reconnect a domain controller whose state has not been assessed after compromise. Reconnecting an enclave may restore central logging and administrative access. It may also allow an attacker still present in that enclave to resume access to broader identity services. Isolating a site may limit adversary movement. It may also prevent urgent credential revocations, policy updates, or directory changes from reaching systems that continue operating locally.

The correct decision depends on the available evidence, the authority at risk, the mission requirement, and the recovery options that have been prepared in advance.

A mature recovery plan identifies the identity functions that must remain available in each operating condition. For a major site, mission enclave, or protected environment, the organization should know whether it requires local DNS, local domain controllers, Global Catalog availability, certificate-validation capability, local policy content, administrative access, event retention, backups, and alternate communications paths. It should also know what identity functions may be unavailable or constrained during isolation, degraded connectivity, or disconnected operations.

These are mission decisions, not only technical preferences.

A remote site may accept dependency on centrally hosted directory services when connectivity is reliable and the mission can tolerate a temporary loss of access. A mission environment that must continue during constrained or disconnected operations may require local identity services and carefully designed credential-caching behavior. That local capability improves continuity, but it also creates a need to protect and eventually revalidate the local authority. The more independently an enclave can operate, the more deliberately the organization must plan how it will reconnect, replicate, review changes, and restore confidence after separation.

Recovery planning must also identify trusted administrative paths.

An incident-response team cannot depend on ordinary user endpoints to administer compromised identity infrastructure. If a privileged administrative workstation, jump host, management network, or remote-access gateway is unavailable, the organization needs an approved alternative that remains inside the identity trust model. That alternative may involve designated emergency workstations, protected break-glass credentials, out-of-band communications, controlled physical access, or prepositioned recovery tooling. Its precise form will vary by environment. Its essential characteristics should not: its authority must be limited, its use must be recorded, and personnel must test it before an incident makes it necessary.

A recovery capability that has never been tested is an assumption, not a control.

Backups form part of this recovery system, but they should be understood as more than copies of server data. A useful identity recovery capability must preserve the information, configurations, credentials, and procedures required to restore a known and trustworthy state. For directory services, that may include system-state backups, documented domain-controller roles, DNS configuration, site topology, replication relationships, SYSVOL and Group Policy content, certificates, recovery keys, privileged-account records, and the protected access needed to use the backups safely.

The question is not only whether a backup exists. It is whether the organization can establish what it will restore and whether that state is appropriate for the incident.

A backup taken before a compromise may be valuable because it represents a known earlier state. It may also lack later legitimate changes to accounts, groups, policies, and applications. A backup taken after compromise may contain attacker-established persistence or altered authority. Recovery decisions must therefore combine technical restoration with a review of identity changes, evidence, and mission requirements. The objective is not to return every system to the most recent possible state. It is to restore a state the organization can again trust.

This requirement is particularly important for domain controllers. Returning a domain controller to service is not solely a matter of successful boot, network reachability, and replication status. The organization must determine whether the server’s operating system, directory database, credentials, administrative configuration, policy content, and recent change history are suitable for rejoining the identity authority system. A compromised or uncertain domain controller should not be permitted to exchange directory state with healthy peers merely because doing so would restore apparent availability.

Recovery begins with trust assessment.

The same principle applies to DNS and network services. A DNS server may appear healthy while holding unauthorized, stale, or incomplete records that affect service location. A firewall or routing configuration may restore connectivity while allowing an unintended management path. A site-link configuration may resume replication while using a route that does not align with the intended protected boundary. In each case, the organization should validate both the technical function and the authority consequence of the restored configuration.

This is where evidence becomes indispensable.

During a network or identity incident, logs, configuration records, change tickets, replication data, administrative-session records, and endpoint telemetry support more than retrospective investigation. They allow decision-makers to determine what remains trustworthy at the moment of recovery. If evidence shows that a privileged account was used from an unapproved endpoint, the organization may need to treat more than that account as affected. If evidence cannot establish whether an emergency permission change replicated before a link failed, the organization may need to assume that some systems retain the prior authority. If logs from an isolated enclave are incomplete, the organization may need a more cautious process before reconnecting it to enterprise identity services.

Trust recovery should be proportionate, but it must be evidence-led.

The network substrate also affects the speed of recovery. Poorly documented DNS dependencies, unmanaged firewall exceptions, obsolete subnet assignments, untested site links, and informal administrative routes turn a contained technical failure into a prolonged operational problem. Teams spend critical time rediscovering which systems depend on which services, which ports or paths are necessary, which records are authoritative, and which exceptions were created years earlier to keep the environment functioning.

Documentation is therefore a recovery control when it reflects the operating environment as it actually exists.

The required documentation is not an exhaustive archive of every configuration detail. It is an accountable map of authority-dependent operations: where identity services reside; how clients locate them; how directory changes replicate; which boundaries constrain communication; which systems administer sensitive components; which logs record material changes; which recovery paths exist; and who owns the decisions associated with each dependency.

That map must be kept current through operational use. A diagram that is never consulted during change planning, exercises, outage response, or incident investigation will not remain a dependable representation of the environment.

The organization should test recovery under conditions that resemble its actual risk. A test that restores one server in an unrestricted laboratory network may demonstrate only that the software can be reinstalled. It does not establish that the organization can recover identity services when DNS is degraded, administrative paths are restricted, replication is incomplete, central logging is unavailable, or a protected enclave must be reconnected safely.

The more consequential the identity authority, the more realistic the recovery validation should be.

The network substrate is often invisible when it works well. DNS resolves, clients locate services, replication converges, administrators connect through approved paths, logs arrive, and site boundaries behave as intended. During disruption, those quiet dependencies become decisive. They determine whether the organization can contain compromise without losing mission access, restore services without restoring attacker control, and establish that its identity decisions are once again worthy of trust.

Chapter 3 has treated DNS, sites, replication, RPC, administrative connectivity, segmentation, and recovery as parts of the same security problem. Together, they form the communications foundation on which directory authority is located, distributed, exercised, observed, and restored. The next chapter turns from that technical substrate to the federal governance structures that define how identity assurance, credentials, access decisions, and accountability must be managed.



<br>

\
<br>

\
<br>

<br>

\
<br>

\
\
<br>

<br>

\
<br>

<br>

\
\
<br>

<br>

\
\
\
<br>

<br>

<br>

<br>

<br>



<br>

\
<br>



<br>

<br>

\
<br>



<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>



<br>







