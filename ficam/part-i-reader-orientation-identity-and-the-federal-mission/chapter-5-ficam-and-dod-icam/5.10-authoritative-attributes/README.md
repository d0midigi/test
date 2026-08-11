# 5.10 Authoritative Attributes

Identity systems do not make access decisions from identity alone.

They rely on facts about the identity.

A directory may know that a principal represents a particular person, but an application may also need to know the person's organization, employment or affiliation status, role, account type, sponsorship relationship, mission assignment, or another characteristic before determining what that principal should be allowed to do. Device and workload identities introduce equivalent requirements: ownership, management state, application role, environment, operational purpose, and other attributes may influence whether access should be permitted.

These facts are attributes.

The security question is not simply whether an attribute exists. It is whether the system consuming the attribute has a defensible reason to trust its value.

That distinction separates an attribute from an authoritative attribute.

Active Directory contains thousands of attributes, and administrators can create additional schema elements when necessary. The presence of data in the directory does not make the directory the authoritative source for that information. Active Directory may merely be storing a value that originated in a personnel system, identity-governance platform, device-management service, application registry, or another enterprise source.

This distinction becomes increasingly important as authorization moves away from simple membership models and begins incorporating richer identity context.

A traditional security group can express a fairly explicit relationship: members of this group receive a particular entitlement.

An attribute-driven policy may make that decision dynamically. If the user's organization equals one value, the person's role equals another, the device satisfies an approved state, and the application is being accessed under an appropriate context, access may be permitted.

The policy can be highly precise.

Its precision is meaningless if one of the underlying attributes can be manipulated by an untrusted principal.

Attribute-Based Access Control therefore creates a different form of privileged authority. The principal capable of changing an authorization-driving attribute may possess indirect control over the access decision even when that principal cannot modify the resource itself.

This is the same effective-authority principle encountered earlier in Active Directory permissions, applied to identity data.
