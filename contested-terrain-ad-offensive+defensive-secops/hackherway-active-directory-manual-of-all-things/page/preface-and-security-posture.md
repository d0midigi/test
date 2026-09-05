# Preface and Security Posture

### Preface

With a threat landscape that it is in constant motion, it becomes imperative to have a strong

security posture, which in reality means enhancing the protection, detection, and response.

Throughout this book, you will learn the attack methods and patterns to recognize

abnormal behavior within your organization with Blue Team tactics. You will also learn

techniques to gather exploitation intelligence, identify risks, and demonstrate impact on

Red and Blue team strategies.

### Who this Book is For

This book is for information security professionals and IT professionals who want to know

more about Cybersecurity.

### What this book covers

Chapter 1, _Security Posture_, defines what constitute a secure posture and how it helps in

understanding the importance of having a good defense and attack strategy.

Chapter 2, _Incident Response Process_ (IRP), introduces the incident response process and the importance of having one. It goes over different industry standards and best practices for

handling the incident response.

Chapter 3, Understanding the Cybersecurity Kill Chain, prepares the reader to understand the mindset of an attacker, the different stages of the attack, and what usually takes place in

each one of those phases.

Chapter 4, Reconnaissance, speaks about the different strategies to perform reconnaissance

and how data is gathered to obtain information about the target for planning the attack.

Chapter 5, Compromising the System, shows current trends in strategies to compromise the

system and explains how to compromise a system.

Chapter 6, Chasing a User's Identity, explains the importance of protecting the user's identity

to avoid credential theft and goes through the process of hacking the user's identity.

Chapter 7, Lateral Movement, describes how attackers perform lateral movement once they

compromise one system.

Chapter 8, Privilege Escalation, shows how attackers can escalate privileges in order to gain

administrative access to the network system.

Chapter 9, Security Policy, focuses on the different aspects of the initial defense strategy,

which starts with the importance of a well-created security policy and goes over the best

practices for security policies, standards, security awareness training, and core security

controls.

Chapter 10, Network Segmentation, looks into different aspects of defense in depth, covering

physical network segmentation as well as the virtual and hybrid cloud.

Chapter 11, Active Sensors, details different types of network sensors that help the

organizations to detect attacks.

Chapter 12, Threat Intelligence, speaks about the different aspects of threat intelligence from

the community as well as from the major vendors.

Chapter 13, Investigating an Incident, goes over two case studies, for an on-premises

compromised system and for a cloud-based compromised system, and shows all the steps

involved in a security investigation.

Chapter 14, Recovery Process, focuses on the recovery process of a compromised system and

explains how crucial it is to know what all options are available since live recovery of a

system is not possible during certain circumstances.

Chapter 15, Vulnerability Management, describes the importance of vulnerability

management to mitigate vulnerability exploitation. It covers the current threat landscape

and the growing number of ransomware that exploits known vulnerabilities.

Chapter 16, Log Analysis, goes over the different techniques for manual log analysis since it

is critical for the reader to gain knowledge on how to deeply analyze different types of logs

to hunt suspicious security activities.

### To get the most out of this book

Readers of this book are expected to have a basic understanding of computer science, networking, information security, and security concepts, as well as familiarity with Windows and Linux operating systems. K

Note 90% of all hacking takes place via a terminal, shell, or CLI. H acking is normally not a GUI-based “point and click” game, so it would be in your best interest to learn these at a minimum

2\. Some of the demonstrations from this book can also be done in a lab environment; therefore, we recommend you have a virtual lab with the following VMs: Windows Server 2012, Windows 10, and Kali Linux.

### Conventions Used

There are a number of text conventions used throughout this book.

CodeInText: Indicates code words in text, database table names, folder names, filenames,

file extensions, pathnames, dummy URLs, user input, and Twitter handles. Here is an

example: "Mount the downloaded WebStorm-10\*.dmg disk image file as another disk in

your system."

**Bold:** Indicates a new term, an important word, or words that you see onscreen. For

example, words in menus or dialog boxes appear in the text like this. Here is an example:

"Select **System info** from the **Administration** panel."

