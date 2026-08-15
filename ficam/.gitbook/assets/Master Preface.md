*This is the "Sales Pitch" to the readers. It explains the philosophy of the book.*

The Identity Battlefield

For decades, the "Network Perimeter" was the wall we defended. We built firewalls and guarded the gates. But in the modern era, that wall has crumbled. In a world of remote work, cloud integration, and sophisticated social engineering, **Identity is the new perimeter**.

Active Directory is the heart of that identity. It is the single source of truth for 90% of the world's corporate networks. To an attacker, it is not just a directory brimming with juicy sensitive details and information; it is a map to the "Crown Jewels." To a defender, it is a complex, legacy-burdened ecosystem that is notoriously difficult to secure.

This book is born from the realization that you cannot defend what you do not understand. We will not look at security as a checklist of GPO settings. Instead, we will look at it through the lens of the adversary. We will walk the paths they walk, use the tools they use, and think the way they think. Only then, once we have seen the domain from the "inside out," will we build a defense that is truly resilient.

This is not just a book about hacking. It is a book about **mastery**. Whether you are a Red Teamer looking to sharpen your edge or a SysAdmin tasked with guarding the kingdom, this is your field manual.

===============================

Master of Your Domain: Hacking and Defending Active Directory (AD) for Ethical Hackers.tex} is a practical exploration of how today's modern Active Directory (AD) environments are breached, abused, and defended in the real-world. This book was written for aspiring and seasoned ethical hackers, red and blue teamers, penetration testers, defenders, and anyone who wants to understand the true dynamics of modern Windows network compromise - beyond theory, beyond checklists.

Active Directory remains one of the most targeted and misunderstood components in enterprise cyber security. It's vast, complex, and oftentimes misconfigured. For attackers, it's a playground - a goldmine. For defenders, it's a battlefield in the truest sense. This book aims to arm you with both perspectives of both offensive and defensive cyber security. You'll find detailed coverage of post-exploitation tactics, including certificate abuse (e.g., Golden Tickets), persistence techniques, lateral movement, privilege escalation, and the tools used and methods in which to attack and defend the Kerberos authentication protocol. But more than just technical content, this book emphasizes mindset: how an attacker thinks when they're inside, undetected, and methodically deciding their next move. Understanding that psychology is just as critical as knowing the tools.

Each chapter is based on real-world engagements and lessons learned the hard way. No two networks are the same - but patterns emerge, and opportunities repeat themselves. The goal of this book is to help you recognize those opportunities. Whether you are breaking in, or locking things down.

To those who supported the long hours, reviewed the raw material, and challenged my thinking - thank you. This book wouldn't exist without your input, insight, and encouragement.

  
  

A preface\index{preface} is a book's preliminary statement, usually written by the \textit{author or editor} of a work, which states its origin, scope, purpose, plan, and intended audience, and which sometimes includes afterthoughts and acknowledgments of assistance.

  

When written by a person other than the author, it is called a foreword. The preface or foreword is distinct from the introduction, which deals with the subject of the work.

  =======================================================================

Master of Your Domain: Hacking and Defending Active Directory (AD) for Ethical Hackers is a practical exploration of how today's modern Active Directory (AD) environments are breached, abused, and defended in the real-world. This book was written for aspiring and seasoned ethical hackers, red, blue, and purple teamers, penetration testers, SOC analysts, incident responder, defenders, and anyone who wants to better understand the true dynamics of modern Windows network compromise - beyond theory, beyond checklists. Active Directory remains one of the most targeted and misunderstood components in enterprise cyber security. It's vast, complex, and oftentimes (more so, than not) misconfigured. An oversight on a security control where one checkbox was forgot to be checked, an "it can wait till tomorrow" kind of day where rebooting domain controllers from patching was delayed by a day, to tricking users online and offline, misconfigurations, "innocent oversights, failure to identify, failiure to validate all equal a low hanging fruit just ripe for the attacker's picking; hence the term of saying tht attackers go after the easy shit first, the "low hanging fruit - they find the most easiest ways in through vulnerability exploitation or beause the one skipped checkbox automatically port <> and they got in. For attackers, it's a playground - a goldmine. For defenders, it's a hellhole in the truest sense. This book aims to arm you with both perspectives of both offensive and defensive cyber security. You'll find detailed coverage of post-exploitation tactics, including certificate abuse (Golden Ticket), persistence techniques like backdooring and using remote trojans, lateral movement, privilege escalation, and the tools used and methods in which to attack and defend the Kerberos authentication protocol. But more than just technical content, this book emphasizes mindset: go an attacker thinks when they're inside, undetected, and methodically deciding their next move, or pivot. Understanding that psychology is just as critical as knowing the tools. Each chapter is based on real-world engagements and lessons learned the hard way. No two networks are the same - but patterns emerge, and opportunities repeat themselves. the goal of this book is to help you recognize those opportunities. Whether you are breaking in, or locking things down there's a section that pertains to you. To those who supported the long hours, reviewed the raw material, and challenged my way of thinking - thank you. This book wouldn't exist without your input, insight, and encouragement.

