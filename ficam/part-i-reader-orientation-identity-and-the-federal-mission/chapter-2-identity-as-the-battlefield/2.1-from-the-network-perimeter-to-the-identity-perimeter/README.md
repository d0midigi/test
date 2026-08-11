# 2.1 From the Network Perimeter to the Identity Perimeter

The phrase _identity is the new perimeter_ has become common enough to lose some of its technical meaning.

Taken literally, it is also incomplete.

Identity did not replace the network perimeter. Networks still require segmentation. Firewalls still matter. Routing controls still determine reachability. Boundary-protection systems remain essential in federal environments. Classified networks remain physically or logically separated for reasons that identity controls alone cannot satisfy. Cross-domain solutions exist precisely because some boundaries must be enforced independently of ordinary authentication and authorization.

What changed is that network location stopped being a sufficiently reliable basis for trust.

In an earlier enterprise model, access frequently reflected physical or network proximity. A user on an internal workstation connected to an internal network was presumed to have crossed several security barriers before reaching a protected application. External access was comparatively exceptional. Administrative interfaces might be reachable only from trusted subnets. Applications often assumed that requests arriving from certain networks had already passed through meaningful security controls.

Those assumptions weakened as enterprise computing became more distributed.

Remote-access technologies allowed users to enter the enterprise from homes, hotels, temporary duty locations, contractor facilities, and mobile networks. Web applications became accessible without direct attachment to the internal network. Cloud computing placed applications and data outside traditional enterprise network boundaries. Federation allowed applications to trust authentication performed by separate identity providers. Software-as-a-Service platforms consumed organizational identity without residing anywhere near the organization's network perimeter.

At the same time, internal networks became increasingly difficult to treat as uniformly trusted environments. Malware, credential theft, compromised endpoints, insider threats, unmanaged devices, third-party access, and lateral movement demonstrated that being "inside" did not establish legitimacy.

The traditional distinction between inside and outside had not disappeared, but it was no longer sufficient.

A more important distinction emerged:

Which identity is requesting access, how was that identity established, how was it authenticated, what attributes are associated with it, what device or workload is presenting it, what authority does it possess, and what system is being asked to trust the resulting decision?

These are identity questions.

They can be evaluated regardless of whether the connection originated from an internal subnet, a remote-access gateway, a cloud network, or another trusted environment.

This is the foundation of the identity perimeter.

The perimeter is no longer represented solely by a physical boundary or firewall interface. It exists wherever an identity decision changes what a principal is permitted to do.

That means the perimeter may be encountered during logon, certificate authentication, federation, application authorization, privileged elevation, remote administration, cloud access, service-to-service authentication, or an automated workload requesting a resource.

Each of those events establishes or exercises trust.
