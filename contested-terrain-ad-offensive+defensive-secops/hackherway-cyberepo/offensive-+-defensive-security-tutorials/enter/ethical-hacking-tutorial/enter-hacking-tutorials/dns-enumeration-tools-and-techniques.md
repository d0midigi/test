# DNS Enumeration Tools and Techniques

> ⚠️ **Ethical & Legal Notice**\
> This tutorial is written for **authorized penetration testers**, **red-team operators**, and **security professionals** who possess **explicit written permission** to assess the target domain.\
> Unauthorized DNS enumeration is **illegal** in most jurisdictions and violates the **Computer Fraud and Abuse Act (CFAA)** and similar laws.\
> **Never** probe domains you do **not own** and **do not have contractual approval** to test.

***

## <mark style="color:yellow;">DNS Enumeration Tools and Techniques Tutorial</mark>

> From passive OSINT to zone-transfer goldmines, with copy-paste commands for every major tool (dig, dnsenum, dnsrecon, fierce, nmap, gobuster, amass, subfinder, metasploit, iodine, dnscat2).

***

### <mark style="color:yellow;">0. Lab Target (Owned by Us)</mark>

```
Domain:  demo.red
NS:      ns1.demo.red (192.168.56.10)
         ns2.demo.red (192.168.56.11)
Range:   192.168.56.0/24
```

***

### <mark style="color:yellow;">1. Passive Reconnaissance (Zero-Packet Sent to Target)</mark>

| 🔸Source                  | 🔸Command                                                                                     | 🔸Purpose                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **crt.sh**                | `curl -s https://crt.sh/\?q\=%25.demo.red\&output\=json \| jq -r '.[].name_value' \| sort -u` | Certificate Transparency logs                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **SecurityTrails** (free) | Web UI or API                                                                                 | Historical A/AAAA/MX/NS                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **VirusTotal**            | `curl -s https://www.virustotal.com/vtapi/v2/domain/report?apikey=$VT_KEY\&domain=demo.red`   | Passive----------- The user requests a comprehensive tutorial on DNS enumeration techniques and tools. The search results provide multiple sources detailing various methods and tools for DNS enumeration. I will synthesize this information into a lengthy, detailed tutorial covering all major techniques and tools, including code snippets and examples. The tutorial will be structured to cover passive reconnaissance, active enumeration, zone transfers, subdomain discovery, reverse DNS, DNSSEC, and DNS tunneling, with practical examples using tools like dig, nslookup, dnsenum, dnsrecon, fierce, nmap, gobuster, amass, subfinder, metasploit, iodine, and dnscat2. I'll ensure to cite the sources appropriately at the end of relevant sections. |

### <mark style="color:yellow;">2. Active DNS Discovery – the “dig” Bible</mark>

(All commands = direct packets to target NS unless you @-specify another resolver)

#### 🔸2.1 Record-Types Quick-Card

| 🔸Flag | 🔸Meaning           | 🔸Use-Case                         |
| ------ | ------------------- | ---------------------------------- |
| A      | IPv4                | Web-facing hosts                   |
| AAAA   | IPv6                | Dual-stack                         |
| MX     | Mail exchanger (MX) | Phishing intel                     |
| TXT    | Text                | SPF, MS=, google-site-verification |
| CNAME  | Alias               | hidden real host                   |
| NS     | Name servers        | Zone-transfer pivot                |
| SRV    | Service location    | LDAP, Kerberos, SIP, XMPP          |
| PTR    | reverse             | Range enumeration                  |
| CAA    | Cert-Auth-Auth      | Which CA can issue                 |
| DNSKEY | public key          | DNSSEC footprint                   |
| DS     | delegation signer   | parent→child trust                 |

#### 🔸2.2 Basic Lookups (one-liners)

```bash
# ANY (now returns what resolver has cached)
dig @192.168.56.10 demo.red ANY +noall +answer

# individual types
for t in A AAAA MX TXT NS CNAME SRV CAA; do
  echo "=== $t ==="
  dig @192.168.56.10 demo.red $t +short
done
```

#### 🔸2.3 Trace Delegation from Root

```bash
dig +trace demo.red
```

Shows every referral from “.” → “red.” → “demo.red.”\
Handy to spot lame-delegation or hijack.

#### 🔸2.4 Reverse-DNS Sweep /24

```bash
for last in {1..254}; do
  dig -x 192.168.56.$last +short &
done | grep -v '^$' | sort -t . -k4,4n
```

Parallel mass-reverse:

```bash
nmap -sn -PR --dns-server 192.168.56.10 192.168.56.0/24
```

***

### <mark style="color:yellow;">3. Zone-Transfer Goldmine</mark>

