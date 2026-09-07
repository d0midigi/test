# Connecting a "Dirty Box" to a Federal Environment for AD Posture Assessment / Penetration Test

Any experienced security professional already knows that in a standard "black box" test, one might just find a rogue drop in a conference room, plug in a laptop, and see how far DHCP may take them; however, in a federal or DoD black box engagement, the stakes and the network controls (like 802.1X, HBSS/ESS, and automated port-security) make that approach almost impossible without setting off immediate alarms or quickly hitting a dead end.

The term "dirty box" often causes confusion because it sounds like a completely rogue device, but in a federal black box context, the deployment process is highly orchestrated behind the scenes.

A federal red team connects an unmanaged "dirty box" or standalone testing appliance during an authorized black box engagement as such:

#### 1. The Pre-Staged "White Cell" Bypass

A true black box test is rarely 100% blind; a microscopic **White Cell** (a tiny group of leadership and network defenders who know the test is happening) always exists for safety. To get an unmanaged testing device onto a hardened network without triggering an immediate physical or automated lockdown:

* **MAC/802.1X Allowlisting:** Formerly known as "whitelisting," the White Cell will pre-authorize the MAC address by manually assigning it to a switchport via mac-address-sticky and once the switchport logs a MAC address violation, the port will automatically shutdown, or bypass 802.1X requirements for a specific, designated network port (or set of ports) in the building.
* **The "Dropbox" Method:** Operators rarely sit in a closet with a laptop. Instead, they physically plant a small, headless, customized tactical appliance (a "Rubber Ducky," a Raspberry Pi, a "Dropbox," or a "puck" - often a hardened Intel NUC or custom 1U server running Kali or Commando VM) into that pre-staged port.









