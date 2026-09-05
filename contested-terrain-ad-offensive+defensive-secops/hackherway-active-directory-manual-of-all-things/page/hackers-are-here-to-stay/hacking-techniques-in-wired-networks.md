# Hacking Techniques in Wired Networks

Hacking Techniques in Wired Networks

**INTRODUCTION**

Wired networks, including the Internet, have become integral to our daily lives; however, over the past decade, security breaches have increasingly challenged the design and development of these networks and systems. Hackers and malicious actors frequently exploit vulnerabilities in existing systems, making cyberattacks an ever-growing threat to society as a whole. To enhance network protection, this section provides insights into various hacking techniques. It examines the objectives, principles, functionalities, and characteristics of different types of hacking methods in wired networks. Additionally, this section will explore the common features of cyberattacks, their structure, and components, and the interrelationships among different attacks. These insights aim to help you more quickly and easily understand the core aspects of emerging cyber threats.

Today, wired networks have evolved into platforms that not only enable high-speed data communications but also support powerful distributed computing infrastructures for a wide range of personal and business activities; however, this expansion has also turned these networks into a vast playground for hackers and malicious actors to explore and exploit. The original principles behind network design and development often focus on connection and communication rather than security. This oversight has become increasingly apparent as significant security breaches continue to escalate, as illustrated in the figure below. Because security is often not integrated into the foundational design of these networks, they remain highly susceptible to cyberattacks due to the various vulnerabilities they house. Whether ethical or unethical, hackers drive the development of numerous hacking techniques, which in turn facilitate cyberattacks. These attacks have become a significant challenge and pain in the ass for network and system engineers and administrators, and they continue to emerge as a serious threat to society as a whole.

Throughout 2023 and early 2024, we continued to see a significant number of low-skill, opportunistic attacks – proof that script kiddies are still very much active; however, the overall skill level and sophistication observed in major incidents have notably increased compared to previous years. While the vulnerabilities in these cases primarily involved perimeter and network edge devices or file transfer technologies, the evolving tactics of attackers has raised alarm in other areas as well, particularly in discussions about supply chain security and insider threats. This concern is well-founded, given the key supply chain attack vectors and significant incidents of 2023.

One critical area of concerns is the rise of pre-patch exploitation, often referred to as _**zero-day**_ attacks. Between the end of 2020 and the end of 2021, the number of large-scale incidents resulting in the compromise of multiple organizations more than doubled, and those numbers have not dropped to pre-2021 levels since. Even more troubling is the sharp increase in widespread zero-days, which quintupled in 2021, and have remained a persistent threat ever since. By 2023, for the second time in three years, more mass compromise events were attributed to zero-day vulnerabilities than to n-day vulnerabilities, underscoring the growing challenge that these unpatched, previously unknown security flaws pose to organizations worldwide.

![A graph of a graph with orange and grey bars

Description automatically generated with medium confidence](<../../.gitbook/assets/0 (35).png>)

Since 2021, researchers and analysts have been tracking the time between when vulnerabilities are publicly disclosed and when they are reliable reported as being exploited in the wild. This period, referred to as _**“Time to Known Exploitation (TTKE),”**_ has significantly shortened over the past three years, primarily due to the increase in zero-day attacks. Zero-day vulnerabilities have made up 43% of the known-exploited CVEs that have been reported on since January 2021. Of these, 55% were exploited in just one week of public disclosure, and 60% within two weeks. In contrast, data from Gartner’s 2020 Vulnerability Intelligence Report showed that zero-day flaws accounted for less than a quarter of reported vulnerabilities, with only 30% being exploited within a week and 32% within two weeks. This sharp increase highlights the growing urgency and challenge of addressing vulnerabilities as quickly as possible in the face of increasingly rapid exploitation.

![A graph with orange bars

Description automatically generated](<../../.gitbook/assets/1 (21).png>)

The average Time of Known Exploitation (TTKE) can be a less informative metric when a significant number of TTKE values are zero, indicating immediate exploitation upon disclosure. Despite this, for CVEs with known TTKE values, the average time to exploitation is just over 22 days, with a median time of just one day. This highlights how quickly vulnerabilities can be exploited once they become public knowledge.

The chart that follows provides an analysis of exploited and widely exploited vulnerabilities and shows the percentage of these vulnerabilities that were exploited as zero-day flaws. Due to increasingly strict and prescribed methodologies for vulnerability classification and selection, the 2023 data presented offers a relatively conservative view of current exploitation trends.

![A graph of a graph with numbers and lines

Description automatically generated with medium confidence](<../../.gitbook/assets/2 (20).png>)

To enhance network protection, this section provides an overview of various hacking techniques. Understanding how hackers operate is crucial for effectively securing networks, and this section aims to shed light on the objectives, principles, functionalities, and characteristics of different types of hacking methods in wired networks; however, it does not examine step-by-step hacking processes, as those are covered in other sections of this book. Instead, this section focuses on well-known and documented vulnerabilities and attacks, most of which have been mitigated by improved protocols and systems. While it is impossible to identify every vulnerability or attack, this section offers in-depth discussions on the common characteristics of cyberattacks, their structure and components, and the interrelationships among them. These insights are intended to help you more easily and quickly understand the essence of new cyber threats.

This subchapter is organized as follows: Section 2 summarizes the principles of hacking, providing an overview of common hacking procedures, reviewing widely-used hacking toolkits, and illustrating how these tools are employed. Section 3 discusses how hacking techniques can be used to attack the Internet infrastructure. Section 4 explores how these techniques can target end systems of the Internet, and Section 5 examines attacks on enterprise network systems.

**PRINCIPLES OF HACKING**

In this section, attacks and hacking techniques are distinct concepts, though they are closely intertwined. An _**attack**_ usually progresses through several phases, each involving specific actions taken by the hacker. These actions often require the use of one or more hacking techniques, which can vary depending on the phase of the attack. Additionally, a single attack or hacking tool may span multiple phases and incorporate various hacking techniques. This relationship highlights the complexity of cyberattacks, where different techniques are strategically employed at different stages to achieve the attacker’s goals.

**HACKING METHODOLOGY**

The process of