========================================

Preface



Option 1:

This book was born out of necessity - a resource I desperately needed almost twenty years ago but could never find. After almost two decades on the front lines of Department of Defense (DoD) Network Security Operations (NetSecOps), I have lived the evolution from help desk technician to ISSE. I've defended vast Cisco backbones, spanning from Riverside, CA, to Germany and Japan, and I have scrutinized classified SIPRNet/SCI and NIPRNet/CUI infrastructure under immense, real-world pressure.

I have conducted vulnerability assessments, penetration tests, and complex Active Directory audits, often manually hardening systems in an era before modern automation. I know all too well the dangers of the infamous "Click here to fix all" button from the old Gold Disk days - the hard way. I have executed numerous Red Team operations where a single misconfiguration meant a failure in the availability of mission-critical network broadcast operations.



This book is the distillation of that operationalized experience, designed for those entering the field who need to know what actually works when an adversary is lurking in the network. the current security and threat landscape is saturated with theoretical texts and outdated methodologies. This is not another sanitized guide. This is a practical, no-nonsense approach to ethical hacking, reflecting how it is actually practiced under tight constraints and against active defenses.



Option 2

After almost 20 years of being a part of the NetSecOps team for the DoD - from help desk technician to ISSE - I've seen what actually holds up under pressure. I've secured critical infrastructure across global SIPR/NIPR environments and learned that theoretical security fails when in production.



This book provides the practical, battle-tested knowledge I needed when I started. It bypasses the AI-generated "fluff" and outdated, sanitized advice to show you how ethical hacking is really conducted: limited time, incomplete intelligence, and active, intelligent adversaries. This is your guide to defensive and offensive security operations, written by someone who has lived through them.



Option 3

I wrote this book because I needed it twenty years ago. Working through the ranks - HBSS administrator, senior analyst, ISSE - I learned that theoretical knowledge doesn't stop adversaries. I've handled everything from manual server hardening with nothing but a Gold Disk to red teaming on classified networks where a mere typo could jeopardize mission-critical functions and ongoing operations.



I have seen what works, and I have seen what breaks when you apply "fix-all" buttons without understanding the potential impact and consequences. If you are entering the cyber field, you don't need another theoretical text. You need to officially know how to defend enterprise infrastructure that spans continents. This book is a raw, honest look at authorized, practical ethical hacking in the messiest, real-world DoD Active Directory ICAM environments.

=====================================

ORIGINAL



This book exists because I needed it twenty years ago, and it did not exist back then.



After almost two decades of operational work in Department of Defense Network Security Operations (NetSecOps) - spanning help desk technician, network engineer, information systems security engineer, HBSS global administrator, senior cybersecurity analyst, vulnerability management analyst, ISSO, and now ISSE - I have seen firsthand what works in the field and what falls apart under real-world pressure.



I have run penetration tests and security control assessments as part of CORI/CCRI operations, including business continuity and continuity of operations gap analyses using FIPS 199 and 200 to categorize and classify an entire Command's most critical mission-supporting server architecture. That meant assessing, critiquing, questioning, scrutinizing, testing, and breaking - then putting it all back together - across both SIPRNet/SCI and NIPRNet CUI infrastructure. I have defended enterprise environments supporting over fifteen hundred endpoints across massive Cisco-based network backbones stretching from Riverside, California, to Yokota, Japan, to Heidelberg and Spangdahlem Germany. I have conducted vulnerability assessments, AD  IAM/ICAM credential audits, and Active Directory security posture reviews against DISA STIGs and SRGs - and I have manually hardened server operating systems in an era when the closest thing to automation was a Gold Disk shipped first-class priority mail, with a single button in the admin UI labeled *Click here to fix all.*



