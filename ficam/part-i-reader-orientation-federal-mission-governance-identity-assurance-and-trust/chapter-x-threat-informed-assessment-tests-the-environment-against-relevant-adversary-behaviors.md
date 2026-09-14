---
description: TOC - Subchapters for FICAM/ICAM in Federal & DoD AD Networks
---

# Chapter X - Threat-Informed Assessment Tests the Environment Against Relevant Adversary Behaviors

**Takeaway:** Below is a fully built, threat-informed TOC structured specifically for FICAM/ICAM, DoD, and federal Active Directory (AD) environments. It aligns identity-centric security with adversary behaviors seen in real federal threat models (APT29, APT28, Volt Typhoon, UNC2452). Every Subchapter begins with a Guided Link to expand any area.

### Purpose of Threat-Informed Assessment Testing

**Threat-informed assessment testing exists for one reason:** To prove whether your environment can withstand the exact behaviors real adversaries use, not just whether it passes compliance inspections and checklists.

That is the core purpose - but the full picture is much richer. Below is a complete breakdown structured for federal/ DoD identity systems and Active Directory.

### Logic Behind Threat-Informed Testing

Threat-informed testing validates your environment against _actual adversary tradecraft_ so you can measure real security, not theoretical compliance.

#### 1. Validate Security Against Real Adversarial Behaviors

Threat-informed testing maps your environment to MITRE ATT\&CK, DoD threat intelligence, and known APT tradecraft. It answers the question:

_"Can our identity, network, and cloud systems withstand the exact techniques used by nation-state actors such as APT29, Volt Typhoon, or UNC2452?"_

This is fundamentally different from compliance testing, which only checks whether controls _exist._

### 1. Threat-Informed Assessment Foundations

