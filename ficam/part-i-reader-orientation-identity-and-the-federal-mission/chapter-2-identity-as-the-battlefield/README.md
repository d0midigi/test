---
icon: person-military-to-person
---

# Chapter 2 - Identity as the Battlefield

#### Abstract

Enterprise cybersecurity was once commonly organized around a relatively intuitive security model: protect the network boundary, control what enters and leaves, harden the systems inside, and treat internal resources as more trustworthy than external ones. That model was never absolute, but it strongly influenced how networks, applications, authentication systems, and administrative controls were designed.

The modern enterprise is substantially more difficult to describe in those terms.

Users authenticate from outside traditional network boundaries. Applications consume identities from multiple directories and identity providers. Cloud services, mobile devices, mission partners, contractors, service accounts, workloads, certificates, federation systems, and automated processes all participate in access decisions. Administrative authority crosses infrastructure layers that are not necessarily contained within a single forest, network segment, or authorization boundary. In federal and Department of Defense environments, those relationships may extend across classified and unclassified networks, Public Key Infrastructure (PKI), Personal Identity Verification (PIV) and Common Access Card (CAC) credentials, cloud services, cross-domain solutions, federation, and mission-partner environments.

As those relationships expanded, identity evolved from an administrative support function into one of the principal mechanisms through which enterprise trust is established and exercised.

That change fundamentally altered the attack surface.

An adversary who compromises a workstation may control one system. An adversary who compromises trusted identity authority may gain the ability to authenticate as other principals, modify authorization, issue or obtain credentials, manipulate policy, traverse trust relationships, impersonate services, control administrative infrastructure, or establish persistence through mechanisms the enterprise is designed to trust.

This chapter establishes the conceptual foundation for the remainder of _Contested Terrain_. It traces the transition from network-oriented security assumptions toward identity-centric security, examines why Active Directory accumulated such significant administrative authority, distinguishes identity from the accounts that represent it, introduces attack-path and assume-breach reasoning, and establishes the offensive identity lifecycle that will later organize the book's adversarial operations.

The purpose is not to declare the network perimeter irrelevant.

It is to demonstrate why network location alone can no longer answer the most important security question in a modern enterprise:

Who—or what—is being trusted, and what authority does that trust create?

#### Keywords

identity security; Active Directory; identity perimeter; network perimeter; trust; authentication; authorization; attack path; assume breach; privilege; enterprise identity; Zero Trust; mission assurance; FICAM; DoD ICAM

#### Key Terms

**Identity boundary:** The logical boundary within which identity assertions, credentials, authentication mechanisms, attributes, and authorization decisions are accepted as sufficiently trustworthy to influence access.

**Network perimeter:** A security boundary established primarily through network architecture and controls separating internal, external, trusted, untrusted, or differently classified network environments.

**Trust relationship:** A defined relationship through which one system, identity domain, service, credential issuer, or security authority accepts some form of identity or authorization information originating from another.

**Identity attack surface:** The collection of identities, credentials, permissions, authentication mechanisms, trust relationships, attributes, services, administrative systems, and supporting infrastructure that can be targeted to influence access or authority.

**Effective authority:** The practical control a principal can exercise after considering direct permissions, inherited permissions, group membership, delegated control, trust relationships, credential access, and indirect control paths.

**Assume breach:** A security design and operational principle that treats compromise of some identities, devices, sessions, or network positions as a realistic condition and designs controls so that such compromise does not automatically result in unrestricted trust.

**Identity control plane:** The collection of authoritative systems and mechanisms through which identities are established, authenticated, authorized, administered, synchronized, privileged, federated, and revoked.

**Attack path:** A sequence of legitimate or unintended control relationships that allows an adversary to progress from an initial position toward greater authority or a strategically significant asset.
