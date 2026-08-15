---
icon: address-card
---

# Chapter 16 - Privileged Authority and the Trusted Core

### Abstract

Privileged authority in Active Directory defines the highest perimeter of enterprise control. In Federal Identity, Credential, and Access Management (FICAM) frameworks, identifying, isolating, and defending the Control Plane—or "Tier 0"—is mandatory for satisfying Zero Trust Architecture principles (NIST SP 800-207) and NIST SP 800-53 controls. Tier 0 extends beyond Domain Controllers to encompass any system, service, application, or dependency that can exert direct or indirect control over the identity infrastructure.

This chapter provides a rigorous technical breakdown of privileged administrative structures, directory replication rights, and extended trust boundaries. It analyzes built-in administrative groups, delegation mechanics (`AdminSDHolder`), Directory Replication Service (DRS) abuse, and the expanded ecosystem of Tier 0 assets—including Active Directory Certificate Services (AD CS), identity synchronization engines, virtualization layers, and configuration management tools. By examining offensive control path mapping (BloodHound, transitive delegation, and Shadow Credentials) alongside defensive alignment with the Enterprise Access Model (EAM), Privileged Access Workstations (PAWs), and Clean Source principles, this chapter enables security engineers to construct unbreachable boundaries around the enterprise identity core.

##