_**New or Unfamiliar Terms:**_ Will appear throughout the chapters and paragraphs indicating a term deemed important enough you should probably highlight it as you will need to know what the words definition is inside and out throughout your ethical hacking journey and career.

| <img src="../.gitbook/assets/0 (73).png" alt="Comment Important with solid fill" data-size="original"> | Warnings or important notes appear like this. |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------- |

| <img src="../.gitbook/assets/1 (54).png" alt="Lightbulb and gear with solid fill" data-size="original"> | Tips and tricks appear like this. |
| ------------------------------------------------------------------------------------------------------- | --------------------------------- |

**Errata**: Although we have taken every care to ensure the accuracy of our content, mistakes

do happen. If you have found a mistake in this book, we would be grateful if you would

report this to us. Please visit www.<>

### Reviews

Please leave a review. Once you have read and used this book, why not leave a review on

the site that you purchased it from. Potential readers can then see and use your unbiased

opinion to make purchase decisions, we at <> can understand what you think about our

products, and our authors can see your feedback on their book. Thank you!

For more information about <>, please visit <>.

|                                            | <h3>CHAPTER</h3> |
| ------------------------------------------ | ---------------- |
| <p><br>THE PROPERTIES OF CYBERSECURITY</p> | 1                |

### Security Posture

Over the years, the investments in security moved from nice to have to must have, and now

organizations around the globe are realizing how important it is to continually invest in

security. This investment will ensure that the company stays competitive in the market.

Failure to properly secure their assets could lead to irreparable damage, and in some

circumstances could lead to bankruptcy. Due to the current threat landscape, investing only

in protection isn't enough. Organizations must enhance their overall security posture. This

means that the investments in protection, detection, and response must be aligned.

In this chapter, we'll be covering the following topics:

* The Current Threat Landscape
* Challenges in the Land of Cybersecurity
* Tips to Enhance Security Postures via Layered Defense and Defense in Depth Approaches
* Understanding the Roles, Responsibilities, and Functionalities of Red and Blue Teams
* The Properties of Cybersecurity

With the prevalence of always-on connectivity and advancements in technology that are

available today, the threats are evolving rapidly to exploit different aspects of these

technologies. Any device is vulnerable to attack, and with Internet of Things (IoT) this

became a reality. In October 2016, a series of Distributed Denial of Service (DDoS) attacks

were launched against DNS servers, which caused some major web services to stop

working, such as GitHub, Paypal, Spotify, Twitter, and others.

Security Posture Chapter 1

\[ 7 ]

This was possible due to the amount of insecure IoT devices around the world. While the

use of IoT to launch a massive cyber attack is something new, the vulnerabilities in those

devices are not. As a matter of fact, they've been there for quite a while. In 2014, ESET

reported 73,000 unprotected security cameras with default passwords (2). In April 2017,

IOActive found 7,000 vulnerable Linksys routers in use, although they said that it could be

up to 100,000 additional routers exposed to this vulnerability (3).

The Chief Executive Officer (CEO) may even ask: what do the vulnerabilities in a home

device have to do with our company? That's when the Chief Information Security Officer

(CISO) should be ready to give an answer. Because the CISO should have a better

understanding of the threat landscape and how home user devices may impact the overall

security that this company needs to mitigate. The answer comes in two simple scenarios,

remote access and Bring your Own Device (BYOD).

While remote access is not something new, the number of remote workers are growing

exponentially. Forty-three percent of employed Americans are already working remotely

according to Gallup (4), which means they are using their own infrastructure to access

company's resources. Compounding this issue, we have a growth in the number of

companies allowing BYOD in the workplace. Keep in mind that there are ways to

implement BYOD securely, but most of the failures in the BYOD scenario usually happen

because of poor planning and network architecture, which lead to an insecure

implementation (5).

What is the commonality among all technologies that were previously mentioned? To

operate them, you need a user and the user is still the greatest target for attack. Humans are

the weakest link in the security chain. For this reason, old threats such as phishing emails

are still on the rise, because it deals with the psychological aspects of the user by enticing

the user to click on something, such as a file attachment or malicious link. Usually, once the

user performs one of these actions, their device becomes compromised by either malicious

software (malware) or is remotely accessed by a hacker.

