# CHAPTER 6.

# ENTERPRISE IDENTITY SERVICES: PKI, AD CS, AD FS, ENTRA ID, FEDERATION, AND HYBRID IDENTITY

## ABSTRACT

Active Directory does not authenticate identities alone. It operates at the center of a broader ecosystem of enterprise identity services that extend its trust outward — into certificate-based authentication, cross-boundary federation, cloud tenants, and hybrid environments where on-premises directories and cloud platforms must agree about who is who. This chapter examines that ecosystem at the component level: the Public Key Infrastructure that anchors cryptographic trust, Active Directory Certificate Services that implements it inside Windows environments, Active Directory Federation Services that brokers cross-boundary assertions, Microsoft Entra ID that hosts cloud-native identities and roles, and the hybrid synchronization fabric that connects on-premises Active Directory to cloud services. Each service is examined for what it does, how it is structured, and where its security significance concentrates — because every component described here will reappear in Part II as an attack surface and in Part III as a hardening target. The chapter situates each service within federal Federal Identity, Credential, and Access Management (FICAM) and Department of Defense Identity, Credential, and Access Management (DoD ICAM) environments, where these services carry assurance, interoperability, and mission obligations that commercial deployments do not. Certificate templates, federation trust configurations, synchronization accounts, and cloud roles that would be low-priority misconfigurations in a commercial enterprise represent Tier 0 exposure in a federal identity trust system.

## KEYWORDS

Public Key Infrastructure; Active Directory Certificate Services; Certificate templates; Active Directory Federation Services; Microsoft Entra ID; Hybrid identity; Federation; Synchronization; X.509; Golden SAML

## KEY TERMS

* **Public Key Infrastructure (PKI):** The ecosystem of certificate authorities, certificates, trust anchors, revocation mechanisms, and policies that enable cryptographic identity verification across distributed systems.
* **Certificate Authority (CA):** An entity that issues, signs, and revokes digital certificates, binding a cryptographic public key to an identity claim. CAs form a hierarchy of trust.
* **X.509:** The International Telecommunication Union (ITU) standard defining the format of public-key certificates used in PKI. X.509 version 3 (v3) introduced certificate extensions that carry additional attributes beyond the core identity binding.
* **Active Directory Certificate Services (AD CS):** The Microsoft Windows Server role that implements PKI within an Active Directory environment, providing certificate issuance, revocation, and enrollment services.
* **Certificate template:** An Active Directory object that defines the policy governing a class of certificates — what keys they use, what purposes they serve, who may enroll, and what identity information they carry.
* **Active Directory Federation Services (AD FS):** A Microsoft Windows Server role that provides Security Token Service (STS) functionality, enabling claims-based authentication and federated identity across organizational boundaries.
* **Claims-based authentication:** An authentication model in which identity assertions are carried as structured attribute-value pairs — claims — inside a cryptographically signed security token rather than through a direct password verification.
* **Microsoft Entra ID:** Microsoft's cloud-based identity platform, formerly known as Azure Active Directory (Azure AD), providing cloud-native identity, authentication, authorization, and access management.
* **Hybrid identity:** An architecture in which on-premises Active Directory and Microsoft Entra ID are connected through synchronization or federation, allowing a single identity to be used across both environments.
* **Microsoft Entra Connect:** The synchronization tool that bridges on-premises Active Directory with Microsoft Entra ID, controlling which objects, attributes, and credentials are replicated to the cloud.
* **Service Principal:** An identity in Microsoft Entra ID that represents an application, service, or automated workload — the non-human equivalent of a user account in cloud environments.
* **Managed Identity:** A Microsoft Entra ID feature that provides an automatically managed service identity for Azure resources, eliminating the need to store credentials in code or configuration.

\---

## 6.1 THE IDENTITY SERVICES LAYER

The previous chapter traced authentication mechanics at the protocol level — how Kerberos and NTLM prove identity across the wire. This chapter moves up one abstraction layer to the services that issue, validate, extend, and federate the credentials those protocols consume. A certificate that enables smart-card authentication exists because a Certificate Authority (CA) issued it according to a template defined in Active Directory Certificate Services (AD CS). A user who accesses a cloud application without re-entering credentials does so because Active Directory Federation Services (AD FS) or Microsoft Entra ID brokered a federation assertion. An identity that exists in both an on-premises domain and a cloud tenant does so because Microsoft Entra Connect synchronized it across that boundary.

These are not peripheral services. They are the infrastructure through which trust is manufactured, extended, and ultimately delegated — and in a federal or military FICAM/DoD ICAM environment, they are the infrastructure through which mission-critical assurance requirements are supposed to be enforced. When they are correctly configured, they carry assurance upward through the identity system. When they are misconfigured, they become the paths through which adversaries manufacture trust for themselves. Understanding each service begins by understanding what it is designed to do, because the attack techniques examined in Part II are, in every case, a consequence of the service working exactly as designed but with the wrong inputs.

\---

## 6.2 PUBLIC KEY INFRASTRUCTURE: THE FOUNDATION OF CRYPTOGRAPHIC TRUST

Public Key Infrastructure (PKI) is not a single product or service — it is an ecosystem. At its core, PKI solves a problem that is fundamental to distributed security: how do two parties who have never met establish trust in each other's identity without a shared secret? The answer is a certificate: a digitally signed document that binds a cryptographic public key to an identity claim, vouched for by a CA that both parties agree to trust.

### 6.2.1 HOW ASYMMETRIC CRYPTOGRAPHY UNDERLIES PKI

PKI rests on asymmetric cryptography, also called public-key cryptography. In an asymmetric key pair, there is a mathematically related public key and private key. What the public key encrypts, only the private key can decrypt. What the private key signs, the public key can verify. The critical property is that knowledge of the public key reveals nothing useful about the private key.

In PKI, an entity generates a key pair and keeps the private key secret. The public key is submitted to a CA in a certificate signing request (CSR). The CA verifies the identity claim associated with that public key — through whatever proofing mechanism the CA policy requires — and issues a certificate binding the verified identity to the public key. The certificate is signed with the CA's own private key. Any party that trusts the CA can verify the signature using the CA's public key, confirming that the certificate was genuinely issued by that CA and has not been modified.

The private key, which the CA never sees, is what makes the certificate useful for authentication. An entity that holds the private key can prove identity to any relying party that trusts the issuing CA — without the relying party ever possessing a shared secret, and without the private key ever crossing the network.

### 6.2.2 CERTIFICATE AUTHORITY HIERARCHIES AND CHAINS OF TRUST

