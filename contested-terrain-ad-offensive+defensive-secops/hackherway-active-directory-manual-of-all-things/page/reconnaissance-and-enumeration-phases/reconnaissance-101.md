# Reconnaissance 101

Reconnaissance 101

Introduction

Utilizing the hacker methodology in an engagement can help make any hacker, penetration tester, or red teamer successful. As defined in previous chapters, the hacker methodology, or hacking life cycle can be broken down broadly into six categories, which include:

1. Reconnaissance/Footprinting/Information Gathering
2. Network Scanning and Enumeration
3. Exploitation
4. Privilege Escalation
5. Maintaining Access (Persistence)
6. Cleanup and Exit Strategy

Depending on who you talk to, some may add or take away from this list to customize it for the way they do business. For example, my hacking methodology is as follows:

1. Reconnaissance/Footprinting/Information Gathering
2. Network Scanning and Enumeration
3. Initial Access (Gaining a Foothold in Target Network)
4. Attack and Exploitation
5. Maintaining Access (Persistence)
6. Post-Exploitation
7. Clean up and Exit Strategy

Doesn’t stray much from the initial one given, so it’s completely up to you to decide how your hacking methodology works for you. In this chapter, we will be discussing the first phase within the hacker methodology and the beginning phase to any well-structured, strategized, and well-organized planned attack.

You may ask yourself, _“What is considered recon?”_ or _“what is the difference between the reconnaissance phase and the network scanning and enumeration phase?”_ Well, I’ll tell you. Recon can be thought of as the passive phase of the hacker methodology. In this phase, none of the victims assets are touched except for maybe the homepage if the client or target organization even has one. Utilizing _**Open-Source Intelligence (OSINT),**_ an attacker will attempt to locate, gather, identify, and record information about their target. The recon phase can be accomplished using search engines, social media platforms, job listing sites, public registry databases, and a few handy tools.

First, let’s talk about using social media as a source of OSINT. Utilizing social media for OSINT operations is often referred to as SOCINT and social media sites are one of the most significant risks to an organization and its secrets. These sites open up numerous opportunities for information gathering due to the vast amount of useful information located in one place. From disgruntled workers leaking information to individuals bragging out of pride about the projects they are working on, if an attacker spends enough time on social media, they can build a vast picture of their target. The phrase _“loose lips sink ships”_ may seem outdated today, but still rings true in the infosec and ethical hacking realms. Another reason social media platforms such as Facebook, Twitter, Reddit, Quora, to name a few, are considered such goldmines of information to hackers is the mere lack of awareness posters have. Posting photos of vacations tells a hacker you are out of town. Posting photos of you and a family member in front of a birthday cake-most posters don’t think about the _background_ details they are also posting along with that yummy cake. Pictures of you and your friends outside bbq’ing can reveal outer details possibly exposing where you live. Hackers have mostly one thing in common and that one thing Ive observed in all my years in this industry is that we have god observation skills. We can often remember the small details, the minutia that most people seem to forget 10 minutes after having seen it. Social media help in the context of reconnaissance because while you think you are posting innocent pictures can reveal a lot more to a hacker at first glance than you could ever imagine.

In addition, social media platforms present the risk to an organization for the potential to expose various attack vectors to perform exploitative actions on a target. For example, attackers can build trust and relationships on social media platforms with employees of a target organization to perform corporate espionage or phishing attacks and campaigns. The more a user trusts someone, the more they will let their guard down. Once this trust has been established, an attacker can convince a target to open a weaponized document or malicious link to gain a foothold. Additionally, through discussions with their target, an attacker can cultivate sensitive data from the victim over time, which could be detrimental to an organization. This data could include information about the target’s network projects they are working on, username schemas (this can be used for brute-force attacks), and potential targets for phishing and spear phishing campaigns.

Another excellent source of information about an organization are public registry databases. Domain name registration databases can give an attacker a plethora of information, giving attacker some insight into your organization. Performing a search for a specific domain using one of these databases is commonly known as a WHOIS lookup.

If the registrant does not use a privacy service when registering their domain, the registrant’s contact information can provide an attacker with potential targets for a phishing campaign. These targets could include the registrant, the site’s admin, tech support, and the billing department. If an attacker successfully phishes any of these targets, it could spell disaster for an organization. In addition to the registrant’s contact information, some WHOIS databases can also provide a domain’s IP information. Suppose the victim is hosting their assets on a local server rather than the cloud. In that case, the IP information provided by a WHOIS database could give attackers a starting point for scanning and enumeration if they already didn’t have one. Now that we have discussed the potential risks of social media and WHOIS let’s discuss something more hands-on.