A spear phish campaign could start with a phishing email, which will basically be the entry

point for the attacker, and from there other threats will be leveraged to exploit

vulnerabilities in the system.

One example of a growing threat that uses phishing emails as the entry point for the attack

is ransomware. Only during the first three months of 2016, the FBI reported that $209

million in ransomware payments were made (6). According to Trend Micro, ransomware

growth will plateau in 2017; however, the attack methods and targets will diversify (7).

Security Posture Chapter 1

\[ 8 ]

The following diagram highlights the correlation between these attacks and the end user:

This diagram shows four entry points for the end user. All of these entry points must have

their risks identified and treated with proper controls. The scenarios are listed as follows:

Connectivity between on-premises and cloud (1)

Connectivity between BYOD devices and cloud (2)

Connectivity between corporate-owned devices and on-premises (3)

Connectivity between personal devices and cloud (4)

Notice that these are different scenarios, but all correlated by one single entity-the end user.

The common element in all scenarios is usually the preferred target for cybercriminals,

which appears in the preceding diagram accessing cloud resources.

Security Posture Chapter 1

\[ 9 ]

In all scenarios, there is also another important element that appears constantly, which is

cloud computing resources. The reality is that nowadays you can't ignore the fact that many

companies are adopting cloud computing. The vast majority will start in a hybrid scenario,

where Infrastructure as a Service (IaaS) is their main cloud service. Some other companies

might opt to use Software as a Service (SaaS) for some solutions. For example, Mobile

Device Management (MDM), as shown in scenario (2). You may argue that highly secure

organizations, such as the military may have zero cloud connectivity. That's certainly

possible, but commercially speaking, cloud adoption is growing and will slowly dominate

most of the deployment scenarios.

On-premise security is critical, because it is the core of the company, and that's where the

majority of the users will be accessing resources. When an organization decides to extend

their on-premise infrastructure with a cloud provider to use IaaS (1), the company needs to

evaluate the threats for this connection and the countermeasure for these threats through a

risk assessment.

The last scenario (4) might be intriguing for some skeptical analysts, mainly because they

might not immediately see how this scenario has any correlation with the company's

resources. Yes, this is a personal device with no direct connectivity with on-premise

resources. However, if this device is compromised, the user could potentially compromise

the company's data in the following situations:

Opening a corporate email from this device

Accessing corporate SaaS applications from this device

If the user uses the same password (8) for his/her personal email and his

corporate account, this could lead to account compromise through brute force or

password guessing

Having technical security controls in place could help mitigate some of these threats against

the end user. However, the main protection is continuous use of education via security

awareness training.

The user is going to use their credentials to interact with applications in order to either

consume data or write data to servers located in the cloud or on-premise. Everything in

bold has a unique threat landscape that must be identified and treated. We will cover these

areas in the sections that follow.

Security Posture Chapter 1

\[ 10 ]

The credentials – authentication and

authorization

According to Verizon's 2017 Data Breach Investigations Report (9), the association between

threat actor (or just actor), their motives and their modus operandi vary according to the

industry. However, the report states that stolen credentials is the preferred attack vector for

financial motivation or organized crime. This data is very important, because it shows that

threat actors are going after user's credentials, which leads to the conclusion that companies

must focus specifically on authentication and authorization of users and their access rights.

The industry agreed that a user's identity is the new perimeter. This requires security

controls specifically designed to authenticate and authorize individuals based on their job

and need for specific data within the network. Credential theft could be just the first step to

enable cybercriminals to have access to your system. Having a valid user account in the

network will enable them to move laterally (pivot), and at some point find the right

opportunity to escalate privilege to a domain administrator account. For this reason,

applying the old concept of defense in depth is still a good strategy to protect a user's

identity, as shown in the following diagram:

Security Posture Chapter 1

\[ 11 ]

Here, there are multiple layers of protection, starting with the regular security policy

enforcement for accounts, which follow industry best practices such as strong password

requirements, a policy requiring frequent password changes, and password strength.

Another growing trend to protect user identities is to enforce MFA. One method that is

having increased adoption is the callback feature, where the user initially authenticates

using his/her credentials (username and password), and receives a call to enter their pin. If

both authentication factors succeed, they are authorized to access the system or network.

