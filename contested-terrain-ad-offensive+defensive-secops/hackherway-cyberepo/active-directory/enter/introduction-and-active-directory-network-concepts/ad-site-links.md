# AD: Site Links

_**Site links**_ are configured to establish connections between sites, specifying transport, cost, and replication schedules to optimize replication traffic and efficiency. The _**Knowledge Consistency Checker (KCC)**_ generates and maintains the replication topology, ensuring that directory updates are propagated between domain controllers within and across sites.

Below is the practitioner-level “missing manual” for AD site links—everything you need to stop treating them as “lines on a Visio” and start using them as traffic-engineering levers that keep 10 000 DCs in sync without saturating a 2 Mb/s MPLS circuit or blowing the CIO’s cloud egress budget.

***

### <mark style="color:yellow;">What a Site-Link Object Actually Is Under the Hood</mark>

***

Class: `siteLink` (in `CN=Inter-Site Transports,CN=Sites,CN=Configuration,<forest DN>`)\
Must-have attributes\
• `cost` (INTEGER) – 1-99 999, lower = preferred.\
• `replInterval` (INTEGER) – minutes between pull cycles (15-10080).\
• `schedule` (OCTET\_STRING) – 168-byte bitmap (0-167 = Mon 00:00 – Sun 23:00).\
• `siteList` (DN\_WITH\_STRING) – multi-value, lists the `CN=<Site>,CN=Sites,…` objects that are adjacent on this logical link.\
Optional but useful\
• `options` (BITMAP) – `bit 0x1 = USE_NOTIFY` (turns on change-notification across the link).\
• `transportType` – distinguished name of the transport object (`CN=IP` or `CN=SMTP`).

The KCC reads these attributes once per hour (default) and builds NTDS Connection objects under each DC’s `NTDS Settings` container. If you delete a site link, the KCC does NOT clean up the connections immediately—it waits until the next topology generation cycle (60 min, tunable).

***

### <mark style="color:yellow;">Transport Containers: IP vs. SMTP (and why SMTP is almost extinct)</mark>

***

`CN=Inter-Site` Transports contains two child objects:

1. `CN=IP` – uses RPC over TCP (135 + high-port). Supports all partitions (schema, config, domain, DNS, app). Can be wrapped inside IPSec tunnels; supports Kerberos sign/seal.
2. `CN=SMTP` – uses signed and encrypted e-mail (`X.400`-style) via `msExchSmtpRelayServer` attribute. Cannot carry domain or DNS partitions (no full-domain context). Requires PKI (certificates on every DC). Only useful for non-contiguous forests or cruise-ship scenarios. Most organizations delete the SMTP container to avoid accidental use.

You can create your own transport (e.g., “IP-HTTPS”) if you write a custom MTA, but the KCC will ignore it unless you also register a new `interSiteTransport` class and provide a DLL that implements `IInterSiteTransport`—in other words, don’t.

***

### <mark style="color:yellow;">Cost = WAN Traffic-Engineering Knob, Not “Preference”</mark>

***

The KCC runs a minimum-cost spanning-tree algorithm (Kruskal) across the site-link graph.&#x20;

**Rules:**

• Cost is additive along a path. A→B cost 100 + B→C cost 50 gives A→C cost 150.\
• If two paths have equal cost, KCC keeps both (dual redundancy).\
• If you need active/passive, make the backup path cost ≥ 10× the primary (e.g., 100 vs 1000).\
• Cost values are opaque to routing protocols—your MPLS OSPF cost 50 does NOT have to match AD cost 50, but keeping them proportional makes troubleshooting easier.

### <mark style="color:yellow;">Quick Reference Matrix</mark>

Bandwidth (Mb/s) Latency (ms) Suggested Cost\
🔸≥ 1000 < 10 10\
🔸100–1000 10-40 100\
🔸10–100 40-80 200\
🔸< 10 or metered > 80 300-500

***

### <mark style="color:yellow;">Schedule Bitmap: The 168-byte Secret</mark>

***

Each bit represents one hour. Byte 0 bit 0 = Monday 00:00–00:59, Byte 0 bit 1 = Monday 01:00–01:59 … Byte 23 bit 7 = Sunday 23:00–23:59.\
GUI only shows 15-minute granularity, but PowerShell can flip individual bits:

```powershell
$sl = Get-ADObject -Identity "CN=DEFAULTIPSITELINK,CN=IP,CN=Inter-Site Transports,CN=Sites,CN=Configuration,DC=contoso,DC=com" -Properties schedule
$sched = New-Object -TypeName System.DirectoryServices.ActiveDirectory.ActiveDirectorySchedule
$sched.SetDailySchedule("Monday","23:00","Tuesday","06:00")   # nightly window
Set-ADObject $sl -Replace @{schedule=$sched.GetSchedule()}
```

If all bits are 0, the link is effectively disabled except for urgent replication (password lockout, etc.).

***

### <mark style="color:yellow;">Change-Notification Across a Site-Link (</mark><mark style="color:yellow;">`USE_NOTIFY`</mark><mark style="color:yellow;">)</mark>

***

`Bit 0x1` in `options` tells the KCC to create connections with the “notify” flag set.

**Result:**

