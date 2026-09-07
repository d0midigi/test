---
icon: cancer
---

# Chapter 91 - PetitPotam, PrinterBug, and Windows Authentication Coercion Against Privileged Systems (Offensive)

### Abstract

Windows authentication coercion attacks exploit legitimate Remote Procedure Call functionality to cause a target system to authenticate to a destination chosen by an adversary. This chapter examines PetitPotam and PrinterBug primarily from the offensive perspective, focusing on the Microsoft Encrypting File System Remote Protocol (MS-EFSRPC) and Microsoft Print System Remote Protocol (MS-RPRN), the conditions that permit coerced machine authentication, and the downstream consequences when that authentication can be captured or relayed. Particular attention is given to coercing domain controllers and other Tier 0 systems, differentiating coercion from credential theft, understanding machine-account authentication, and chaining coerced authentication into Lightweight Directory Access Protocol, Server Message Block, HTTP, and Active Directory Certificate Services abuse. The chapter also compares PetitPotam and PrinterBug with adjacent coercion primitives to show that the durable security problem is broader than any one named technique. Defensive treatment follows through spooler reduction, RPC exposure control, NTLM restriction, signing, Extended Protection for Authentication, certificate-services hardening, telemetry correlation, and attack-path validation.