We are going to explore this topic in greater detail in Chapter 6, Chasing User's Identity.

Apps

Applications (we will call them apps from now on), are the entry point for the user to

consume data and to transmit, process, or store information onto the system. Apps are

evolving rapidly and the adoption of SaaS-based apps is on the rise. However, there are

inherited problems with this amalgamation of apps. Here are two key examples:

Security: How secure are these apps that are being developed in-house and the

ones that you are paying for as a service?

Company-owned versus personal apps: Users will have their own set of apps on

their own devices (BYOD scenario). How do these apps jeopardize the company's

security posture and can they lead to a potential data breach?

If you have a team of developers that are building apps in-house, measures should be taken

to ensure that they are using a secure framework throughout the software development

lifecycle, such as the Microsoft Security Development Lifecycle (SDL) (10). If you are

going to use a SaaS app, such as Office 365, you need to make sure you read the vendor's

security and compliance policy (11). The intent here is to see if the vendor and the SaaS app

are able to meet your company's security and compliance requirements.

Another security challenge facing apps is how the company's data is handled among

different apps, the ones used and approved by the company and the ones used by the end

user (personal apps). This problem becomes even more critical with SaaS, where users are

consuming many apps that may not be secure. The traditional network security approach to

support apps is not designed to protect data in SaaS apps, and worse. They don't give IT the

visibility they need to know how employees are using them. This scenario is also called

Shadow IT, and according to a survey conducted by Cloud Security Alliance (CSA) (12),

only 8 percent of companies know the scope of shadow IT within their organizations. You

can't protect something you don't know you have, and this is a dangerous place to be.

Security Posture Chapter 1

\[ 12 ]

According to Kaspersky Global IT Risk Report 2016 (13), 54 percent of businesses perceive

that the main IT security threats are related to inappropriate sharing of data via mobile

devices. It is necessary for IT to gain control of the apps and enforce security policies across

devices (company-owned and BYOD). One of the key scenarios that you want to mitigate is

the one described in the following diagram:

In this scenario, we have the user's personal tablet that has approved applications as well as

personal apps. Without a platform that can integrate device management with application

management, this company is exposed to a potential data leakage scenario. In this case, if

the user downloads the excel spreadsheet onto his/her device and uploads it to a personal

Dropbox cloud storage and the spreadsheet contains the company's confidential

information, the user has now created a data leak without the company's knowledge or the

ability to secure it.

Security Posture Chapter 1

\[ 13 ]

Data

As we finished the previous section talking about data, we should ensure that data is

always protected regardless of its current state (in transit or at rest). There will be different

threats according to the data's state. The following are some examples of potential threats

and countermeasures:

State Description Threats Countermeasures Security triad

affected

Data at rest

on the

user's

device.

The data is

currently

located on the

user's device.

The unauthorized or

malicious process

could read or

modify the data.

Data encryption at

rest. It could be filelevel encryption or

disk encryption.

Confidentiality

and integrity.

Data in

transit.

The data is

currently

being

transferred

from one host

to another.

A man-in-themiddle attack could

read, modify, or

hijack the data.

SSL/TLS could be

used to encrypt the

data in transit.

Confidentiality

and integrity.

Data at rest

on-premise

(server) or

cloud.

The data is

located at rest

either on the

server's hard

drive located

on-premise or

in the cloud

(storage pool).

Unauthorized or

malicious processes

could read or

modify the data.

Data encryption at

rest. It could be filelevel encryption or

disk encryption.

Confidentiality

and integrity.

These are only some examples of potential threats and suggested countermeasures. A

deeper analysis must be performed to fully understand the data path according to the

customer's needs. Each customer will have their own particularities regarding data path,

compliance, rules, and regulations. It is critical to understand these requirements even

before the project is started.

Security Posture Chapter 1

\[ 14 ]

Cybersecurity challenges

To analyze the cybersecurity challenges faced by companies nowadays, it is necessary to

obtain tangible data, and evidence of what's currently happening in the market. Not all

industries will have the same type of cybersecurity challenges, and for this reason we will

enumerate the threats that are still the most prevelant across different industries. This seems

