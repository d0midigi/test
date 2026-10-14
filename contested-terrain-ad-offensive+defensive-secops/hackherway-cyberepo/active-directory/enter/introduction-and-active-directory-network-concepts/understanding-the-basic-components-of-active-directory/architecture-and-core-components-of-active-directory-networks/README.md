# Architecture and Core Components of Active Directory Networks

### Active Directory Core Components Overview

Active Directory (AD) is the foundation of an enterprise-level Windows network, providing directory services that organize and manage user accounts, file servers, printers, applications, databases, and other shared resources in a logical, hierarchical fashion. This structure makes information accessible and manageable across the network.

AD was first introduced in Windows 2000 Server. Once installed on Windows 2000 Server or Windows Server 2003, the server becomes a domain controller (DC) responsible for authentication and management of user accounts and other objects.

In Microsoft networking, a domain is a network model where a domain controller acts as the _**Authentication Server (AS)**_, storing a security accounts database that holds users' network-wide account information and controlling access to network resources based on security groups.

### Active Directory Historical Origins: How AD Came To Be

The historical development of directory services began with products like Banyan's StreetTalk in 1984 and Novell's NetWare Directory Services (NDS) in 1993, evolving into hierarchical and object-oriented systems. Microsoft’s Windows NT Directory Services (NTDS) supported up to 25,000 users per domain, while Active Directory increased this to a theoretical 10 million objects per domain.

Active Directory and other directory services use standards such as X.500 and the _**Lightweight Directory Access Protocol (LDAP)**_ to provide interoperability between different systems.

LDAP is a lightweight and efficient protocol for directory access, designed for use over local networks and the Internet. _**Secure Sockets Layer (SSL)**_ and _**Transport Layer Security (TLS)**_ can be used to encrypt LDAP communications, providing data encryption and authentication.

## Architecture and Core Components of Active Directory Networks

A Microsoft Active Directory network consists of both _**logical**_ and _**physical structures**_.

### Logical Structure

The logical structure is defined by forests and domains, with _**domains**_ organized into domain trees where subdomains, known as child domains, can be created under parent domains in a branching structure. Domains serve as logical units that contain users, groups, computers, and _**Organizational Units (OUs)**_, which themselves can include users, groups, computers, and other OUs. _**Forests**_ are collections of domain trees that maintain trust relationships with each other, while each domain tree has its own separate namespace.

#### Organizational Units (OUs)

Organizational units are containers that allow storage of users, computers, groups, and other OUs. By placing objects in different OUs, the layout of Active Directory can mirror a company’s logical structure without creating separate domains. OUs are the smallest Active Directory unit to which administrative authority can be delegated, allowing specific users or groups to manage the users and resources within an OU.&#x20;

#### Active Directory Schema

The schema determines the types of objects and attributes that can exist within Active Directory, and modifications to the schema can only be made on the domain controller holding the _Schema Master_ role.

The _**Global Catalog (GC)**_ is a subset of directory data used for search and logon functionality across multiple domains. _**Directory partitions**_ include the domain partition, configuration partition, schema partition, and application partition, each storing specific types of data essential for network operations.

### Physical Structure

The physical structure of Active Directory is defined by sites, subnets, and domain controllers. Sites consist of one or more IP subnets connected by reliable links and are used to optimize replication and authentication processes by reducing traffic across slow, high-cost wide area network (WAN) links.

* _**Subnets**_ are associated with sites to help clients locate the nearest domain controller for authentication.
* _**Domain controllers**_ store writable copies of the directory and manage replication and authentication within the network.
* _**Flexible Single Master Operations (FSMO) roles**_ are specialized domain controller roles that maintain master copies of certain data, with five types of FSMO roles distributed across domains and forests.&#x20;

### Five Core FSMO Roles

The five core Active Directory FSMO (Flexible Single Master Operation) roles are: **Schema Master, Domain Naming Master (Forest-wide)**, and within each domain: **RID Master, PDC Emulator,** and **Infrastructure Master**, each handling critical, unique tasks like schema updates, domain creation, Security ID allocation, password syncing, and cross-domain object references, ensuring AD integrity.

### A. Forest-Wide Roles (One per Forest)

#### 1. Schema Master

Controls all updates to the Active Directory Schema (the blueprint for objects like users and computers) across the entire forest.

#### 2. Domain Naming Master

Manages adding, removing, and renaming domains and trusts within the AD forest.

### B. Domain-Level Roles (One per Domain)

#### 3. Relative ID (RID) Master

Allocates pools of unique Relative IDs (RIDs) to domain controllers, ensuring every security principal (user/group) gets a unique Security Identifier (SID).

#### 4. PDC Emulator

Acts as the master for password changes, time synchronization, and handles legacy NT compatibility, providing a fallback for authentication in case the preliminary fails.

#### 5. Infrastructure Master

Updates references from objects and its domain to objects (like group memberships) in other domains, ensuring consistency.

These components collectively enable secure communication, efficient replication, and robust authentication within Active Directory networks.
