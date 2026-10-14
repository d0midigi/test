# Information Gathering

## <mark style="color:yellow;">Information Gathering</mark>

### 🔸Passive Reconnaissance <a href="#passive-reconnaissance" id="passive-reconnaissance"></a>

🔸**Physical** engagement / **Social** engineering

* **Location** information, such as:
  * satellite images
  * drone recon
  * building layout (badge readers, security, fencing, etc)
* **Job** information
  * employees (name, job title, phone number, etc)
  * pictures (badge photos, desk photos, computer photos, etc)

#### 🔸Web / Host Assessment

* Target Validation
  * `whois`, `nslookup`, `dnsrecon`
* Finding Subdomains:
  * Google, `dig`, `nmap`, `crt.sh`, etc
* Fingerprinting:
  * `nmap`, `wappalyzer`, `netcat`, etc
* Data Breaches:
  * [HaveIBeenPwned](https://haveibeenpwned.com/), Breach-Parse, WeLeakInfo

#### 🔸Target <a href="#target" id="target"></a>

> ❗ Always refer to a Bug Bounty program to find valid targets that can be legally tested
>
> 🔗 [Bugcrowd](https://bugcrowd.com/engagements)
>
> * 🧪 `e.g.` - [Tesla](https://bugcrowd.com/tesla)

* Read the **program details**, follow the terms and stay in scope
* Following test will be made on the `*.tesla.com` target

***

### <mark style="color:yellow;">Discovering Email Addresses</mark> <a href="#discovering-email-addresses" id="discovering-email-addresses"></a>

* The goal is discovering public email addresses and check if they really exist

#### 🔸**Tool:️** [Hunter.io](https://hunter.io/domain-search) (free registration)

Find email addresses from any company name or website

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-c52fa1c230971ebc3fd4d736befeebe8c23b8ba2%252F2024-07-02_20-03-06_537.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=85393e4d&#x26;sv=2" alt=""><figcaption><p>hunter.io</p></figcaption></figure>

* [Phonebook.cz](https://phonebook.cz/) (free registration) - Phonebook lists all domains, email addresses, or URLs for the given input domain
* [VoilaNorbert](https://www.voilanorbert.com/)
* [Clearbit Connect](https://clearbit.com/resources/tools/connect) (Chrome extension)
* [EmailHippo Email address verifiy](https://tools.emailhippo.com/) - Free email address verification tool
* [Email-checker](https://email-checker.net/)

***

### <mark style="color:yellow;">Breached Credentials</mark> <a href="#breached-credentials" id="breached-credentials"></a>

* [HaveIBeenPwned](https://haveibeenpwned.com/) - Check if your email address is in a data breach
* [breach-parse](https://github.com/hmaverickadams/breach-parse) - A tool for parsing breached passwords
* `BreachCompilation` password list (44 GB) file comes from breached password dumps

```
breach-parse @tesla.com tesla.txt "~/Downloads/BreachCompilation/data"
```

**Credential stuffing** and **Password spraying** can be done using the results.

#### 🔸Tool: DeHashed.com

* [DeHashed.com](https://dehashed.com/) (subscription) - public data search-engine
* Hashed passwords or other data can be found
* Collect all the data (email, username, IP, address, etc) with the goal to find patterns, that could be related to personal accounts too
* Investigation to tie the data to other accounts, etc
* Use tools to try to decrypt the hashed password, like [Hashes.com](https://hashes.com/en/decrypt/hash), Google, etc

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-b50302160b1ab39adc4c8e402dc00fe063b10099%252F2024-07-02_20-30-23_539.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=afc33560&#x26;sv=2" alt=""><figcaption><p>dehashed.com</p></figcaption></figure>

***

### <mark style="color:yellow;">Hunting for Subdomains</mark> <a href="#hunting-subdomains" id="hunting-subdomains"></a>

Identify subdomains

#### 🔸Tool: Sublist3r

* [Sublist3r](https://github.com/aboul3la/Sublist3r) (outdated) - enumerate subdomains of websites using OSINT

```
sudo apt install sublist3r
```

```
sublist3r -d tesla.com

sublist3r -d tesla.com -t 100 -v
```

#### 🔸Tool: crt.sh

* [crt.sh](https://crt.sh/) - look for registered certificates and find subdomains or sub-subdomains

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-7dc7300324651e8e80f101fef4c0df2dcb0dbe59%252F2024-07-02_23-58-39_542.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7672579a&#x26;sv=2" alt=""><figcaption><p>crt.sh</p></figcaption></figure>

#### 🔸Tool: Amass

* [Amass](https://github.com/owasp-amass/amass) - in-depth attack surface mapping and asset discovery

```
sudo apt install amass
```

```
amass enum -d tesla.com

amass enum -d syselement.com
```

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-c54d87b22b18bd233242ce0e0cc1b22337e14c1f%252F2024-07-03_00-09-39_543.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=342d16bb&#x26;sv=2" alt=""><figcaption><p>amass enum -d tesla.com</p></figcaption></figure>

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-faf55a34c671a9919edaaa0976af5c72fe544103%252F2024-07-03_00-12-42_544.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1129e58a&#x26;sv=2" alt=""><figcaption><p>amass enum -d syselement.com</p></figcaption></figure>

#### 🔸Tool: httprobe

* [httprobe](https://github.com/tomnomnom/httprobe) - take a list of domains and probe for working (alive) http and https servers

```
# Go is necessary (installed via pimpmykali.sh)
go install github.com/tomnomnom/httprobe@latest

# or on Kali
sudo apt install httprobe
```

```
cat tesla.com/recon/final.txt | httprobe

# Skip default probes, and use only https:443 probe
cat tesla.com/recon/final.txt | httprobe -s -p https:443

# Strip only subdomains from the list
cat tesla.com/recon/final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443'
```

#### 🔸Tool: assetfinder

* [assetfinder](https://github.com/tomnomnom/assetfinder) - find domains and subdomains related to a given domain

```
# Go is necessary (installed via pimpmykali.sh)
go get -u github.com/tomnomnom/assetfinder

# or on Kali
sudo apt install assetfinder
```

```
assetfinder syselement.com

assetfinder --subs-only tesla.com
```

***

### <mark style="color:yellow;">Screenshotting Websites</mark> <a href="#screenshotting-websites" id="screenshotting-websites"></a>

#### 🔸Tool: gowitness

* [gowitness](https://github.com/sensepost/gowitness) - A Golang, web screenshot utility using Chrome Headless

```
# Go is necessary (installed via pimpmykali.sh)
go install github.com/sensepost/gowitness@latest

# or on Kali
sudo apt install gowitness
```

```
gowitness scan single --url "https://tesla.com" --write-db

gowitness scan single --url "https://blog.syselement.com"
```

***

### <mark style="color:yellow;">Website Technologies</mark> <a href="#website-technologies" id="website-technologies"></a>

#### 🔸Tool: BuiltWith.com

* [BuiltWith.com](https://builtwith.com/) - find out what websites are built with:

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-f22c0f1464c61932ce859347e7a1ba69f2822556%252F2024-07-03_19-54-58_561.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a8918ceb&#x26;sv=2" alt=""><figcaption><p>builtwith.com</p></figcaption></figure>

#### 🔸Tool: Wappalyzer.com

* [Wappalyzer.com](https://www.wappalyzer.com/) - via browser extension
* By visiting the webpage, interact with the browser extension to check the website technologies

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-e5a0c166600c6881803d3c79de5f3ae6b124ac57%252F2024-07-03_20-14-16_570.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a63162c7&#x26;sv=2" alt=""><figcaption></figcaption></figure>

#### 🔸Tool: WhatWeb

* [WhatWeb](https://github.com/urbanadventurer/WhatWeb/)

```
whatweb https://blog.syselement.com/
```

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-faedfe47708d38bedc7a74c6a20a5bb3c1e4d513%252F2024-07-03_20-17-06_571.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c8ba00c4&#x26;sv=2" alt=""><figcaption></figcaption></figure>

***

### <mark style="color:yellow;">Automated Recon Script</mark> <a href="#automated-recon-script" id="automated-recon-script"></a>

* Little `bash` script for sub-domains hunting

```
#!/bin/bash

url=$1

if [ ! -d "$url" ]; then
	mkdir $url
fi

if [ ! -d "$url/recon" ]; then
	mkdir $url/recon
fi

# Assetfinder #
echo "[+] Harvesting subdomains with assetfinder..."
assetfinder $url >> $url/recon/assets.txt
# get only subdomains containing $url
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt

# Amass #
# echo "[+] Harvesting subdomains with amass..."
# amass enum -d $url >> $url/recon/f.txt
# sort -u $url/recon/f.txt >> $url/recon/final.txt
# rm $url/recon/f.txt

# httprobe #
echo "[+] Probing for alive domains..."
cat $url/recon/final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> $url/recon/alive.txt

###
```

#### 🔸Tool: sumrecon

* [sumrecon](https://github.com/Gr1mmie/sumrecon/blob/master/sumrecon.sh) - web recon script

```
wget https://raw.githubusercontent.com/Gr1mmie/sumrecon/refs/heads/master/sumrecon.sh
```

* Modified final script
  * **Creates a directory structure** for reconnaissance under a given URL
  * **Harvests subdomains** using `assetfinder`
  * **Filters valid subdomains** and saves them to `final.txt`
  * **Checks for live domains** using `httprobe`
  * **Identifies potential subdomain takeovers** using `subjack`
  * **Scans for open ports** using `nmap`
  * **Scrapes archived URLs** from `waybackurls`
  * **Extracts parameters** from Wayback Machine data
  * **Categorizes JavaScript, PHP, JSON, JSP, and ASPX files** from Wayback Machine data
  * **Removes temporary files** to keep the structure clean
  * (Commented out) **Could run `amass` for subdomain discovery** and **use `EyeWitness` for screenshots**

```
# 0. Requirements
sudo apt install amass assetfinder httprobe gowitness nmap subjack
go install github.com/tomnomnom/waybackurls@latest

# 1. Copy the code here https://pastebin.com/raw/MhE6zXVt to a new file

# 2. Fix last 2 lines with gowitness and uncomment them
# echo "[+] Running eyewitness against all compiled domains..."
# gowitness scan file -f $url/recon/httprobe/alive.txt

chmod +x finalrecon.sh
./finalrecon.sh syselement.com
```

> * Check those additional resources
>   * The Bug Hunter's Methodology - [The Bug Hunter's Methodology Full 2-hour Training by Jason Haddix](https://www.youtube.com/watch?v=uKWu6yhnhbQ)
>   * [Nahamsec Recon Playlist](https://www.youtube.com/watch?v=MIujSpuDtFY\&list=PLKAaMVNxvLmAkqBkzFaOxqs3L66z2n8LA)

***

### <mark style="color:yellow;">Using Burp Suite</mark> <a href="#using-burpsuite" id="using-burpsuite"></a>

#### 🔸Tool: Burp Suite

* [Burp Suite](https://portswigger.net/burp/communitydownload)

<figure><img src="https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-318e3ae308ba934e7cb560e1daa9fab4cf3f9429%252F2024-07-03_20-25-14_572.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d11049eb&#x26;sv=2" alt=""><figcaption></figcaption></figure>

***

### <mark style="color:yellow;">Google Fu</mark> <a href="#google-fu" id="google-fu"></a>

#### 🔸Tool: Google Fu

* [Google.com](https://www.google.com/)
* [Google Search Syntax](https://www.google.com/search?client=firefox-b-e\&q=google+search+syntax)
* [Google Search Operators: The Complete List (44 Advanced Operators)](https://ahrefs.com/blog/google-advanced-search-operators/)

```
site:tesla.com filetype:pdf
```

***

### <mark style="color:yellow;">Social Media</mark> <a href="#social-media" id="social-media"></a>

* [LinkedIn](https://www.linkedin.com/), [Twitter (X)](https://x.com/) or other public websites can be used for some social media OSINT (Open-Source Intelligence).