#### 🔸3.1 Manual Attempt

```bash
dig @192.168.56.10 demo.red AXFR
```

Success output:

```
demo.red.           3600  IN  SOA  ns1.demo.red. admin.demo.red. 2024060101 3600 1800 604800 86400
demo.red.           3600  IN  NS   ns1.demo.red.
demo.red.           3600  IN  NS   ns2.demo.red.
demo.red.           3600  IN  A    192.168.56.20
mail.demo.red.      3600  IN  A    192.168.56.21
vpn.demo.red.       3600  IN  A    192.168.56.22
internal.demo.red.  3600  IN  A    10.10.10.5
```

> **10.10.10.5** = internal leak → pivot target.

#### 🔸3.2 Tool-Wrapped AXFR

```bash
dnsenum --axfr demo.red
dnsrecon -d demo.red -t axfr
fierce --domain demo.red --dns 192.168.56.10 --axfr
```

All save CSV/JSON for reporting.

#### 🔸3.3 AXFR Against Every NS Discovered

```bash
for ns in $(dig demo.red NS +short); do
  echo "[*] Trying AXFR against $ns"
  dig @$ns demo.red AXFR +time=3 +tries=2
done
```

🔸**Pro-tip**: Even **cloud providers** occasionally allow AXFR between secondaries → always check.

***

### <mark style="color:yellow;">4. Sub-Domain Brute-Forcing</mark>

#### 🔸4.1 Classic dig + Bash

```bash
while read sub; do
  ans=$(dig @192.168.56.10 $sub.demo.red A +short)
  [[ -n $ans ]] && echo "$sub.demo.red  ->  $ans"
done < /usr/share/seclists/Discovery/DNS/subdomains-top1mil-5000.txt
```

Parallel at lightning speed:

```bash
massdns -r resolvers.txt -t A -o S -w massdns.out subdomains-10k.txt
```

#### 🔸4.2 dnsenum Dictionary

```bash
dnsenum --dnsserver 192.168.56.10 -f /usr/share/dnsenum/dns.txt demo.red
```

Options:

```
--threads 25 --delay 200 --recursion
```

#### 🔸4.3 gobuster (also supports wildcard-busting)

```bash
gobuster dns -d demo.red -r 192.168.56.10 \
             -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100K.txt \
             -t 100 --wildcard --no-error
```

Output:

```
Found: api.demo.red
Found: staging.demo.red
Found: gitlab.demo.red
```

#### 🔸4.4 Nmap NSE Scripts

```bash
nmap -sn --script dns-brute demo.red
nmap --script dns-brute --script-args dns-brute.domain=demo.red,dns-brute.threads=10
```

#### 🔸4.5 Permutation/Alteration (Alt-DNS)

```bash
subfinder -d demo.red -o subfinder.out
cat subfinder.out | altdns -i -o permuted.out -r -s 192.168.56.10
```

Creates words like `api-staging`, `api-01`, `api-bkp`, etc.

***

### <mark style="color:yellow;">5. Certificate-Transparency (Passive) Revisited</mark>

**One-shot CLI** (no API key):

```bash
curl -s https://crt.sh/\?q\=%25.demo.red\&output\=json | \
     jq -r '.[].name_value' | \
     sed 's/\*\.//g' | sort -u > ct-subs.txt
```

Feed into brute-tool:

```bash
gobuster dns -d demo.red -r 192.168.56.10 -w ct-subs.txt
```

**SecurityTrails API** (free tier 50 queries/day):

```bash
curl -s -H "APIKEY: $ST_KEY" \
  "https://api.securitytrails.com/v1/domain/demo.red/subdomains" | \
  jq -r '.subdomains[]' | sed 's/^/www./' | sort -u > st-subs.txt
```

***

### <mark style="color:yellow;">6. Reverse-DNS (Range) Discovery</mark>

#### 🔸6.1 Dig Batch

```bash
for i in {1..254}; do
  dig -x 203.0.113.$i +short &
done | sort -u
```

#### 🔸6.2 Nmap with DNS System Resolver

```bash
nmap -sn -PR 203.0.113.0/24
```

#### 🔸6.3 dnsrecon PTR Sweep

```bash
dnsrecon -r 203.0.113.0/24 -n 192.168.56.10 -t rvl
```

Exports CSV with PTR→A pairs.

***

### <mark style="color:yellow;">7. SRV Record Mining (Active-Directory, SIP, XMPP, …)</mark>

Common query matrix:

```bash
# Global-Catalog
dig @192.168.56.10 _gc._tcp.demo.red SRV +short
# Kerberos
dig @192.168.56.10 _kerberos._tcp.demo.red SRV +short
# LDAP
dig @192.168.56.10 _ldap._tcp.demo.red SRV +short
# SIP
dig @192.168.56.10 _sip._tcp.demo.red SRV +short
```

