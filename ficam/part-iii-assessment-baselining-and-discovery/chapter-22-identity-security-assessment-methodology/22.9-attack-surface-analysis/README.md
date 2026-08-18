# 22.9 Attack Surface Analysis

The federal government and the Department of Defense (DoD) conduct distinct types of security, assessment, and command and mission readiness engagements tailored for federal agencies, military components, and the Defense Industrial Base (DIB). These programs range from contractor compliance verifications (e.g., CMMC) to civilian infrastructure evaluations.

### Department of Defense (DoD) and Defense Contractor Engagements

#### DIBCAC Assessment

Conducted by the Defense Industrial Base Cybersecurity Assessment Center (DIBCAC) under the Defense Contract Management Agency (DCMA), these security engagements evaluate defense contractors' compliance with the NIST SP 800-171 and the Cybersecurity Maturity Model Certification (CMMC) requirements. They span Basic (self-assessments), Medium, and High (government-led verification).

#### Cyber Operational Readiness Assessment (CORA) and the Cyber Command Readiness Inspection (CCRI)

In March 2024, the Joint Force Headquarters-DoD Information Network (JFHQ-DoDIN) officially launched the Cyber Operational Readiness Assessment (CORA), replacing the decade-old Command Cyber Readiness Inspection (CCRI). This change shifted the military's cybersecurity evaluation framework from rigid check-box compliance to active, threat-informed operational survivability. As part of the CORA process. boundary reviews assess how well external-facing systems are fortified against both internal and external cyber threats.

#### The Evolution From CCRI to CORA

Introduced in 2010 by the Defense Information Systems Agency (DISA), the Command Cyber Readiness Inspection (CCRI) was a rigorous, compliance-driven technical audit. Air Force and Army assessment teams from the JFHQ-DoDIN physically visited DoD commands to run vulnerability scans using the eEye Retina Security Vulnerability Scanner and the DISA Gold Disk and manually audited system configurations against Security Technical Implementation Guides (STIGs). The program graded installations on a traditional pass or fail system, where a score below 70% was a failure. The major flaw with this structure was that it created a culture of compliance surges. Commands would scramble to fix vulnerable systems immediately by doing last minute patching and system hardening before a scheduled inspection to pass the inspection, only for network discipline to degrade shortly afterward.

The Department of Defense recognized this repeated, flawed pattern, and moved away from the old framework because static compliance audits do not equal real-world security, especially since adversaries exploit dynamic network behaviors rather than just missing patches. CORA addresses these gaps by prioritizing operational resilience, mission assurance, and data-driven risk mitigation. Instead of mapping vulnerabilities to generic severity lists, CORA utilizes threat matrices from the MITRE ATT\&CK Framework to assess broad authorization boundaries and perimeters. Furthermore, while finding a major flaw during the old inspection meant an automatic failure, the new model allows commands to actively remediate flaws live during the assessment. This structure prioritizes Key Indicators of Risk (KIORs) and heavily penalizes boundary and perimeter vulnerabilities, which allows commands to dynamically allocate resources based on actual threat data rather than generic vulnerability lists generated from the Gold Disk scanning.

The table below demonstrates the differences in how both security assessments addressed gaps in key areas of network:

| Capability           | Legacy CCRI                                   | Modern CORA                                     |
| -------------------- | --------------------------------------------- | ----------------------------------------------- |
| **Core Mindset**     | Compliance and static check-boxes.            | Operational resilience and mission assurance.   |
| **Scoring Logic**    | Pass/Fail numeric grade (1–100).              | Data-driven risk mitigation and threat impact.  |
| **Threat Context**   | Vulnerability severity maps (e.g., IAVMs).    | MITRE ATT\&CK framework threat matrices.        |
| **Inspection Scope** | Limited subset of infrastructure samples.     | Broad authorization boundaries and perimeters.  |
| **Remediation**      | Finding a major flaw meant an automatic fail. | Flaws can be remediated live during assessment. |

#### Contractor Compliance and Civilian Engagements

Outside of active military commands, defense contractors and civilian entities face their own distinct engagements. The Defense Industrial Base Cybersecurity Assessment Center (DIBCAC), operating under the Defense Contract Management Agency (DCMA), conducts DIBCAC Assessments to evaluat3e contractors' compliance with the NIST SP 800-171 and the Cybersecurity Maturity Model Certification (CMMC) requirements. These engagements span Basic self-assessments up to High government-led verifications. To support this, the Supplier Performance Risk System provides a mandatory scoring mechanism where defense contractors log their summary scores to demonstrate baseline cyber readiness before contract awards.

On the civilian and interagency side, the Cybersecurity and Infrastructure Security Agency (CISA) provides the Cyber Security Evaluation Tool (CSET). This downloadable software application guides both public and private infrastructure owners through systematic evaluations of IT and Industrial Control Systems (ICS), featuring specialized modules like the Ransomware Readiness Assessment (RRA). CISA also deploys regional Protective Security Advisors (PSAs) to conduct on-site vulnerability surveys, infrastructure evaluations, and facilitated tabletop exercises for state, local, and private sector partners.

