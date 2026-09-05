# Denial of Service

Denial of Service (DoS) and Distributed Denial of Service (DDoS) attacks have been major concerns for network administrators over the past two decades. These attacks aim to exhaust resources such as memory, CPU cycles, and network bandwidth, rendering them unavailable to legitimate users and thereby violating the cybersecurity principle of availability. Launching a DoS attack typically requires minimal bandwidth from the attacker and can be executed using just a few devices. In contrast, a DDoS attack involves flooding the victim with packets, which can be done in two ways: by sending packets with spoofed IP addresses (e.g., amplification/reflection attacks) or by using a botnet of compromised devices to send the flood of packets.

Motivations for these attacks vary, from gaining recognition in underground communities to corporate sabotage against competitors. Traditional network/transport layer DDoS attacks disrupt connectivity by targeting network equipment and infrastructure. These attacks are well-known, and numerous surveys have been published on them.

Recently, a new class of attacks known as application layer DoS attacks has gained popularity. These attacks exploit vulnerabilities in application layer protocols, often due to insufficient security measures during protocol development. For instance, the focus on functionality over security in protocols like HTTP/2 compared to HTTP/1.1 has left a significant attack surface. Application layer DoS attacks can incapacitate servers with substantial computational power and bandwidth using minimal resources. Typically, a single computer can execute an application layer DoS attack, making these attacks more stealthy and difficult to detect than network/transport layer DDoS attacks.

Application layer DoS attacks specifically target services on the victim with minimal impact on network resources. For example, Slow Rate DoS attacks against HTTP can prevent a web server from responding to legitimate clients, while attacks against NTP can disrupt clients' ability to synchronize their clocks. These attacks generate less traffic than network/transport layer DDoS attacks, making them harder to mitigate. Modifying protocol operations to prevent these attacks is challenging, as it requires updating protocol standards and widespread implementation of these changes, which is a lengthy and complex process.

\### Recent Trends and Incidents

According to the 2019 Global DDoS Threat Landscape Report by Imperva, the largest application layer DoS attack in history was recorded in 2019. This attack lasted for 13 days and peaked at 292,000 Requests Per Second (RPS). Another report indicates that the number of application layer DoS/DDoS attacks is doubling every quarter, even though the number of network layer assaults in the fourth quarter of 2017 decreased by 50% from the third quarter of 2017. The growing popularity of application layer DoS attacks is evident from several incidents outlined in Table 1, showing how these attacks were encountered. Besides these reported incidents, many DoS/DDoS attacks caused by insider threats go unreported due to fear of negative publicity. Additionally, some common application layer DoS attacks, such as DHCP starvation attacks, occur within local networks and are thus not reported. According to a 2018 Insider Threat report, 53% of organizations confirmed insider attacks against them in the past year.

Security researchers have recently scrutinized protocols such as HTTP/2, DHCP, NTP, DNS, and others to uncover potential vulnerabilities that can be exploited for DoS attacks. To counter these attacks, researchers have proposed various defense mechanisms. These recent developments and corresponding detection and mitigation schemes are not covered in previous surveys, highlighting the need for a comprehensive study of attacks against commonly targeted application layer protocols and their defense mechanisms.

\### Application Layer DDoS Attack Incidents

\| Year | Target | Scale | Attack | Impact |

\|------|--------|-------|--------|--------|

\| 2020 | A state voter registration site | ≈ 200,000 DNS requests | DNS flood | Not disclosed |

\| 2019 | An Imperva client (name not disclosed) | 292,000 requests per second | Not disclosed | Not disclosed |

\| 2019 | National Union of Journalists of the Philippines website | 76 Gbps | HTTP flood | Website went offline |

\| 2018 | Three banks - ABN AMRO, ING, and Rabobank | Not disclosed | Not disclosed | Disruption of mobile banking services |

\| 2017 | Bitcoin gold website | 10M requests per minute | HTTP flood | The website went down |

\| 2017 | Spanish government websites | Not disclosed | HTTP flood | Websites of the constitutional court were taken offline |

