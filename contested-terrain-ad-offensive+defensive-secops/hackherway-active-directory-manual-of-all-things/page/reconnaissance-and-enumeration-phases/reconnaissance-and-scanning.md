# Reconnaissance and Scanning

Reconnaissance and Scanning

This chapter covers the following objectives:

* Reconnaissance types
* Scanning techniques
* Scanning tools
* Evasion techniques

One of the fundamental tasks with ethical hacking and penetration testing is gathering information about the target; this is called _**reconnaissance.**_ A successful penetration test depends on having information about the target site. Scanning tools and techniques are critical to conducting a successful penetration test.

In this section, we discuss various scanning techniques and tools. We also discuss specific terminology and methodology. There are alternative terms for reconnaissance and one such term that is used is _**footprinting.**_

In addition, there are many ways to conduct reconnaissance, or footprinting. There are two main types of footprinting: active and passive. _**Passive footprinting**_ involves gathering information about your target without any direct interaction with the target systems, personnel, or network. _**Active footprinting**_ requires some level of human-to-human interaction with the target systems such as social engineering for a phishing campaign, or piggybacking user’s to enter a building without badge credentials.

**Passive Reconnaissance Techniques**

Passive reconnaissance techniques allow you to gather a plethora of information from websites and publicly accessible information and intelligence without any interaction with the website. The target doesn’t actually know you are gathering information. This is usually the first step in the ethical hacking process: gathering as much information about the target as you can before moving ahead in the Cyber Kill Chain (CKC). There are a wide range of tools and techniques to facilitate this process, many of them open-source, and free.

Google Dorking/Google Hacking

One passive footprinting technique is using Google searches, often referred to as _Dorking, Google Dorks,_ or _Google Hacking._ You can do quite a bit with a Google search. This is a list of commonly used Google hacking techniques:

* **\[cache:]:** Displays the webpages stored in Google cache. For example, the Google cache of my page can be retrieved with _cache:mindhackdiva.tech._
* **\[link:]:** Lists webpages that have links to the specified webpage.
* **\[related:]:** Lists webpages that are similar to a specified webpage.
* **\[info:]:** Presents some information that Google has about a particular webpage.
* **\[site:]:** Presents results only for websites in the given domain. For example, to search my website for the word _cryptography,_ you would use _cryptography site:mindhackdiva.tech._
* **\[allintitle:]:** Presents results only for websites with all of the search keywords in the title.
* **\[intitle:]:** Restricts the results to documents containing the search keyword in the title.
* **\[allinurl:]:** Restricts the results to those with all of the search keywords in the URL.
* **\[inurl:]:** Restricts the results to documents containing the search keyword in the URL.
* **\[location:]:** Finds information for a specific location.
* **\[filetype:]:** Finds results that are a specific file type. For example, if you want hacking but only PDF results, you can use _hacking filetype:pdf._

Figure 1.1 shows an example in which _inurl:view/index.shtml_ has been entered in Google. The results are links to pages with web cameras.

![A screenshot of a webcam

Description automatically generated](<../../.gitbook/assets/0 (68).png>)\
FIGURE 1: Google dork search.

In this example, the search string tells Google to find any webpages that have the text _view/index.shtml_ in the URL of the website. This URL denotes a control interface for a web camera. You can use this technique to find any number of things on websites. A few examples of some Google dorks that you may find useful are listed in Table 1.1.

**TABLE 1.1 Google Hacking Examples**

| **Search String**                                                   | **Explanation**                                   |
| ------------------------------------------------------------------- | ------------------------------------------------- |
| _Inurl:/voice/advanced/ intitle:Linksys SPA configuration_          | Finds pages containing login portals.             |
| _Intitle:”Login Page” intext:”Phone Adapter Configuration Utility”_ | Finds the Linksys VoIP router configuration page. |
| _Allintext:username filetype:log_                                   | Finds logs with usernames in them.                |
| _Filetype:xls inurl:”email.xls”_                                    | Finds email lists.                                |
| _Intitle:”index of” inurl:/backup_                                  | Searches for backup directories.                  |

You can use Google Advanced Search, shown below in Figure 1.2, to search using these strings and more.

![A screenshot of a search engine

Description automatically generated](<../../.gitbook/assets/1 (52).png>)

FIGURE 1.2: Google Advanced Search.

Google Advanced Image Search works much like Google Advanced Search, but it allows you to search for images rather than terms.

There is an exploit database called the Google Hacking Database (GHDB) at _https://exploit-db.com/google-hacking-database._ This is a good place to find vulnerabilities. You can search for specific operating systems, software, and more. This website is shown below in Figure 1.3.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/2 (45).png>)

FIGURE 1.3: Google Hacking Database

These are a few of the internet resources that provide even more details on Google hacking:

* _https://resources.infosecinstitute.com/topic/google-hacking-overview/_
* _https://www.blackhat.com/presentations/bh-europe-05/BH\_EU\_05-Long.pdf_
* _https://www.sans.org/posters/google-hacking-and-defense-cheat-sheet/_

**Geographic Searches**

Many online maps can help you find the geographic location of a given target. A few of them are listed here:

* **Google Maps:** https://maps.google.com
* **National Geographic Maps:** http://maps.nationalgeographic.com
* **Bing Maps:** https://www.bing.com/maps
* **Wikimapia:** http://www.wikimapia.org

**Data Gathering**

For reconnaissance, footprinting, and information gathering activities to be successful you need to know that people searches are part of the passive footprinting process. For example, after you find out the name of a company’s CISO (Chief Information Security Officer), you might want to try and find out more about that person through various websites and social media platforms. Here are a few of the sites you might use:

* **Intelius:** https://www.intelius.com
* **BeenVerified:** https://www.beenverified.com
* **Facebook:** https://www.facebook.com
* **Twitter:** https://www.twitter.com
* **LinkedIn:** https://www.linkedin.com

There are also tools that will help you to gather information from some social media sites. The tool **InSpy** is a shell utility you can use with Linux. InSpy has two modes. The first mode, TechSpy, crawls LinkedIn job listings based on a target company. The second mode, EmpSpy, crawls LinkedIn for employees working at a company. The second mode, EmpSpy, crawls LinkedIn for employees working at a company. This tool is a Python script that can be downloaded from https://github.com/leapsecurity/InSpy. It works on Windows and macOS as well as Linux.

As an ethical hacker, you also need to know how to use a wide range of websites to gather information, including financial websites and job websites. Job websites are particularly useful. If a company is looking for a web administrator who has Apache and Debian Linux experience, you can deduce that their web server is Debian Linux running Apache.