Certificate Authorities are organized into hierarchies. At the top is a Root CA — a CA that signs its own certificate (called a self-signed certificate) and is trusted by relying parties as a trust anchor. Below the Root CA are one or more Subordinate CAs, also called Intermediate CAs or Issuing CAs, whose certificates are signed by the Root CA or by another Subordinate CA. Leaf certificates — the certificates issued to end entities such as users, computers, and services — are issued by Issuing CAs.

This hierarchy exists for security and operational reasons. The Root CA private key is the ultimate trust anchor. If it is compromised, all certificates in the hierarchy must be considered untrustworthy. To protect it, Root CAs are typically kept offline — physically secured, powered down, and brought online only to issue or renew subordinate CA certificates. Day-to-day certificate operations are handled by online Issuing CAs, whose compromise is serious but recoverable: the Issuing CA can be revoked from the Root CA's perspective, new issuing capacity deployed, and the damage contained.

When a relying party receives a certificate, it validates the chain: the certificate was signed by the Issuing CA, the Issuing CA certificate was signed by the Root CA, and the Root CA certificate is in the relying party's trust store. A break anywhere in that chain — an expired certificate, a revoked CA, an untrusted root — causes the validation to fail.

In federal environments, the Federal Public Key Infrastructure (FPKI) extends this model across agencies. The Federal Common Policy Certificate Authority (FCPCA) serves as the federal trust anchor, and agency CAs chain up to it. When a Personal Identity Verification (PIV) card is used to authenticate, the certificate on the card must chain to a CA trusted by the verifying system — and in federal environments, that chain ultimately runs through the FPKI.

### 6.2.3 THE X.509 v3 CERTIFICATE STRUCTURE

Every certificate used in PKI follows the X.509 v3 format. Understanding the structure of a certificate is prerequisite to understanding how certificates are used, how they can be abused, and how to evaluate whether a certificate template is safe.

A certificate contains: the version (always 3 for modern certificates); a unique serial number assigned by the issuing CA; the signature algorithm used to sign the certificate; the issuer — the distinguished name (DN) of the CA that signed it; the validity period — not-before and not-after timestamps; the subject — the distinguished name of the entity the certificate was issued to; the subject public key information — the public key and the algorithm it uses; and a set of extensions.

The extensions are where most of the security-relevant information lives in a modern certificate. The most important for Active Directory and FICAM contexts are:

**Subject Alternative Name (SAN):** Specifies additional identity values beyond the subject distinguished name. For user authentication certificates, this commonly includes the User Principal Name (UPN). In certain Active Directory configurations, the SAN is what determines which account a certificate maps to — a fact exploited by several AD CS attack paths.

**Extended Key Usage (EKU):** Specifies what purposes the certificate is valid for. Common EKU values include Client Authentication (OID 1.3.6.1.5.5.7.3.2), which allows the certificate to authenticate a user or computer to a service; Smart Card Logon (OID 1.3.6.1.4.1.311.20.2.2); and Certificate Request Agent (OID 1.3.6.1.4.1.311.20.2.1), which allows the holder to request certificates on behalf of other principals. The EKU field is critical: a certificate with an overly permissive EKU — or certain combinations of EKUs — can be used for purposes far beyond what was intended.

**Key Usage:** Specifies the cryptographic operations the key pair may be used for: Digital Signature, Key Encipherment, Certificate Signing, CRL Signing. Restricting key usage to intended purposes limits the damage from certificate theft.

**Certificate Policies:** Identifies the policy under which the certificate was issued, including policy Object Identifiers (OIDs) that map to assurance levels. In federal environments, specific policy OIDs indicate whether a certificate meets PIV-I, PIV, or other federal assurance requirements.

**Authority Information Access (AIA):** Contains URLs for the issuing CA certificate and for the Online Certificate Status Protocol (OCSP) responder, enabling relying parties to build the certificate chain and check revocation status.

**CRL Distribution Points (CDP):** Contains URLs for the Certificate Revocation List (CRL) published by the issuing CA.

### 6.2.4 CERTIFICATE LIFECYCLE: ISSUANCE, VALIDATION, AND REVOCATION

A certificate does not exist in isolation — it moves through a lifecycle that has security implications at every stage.

**Issuance** begins with enrollment. An entity generates a key pair and submits a certificate signing request to the CA, identifying itself and specifying what kind of certificate it needs. The CA validates the request against its policy — checking that the requester is authorized to receive that type of certificate, that the identity information is correct, and that the request conforms to the applicable template or profile. If validation passes, the CA signs the certificate and delivers it to the requester. In Active Directory environments, this process is often automated through auto-enrollment, which reduces manual overhead but also reduces the human review that might catch a misconfigured request.

**Validation** occurs every time a relying party evaluates a certificate presented for authentication. The relying party checks that the certificate has not expired, that the issuing CA is trusted, that the chain of signatures is intact from the leaf certificate to the trust anchor, and that the certificate has not been revoked. Each of these checks can fail in ways that have security consequences — a check that is skipped or that fails silently is a path through which an invalid certificate can be accepted.

**Revocation** is the mechanism by which a certificate is declared untrustworthy before its natural expiry. This is necessary when a private key is compromised, when an account is deprovisioned, or when a certificate was issued in error. There are two primary revocation mechanisms: Certificate Revocation Lists (CRLs) and Online Certificate Status Protocol (OCSP).

### 6.2.5 REVOCATION MECHANISMS: CRL AND OCSP

A Certificate Revocation List (CRL) is a signed list published by a CA containing the serial numbers of revoked certificates. Relying parties download the CRL and check whether a presented certificate's serial number appears on it. CRLs have a publication interval — they are published periodically, not in real time. A certificate revoked at 9:00 AM may not appear in the next CRL until several hours later, creating a window during which the revoked certificate remains valid from a relying party's perspective. CRL files also grow over time as revoked certificates accumulate.

The Online Certificate Status Protocol (OCSP) provides a real-time alternative to CRL checking. A relying party sends a query to an OCSP responder — a service hosted by or on behalf of the CA — asking whether a specific certificate is currently valid. The responder replies with a signed status of "good," "revoked," or "unknown." OCSP responses are near-real-time and do not require downloading large lists, but they introduce a dependency on the availability of the OCSP service and create a record at the OCSP responder of which certificates are being checked.

The security significance of revocation becomes concrete when an attacker compromises a private key. If revocation is not processed quickly, or if relying parties are configured to ignore revocation failures (a "soft-fail" configuration common in environments that trade security for availability), a compromised certificate may remain usable long after the theft is discovered.

\---

## 6.3 ACTIVE DIRECTORY CERTIFICATE SERVICES (AD CS)

Active Directory Certificate Services is the Microsoft Windows Server role that implements PKI within an Active Directory forest. AD CS provides CA functionality, certificate template management, enrollment services, revocation publishing, and the integration between certificates and Active Directory identities. In virtually every Active Directory environment of any size, AD CS is present — issuing certificates for smart card authentication, encrypted email, code signing, web server TLS, and dozens of other purposes.

