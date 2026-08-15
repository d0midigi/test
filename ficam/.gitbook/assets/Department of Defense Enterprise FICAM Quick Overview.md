DoD FICAM / E-ICAM Security Framework Model Quick Overview



Department of Defense Enterprise Identity, Credential, and Access Management (DoD E-ICAM) is the primary enterprise identity service solution for DISA on an unclassified (NIPRNet) network. DoD E-ICAM system creates a single user record, consolidates all pertinent data associated with the individual requesting access under one (1) account. DoD E-ICAM captures and maintains a record of names, digital signatures, access granted permissions, and other identifiers and identifying attributes from authoritative domain sources to provide and maintain an active record of access management to DoD systems and resources. This record of access management includes Financial Management and Reporting Records and Information Systems Security Records. This information is used to audit application access and to validate those individuals that have the appropriate, cleared level of access required when attempting to access DoD applications and information systems.



###### **DoD E-ICAM Primary Systems**



DoD E-ICAM consists of three key primary systems: 



1\. DoD E-ICAM Identity Provider (IdP)

2\. DoD E-ICAM Master User Record (MUR)

3\. DoD E-ICAM Automated Account Provisioning (AAP)



DoD E-ICAM systems are hosted in the Microsoft Cloud Azure tenant DEAS INF, referred to as the "GFUD Tenant." What the general populous commonly refers to as GFUD or GD is a subsystem of the DoD E-ICAM IdP built across multiple subscriptions and virtual machines in the 'GFUD Tenant' alongside of the virtual machines and subscriptions hosting SailPoint, Radiant Logic, DIU, and other systems.



###### **DoD E-ICAM IdP PII Collection Process**



The DoD E-ICAM IdP collects user data to include a user's name (last name, first name, middle initial); unique identifiers including DoD identification number (DoD ID Number), other unique identifiers (not SSN), FASC-N, login name, legacy login name, and persona user-name; object class; rank; title; job title; Persona Type Code (PTC); primary and other work email addresses; personal display name (PDN); work contact information, including administrative organization, duty organization, department, company (derived), building, address, mailing address, country, organization, phone, fax, mobile, pager, DSN phone, VoIP bridge, other pager, city, zip code, post office mailing address,  country, organization, phone, fax, mobile, pager, DSN phone, other fax, other mobile, other pager, city, zip code, post office 

box, street address, Country Of Citizenship (CTZP \_CTRY \_CD), state, room number, assigned unit name, code and location, attached unit name, code and location, major geographical location, major command, assigned major command, and base, post, camp, or station; US 

government agency code; service code; personnel category code; non-US government agency object common name; user account control; information technology service entitlements; and PKI certificate Information, including FASN-C, PIV Auth certificate Issuer, PIV Auth certificate serial number, PIV Auth certificate principal name, PIV Auth  certificate `SubjectAlternativeName`, PIV Auth Thumbprint, PIV Auth Issuer, PlV Auth Common Name (CN), certificate issuer, ID certificate serial number, ID certificate principal name, ID Thumbprint, ID CN, signature certificate e-mail address, Signature Subject Alternative Name UPN, Signature Thumbprint, Signature Issuer, Signature serial number, Signature CN, Encryption (Public Binary Certificate), Encryption Thumbprint, `CertificateIssuer`, Encryption Serial Number, Encryption CN, distinguished name, PKI login identity, e-mail encryption certificate, and other certificate information. 



DoD E-ICAM AAP provides an automated System Authorization Access Required (SAAR) service that leverages authoritative data sources to pre-populate data.



###### **An Important Note on FICAM and Privacy: Why PII Must be Collected**



PII data is required to implement and operate DoD information technology (IT). If the PII data is not available for a specific individual, then that individual would not be able to access key new components of DoD IT such as business systems access, which is required for individuals to complete their work. DoD E-ICAM cannot remove an individual's PII data, since it does not actively collect PII directly from the individual, but rather obtains those data elements from other established systems that are approved to collect PII data.



DoD E-ICAM provides a Privacy Act statement to its users which notifies individuals about the authority to collect such information requested, and for the purposes of which it will be used, other routine uses of the information, and the consequences of declining to provide the information. The consent banner is presented on the Mission Partner SailPoint website upon gaining initial access.

###### 

###### **Principle Purpose of FICAM / DoD E-ICAM**



Department of Defense Enterprise Identity, Credential, and Access Management (DoD E-ICAM) Systems is a DoD Enterprise Identity Service that creates a single user record, consolidating all pertinent data associated with the individual under one (1) account. Its principle purpose is to capture and maintain a record of names, signatures, and other identifiers for the purpose of validating the trustworthiness of individuals requesting access to Department of Defense (DoD) systems and information.



###### **Supporting DoD ICAM Documentation**



* DoDI 5105.19, Defense Information Systems Agency (DISA)
* DoDD 1000.25, DoD Personnel Identity Protection (PIP) Program
* DoD Personal Identity Verification (PIV) Program
* DoD Enterprise User Data Management Plan for Persons and Personas
* DoD Global Information Grid 2.0 Concept of Operations (GIG 2.0 CONOPS)
* DoDI 5200.46, DoD Investigative and Adjudicative Guidance for Issuing the Common Access Card (CAC)
* DoDI 8520.03, Identity Authentication for Information Systems
* Homeland Security Presidential Directive-12 (HSPD-12), National Cybersecurity
* Federal Information Processing Standards Publication 201-3, Personal Identity Verification (PIV) of Federal Employees and Contractors
* DoD Regulation 5200.2-R, Personnel Security Program
* Department of Defense Manual (DoDM) 1000.13, Volume 1 - DoD Identification (ID) Cards: ID Card Lifecycle
* Mission Partner Identity, Credential and Access Management (MP-ICAM) User Guide



###### **Key Terminology**



* DoD E-ICAM - DoD Enterprise Federal Identity, Credential, and Access Management
* IdSS - Identity Synchronization Services
* DISS - Defense Information Security System
* DCPDS - Defense Civilian Personnel Data System
* AMID - Army Master Identity Directory
* AFDS - Air Force Directory Services
* CMIS - DISA Corporate Management Information System
* DISA Global Directory
* EIAS - Enterprise Identity Attribute Service
* GFUD - Global Federated User Directory
* DMDC BAE - Defense Manpower Data Center Backend Attribute Exchange
* eMASS - Enterprise Mission Assurance Support
* Navy Federation
* DMDC - Defense Manpower Data Center

