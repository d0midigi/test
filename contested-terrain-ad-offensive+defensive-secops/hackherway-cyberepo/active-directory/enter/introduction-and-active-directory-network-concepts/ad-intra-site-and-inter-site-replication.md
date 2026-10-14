---
description: Differences Between Two Replication Engines Explained
---

# AD: Intra-Site and Inter-Site Replication:

Below I've provided some field-level detailed that are based on my experiences (and that are not contained in textbooks): the exact algorithms, timers, registry knobs, compression math, failure behaviors, and security edge-cases that determine whether your next password change reaches a branch office in 15 seconds or 15 hours.

### <mark style="color:yellow;">Architectural Split: Why Microsoft Created Two Engines</mark>

Active Directory is a multi-master directory, but WAN links are neither symmetric nor are they reliable. Microsoft, therefore, split replication into two manually-invisible transports:

<p align="center"><em><strong>Intra-Site (IS) Replication</strong></em> assumes LAN-like conditions (&#x3C;10 MS, ≥10 Mb/s, no monetary cost).</p>

<p align="center"><em><strong>Inter-Site (IT) Replication</strong></em> assumes "slow, expensive, possibly dial-up" links. Each site object in AD can declare its own cost, schedule, interval, and transport protocol (RPC/IP, or SMTP for non-contiguous namespaces).</p>

The transport decision is made by the _**KCC (Knowledge Consistency Checker)**_ on each DC. The KCC builds two NTDS Connection objects for every DC: one under NTDS Settings (**intra**) and another under the Site-Link (**inter**). They never share connections; if a DC is moved to a different site, the KCC will delete the old intra connections and will regenerate new inter ones.

### <mark style="color:yellow;">Intra-Site Replication – Deeper Than a "Ring"</mark>

Ring topology is only the default for ≤ 7 DCs. Above that, the KCC creates a "mesh with shortcuts" to guarantee ≤ 3 hops between any two DCs and ≤ 4 transitive partners per DC (to cap LDAP search overhead). The algorithm is documented in the MS-KCC.

#### 🔸Timers

* Change notification (default 15 seconds): originating DC queues an RPC packet to all inbound partners.
* Subsequent notification delay (default 3 seconds): staggered to avoid ACK collisions.
* Poll interval for partners that missed the notification: 1 hour (controlled by the replication topology update period (seconds) registry `DWORD` under `HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters`).

#### 🔸Transport

* Uses RPC over TCP dynamic ports:
  * 49152-65535 on 2008+
  * 1024-5000 on 2003, or the port you set in `HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\TCP/IP Port`
* No compression; Data is sent "as-is" to save CPU cycles.
* Packet size is limited by `MaxReplicationSize` (default 40 MB). Larger objects (e.g., 200 MB certificate template) trigger an "out-of-band" replication cycle that immediately bypasses the normal queue.

#### 🔸Concurrency

* Each directory partition (schema, config, domain, DNS, app) gets its own IS connection object, so a DC can sustain up to `N` partitions x `M` partners concurrent RPC calls. You can throttle with Replicator concurrency registry `DWORD` (default 8).

### <mark style="color:yellow;">Inter-Site Replication - Every Knob You Can Turn</mark>

* Default "window" is 180 minutes (3 hours) with 90 minute intervals (the time between the start of two consecutive cycles). You can set per-site-link values in AD Sites and Services (AD SS); the UI only shows 15 minute granularity, but the attribute `schedule` is a 168-byte bitmap (one bit per hour). Set it to all `0s` except one bit if you want nightly replication.

#### 🔸Compression

* **Trigger:** > 32 kB of uncompressed data in a single object or aggregate packet.
* **Algorithm:** XPRESS (LZNT1) via `RtlCompressBuffer`, same as NTFS compressed folders. Typical ratio 3-10x's depending on attribute density (`samAccountName`, description compression well; JPEG certificates do not).
* **CPU Cost:** ≈ 1 core-second per 100 MB on 2019+; older DCs may stall for large blocks.
* **Disable for Lab Testing:** `HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Disable Inter-site Compression = 1` (`DWORD`).

#### 🔸Transport Choices

* **RCP/IP (default):** Requires 135/TCP + high-port range; needs to traverse firewalls.
* **SMTP:** Only for schema, config, and GC-partial replicas; uses signed and encrypted mails via `msExchSmtpRelayServer` attribute; cannot carry domains or DNS partitions; rarely used today.

### <mark style="color:yellow;">Bridgehead (BH) Election</mark>

* Per partition, per site, the _**ISTG (Inter-Site Topology Generator)**_ picks on BH server. The algorithm prefers:

1. Up-time > 24 hours
2. NTDS Settings object has `options |= IS_INTER_SITE_AUTO_GENERATED`
3. Lowest `bridgeheadRole` weight (manually assigned weight wins).
4. **You can pin a BH:** NTDS Settings → Right-click → _"This server is a preferred bridgehead,"_ but then you must do it for every partition or the KCC will complain (Event ID `1569`).

### <mark style="color:yellow;">Change-Tracking and USN Bubbles</mark>

Both IS and IT use the same database layer: each DC keeps a high-watermark USN for every partner. The _**"Up-to-Dateness Vector (UTDV)"**_ table prevents echo-chambers. When a DC writes a new USN it also increments the `invocationId` (database epoch) so that restore-then-replicate scenarios do not create divergence. If a DC is restored with an unsupported method (e.g., snapshot older than tombstoned lifetime) its `invocationId` changes and the entire partition is re-replicated (full sync), possibly saturating your WAN.

### <mark style="color:yellow;">Conflict Resolution (Who Wins When the Same Attribute Changes)?</mark>

1. Version number (higher one wins)
2. Timestamp (later wins)
3. Server GUID (lower GUID wins - deterministic tie-breaker)

{% hint style="info" %}
### **Note:**

Password changes are an exception: they use a "last-writer-wins" policy but also trigger urgent replication.
{% endhint %}

### <mark style="color:yellow;">Urgent/Special Replication Events</mark>

These bypass the normal schedule and compress even inside the same site:

| 🔸Event                                                    | 🔸Outcome (Description)                                                        |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Account lockout                                            | Event ID `4740`                                                                |
| Password change for domain admin, server, or trust account | <p><code>userPwd</code><br><code>unicodePwd</code><br><code>dBCSPwd</code></p> |
| RID pool exhaustion                                        | Replicate new RID block                                                        |
| LAPS password write                                        | `ms-Mcs-AdmPwd`                                                                |
| DNS records update                                         | `_msdcs.<forest>`                                                              |

Notification still uses the same RPC channel, but the delay is 0 seconds, which is configurable. Urgent replication delay is set to registry `DWORD` default 0.

### <mark style="color:yellow;">Monitoring and Health Checks</mark>

#### 🔸Performance Counters

* NTDS/DRA Inbound Bytes Compressed (between sites, after compression)
* NTDS/DRA inbound Bytes Total (between sites, before compression) - divide to get compression ratio.
* NTDS/DRA Pending Replication Synchronizations - sustained > 25 indicates backlog.

#### 🔸Event Log KPIs

* `1399:` partner cannot bind (check port `135/TCP` or high-range).
* `1586:` ISTG cannot elect a BH (empty site)?
* `2042:` "It has been too long since this machine replicated" - tombstone lifetime breach.

### <mark style="color:yellow;">One-Liner to Find Largest Unreplicated Delta</mark>

Using PowerShell, execute the below command to find the largest unreplicated Delta in your domain:

```
repadmin /showrepl * /csv | ConvertFrom- Csv | Where-Object {$_. 'Number of Failures' -gt 0} | Sort-Object 'Time Since Last Success' -Descending
```

### <mark style="color:yellow;">Tuning and Capacity Rules of Thumb</mark>

| 🔸Link Speed          | 🔸Recommended Interval | 🔸Compression Benefit  |
| --------------------- | ---------------------- | ---------------------- |
| ≥ 100 Mb /s           | 15 minutes             | Minimal                |
| 10-100 Mb /s          | 30 minutes             | 2-3x's size reduction  |
| < 10 Mb /s or metered | 60-180 minutes         | 5-10x's size reduction |

* **Maximum Practical latency:** 500 MS _**RTT (Round Trip Time)**_ before RPC timeouts start to pile up (hard-coded in RPC runtime).
* Satellite links should use SMTP transport or deploy a _**Read-Only Domain Controller (RODC)**_.

### <mark style="color:yellow;">Security Considerations That Byte</mark>

* Replication traffic is signed by Kerberos, but not encrypted by default for IS. In the registry, set `HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\LDAPServerIntegrity = 2` and `Replicator encryption = 1` to force Kerberos sealing.
* Inter-site encryption is automatic when you use IPSec transport rules or VPN tunnels; RPC-level encryption is still optional unless you set \``RPC_C_AUTHN_LEVEL_PKT_PRIVACY`.
* RODCs pull from a single "replication partner" (a writable DC) that you define; be sure that partner is not across a high-cost link or the RODC will remain empty.
* A rogue DC can inject Data if it possesses the `krbtgt` hash for which then a Golden Ticket attack can be performed; monitor for Event ID `1966` (replication from an unknown DC).

### <mark style="color:yellow;">Troubleshooting Cheatsheet</mark>

<h4 align="center"><mark style="color:blue;">Symptom → Likely (Root) Cause → Fix</mark></h4>

* _"Replication postponed because of pending shutdown"_ → partner rebooting → wait or force with `repadmin/syncall /AdeP`
* _"Access denied"_ → SPN missing for RPC → `setspn -L <DC>$` verify `E3514235-4B06-11D1-AB04-00C04GC2DCD2/<NTDS GUID>/<DNS name>`
* _"Compression ratio 1.0"_ → object < 32 kB or already compressed (JPEG, PKCS) → normal
* _"ISTG quarantined"_ → cyclic site-link costs → run `repadmin /istg` and lower cost on one link.

### <mark style="color:yellow;">Bottom Line</mark>

Intra-site replication is tuned for speed and assumes you have infinite bandwidth; on the other hand, inter-site replication is tuned for cost and assumes you have almost none. Mis-align one timer or firewall rule and a single password change can take hours to reach a remote site - or worse, an attacker can poison a lagging DC and have that change rolled back by collision resolution. Treat site topology as live network documentation: update subnet objects when you spin up a new VLAN, measure compression ratios monthly, and let the KCC regenerate instead of hand-crafting every connection.
