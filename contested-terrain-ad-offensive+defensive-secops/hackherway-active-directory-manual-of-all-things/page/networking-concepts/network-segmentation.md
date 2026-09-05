# Network Segmentation

Network Segmentation

In the previous chapter, the defense strategy emphasized the critical role of a robust security policy. Building upon this foundation, the next phase involves ensuring the security of the network infrastructure. To kickstart this process, the network must be segmented and isolated to establish effective intrusion prevention measures. It is crucial for defenders to possess comprehensive knowledge about network segmentation best practices, encompassing both physical and virtual dimensions, as well as remote access protocols. Even for companies not entirely reliant on cloud services, considerations for hybrid scenarios are vital, emphasizing the necessity for stringent security controls to fortify defensive security stances. At the core of this framework lies the network infrastructure security, acting as a cornerstone for the entire network security ecosystem. The upcoming chapter will journey into various pertinent subjects including topics such as:

* Defense in Depth
* Physical Network Segmentation
* Strategies for Securing Remote Network Access
* Virtual Network Segmentation Techniques
* Critical Aspects of Hybrid Cloud Network Security

Defense in Depth/Layered Security Approach

You might think this is an outdated method that no longer meets today’s critical security standards and demands, but the fact is that it still very much applies, even if you’re not using the same technologies as before. The core concept behind the defense in depth approach is to create multiple layers of protection, each with its own set of security controls and policy enforcements, designed to slow down an attack. The sensors within these layers helps detect unusual activities, enabling you to interrupt the attack before it can fully unfold – essentially breaking the cyberattack kill chain.

However, to implement a defense in depth strategy for today’s moder networking and computing needs, it’s essential to move beyond just the physical layer and think in terms of protection layers based on entry points and attack vectors. The diagram below illustrates how defense in depth is applied today. This shift requires abandoning the traditional mindset that links defense in depth with outdated methods and recognizing that its fundamental principle establishing multiple protective layers of security – is still crucial in today’s rapidly changing threat landscape; therefore, it’s imperative to adopt this apoproach to modern technologies and considering potential vulnerabilities at avarious entry points so that you can better protect and guide client organizations to better strengthen their cybersecurity postures and protect their systems and data more effectively against evolving threats. Continuously reassessing and refining the defense in depth strategy is vital to keeping up with the changing threat landscape and for maintaining a strong and resilient security framework.

![A diagram of a computer network

Description automatically generated](<../../.gitbook/assets/0 (52).png>)

The attacker has broad access to various resources, allowing them to target the infrastructure and services, documents and data in transit, and endpoints. This underscores the need to increase the attacker’s cost in ever possible scenario. Below, we will break down this diagram in the following sections.

**Security Components of Network Infrastructure**

Attackers can significantly disrupt a company’s productivity by targeting its network infrastructure and the services, resources, and data it provides. Even in an on-premise-only scenario, you will still have critical services managed by local IT shops and teams. For example, a publicly-facing database server is a service that stores vital data used by users, and if it becomes unavailable, it directly impacts productivity, leading to negative financial consequences, and more, for the client organization.

To safeguard against such threats, you must first enumerate all the services the target or client organization offers to its end users and partners, then identify the possible attack vectors. Once these vectors are identified, implement strong security controls to mitigate the associated vulnerabilities. This could include enforcing compliance through patch management, securing servers with appropriate security policies, controls, baseline, and hardening management, implementing network isolation, maintaining clean backups, and more. These measures are only a few options that can aid in acting as layers of extra protection within the infrastructure and services domain. Additional layers of protection is necessary for other areas of the infrastructure, as well, to ensure comprehensive security measures are in place to thwart any emerging or ongoing attacks against the infrastructure.

The same diagram also includes cloud computing, specifically _**Infrastructure-as-a-Service (IaaS)**_, as this company utilizes virtual machines hosted in the cloud. If you’ve already performed threat hunting and threat modeling and implemented security controls based off of those findings for you on-premises environment, it’s now essential to reassess the impact of integrating cloud connectivity with your on-premises infrastructure. Creating a hybrid environment, you get the best of both worlds. It allows you to re-evaluate the threats, potential entry points, and how these points might be exploited while protecting the infrastructure at the same time. This exercise in futility often reveals the need for additional security controls, as layered security and defense in depth approaches often piggyback off one security control to another prompting for further secure implementations.