For cloud technologies, the Federal Risk and Authorization Management Program, or FedRAMP, provides a standardized security assessment and authorization process for Cloud Service Providers (CSPs) looking to offer services to federal agencies, utilizing accredited Third Party Assessment Organizations, or 3PAOs, to validate security controls.

#### Service-Specific Cyberspace Readiness Engagements

While joint forces set the overarching requirements, each branch of the military maintains its own dedicated cyber commands and execution wings to perform localized readiness engagements.

#### United States Army Security (USA) Engagements

The U.S. Army operates Command Cyber Readiness Teams (CCRTs) and Cyber Readiness Brigades under the U.S. Army Cyber Command (ARCYBER). These units conduct localized Cyber Readiness and Information Assurance (CRIA) evaluations across Army posts, camps, and stations, helping local commanders shift into active CORA-style monitoring to harden both tactical networks and garrison installation alike. This massive enterprise focus allows the Army to prevent initial access by shutting down weak entry points across hundreds of sprawling military bases.

#### United States Navy (USN) Security Engagements

The U.S. Navy manages its cyber posture through Fleet Cyber Command (FLTCYBER) and the U.S. 10th Fleet, which deploys Navy Cyber Readiness Teams to assess both afloat shipboard networks and ashore naval facilities. The Navy also maintains rigorous Strategic Systems Programs (SSP) assessments to evaluate the specific readiness and command cybersecurity controls of its nuclear and ballistics deterrent infrastructure. Because ships at sea rely heavily on satellite communications, these naval engagements test island-mode survival and enforce strict air-gapping. This prevents lateral movement within the network and ensures that a crew can successfully thwart an active attack locally without losing control of radars or missile systems.

#### United States Air Force (USAF) Security Engagements

The U.S. Air Force operates through the 16th Air Force (AFCYBER) and its 688th Cyberspace Wing, which established the first sanctioned CORA team within the service to train specialists for internal readiness checks across Air Force bases. The Air Force also conducts Cyber Vulnerability Assessments (CVAs) on specific mission-critical weapon systems and flight-line networks to identify threat susceptibilities outside of traditional IT systems. This focus protects Operational Technology (OT) like cargo planes, fighter jets, and ballistics systems from firmware manipulation and supply chain malware, preventing execution of malicious code via diagnostic tools before it can infect aircraft and surface station security postures.

#### United States Space Force (USSF) Security Engagements

The U.S. Space Force orchestrates targeted readiness engagements primarily through Space Delta 6 (SPOC), focusing specifically on satellite control networks, ground stations and bases, and space launch deltas. Because space assets are uniquely vulnerable to telemetry and link disruptions, their Defensive Cyber Operations (DCO) focuses closely on boundary defenses and immediate threat isolations defined by the CORA framework. These assessments focus primarily on preventing command injections, ensuring that ground control stations can successfully detect and discard altered or forged satellite communications and signals to prevent an adversary from blinding a spy satellite or steering a military asset out of orbit.

#### United States Marine Corps (USMC) Security Engagements

The U.S. Marine Corps relies on Marine Corps Cybersecurity Command (MARFORCYBER) to deploy assessment elements that ensure the Marine Corps Enterprise Network and the Marine Corps Base networks (MCEN) conform to joint standards. Given the expeditionary nature of the Marines, they place a significantly heavy emphasis on Tactical Cyber Readiness Assessments to secure deployed tactical networks by Marine Expeditionary Units (MEUs). These engagements simulate a chaotic frontline environment and train forward-deployed Marines to rapidly isolate compromised radios or field laptops under fire, combating active intrusions and preventing adversaries from eavesdropping or intercepting troop movements via local WiFi intercept tools or drone-based hacking rigs.

Primarily managed by the Joint Force Headquarters-DoD Information Networks (JFHQ-DoDIN), CORA replaced legacy inspections to focus more on operational behaviors, perimeter defenses, and real-time mission assurance across DoD installations.

#### Supplier Performance Risk System (SPRS) Scoring

A mandatory reporting engagement where defense contractors log and manage their NIST SP 800-171 summary scores to demonstrate baseline cyber readiness before contract awards.

### Civilian and Interagency Federal Security Engagements

#### CISA Cyber Security Evaluation Tool (CSET)

Provided at no cost by the Cybersecurity and Infrastructure Security Agency (CISA), CSET is a downloadable software GOTS (Government-Off-The-Shelf) application guiding both public and private infrastructure owners through systematic evaluations of IT and Industrial Control Systems (ICS), featuring specialized modules like the Ransomware Readiness Assessment (RRA).

#### FedRAMP Security Assessments

The Federal Risk and Authorization Management Program (FedRAMP) provides a standardized security assessment and authorization process for Cloud Service Providers (CSPs) looking to offer services to federal agencies, utilizing accredited Third Party Assessment Organizations (3PAOs).

#### Protective Security Advisors (PSAs) and Critical Infrastructure Assessments

CISA deploys regional PSAs to conduct on-site vulnerability surveys, infrastructure evaluations, and facilitated tabletop exercises (via CISA Tabletop Exercise Packages) for state, local, and private sector partners.

