---
icon: cassette-vhs
---

# Chapter 97 - Privileged Access Workstation/Secured Administrative Workstation (PAW/SAW) and Jump-Host Compromise, Administrative Session Theft, and Tier 0 Pivoting (Offensive)

### Abstract

Privileged Access Workstations, jump hosts, bastions, remote administration servers, and management enclaves are intended to constrain privileged operations to hardened locations. Their concentration of administrative sessions, tools, credentials, certificates, remote-management access, and Tier 0 connectivity also makes them high-value offensive targets. This chapter examines privileged access infrastructure primarily from the attacker’s perspective, progressing from system discovery through local privilege escalation, session identification, token theft, Kerberos ticket access, certificate exposure, RDP and remote-management abuse, clipboard and drive redirection, management-tool credential storage, administrative session hijacking, and pivoting into domain controllers, PKI, federation, cloud identity, and management platforms. Defensive treatment follows through credential isolation, Remote Credential Guard, privileged-session separation, application control, device attestation, network restriction, session telemetry, reauthentication, and attack-path validation.
