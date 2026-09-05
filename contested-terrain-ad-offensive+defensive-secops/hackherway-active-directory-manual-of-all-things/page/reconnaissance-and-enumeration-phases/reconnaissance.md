# Reconnaissance

Reconnaissance, Information Gathering, and Footprinting

The most important part of any attack strategy is learning how to gather information about our targets _before we even try to attack them._ This chapter is all about the tools and techniques for doing just that. And for those of you who enjoy the idea of Spy vs. Spy and espionage, there is still a lot to be learned through good old-fashioned legwork and observation, even if most of it is done by virtual means.

Footprinting

Gathering information about your target is more than just a first step in the overall attack; it's an essential skill to perfect as an ethical hacker. I believe what most aspiring ethical hackers ask themselves about this particular area of our profession boils down to two questions:

1. What information am I looking for?
2. How do I get it?

Both are excellent questions, and both will be answered in this section. As always, we'll cover some of the basics in terms of definitions, terms, and knowledge you'll need before we get into the harder stuff.

You were introduced to the term _reconnaissance_ in Chapter 1, so I won't bore you with the definition here. However, I think it's important for you to understand that there may be a difference in definition between reconnaissance, _footprinting_ , and _information gathering_ , depending on which security professional you're talking to. For many professionals, recon is more of a general, overarching term for gathering information about targets, while footprinting is more of an effort to map out, at a high level, what the landscape looks like. They are interchangeable terms, but if you just remember that footprinting is part of the recon phase, you'll be fine.

During the footprinting phase, you're looking for any information that might give you some insight into the target, no matter how big or small. And the information doesn't necessarily have to be technical. Sure, things like the high-level network architecture (what routers do they use, and what servers did they buy?), the applications and Web sites (are they public-facing?), and the physical security measures in place (what kind of access control systems are the first line of defense, and what routines do employees seem to go through on a daily basis?) are great to know, but you'll probably be answering other questions first during this phase. Questions about the critical business functions, the most important intellectual property, and the most sensitive information held by this organization may well be the most important hills to climb in order to properly and diligently reconnoiter your target.

Of course, anything that provides information about the employees themselves is always great to have, because the employees are a huge target for you. Although some of this data can be a little tricky to get, most of it is relatively easy to get and is right in front of you if you just open your virtual eyes.

As far as footprinting terminology and getting your feet wet with the reconnaissance phase, most of it is fairly easy to remember. For example, while most footprinting is passive in nature, using freely available information, and designed to be blind to your target, sometimes an overly security-conscious target organization may catch on to your efforts. If you prefer to stay in the virtual shadows (and since you're reading this book, I can safely assume that you do), your footprinting efforts can be designed to obscure their source. If you're really sneaky, you might even take the next step and create ways for your efforts to be traced back to anyone and anywhere but you.

**Note: Making it appear that someone else has done something illegal is a crime in and of itself. Even if it's not criminal activity you're accusing someone of, the threat of jail time and/or a civil lawsuit should be enough to make you think twice.**

_**Anonymous footprinting**_, where you try to hide the source of all that information gathering, may be a great way to work in the shadows, but _**Pseudonymous footprinting**_ is just plain naughty, letting someone else take the blame for your actions. Passing the buck, as they call it. You don't even have to blame a real person - Keyser Soze or John Wick, for example.

There are four key principles of reconnaissance and footprinting:

* Know the security posture (footprinting helps make this clear).
* Reduce the focus area (network range, number of targets, and so on).
* Identify vulnerabilities (self-explanatory).
* Draw a network map.

Footprinting, like everything else in hacking, usually follows a fairly organized path to completion. You start with information you can gather from the "50,000-foot view"-using the target's website and web resources to gather other information about the target-and then move on to a more detailed view. Targets for gathering this type of information are numerous and can be easy or relatively difficult to crack. You can use search engines and public-facing websites for general, easy-to-get information, while digging through the Domain Name System (DNS) for detailed, network-level knowledge. It's all part of the footprint, and it's all valuable; just like an investigation in a mystery novel, no piece of evidence should be overlooked, no matter how small or seemingly insignificant.

But it's also important for you to remember what's really important and what the end goal is. Milan Kundera famously wrote in _The Unbearable Lightness of Being_ : "Seeing is limited by two boundaries: strong light, which blinds, and total darkness," and it really applies here. In the real world, the only thing more frustrating to an ethical hacker than no data is too much data. If you're on a hacking security engagement and you've defined your goals in advance, you'll know what information you want, and you'll focus your activities to get it. In other words, you won't (or shouldn't) collect data just for the sake of collecting it; you should focus your efforts on the good stuff.