Metasploit auxiliary:

```bash
use auxiliary/gather/dns_srv_enum
set DOMAIN demo.red
set NS 192.168.56.10
run
```

***

### <mark style="color:yellow;">8. DNSSEC Foot-Printing</mark>

#### 🔸8.1 Key Harvest

```bash
dig @192.168.56.10 demo.red DNSKEY +multi
dig @192.168.56.10 demo.red DS +multi
```

#### 🔸8.2 NSEC Walking (no NSEC3)

```bash
ldns-walk demo.red @192.168.56.10
```

Each NSEC record leaks the next valid name → full zone discovery without AXFR.

#### 🔸8.3 NSEC3 Walking (with hash)

```bash
nsec3hash.py <salt> <iterations> <name>
```

Use **nsec3map**:

```bash
nsec3map demo.red | nsec3map-print
```

Crack hashes with **hashcat** (mode 8300) if salt/iterations known.

***

### <mark style="color:yellow;">9. Wildcard Detection & Bypass</mark>

Quick test:

```bash
dig @192.168.56.10 zzqwertyuiop123.demo.red A +short
```

If returns same IP as root domain → **wildcard ON**.\
**gobuster** & **dnsrecon** auto-skip or flag; for dig scripts subtract the base-IP from results.

***

### <mark style="color:yellow;">10. Performance & Stealth Tips</mark>

* **Delay/thread jitter**: `--delay 200 –threads 5` in dnsenum.
* **Rotate resolvers**: massdns, dnsgen, or `dig +rotate` to avoid rate-limit.
* **TCP instead of UDP** (`dig +tcp`) to bypass source-port fire-walling.
* **Use multiple vantage points**: cloud shell + home ISP + VPN → detect split-horizon DNS.

***

### <mark style="color:yellow;">11. Consolidated Tool Reference</mark>

| 🔸Tool        | 🔸Typical one-liner                            | 🔸Output format |
| ------------- | ---------------------------------------------- | --------------- |
| **dig**       | `dig @8.8.8.8 demo.red AXFR`                   | raw text        |
| **dnsenum**   | `dnsenum --axfr -f sub.txt demo.red`           | XML, JSON       |
| **dnsrecon**  | `dnsrecon -d demo.red -t brt -D sub.txt`       | CSV             |
| **fierce**    | `fierce --domain demo.red --wide`              | hostname list   |
| **nmap**      | `nmap -sn --script dns-brute demo.red`         | nmap normal     |
| **gobuster**  | `gobuster dns -d demo.red -w subs.txt`         | gobust plain    |
| **amass**     | `amass enum -passive -d demo.red`              | JSON graph      |
| **subfinder** | `subfinder -d demo.red -o subs.txt`            | line-per-host   |
| **massdns**   | `massdns -r resolvers.txt -w out.mass sub.txt` | massdns         |
| **ldns-walk** | `ldns-walk demo.red`                           | zone walk       |



***

### <mark style="color:yellow;">12. Defensive Counter-Cheatsheet</mark>

1. **Disable AXFR** on public NS (allow **only** listed secondaries).
2. **Split-horizon DNS**: internal view ≠ external view.
3. **NSEC3** with **high iterations** (100-500) to slow NSEC3 walks.
4. **Rate-limit** responses (`rate-limit { responses-per-second 10; };`) – BIND 9.
5. **Monitor queries** > 5 qps per IP → auto-block (Fail2ban + BIND RPZ).
6. **Rotate** NSEC3 salt periodically → invalidates pre-computed dictionaries.
7. **Hide** in-addr.arpa zones behind VPN – prevents reverse sweeping.
8. **Use** CDN proxy (Cloudflare, Akamai) so real origin IPs not in A/AAAA records.

***

### <mark style="color:yellow;">13. TL;DR Summary</mark>

```bash
# Passive subs
curl -s "https://crt.sh/?q=%25.demo.red&output=json" | jq -r '.[].name_value' | sort -u > subs.txt

# Zone xfer
dig @ns1.demo.red demo.red AXFR

# Brute 10 k subs
gobuster dns -d demo.red -w /usr/share/seclists/Discovery/DNS/subdomains-top1mil-10000.txt -t 100

# Reverse sweep /24
for i in {1..254}; do dig -x 203.0.113.$i +short & done | sort -u

# NSEC walk (no NSEC3)
ldns-walk demo.red @ns1.demo.red
```

***

> **“The DNS is the Internet’s phonebook – abuse it and you get every number in the city.”**\
> Enumerate **legally**, document **thoroughly**, and patch **ruthlessly**.