### Understanding How These Programs Protect the Military

To understand how these security readiness and security assessment programs protect the military and federal defenses, it helps to view them through the lens of a typical castle defense> The legacy CCRI was more of an inventory audit - it checked if the castle gates were locked and if the guards had manuals. CORA, on the other hand, is a live siege drill - it tests how fast the guards react when an enemy actually tries to scale the mote or wall.

While the JFHQ-DoDIN provides the overarching CORA framework, each military branch faces distinct battlefield environments (e.g., ships at sea, satellites in orbit, tactical radios in the mud); therefore, their specific engagements focus on preventing different types of intrusions.

#### Strategic Differences in Thwarting Attacks

```
[Attacker Vector]
       │
       ├──► Air Force CVA ──────────► Thwarts Ground & Avionic System Hijacks
       ├──► Navy Afloat/SSP ────────► Thwarts Electronic/RF Spoofing & Silo Breaches
       ├──► Space Delta 6 ──────────► Thwarts Telemetry Interception & Signal Jamming
       └──► Marine Tactical Cyber ──► Thwarts Frontline Eavesdropping & Spoofing
```

The table below breaks down the specific tactical value and defensive significance each service's assessment brings to the table:

| Service Engagement    | Strategic Focus                      | Primary Threat Detected                                                                | How It Thwarts/Prevents Attacks                                                                                                       |
| --------------------- | ------------------------------------ | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Air Force CVA         | Weapon and Avionic Systems           | Firmware maniulation and supply chain malware.                                         | Thwarts execution by finding hidden vulnerabilities in flight-line diagnostic tools before they can infect aircraft.                  |
| Navy Afloat and SSP   | Isolation and Maritime RF            | Sattelite link eavesdropping, C3 signal interception, and ballistic control tampering. | Prevents lateral movement by ensuring shipboard networks remain strictly isolated (a                                                  |
| Space Delta 6         | Ground-to-Space Links                | Telemetry spoofing and command injection attacks.                                      | Thwarts intercedption by testing encryption and validating that satellite commanding networks reject unauthorized or unknown signals. |
| Army CCRTs            | Massive Enterprise Scale             | Identity theft, phishing, and unpatched base systems and networks.                     | Prevents initial access by shutting down weak entry points across hundreds of sprawling military bases.                               |
| Marine Tactical Cyber | Expeditionary/Field and Ground Units | Electronic warfare, cyber terrorism, signal intercept, and tactical spoofing.          | Combats active intrusions by training forward-deployed Marines to rapidly isolate compromised radios or field laptops under fire.     |

#### The Tactical Impact: CORA Versus Branch Engagements

#### **1. General CORA (JFHQ-DoDIN): Thwarting Perimeter Breaches**

CORA focuses heavily on Key Indicators of Risk, or KIORs, specifically targeting outer perimeters and public-facing servers and their networks.

* **The Significance:** It assumes an adversary is already trying to break in. By constantly analyzing boundary defenses, CORA ensures that a single compromised password on an unmonitored server cannot be used to breach the entire Department of Defense Information Network (DoDIN) and DoD Global Information Grid (GIG).

#### **2. Air Force Cyber Vulnerability Assessments (CVAs): Preventing Weapon Sabotage**

While CORA protects the office computers and email networks (the IT), the Air Force CVA protects the planes and missiles (the Operational Technology, or OT).

* **The Significance:** If an adversary tries to upload malicious code into an F-35 fighter jet via a maintenance laptop, a standard network scan won't catch it. Air Force CVAs actively look for these highly specialized, non-traditional software threats to prevent catastrophic hardware failure during flight.

#### 3. Navy Afloat & Strategic Systems Programs (SSP): Thwarting Maritime Isolation Failures

A Navy destroyer at sea relies on satellite communication. If a sailor plugs an infected USB drive into a shipboard computer, the ship cannot easily call back to a central cybersecurity team for help.

* **The Significance:** Navy afloat assessments test "island-mode" survival. They ensure that if a ship is hit with ransomware, the crew can successfully thwart the attack locally, isolate the infected deck, and keep the ship's radar and missiles fully functional without losing control of the vessel.

#### 4. Space Delta 6 Mission Assessments: Thwarting Satellite Hijacking

Space Force networks do not just face attackers; they face heavy electronic jamming, signal manipulation, and rogue ground stations trying to send malicious telemetry to satellites.

* **The Significance:** Space Delta 6 assessments focus heavily on preventing **command injection**. They ensure that ground control stations can successfully detect and discard altered or forged signals, ensuring an adversary can never blind a spy satellite or steer a military asset out of orbit.

#### 5. Marine Corps Tactical Assessments: Thwarting Frontline Electronic Warfare

Marines operate on the move, establishing temporary command tents using tactical satellite dishes and field radios.

* **The Significance:** These assessments simulate a chaotic frontline environment. They test how well communications equipment thwarts local Wi-Fi intercept tools, drone-based hacking rigs, and physical theft of gear, preventing adversaries from eavesdropping on active troop movements.
*



*
