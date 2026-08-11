# Author Note

An Active Directory identity attack chain moves from an initial entry point to domain takeover. Attackers use credential theft, privilege escalation, and lateral movement to compromise the entire domain network.

#### Initial Access

* Phish a user via email or web links (social engineering).

<details>

<summary><strong>Technical Attack Chain for Initial Email Phishing Campaign</strong></summary>

<mark style="color:pink;">**1. Infrastructure Setup & Weaponization**</mark>\
Build delivery framework and create malicious payload or link.

* **GoPhish / Evilginx:** Setting up the phishing framework and reverse-proxy landing pages to bypass Multi-Factor Authentication (MFA).
* **MacroPack** / **Changeil**: Weaponizing Office documents, PDFs, or shortcut files (.LNK) with malicious code.
* **Namecheap** / **Cloudflare**: Registering lookalike domains (typosquatting) and hiding behind legitimate CDNs to bypass basic web filters.

<mark style="color:pink;">**2. Reconnaissance & Target Harvesting**</mark>\
Attackers gather email addresses, organizational charts, and public details about the targets.

* **theHarvester** / **Hunter.io**: Scraping public search engines, LinkedIn, and data breaches for valid corporate email addresses.
* **Sherlock**: Searching social media platforms to profile specific high-value employees (spear-phishing targets).

<mark style="color:pink;">**3. Delivery & Evasion**</mark>\
The phishing email is sent while attempting to bypass Secure Email Gateways (SEGs).

* **Swaks (Swiss Army Knife for SMTP)**: Crafting and sending raw SMTP emails with custom headers to test spam filters.
* **SpoofCheck**: Checking if the target domain lacks proper SPF, DKIM, or DMARC records, allowing email spoofing.

<mark style="color:pink;">**4. Execution & Initial Access**</mark>\
The user clicks the link or opens the file, executing the malicious code on their endpoint.

* **Cobalt Strike** / **Sliver**: Deploying a command-and-control (C2) beacon or agent onto the system via the malicious attachment.
* **Certutil** / **PowerShell**: Living-off-the-Land (LotL) binaries built into Windows, used by the payload to download the actual malware silently.

<br>

</details>

fffff

<details>

<summary></summary>



</details>

* Exploit a public-facing service or weak firewall port.
* Gain a standard, low-privileged domain user account.

#### Reconnaissance and Enumeration

* Query Active Directory using tools like BloodHound or PowerView.
* Map domain trusts, user groups, and computer objects.
* Find misconfigured permissions or exposed sensitive data.

#### Credential Theft and Access

* Dump local SAM database or LSASS memory on compromised machines.
* Perform Kerberoasting to crack service account passwords.
* Perform AS-REP Roasting on accounts with pre-authentication disabled.

#### Privilege Escalation

* Exploit weak group policies or unpatched local system flaws.
* Abuse explicit or implicit permissions to add accounts to high-privileged groups.
* Target Domain Admin or Enterprise Admin groups.

#### Lateral Movement

* Use stolen NTLM hashes or Kerberos tickets to move across machines (Pass-the-Hash / Pass-the-Ticket.
* Leverage remote management tools like WinRM, WMI, or SMB/RPC.
* Log into adjacent workstations and servers to find higher-value targets.

#### Persistence and Domain Dominance

* Create backdoors using RATs and administrator accounts.
* The Slow-and-Low Method
* Inject malicious history into `SIDHistory` attribute.
* Execute a Golden Ticket or Silver Ticket attack for long-term access.