• Originating DC still waits 15 s (configurable) then pushes changes instead of waiting for the next pull cycle.\
• Compression still occurs if >32 kB.\
• Only use on high-bandwidth, low-latency links (≤40 ms, ≥100 Mb/s) or you will saturate the WAN every time HelpDesk resets 50 passwords at 08:00.

**Enable:**

```powershell
Set-ADObject "CN=HQ-Branch1,CN=IP,CN=Inter-Site Transports,CN=Sites,CN=Configuration,DC=contoso,DC=com" -Replace @{options=1}
```

***

### <mark style="color:yellow;">Site-Link Bridges (SLB) – When and Why?</mark>

***

Global flag “Bridge all site links” (default = YES) creates transitive adjacency: if SiteA linked to Hub, and Hub linked to SiteB, KCC treats SiteA–SiteB as cost = A–Hub + Hub–B.

Disable it (NO) if your IP routing is NOT fully meshed—e.g., carrier L3VPN that drops spoke-to-spoke traffic. Then you must create an SLB object that explicitly lists the site-links you want to be transitive.

**Example:**\
🔸**Site-links:** Main-SiteA, Main-SiteB, Main-SiteC\
🔸**Routing:** spokes can only reach Main, not each other.

Create SLB “SpokeBridge” containing all three links; KCC can now build A→B via Main.

***

### <mark style="color:yellow;">Bridgehead Servers: Let KCC Pick, Unless You Have a Better Reason</mark>

***

KCC elects one BH per partition per site (schema, config, each domain, DNS, custom).\
Manual list (“preferred”) is supported, but:

• If all preferred BHs for a partition are down, replication STOPS until you either promote one or remove the list.\
• You must list at least two DCs per partition or you create a single point of failure.\
• Preferred BHs are stored in `msDS-PreferredGCSite` and `msDS-PreferredDataLocation` on the DC object—document them!

***

### <mark style="color:yellow;">Registry and Attribute Knobs Most People Miss</mark>

***

`HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters`\
• `Inter-site replication delay` (secs) – default 900 (15 min) before first pull after schedule opens.\
• `Disable Inter-site Compression` (DWORD) – 1 = turn off XPRESS (lab testing only).\
• `RPC/IP Port` – nail DC to single high port so firewall rule is one line.

🔸**Site-link attribute:**\
• `replInterval` can be set to 0 → replicate only during schedule window, but immediately when window opens (useful for “nightly only” DR links).

***

### <mark style="color:yellow;">Cloud and Hybrid Edge-Cases</mark>

***

#### 🔸Azure VNet–to–On-Prem

• Create an AD site whose subnet = VNet CIDR; cost 100, interval 30 min, schedule 24×7.\
• If you u

se Azure ExpressRoute, measure latency—if <10 ms you can safely enable `USE_NOTIFY`.\
AWS Transit Gateway with multiple VPCs\
• Each VPC = separate subnet object; if inter-region latency >100 ms create separate sites or you will see random DC Locator timeouts.

#### 🔸Azure AD DS

• AADDS creates its own site named “AADDS”; do NOT add on-prem DCs to it—KCC will try to build connections and fail with event 1265.

***

### <mark style="color:yellow;">Monitoring and Alerting</mark>

***

#### 🔸Event IDs

`1586` – ISTG cannot elect a BH (empty site?)\
`1569` – All preferred BHs down.\
`1399` – Partner cannot bind (firewall or SPN).\
`2042` – _“It has been too long…”_ – tombstone lifetime breach.

#### 🔸Performance Counters

🔸`NTDS\DRA Inbound Bytes Compressed (between sites, after compression)`\
🔸`NTDS\DRA Inbound Bytes Total (between sites, before compression)` – ratio should be 3-10×.

**PowerShell one-liner to find site-links with default cost (lazy design):**

```powershell
Get-ADReplicationSiteLink -Filter * -Properties Cost | Where-Object {$_.Cost -eq 100} | Measure-Object
```

***

### <mark style="color:yellow;">Quick Design Recipe</mark>

***

1. List every physical location with WAN circuit size and latency.
2. Create one AD site per location (unless RTT <10 ms and unlimited bandwidth).
3. Create subnet objects that match your IP plans; assign to sites.
4. Pick a cost scheme (10/100/200/300) and document it.
5. Set interval 15 minutes for LAN, 30-180 minutes for WAN, 360 minutes for satellite.
6. Leave “Bridge all site links” = YES unless your carrier blocks spoke-spoke.
7. Enable `USE_NOTIFY` only on LAN-grade links.
8. Never pin bridgeheads without listing at least two DCs per partition.
9. Review replication compression ratio monthly; re-cost links if ratio <2×.
10. After every WAN change, update cost or schedule and regenerate topology diagram.

***

### <mark style="color:yellow;">Bottom Line</mark>

A site-link is not a “dumb pipe”—it is a weighted, scheduled, compressible, firewall-friendly, Kerberos-authenticated replication contract between islands of domain controllers. Treat it like an OSPF interface: give it the right cost, keep the bitmap clean, and the KCC will build you a self-healing, loop-free, multi-path topology that survives DC failures, WAN outages, and even your next acquisition’s mystery network.