\| 2017 | Swedish transportation services | Not disclosed | HTTP flood | Attack caused train delays and disruption of travel services |

\| 2016 | Finland heating systems | Not disclosed | DNS flood | The heating systems stopped working |

\| 2016 | HSBC bank website | Not disclosed | HTTP flood | Attack mitigated successfully |

\| 2016 | Rio Olympic games websites | Not disclosed | HTTP flood | Several Rio Olympic games websites denied access to legitimate clients |

\| 2016 | DYN’s DNS infrastructure | Not disclosed | DNS flood | Popular websites such as Etsy, Github, Spotify, and Twitter suffered service interruptions or went offline altogether |

\| 2016 | Liberia’s Internet infrastructure | Not disclosed | Not disclosed | The internet in the country went down |

\| 2015 | Github’s website | Not disclosed | HTTP flood | Github managed to overcome the attack |

\| 2014 | Hong Kong media website | 250 million DNS requests per second | DNS flood | Campaigning for a democratic voting system affected |

\| 2012 | Web infrastructure of several banks | 63.3 Gbps | HTTP flood | Access to online and mobile banking services got affected |

\| 2009 | Iranian presidential election campaign | Not disclosed | Slowloris | Not disclosed |

In this paper, we present a structured survey of various application layer DoS attacks. We also review various state-of-the-art defense mechanisms known to counter attacks against these protocols. We make the following specific contributions:

1\. \*\*Comprehensive Survey\*\*: We present a detailed survey of application layer DoS attacks, classifying them based on their effectiveness against specific protocols or a broad range of protocols.

2\. \*\*Attack Analysis\*\*: We discuss the mechanisms of these attacks, compare them based on various parameters, and describe tools and libraries used to launch them.

3\. \*\*Defense Mechanisms\*\*: We review and classify various defense mechanisms, explaining their strengths and weaknesses and comparing them based on multiple criteria.

4\. \*\*Commercial Mitigation Products\*\*: We compare several popular commercial DoS mitigation products based on their ability to counter different attacks.

5\. \*\*Future Research Directions\*\*: We identify gaps in current research and suggest promising areas for future investigation.

The paper is organized as follows: Section 2 reviews related surveys and justifies the motivation for our work. Section 3 discusses protocol-specific application layer DoS attacks and their defense mechanisms. Section 4 describes generic application layer DoS attacks and the defenses against them. Section 5 compares different application layer DoS attacks and defense mechanisms. Section 6 presents a comparative study of commercial DoS mitigation products. Finally, Section 7 concludes the paper and suggests future research directions.

According to the 2024 Global DDoS Threat Landscape Report by Imperva, the largest application layer DoS attack in history was recorded in 2024. This attack lasted for 16 days and peaked at 450,000 Requests Per Second (RPS). Another report indicates that the number of application layer DoS/DDoS attacks has been increasing by 80% annually, even though the number of network layer assaults in the fourth quarter of 2023 decreased by 40% from the third quarter of 2023. The growing prevalence of application layer DoS attacks is evident from several incidents outlined in Table 1, illustrating how these attacks have been encountered. Besides these reported incidents, many DoS/DDoS attacks caused by insider threats go unreported due to fears of negative publicity. Additionally, some common application layer DoS attacks, such as DHCP starvation attacks, occur within local networks and are thus not reported. According to a 2023 Insider Threat report, 60% of organizations confirmed insider attacks against them in the past year.

DDoS attacks continued to disrupt and destabilize organizations, industries, and nation-states in 2022. Application layer DDoS attacks increased by 82% compared to 2021, with attacks on the financial services sector growing by 121% year on year. The largest application layer DDoS attack mitigated by Imperva in 2022 was a ransom DDoS attack measuring 3.9 million requests per second (RPS). Repeat attacks continued to be a trend in 2022, with around 46% of websites targeted by a DDoS attack being attacked more than once. The largest Layer 3 and Layer 4 DDoS attack occurred in July and peaked at 1,373 gigabits per second (Gbps). Layer 3 and Layer 4 attacks rose dramatically in August 2022 compared to any other month of the year.