to be the most appropriate approach for cybersecurity analysts that are not specialized in

certain industries, but at some point in their career they might need to deal with a certain

industry that they are not so familiar with.

Old techniques and broader results

According to Kaspersky Global IT Risk Report 2016 (14), the top causes for the most costly

data breaches are based on old attacks that are evolving over time, which are in the

following order:

Viruses, malware, and trojans

Lack of diligence and untrained employees

Phishing and social engineering

Targeted attack

Crypto and ransomware

Although the top three in this list are old suspects and very well-known attacks in the

cybersecurity community, they are still succeeding, and for this reason they are still part of

the current cybersecurity challenges. The real problem with the top three is that they are

usually correlated to human error. As explained before, everything may start with a

phishing email that uses social engineering to lead the employee to click on a link that may

download a virus, malware, or Trojan. In the last sentence, we covered all three in a single

scenario.

The term targeted attack (or advanced persistent threat) sometimes is not too clear for some

individuals, but there are some key attributes that can help you identify when this type of

attack is taking place. The first and most important attribute is that the attacker has a

specific target in mind when he/she starts to create a plan of attack. During this initial

phase, the attacker will spend a lot of time and resources to perform public reconnaissance

to obtain the necessary information to carry out the attack. The motivation behind this

attack is usually data exfiltration, in other words, stealing data. Another attribute for this

type of attack is the longevity, or the amount of time that they maintain persistent access to

the target's network. The intent is to continue moving laterally across the network,

compromising different systems until the goal is reached.

Security Posture Chapter 1

\[ 15 ]

One of the greatest challenges in this area is to identify the attacker once they are already

inside the network. The traditional detection systems such as Intrusion Detection Systems

(IDS) may not be sufficient to alert on suspicious activity taking place, especially when the

traffic is encrypted. Many researchers already pointed out that it can take up to 229 days

between the infiltration and detection (15). Reducing this gap is definitely one of the

greatest challenges for cybersecurity professionals.

Crypto and ransomware are emerging and growing threats that are creating a whole new

level of challenge for organizations and cybersecurity professionals. In May 2017, the world

was shocked by the biggest ransomware attack in history, called Wannacry. This

ransomware exploited a known Windows SMBv1 vulnerability that had a patch released in

March 2017 (59 days prior to the attack) via MS17-010 (16) bulletin. The attackers used an

exploit called EternalBlue that was released in April 2017, by a hacking group called

Shadow Brokers. According to MalwareTech (18), this ransomware infected more than

400,000 machines across the globe, which is a gigantic number, never seen before in this

type of attack. One lesson learned from this attack was that companies across the world are

still failing to implement an effective vulnerability management program, which is

something we will cover in more detail in Chapter 15, Vulnerability Management.

It is very important to mention that phishing emails are still the number one delivery

vehicle for ransomware, which means that we are going back to the same cycle again,

educate the user to reduce the likelihood of successful exploitation of human factor via

social engineering, and have tight technical security controls in place to protect and detect.

The shift in the threat landscape

In 2016, a new wave of attacks also gained mainstream visibility, when CrowdStrike

reported that it had identified two separate Russian intelligence-affiliated adversaries

present in the United States Democratic National Committee (DNC) network (19).

According to their report, they found evidence that two Russian hacking groups were in the

DNC network: Cozy Bear (also classified as APT29) and Fancy Bear (APT28). Cozy Bear

was not a new actor in this type of attack, since evidence has shown that in 2015 (20) they

were behind the attack against the Pentagon email system via spear phishing attacks.

This type of scenario is called Government-sponsored cyber attacks, but some specialists

prefer to be more general and call it data as a weapon, since the intent is to steal information

that can be used against the hacked party. The private sector should not ignore these signs.

Security Posture Chapter 1

\[ 16 ]

Nowadays, continuous security monitoring must leverage at least the three methods shown

in the following diagram:

This is just one of the reasons that it is becoming primordial that organizations start to

invest more in threat intelligence, machine learning, and analytics to protect their assets. We

will cover this in more detail in Chapter 12, Threat Intelligence.

Enhancing your security posture

If you carefully read this entire chapter, it should be very clear that you can't use the old

approach to security facing today's challenges and threats. For this reason, it is important to

