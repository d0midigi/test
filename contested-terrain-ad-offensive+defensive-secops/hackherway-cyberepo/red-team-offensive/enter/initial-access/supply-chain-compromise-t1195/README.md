---
description: 'MITRE ATT&CK Tactic #T1195'
---

# Supply Chain Compromise (T1195)

Adversaries may manipulate products or their delivery mechanisms within the supply chain, aiming to compromise data or systems before reaching the end consumer.

Various stages in the supply chain are vulnerable to compromise:

1. <mark style="color:purple;">**Manipulation of Development Tools**</mark>**:**
   * Attackers may tamper with the tools used during software development.
2. <mark style="color:purple;">**Manipulation of a Development Environment**</mark>**:**
   * Adversaries could compromise the overall development environment where software is created.
3. <mark style="color:purple;">**Manipulation of Source Code Repositories**</mark>**:**
   * Source code repositories, whether public or private, may be targeted for manipulation.
4. <mark style="color:purple;">**Manipulation of Source Code in Open-Source Dependencies**</mark>**:**
   * Attackers may inject malicious code into open-source dependencies used by various applications.
5. <mark style="color:purple;">**Manipulation of Software Update/Distribution Mechanisms**</mark>**:**
   * Compromising the mechanisms for software updates or distribution allows adversaries to inject malicious software.
6. <mark style="color:purple;">**Compromised/Infected System Images**</mark>**:**
   * Removable media, like USB drives, infected at the manufacturing stage can introduce compromise.
7. <mark style="color:purple;">**Replacement of Legitimate Software**</mark>**:**
   * Legitimate software may be replaced with modified versions containing malicious code.
8. <mark style="color:purple;">**Sales of Modified/Counterfeit Products**</mark>**:**
   * Legitimate distributors might unintentionally sell products that have been modified or are counterfeit.
9. <mark style="color:purple;">**Shipment Interdiction**</mark>**:**
   * Intercepting shipments provides an opportunity for adversaries to compromise the products during transit.

While any component of hardware or software can be affected, attackers often focus on adding malicious code to legitimate software through distribution or update channels. Targeting may be broad, affecting many consumers, or specific, with additional tactics deployed only against selected victims. Additionally, popular open-source projects, widely used as dependencies, may be targeted to spread malicious code to users of those dependencies.