There are two main ways to get the information you're looking for. I'll define active footprinting and passive footprinting here, and then spend more time breaking them down in the rest of this chapter. An _active footprinting_ effort is one that requires the attacker to touch the device, network, or resource, while _passive footprinting_ refers to efforts to gather information from publicly available sources. For example, passive footprinting could be browsing websites or looking up public records, while running a scan against an IP address you find on the network would be active footprinting. When it comes to the footprinting phase of hacking, the vast majority of your activities will be passive in nature. Think of it this way: passive footprinting is mostly considered when you're online, checking websites and looking up DNS records, and active footprinting is when you're gathering social engineering information by communicating with employees.

**Note: You're probably wondering,&#x20;**_**"What about websites designed to scan your target?"**_**&#x20;There are plenty of sites out there that will scan a target for you, and while it's actively scanning your target, it's not YOU actively scanning it.**

Passive Footprinting

Passive footprinting has nothing to do with lack of effort, and even less to do with how you do it (using a computer network or not). In fact, in many ways it takes much _more_ effort to be an effective passive footprinter than an active one. Passive footprinting is all about the publicly available information you gather, and not so much about how you get it. Some methods include gathering competitive intelligence, using search engines, browsing social media sites, participating in the ever-popular dumpster diving, obtaining network ranges, and raiding DNS for information. As you can see, some of these methods might ring a bell to anyone who's paying attention, and they don't seem very passive to common sense people anywhere, let alone in our profession. But you're going to have to get over this feeling that you have about passive versus active footprinting and just accept it for what it is.

Passive information gathering includes an information-gathering technique known as _**competitive intelligence**_, which refers to the information a company gathers about its competitors' customers, products, and marketing strategies. Most of this information is readily available and can be obtained through a variety of means. It's not only legal for companies to gather and analyze this information, its expected behavior. In the business world, you're simply not doing your job if you're not keeping up with what the competition is doing. At the same time, that same information is valuable to you as an ethical hacker, and there are more than a few ways to gain competitive intelligence.

Your company's website or home page is a great place to start. Think about it: What do people want on their company's Web site? They want to provide as much information as possible to show potential customers what they have and what they can offer. Sometimes, however, this information becomes information overload. Just some of the open source information you can gather from almost any company's Web site includes company history, directory listings, employee photos, current and future plans, and technical information. Directory listings are useful for social engineering, and you'd probably be surprised at how much technical information companies keep on their sites. Designed to reassure customers, sites sometimes inadvertently give hackers a leg up by providing details about the technical capabilities and makeup of the network.