If you have been in this industry long enough, you already know why that button is a hard no. Clicking it without proper documentation means you have no rollback, no audit trail, no CYA accountability, and no real way to determine what exactly broke what when the system inevitably decided to misbehave afterward. I learned that lesson the way most practitioners do - under pressure, with no margin for error, in environments where a single misconfiguration was not only just a minor inconvenience, but an issue of military and defense security liability.



I have conducted red team operations - Kerberoasting, Golden Ticket attacks and beyond - in exactly those kinds of environments. This book is the distillation of that operational experience, structured for practitioners who need more than just theory. They need what actually works in the field when an adversary is already pivoting around the network.



The modern cybersecurity publishing landscape is saturated with introductory texts, certificate guides, and repetitive theoretical overviews. They have their place, and they certainly have had their time; however, most security forums today are either flooded with AI-generated noise or practitioners who are repackaging content written over fifteen years ago by someone else. What is largely absent are resources that reflect the messy reality of production Active Directory environments - the kind where sanitized methodology meets incomplete intelligence, compressed timelines, active detection mechanism, and defensive teams who are neither incompetent nor asleep.



This book does not tell you what ethical hacking is. It shows you how it is actually conducted under the constraints that define real security and ethical hacking engagements. It approaches the discipline the way security practitioners do: as an authorized, adversarial exercise requiring fluency on both sides of the operation.



The cybersecurity publishing landscape is saturated with introductory texts, certification guides, and theoretical overviews. Helpful? Most definitely. Needed? Surely. Straightforward and forthcoming? Not so much. Most of security-related forums nowadays are either filled with AI slop or individuals rewriting what someone else wrote over 15 years ago. Most of them present sanitized methodologies divorced from the messy ty AD production environments. They tell you what ethical hacking is; they do not show you how it is conduct under the constraints that define real security engagements: limited time, incomplete intelligence, detection mechanisms actively hunting for your presence, and defensive teams who are neither incompetent nor asleep. this book approaches ethical hacking the way it is actually practiced in authorized security assessments and as a disciplined adversarial exercise conducted by professionals who understand both sides of the operation.



The DoD Perspective

Modern Government and defense agencies and network environments operate under constraints that do not exist in commercial IT. STIGs, SRGs, Risk management Framework (RMF), CNSSI, NSA NSS, NIST, FIPS, CMMC, FedRAMP, and FISMA compliance - mandated, and these are not abstractions. They are operational requirements enforced through Presidential Executive Orders (EOs), IAVAs, and through formal internal policy monitored through continuous assessments, and audited through external validation. An ethical hacker working in this space must understand not only how to exploit a vulnerability, but how that vulnerability maps back to a specific control or TTP identified by the MITRE ATT\&CK Framework or within the RMF framework, what the remediation requirements are under the applicable STIG, and how exactly the finding will be categorized (Category 1 - III) during an Authorization to Operate (ATO) Certification and Accreditation security review.



This book incorporates that perspective throughout. When discussing Active Directory Identity, Credential, and Access Management (ICAM) exploitation, I address it in the context of environments where every Domain Controller is hardened against the most current baseline STIG, where privileged access is governed by form credential management procedures using PKI and smart card-based logon, and where lateral movement must account for endpoint detection and response tooling that is mandatory rather than optional. When covering password analysis, I frame it through the lens of NIST Special Publication (SP) 800-63 B requirements and explain how credential analytics is conducted in production AD environments where security is also not a feature or a luxury - it is a compliance obligation and necessity with measurable and actionable enforcement.



Purple Team Operations: Attack and Defense as Unified Disciplines



Throughout my career, I have worked both offense and defense, and I reject the notion that one side is inherently more sophisticated or intellectually demanding than the other. Red team operations - penetration testing, vulnerability exploitation, credential theft, lateral movement - are technically challenging and require deep knowledge of systems, protocols, topologies, technologies, tooling, and more; however, Blue Team operators - threat hunting, log analysis, correlation, threat aggregation and trending, intelligence gathering, incident response for everything, defensive hardening, security implementation strategies, layered security, defense in depth - are equally sophisticated and demand the same depth of expertise. A competent ethical hacker understands both perspectives because that really is the only way to conduct meaningful security assessments.



This book is written from that unified perspective: Every attack technique presented is accompanied by an analysis of how defenders detect it, what log artifacts it generates, and what hardening measures disrupt it. Every defensive control discussed is evaluated through the lens of how an attacker would attempt to breach or bypass it. This is not red team versus blue team - this is Operational Security assessment (OPSEC) conducted by professionals who understand that meaningful improvements come from testing defenses under realistic adversarial conditions and then fixing whatever breaks.



