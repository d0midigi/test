---
icon: camera-web
---

# Chapter 95 - SQL Server Integrated Authentication, Linked-Server Abuse, and Service-to-Domain Privilege Escalation (Offensive)

### Abstract

Microsoft SQL Server frequently participates in Active Directory through Windows Integrated Authentication, domain service accounts, Service Principal Names, constrained delegation, linked servers, scheduled jobs, backup systems, application identities, and administrative automation. Those relationships can transform database compromise into a broader identity attack path. This chapter examines SQL Server primarily from the offensive perspective, beginning with server and instance discovery and progressing through integrated authentication, SQL role escalation, impersonation, database trust, linked-server traversal, SQL Agent, service-account compromise, credential storage, SPN and delegation relationships, and movement from database authority into Windows or Active Directory. Defensive treatment follows through service-identity reduction, linked-server governance, delegation control, SQL role hardening, credential separation, network segmentation, auditing, and attack-path validation.