The infrastructure security strategy should aim to reduce the number and severity of identified vulnerabilities, minimize its exposure time, and increase the difficulty and cost of exploitation. By employing a layered security approach, you can achieve these objectives for your clients efficiently and effectively.

**Data In Transit**

While the diagram specifically mentions documents, this concept actually applies to any type of data, which is often vulnerable when in transit between locations. It’s crucial to use encryption to protect data during transit, and most importantly, it’s best to not assume that encryption is only necessary for public networks; it should also be implemented within internal networks.

For instance, all segments within the on-premises infrastructure illustrated in the previous diagram should employ network-level encryption, such as IPSec. If you need to transmit data across networks, ensure the entire transmission path is encrypted, and once the data reaches its destination, secure it with encryption at rest in storage.

In addition to encryption, it’s essential to implement other security controls, such as monitoring and access control, as depicted in the following diagram:

![A diagram of a computer data

Description automatically generated](<../../.gitbook/assets/1 (39).png>)

This approach essentially adds multiple layers of protection and detection, which is the core principle of a layered security strategy defense and defense in depth strategy. This mindset should guide you to think about safeguarding the assets you strive to protect.

Let us consider another example illustrated in the following diagram: A document was encrypted at rest on an on-premises server. It then traveled across the internet, where the user was authenticated in the cloud, and the encryption remained intact all the way to its destination, the mobile device, where it was al encrypted at rest in local storage.

![A diagram of a cloud computing system

Description automatically generated](<../../.gitbook/assets/2 (34).png>)

This diagram illustrates that in a hybrid scenario, the attack vector will shift, requiring you to consider the entire end-to-end communications path. To effectively identify potential threats and mitigate them, it’s essential to evaluate every point along this communications pathway.

**Endpoint Layered Security Strategies**

When planning defense in depth for endpoints, it’s crucial to think beyond just computers. Today, an endpoint can be any device that consumes data. The application determines which devices will be supported, and by working closely with your development team, you should be aware of the supported devices. Most applications are generally available for both mobile devices and computers, but some may extend accessibility to wearable devices like Fitbits. Regardless of the device type, you must conduct thorough threat modeling to identify all potential attack vectors and plan mitigation strategies accordingly.

Some key countermeasures for securing endpoints include:

* Separation of corporate and personal data/apps (isolation)
* Use of TPM (Trusted Platform Module hardware protections)
* OS hardening and secure baseline implementations
* Storage encryption

**NOTE: Endpoint protections should cover both corporate-owned devices and BYOD (Bring Your Own Device) scenarios. For more information on a vendor-agnostic approach to BYOD, you can read this article: BYOD Article Published at ISSA Journal at&#x20;**_**(Source:**_ [_**https://blogs.technet.microsoft.com/yuridiogenes/2014/03/11/byod-article-published-at-issa-journal/**_](https://blogs.technet.microsoft.com/yuridiogenes/2014/03/11/byod-article-published-at-issa-journal/)_**)**_

**Segmenting Physical Layer Endpoints**

One of the biggest challenges I’ve seen for defenders in network segmentation efforts is obtaining an accurate view of the current network implementations. Often as the network expands to meet growing demands, its security features are not updated accordingly, and/or are simply forgotten about. For large corporations, this can mean rethinking and potentially rearchitecting the entire network from scratch.

To establish effective physical network segmentation, start by understanding the logical distribution of resources based on your client organizational needs. This dispels the myth that a one-size-fits-all approach works, which it generally does not. Each network scenario should be analyzed individually, and segmentation should be planned based on resource demand and logical access.

For small- and medium-sized organizations, it might be simpler to group resources by department – such as financial, human resources, and operations. In such cases, creating a Virtual Local Area Network (VLAN) for each department and isolating resources accordingly can enhance both performance and network stability.