AD CS deserves more security attention than it typically receives. In a federal environment, it is not merely a supporting service. An AD CS enterprise CA whose certificate can be used for client authentication against domain controllers is Tier 0 infrastructure, because a certificate issued by that CA can be used to authenticate as any domain account — including domain administrators — if the template and enrollment permissions are misconfigured. The security community's growing understanding of AD CS attack paths (broadly known as the ESC vulnerabilities, named by researchers Will Schroeder and Lee Christensen in their 2021 research "Certified Pre-Owned") has significantly elevated AD CS from an overlooked supporting role to a primary hardening target.

### 6.3.1 ENTERPRISE CA VERSUS STANDALONE CA

AD CS supports two CA types with fundamentally different security models.

An **Enterprise CA** is integrated with Active Directory. It stores certificate templates in the directory, uses Active Directory for authorization (determining who may enroll for which certificate types), and automatically publishes issued certificates to enrolling users' Active Directory objects. Enterprise CAs support auto-enrollment, which allows domain computers and users to automatically receive appropriate certificates without manual intervention. Because Enterprise CAs query Active Directory for authorization decisions, a compromise of the CA's private key — or a misconfiguration in a template's enrollment permissions — can have domain-wide consequences.

A **Standalone CA** operates independently of Active Directory. It does not use AD for authorization, does not publish to AD, and does not support auto-enrollment. All certificate operations require manual administrator approval. Standalone CAs are commonly used for Root CAs that are kept offline, precisely because their disconnection from AD means they cannot be reached through the same attack paths that threaten Enterprise CAs.

The typical secure architecture uses a Standalone offline Root CA to issue certificates to one or more online Issuing CAs configured as Enterprise CAs. The Root CA is powered off and locked away; the Enterprise Issuing CAs handle day-to-day operations. If an Issuing CA is compromised, its certificate can be revoked by the Root CA, limiting the blast radius.

### 6.3.2 CERTIFICATE TEMPLATES: THE POLICY CONFIGURATION INTERFACE

Certificate templates are the central policy mechanism in AD CS. A certificate template is an Active Directory object stored in the configuration naming context, under `CN=Certificate Templates,CN=Public Key Services,CN=Services,CN=Configuration,DC=<domain>`. Each template defines a policy governing a class of certificates: what cryptographic algorithm and key length to use, what Extended Key Usages to include, how long the certificate is valid, whether the subject name is provided by the requester or derived from Active Directory, who may enroll, whether manager approval is required, and dozens of additional attributes.

The following template attributes carry the most security significance:

**`msPKI-Certificate-Name-Flag`:** Controls how the subject name is constructed. The flag `CT\\\\\\\_FLAG\\\\\\\_ENROLLEE\\\\\\\_SUPPLIES\\\\\\\_SUBJECT` (value 1) allows the enrolling user to specify the subject name in the certificate signing request rather than having AD CS derive it from the Active Directory account. When this flag is set alongside client authentication EKU and permissive enrollment rights, any user with enrollment access can request a certificate claiming to be any identity — including domain administrators. This is the configuration that enables ESC1, the most straightforward AD CS privilege escalation path.

**`msPKI-Enrollment-Flag`:** Controls enrollment behavior. The flag `CT\\\\\\\_FLAG\\\\\\\_PEND\\\\\\\_ALL\\\\\\\_REQUESTS` (value 2) requires manager approval before a certificate is issued; its absence means certificates are issued automatically upon a valid enrollment request. The flag `CT\\\\\\\_FLAG\\\\\\\_NO\\\\\\\_SECURITY\\\\\\\_EXTENSION` (value 0x80000) disables embedding the security extension that ties the certificate to the enrolling account's Security Identifier (SID) — relevant to newer exploitation paths.

**`msPKI-Private-Key-Flag`:** Controls private key handling. Certain flag values enable key archival (the CA keeps a copy of the private key) and specify whether the private key is exportable. Exportable private keys create recovery options but also mean that a user or attacker who obtains the certificate can export the private key for use elsewhere.

**Security Descriptor on the template:** Determines which principals have Enroll permission (the right to request a certificate from this template) and Full Control or Write permissions (which allow modification of the template itself). Misconfigured enrollment permissions — particularly granting Domain Users or Authenticated Users the Enroll right — are the prerequisite for many AD CS attacks.

**Extended Key Usage (EKU) on the template:** Templates intended for user authentication must have appropriate EKUs. A template that enables Certificate Request Agent EKU allows the certificate holder to request certificates on behalf of other accounts, which - when combined with permissive enrollment rights - enables enrollment-on-behalf-of attacks.

In my experience assessing federal environments, the most common AD CS finding is not a complex misconfigurations but a simple one: a template created years ago for a specific purpose that still has Authenticated Users in the enrollment rights. Nobody remembered it existed. The CA kept issuing against it. The template's EKU and subject name flags made it E, and nobody had looked.

### 6.3.3 CERTIFICATE ENROLLMENT AND AUTO-ENROLLMENT

Certificate enrollment is the process by which an entity requests and receives a certificate from a CA. AD CS supports several enrollment mechanisms:

**Manual enrollment** requires an administrator or user to explicitly request a certificate through the Certificates Microsoft Management Console (MMC) snap-in, the CertReq command-line tool, or the CA web enrollment interface.

**Auto-enrollment** is driven by Group Policy and allows domain computers and users to automatically receive certificates defined in their applicable templates without any user action. Group Policy Object (GPO) settings in Computer Configuration or User Configuration → Windows Settings → Security Settings → Public Key Policies → Certificate Services Client define which templates apply to which principals. When auto-enrollment is configured, clients periodically contact the CA to check whether they are entitled to new or renewed certificates. This is operationally convenient and a significant source of certificate sprawl - templates that were deployed via auto-enrollment years ago may be issuing certificates into the environment with no active awareness.

**Web enrollment** allows certificate requests via an Internet Information Services (IIS)-hosted interface. This is often the path through which cross-platform clients that cannot use native Windows enrollment mechanisms obtain certificates. The web enrollment interface has historically been targeted by authentication relay attacks because it accepts NTLM authentication and, in default configurations, does not enforce Extended Protection for Authentication.

**Network Device Enrollment Service (NDES)** implements the Simple Certificate Enrollment Protocol (SCEP), enabling network devices such as routers, firewalls, and mobile devices to enroll for certificates. NDES runs as an IIS application and uses a registration authority model; its security configuration - particularly the NDES service account's permissions and the challenge password handling - has been a source of attack paths.

### 6.3.4 CERTIFICATE-TO-IDENTITY MAPPING: PKINIT AND ALTSECURITYIDENTITIES

