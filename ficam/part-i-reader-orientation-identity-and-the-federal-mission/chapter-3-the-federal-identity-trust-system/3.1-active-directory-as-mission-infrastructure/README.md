# 3.1 Active Directory as Mission Infrastructure

Active Directory is sometimes described as enterprise plumbing: indispensable, largely invisible when functioning correctly, and noticed most often when something breaks.

That description understates its security role.

In an enterprise that depends heavily on Windows identity, Active Directory is not merely supporting mission systems. It participates in the conditions under which those systems can be used, administered, and trusted.

A user may require domain authentication before reaching an application. An administrator may require domain-group membership before managing a server. A workstation may depend upon the directory to establish its machine identity, locate services, process Group Policy, and authenticate users. A file server may use domain security principals to determine access. A network-access platform may query directory-backed identities. A certificate service may depend upon Active Directory objects and groups when deciding who may enroll for credentials. A cloud synchronization service may begin with the on-premises directory as a source for identities or attributes.

The directory therefore sits beneath many activities that appear to belong to other technical domains.

A storage outage is obviously a storage problem.

An application failure appears to be an application problem.

A remote-access problem appears to belong to networking.

Yet any of these services may become unavailable because the affected user cannot authenticate, a group relationship is wrong, a Domain Controller cannot be reached, a trust has failed, a certificate does not map correctly, or an account has been disabled upstream.

Identity infrastructure creates dependencies that are often invisible until they fail.

This is why treating Active Directory as merely an administrative convenience produces an incomplete risk model.