* [**Purpose of Threat-Informed Testing**](chapter-x-threat-informed-assessment-tests-the-environment-against-relevant-adversary-behaviors.md#purpose-of-threat-informed-assessment-testing)**:** Why federal AD environments require Adversary-behavior validation.
* [**Mapping Adversary Behaviors to FICAM/ICAM**](chapter-x-threat-informed-assessment-tests-the-environment-against-relevant-adversary-behaviors.md#mapping-adversary-behaviors-to-ficam-icam)**:** Identity-centric threat alignment.
* **Threat Models for Federal and DoD AD:** Nation-state, insider, supply chain, hybrid identity threats.
* **Assessment Scope Definition:** Domains, forests, enclaves, hybrid identity boundaries.

### 2. Identity-Centric Adversary Behaviors

* **Credential Access Techniques:** LSASS scraping, DPAPI abuse, token theft.
* **Authentication Downgrade Attacks:** NTLM fallback, Kerberos downgrade, channel binding bypass.
* **Privilege Escalation Chains:** Shadow admins, misconfigured delegations, SIDHistory abuse.
* **Identity Trust Exploitation:** AD trust abuse, hybrid identity trust chain compromise.

### 3. Active Directory Attack Surface Mapping

* **AD Object Exposure Analysis:** ACLs. GPOs, privileged groups.
* **Kerberos Attack Surface:** AS-REP Roasting, TGS Roasting, delegation abuse.
* **Service Account Vulnerabilities:** SPNs, weak passwords, unconstrained delegation.
* **Domain Trust and Forest Boundary Weaknesses:** External trusts, forest trusts, SID filtering gaps.

### 4. Network-Centric Adversary Behaviors

* **Lateral Movement Techniques:** SMB, WinRM, RDP, DCOM, WMI.
* **Internal Network Trust Boundary Testing:** VLAN segmentation, Tier 0 isolation, privileged network paths.
* **Boundary Bypass Techniques:** VPN pivoting, enclave hopping, identity-to-network pivoting.
* **Identity-Network Mapping:** Mapping AD privilege-to-network access.

### 5. Hybrid Identity Adversary Behaviors

* **AD Connect Attack Surface:** PTA/PHS risks, connector permissions, sync rule abuse.
* **Federation Service Exploitation:** AD FS token signing theft, misconfigured claims.
* **Cloud Token Abuse:** Refresh token theft, CA bypass, session hijacking.
* **Cross-Cloud Trust Chain weaknesses:** Identity bridging risks.

### 6. Threat-Informed Test Design

* **Selecting Relevant Adversary Behaviors:** MITRE ATT\&CK, DoD threat intel, federal-adversary profiles.
* **Building Identity-Centric Test Cases:** Credential theft, privilege escalation, trust abuse.
* **Building Network-Centric Test Cases:** Lateral movement, segmentation bypass.
* **Hybrid Identity Test Cases:** Cloud pivoting, federation compromise.
* **Test Coverage Mapping:** Ensuring alignment with FICAM/ICAM controls.

### 7. Execution of Threat-Informed Assessment

* **Identity Attack Path Execution:** Graph-based privilege escalation validation.
* **Kerberos and NTLM Attack Simulation:** Roasting, relaying, downgrade attempts.
* **Network Lateral Movement Simulation:** East-West movement validation.
* **Hybrid Identity Compromise Simulation:** Cloud pivoting, federation token abuse.
* **Boundary Security Validation:** Enclave boundaries, Tier 0 isolation.

### 8. Defensive Control Validation

* **Identity Hardening Validation:** Credential Guard, LSA protection, privileged access tiering.
* **Kerberos and NTLM Hardening Validation:** Signing, channel binding, delegation restrictions.
* **Network Segmentation Validation:** Tiered admin model, privileged network isolation.
* **Hybrid Identity Hardening Validation:** AD Connect, AD FS, Conditional Access.
* **Detection and Logging Validation:** AD logs, Kerberos logs, DNS logs, EDR identity telemetry.

### 9. Findings, Risk Scoring and FICAM/ICAM Alignment

* **Identity-Centric Findings:** Credential exposure, privilege escalation paths.
* **Network-Centric Findings:** Segmentation gaps, lateral movement paths.
* **Hybrid Identity Findings:** Federation weaknesses, cloud pivot paths.
* **Risk Scoring Against FICAM/ICAM:** Mapping findings to federal identity requirements.
* **Remediation Prioritization:** Tier 0 first, identity trust second, network segmentation third.

### 10. Reporting and Continuous Threat-Informed Improvement

* **Threat-Informed Reporting Structure:** Identity, network, hybrid identity sections.
* **Adversary Behavior Coverage Metrics:** ATT\&CK mapping, identity coverage.
* **Continuous Assessment Cycles:** Quarterly identity testing, annual trust chain validation.
* **Integration with CCRI/CORA:** Mapping threat-informed tests to federal scoring frameworks.

### Full Chapter Narrative

### Threat-Informed Assessment Tests the Environment Against Relevant Adversary Behaviors

Threat-informed assessment is the disciplined practice of evaluating an identity-centric environment - particularly federal and DoD Active Directory (AD) domains - against the real behaviors adversaries use to compromise identity systems. Rather than relying solely on compliance checklists or theoretical controls, threat-informed testing validates whether FICAM/ICAM-aligned identity architectures can withstand the Tactics, Techniques, and Procedures (TTPs) used by nation-state actors, Advanced Persistent Threats (APTs), and sophisticated insiders.

In federal and DoD networks, identity is the operational backbone. Active Directory forests, domain trusts, federation services, and hybrid identity bridges form the trust fabric that enables authentication, authorization, and access control. When adversaries compromise identity, they compromise everything. Threat-informed assessment ensures that identity systems are not only compliant, but resilient against adversarial behaviors observed in real-world incidents such as the SolarWinds/UNV2452, APT29 credential theft campaigns, Volt Typhoon Living-Off-The-Land (LOTL) operations, and privilege escalation chains seen across federal enclaves.

#### Identity-Centric Adversary Behaviors

Adversaries target identity first because it provides the most leverage. Credential theft, token impersonation, Kerberos manipulation, and abuse of misconfigured delegation allow attackers to quickly escalate privileges rapidly. Threat-informed assessment evaluates whether identity protections - Credential Guard, hardened Kerberos policies, privileged access tiering, and strong authentication - actually prevent these behaviors.

#### Active Directory Attack Surface

ADs complexity creates fertile ground for misconfigurations. Weak ACLs, over-privileged service accounts, unconstrained delegation, and legacy NTLM authentication expand the attack surface ten-fold. Threat-informed testing maps these exposures to adversarial techniques, validating whether the environment can resist roasting attacks, trust exploitation, and privilege escalation paths.

#### Network-Centric Behaviors

Identity compromise often leads to lateral movement. Threat-informed assessment tests whether segmentation, Tier 0 isolation, and enclave boundaries prevent identity-driven movement across the network. It validates whether adversaries can pivot using SMB, WinRM, WMI, or RDP once they obtain the needed credentials.

#### Hybrid Identity Behaviors

Federal and DoD environments increasingly rely on hybrid identities: AD Connect, AD FS, Azure AD, and cloud tokens, to name a few. Threat-informed assessment evaluates whether adversaries can compromise federation services, steal token-signing certificates, abuse sync permissions, or bypass Conditional Access controls.

#### Test and Design

Threat-informed tests are built by selecting adversary behaviors relevant to the environment's established threat model. Each test simulates a real attack chain - credential theft > privilege escalation > trust exploitation > lateral movement > cloud pivot. Execution therefore validates whether controls work as intended, not just whether they exist and are "in place."

#### Findings and FICAM/ICAM Alignment

Findings are mapped to FICAM/ICAM identity requirements, ensuring federal identity governance aligns with adversary-resistant architecture. Risk scoring prioritizes identity trust chain weaknesses, Tier 0 exposures, and hybrid identity vulnerabilities.

#### Continuous Improvement

Threat-informed assessment is not a one-time event, or a set-it-and-forget-it process. Federal and DoD identity systems evolve, and so do adversaries. Continuous testing ensures identity resilience remains aligned with real-world threats.

### MITRE ATT\&CK Mapping for Each Subchapter

Below is a precise mapping of each subchapter to relevant MITRE ATT\&CK Framework Tactics, Techniques, and Procedures (TTPs). Each item begins with a Guided Link so you can expand any area.

#### 1. Threat-Informed Assessment Foundations

* **Threat Models:** T1589, T1591 (Reconnaissance)
* **Scope Definition:** T1069 (Permissions Group Discovery)

#### 2. Identity-Centric Adversary Behaviors

* **Credential Access:** T1003 (LSASS), T1555 (Credentials From Password Stores), T1550 (Use of Valid Accounts)
* **Authentication Downgrade:** T1557.001 (NTLM Relay), T1208 (Kerberos Downgrade)
* **Privilege Escalation Chains:** T1068 (Exploitation for Privilege Escalation), T1098 (Account Manipulation)
* **Identity Trust Exploitation:** T1484.001 (Domain Trust Modification)

#### 3. Active Directory Attack Surface Mapping

* **AD Object Exposure:** T1069.002 (Domain Groups), T1484 (Domain Policy Modification)
* **Kerberos Attack Surface:** T1558.003 (Kerberoasting), T1558.004 (AS-REP Roasting)
* **Service Account Vulnerabilities:** T1078.002 (Service Accounts)
* **Domain Trust Weaknesses:** T1484.001 (Domain Trust Modification)

#### 4. Network-Centric Adversary Behaviors

* **Lateral Movement:** T1021 (Remote Services), T1047 (WMI), T1059 (Command Execution)
* **Trust Boundary Testing:** T1078 (Valid Accounts), T1570 (Lateral Tool Transfer)
* **Boundary Bypass:** T1090 (Proxy), T1563 (Remote Service Session Hijacking)

#### 5. Hybrid Identity Adversary Behaviors

* **AD Connect:** T1098 (Account Manipulation), T1550 (Token Abuse)
* **Federation Exploitation:** T1550.003 (Pass-the-Ticket), T1552 (Sensitive Files)
* **Cloud Token Abuse:** T1528 (Cloud Tokens), T1550.004 (Refresh Token Theft)
* **Cross-Cloud Trust:** T1484 (Policy Modification)

#### 6. Threat-Informed Test Design

* **Selecting Behaviors:** TTP alignment across ATT\&CK
* **Identity Test Cases:** T1003, T1558, T1098
* **Network Test Cases:** T1021, T1047
* **Hybrid Test Cases:** T1550, T1528
* **Coverage Mapping:** ATT\&CK matrix alignment

#### 7. Execution of Threat-Informed Assessment

* **Identity Attack Paths:** T1069, T1484
* **Kerberos/NTLM Simulation:** T1558, T1557
* **Lateral Movement Simulation:** T1021, T1047
* **Hybrid Compromise Simulation:** T1550, T1528
* **Boundary Validation:** T1570, T1090

#### 8. Defensive Control Validation

* **Identity Hardening:** T1003 mitigation, T1555 mitigation
* **Kerberos/NTLM Hardening:** M1026 (Privileged Account Management)
* **Segmentation Validation:** M1030 (Network Segmentation)
* **Hybrid Hardening:** M1017 (User Training), M1027 (Multi-Factor Authentication (MFA))
* **Detection and Logging:** M1041 (Behavioral Analytics)

#### 9. Findings, Risk Scoring, and FICAM/ICAM Alignment

* **Identity Findings:** Credential exposure, privilege escalation
* **Network Findings:** Segmentation gaps
* **Hybrid Findings:** Federation weaknesses
* **Risk Scoring:** ATT\&CK-aligned scoring
* **Remediation:** Tier 0 prioritization

#### 10. Reporting and Continuous Improvement

* **Reporting Structure:** Identity-network-hybrid sections
* **Coverage Metrics:** ATT\&CK coverage
* **Continuous Cycles:** Quarterly identity testing
* **CCRI/CORA Integration:** Mapping to federal scoring frameworks



### Mapping Adversary Behaviors to FICAM/ICAM