For a certificate to authenticate a domain account, the verifying system must be able to map from the certificate to the Active Directory principal it represents. Active Directory provides two primary mapping mechanisms.

**PKINIT (Public Key Cryptography for Initial Authentication in Kerberos):** PKINIT is the Kerberos extension, defined in RFC 4556, that allows a client to authenticate to the Key Distribution Center (KDC) using a certificate rather than a password. Instead of the normal AS-REQ pre-authentication (an encrypted timestamp), the client sends its certificate and a signature proving possession of the corresponding private key. The KDC validates the certificate, maps it to an Active Directory account, and — if validation succeeds — issues a Ticket Granting Ticket (TGT) for that account. PKINIT is the mechanism through which PIV and Common Access Card (CAC) smart-card authentication operates in Active Directory environments.

The mapping from certificate to account during PKINIT can occur through several methods. The default method in modern Windows environments (post-May 2022 security updates) is the new strong mapping, which embeds the account's Security Identifier (SID) in the certificate's Subject Alternative Name (SAN) using a specific OID. Prior to this update, the weak mapping relied on the UPN in the SAN matching an account's userPrincipalName attribute — a mapping that could be abused if the UPN could be manipulated.

**The `altSecurityIdentities` attribute:** This Active Directory user attribute allows administrators to manually specify certificate identifiers that should map to an account. Values can include the certificate's issuer and serial number (`X509:<I>issuer DN<SR>serial`), the subject key identifier, or the UPN value from the SAN. This attribute is used for PIV/CAC mappings in federal environments and also for certificates from non-Windows CAs. Any principal with write access to another account's `altSecurityIdentities` attribute can map a certificate they control to that account - a privilege escalation path when the permission is misconfigured.

### 6.3.5 AD CS AS TIER 0 INFRASTRUCTURE

The classification of Active Directory  Certificate Services (AD CS) as Tier 0 infrastructure is not a matter of convention - it is a consequence of what a compromised AD CS CA can do. An Enterprise CA that is trusted for domain authentication can issue certificates that authenticate as any account in the forest, including Domain Admins and `krbtgt`. An attacker who achieves compromise of an Enterprise CA's private key does not need to attack domain controllers, steal credentials, or forge Kerberos tickets. They can simply issue themselves a certificate mapping to any account they choose, use PKINIT to obtain a TGT for that account, and proceed from there.

This means the CA server, the CA private key, the certificate template permissions, and the enrollment endpoints are all Tier 0 components - they must be governed, monitored, and protected with the same rigor as domain controllers. In practice, many environments treat the CA server as a normal member server. The consequences of that misclassification surface in Part II.

\---

## 6.4 ACTIVE DIRECTORY FEDERATION SERVICES (AD FS)

Active Directory Federation Services is a Windows Server role that implements a Security Token Service (STS) - a service that accepts authentication from one identity context and issues a security token asserting that identity to a different context. AD FS enables an organization to be an Identity Provider (IdP), issuing tokens that relying-party applications trust without requiring users to authenticate separately to each application. It also enables an organization to consume tokens from external IdPs, trusting identities that were authenticated by another organization's systems.

Federation is what makes Single Sign-On (SSO) possible across organizational boundaries. In federal environments, federation enables mission partners, contractors, and coalition members to access resources with their own credentials - without requiring those identities to exist in the resource-owning organization's directory. It is also what enables hybrid identity scenarios where a user authenticates on-premises but accesses cloud services without re-authentication.

### 6.4.1 CLAIMS-BASED AUTHENTICATION

AD FS operates on a claims-based authentication model. When a user authenticates to AD FS, the service does not simply issue a pass/fail verdict - it issues a security token containing a set of claims about the authenticated user. A claim is a structured assertion: a name-value pair stating something about the identity. Claims commonly include the user's name, email address, group memberships, department, assurance level, and any custom attributes relevant to the relying party's access control decisions.

The claims a user receives are determined by AD FS claim rules - a policy language that defines how Active Directory attributes are transformed into token claims, how claims from an external IdP are passed through or filtered, and what conditions must be met before a token is issued. The flexibility of claim rules is AD FS's primary value as a federation broker and also one of its primary complexity sources: claim rules can become difficult to audit, especially in long-running environments where rules accumulate without regular review.

### 6.4.2 FEDERATION PROTOCOLS: SAML, WS-FEDERATION, OAUTH, AND OIDC

AD FS supports multiple federation protocols, each suited to different application types.

**Security Assertion Markup Language 2.0 (SAML 2.0):** The dominant federation protocol for enterprise web applications. A SAML assertion is an XML document containing the identity claims, signed with the IdP's private key. The relying party validates the signature using the IdP's public key (the token-signing certificate) and extracts the claims. SAML is the protocol underlying Golden SAML attacks, in which an attacker who possesses the token-signing private key can create arbitrary assertions without authenticating through AD FS at all.

**WS-Federation:** An older Microsoft-centric federation protocol used heavily by SharePoint, Exchange, and other Microsoft applications. WS-Federation tokens are XML-based like SAML but follow a different structure. Both protocols are supported by AD FS for backward compatibility.

**OAuth 2.0:** An authorization framework that issues access tokens enabling a client to access resources on behalf of a user without exposing the user's credentials. OAuth does not itself define how authentication is performed — it defines how authorization is delegated. AD FS implements an OAuth authorization server that issues access tokens for registered applications.

**OpenID Connect (OIDC):** An identity layer built on top of OAuth 2.0 that adds an ID token - a signed JSON Web Token (JWT) - carrying authenticated user information. OIDC has become the dominant protocol for modern web and mobile application authentication, and it is the primary protocol used by Microsoft Entra ID.

### 6.4.3 AD FS ARCHITECTURE

A production AD FS deployment consists of several components. The AD FS server (or farm, for high availability) hosts the STS service, stores configuration in a SQL Server database or Windows Internal Database (WID), and communicates with Active Directory to authenticate users and retrieve attribute information. The Web Application Proxy (WAP) is an optional component deployed in a perimeter network that pre-authenticates incoming requests before they reach the AD FS server, reducing the attack surface exposed to the internet.

AD FS stores its configuration data - including the token-signing certificate's private key - in encrypted form. The encryption key is managed through the Distributed Key Manager (DKM), which stores the actual decryption key in an Active Directory container: `CN=ADFS,CN=Microsoft,CN=Program Data,DC=<domain>`. Any principal with read access to this container can retrieve the DKM key and use it to decrypt the AD FS configuration database, extracting the token-signing certificate's private key. This access path is one of the primary targets in AD FS compromise scenarios.

Relying parties are registered with AD FS through Relying Party Trusts, which define the applications AD FS will issue tokens for, what claims they receive, and what protocol they use. AD FS also maintains Claim Provider Trusts for external IdPs whose tokens AD FS will accept - the inbound federation configuration.