\### Notable Application Layer DoS and DDoS Attacks Since 2020

1\. \*\*Akamai Attack (2020)\*\*

\- \*\*Target:\*\* Unnamed European bank

\- \*\*Scale:\*\* 809 million packets per second (PPS)

\- \*\*Description:\*\* This attack was one of the largest packet-per-second attacks mitigated by Akamai. It utilized multiple attack vectors to overwhelm the target’s infrastructure.

2\. \*\*New Zealand Stock Exchange (NZX) Attack (2020)\*\*

\- \*\*Target:\*\* New Zealand Stock Exchange

\- \*\*Scale:\*\* Not disclosed

\- \*\*Description:\*\* The NZX experienced a series of sophisticated DDoS attacks that forced trading halts over several days. The attack was reportedly driven by a ransom demand.

3\. \*\*AWS Attack (2020)\*\*

\- \*\*Target:\*\* Amazon Web Services (AWS) customer

\- \*\*Scale:\*\* 2.3 Tbps

\- \*\*Description:\*\* This was the largest DDoS attack mitigated by AWS at the time, leveraging a high-volume connectionless Lightweight Directory Access Protocol (CLDAP) reflection technique.

4\. \*\*Singapore Government Websites (2020)\*\*

\- \*\*Target:\*\* Multiple government websites

\- \*\*Scale:\*\* Not disclosed

\- \*\*Description:\*\* Several government websites in Singapore were hit by DDoS attacks, leading to temporary disruptions. The specifics of the attack vectors were not publicly detailed.

5\. \*\*Microsoft Azure Attack (2021)\*\*

\- \*\*Target:\*\* Unspecified Azure customers

\- \*\*Scale:\*\* 2.4 Tbps

\- \*\*Description:\*\* The attack peaked at 2.4 Tbps and lasted over 10 minutes, with multiple short-lived bursts. The attack used a variety of UDP reflection techniques.

6\. \*\*VoIP.ms Attack (2021)\*\*

\- \*\*Target:\*\* VoIP.ms

\- \*\*Scale:\*\* Not disclosed

\- \*\*Description:\*\* VoIP.ms, a Voice-over-IP (VoIP) provider, was targeted by a sustained ransom DDoS attack that disrupted services for several days.

7\. \*\*Cloudflare Attack (2022)\*\*

\- \*\*Target:\*\* Unspecified Cloudflare customer

\- \*\*Scale:\*\* 15.3 million RPS

\- \*\*Description:\*\* This was the largest HTTPS DDoS attack recorded by Cloudflare, utilizing a botnet to generate massive volumes of HTTPS requests.

8\. \*\*Imperva Mitigated Attack (2022)\*\*

\- \*\*Target:\*\* Financial services sector

\- \*\*Scale:\*\* 3.9 million RPS

\- \*\*Description:\*\* Imperva mitigated a significant ransom DDoS attack targeting a financial services client, highlighting the ongoing threat to critical infrastructure.

9\. \*\*Russian Government Websites (2022)\*\*

\- \*\*Target:\*\* Various Russian government websites

\- \*\*Scale:\*\* Not disclosed

\- \*\*Description:\*\* Amid geopolitical tensions, several Russian government websites were targeted by DDoS attacks, leading to disruptions. The attacks were part of broader cyber warfare activities.

10\. \*\*European Gaming Company (2023)\*\*

\- \*\*Target:\*\* Unspecified European gaming company

\- \*\*Scale:\*\* 1.7 Tbps

\- \*\*Description:\*\* The attack targeted the gaming company's servers, leveraging multiple vectors including application-layer techniques to disrupt services during a major event.

11\. \*\*Healthcare Sector Attack (2023)\*\*

\- \*\*Target:\*\* Unspecified healthcare organization

\- \*\*Scale:\*\* Not disclosed

\- \*\*Description:\*\* The attack leveraged application-layer vulnerabilities to disrupt healthcare services, raising concerns about the security of critical healthcare infrastructure.

These examples highlight the evolving and persistent threat of application layer DDoS attacks, affecting a wide range of industries and sectors globally.
