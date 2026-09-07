---
icon: compact-disc
---

# Chapter 69 - Credential Material Extraction, Secret Recovery, and Post-Compromise Identity Harvesting (Offensive)

### Abstract

Once an adversary obtains execution on a Windows endpoint, server, administrative workstation, or identity infrastructure system, the next question is often not what vulnerability to exploit, but what authentication material the compromised system already possesses. This chapter examines credential access primarily from the offensive perspective: Local Security Authority Subsystem Service memory, Security Account Manager and SECURITY hives, cached domain credentials, Local Security Authority secrets, Kerberos tickets, Data Protection API material, Windows Credential Manager, browser secrets, private keys, certificates, application credentials, service-account secrets, cloud tokens, synchronization credentials, directory databases, backups, and administrative artifacts. Particular attention is given to credential provenance, portability, privilege context, offline extraction, protected-process boundaries, and deciding which recovered artifact most efficiently advances the attack graph. Defensive treatment follows the offensive analysis through credential isolation, Windows Defender Credential Guard, Local Security Authority protection, privileged-access separation, managed identities, secret reduction, key protection, telemetry, and post-compromise credential invalidation. The chapter establishes that compromised systems should be evaluated not merely as hosts, but as repositories of reusable identity authority.