### 6.4.4 THE TOKEN-SIGNING CERTIFICATE

The token-signing certificate is the single most sensitive asset in an AD FS deployment. Its private key is what AD FS uses to sign every assertion it issues. Any SAML or WS-Federation token bearing a valid signature from this certificate will be trusted by every relying party in the federation — regardless of what claims the token contains, regardless of whether the user actually authenticated, and regardless of what access controls those claims would normally be subject to.

AD FS generates a self-signed token-signing certificate by default and renews it automatically. The certificate is also published in the federation metadata at the endpoint `https://<adfs-hostname>/federationmetadata/2007-06/federationmetadata.xml`, which relying parties use to automatically update their trust when the certificate rolls over. This automatic rollover is operationally convenient but means that a token-signing certificate rotation does not immediately invalidate signatures from the old certificate - relying parties may continue trusting both old and new certificates through the rollover window.

When an attacker extracts the token-signing private key, they hold the ability to issue valid assertions for any identity, to any relying party, indefinitely - or at least until the certificate is explicitly revoked and relying parties are updated. This is the fundamental persistence of Golden SAML: it survives password resets, account lockouts, Multi-Factor Authentication (MFA) configuration changes, and Conditional Access policy updates, because none of those controls are evaluated when the assertion is a pre-signed forgery. The only effective remediation requires rotating the token-signing certificate and confirming that every relying party has updated its trust metadata.

\---

## 6.5 MICROSOFT ENTRA ID

Microsoft Entra ID (formerly known as Azure Active Directory, or Azure AD) is Microsoft's cloud-native identity platform. Where on-premises Active Directory is built around Kerberos, Lightweight Directory Access Protocol (LDAP), and domain membership, Entra ID is built around modern web protocols - OAuth 2.0, OpenID Connect, and Security Assertion Markup Language 2.0 - and designed for internet-scale access management across tenants, organizations, and geographic boundaries.

Entra ID is not a cloud version of Active Directory. The two share a name and a synchronization relationship, but they are architecturally distinct. Active Directory uses a hierarchical forest-and-domain model with Kerberos-based authentication and LDAP-based directory access. Entra ID uses a flat tenant model, authenticates via OAuth/OIDC, and provides directory access through the Microsoft Graph API. Understanding these differences matters because attacks and defenses that apply to one do not necessarily apply to the other.

### 6.5.1 TENANT ARCHITECTURE

An Entra ID tenant is the top-level organizational boundary in the Microsoft cloud - a dedicated instance of the Entra ID service hosting all identities, applications, and configurations for a given organization. Tenants are identified by a tenant ID (a Globally Unique Identifier, or GUID) and one or more domain names verified through DNS. Every Microsoft cloud service - Microsoft 365, Azure, Dynamics 365 - is associated with an Entra ID tenant that provides its identity and access management.

Within a tenant, identities are organized as users and groups, similar in concept to on-premises Active Directory but without the forest-and-domain hierarchy. Access to resources is controlled through role assignments, application registrations, and Conditional Access policies rather than through Group Policy and Kerberos tickets.

### 6.5.2 SERVICE PRINCIPALS, APP REGISTRATIONS, AND MANAGED IDENTITIES

In Entra ID, applications and services are represented by distinct identity objects rather than by user accounts.

An **App Registration** is the definition of an application's identity in Entra ID - its name, the permissions it needs, and its authentication configuration. When an application is registered, Entra ID creates a corresponding Service Principal in the tenant.

A **Service Principal** is the runtime identity of an application within a specific tenant. If an App Registration represents the template, the Service Principal represents the instantiation of that template in a given organizational context. Service Principals can be assigned roles, granted API permissions, and used to authenticate as the application to Entra ID-protected resources. Service Principals are the Entra ID equivalent of service accounts - and like on-premises service accounts, they are frequently over-privileged, under-monitored, and left in place long after the application they support has changed or been decommissioned.

A **Managed Identity** is a special type of Service Principal whose credentials are managed entirely by Microsoft Azure. The application or resource never holds or manages a credential - it requests tokens from Entra ID using its managed identity, and Azure handles the key material behind the scenes. There are two types: System-assigned managed identities are tied to a specific Azure resource and share its lifecycle (they are deleted when the resource is deleted); User-assigned managed identities are independent resources that can be associated with multiple Azure resources. Managed identities solve the credential-storage problem but can still be over-privileged - a managed identity with excessive Azure role assignments represents a horizontal attack path if the resource it belongs to is compromised.

### 6.5.3 CONDITIONAL ACCESS AND RISK-BASED AUTHENTICATION

Conditional Access is the Entra ID mechanism for enforcing access control policies that depend on context rather than identity alone. A Conditional Access policy evaluates conditions - user identity, group membership, device compliance state, application being accessed, network location, and sign-in risk signals - and enforces controls such as requiring MFA, blocking access, requiring a compliant device, or restricting access to managed locations.

Conditional Access is the closest Entra ID equivalent of a firewall for identity: it is the point where authentication context meets authorization policy. The security significance is bilateral. Correctly configured Conditional Access policies close a wide range of attack paths - requiring phishing-resistant MFA for privileged roles, blocking legacy authentication protocols that do not support modern authentication, requiring managed-device access for sensitive applications. Incorrectly configured or missing Conditional Access policies are the gaps through which cloud identity attacks commonly succeed.

Legacy authentication protocols - older email clients, on-premises synchronization connectors, applications using basic authentication - bypass Conditional Access because they cannot participate in the OAuth 2.0 flow that Conditional Access evaluates. Blocking legacy authentication through Conditional Access is one of the highest-value single security improvements available to an Entra ID tenant, and one of the most consistently missing controls in environments assessed before they experience an incident.

### 6.5.4 PRIVILEGED IDENTITY MANAGEMENT (PIM)

Privileged Identity Management (PIM) is an Entra ID feature that implements just-in-time (JIT) privileged access for Entra ID roles. Rather than assigning a user permanent membership in a privileged role such as Global Administrator, PIM makes them eligible for the role - they can activate it on demand for a defined duration, optionally after providing a justification and completing MFA, and the activation is logged. At the end of the activation window, the role assignment expires automatically.

PIM reduces the standing attack surface of privileged cloud roles. A Global Administrator account that is only activated when needed is not useful to an attacker who compromises the account at an idle moment. PIM also provides the audit trail - who activated which role, when, for how long, with what justification - that FICAM's access governance requirements expect to see.

The limitation worth stating plainly: PIM protects Entra ID role assignments. It does not protect Azure Resource Role Based Access Control (RBAC) assignments in the same way by default, though Azure PIM can be extended to Azure resources. It also does not protect application-level permissions granted to Service Principals. An account that holds a Global Administrator role under PIM may still have Service Principals with high-privilege permissions that are permanently active, and those Service Principals are the attack path that PIM did not harden.