Several websites are great sources of competitive intelligence. Information about a company's origins and how it has evolved over the years can be found in places like the Security and Exchange Commission's (SEC) Electronic Data Gathering, Analysis, and Retrieval (EDGAR) database ([https://www.sec.gov/edgar.shtml](https://www.sec.gov/edgar.shtml)), D\&B Hoovers ([https://www.hoovers.com](https://www.hoovers.com/)), LexisNexis ([https://www.lexisnexis.com](https://www.lexisnexis.com/)), and Business Wire ([https://www.businesswire.com](https://www.businesswire.com/)). If you're interested in corporate plans and financials, the following list provides some great resources:

* SEC Information ([https://www.secinfo.com](https://www.secinfo.com/))
* Experian ([https://www.experian.com](https://www.experian.com/))
* MarketWatch ([https://www.marketwatch.com](https://www.marketwatch.com/))
* The Wall Street Transcript ([https://www.twst.com](https://www.twst.com/))
* Euromonitor ([https://www.euromonitor.com](https://www.euromonitor.com/))

**Note: Other aspects of competitive intelligence that may be of interest include the company's online reputation (as well as the company's efforts to control it) and the company's actual web traffic statistics (https://www.alexa.com is a great resource for this). Also, check out https://www.google.com/finance, which shows you the company's press releases on a timeline of its stock performance - in effect, showing you when key milestones occurred.**

**Active Footprinting**

When it comes to active footprinting, we're really talking about social engineering, human interaction, and anything that requires you to interact with the organization. In short, while passive measures use publicly available information that doesn't (usually) set off alarm bells, active footprinting involves exposing your information gathering to discovery. For example, you can usually scrub through DNS records without anyone noticing, but if you were to walk up to an employee and start asking questions about the organization's infrastructure, _someone_ would notice.

**Note: Social engineering is often overlooked in many hacking cycles, but honestly, it's an extremely effective footprinting method. Books like&#x20;**_**How to Win Friends and Influence People**_**&#x20;and&#x20;**_**The Art of Conversation**_**&#x20;are fantastic social engineering resources. You'd be surprised how much you can learn about a target simply by being nice, charming, and a good listener. And if you want a couple of books that hit very close to home, some of my favorites are&#x20;**_**Social Engineering: The Science of Human Hacking**_**&#x20;and&#x20;**_**Unmasking the Social Engineer: The Human Element of Security**_**&#x20;by Chris Hadnagy.**

Social engineering has a variety of definitions, but it basically boils down to convincing people to give up sensitive information, sometimes without them even realizing it. There are millions of ways to do this, which can sometimes get really confusing. From an Active Footprinting perspective, the social engineering methods you should be concerned about involve human interaction. If you call an employee or meet them face-to-face for a conversation, you're practicing active footprinting.

This may seem easy to understand, but it can get complicated in a hurry. For example, I just told you that social media is a great way to passively uncover information, but I'm sure you're aware that you can use some of these social sites in an active way. What if you openly use Facebook connections to ask for information? Or what if you tweet a question to someone? Both of these examples could be considered active in nature, so be forewarned.

Footprinting Methods and Tools

Some books focus a lot on the tools themselves, and not so much on the definitions and terms associated with them. This is actually good news from one standpoint-these definitions and terms can get ridiculous, and memorizing the difference between one term and another doesn't really do much to demonstrate your ability as a real ethical hacker. The bad news is that you need to know countless tools and methods to be considered an effective hacker. There are many tools and techniques in footprinting that you can learn for your future pentesting and hacking endeavors.

Search Engines

Search engines can provide a treasure trove of information for footprinting and, if used properly, won't alert anyone that you're looking for information about them. Mapping and location-specific information, including drive-by pictures of the company's exterior and overhead shots, have become so commonplace that people don't think of them as footprinting opportunities; however, Google Earth, Google Maps, and Bing Maps can provide location information and, depending on when the pictures were taken, can reveal potentially interesting information. Even personal information - such as home addresses and phone numbers for employees - is often easy enough to find through the websites of companies such as LinkedIn ([www.linkedin.com](http://www.linkedin.com/)) and Pipl ([www.pipl.com](http://www.pipl.com/)).

A really cool tool along the same lines is Netcraft ([https://www.netcraft.com](https://www.netcraft.com/)). Fire it up and see what you can find. Restricted URLs, not meant for public consumption, might just show up and provide some juicy tidbits. If the site owner is really sloppy or just plain lazy, Netcraft's output can also show you the operating system (OS) on the box.

**Note: Netcraft has a pretty cool toolbar add-on for Firefox and Chrome (**[**https://www.netcraft.com/apps/browser/**](https://www.netcraft.com/apps/browser/)**).**

Another absolute goldmine of information about a potential target is job boards. Go to CareerBuilder, Monster, Dice, or any of the many others, and you'll find almost anything you want to know about the company's technical infrastructure. For example, a job listing that says "Candidate must be familiar with Windows Server 2016, Microsoft SQL Server 2015, and IIS" isn't representative of a network infrastructure that consists of Linux servers. The technical job listing will tell you exactly what's on the company's network-and often what versions. Combine that with your keen knowledge of vulnerabilities and attack vectors, and you're well on your way to a successful pentest!

**Footprinting Gone Wild**

**Imagine you're part of a pentesting team that has handled everything correctly. You’ve defined your agreement, set the scope, decided on what can and cannot be exploited, and secured all necessary legal approvals. Following the team lead's guidance, you carry out the assigned tasks, which this time involve basic passive reconnaissance. After some initial exploration, you run a web crawler like BlackWidow, GSA Email Spider, NCollector Studio, or GNU Wget to gather contact information and employee data. At the end of the day, the team convenes to review the findings and potential issues. Your team lead enters the room visibly upset. Apparently, some web application data was deleted in response to an information gathering attempt. The team turns to you: “What did I do?” Most pentest agreements include clauses that protect the team from such incidents. However, can a web spider actually cause data deletion on a poorly programmed web application? Absolutely, and you – the unsuspecting team member – would not have known about the flawed application until the crawl was initiated.**

**Could you be held accountable for pentesting mishaps? Should you be held accountable? The answer is, maybe. It hinges on whether your pentesting agreement is meticulously crafted. It should include language that covers potential unintentional consequences, such as:**

**"Due to the execution of toolsets, exploits, and techniques, there is a possibility for the unintentional deletion or modification of sensitive data in the test environment, including production-level systems."**

**This should be followed by a clause absolving your team from unintentional issues that might arise. Without this, yes, you could indeed be accountable.**

**Consider another potential pitfall: the actions your target might take in response to your activities. If a network admin panics and shuts everything down, causing significant disruptions, are you at fault? You might be, unless your agreement includes a clause like:**

**"The actions taken by the target in response to the detection of our activities are beyond our control."**

**If a client refuses to accept such clauses, it’s a red flag. Given there’s no infallible way to ensure even the most benign pentest tools and techniques won’t inadvertently alter or damage data or systems, it’s wise to reconsider engaging with that client. Remember, tools don’t care about your intentions. So, secure a robust agreement before deploying your tools.**

**It’s also critical to acknowledge the legal landscape. The Computer Fraud and Abuse Act (1986) criminalizes conspiracy to commit hacking, making it vital to have an ironclad agreement before you even start basic footprinting.**

**While we’re discussing using websites for information gathering, don’t overlook the plethora of free and legal options available. Social networking sites are treasure troves of information. LinkedIn is excellent for profiling potential targets by understanding professional relationships and history. Facebook and Twitter can also provide valuable insights, particularly if the target company recently experienced layoffs or other personnel issues. Disgruntled former employees often share revealing company information.**

**For a real-world example of social networking’s power, read about Robin Sage on Wikipedia. This case underscores how determined hackers can leverage social networking effectively.**

**Additionally, consider using alerting services offered by platforms like Google, Yahoo!, and Twitter. These services can send real-time updates via text or email about any changes related to your target, keeping you informed and ahead of the curve.**

**In summary, thorough preparation and comprehensive agreements are fundamental to mitigating risks in pentesting. Couple this with savvy use of open-source intelligence tools, and you can navigate the complex landscape of ethical hacking with greater confidence.**

**Google**

A highly effective tactic in footprinting a target emerged in late 2004, popularized by Johnny Long, a member of an IT security team. During his work in pentesting and ethical hacking, Long began to pay close attention to the search strings used in Google. The search engine includes additional operators designed to fine-tune search strings, which Long ingeniously adapted for cybersecurity purposes.

Instead of merely searching for a common webpage or an image, imagine instructing the search engine to, for example, find systems using Remote Desktop Web Connection or uncover MySQL history pages to extract passwords. Astonishingly, search engines can perform these tasks and more, a practice now known as Google Dorking, Dorking, or Google Hacking.

Google hacking involves the use of advanced search operators to manipulate search strings and uncover vulnerabilities. Below is a table that describes some of these advanced operators for Google hacking search strings:

\| Operator | Description |

\|------------------|---------------------------------------------------------------------------------|

\| \`site:\` | Limits results to pages on a specific site. |

\| \`filetype:\` | Searches for specific file types. |

\| \`intitle:\` | Finds pages with specific words in the title. |

\| \`inurl:\` | Looks for specific words in the URL. |

\| \`intext:\` | Searches for specific words in the body text. |

\| \`allinurl:\` | Similar to \`inurl:\` but searches for multiple words in the URL. |

\| \`allintitle:\` | Similar to \`intitle:\` but searches for multiple words in the title. |

For further exploration of these advanced operators, numerous websites provide comprehensive guides on crafting Google hack strings. One valuable resource is the Google Hacking Database (GHDB), which Johnny Long originally managed under Hackers for Charity and is now under the stewardship of Offensive Security. You can access it at \[exploit-db.com/google-hacking-database]\(https://www.exploit-db.com/google-hacking-database).

To see Google Dorking in action, try this search string: \`allinurl:tsweb/default.htm\`. Additionally, the \`filetype:\` operator is particularly useful, offering access to a wide array of file types. For an extensive list, visit Google's support page at \[support.google.com/webmasters/answer/35287?hl=en]\(https://support.google.com/webmasters/answer/35287?hl=en).

It's essential to recognize the potential of Google hacking in indexing and accessing source code and various types of sensitive information. By manipulating search strings with these operators, ethical hackers can uncover significant vulnerabilities, underscoring the importance of understanding and securing these weaknesses before malicious actors can exploit them.

In the realm of cybersecurity, leveraging tools like Google Dorking can provide profound insights into a target's vulnerabilities. However, this requires a responsible approach, ensuring that all activities are conducted within the bounds of legality and ethical standards. Properly applied, these techniques enhance defensive measures, offering a proactive stance against potential threats.

Integrating Google hacking into your security toolkit can significantly bolster your ability to perform thorough reconnaissance and identify vulnerabilities. Always ensure your activities are legally and ethically sound, reflecting the professionalism and integrity essential in the cybersecurity field.

Basically, you’re telling Google to go look for webpages that have TSWEB in the URL (indicating a remote access connection page) and you want to see only those that are running the default HTML page (default installs are common in a host of different areas and usually make things a lot easier for an attacker). I think you may be surprised by the results – I even saw one page where an admin had edited the text to include the logon information.

| **Operator** | **Syntax**                             | **Description**                                                                                                                                                                                                                                                                                   |
| ------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| filetype     | filetype:_type_                        | <p>Searches only for files of a specific type (DOC, XLS, and so on). For example, the following will return all Microsoft Word documents:</p><p>filetype:doc</p>                                                                                                                                  |
| index of     | index of /_string_                     | <p>Displays pages with directory browsing enabled, usually used with another operator. For example, the following will display pages that show directory listings containing <em>passwd:</em></p><p>“intitle:index of” passwd</p>                                                                 |
| info         | info:_string_                          | <p>Displays information Google stores about the page itself:</p><p>info:www.anycomp.com</p>                                                                                                                                                                                                       |
| intitle      | intitle:_string_                       | <p>Searches for pages that contain the string in the title. For example, the following will return pages with the word <em>login</em> in the title:</p><p>intitle:login</p><p>For multiple string searches, you can use the allintitle operator. Here’s an example:</p><p>allinurl:etc passwd</p> |
| link         | link:_string_                          | Displays linked pages based on a search term.                                                                                                                                                                                                                                                     |
| related      | related:_webpagename_                  | Shows webpages similar to _webpagename_.                                                                                                                                                                                                                                                          |
| Site         | site:_domain_ or _web_ _page_ _string_ | <p>Displays pages for a specific website or domain holding the search term. For example, the following will display all pages with the text <em>passwds</em> in the site anywhere.com:</p><p>site:anywhere.com passwds</p>                                                                        |

**Note: Google hacking is such a broad topic that covering all of it in one section of a single book is impossible. This link, among others, provides a great list to work through: http://it.toolbox.com/blogs/managing-infosec/google-hacking-master-list-28302. Take advantage of any of the websites available and learn more as you go along.**

The practice of Google hacking encompasses a broad range of applications. It can be utilized to discover illicit music downloads, although I must emphasize that engaging in music piracy is illegal and should be avoided. An example search string for finding such downloads is "intitle:index of" nameofsong.mp3. Additionally, Google hacking can be employed to identify vulnerabilities within a network. For instance, a search query like "intitle:Nessus Scan Report" "This file was generated by Nessus" can reveal web pages containing the results of a vulnerability scan conducted with Nessus. By leveraging advanced search operators, users can delve deeper into the search results and uncover intriguing information. It is crucial to note that none of these search strings or hacking techniques themselves are illegal. Users are free to search for anything within legal bounds. However, it is imperative to exercise restraint and refrain from exploiting any findings without prior consent, as this can result in legal consequences. While the aforementioned Google hacking examples serve as a solid foundation, there are numerous additional techniques to be explored, which can be found in the GHDB. Aspiring ethical hackers may find particular interest in the application of Google hacking to VoIP and VPN systems. VoIP systems, for example, present intriguing opportunities when one possesses knowledge of their location and functionalities. It is worth noting that certain VoIP systems utilize unprotected Trivial FTP (TFTP) for retrieving configuration files, and some even offer packet capture capabilities directly on the phone. Furthermore, most VoIP devices feature web servers for remote management. Such insights should undoubtedly grab the attention of aspiring ethical hackers. VPN systems also offer fascinating opportunities. Should one successfully obtain and compromise encryption keys, gaining access to a VPN connection becomes almost equivalent to physically infiltrating an office and connecting their own device to an employee's workstation. The principles and methods underlying Google hacking for VoIP and VPN are similar to those for any other application. The objective is to identify web pages containing specific information to facilitate the intended goals, and the combination of search terms and operators narrows down the scope of the search. For instance, employing search terms like "login," "login page," and "welcome," in conjunction with the intitle: operator, could yield login portals in the search results. For more precise results, one can try terms like "D-Link VIP Router" to target D-Link router portals, or "SPA504G" for Cisco configuration utilities. Additionally, employing the search query filetype:pdf vpn OR Group can help locate publicly accessible VPN client profile configuration (PFC) files. Another option is to use inurl:/remote/login?lng=en to identify FortiGate Firewall SSL VPN portals. The possibilities for Google hacking in the context of VoIP and VPN are limitless.

I would like to emphasize that Google hacking has become more challenging in recent times. Google has taken steps to monitor search results and prevent misuse of its search engine. To deter "bots" and individuals attempting unethical activities, Google may occasionally present a CAPTCHA as a security measure. These CAPTCHAs can be bypassed using techniques that are widely available and can be found through additional searches on Google; however, it is important to note that despite such workarounds, the annoyance factor remains; therefore, in your quest for the information you are seeking, it is worth considering other search engines in addition to Google. By exploring alternative search engines, you may increase your chances of finding the desired results.

![Google Operating System: Google's "We're Sorry" Error Page](<../../.gitbook/assets/0 (69).png>)