You should also know how to use Google groups, other forums, and blogs to gather information about a target. You may find employees discussing items in the organization that can possibly provide you valuable intel. A simple example would be a network administrator complaining in a forum that he or she is having difficulty configuring the new firewall. That would strongly indicate that the firewall is quite vulnerable, and you might also be able to gather the specs of the firewall and the vendor details.

Many sites allow you to set alerts, so that after you have conducted a search, you can be alerted when anything changes. Two examples are:

* **Twitter Alerts:** [https://twitter.com/alerts](https://twitter.com/alerts)
* **Google Alerts:** [https://www.google.com/alerts](https://www.google.com/alerts)

**Useful Websites**

There are a number of websites that allow you to gather information about a target without interacting with the target. A website commonly used for passive footprinting is [https://www.netcraft.com](https://www.netcraft.com/). This site allows you to scan websites for free and now also sells a wide range of cybersecurity services. Figure 1.4 shows a scan of my own website.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/3 (33).png>)

FIGURE 1.4: Netcraft.com Scan

Another popular site for gathering information is [https://shodan.io](https://shodan.io/). This site requires you to register, but registration is free. You can then perform a wide range of services. Figure 1.5 shows the results of a search for public-facing devices with default passwords in the city of Chicago.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/4 (36).png>)

FIGURE 1.5: Shodan.io search.

There are quite a few search types you can do. Some commonly used searches are given here:

* **Search for default passwords**

_default password country:US_

*
  * _default password hostname:example.com_
  * _default password city:Plano_
* **Find Apache servers**
  * _Apache city:”San Francisco”_
* **Find Webcams**
  * _webcamxp city:Chicago_
* **Find old IIS**
  * _“iis/6.0”_

Some commonly used Shodan filters are:

* Country
* City (though it does not always work)
* Hostname
* Net (IP address range)
* Operating System
* Port

Shodan is a very versatile tool, and you should be quite familiar with it.

The site [https://censys.io](https://censys.io/) is a paid service that provides a number of search options.

Another site you should be familiar with is [https://archive.org](https://archive.org/). This site, which archives versions of websites, is known as _**The Wayback Machine.**_ The number of previous versions of a website that are archived, or indexed, depends on the popularity of the website. You will, for example, find a great many more past versions of Yahoo.com than you will of my own website. A search for [www.yahoo.com](http://www.yahoo.com/) on archive org is shown below in Figure 1.6.

![A screenshot of a web page

Description automatically generated](<../../.gitbook/assets/5 (31).png>)

FIGURE 1.6: Archive.org search.

**Metadata Tools**

It is useful to know how to be able to extract data. Whether you are working with a PDF, a Word document, or some other type of file, understanding the metadata of the file can be useful. A few metadata extraction tools are listed here:

* _**ExtractMetadata:**_ [https://www.extractmetadata.com](https://www.extractmetadata.com/)
* _**FOCA:**_ [https://github.com/ElevenPaths/FOCA](https://github.com/ElevenPaths/FOCA)
* _**PhotoME:**_ [https://www.photome.de](https://www.photome.de/)
* _**Meta Tag Analyzer:**_ [https://www.powermapper.com/products/sortsite/ads/website-meta-tags](https://www.powermapper.com/products/sortsite/ads/website-meta-tags)
* _**BuzzStream:**_ [http://tools.buzzstream.com](http://tools.buzzstream.com/)
* _**Exif Data Reader:**_ [https://www.dcode.fr/exif-data](https://www.dcode.fr/exif-data)
* _**Analyze Metadata:**_ [http://www.exadium.com](http://www.exadium.com/)
* _**Exiftool:**_ [https://sno.phy.queensu.ca](https://sno.phy.queensu.ca/)
* _**Exif Data Viewer:**_ [https://www.exifdata.com](https://www.exifdata.com/)

Along with these metadata extraction tools, there are also sites that allow you to monitor websites, indicating the following:

* _**VisualPing:**_ [https://visualping.io](https://visualping.io/)
* _**Versionista:**_ [https://versionista.com](https://versionista.com/)
* _**WatchThatPage:**_ [http://www.watchthatpage.com](http://www.watchthatpage.com/)
* _**Sken.io**_: [https://sken.io](https://sken.io/)
* _**Page Crawl**_: [https://pagecrawl.io](https://pagecrawl.io/)
* _**On Web Change**_: [https://onwebchange.com](https://onwebchange.com/)
* _**Change Tower**_: [https://changetower.com](https://changetower.com/)

**Email**

It’s important that you understand tracking information about emails. This involves using email headers as well as email tracking applications. Email headers can provide you a great deal of information. The format and content of email are actually established via a standard RFC 3864, _“Header Field Registration,”_ which describes message header field names. Common header fields for email include:

* _**To:**_ The email address and, optionally, the name of the message’s primary recipient(s).
* _**Subject:**_ A brief summary of the topic of the message.
* _**Cc:**_ Carbon copy, for sending a copy to secondary recipients.
* _**Bcc:**_ Blind carbon copy, for adding addresses to the SMTP delivery list but making them invisible to other recipients.
* _**Content-Type:**_ Information about how the message is to be displayed, usually a MIME type.
* _**Procedure:**_ Used to indicate the automated vacation or out-of-office responses should not be returned for this mail (e.g., to prevent vacation notices from being sent to all other subscribers of a mailing list). Common values are “bulk,” “junk,” and “list.”
* _**Received:**_ Tracking information generated by mail servers that have previously handled a message, in reverse order (e.g., last handler first).
* _**References:**_ Message ID of the message that this is a reply to.
* _**Reply-To:**_ Address that should be used to reply to a message.
* _**Sender:**_ Address of the actual sender acting on behalf of the author listed in From.

As an ethical hacker, you might want to send an email to someone at an organization just to get a response and examine the headers. This can tell you a lot about the organization, including its email servers. There are several websites and applications for tracking emails and checking to see if an email address is valid. A few are listed here:

* _**PoliteMail:**_ [http://www.politemail.com](http://www.politemail.com/)
* _**Yesware:**_ [http://www.yesware.com](http://www.yesware.com/)
* _**Mail Tracker:**_ [https://hunter.io/mailtracker](https://hunter.io/mailtracker)
* _**ContactMonkey:**_ [https://www.contactmonkey.com](https://www.contactmonkey.com/)
* _**Zendio:**_ [http://www.zendio.com](http://www.zendio.com/)
* _**Rocket Reach:**_ [https://rocketreach.co](https://rocketreach.co/)
* _**DidTheyReadIt:**_ [http://www.didtheyreadit.com](http://www.didtheyreadit.com/)
* _**Trace Email:**_ [http://whatismyipaddress.com](http://whatismyipaddress.com/)
* _**Email Tracker (add-on for Google Chrome):**_ [https://chrome.google.com/webstore/detail/email-tracker/](https://chrome.google.com/webstore/detail/email-tracker/)

You can look up email servers for any given domain. The following are a few websites that will facilitate this process for you:

* _**Online Domain Tools:**_ [https://mxlookup.online-domain-tools.com](https://mxlookup.online-domain-tools.com/)
* _**MX Lookup:**_ [http://www.hashemian.com/tools/domain-email.php](http://www.hashemian.com/tools/domain-email.php)

You can also check to see if an email address of a person exists:

* _**MailTester:**_ [http://mailtester.com](http://mailtester.com/)

**Open-Source Intelligence (OSINT)**

In general, the ethical hacking communities expect that you know how to attempt to get information from a wide array of resources, such as company press releases, online searchers, and regulatory reports. A few helpful websites are listed here:

* _**EDGAR:**_ [https://www.sec.gov/edgar.shtml](https://www.sec.gov/edgar.shtml)
* _**LexisNexis:**_ [https://lexisnexis.com](https://lexisnexis.com/)
* _**Bloomberg:**_ [https://www.bloomberg.com](https://www.bloomberg.com/)
* _**MarketWatch:**_ [https://www.marketwatch.com](https://www.marketwatch.com/)
* _**Alexa:**_ [https://www.alexa.com](https://www.alexa.com/)

The website [https://osintframework.com](https://osintframework.com/) is a landing page for a wide range of open-source intelligence (OSINT) websites. You can see this site below in Figure 1.7.

![A diagram of a search engine

Description automatically generated](<../../.gitbook/assets/6 (34).png>)

FIGURE 1.7: OSINT homepage.

At some point you might want to get information about who registered a certain domain name. Such a search is called a WHOIS search because the underlying protocol is called Whois. Regional Internet Registries (RIRs) store domain name registry information. WHOIS searches these, but you should know them for general knowledge.

* _**American Registry for Internet Numbers (ARIN):**_ [https://www.arin.net](https://www.arin.net/)
* _**Africa Network Information Center (AfRINIC):**_ [https://www.afrinic.net](https://www.afrinic.net/)
* _**Réseaux IP Européens Network Coordination Centre (RIPE NCC):**_ [https://www.ripe.net](https://www.ripe.net/)
* _**Latin American and Caribbean Network Information Center (LACNIC):**_ [https://www.lacnic.net](https://www.lacnic.net/)
* _**Asia Pacific Network Information Center (APNIC):**_ [https://www.apnic.net](https://www.apnic.net/)

A number of websites can facilitate Whois lookups for you. Some of them are listed here:

* _**OSINT Framework:**_ [https://osintframework.com](https://osintframework.com/)
* _**ICANN WhoIS:**_ [https://whois.icann.org](https://whois.icann.org/)
* _**WhoIS:**_ [http://cqcounter.com/whois](http://cqcounter.com/whois)
* _**Network Solutions WhoIS:**_ [https://www.networksolutions.com/whois](https://www.networksolutions.com/whois)
* _**WhoIS:**_ [https://www.whois.net](https://www.whois.net/)
* _**WhoIS:**_ [https://www.whois.com](https://www.whois.com/)
* _**WhoIS:**_ [https://who.is](https://who.is/)

Once you have an IP address, you can use a number of sites to get the geolocation of that IP address. Here are some of them:

* _**IP Location Finder:**_ [https://tools.keycdn.com/geo](https://tools.keycdn.com/geo)
* _**IP Geolocator:**_ [https://www.ipligence.com/geolocation](https://www.ipligence.com/geolocation)
* _**Neustar:**_ [https://www.home.neustar/resources/tools/ip-geolocation-lookup-tool](https://www.home.neustar/resources/tools/ip-geolocation-lookup-tool)
* _**IP Address Geographical Location Finder:**_ [https://www.ipfingerprints.com](https://www.ipfingerprints.com/)
* _**IP Location:**_ [_**https://www.iplocation.com**_](https://www.iplocation.com/)
* _**GeoIP Lookup Tool:**_ [_**https://www.ultratools.com**_](https://www.ultratools.com/)
* _**Geo IP Tool:**_ [_**https://geoiptool.com**_](https://geoiptool.com/)

Figure 1.8 shoes the use of the Neustar tool to find the geolocation of an IP address.

![](<../../.gitbook/assets/7 (30).png>)

FIGURE 1.8: Neustar Geolocation tool.

As you gather information about a target, DNS (Domain Name System) information is important. DNS maps IP addresses to domain names, and DNS contains many ercord types which you should be well-informed about including thir unique uses, how they differ, and how they operate and what they specifically do in DNS.

* **A Record:** Host (Hostname to IP address)
* **PTR (Pointer) Record:** Pointer (IP address to Hostname)
* **NS:** Name Server
* **SOA:** Start of Authority
* **SRC:** Service Locator
* **MX:** Mail Server
* **CNAME:** Canonical, or Common Name/Naming ( aliases for hosts)
* **RP:** Responsible Person
* **HINFO:** information about the host, which can include OS and CPU

Fortunately, there are a number of sites that can provide DNS information about any domain name. A few of them are listed here:

* **DNS Tools:** [https://www.mydnstools.info](https://www.mydnstools.info/)
* **DNS Lookup:** [https://mxtoolbox.com/DNSLookup.aspx](https://mxtoolbox.com/DNSLookup.aspx)
* **Online DIG:** [https://toolbox.googleapps.com/apps/dig](https://toolbox.googleapps.com/apps/dig)
* **DNS Tools:** [https://dnschecker.org/all-tools.php](https://dnschecker.org/all-tools.php)
* **Nirsoft Tools:** [http://www.nirsoft.net](http://www.nirsoft.net/)
* **DNS Watch:** [https://www.dnswatch.info](https://www.dnswatch.info/)

Figure 1.9 below shows DNS results for _mindhackdiva.net_ from [https://mxtoolbox.com/DNSLookup.aspx](https://mxtoolbox.com/DNSLookup.aspx).

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/8 (26).png>)\
FIGURE 1.9: [https://mxtoolbox.com/DNSLookup.aspx DNS results for mindhackdiva.net](https://mxtoolbox.com/DNSLookup.aspx%20DNS%20results%20for%20mindhackdiva.net) domain.

**Operating System (OS) Commands**

There are also a number of commands you need to k now if you expect to become a proficient hacker. About 90% of all attacks and defenses you will execute will be done so using a terminal, shell, or command-line interface (CLI) which means you must have a familiarity with codes, syntax, and command-line functions. Many of these commands can also aid you in troubleshooting network connectivity issues or mail routing problems. _**Traceroute**_ is a command that traces the route, or hops, from your machine to a target’s destination. The command _**tracert**_ in Windows works the same way. Figure 1.10 below shows the _**tracert**_ (Windows) command being used from my computer to mindhackdiva.net.

![](<../../.gitbook/assets/9 (25).png>)

FIGUTE 1.10: tracert results.

It probably will not surprise you that there are a number of tools that can help you trace the route to any address. Some of them even display results in very nice graphical interfaces. A few of those tools are listed here.

* _**Tialsoft Tools:**_ [http://www.tialsoft.com](http://www.tialsoft.com/)
* _**OreWare:**_ [http://www.oreware.com](http://www.oreware.com/)
* _**Ping Plotter:**_ [http://www.pingplotter.com](http://www.pingplotter.com/)
* _**Visual Route:**_ [http://www.visualroute.com](http://www.visualroute.com/)

There are also other commands you should know. The _**ping**_ command somply sends an ICMP (internet Control Management Protocol) packet to the destination. It only tells you if the destination is reachable. The difference between **ping** and **traceroute** was explained to me like this back in the day: **ping** tells you _**if**_ you can get there and **traceroute** tells you _**how**_ to get there.

You should also know the _**nslookup**_ utility like the back of your hand. You can use nslookup to attempt to gather information about any domain. It opens up a command-line interface so you can try nslookup commands on your target. Usually, if the DNS server you are attempting to query with nslookup is secure, the commands will fail.

**Hacker and Hacking Terminology**

Some terms of the industry that will help you to understand hacker and hacking terminology. A few basic terms you should know are listed here:

| **Term**                           | **Definition**                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Hacker**                         | A person who uses their technical skills to gain authorized/unauthorized access to systems or networks.                                                                                                                                                                                                                                                                                                                                  |
| **Cracker**                        | A hacker with malicious intent, often referred to as a _black hat hacker._                                                                                                                                                                                                                                                                                                                                                               |
| **White Hat Hacker**               | A hacker who uses their skills to improve security posture by finding and fixing vulnerabilities.                                                                                                                                                                                                                                                                                                                                        |
| **Black Hat Hacker**               | A hacker who exploits vulnerabilities for malicious purposes.                                                                                                                                                                                                                                                                                                                                                                            |
| **Gray Hat Hacker**                | A hacker who may violate laws or ethical standards but does not have malicious intent. Crosses somewhere between a white hat hacker and a black hat hacker.                                                                                                                                                                                                                                                                              |
| **Script Kiddie, or Skidd/Skiddz** | An inexperienced hacker, or _**noob**_, who uses pre-written scripts or tools to conduct attacks without having any educated idea of what they’re doing or how the tool works.                                                                                                                                                                                                                                                           |
| **Hacktivist**                     | A hacker who uses their skills for political or social activism.                                                                                                                                                                                                                                                                                                                                                                         |
| **State-Sponsored Hacker**         | A hacker employed by a government to conduct cyber espionage or cyber warfare.                                                                                                                                                                                                                                                                                                                                                           |
| **Cyber Terrorist**                | A hacker motivated by political or religious beliefs, targeting critical infrastructure to cause fear, anarchy, chaos, or disruption.                                                                                                                                                                                                                                                                                                    |
| **Suicide Hacker**                 | A suicide hacker is an attacker who does not care about the consequences of their actions, including getting caught or facing legal repercussions. They are willing to execute high-risk attacks, often with the intention of causing maximum damage or disruption, without concern for their own safety or anonymity. Depending on the personal or societal cause, a suicide hacker may take their own life such as suicide bombers do. |
| **Lone Wolf**                      | A lone wolf is a hacker who operates independently, without affiliation to any hacking group or organization, or state. They work alone, driven by personal motives which can range from curiosity and challenge to revenge or financial gain. These hackers typically rely on their own skills and resources to carry out attacks.                                                                                                      |
| **Penetration Testing**            | A method used by white hat hackers to test the security of a system by attempting to exploit vulnerabilities in an authorized manner.                                                                                                                                                                                                                                                                                                    |
| **Footprinting**                   | The process of gathering information about a target system or network.                                                                                                                                                                                                                                                                                                                                                                   |
| **Bug**                            | An error or flaw in software that can be exploited by hackers.                                                                                                                                                                                                                                                                                                                                                                           |
| **Patch**                          | A software update that fixes vulnerabilities or bugs.                                                                                                                                                                                                                                                                                                                                                                                    |
| **Security Breach**                | An incident where unauthorized access to data, applications, services, networks, or devices is achieved.                                                                                                                                                                                                                                                                                                                                 |
| **Data Breach**                    | An incident where sensitive, protected, or confidential data, such as PII, or PHI, is accessed, disclosed, or stolen and leaked.                                                                                                                                                                                                                                                                                                         |
| **Insider Threat**                 | A security risk that originates from within the organizations, typically involving disgruntled employees or contractors.                                                                                                                                                                                                                                                                                                                 |
| **Phreaking**                      | Hacking into telecommunications systems, especially to make free long distance calls.                                                                                                                                                                                                                                                                                                                                                    |
| **Dumpster Diving**                | Searching through physical waste receptacles to find sensitive information that can be used in an attack.                                                                                                                                                                                                                                                                                                                                |
| **Eavesdropping**                  | Intercepting private communications, such as phone calls or data transmissions. Phone call interception is most commonly referred to as _**wiretapping.**_                                                                                                                                                                                                                                                                               |
| **Tailgating**                     | Gaining physical access to a secure area by following closely behind someone with authorized access.                                                                                                                                                                                                                                                                                                                                     |
| **Piggybacking**                   | Similar to tailgating but involves gaining entry with the knowledge and consent of the authorized person.                                                                                                                                                                                                                                                                                                                                |
| **Wardriving**                     | Searching for WiFi networks by driving around with a laptop or smartphone.                                                                                                                                                                                                                                                                                                                                                               |
| **Warchalking**                    | Drawing symbols in public places to indicate the presence and status of WiFi networks.                                                                                                                                                                                                                                                                                                                                                   |

**Other Tools**

There are many tools to aid you in all phases of ethical hacking. You should note that tools are a big part of your job as an ethical hacker. Not only should you memorize the names of tools and what they are used for, but you should use as many of them as you can. Many of these tools can be downloaded for free. And some of them come with Kali Linux, which is a Linux distribution that comes with a number of hacking and forensics tools already installed and is available as a free download. For any ethical hacker, having Kali Linux is a must. Kali is full of many penetration testing and ethical hacking tools, including the infamous Metasploit, which you will use in later chapters.

**Cram Quiz**

Answer these questions. The answers follow the last question. If you cannot answer these questions correctly, consider reading this section again until you can.

1. Which of the following Google search strings will find documents in the URL that contains the keyword given?
2. **inurl**
3. **allinurl**
4. **intitle**
5. **inname**
6. Which of the following modes for InSpy specifically searches for employees of a company on LinkedIn?
7. TechSpy
8. LinkSpy
9. EmpSpy
10. CompSpy
11. You have been asked to perform a penetration test on a company. You have only been given the company domain name and gateway IP address. What type of test is this?
12. Clear box
13. Glass box
14. White box
15. Black box
16. Clarence is performing an Nmap scan of a database server, using nmap -sR -oX T3 192.168.1.19. What is this scan?
17. Nothing; it is not valid
18. An RPC scan with normal speed and XML output
19. An RPC scan with aggressive speed and no output
20. A TCP scan with normal speed and null flags
21. What is the TCP window size for Windows 10?
22. 5840
23. 4128
24. 16384
25. 65535
26. Jerrod is running a v3 scan on a target machine. He wants to send TCP SYN packets every 3 seconds on port 445 on host 10.10.10.15. Which command will do that?
27. hping3 -i 3 10.10.10.15 -sS -V -p 445
28. hping3 10.10.10.15 -sS -V -p 445 -i 3
29. hping3 10.10.10.15 -S -V -p 445 -i 3
30. hping3 -i 3 10.10.10.15 -S -V -p 445 -i 3

**Answers**

1. **A.** The command **inurl** seeks out the given keyword anywhere in the URL. **allinurl** and **intitle** are commands that perform different types of searches. **inname** is not a real Google string.
2. **C.** The **EmpSpy** module of the InSpy tool searches for employees of a specified organization on LinkedIn.
3. **D.** A test in which the tester is given only the public-facing IP address and/or domain name is a black box test.
4. **B. -sR** is an RPC scan, **-T3** is normal speed, and **-oX** is XML output.
5. **D.** 65535 is the window size for Windows 10 and FreeBSD. 5840 is the window size for Linux kernel 2.4 and 2.6. 4128 is the window size for Cisco routers running IOS 12.4. 16384 is the window size for OpenBSD.
6. **C.** The structure of **hping** is always the target first, then the scan type, then other flags (in this case **-V** is verbose output), then port, and then interval.

**Active Reconnaissance Techniques**

Active scanning involves actually interacting with the target network. This means there is a chance of the target network detecting your scanning activities. To perform scanning on a target or network you must know and understand how TCP communications function. The discussion that follows is about TCP packets, not UDP packets. UDP (User Datagram Protocol) doesn’t confirm the receipt of each packet, so these packets behave a bit differently from TCP packets.

A network packet has at least three headers:

* TCP (Transmission Control Protocol)
* IP (Internet Protocol)
* Ethernet

Each of these headers contains different information that can be useful. For example, the IP header contains the source and destination IP addresses. There are also a number of TCP flags that define how each specific part of a packet should work.

* **SYN = 2: Synchronized.** This is a request to synchronize the sender and receiver.
* **RST = 4.** **Reset.** This is used when communications need to be reset.
* **PSH = 8.** **Push.** This indicates to push the communications forward.
* **ACK = 16.** **Acknowledgement.** All packets after the initial SYN packet sent by the client should have this flag set.
* **URG = 32.** **Urgent.** This marks the packet as urgent.
* **ECE = 64.** **ECN-Echo.** This indicates things about the sender. If the SYN flag is set, the TCP peer is ECN capable.
* **CWR = 128.** **Congestion Windows Reduced (CWR).** This flag is set by the sending host to indicate that it received a TCP segment with the ECE flag set and had responded in the congestion control mechanism.

A typical connection begins with the machine requesting a connection sending a packet with the SYN flag set. The target machine responds with the SYN and ACK flags set. Then the sender sends back the ACK flag. This is called the _**TCP Three-Way Handshake.**_ When communications are over, the side ending the communications chain sends a packet with the FIN flag, the other side sends an ACK and then a FIN, and the machine that requested the termination sends another ACK flag back.

Many scanning tools work by sending an unexpected flag. For example, a tool may send the FIN flag when there is no connection. Different systems respond to this flag in different ways. The FIN flag allows the scanning tool to make guesses about the target system and gain information about the target. Another technique is called the _**XMAS scan**_ because several flags are turned on – like lights on a Christmas tree. The _**null scan**_ has all flags turned off. Again, the goal is to send unexpected packets to the destination and see what sort of response comes back.

Another type of scan that is sometimes used is known as the _**IDLE scan,**_ sometimes called the _**IPID header scan.**_ An IP packet has an IPID (IP identification) number. Operating systems increase the IPID number for each packet sent. The IDLE scan uses an idle machine (thus the name), also called a zombie machine, to help scan the target. The IDLE scan works like this:

1. You send a SYN + ACK packet to the zombie machine to probe its IPID number.
2. That machine is not expecting a SYN + ACK packet, as there was no preceding SYN, so it sends an RST packet. The RST packet contains the current IPID number.
3. You send a SYN packet to the target machine, spoofing the IP address of the zombie machine.
4. If the port is open, the target sends a SYN + ACK packet to the zombie machine. In response, the zombie sends an RST to the target.
5. If the port is closed, the target sends an RST to the zombie, but the zombie does not send anything back.
6. You probe the zombie IPID number again. An IPID increased by 2 indicates an open port, whereas an IPID increased by 1 indicates a closed port.

The idea is to perform a port scan of the target, but the target’s logs will contain only the IP address of the zombie machine.

**Note: The FIN, SYN, ACK, and RST flags are most often used by scanning tools, so you should ensure that you understand these flags. Also make certain you understand the three-way handshake.**

**To be a successful hacker, you must have, at least, a basic understanding of networking knowledge. If you don’t have a working knowledge of networking, you won’t be able to fully understand the information provided by many tools. We cover a few basic facts here; however, if you feel you need more help with networking concepts and terminology, you might want to read the&#x20;**_**CompTIA Network+ N10-008 ExamCram, 6th edition,**_**&#x20;by Emmet Dulaney.**

IP version 4 (IPv4) addresses are continuing to be replaced by IP version 6 (IPv6) addresses; however, due to the many problems with deploying IPv6 in an IPv4-based network raised many problems and issues with legacy IPv4-based assets, IPv4 addresses are still quite common in 2024. An IPv4 address appears as a series of four decimal numbers, called _**octets,**_ separated by periods (for example, 162.31.44.125). Each octet must be between 0 and 255; therefore, the address 162.31.44.466 would not be a valid IP address. An IPv4 address is actually four binary numbers; it is displayed in decimal format so that humans can readily read them.

Given that an IPv4 address is 32 bits long (in binary format), there are 232 possible IPv4 addresses; that is a total of over 4.2 billion possible IP addresses. This might seem like a lot of addresses, but, as of current, we have run out of new IPv4 addresses. A number of measures have been used to expand the number of IP addresses, including private and public IP address space. Also, we now have IPv6 to address this issue.

IPv6 utilizes a 128-bit address (instead of a 32-bit address), so there is no chance of running out of IP addresses in the foreseeable future. IPv6 also utilizes a hex numbering method in order to avoid long addresses such as 132.66.34.26.64.156.143.57.1.3.7.44.122.111.201.5. An example of a hex address is as such: 3FFE:B00:800:2::C.

**SSDP Scan**

SSDP (Simple Service Discovery Protocol) enables one machine to discover the services on another machine. It allows a computer to find out which machines are running DHCP, DNS, or other services. The UPnP SSDP M-SEARCH information discovery tool is part of Metasploit that can be used to find services on other machines (see Figure 1.12). We will explore Metasploit in detail in later chapters.

![SSDP search](<../../.gitbook/assets/10 (23).png>)

FIGURE 1.12: UPnP SSDP M-SEARCH

**Nmap (Network Mapper)**

Nmap is the most popular port scanner that every hacker either knows very well or doesn’t. Nmap allows you to set a number of flags to customize a scan. For beginners, here is a list of the most common and allowable flags Nmap employs:

* **-O:** Operating system detection
* **-sP:** Ping scan
* **-sT:** TCP connect scan
* **-sS:** SYN scan
* **-sF:** FIN scan
* **-sX:** Xmas scan
* **-sN:** NULL scan
* **-sU:** UDP scan
* **-sO:** Protocol scan
* **-sA:** ACK scan
* **-sW:** Windows scan
* **-sR:** RPC scan
* **-sL:** List/DNS scan
* **-sI:** IDLE scan
* **-Po:** Don’t ping
* **-PT:** TCP ping
* **-PS:** SYN ping
* **-PI:** ICMP ping
* **-PB**: TCP and ICMP ping
* **-PM:** ICMP netmask
* **-oN:** Normal output
* **-oX:** XML output
* **-oG:** Greppable output
* **-oA:** All output
* **-T:** Timing
  * **-T0:** **Paranoid**
    * **Description:** The slowest and most stealthy setting.
    * **Use Case:** Useful for evading Intrusion Detection Systems (IDS) and firewalls.
    * **Behavior:** Sends packets at long intervals, often taking hours or days to complete a scan.

| **Advantages**                                                                                                                             | **Disadvantages**                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p> Extremely stealthy; minimizes detection by IDS and firewalls</p><p><strong>✓</strong>Ideal for environments with strict monitoring</p> | <p><strong>✗</strong> Very slow; can take hours or days to complete a scan.</p><p><strong>✗</strong> Not practical for time-sensitive assessments</p> |

*
  * **-T1:** **Sneaky**
    * **Description:** Slightly faster than Paranoid but still very slow and cautious.
    * **Use Case:** Also used for stealth scans to avoid detection by IDS.
    * **Behavior:** Sends packets at a slow rate, but not as slow as Paranoid. Suitable for avoiding detection in environments with less stringent IDS settings.
    * **Advantages:**
    * -Extremely stealthy; minimizes detection by IDS and firewalls.
    * -Ideal for environments with strict monitoring.
    * **Disadvantages:**
    * -Very slow; can take hours or days to complete a scan.
    * -Not practical for time-sensitive assessments.
  * **-T2:** **Polite**
    * **Description:** A balance between speed and stealth.
    * **Use Case:** Useful when scanning in environments where network bandwidth is a concern, to avoid overwhelming the target.
    * **Behavior:** Slows down the scan to reduce the impact on the network and the target system.
    * **Advantages:**
    * -Balances speed and stealth; less likely to overwhelm the network.
    * -Good for environments where bandwidth is limited or sensitive.
    * **Disadvantages:**
    * \- Slower than Normal; might still take a considerable amount of time.
    * -May not evade detection by more advanced IDS setups.
  * **-T3: Normal**
    * **Description:** The default timing template.
    * **Use Case:** Suitable for most scanning activities where speed and stealth are both considered.
    * **Behavior:** Balances can speed and network load, providing reasonable performance without being overly aggressive.
  * **-T4: Aggressive**
    * **Description:** Faster than normal, but potentially more detectable.
    * **Use Case:** Suitable for when quick results are needed, and stealth is less of a concern.
    * **Behavior:** Increases scan speed and reduces timeouts, making it more likely to be detected by IDS but providing faster results.
    * **Advantages:**
    * -Default setting; balances speed and network load.
    * -Suitable for most general-purpose scans.
    * -Reasonably fast without being overly aggressive.
    * **Disadvantages:**
    * \- May not be stealthy enough for highly monitored environments.
    * \- Not the fastest option available.
  * **-T5:** Insane

\### Advantages and Disadvantages of Nmap Timing Templates

\#### -T0 (Paranoid)

\- \*\*Advantages\*\*:

\- Extremely stealthy; minimizes detection by IDS and firewalls.

\- Ideal for environments with strict monitoring.

\- \*\*Disadvantages\*\*:

\- Very slow; can take hours or days to complete a scan.

\- Not practical for time-sensitive assessments.

\#### -T1 (Sneaky)

\- \*\*Advantages\*\*:

\- Stealthy; reduces the risk of detection.

\- Slightly faster than Paranoid, making it a bit more practical for long-term scanning.

\- \*\*Disadvantages\*\*:

\- Still very slow; may take a long time to complete.

\- Not suitable for quick assessments.

\#### -T2 (Polite)

\- \*\*Advantages\*\*:

\- Balances speed and stealth; less likely to overwhelm the network.

\- Good for environments where bandwidth is limited or sensitive.

\- \*\*Disadvantages\*\*:

\- Slower than Normal; might still take a considerable amount of time.

\- May not evade detection by more advanced IDS setups.

\#### -T3 (Normal)

\- \*\*Advantages\*\*:

\- Default setting; balances speed and network load.

\- Suitable for most general-purpose scans.

\- Reasonably fast without being overly aggressive.

\- \*\*Disadvantages\*\*:

\- May not be stealthy enough for highly monitored environments.

\- Not the fastest option available.

\#### -T4 (Aggressive)

\- \*\*Advantages\*\*:

\- Faster than Normal; provides quicker results.

\- Suitable for situations where speed is more important than stealth.

\- \*\*Disadvantages\*\*:

\- More likely to be detected by IDS and firewalls.

\- Can cause noticeable load on the target network.

\#### -

\- \*\* \*\*:

\- \*\*:

| T5 (Insane)   |   |   |                                                                                                        |                                                                                                                                                                                                |
| ------------- | - | - | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Advantages    |   |   | <p>- Extremely fast; ideal for time-critical assessments.</p><p>- Can quickly scan large networks.</p> | <p>- Can overwhelm the target network, potentially causing disruptions.</p><p>Not suitable for stealth operations.</p><p>- Highly detectable; almost certain to trigger IDS and firewalls.</p> |
| Disadvantages |   |   |                                                                                                        |                                                                                                                                                                                                |
|               |   |   |                                                                                                        |                                                                                                                                                                                                |
|               |   |   |                                                                                                        |                                                                                                                                                                                                |
|               |   |   |                                                                                                        |                                                                                                                                                                                                |

\### Summary Table

\| Timing Template | Advantages | Disadvantages |

\|-----------------|------------|---------------|

\| \*\*-T0 (Paranoid)\*\* | Highly stealthy; minimizes detection | Extremely slow; impractical for quick assessments |

\| \*\*-T1 (Sneaky)\*\* | Stealthy; reduces detection risk | Very slow; not suitable for quick scans |

\| \*\*-T2 (Polite)\*\* | Balances speed and stealth; gentle on the network | Slower; may not evade advanced IDS |

\| \*\*-T3 (Normal)\*\* | Default; balances speed and network load | May not be stealthy enough for highly monitored environments |

\| \*\*-T4 (Aggressive)\*\* | Faster; provides quicker results | More detectable; can cause network load |

\| \*\*-T5 (Insane)\*\* | Extremely fast; ideal for time-critical scans | Highly detectable; can overwhelm the network |

Selecting the appropriate timing template depends on the specific requirements of your scan, including the need for stealth, the urgency of the task, and the sensitivity of the target network.

A scan that leaves the target half open is often called a _**stealth scan.**_ In such a scan, you send a SYN packet, the server responds with SYN/ACK, and the client sends an RST before the connection is complete. This is often not noted by defensive systems. The most reliable scan is a _**full open scan.**_ This means simply completing the three-way handshake and getting a full connection. The data from a full open scan is quite reliable, but it is guaranteed that your scan is at least in the logs of the target system. Scans can be done with any of the flags set, all of them set, or none of them set. There is a graphical version of Nmap, called _**Zenmap,**_ as shown in Figure 1.13.

![Zenmap](<../../.gitbook/assets/11 (19).png>)

_**FIGURE 1.13:** Zenmap tool._

While Nmap is the most commonly used scanning tool, there are other tools that are beneficial for you to know. A few of them are listed here:

* **NetScan Tools:** https://www.netscantools.com
* **hping:** http://hping.org
* **Ping Scanner Pro:** https://ping-scanner-pro.soft112.com
* **SuperScan:** https://sectools.org/tools/superscan
* **Fing:** https://www.fing.io (for mobile devices)
* **IP Scanner:** https://10base-t.com (for mobile devices)
* **Visual Ping Tester:** http://www.pingtester.net
* **NetScan Tools Pro:** https://www.netscantools.com
* **SolarWinds:** http://www.solarwinds.com

**hping**

**hping** is a versatile tool that allows you to perform a number of different scans from the command line. A few examples of hping scans are shown here:

* hping3 -1 192.168.1.25 (ICMP ping)
* hping3 -2 192.168.1.25 -p 80 (UDP scan on port 80)
* hping3 -1 192.168.1.x—rand-dest -I eth0 (scan of a subnet for live hosts)
* hping3 -8 80-200 -S 192.168.1.25 -V (SYN scan of ports 80 to 200).

Commonly used hping flags include the following:

| -v –version    | Show version                                        |
| -------------- | --------------------------------------------------- |
| -q –quite      | Quiet                                               |
| -I – Interface | Interface name                                      |
| --beep beep    | For each matching packet                            |
| -a –-spoof     | Spoof source address                                |
| -t –-ttl       | Sets the Time to Live value, which by default is 64 |
| -f –-frag      | Splits packets into fragments                       |
| -p –destpot    | Destination port                                    |
| -F             | FIN flag                                            |
| -S             | SYN flag                                            |
| -A             | ACK flag                                            |
| -R             | Reset flag                                          |
| -U             | Urgent flag                                         |
| -X             | Xmas tree                                           |

hping also lets you spoof the source IP address. For example, hping3 www.mindhackdiva.net -a 182.10.10.10 uses the spoofed IP address 182.10.10.10 to scan www.mindhackdiva.net.

**Banner Grabbing**

_**Banner Grabbing**_ involves attempting to grab a banner, usually from a web server, to learn about that server. _**Active banner grabbing**_ techniques open a TCP (or similar) connection between an origin host and a remote host. _**Passive banner grabbing**_ involves trying to derive information from error messages, network traffic, web page extensions, and similar data. One simple way to try active banner grabbing is to use Telnet:

1. Enter **telnet \<IP Address>\<Port 80>** (for example, **telnet 127.0.0.1 80**) and then press **Enter.**
2. Enter **HEAD/HTTP/1.0** and then press **Enter** twice.

**Banner Grabbing Countermeasures**

There are also several countermeasures to banner grabbing. Here are a few:

* If you are using Apache 2.x with the mod\_headers module, you can use a directive in the httpd.conf file to change banner information. For example, in the header, you can set the server to a new server name.
* With Apache, you can change the ServerSignature line to **ServerSignature Off** in the httpd.conf file.
* You can display false banners to mislead or deceive attackers.
* You can use ServerMask (https://www.iis.net/downloads/community/2009/01/servermask) tools to disable or change banner information.
* You can turn off unnecessary services on the server to limit information disclosure.

**TTL and TCP Scanning**

It is possible to identify the target operating system by examining the _**TTL (Time-to-Live)**_ and TCP window size in packets coming from a target.

In addition, it’s important to note that older configurations or a specific context where the default TCP window size was set to 8192 bytes (8 KB). Historically, earlier versions of Windows had smaller default TCP window sizes before the implementation of TCP window scaling.

Some common TTL and TCP window size values are shown in Table 1.2.

| **Operating System**       | **Time to Live** | **TCP Windows Size**                                                                         |
| -------------------------- | ---------------- | -------------------------------------------------------------------------------------------- |
| Linux (Kernel 2.4 and 2.6) | 64               | Dynamic scaling (default initial size 85.3KB can grow up to 4MB with scaling).               |
| FreeBSD                    | 64               | <p>Default size 16KB</p><p>Can grow up to 2MB with scaling</p>                               |
| Windows 10/11              | 128              | <p>Dynamic scaling (default initial size is 64KB)</p><p>Can grow up to 16MB with scaling</p> |
| macOS                      | 64               | <p>Dynamic scaling (default initial size 64KB</p><p>Can grow up to 16MB with scaling</p>     |
| iOS                        | 64               | <p>Dynamic scaling (default initial size 64KB</p><p>Can grow up to 16MB with scaling</p>     |
| Android                    | 64               | <p>Dynamic scaling (default initial size 64KB</p><p>Can grow up to 16MB with scaling</p>     |
| AIX                        | 60               | <p>Default size 16KB</p><p>Can grow up to 2MB with scaling</p>                               |
| Solaris                    | 64               | <p>Default size 128KB</p><p>Can grow up to 1MB with scaling</p>                              |
| Juniper Routers            | 64               | Configurable, generally starts at 64KB with scaling available                                |

**Note:**

* **Dynamic Scaling:** Many modern operating systems support TCP window scaling (RFC 1323), allowing the TCP window size to adjust dynamically based on network conditions.
* **TTL Values:** TTL (Time to Live) is a field in the IP header that specifies the maximum number of hops a packet can take before being discarded. It helps prevent routing loops.

The values for TTL and TCP window size can often be modified by administrators to optimize performance for specific network environments.

**TCP Window Size Evolution in Windows**

* **Older Windows versions (e.g., Windows 95/98/ME/NT):** These systems had default TCP window sizes of 8192 bytes (8 KB).
* **Windows XP and Later:** Windows started to support TCP window scaling, which allows the window size to grow dynamically based on network conditions.

**Default TCP Windows Size in Modern Windows (10/11)**

Modern versions of Windows, including Windows 10 and 11, use a dynamic window size by default, thanks to TCP window scaling (**RFC 1323**). This allows the initial window size to start at a smaller value, such as 64 KB, and increase up to several megabytes as needed to optimize throughput over high-latency networks.

**Verification**

To verify the current TCP window size settings on a Windows system, you can use the netsh command or check the registry settings.

1. **Using netsh:**
   * Open Command Prompt and elevate.
   * Run the command netsh int tcp show global

This command displays the global TCP settings, including whether auto-tuning (dynamic window scaling) is enabled.

1. **Using Registry Editor:**
   * Open the Registry Editor (Start -> Run -> regedit
   * Navigate to HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
   * Look for the TcpWindowSize entry. If it doesn’t exist, Windows uses the default dynamic settings.

**TTL and TCP Countermeasures**

It’s necessary knowledge that you understand the general countermeasures to stop TTL and TCP probes. Some basic countermeasures are listed here:

* Filter all inbound ICMP messages at the firewalls and routers.
* Configure firewall and IDS rules to detect and block probes.
* Ensure that all router, IDS, and firewall firmware is updated to the latest release/version.
* Close all unused TCP/UDP ports.
* Check logs for signs that you have been under reconnaissance (e.g., logs from a security information and event management system).

Remember that the role of an ethical hacker is to make the target organization more secure. So, understanding countermeasures is an important part of being an ethical hacker.

**Evading IDS and Firewall**

One of the skills that is critical for an ethical hacker is the ability to evade firewalls and IDS. Testing evasion techniques is an important part of a penetration test.

One way to evade firewalls and IDS/IPS is to spoof an IP address. Many scans don’t work with IP spoofing because you are looking for a response from the target. If you spoof another IP address, the response to your scan will go to the spoofed IP address.

Fragmenting packets and having them reassembled after all fragments arrive can also obfuscate what is in the packets. This can be useful in evading firewalls and IDS/IPS because fragmented packets may not be inspected thoroughly or correctly reassembled by security devices, leading to incomplete or incorrect analysis of the traffic. This allows malicious payloads to bypass detection mechanisms by hiding within the fragments until they are reassembled at the destination.

**Packet Fragmentation with Nmap**

The Nmap tool provides options for fragmenting packets, which can help evade detection by firewalls and intrusion detection/prevention systems (IDS/IPS). For example, the following command performs a SYN scan with Polite Timing, attempts to detect services, and fragments the packets:

nmap -sS -T2 -A -f 192.168.1.51

* -sS: Initiates a SYN scan
* -T2: Sets the timing template to “polite,” reducing the likelihood of detection

Nmap also allows you to use a decoy address with the -D flag. You can either generate a random number of decoy addresses or specify them. The following example shows the generation of a random number of decoy addresses:

nmap -D RND:192.168.1.51

Another evasion technique is to connect via a proxy server. A proxy server is essentially an intermediary that your connections go through. There are many such tools available. Some are free, others have a minimal cost:

* **Proxy Switcher:** httpsL//www.proxyswitcher.com
* **Proxifier:** [https://www.proxifier.com](https://www.proxifier.com/)
* **HMA:** [https://www.hidemyass.com/en-us/index](https://www.hidemyass.com/en-us/index)

Another option is to use the Tor Browser. Tor is an acronym for _**The Onion Router.**_ Onion routing essentially routes packets all around the world, bouncing them through proxy servers. Each packet is encrypted with multiple layers of encryption. Each proxy can decrypt only one layer and send the packet to the next proxy. Someone who intercepts a packet in transit between two proxies can only determine the previous proxy and the next proxy – and not the origin or destination.

Tor was originally designed, implemented, and deployed as an onion routing project of the U.S. Naval Research Laboratory, for the primary purpose of protecting government communications. Tor Browser is a free tool that allows people to use the internet anonymously. It is actually a modified Mozilla Firefox browser. Tor anonymizes the origin of your traffic.

**Cram Quiz**

Answer these questions. The answers follow the last question. If you cannot answer these questions correctly, consider reading this section again until you can.

1.Which of the following nmap commands performs a SYN scan on the target 192.168.1.10 using aggressive speed?

**A. nmap -sY -T4 192.168.1.10**

**B. nmap -sY -T5 192.168.1.10**

**C. nmap -sS -T4 192.168.1.10**

**D. nmap -sS -T5 192.168.1.10**

2\. What type of scan does hping3 www.mindhackdiva.net -a 182.10.10.10 perform?

**A.** It performs an **hping** ACK scan of the domain and IP address given.

**B.** It performs an **hping** scan of www.mindhackdiva.net, spoofing the IP address 182.10.10.10.

**C.** It performs an **hping** scan of 182.10.10.10 www.mindhackdiva.net

**D.** It doesn’t work without an IP address and a domain name.

3\. What will you accomplish by changing the ServerSignature line to **ServerSignature** **Off** in the httpd.conf file?

**A.** Turn off banner information in Apache.

**B.** Turn off banner information in IIS.

**C.** Turn off digital signatures in Apache.

**D.** Turn off digital signatures in IIS.

**Answers**

1. **C. sS** indicates the SYN scan, and **T4** indicates the aggressive speed of the scan.
2. **B.** The -a flag allows you to spoof an IP address – in this case, 182.10.10.10.
3. **A.** This command prevents most information from being revealed when someone attempts a browser grab of an Apache server.

**What Next?**

If you want more practice on this chapter’s objectives before you move on, remember that there are plenty of reputable vendors online who have free practice engines in which you can use to continue further enhancing your ethical hacking skills. The next chapter covers enumeration and network vulnerability scanning techniques in detail.