\---

## 6.6 HYBRID IDENTITY: THE BRIDGE BETWEEN ON-PREMISES AND CLOUD

Most organizations of any size operate in a hybrid identity model: they have an on-premises Active Directory that existed before cloud services, and they have adopted Microsoft 365, Azure, or other cloud platforms that require Entra ID identities. Hybrid identity is the architecture that connects these two worlds so that a user can authenticate on-premises and access cloud resources without separate cloud credentials.

The bridge between on-premises Active Directory and Entra ID is provided by Microsoft Entra Connect (formerly known as Azure AD Connect). Entra Connect is a software component installed on an on-premises Windows Server. It synchronizes selected objects and attributes from on-premises Active Directory to Entra ID on a scheduled basis, creating and maintaining corresponding identities in both environments.

### 6.6.1 MICROSOFT ENTRA CONNECT ARCHITECTURE

Entra Connect runs as a service on a dedicated on-premises server and connects to both on-premises Active Directory (as an Active Directory user with specific permissions to read the directory) and Entra ID (as a high-privilege cloud account with Hybrid Identity Administrator and Global Administrator rights during setup). After initial synchronization, the ongoing connection uses a service account with Directory Synchronization Account rights.

The on-premises service account used by Entra Connect (historically prefixed with `MSOL\\\\\\\_` or `AAD\\\\\\\_`, depending on the version and configuration) requires specific permissions in on-premises Active Directory: replication rights on the domain, read access to user and group attributes, and write access for certain writeback features. These permissions are substantial - replication rights on the domain are sufficient to perform a DCSync attack, extracting all password hashes from the domain.

This creates a significant and frequently overlooked security risk. The Entra Connect service account is a high-privilege Active Directory account that exists in virtually every hybrid environment, often in the default Users container, with no monitoring specific to its activities. An attacker who compromises this account - through credential theft, lateral movement, or any other means - holds the keys to execute DCSync without needing Domain Admin rights.

### 6.6.2 SYNCHRONIZATION MODELS: PHS, PTA, AND FEDERATED

Entra Connect supports three models for how authentication is handled across the hybrid boundary.

**Password Hash Synchronization (PHS):** The most common configuration. Entra Connect computes a derivative of the on-premises NT hash - specifically, an MD5 hash of the UTF-16LE encoded password, salted with a random value, iterated 1,000 times using Password-Based Key Derivation Function 2 (PBKDF2) - and synchronizes it to Entra ID. When a user authenticates to a cloud service, Entra ID validates the credential against this synchronized hash directly, without contacting the on-premises environment. PHS enables cloud sign-in even when on-premises infrastructure is unavailable, and it also enables leaked credential detection - Microsoft's Identity Protection service can detect when synchronized password hashes appear in breach datasets.

The security nuance: the synchronized hash is not the raw NT hash. It is a transformed, salted, iterated derivative that cannot be used for on-premises Pass-the-Hash attacks; however, if an attacker compromises Entra ID's internal credential stores (which is a Microsoft-side concern, not a customer-side one in standard configurations), they would hold these cloud-side derivatives, not the original NT hashes.

**Pass-through Authentication (PTA):** Authentication requests are forwarded to an on-premises agent - the Pass-through Authentication Agent - which validates the credential against on-premises Active Directory and returns the result. The password never leaves the on-premises environment. PTA requires the PTA Agent to be available for authentication to succeed, which means on-premises infrastructure availability affects cloud sign-in.

**Federated Authentication:** Authentication is delegated to an on-premises federation service - typically AD FS - which issues tokens that Entra ID trusts. This model provides the most control over the authentication experience and enables use of on-premises smart-card authentication for cloud services, but it is architecturally complex and shifts the trust anchor to the federation service's token-signing certificate.

### 6.6.3 WRITEBACK FEATURES AND THEIR SECURITY IMPLICATIONS

Entra Connect includes optional writeback features that synchronize changes from Entra ID back to on-premises Active Directory, reversing the default synchronization direction. The most security-relevant writeback features are:

**Password writeback:** Changes made to passwords in Entra ID (including self-service password reset) are written back to the on-premises account. This is convenient for users but means that an attacker who can reset a password through Entra ID (perhaps by passing MFA through phishing or MFA fatigue) can change the on-premises password, breaking the on-premises Kerberos key.

**Device writeback:** Entra ID device records are written back to on-premises Active Directory, enabling on-premises resources to use device compliance signals from Entra ID for access decisions.

**Group writeback:** Entra ID groups are written back as on-premises distribution groups or security groups, allowing cloud-managed groups to be used for on-premises access control.

Each writeback feature extends the cloud's ability to modify the on-premises environment, which means that security controls applied only at the on-premises level may be bypassed through the cloud writeback path.

### 6.6.4 THE SEAMLESS SINGLE SIGN-ON KERBEROS ACCOUNT

When Entra Connect's Seamless Single Sign-On feature is enabled, a computer account named `AZUREADSSOACC` is created in on-premises Active Directory. Entra ID uses this account's Kerberos key to decrypt Kerberos tickets that on-premises domain-joined computers obtain and present during cloud authentication, enabling transparent SSO to cloud services from domain-joined endpoints.

The `AZUREADSSOACC` account's Kerberos key is known to Entra ID (Microsoft's cloud service), which means that anyone who compromises Entra ID's access to that key could potentially forge Kerberos tickets - though this is a Microsoft-infrastructure-level concern rather than a customer-side configuration issue. What is a customer-side concern is the rotation cadence of the `AZUREADSSOACC` password: Microsoft recommends rotating it every 30 days, but many environments have never rotated it since Entra Connect was first deployed.

\---

## 6.7 FEDERATION, TRUST, AND THE IDENTITY PROVIDER / RELYING PARTY MODEL

Federation is the mechanism by which one organization's authenticated identity is accepted as valid by another organization's resources, without those organizations sharing a directory or a credential store. The model is built on a contractual trust relationship between an Identity Provider (IdP) and a Relying Party (RP).

### 6.7.1 THE IDP/RP TRUST MODEL

An **Identity Provider** is the system responsible for authenticating the user and issuing the identity assertion. The IdP holds credentials, performs authentication, and signs the resulting token with its private key.

A **Relying Party** is the system that consumes the identity assertion to make an access decision. The RP trusts the IdP's assertion without independently verifying the user's credential — it validates the token's signature against the IdP's public key and uses the claims inside the token to make its authorization decision.