Methodology and Approach

Ethical hacking is not a linear practice or process with a universal "one-size-fits-all" approach that applies to every engagement. The methodology I present in this book reflects that very reality. Security assessments vary based on the scope of the engagement, the threat model that is being evaluated, the client's risk tolerance and appetite, the resources that are allocated to the assessment, and the regulatory framework that is governing the target environment. An external penetration test conducted against a public-facing web application with no prior knowledge differs fundamentally from an internal-assumed breach assessment conducted with domain user credentials in a production Active Directory ICAM environment. The techniques overlap, but the execution, the constraints, and the objectives are all mostly distinct from each other.



The approach taught throughout this book is structured around the phases that define real-world penetration testing engagements: reconnaissance and intelligence gathering, where you build a target profile, or dossier, from Open-Source Intelligence (OSINT) and network enumeration; discovery and planning, where you threat model attack strategies based on identified and discovered target assets and assess  relationships to high-level and valued assets such as Domain Controllers; vulnerability detection, where you systematically probe for security weaknesses; exploitation, where you validate vulnerabilities through controlled compromise; and post-exploitation analysis, where you measure the impact of successful attacks and document findings for remediation. This is not a theoretical framework - this is the operational workflow used in Department of Defense security assessments, commercial penetration tests, and authorized red and blue team exercises (CORI/CCRI).



Throughout this book, I aim to emphasize practical execution over abstract concepts. You will learn how to use various Active Directory penetration testing-related tools, such as Impacket Tool Suite's `secretsdump.py` to extract credentialed material from Active Directory Certificate Services (AD CS) via Domain Controller breach, as well as learn the art of how to conduct offline password cracking with Hashcat against NTLM hashes using both generic breach wordlists and organization-specific contextual terms generated with CeWL. You will learn how to analyze credential reuse patterns using DSInternals and quantify password security posture using metrics that map directly to exploitable attack vectors and pathways using BloodHound and SharpHound. These are not hypothetical exercises - these are the exact techniques I, as have attackers in the real-world, used in operational assessment and attacks, and they are proven to work.



Tool Philosophy: Open-Source and Accessible

Every tool and technique in this book is built on open-source software. There are no commercial licensing requirements, no vendor-locked toolchains, and no paywalls that will prevent you from replicating the work. Impact, Hashcat, BloodHound, PowerView, CrackMapExec, Mimikatz, Rubeus, DSInternals - all of these tools are freely available for download and provide up to date documentation that is actively maintained by the security researchers of the community. If you have a standard penetration testing workstation and an internet connection, you have everything you need to perform the assessments described in this book.



The expectation is that you fully engage with the material actively. Set up lab environments. Run the tools. Break things intentionally and observe and take note of what happens, or what doesn't for that matter. Security knowledge is not acquired passively through reading - it is build through doing, with hands-on experimentation under controlled conditions. If you encounter a technique you do not understand, research the underlying mechanism> If you discover a defensive control that defeats an attack I describe, investigate why it works and document it. This field rewards curiosity yet punishes complacency.



There is also an expectation that you contribute back to the community. The knowledge in this book was not developed in isolation - it was learned from other practitioners, refined through experience, and shared openly because that is how progress happens in this field. If you find value in this material, pass it forward. Mentor junior analysts. Document your findings and publish them. Share techniques that are known and proven to work and warn others about approaches that fail. The security community operates on reciprocity: the more you give, the more you receive. Consider this book my contribution to that exchange, and consider yourself obligated to continue it.



Terminology: Hackers, Attackers, Threat Actors, Adversaries, Black-Hats



The term "hacker" carries different meanings depending on context and audience. In academic and research communities, it describes someone with a deep technical skill who pushes systems beyond their intended limits. In media coverage and public perception, it describes a criminal who breaks into computer systems for malicious purposes. This semantic ambiguity creates confusion, so I define the terms clearly here for the remainder of this book.



When I refer to *'hackers,' 'ethical hackers,' 'white-hat hackers,'* or *'blue teams/blue teamers,'* I mean security professionals conducting authorized penetration tests, vulnerability assessments, and red and blue team operations with explicit written permission form the target organization. These are individuals who are operating within legal and contractual boundaries, testing and penetrating defenses to identify weaknesses, gaps, flaws, misconfigurations, deficiencies, and defects before real adversaries exploit them.



