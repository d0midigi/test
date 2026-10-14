# Introduction to Practical Ethical Hacking and Networking

### Intro <a href="#intro" id="intro"></a>

**Ethical hackers** are _allowed and hired_ to try to hack into an organization by assessing its security posture.

#### Network Assessments <a href="#network-assessments" id="network-assessments"></a>

* **External** Pentest - hacking/assessing from outside of the organization's network
  * OSINT (Open-Source Intelligence) - organization's users, web login pages, emails, etc
  * Vulnerability scanning from the Internet
  * Pentest takes 32-40 hours on average and 8-16 hours for report writing
* **Internal** Pentest - assessing from the inside of the organization's network
  * Active Directory attacks
  * Pentest takes 32-40 hours on average (longer if bigger scope ) and 8-16 hours for report writing
* **Web Application** Pentest - assessing the web application security
  * Web-based attacks & [OWASP](https://owasp.org/) guidelines
  * Pentest takes a minimum of 32-40 hours and 8-16 hours for report writing
* **Wireless** Pentest - assessing the wireless network security
  * Guest, WPA2-PSK, WPA2 Enterprise - pentesting with external Wireless adapters
  * Takes 4-8 hours per SSID and 2-4 for report writing
* **Physical** & Social Engineering Pentest - assessing an organization's physical security
  * On site badges cloning, social engineering, picking locks, etc - depends on the client's goal
  * Phishing, Vishing, Smishing campaigns
  * Lasts 16-40 hours and 4-8 for report writing
* Mobile Pentesting, IoT Pentesting, Red Team Engagements (weeks, months), Purple Team Engagements, Car Hacking, etc

⬇️

#### Report <a href="#report" id="report"></a>

* Good technical skills, report writing, communication and presentation skills
* Report withing a week
  * Executive Summary - a non-technical report
  * Technical findings section - for the technicians
  * Recommendations for remediation - clear to both executives and tech staff

⬇️

#### Debrief <a href="#debrief" id="debrief"></a>

* The client (both technical and executive staff) is taken through the report findings.
* Client can ask questions and address any concerns
* Release the final report

***

### Networking <a href="#networking" id="networking"></a>

> 🔗 [Networking Fundalmentals - Practical Networking Youtube](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi)

Copy

```
ifconfig
ipconfig /all
```

➡️ **Layer 3**

**IP** (Internet Protocol) addresses - identify/locate devices on a network, on the layer 3 OSI model.

* **IPv4 Address**: `192.168.1.50` - decimal notation
  * 4 octets of 8 bits = 32bits = 4bytes
  *   Total IPv4 addresses

      232=4.294.967.296232=4.294.967.296
* **IPv6 Address**: `fe80::ab4c:8503:3248:9993%6` - hexadecimal notation
  * 8 groups of 4 hex digits = 128bits
  *   Total IPv4 addresses

      2128=3.4×10382128=3.4×1038

➡️ **Layer 2**

**MAC** (Media Access Control) access is a unique identifier/hardware address given to NICs (network interface controllers). Used at the layer 2 OSI model (data link).

* **MAC Address**: `00:50:56:C0:00:01` - hexadecimal notation
  * 6 pairs of hex digits = 48 bits
  * First 3 pairs = NIC manufacturer
  * local network

➡️ **Layer 4**

**TCP** (Transmission Control Protocol)

* Connection oriented, high reliability, guaranteed delivery
* [3 Way Handshake](https://www.guru99.com/tcp-3-way-handshake.html): `SYN` ➡️ `SYN ACK` ➡️ `ACK` = Connection established

**UDP** (User Datagram Protocol)

* Connectionless, lightweight, no acknowledgement/reliability, real-time apps

#### **Common TCP Ports** <a href="#common-tcp-ports" id="common-tcp-ports"></a>

TCP PortsService

21 / 990

**FTP** (File Transfer Protocol) / **FTPS** (FTP over SSL/TLS)

22

**SSH** (Secure Shell)

23

**Telnet**

25

**SMTP** (Simple Mail Transfer Protocol)

53

**DNS** (Domain Name System)

80 / 443

**HTTP** / **HTTPS** (Hypertext Transfer Protocol over SSL)

110

**POP3** (Post Office Protocol)

123

**NTP** (Network Time Protocol)

139 / 445

**NetBIOS** / **SMB, Samba** (Server Message Block)

143

**IMAP** (Internet Message Access Protocol)

389

**LDAP** (Lightweight Directory Access Protocol)

1433-1434

Microsoft Sql Server

3306

**MySQL**

3389

**RDP** (Terminal Server)

#### **Common UDP Ports** <a href="#common-udp-ports" id="common-udp-ports"></a>

UDP PortsService

53

**DNS** (Domain Name System)

67 / 68

**DHCP** (Dynamic Host Configuration Protocol)

69

**TFTP** (Trivial File Transfer Protocol)

161

**SNMP** (Simple Network Management Protocol)

389

**LDAP** (Lightweight Directory Access Protocol)

#### **OSI Model** <a href="#osi-model" id="osi-model"></a>

> 🔗 [guru99 - OSI Model Layers](https://www.guru99.com/layers-of-osi-model.html)
>
> 🔗 [SMB University - Cisco Networking Fundamentals](https://www.cisco.com/c/dam/global/fi_fi/assets/docs/SMB_University_120307_Networking_Fundamentals.pdf)

➡️ **OSI** (Open Systems Interconnection) model is a conceptual framework that offers a 7 layers structured method for communication system functions and network protocols.

![](https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-9e29a38bb57f3a2d081de8640e39b9bdd775f068%252FLayersofOSI1.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=efef547a\&sv=2)OSI Model - guru99.com

_**P**lease_ ➡️ 1. Physical

* data cables

_**D**o_ ➡️ 2. Data Link

* Switching, MAC

_**N**ot_ ➡️ 3. Network

* IPs, Routing

_**T**hrow_ ➡️ 4. Transport

* TCP/UDP

_**S**ausage_ ➡️ 5. Session

* Session management

_**P**izza_ ➡️ 6. Presentation

* Media files

_**A**way_ ➡️ 7. Application

* HTTP, SMTP, apps

![](https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-e6c65033206887476514fc6534501d7e89ad4ece%252Foriginal-seven-layers-of-osi-model.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=17a1398\&sv=2)Seven layers of OSI model - community.fs.com

![](https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-be4e727e6da49f01b2dc8e13e6cb92c184dc3a22%252Fosi-attacks.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=8fd01644\&sv=2)OSI Model Cyber Attacks - byos.io

#### Subnetting <a href="#subnetting" id="subnetting"></a>

> 🔗 [Subnetting Mastery - Practical Networking Youtube](https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE)
>
> 🔗 [Subnet Guide - TCM](https://drive.google.com/file/d/1ETKH31-E7G-7ntEOlWGZcDZWuukmeHFe/view)

Subnetting consists of dividing a network into multiple subnetworks/subnets.

* Subnet - own range of IP addresses
* **NAT** (Network Address Translation) prevents from running out of IPv4 addresses

**CIDR** (Classless Inter-Domain Routing) notation

* `192.168.1.0/24` - `/xx` is the network prefix length (network portion bits number)
  * 24 bits = network portion (_turned on bits_)
  * (remaining) 8 bits = host portion
  *   Total hosts

      (28=256)−2=254(28=256)−2=254
  * Subnet Mask = `255.255.255.0`
* Network ID - First Address `192.168.1.0`
* Broadcast - Last Address `192.168.1.255`

> 🔗 [Subnet Calculator - vultr.com](https://www.vultr.com/resources/subnet-calculator/)
>
> 🔗 [Subnet Calculator - mxtoolbox.com](https://mxtoolbox.com/subnetcalculator.aspx)
>
> 🔗 [CIDR to IPv4 Conversion](https://www.ipaddressguide.com/cidr)

![](https://blog.syselement.com/tcm/~gitbook/image?url=https%3A%2F%2F1178537843-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F2KUxfxUFmy000PDT7MtM%252Fuploads%252Fgit-blob-6577180961faf7f0c77658d01e092b778cca33e5%252F2023-06-13_13-16-35_56.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=e6454e00\&sv=2)TCM Subnetting Sheet