Google Dorking and Google Hacking

Dorking Basics

Search engines spider through webpages and archive information that organizations may not want users to see. For example, an organization may decide to store sensitive information on the same server as their web applications. If a target stores sensitive information on the same server as their web application, this could result in its discovery by a search engine spider. Once the data has been discovered and archived, anyone utilizing that search engine can find the data.

One of the best search engines for discovering spidered and indexed, or archived data is via Google. Searching Google for targeted data can be accomplished using a series of special filters. Using Google in this way is known as Google Dorks, Dorking, or Google Hacking. Simple syntax for Google Dorking would be something like site:website “searchString.” For example, if you wanted to search for the admin page of www.example.com, the syntax would be site:example.com “admin.”

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/0 (66).png>)

The above is just a simple example of a basic targeted term search. Let’s discuss more advanced search filters to perform Google Dorking. Say you wanted to find a specific file type on a webpage. If you use the search filter filetype: combined with a file extension, Google will return a list of pages containing that file type. For example, say we wanted to search for PDFs on www.example.com, the syntax for this search would be site:example.com filetype:pdf. As you can see in the image below, our search has returned 72 possible PDF files located on the website www.example.com. Using only this one filter can make things a bit difficult, especially if a website has a large number of files related to your filetype filter. What can an attacker do to refine their search?

![A screenshot of a web page

Description automatically generated](<../../.gitbook/assets/1 (50).png>)

You can use multiple filters when performing Google Dorking to refine your searches. For example, if you wanted to search for an env file containing passwords, you could use the search site.example.com allintext:password filetype:log. This search will look for occurrences of the word “password” in any log filetypes on www.example.com.

What other pieces of information can Google Dorking reveal about an organization's online assets? If you want to find sensitive directories, you could use a search such as intitle:"index of" "/home/ROOT\_PATH/". To identify server information, you could use a search such as site:example.com intitle:"Lists Web Service" or site:example.com intitle:"Directory Listing, Index of /\*/". An attacker can also use Google Dorking to find login portals with a search such as site: example.com intitle:"web client: login" or site:example.com inurl:weblogin.cgi?=1. These are just a few examples, and if you want to see more, check out the Google Hacking Database on ExploitDB at https://www.exploit-db.com/google-hacking-database. Additionally, Some examples of more filters are below.

1. allintext: Searches for occurrences of all the keywords given (allintext:"keyword")
2. intext: Searches for the occurrences of keywords all at once or one at a time (intext:"keyword")
3. inurl: Searches for a URL matching one of the keywords (inurl:"keyword")
4. allinurl: Searches for a URL matching all the keywords in the query (allinurl:"keyword")
5. intitle: Searches for occurrences of keywords in title all or one (intitle:"keyword")
6. allintitle: Searches for occurrences of keywords all at a time (allintitle:"keyword")
7. before/after: Used to search within a particular date range (filetype:pdf & (before:2000-01-01 after:2001-01-01))

**theHarvester**