When I refer to *'attackers,' 'adversaries,' 'threat actors,'* or *'black-hat hackers,'*  I mean individuals conducting exactly the opposite of what a white-hat hacker aims to achieve: unauthorized intrusions with criminal or hostile intent. These are the threat actors that defenders aim to protect against - nation-state intelligence services and agencies, organized cybercrime syndicates and groups, hacktivists, and opportunistic script kiddies, or *'skiddz.'*



This distinction matters legally and operationally. Ethical hacking is conducted under formal authorized agreements that define scope, acceptable actions, Rules of Engagement, data handling procedures, hard stops, and reporting requirements and frequencies. Unauthorized intrusion - regardless of the stated intent - is a criminal act under the Computer Fraud and Abuse Act (CFAA) in the United States and equivalent statutes in other jurisdictions. If you conduct the techniques provided herein without explicit written authorization, you are not an ethical hacker - you are a criminal. There is no grey area here.



A Final Word



Security is a discipline where the cost of failure can be measured in compromised credentials, stolen intellectual property, disrupted operations, regulatory penalties and fines, and in some contexts, loss of life. The stakes are real. The adversaries are more than capable. The defenses are and remain imperfect. If you choose to work in this field - whether as a penetration tester validating security controls, a defender who is hardening infrastructure, an incident responder investigating continued breaches, or a security architect who is designing resilient systems - you carry responsibility for the confidentiality, integrity, availability, and accountability for the environments you touch. That responsibility demands technical aptitude, professionalism, competence, operational discipline, and ethical clarity. This book provides the technical foundation. The rest is on you.



All my best.



Stay safe. Stay vigilant. Stay informed.

================================================

PREFACE

The first microprocessors appeared in the early 1970 s and were immediately employed in _Personal Computers_, or _PCs_. A popular question in those early years was: _Why would anyone want a computer in their home?_ Typical answers varied from: _To balance your checking account, to store your recipes, and to help you compute your taxes._ It was only a few years later, when many already owned personal computers, that computer owners discovered the real reasons for the utter usefulness of their machines. We buy and use personal computers mainly because they provide us with communications, news, and entertainment.

Games, initially primitive, were written for the early personal computers and became a powerful selling tool in the hands of computer salespersons because of the entertainment they provided. The development of email in the 1970 s and of the _World Wide Web (WWW)_ in the 1980 s have turned computers into tools for communications, which is why they became the common household appliances they are today. Most owners of home computers use their computers to play games and to communicate, to send and receive email, and to browse the Internet. Relatively few users perform computations, benefit from a personal database, or know how to use a spreadsheet.

Once personal computers became a part of our daily lives, it had quickly been realized that like many other technological advances, computers and data networks have their dark side. Security problems in the form of malicious programs, loss of privacy, and floods of unwanted advertisements and spam, have popped up immediately and have become a way of life for virtually every computer user.

**Exercise Intro. 1:** What industry is the biggest user of computers?

**Definitions.** The Webster’s Collegiate Dictionary defines security as _“the quality or state of being free from danger”_ or _:measures taken to guard espionage or sabotage, crime, attack, or escape.”_ This book explores some of the ways computers and computer networks are put at risk by perpetrators like nation-state and state-sponsored hackers, or _Advanced Persistent Threat (APT) actors_, and other wrongdoers. The terms “attack” and “threat” are used here to identify any activity that aims to gain access to computers for malicious reasons. The terms “security hole,” “weakness,” and “vulnerability” refer to a state that can be exploited for such an attack (some would even go as far as to argue that a security hole _invites_ attack).

For the purpose of computer security, there are two types of people: _insiders_ (employees) and _outsiders_ (non-employees). The figure below shows the three classes of computer security and cybercrime caused by each of the two types plus the special class of threats that are not directly caused by humans, namely accidents.

- Insiders Overt. Overt actions by insiders are often performed by disgruntled employees and results in destruction of data, equipment, and ultimately reputations.
- Insiders Covert. Generally, insiders have more information about a place of work than outsiders, which is why they can wreak more havoc. Thus, this class corresponds to serious threats and criminal actions.
- Insiders Unintended. Employees make errors and can also neglect their duties. Consequently, this class encompasses actions such as wrong inputs, wrong data, or damage as a result of extreme temperatures or other harsh conditions, and interruption of vital services.
- Outsiders Overt. Physical attacks on computer and networked facilities belong in this class as do DoS attacks.
- Outsiders Covert. This wide class consists of the various types of rogue software sent from the outside to a personal computer or to a large computer facility.
- Outsiders Unintended. It is fairly rare that an outsider will harm a computer or data unintentionally.
- Finally, there are accidents. They always happen, not just in the computing field. Accidents are caused by many elements that are combined with risk, such as by nature: earthquake, floods, tsunami, or indirectly by humans (see the “insiders unintended” class).