ensure that your security posture is prepared to deal with these challenges. To accomplish

this, you must solidify your current protection system across different devices regardless of

the form factor.

It is also important to enable IT and security operations to quickly identify an attack, by

enhancing the detection system. Last but certainly not least, it is necessary to reduce the

time between infection and containment by rapidly responding to an attack by enhancing

the effectiveness of the response process.

Security Posture Chapter 1

\[ 17 ]

Based on this, we can safely say that the security posture is composed of three foundational

pillars as shown in the following diagram:

These pillars must be solidified and if in the past, the majority of the budget was put into

protection, now it's even more imperative to spread that investment and level of effort

across the other pillars. These investments are not exclusively in technical security controls,

they must also be done in the other spheres of the business, which includes administrative

controls.

It is recommended to perform a self-assessment to identify the gaps within each pillar from

the tool perspective. Many companies evolved over time and never really updated their

security tools to accommodate the new threat landscape and how attackers are exploiting

vulnerabilities.

Security Posture Chapter 1

\[ 18 ]

A company with an enhanced security posture shouldn't be part of the statistics that were

previously mentioned (229 days between the infiltration and detection). This gap should be

drastically reduced and the response should be immediate. To accomplish this, a better

incident response process must be in place, with modern tools that can help security

engineers to investigate security-related issues. Chapter 2, Incident Response Process will

cover incident response in more detail and Chapter 13, Investigating an Incident, will cover

some case studies related to actual security investigations.

The Red and Blue Team

The Red/Blue Team exercise is not something new. The original concept was introduced a

long time ago during World War I and like many terms used in information security,

originated in the military. The general idea was to demonstrate the effectiveness of an

attack through simulations.

For example, in 1932 Rear Admiral Harry E. Yarnell demonstrated the efficacy of an attack

on Pearl Harbor. Nine years later, when the Japanese attacked Pearl Harbor, it was possible

to compare and see how similar tactics were used (22).

The effectiveness of simulations based on real tactics that might be used by the adversary

are well known and used in the military. The University of Foreign Military and Cultural

Studies has specialized courses just to prepare Red Team participants and leaders (23).

Although the concept of read eaming in the military is broader, the intelligence support via

threat emulation is similar to what a cybersecurity Red Team is trying to accomplish. The

Homeland Security Exercise and Evaluation Program (HSEEP) (24) also uses red teaming

in the preventions exercise to track how adversaries move and create countermeasures

based on the outcome of these exercises.

In the cybersecurity field, the adoption of the Red Team approach also helped organizations

to keep their assets more secure. The Red Team must be composed of highly trained

individuals, with different skill sets and they must be fully aware of the current threat

landscape for the organization's industry. The Red Team must be aware of trends and

understand how current attacks are taking place. In some circumstances and depending on

the organization's requirements, members of the Red Team must have coding skills to

create their own exploit and customize it to better exploit relevant vulnerabilities that could

affect the organization.

Security Posture Chapter 1

\[ 19 ]

The core Red Team workflow takes place using the following approach:

The Red Team will perform an attack and penetrate the environment by trying to

breakthrough the current security controls, also known as penetration testing. The intent of

the mission is to find vulnerabilities and exploit them in order to gain access to the

company's assets. The attack and penetration phase usually follows the Lockheed Martin

approach, published in the paper, Intelligence-Driven Computer Network Defense Informed by

Analysis of Adversary Campaigns and Intrusion Kill Chains (25). We will discuss the kill chain

in more detail in Chapter 3, Understanding the Cybersecurity Kill Chain.

The Red Team is also accountable to register their core metrics, which are very important

for the business. The main metrics are as follows:

Mean Time to Compromise (MTTC): This starts counting from the minute that

the Red Team initiated the attack to the moment that they were able to

successfully compromise the target

Mean Time to Privilege Escalation (MTTP): This starts at the same point as the

previous metric, but goes all the way to full compromise, which is the moment

that the Red Team has administrative privilege on the target

So far, we've discussed the capacity of the Red Team, but the exercise is not completed

without the counter partner, the Blue Team. The Blue Team needs to ensure that the assets

are secure and in case the Red Team finds a vulnerability and exploits it, they need to

