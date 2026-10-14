# AD: Replication Topology Planning

Replication topology planning is essential for maintaining consistency and performance in an Active Directory network. Sites and site links define the physical structure, with sites and the subnets of which sites are comprised defining the physical structure of the networks.

Below is the field-level playbook that senior architects keep in their OneNote and includes details such as:

* how to translate WAN circuits
* domain-controller hardware
* business RPO/RTO into an AD site topology that won’t buckle the first time a branch office loses 30 % of its bandwidth—or an attacker drops a rogue DC into a conference room VLAN.

Below is the field-level playbook that senior architects keep in their OneNote: how to translate WAN circuits, domain-controller hardware, and business RPO/RTO into an AD site topology that won’t buckle the first time a branch office loses 30 % of its bandwidth—or an attacker drops a rogue DC into a conference room VLAN.

***

1. ### <mark style="color:yellow;">Start with the Physics: Three Numbers You Must Collect</mark>

***

a. One-way latency (ms) and available bandwidth (Mb/s) between every physical location.\
b. Cost per Mb/s (if metered) or political requirement to keep traffic off certain links during trading hours.\
c. Number of users AND number of authentications per second (not just head-count). A 24×7 factory with 500 shift workers doing hourly re-auth generates more Kerberos traffic than a 2 000-user HQ that works 09:00-17:00.

Put these into a matrix; anything >500 ms or <512 kb/s is a candidate for a read-only DC (RODC) or a separate site with reduced replication frequency.

***

2. ### <mark style="color:yellow;">Map Layer-3 to AD: Subnets First, Sites Second</mark>

***

1. Create one AD subnet object for every L3 summary route (e.g., `10.4.32.0/20`) that is routed to a single location.
2. Never assign a subnet to more than one site; Windows uses the “longest-prefix match” and will pick the first one returned by the DC Locator if there is overlap, causing seemingly random logon delays.
3. Use Description field to store the VLAN ID and WAN circuit ID; your future self (and the firewall team) will thank you.
4. For cloud VNets (Azure VNet, AWS VPC) treat each region as a separate site even if Microsoft or Amazon advertises <2 ms latency—because egress charges are real money and the virtual DC bill will spike if you replicate every 15 min.

***

3. ### <mark style="color:yellow;">Site-Object Design Rules of Thumb</mark>

***

🔸**Rule 1:** One site per “failure domain” that has local IT staff.\
🔸**Rule 2:** ≥2 writable DCs per site if you have ≥500 users or any 24×7 workload.\
🔸**Rule 3:** If the link is metered (satellite, LTE backup) create its own site and set 180-360 min replication interval—even if it is physically next door.\
🔸**Rule 4:** Separate site for DMZ, lab, and Azure AD DS (they get different GPOs and RODCs anyway).\
🔸**Rule 5:** No site should contain DCs from different domains unless you are doing a cross-forest trust migration; otherwise USN rollbacks are almost guaranteed during disaster recovery.

***

4. ### <mark style="color:yellow;">Site-Link Object: More Than Just “</mark><mark style="color:yellow;">`DEFAULTIPSITELINK`</mark><mark style="color:yellow;">”</mark>

***

Attributes you actually care about:

<mark style="color:yellow;">**a.**</mark>**&#x20;Cost (1-99 999) – lower is preferred. Use a consistent scheme:**\
🔸10 = LAN ≤1 Gb/s, <10 ms\
🔸100 = MAN/MPLS 100 Mb/s, 10-40 ms\
🔸200 = VPN 50 Mb/s, 40-80 ms\
🔸300 = satellite 10 Mb/s, >500 ms

<mark style="color:yellow;">**b.**</mark>**&#x20;Interval (minutes):**\
🔸default 180; can go as low as 15, but remember urgent events still fire immediately.\
\
<mark style="color:yellow;">**c.**</mark>**&#x20;Schedule:**\
🔸168-bit bitmap; if you need “trading hours off” set the bits 07:00-17:00 Mon-Fri to 0.\
\
<mark style="color:yellow;">**d.**</mark> **Transport:**\
🔸RPC/IP (default) or SMTP (legacy, schema-only).\
\
<mark style="color:yellow;">**e.**</mark> **Options:**\
🔸`BIT 0x1 = “USE_NOTIFY` (turns on change notification across the link, effectively making it behave like intra-site). Use sparingly; only on high-bandwidth, low-latency MPLS.

### <mark style="color:yellow;">Site-Link Bridge (SLB)</mark>

Only required if you disabled “Bridge all site links” (ISTG option). Create an SLB when you have a hub-and-spoke WAN that does **NOT** route spoke-to-spoke (e.g., carrier-layer-3 VPN that drops traffic between branches). Otherwise, the KCC will try to build direct replicate-to connections and will fail miserably.

***

5. ### <mark style="color:yellow;">KCC & ISTG: The Algorithm That Builds the Graph</mark>

***

Every site owns one ISTG DC (auto-elected = highest NTDS Settings `objectVersionNumber`). The ISTG runs the same KCC algorithm but with two extra constraints:

1. Build a minimum-cost spanning tree using site-link cost as edge weight.
2. Guarantee ≤3 hops between any two DCs in the forest (configurable: `HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Maximum Inter-Site Hops`).
3. Create at least two disjoint paths for config/schema partition (automatic fail-over within 30 min).

If you pin bridgeheads (“preferred bridgehead”), the ISTG skips the election part and only builds connections from the pinned list—if none are available, replication stops (Event ID `1569`).

***

6. ### <mark style="color:yellow;">Placement Math: How Many DCs Per Site?</mark>

***

#### 🔸Authentication-Load Method

Peak logons per second × 2 KB per auth ÷ 0.3 (CPU overhead) = required auth throughput.\
A 2019 VM with 2 vCPU handles ≈1 200 auths/s; divide accordingly.

#### 🔸Replication-Backlog Method

`Expected changes per hour × average object size × (1/compression ratio) × safety factor 3` must be < link capacity during the replication window. Example:\
• 500 password resets/h = 500 × 1 kB = 500 kB\
• Compression 5× → 100 kB\
• 100 kB × 3 = 300 kB must fit inside the 15-min burst\
A 2 Mb/s MPLS can move 225 kB/s → plenty of headroom, so one DC is enough; a 256 kb/s LTE cannot, so either increase interval or drop an RODC locally.

***

7. ### <mark style="color:yellow;">Firewall & Router Checklist</mark>

***

#### 🔸Port Summary

🔸**Intra-site:** 135/TCP + high-port 49152-65535 (2008+) or 1024-5000 (2003)\
🔸**Inter-site:** same, but you can nail 135 + one high port per DC (`HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\TCP/IP Port`)\
LDAPS: 636/TCP (if you use IPSec tunnel mode)\
🔸**Kerberos:** 88/TCP+UDP\
🔸**DNS:** 53/TCP+UDP (RODCs require 53 to writable DNS master)

#### 🔸QoS (Quality of Service)

* Mark DSCP 46 (EF) for RPC traffic coming from DCs; otherwise a 500-machine patch Tuesday will starve replication.

***

8. ### <mark style="color:yellow;">Redundancy Patterns That Actually Work</mark>

***

#### 🔸Hub-and-Spoke HQ + 3 Branches

• Create hub site with 3 DCs (spread across two racks).\
• Each branch = own site, 1 writable DC + 1 RODC for DMZ.\
• Site-link cost 100 HQ→Branch, cost 200 Branch→Branch (via HQ).\
• Enable “Bridge all site links” = YES; no SLB needed.

#### 🔸Full-Mesh Metro (hospital campus)

• One site, four buildings, 10 Gb/s dark fibre.\
• Keep intra-site ring; enable change notification (already default).\
• No site-links needed; treat as single failure domain.

#### 🔸Active-Passive DR Data Center

• DR site = separate site, cost 300, interval 360 min, schedule nights only.\
• Disable automatic site-link bridging; create SLB DR-HQ only.\
• Stand up DCs as RODCs during normal ops; promote to writable only when declared DR (prevents USN rollback).

***

9. ### <mark style="color:yellow;">Cloud & Hybrid Edge-Cases</mark>

***

#### 🔸Azure AD DS

• Creates its own “AADDS” site; do NOT add on-prem DCs to it—KCC will build connections and fail.\
Azure AD joined + line-of-sight to on-prem\
• Devices still use DC Locator; create an AD site whose subnet matches the Azure VNet address space and put at least one DC (IaaS) in it.

#### 🔸AWS Transit Gateway

• Treat each VPC CIDR as a subnet; if you peer VPCs across regions, measure latency—if >100 ms, create separate sites or you will see random logon storms.

***

10. ### <mark style="color:yellow;">Validation and Ongoing Governance</mark>

***

1. **Monthly:** `repadmin /showrepl * /csv | ConvertFrom-Csv | Group-Object 'Number of Failures' | ft Count,Name` – any count >0 needs a root-cause.
2. **Quarterly:** run “Active Directory Topology Diagrammer” (still works on 2022) and diff the Visio against last quarter—new unmanaged site-links = red flag.
3. **After every WAN change:** verify cost still reflects bandwidth; update description field with circuit ID.
4. **After every DC promotion:** check that the new DC is NOT acting as a bridgehead for more than 50 % of its partners (load-spread).
5. **Disaster-recovery test:** Shut down all DCs in one site; verify logon still works and that the KCC rebuilt inbound connections within 30 min (Event ID `1568`).

***

### <mark style="color:yellow;">One-Page Take-Away</mark>

1. Subnet objects must be exact, non-overlapping, and documented.
2. Site-link cost is your WAN traffic-engineering knob—treat it like OSPF cost.
3. Let KCC do its job; disable “preferred bridgehead” unless you have a political need.
4. Anything >500 ms or <512 kb/s gets an RODC and a 360-minute interval.
5. Revisit the topology every time the WAN team changes a circuit; AD replication is only as good as your Layer-3 map.