The last topic we will discuss in this module is a fantastic all-in-one tool used by many attackers to help perform recon call "theHarvester". This tool is available on Kali by default; however, if you are not using Kali it can be downloaded from [https://github.com/laramies/theHarvester](https://github.com/laramies/theHarvester). This tool combines many of the techniques discussed in the previous lessons. It is also helpful for any blue team member who wants to know what an attacker can see about their organization.

One of the top benefits of using this tool is the ability to quickly query a target using a wide swath of data sources. These sources include baidu, bing, bingapi, dogpile, google, googleCSE, googleplus, google-profiles, linkedin, pgp, twitter, vhost, virustotal, threatcrowd, crtsh, netcraft, and yahoo. These sources can be queried individually or all at once to help speed up the recon phase.

The syntax for theHarvester is pretty simple "theHarvester -d targetDomain options". For example, if we wanted to perform recon on [example.com](http://example.com/) using bing the syntax would be "theharvester -d [microsoft.com](http://microsoft.com/) -b bing". Additionally, to speed up your search the -l option can limit the number of results. Some search engines such as Google can slow down your harvester searches due to their search engine database sizes. Image 2.3 demonstrates a search performed for [yahoo.com](http://yahoo.com/) and limiting the search results to 100. The search engine used for this query was Google.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/2 (43).png>)

As you can see from this search theHarvester returned two email addresses and 12 IPs/URLs. Had we expanded the search limit to something like 1000 we would have received even more data. Additionally, using different data sources for your search will provide different results. For example, in image 2.4 we performed the query "theHarvester -d funimation -l 100 -b linkedin" and were returned with a list of potential targets for a phishing campaign. As you can see theHarvester is a simple tool, but it could help you build a bigger image of a target organization and help you plan a better engagement by providing you with valuable data quickly.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/3 (32).png>)

**DNS Zone Transfer**

**Intro**

What if you want to collect information about all of the potential subdomains related to a domain? That's where DNS Zone Transfer can come in handy. A DNS Zone transfer is the act of requesting information from an improperly configured nameserver to acquire valuable information. Typically large organizations will have a primary nameserver and a secondary nameserver for backup. If the primary nameserver were to fail, the secondary would serve DNS requests in its place. If the nameservers are correctly configured, they will only serve requests of Zone transfer from other nameservers. These Zone Transfers are typically performed between nameservers, so they stay in sync. If an attacker can execute a Zone Transfer against an organization's nameserver, the hostnames will be revealed for all of their IP ranges.

Why is this dangerous? The information gained by performing a Zone Transfer gives an attacker a better picture of a victim organization's network. For example, a Zone Transfer could reveal assets an organization doesn't want the general public to know about, such as subdomains with unpatched servers. This bigger picture of an organization's network gives attackers the ability to plan better.

**Identification/Exploitation**

For this lesson, we combined the identification and exploitation sections. We did this because the identification and exploitation of a DNS Zone use the same steps. We will cover how to exploit a DNS Zone Transfer vulnerability using Dig and NSLookup. Both tools are available natively on Linux, but the only one available natively on Windows is NSLookup. For this lesson, we will use Linux to demonstrate their usage.

The first of the two tools we will cover is NSLookup, which uses the syntax "nslookup -option target". If you wanted to specify a nameserver, you would need to add it to the end of your command. This syntax for this would be "nslookup -option target nameserver". See image 3.1 for an example of us performing a basic query.

![A screen shot of a computer

Description automatically generated](<../../.gitbook/assets/4 (35).png>)

As you can see from this image, we received only one record from the query we performed. We obtain this single result because we did not specify a query type. By default, nslookup will retrieve a domain's "A record" if no query type is specified. To specify a query type, you need to add the "-query=" option to the command. Below is a list of query types you can select.

* NS: To query a given nameserver for a domains NS record
* PTR: To query for a reverse lookup (PTR record) of an IP address
* ANY: To query for ANY available records
* AXFR: To query a given nameserver for the whole zone file of a domain
* MX: To query for a mail server (MX record) of a domain

If an attacker wants to check for and exploit a DNS Zone Transfer vulnerability, the syntax "nslookup -query=AXFR [target.com](http://target.com/) nameserver" can be used. Using this command results in us receiving the entire Zone file; if we were attackers, this information could help us build a better picture of the victim organization and reveal potential actor vectors. For example, image 3.2 shows [admin.cydefe.com](http://admin.cydefe.com/) as one of the entries. This subdomain may contain a web application that, if exploited could result in a devastating compromise. See image 3.2 for the results of our command.

![A screen shot of a computer

Description automatically generated](<../../.gitbook/assets/5 (5).jpeg>)

If you wish to use Dig instead of NSLookup, the syntax is very similar, so there isn't much of a learning curve. The syntax for Dig is "dig target type," and you can specify a nameserver to query with this tool as well. The syntax for including a specific nameserver would be "dig @nameserver target type." For example, "dig @8.8.8.8 [cydefe.com](http://cydefe.com/) MX" would be the command to specify the server of 8.8.8.8 and perform a mail exchange query against the target [cydefe.com](http://cydefe.com/). See image 3.3 for an example of us performing a basic query.

![A computer screen shot of a computer

Description automatically generated](<../../.gitbook/assets/6 (33).png>)

In image 3.3, you can see we received some information regarding the IP of [www.cydefe.com](http://www.cydefe.com/) and information about the nameservers. If we want to perform a Zone Transfer with Dig, the syntax would be "dig @nameserver target AXFR." See image 2.2 for an example of this command. For this lab, we used the command "dig @172.17.0.2 [cydefe.com](http://cydefe.com/) AXFR" the nameserver of 172.17.0.2 is used because that is the IP of our VM. Please note that your nameserver IP will be different when running the VM.

![A computer screen with white text

Description automatically generated](<../../.gitbook/assets/7 (4).jpeg>)

Using Dig to perform a Zone Transfer gives the same results as using NSLookup. Images 3.3 and 3.4 demonstrate you can use either tool to get the same results. The main difference between the two is the formatting of their output. When picking which of these two tools to use, it comes down to preference and availability. Now that you know how to perform a Zone Transfer get out there and HACK THE PLANET!

**Mitigation**

To prevent a Zone Transfer to untrusted machines, you will want to set up your DNS servers ACL. Typically the ACL will be located in your server's configuration file. The ACL will look like something below and note that you will want to put your nameservers IPs in the ACL, not the example below IPs.

Copy

acl trusted-servers {

10.0.0.1; // ns1

10.0.0.2; // ns2

};

After you set your ACL, you will need to edit your Zone configuration file. Edit this file and add the line "allow-transfer { trusted-servers; };" to define what ACLs you will be using. See below for a simple example of how this file would look.

Copy

zone cydefe.com {

type master; file "zones/cydefe.com";

allow-transfer { trusted-servers; };

};

Once these edits have been made, restart your server for the changes to take effect.

**Passive Reconnaissance**

**Scope of Work Examples**

[https://bugcrowd.com/](onenote:https://d.docs.live.net/4bbcb50bcd26f81b/Documents/OSCP/Reconnaissance.one#Passive%20Reconnaissance\&section-id={5F483E01-1126-4CB9-8B6E-0B105634F5F6}\&page-id={3522D7FF-83E9-43EC-A644-64F7E3388EDC}\&object-id={5D7E8AC1-5A74-458B-B40F-0168C40456CA}&12)

**Location Information**

* Satellite Images
* Drone recon
* Building Layout (Badge readers, Break areas, Security, Fence)

**Job Information**

* Employees (Name, Job title, Phone, Manager, ...)
* Pictures (Badge photos, Desk photos, Computer photos, ...)

**Web / Host**

**Target Validation**

* WHOIS
* nslookup
* DNSRecon

**Find Subdomains**

* Google Fu
* Dig
* Nmap
* Sublist3r
* Bluto
* crt.sh

**Fingerprinting**

* Nmap
* Wappalyzer
* WhatWen
* BuiltWith
* Netcat

**Data Breach**

* HaveIBeenPwned
* Breach-Parse
* WeLeakInfo

**Email Gathering**

Use [https://hunter.io/search](https://hunter.io/search) to gather a list of valid users, as well as the **pattern**! For example:

{first}@example.com {first}.{last}@example.com

This step is very useful for creating a user list for **password spraying**.

**Gather Breached Passwords**

**Breach Parse**

[![Logo](<../../.gitbook/assets/8 (25).png>)GitHub - hmaverickadams/breach-parse: A tool for parsing breached passwordsGitHub](https://github.com/hmaverickadams/breach-parse)

Copy

./breach-parse.sh @\<domain> \<output\_file>

**TheHarvaster**

The objective of this program is to **gather emails, subdomains, hosts, employee names, open ports and banners** from different public sources like search engines, PGP key servers and SHODAN computer database.

This tool is intended to help Penetration testers in the early stages of the penetration test in order to understand the customer footprint on the Internet. It is also useful for anyone that wants to know what an attacker can see about their organization.

This is a complete rewrite of the tool with new features like:

* Time delays between request
* All sources search
* Virtual host verifier
* Active enumeration (DNS enumeration, Reverse lookups, TLD expansion)
* Integration with SHODAN computer database, to get the open ports and banners
* Save to XML and HTML
* Basic graph with stats
* New sources

Copy

usage: theHarvester \[-h] -d DOMAIN \[-l LIMIT] \[-S START] \[-g] \[-p] \[-s] \[-v]

\[-e DNS\_SERVER] \[-t DNS\_TLD] \[-n] \[-c] \[-f FILENAME]

\[-b SOURCE]

theHarvester is used to gather open source intelligence (OSINT) on a company

or domain.

optional arguments:

-h, --help show this help message and exit

-d DOMAIN, --domain DOMAIN

company name or domain to search

-l LIMIT, --limit LIMIT

limit the number of search results, default=500

-S START, --start START

start with result number X, default=0

-g, --google-dork use Google Dorks for Google search

-p, --port-scan scan the detected hosts and check for Takeovers

(21,22,80,443,8080)

-s, --shodan use Shodan to query discovered hosts

-v, --virtual-host verify host name via DNS resolution and search for

virtual hosts

-e DNS\_SERVER, --dns-server DNS\_SERVER

DNS server to use for lookup

-t DNS\_TLD, --dns-tld DNS\_TLD

perform a DNS TLD expansion discovery, default False

-n, --dns-lookup enable DNS server lookup, default False

-c, --dns-brute perform a DNS brute force on the domain

-f FILENAME, --filename FILENAME

save the results to an HTML and/or XML file

-b SOURCE, --source SOURCE

baidu, bing, bingapi, certspotter, crtsh, dnsdumpster,

dogpile, duckduckgo, github-code, google, hunter,

intelx, linkedin, linkedin\_links, netcraft, otx,

securityTrails, spyse(disabled for now), threatcrowd,

trello, twitter, vhost, virustotal, yahoo, all

**Hunting Subdomains**

**Sublist3r**

To install:

Copy

apt install sublist3r

Usage:

Copy

sublist3r -d \<domain>

**crt.sh**

Search for %.\<domain>

**OWASP Amass**

The OWASP Amass Project has developed a tool to help information security professionals perform network mapping of attack surfaces and perform external asset discovery using open source information gathering and active reconnaissance techniques. The gathering technique used:

* **DNS**: Basic enumeration, Brute forcing (optional), Reverse DNS sweeping, Subdomain name alterations/permutations, Zone transfers (optional)
* **Scraping**: Ask, Baidu, Bing, DNSDumpster, DNSTable, Dogpile, Exalead, Google, HackerOne, IPv4Info, Netcraft, PTRArchive, Riddler, SiteDossier, ViewDNS, Yahoo
* **Certificates**: Active pulls (optional), Censys, CertSpotter, Crtsh, Entrust, GoogleCT
* **APIs**: AlienVault, BinaryEdge, BufferOver, CIRCL, CommonCrawl, DNSDB, GitHub, HackerTarget, IPToASN, Mnemonic, NetworksDB, PassiveTotal, Pastebin, RADb, Robtex, SecurityTrails, ShadowServer, Shodan, Spyse (CertDB & FindSubdomains), Sublist3rAPI, TeamCymru, ThreatCrowd, Twitter, Umbrella, URLScan, VirusTotal, WhoisXML
* **Web Archives**: ArchiveIt, ArchiveToday, Arquivo, LoCArchive, OpenUKArchive, UKGovArchive, Wayback

**Tomnomnom Httpprobe**

* Use this to probe a list of domains

**Find Websites' Technology**

**Builtwith**

[https://builtwith.com/builtwith.com](https://builtwith.com/)

**Wappalyzer**

Install as a browser add-on to display the technologies on the current web

**WhatWeb**

Copy

whatweb \<website>

**Burp Suite**

Proxy, Intercept, and inspect the response

**Active Reconnaissance**

**Nmap**

**Ping Sweep**

Copy

nmap -sP 192.168.1.0/24 -oN scan-alive-hosts.txt

nmap -sP 192.168.1.1,5,100,150 -oN scan-alive-hosts.txt

**General Scans for a host**

Default script, All ports, Version + OS Discovery, TCP scan

Copy

nmap -sC -A -T4 -oN nmap-tcp-initial.txt 192.168.1.1 -p-

UDP Scan:

Copy

nmap -sU --top-ports 100 -oN nmap-udp-initial.txt 192.168.1.1

**Shellshock**

Copy

nmap \<ip> -p 80,443 --script=http-shellshock --script-args uri=/cgi-bin/xx.cgi

[![Logo](<../../.gitbook/assets/9 (24).png>)GitHub - mubix/shellshocker-pocs: Collection of Proof of Concepts and Potential Targets for #ShellShockerGitHub](https://github.com/mubix/shellshocker-pocs)

**DNS Zone Transfer**

Copy

dig @\<dns\_server> \<domain\_name> -t AXFR +nocookie

**Massscan**

[![Logo](<../../.gitbook/assets/10 (22).png>)GitHub - robertdavidgraham/masscan: TCP port scanner, spews SYN packets asynchronously, scanning entire Internet in under 5 minutes.GitHub](https://github.com/robertdavidgraham/masscan)

Build for doing large scale but fast scanning

**Metasploit Scanning Modules**

Copy

scanner/portscan

Copy

post/windows/gather/arp\_scanner RHOST=\<ip\_range>

To use a session as a route:

Copy

post/multi/manage/autoroute

**Searchsploit**

Find known exploit. Usage:

Copy

searchsploit \<keyword>

To copy the exploit script:

Copy

searchsploit \<EDB-ID> -m \<Output\_Location>