rapidly remediate and document it as part of the lessons learned.

Security Posture Chapter 1

\[ 20 ]

The following are some examples of tasks done by the Blue Team when an adversary (in

this case the Red Team) is able to breach the system:

Save evidence: It is imperative to save evidence during these incidents to ensure

you have tangible information to analyze, rationalize, and take action to mitigate

in the future.

Validate the evidence: Not every single alert, or in this case evidence, will lead

you to a valid attempt to breach the system. But if it does, it needs to be cataloged

as an Indication of Compromise (IOC).

Engage whoever is necessary to engage: At this point, the Blue Team must know

what to do with this IOC, and which team should be aware of this compromise.

Engage all relevant teams, which may vary according to the organization.

Triage the incident: Sometimes the Blue Team may need to engage law

enforcement, or they may need a warrant in order to perform the further

investigation, a proper triage will help on this process.

Scope the breach: At this point, the Blue Team has enough information to scope

the breach.

Create a remediation plan: The Blue Team should put together a remediation

plan to either isolate or evict the adversary.

Execute the plan: Once the plan is finished, the Blue Team needs to execute it and

recover from the breach.

The Blue Team members should also have a wide variety of skill sets and should be

composed of professionals from different departments. Keep in mind that some companies

do have a dedicated Red/Blue Team, while others do not. Companies put these teams

together only during exercises. Just like the Red Team, the Blue Team also has

accountability for some security metrics, which in this case is not 100% precise. The reason

the metrics are not precise is that the true reality is that the Blue Team might not know

precisely what time the Red Team was able to compromise the system. Having said that, the

estimation is already good enough for this type of exercise. These estimations are selfexplanatory as you can see in the following list:

Estimated Time to Detection (ETTD)

Estimated Time to Recovery (ETTR)

Security Posture Chapter 1

\[ 21 ]

The Blue Team and the Red Team's work doesn't finish when the Red Team is able to

compromise the system. There is a lot more to do at this point, which will require full

collaboration among these teams. A final report must be created to highlight the details

regarding how the breach occurred, provide a documented timeline of the attack, the details

of the vulnerabilities that were exploited in order to gain access and to elevate privileges (if

applicable), and the business impact to the company.

Assume breach

Due to the emerging threats and cyber security challenges, it was necessary to change the

methodology from prevent breach to assume breach. The traditional prevent breach

approach by itself does not promote the ongoing testing, and to deal with modern threats

you must always be refining your protection. For this reason, the adoption of this model to

the cybersecurity field was a natural move.

When the former director of the CIA and National Security Agency Retired Gen. Michael

Hayden said in 2012(26):

"Fundamentally, if somebody wants to get in, they're getting in. Alright, good. Accept

that."

During an interview, many people didn't quite understand what he really meant, but this

sentence is the core of the assume breach approach. Assume breach validates the protection,

detection, and response to ensure they are implemented correctly. But to operationalize this,

it becomes vital that you leverage Red/Blue Team exercises to simulate attacks against its

own infrastructure and test the company's security controls, sensors, and incident-response

process.

In the following diagram, you have an example of the interaction between phases in the

Red Team/Blue Team exercise:

Security Posture Chapter 1

\[ 22 ]

It will be during the post breach phase that the Red and Blue Team will work together to

produce the final report. It is important to emphasize that this should not be a one off

exercise, instead, must be a continuous process that will be refined and improved with best

practices over time.

References

You can refer to the following articles:

1\. Refer to http://www.darkreading.com/attacks-breaches/new-iot-botnetdiscovered-120k-ip-cameras-at-risk-of-attack/d/d-id/1328839

2\. Refer to https://www.welivesecurity.com/2014/11/11/website-reveals73000-unprotected-security-cameras-default-passwords/

3\. Refer to https://threatpost.com/20-linksys-router-models-vulnerable-toattack/125085/

4\. Refer to https://www.nytimes.com/2017/02/15/us/remote-workers-work-fromhome.html

5\. Read the vendor-agnostic guidelines to adopt BYOD published at the ISSA

Journal https://blogs.technet.microsoft.com/yuridiogenes/2014/03/11/