The contractual element is the federation agreement: a documented policy governing what claims the IdP will assert, what assurance levels apply, what the RP will accept, and how incidents will be handled. In federal environments, this contract is formalized through Federation Practice Statements and Federation Trust Agreements — documents that establish the legal and technical basis for the cross-boundary trust. The DoD ICAM Federation Framework specifically addresses these agreements for internal and external federation, covering the DoD Federation Hub, classified systems, mission partners, and Special Access Program (SAP) environments.

### 6.7.2 CLAIMS AND ATTRIBUTES IN FEDERATION

The assertion a federation protocol carries is only as valuable as the attributes it includes. Claims provide the RP with the information needed to make access control decisions. A relying party that needs to know whether a user is authorized to access a particular resource might require claims stating the user's department, clearance level, job title, organizational affiliation, or membership in a specific group.

The security significance of attributes in federation is bidirectional. Too few attributes and the RP cannot make meaningful access decisions — it may either block all access or grant excessive access based on minimal identity information. Too many attributes and the assertion becomes a privacy exposure — attributes that the RP does not need should not be included in the assertion, because each attribute in a federation assertion that traverses the network is attribute that an interceptor can read.

In FICAM contexts, claims often carry federal-specific values: PIV policy OIDs (assurance level indicators), agency codes, position sensitivity codes, and cross-agency user identifiers. These attributes are what enable attribute-based access control (ABAC) decisions at the receiving resource — the resource does not simply know "this is Alice from Agency X," it knows "this is Alice from Agency X, with a Top Secret clearance, in position sensitivity category 6, eligible for access to resources requiring FICAM IAL3/AAL3."

### 6.7.3 OAUTH 2.0 AND OPENID CONNECT IN FEDERAL ENVIRONMENTS

OAuth 2.0 and OpenID Connect (OIDC) have become the dominant protocols for modern application authentication, including in federal environments adopting cloud-native and mobile architectures. Unlike SAML, which carries identity information in signed XML assertions, OIDC carries identity in signed JSON Web Tokens (JWTs) — a more compact format suited to web APIs and mobile applications.

In an OIDC flow, authentication produces two primary tokens. The **ID token** is a signed JWT issued by the IdP that carries the authenticated user's identity claims. The **access token** is a credential that the client presents to a protected API to prove it has been authorized to act on the user's behalf. Access tokens may be JWTs themselves or opaque strings, depending on the API design.

The security significance of token-based authentication is the lifecycle of the tokens themselves. Access tokens are typically short-lived (minutes to an hour), limiting the damage from theft. **Refresh tokens** are longer-lived credentials that allow a client to obtain new access tokens without re-authenticating the user. The **Primary Refresh Token (PRT)** is Microsoft's implementation of a long-lived refresh token for domain-joined and Entra ID-joined devices — it is stored in LSASS on the device, renewed through Entra ID, and used to obtain access tokens for all Microsoft cloud services. Theft of a PRT provides an attacker with persistent, MFA-bypassing access to all cloud resources the user is entitled to, until the token expires or is explicitly revoked.

\---

## 6.8 AUTHORITATIVE ATTRIBUTES AND NON-PERSON ENTITY IDENTITY

Federal identity frameworks increasingly distinguish between person identities and non-person entity (NPE) identities — the service accounts, devices, workloads, and automated processes that operate within federal systems but are not human users. The governance of NPE identity is one of the most significant gaps in many FICAM implementations, partly because NPE identity has historically been an afterthought in identity governance programs designed around human users.

An authoritative identity attribute is an attribute whose value is established by an authoritative source — the source of record for that particular data element — and conveyed to consuming systems through a trusted mechanism. In federal environments, authoritative attributes for person identities typically originate from HR systems, personnel databases, and credential issuers; they include legal name, position, organizational affiliation, clearance level, and identity assurance indicators.

For NPE identities, the concept of authoritative attributes is analogous but different in character. A service account's authoritative attributes include its purpose, the system it serves, its owner (a human accountable for it), its approved privileges, its expected network behavior, and its certificate or managed credential information. The challenge is that most organizations lack a systematic registry of NPE identities with authoritative attributes — service accounts accumulate across years of system deployment with inconsistent documentation and unclear ownership.

The security significance of this gap is direct. Services that consume identity attributes for access control decisions will make incorrect decisions when the attributes are wrong, stale, or absent. A workload identity that has not had its attributes reviewed in three years may retain permissions that were appropriate at deployment but are excessive today. An NPE whose owner has left the organization may have no one responsible for its security configuration. And an NPE with no authoritative registration is, by definition, undocumented — which means it is not subject to whatever governance controls the organization applies to documented identities.

\---

## 6.9 HOW THESE SERVICES BECOME ATTACK SURFACE: AN INTEGRATED VIEW

The services described in this chapter do not fail in isolation. The attack paths that Part II examines in operational detail typically exploit the connections between services rather than a single vulnerable component. A brief integrated view is appropriate here — not to teach the techniques, but to ensure the reader carries the right mental model of how these services relate to each other before encountering the exploitation details.

### 6.9.1 THE AD CS ATTACK SURFACE

AD CS attack surface concentrates in certificate templates. A template that allows the enrollee to specify the subject name, that includes a client authentication EKU, and that grants broad enrollment rights creates a path from a low-privileged domain account to a certificate that can authenticate as any domain principal. The certificate obtained through this path can be used for PKINIT to obtain a Kerberos TGT — completing the escalation to domain administrator without ever touching the domain controller directly.

Beyond templates, the CA private key itself is Tier 0. An attacker who obtains the CA private key can issue certificates for any purpose to any principal, permanently, until the CA is revoked and reissued. The CA's placement in the Tier 0 administrative model — not on general-purpose servers, not reachable through standard administrative channels, protected by the same controls as domain controllers — is what makes this risk manageable rather than realized.

### 6.9.2 THE AD FS AND FEDERATION ATTACK SURFACE

The AD FS attack surface converges on the token-signing certificate. An attacker who extracts the private key can issue Golden SAML assertions for any identity, bypassing all authentication controls, for as long as the certificate remains trusted by relying parties. The extraction path typically runs through the AD FS server (which must be Tier 0 level security), through the service account that can read the DKM container, or through the DKM container in Active Directory itself if access permissions are misconfigured.

The federation trust configuration also creates attack surface: Relying Party Trusts that are overly permissive in what claims they accept, Claim Provider Trusts that do not validate the integrity of incoming assertions, and claim transformation rules that promote asserted attributes to trusted authorization decisions without verification.

### 6.9.3 THE HYBRID IDENTITY ATTACK SURFACE

Hybrid identity creates bidirectional attack surface. From on-premises to cloud: the Entra Connect synchronization account has DCSync-equivalent permissions — compromise of this account is effectively equivalent to domain compromise plus cloud tenant compromise. The PTA agents and AD FS servers are high-value targets whose compromise enables cloud authentication manipulation. From cloud to on-premises: writeback features allow cloud-side changes to propagate to the on-premises directory, meaning an attacker who compromises cloud-privileged roles can potentially affect on-premises accounts.