There are many different types of computer security threats and problems of all sorts and sizes; however, they can be classified into three primary classes, as follows below:

- **Physical Security.** A personal computer can be stolen. A large computer center can be broken into and equipment and cash taken. Fire, electrical surges, and floods can damage computer hardware and network connections and cause loss of data. These and other physical threats are only part of the problem.
- **Rogue Software.** We have all heard of computer viruses. Small, crappy programs that invade our computers and spread quickly and silently. Viruses are only one aspect of the general threat posed by rogue software.
- Most computers are connected to networks, and most local networks are connected to the Internet, which is the largest _Wide Area Network (WAN)_ to date. Thus, there is a large class of computer security threats that are related to networks and fall under the category of network security. This wide area of security includes threats such as port scanning, spoofing, password cracking, spyware, and identity theft.

Almost nonexistent two decades ago, computer security is now a vast, complex, and critical field. This book is just one of many books, articles, reports, and other publications that discuss, explain, theorize, and analyze the various aspects of and approaches for computer security. The feature that makes this book special is its reliance on the keyword “compromise.” This word is employed here in two distinct meanings, as follows below:

1. Computer security equals compromise. The more security is needed, the less convenient it is for the end-user to use their internet-connected devices.

2. An attacker has to find only one security weakness and cause extensive psychological and financial damage to users, their identities, software, and personal and commercial data.

Any security threat or vulnerability described in this book can be reduced, managed, solved, or overcome in some way, but the solution makes it more difficult or less convenient to use the computer, the network, or a particular operating system or program.

Why does the problem of computer security even exist? Why are computers so vulnerable to attacks and so easy to damage? This book offers four reasons, but the reader may come up with more.

Reason 1. Computers are fast, accurate, and powerful for certain tasks such as computing, searching, and manipulating data, while being inadequate and inefficient to other tasks, most notably in anything requiring intelligence.

The field of _Artificial Intelligence (AI)_ is almost as old as the modern electronic computer. Researchers have been trying since the 1950 s to teach computers how to solve real-world problems such as recognizing patterns, playing games against a human opponent, and translating natural languages, all without success. Today, after almost half a century of effort, computers can recognize handwriting, can identify speech commands, and can prove certain types of mathematical theorems, but are not good at any of these tasks. Computers have recently become good at beating chess masters at their own game, but only because they (the computers) are fast enough to analyze every possible move within a reasonable amount of time, not because they understand chess.

Thus, computers are fast, reliable, and not to mention useful, but are not very intelligent, which makes them victims of (computer) crime. Even humans, who are much more intelligent, (too?) often fall prey to clever schemes designed to take their money, so it is no wonder that the problem of computer security is serious and is getting worse by the day.

**Exercise Intro.2:** Computers are fast, reliable, and not to mention useful, but they are not very intelligent. With this in mind, can they be trusted?

Reason 2. It is far easier to break computer security than it is to build fully secure computers. A modern computer nowadays has many security weaknesses and an attacker has to find only to do harm. A security worker, on the other hand, has to find and correct _all_ of the security holes, a virtually impossible task.

Reason 3. A computer is controlled by its _Operating System (OS)_ and modern operating systems (e.g., Windows, Linux) are extremely complex. A systems programmer designs an operating system with a view towards making it easy to use, but as we already know, the easier it is to use a computer, the less secure it is. Today’s modern _Graphical User Interface (GUI)_ operating systems are designed around several layers where the user interacts with the top level and the hardware is controlled by the bottom level. Each level controls the one directly below it and it is this organization in levels that allows malware to hide from the user and perform its operations in relative obscurity and safety.

At the time of this writing (mid-2025), operating systems have become so complex (not to mention so bloated), that attackers constantly find ways to exploit vulnerabilities and security holes in them. Quite often, such holes are discovered by honest users who then notify the vendor or manufacturer of the vulnerable product, resulting in a patch rollout or an update being promptly issued to remediate the problem, only for a new hole to be quickly discovered. The following warning, found on the Internet in late October 2024, is typical. It shows how difficult it is to identify a security vulnerability, because it may occur in rare circumstances. Don’t worry about the details, just keep in mind that this announcement is typical.