byod-article-published-at-issa-journal/

Security Posture Chapter 1

\[ 23 ]

6\. Refer

to http://www.csoonline.com/article/3154714/security/ransomware-took-in

-1-billion-in-2016-improved-defenses-may-not-be-enough-to-stem-thetide.html

7\. Refer to http://blog.trendmicro.com/ransomware-growth-will-plateau-in2017-but-attack-methods-and-targets-will-diversify/

8\. Read this article for more information about the dangerous aspects of using the

same password for different accounts http://www.telegraph.co.uk/finance/

personal finance/bank-accounts/12149022/Use-the-same-password-foreverything-Youre-fuelling-a-surge-in-current-account-fraud.html

9\. Download the report from http://www.verizonenterprise.com/resources/

reports/rp\_DBIR\_2017\_Report\_en\_xg.pdf

10\. Read more information about SDL at https://www.microsoft.com/sdl

11\. Microsoft Office 365 Security and Compliance can be found at https://support.

office.com/en-us/article/Office-365-Security-Compliance-Center7e696a40-b86b-4a20-afcc-559218b7b1b8

12\. Read the entire study at https://downloads.cloudsecurityalliance.org/

initiatives/surveys/capp/Cloud\_Adoption\_Practices\_Priorities\_Survey\_

Final.pdf

13\. Read the full report at http://www.kasperskyreport.com/?gclid=CN\_

89N2b0tQCFQYuaQodAQoMYQ

14\. You can download the report at http://www.kasperskyreport.com/?gclid=CN\_

89N2b0tQCFQYuaQodAQoMYQ

15\. Refer to https://info.microsoft.com/ME-Azure-WBNR-FY16-06Jun-21-22-

Microsoft-Security-Briefing-Event-Series-231990.html?ls=Social

16\. Read the Microsoft bulletin for more information https://technet.microsoft.

com/en-us/library/security/ms17-010.aspx

17\. Read this article for more information about this group https://www.symantec.

com/connect/blogs/equation-has-secretive-cyberespionage-group-beenbreached

Security Posture Chapter 1

\[ 24 ]

18\. Refer to https://twitter.com/MalwareTechBlog/status/865761555190775808

19\. Refer to https://www.crowdstrike.com/blog/bears-midst-intrusiondemocratic-national-committee/

20\. Refer to http://www.cnbc.com/2015/08/06/russia-hacks-pentagon-computersnbc-citing-sources.html

21\. Refer to https://www.theverge.com/2017/5/17/15655484/wannacry-variantsbitcoin-monero-adylkuzz-cryptocurrency-mining

22\. Refer to https://www.quora.com/Could-the-attack-on-Pearl-Harbor-havebeen-prevented-What-actions-could-the-US-have-taken-ahead-of-time-todeter-dissuade-Japan-from-attacking#!n=12

23\. You can download the Red Team handbook at http://usacac.army.mil/sites/

default/files/documents/ufmcs/The\_Applied\_Critical\_Thinking\_Handbook\_

v7.0.pdf

24\. Refer to https://www.fema.gov/media-library-data/20130726-1914-25045-

8890/hseep\_apr13\_.pdf

25\. Download the paper from https://www.lockheedmartin.com/content/dam/

lockheed/data/corporate/documents/LM-White-Paper-Intel-Driven-Defense.

pdf

26\. Refer to http://www.cbsnews.com/news/fbi-fighting-two-front-war-ongrowing-enemy-cyber-espionage/

Summary

In this chapter, you learned more about the current threat landscape and how these new

threats are used to compromise credentials, apps, and data. In many scenarios, old hacking

techniques are used, such as phishing emails. However, with a more sophisticated

approach. You also learned the current reality regarding the nationwide type of threat, and

government-targeted attacks. In order to protect your organization against these new

threats, you learned about key factors that can help you to enhance your security posture. It

is essential that part of this enhancement shifts the attention from protection only to include

detection and response. For that, the use of Red and Blue Team becomes imperative. The

same concept applies to the assume breach methodology.

In the next chapter, you will continue to learn about the enhancement of your security

posture: however, the chapter will focus on the incident response process. The incident

response process is primordial for companies that need a better detection and response

against cyber threats
