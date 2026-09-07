# Offensive and Assessment Appendices

These appendices help red teams, penetration testers, and continuous monitoring tools evaluate the environment against real-world attack pathways.

{% hint style="warning" %}
_All offensive testing, reconnaissance (e.g., BloodHound, PowerView) and post-exploitation tools (e.g., Impacket) must be executed from designated standalone assessment systems or explicitly authorized via the Command's localized **Authorized Tool List (ATL)** and active **Rules of Engagement (RoE)**, as they fall outside the standard commercial scope of the DoDIN APL._
{% endhint %}

The **DoD Information Network Approved Products List (DoDIN APL)**, which is managed by the Defense Information Systems Agency (DISA) incorporates a list of allowable software that is allowed to be executed in federal Active Directory domains.

However, there is a major catch when it comes to specialized offensive tools: **Open-source tools like BloodHound, PowerView, and Impacket are almost never found on the DoDIN APL.**

To get onto the DoDIN APL, a vendor must sponsor the software through a rigorous, incredibly expensive multi-month testing process overseen by the Joint Interoperability Test Command (JITC). Since free, open-source projects do not have corporate backing to fund such a process, they are omitted by default.

DoD Red Teams, Cyber Protection Teams (CPTs), and authorized penetration testers instead bypass the standard DoDIN APL through alternative approval frameworks:

#### **1. Command-Specific Authorized Tool Lists (ATL)**

Every major military cyber component (e.g., USCYBERCOM, ARCYBER, AFCYBER) maintains an internal Authorized Tool List (ATL) or Approved Software List (ASL) specifically for its cyber operators.

* These lists allow specialized scripts, exploit frameworks, and post-exploitation toolkits (like BloodHound, Impacket, Mimikatz) to be used strictly during active, authorized engagements.
* Use of these tools is strictly governed by the engagement's Rules of Engagement (RoE) and the team's localized Authority to Operate (ATO).

#### 2. "Dirty Box" and Standalone System Exemptions

Red teams frequently conduct their assessments from completely isolated, non-cleared laptops or closed-loop networks (often referred to as "dirty boxes"). Because these devices do not directly connect to or persist on the operational enterprise DoDIN, they do not require standard DoDIN APL clearance. This allows operators to leverage full distributions like Kali Linux or Commando VM legally.