The on-premises-to-cloud attack path is particularly concerning because it means that an Active Directory compromise — which traditional security architecture may view as contained on-premises — can immediately translate to cloud tenant compromise. And conversely, cloud-side compromises — Global Administrator accounts, Service Principals with privileged roles, or stolen Primary Refresh Tokens — may provide paths back to on-premises resources through federation and writeback.

\---

## 6.10 SUMMARY AND TRANSITION

This chapter has examined the enterprise identity services that surround Active Directory and extend its trust across certificate authentication, federation boundaries, cloud tenants, and hybrid architectures.

Active Directory Certificate Services implements PKI inside the Windows environment, with certificate templates as the central policy interface whose misconfiguration creates direct paths to domain compromise through forged certificate authentication. The CA's private key and the template configuration are Tier 0 assets even when the CA server is not treated as one. Active Directory Federation Services implements cross-boundary identity assertion through claims-based security tokens, with the token-signing certificate as the asset whose theft enables the most durable and broadly destructive persistence available — Golden SAML. Microsoft Entra ID provides cloud-native identity with its own attack surface in Service Principals, application permissions, legacy authentication protocols, and the long-lived tokens that MFA bypass attacks target. Hybrid identity, through Microsoft Entra Connect, bridges these environments and introduces synchronization accounts with replication-equivalent permissions, writeback paths that allow cloud changes to affect on-premises directories, and Kerberos accounts whose rotation is commonly neglected.

The connecting thread is that every service described here extends trust, and extending trust means extending attack surface. The security boundary is not the domain controller; it is the entire identity trust system described across the last six chapters — directory architecture, networking substrate, governance framework, authentication protocols, and now the enterprise services that issue, extend, and federate the credentials those protocols consume.

The next chapter completes Part I by establishing the assessment and baseline engineering discipline that connects foundational knowledge to the offensive and defensive operations of Parts II and III — teaching how to evaluate an identity trust system against its intended configuration, identify where it has drifted, and prioritize what must be corrected before an adversary finds it first.

\---

## ACRONYMS

ABAC — Attribute-Based Access Control · AD — Active Directory · AD CS — Active Directory Certificate Services · AD FS — Active Directory Federation Services · AIA — Authority Information Access · API — Application Programming Interface · CA — Certificate Authority · CAC — Common Access Card · CAR — Certification Authority Revocation · CDP — Certificate Revocation List Distribution Points · CRL — Certificate Revocation List · CSR — Certificate Signing Request · DC — Domain Controller · DKM — Distributed Key Manager · DN — Distinguished Name · DoD — Department of Defense · DoD ICAM — Department of Defense Identity, Credential, and Access Management · DNS — Domain Name System · EKU — Extended Key Usage · FCPCA — Federal Common Policy Certificate Authority · FICAM — Federal Identity, Credential, and Access Management · FPKI — Federal Public Key Infrastructure · GUID — Globally Unique Identifier · HR — Human Resources · IdP — Identity Provider · IIS — Internet Information Services · ITU — International Telecommunication Union · JIT — Just-In-Time · JWT — JSON Web Token · KDC — Key Distribution Center · LDAP — Lightweight Directory Access Protocol · MFA — Multi-Factor Authentication · MMC — Microsoft Management Console · NDES — Network Device Enrollment Service · NPE — Non-Person Entity · NTLM — New Technology LAN Manager · OID — Object Identifier · OIDC — OpenID Connect · OCSP — Online Certificate Status Protocol · PHS — Password Hash Synchronization · PIV — Personal Identity Verification · PIM — Privileged Identity Management · PKI — Public Key Infrastructure · PKINIT — Public Key Cryptography for Initial Authentication in Kerberos · PRT — Primary Refresh Token · PTA — Pass-through Authentication · RBAC — Role-Based Access Control · RP — Relying Party · SAM — Security Account Manager · SAML — Security Assertion Markup Language · SAP — Special Access Program · SCEP — Simple Certificate Enrollment Protocol · SID — Security Identifier · SSO — Single Sign-On · STS — Security Token Service · TGT — Ticket Granting Ticket · TLS — Transport Layer Security · UPN — User Principal Name · WAP — Web Application Proxy · WID — Windows Internal Database

## REFERENCES

1. Schroeder, W., Christensen, L. Certified Pre-Owned: Abusing Active Directory Certificate Services. SpecterOps Blog. 2021. https://posts.specterops.io/certified-pre-owned-d95910965cd2 (accessed July 14, 2026).
2. Microsoft. Active Directory Certificate Services Overview. Microsoft Learn. https://learn.microsoft.com/windows-server/identity/ad-cs/active-directory-certificate-services-overview (accessed July 14, 2026).
3. Microsoft. Active Directory Federation Services Overview. Microsoft Learn. https://learn.microsoft.com/windows-server/identity/active-directory-federation-services (accessed July 14, 2026).
4. Microsoft. What is Microsoft Entra ID? Microsoft Learn. https://learn.microsoft.com/entra/fundamentals/whatis (accessed July 14, 2026).
5. Microsoft. What is Microsoft Entra Connect? Microsoft Learn. https://learn.microsoft.com/entra/identity/hybrid/connect/whatis-azure-ad-connect (accessed July 14, 2026).
6. Microsoft. What is Privileged Identity Management? Microsoft Learn. https://learn.microsoft.com/entra/id-governance/privileged-identity-management/pim-configure (accessed July 14, 2026).
7. National Institute of Standards and Technology. Digital Identity Guidelines: Federation and Assertions (SP 800-63C-4). July 2025. https://csrc.nist.gov/pubs/sp/800/63/c/4/final (accessed July 14, 2026).
8. General Services Administration. FICAM Architecture. IDManagement.gov. https://www.idmanagement.gov/arch/ (accessed July 14, 2026).
9. Department of Defense. DoD ICAM Federation Framework. (Confirm current edition and date at manuscript submission.)
10. RFC 4556 — Public Key Cryptography for Initial Authentication in Kerberos (PKINIT). https://www.rfc-editor.org/rfc/rfc4556 (accessed July 14, 2026).
11. RFC 6749 — The OAuth 2.0 Authorization Framework. https://www.rfc-editor.org/rfc/rfc6749 (accessed July 14, 2026).
12. RFC 8414 — OAuth 2.0 Authorization Server Metadata. https://www.rfc-editor.org/rfc/rfc8414 (accessed July 14, 2026).
13. OASIS Standard. Security Assertion Markup Language (SAML) 2.0. https://docs.oasis-open.org/security/saml/ (accessed July 14, 2026).

