# README

## Networking & Cybersecurity

Welcome to the world of Networking.\
An ongoing curated collection of awesome software, libraries, frameworks, talks & videos, best practices, learning tutorials and important practical resources about networking in cybersecurity. Thanks to all contributors, you're awesome and wouldn't be possible without you! Our goal is to build a categorized community-driven collection of very well-known resources.

### Network Foundations

* [Computer networking](https://www.cisco.com/c/en/us/solutions/enterprise-networks/what-is-computer-networking.html) refers to connected **computing devices** (such as laptops, desktops, servers, smartphones, and tablets) and an ever-expanding array of **IoT devices** (such as cameras, door locks, doorbells, refrigerators, audio/visual systems, thermostats, and various sensors) that communicate with one another.

![network](https://github.com/paulveillard/cybersecurity-networking/blob/main/img/network.png)

### TCP/IP Protocols

{% hint style="info" %}
Note: Links without description are official RFCs from the Internet Engineering Task Force (IETF).
{% endhint %}

*   DNS

    * [DOMAIN NAMES - IMPLEMENTATION AND SPECIFICATION](https://www.ietf.org/rfc/rfc1035.txt)

    ![dns](https://github.com/paulveillard/cybersecurity-networking/blob/main/img/dns.png)

    > DNS, or the Domain Name System, translates human readable domain names (for example, www.amazon.com) to machine readable IP addresses (for example, 192.0.2.44).
*   DHCP

    * [DYNAMIC HOST CONFIGURATION PROTOCOL](https://www.ietf.org/rfc/rfc2131.txt)

    ![dhcp](https://github.com/paulveillard/cybersecurity-networking/blob/main/img/dhcp.png)

    Dynamic Host Configuration Protocol, or DHCP, is used to provide quick and centralized management of IP addresses and other TCP/IP settings on your network. These are things like host IP address, subnet mask, DNS settings, default gateway address, and so on (IP configuration settings). When you power on your computer, a DHCP server likely provides these IP configuration settings to you. Even if you don’t have a stand-alone DHCP server, your default gateway likely has its own DHCP server feature.

    DHCP eliminates the need for manually assigning IP addresses to devices. DHCP server port is 67 and client port is 68. It is a client–server protocol which uses UDP.
*   FTP

    * [FILE TRANSFER PROTOCOL (FTP)](https://www.ietf.org/rfc/rfc959.txt)

    ![ftp](https://github.com/paulveillard/cybersecurity-networking/blob/main/img/ftp.png)
* HTTP
  * [Hypertext Transfer Protocol -- HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
  * [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.ietf.org/rfc/rfc7540.txt)
* UDP
  * [User Datagram Protocol](https://www.ietf.org/rfc/rfc768.txt)
* TCP
  * [TRANSMISSION CONTROL PROTOCOL](https://www.ietf.org/rfc/rfc793.txt)
* IP
  * [INTERNET PROTOCOL](https://tools.ietf.org/html/rfc791)
  * [Internet Protocol, Version 6 (IPv6) Specification](https://www.ietf.org/rfc/rfc2460.txt)
* Telnet
  * [TELNET PROTOCOL SPECIFICATION](https://www.ietf.org/rfc/rfc854.txt)
* SSH
  * [The Secure Shell (SSH) Protocol Architecture](https://www.ietf.org/rfc/rfc4251.txt)
* NAT
  * [The IP Network Address Translator (NAT)](https://www.ietf.org/rfc/rfc1631.txt)

### Courses

* [Cisco Networking Academy Courses](https://www.netacad.com/courses/networking) - Various networking courses (Essentials, CCNA, CCNP, etc.).
* [CBT Nuggets](https://www.cbtnuggets.com/) - Courses on various topics (Cisco, Juniper, CompTIA, etc.).
* [ipSpace](https://www.ipspace.net/) - Courses and webinars on various network topics.
* [GNS3 Academy](https://academy.gns3.com/) - Courses related to networking with GNS3.
* [The Complete Networking Fundamentals Course](https://www.udemy.com/complete-networking-fundamentals-course-ccna-start/) - Popular Networking Essentials course on Udemy.

### Tutorials

* [Networking (Eli the Computer Guy)](https://www.youtube.com/watch?v=rL8RSFQG8do\&list=PLF360ED1082F6F2A5) - YouTube tutorial series.
* [Wireshark Tutorial for Beginners (TheNewBoston)](https://www.youtube.com/watch?v=flDzURAm8wQ\&list=PL6gx4Cwl9DGBI2ZFuyZOl5Q7sptR7PwYN)
* [MikroTik WinBox Manual](https://wiki.mikrotik.com/wiki/Manual:Winbox) - Official MikroTik WinBox manual.

### Books

* [Computer Networking: A Top-Down Approach (7th Edition)](https://www.amazon.com/Computer-Networking-Top-Down-Approach-7th/dp/0133594149)
* [Internetworking with TCP/IP Volume One (6th Edition)](https://www.amazon.com/Internetworking-TCP-IP-One-6th/dp/013608530X)
* [Network Security Essentials: Applications and Standards (6th Edition)](https://www.amazon.com/Network-Security-Essentials-Applications-Standards/dp/013452733X/)
* [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/) - Free guide to socket programming.
* [Red Hat Enterprise Linux 7 Networking Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/networking_guide/Red_Hat_Enterprise_Linux-7-Networking_Guide-en-US.pdf)
* [Practical Packet Analysis (3rd Edition)](https://nostarch.com/packetanalysis3)
* [Attacking Network Protocols](https://nostarch.com/networkprotocols) - A Hacker's Guide to Capture, Analysis, and Exploitation by James Forshaw.
* [Cisco Press](https://www.ciscopress.com/) - Cisco-authorized books and certification guides.

### Software and Tools

* [Wireshark](https://www.wireshark.org/) - Network protocol analyzer.
* [tcpdump](http://www.tcpdump.org/) - Command-line packet analyzer.
* [Nmap](https://nmap.org/) - Network discovery and security auditing.
* [Zenmap](https://nmap.org/zenmap/) - Nmap GUI.
* [GNS3](https://gns3.com/) - Network simulator.
* [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) - Cisco network simulation tool.
* [pfSense](https://www.pfsense.org/) - Open source firewall/router distribution.
* [WinBox](https://mikrotik.com/download) - MikroTik RouterOS GUI.
* [Online nslookup](https://www.nslookup.io/) - Online DNS client.
* [Online whois](https://whois.domaintools.com/) - Whois lookup tool.
* [OUI Lookup Tool](https://www.wireshark.org/tools/oui-lookup.html) - MAC vendor lookup.
* [Draw.io](https://github.com/jgraph/drawio-desktop) - Network diagram software.

### Certifications

* [Cisco certifications](https://www.cisco.com/c/en/us/training-events/training-certifications/certifications.html)
* [MikroTik certified training programs](https://mikrotik.com/training/about)
* [Juniper Certification Tracks](https://www.juniper.net/us/en/training/certification/certification-tracks/)
* [CompTIA Network+](https://certification.comptia.org/certifications/network)

### Miscellaneous

* [Network Analysis (awesome list)](https://github.com/briatte/awesome-network-analysis)
* [Software Defined Networks (SDN) (awesome list)](https://github.com/sdnds-tw/awesome-sdn)
* [Reddit Networking](https://www.reddit.com/r/networking/)
* [Network Engineering Stack Exchange](https://networkengineering.stackexchange.com/)
* [Server Fault](https://serverfault.com/)

### Network Design Resources

* [Cisco Design Zone](https://www.cisco.com/c/en/us/solutions/design-zone.html#~stickynav=1)
* [Cumulus Networks Validated Design Guides](https://cumulusnetworks.com/learn/web-scale-networking-resources/?validated-design-guides)
* [Juniper Solution Center](https://www.juniper.net/documentation/en_US/release-independent/solutions/information-products/pathway-pages/solutions/index.html)

### Network Implementation

#### Routing

* [Free Range Routing](https://frrouting.org/) - IP routing protocol suite (BGP, IS-IS, LDP, OSPF, PIM, RIP).
* [VyOS](https://vyos.io/) - Open source network operating system.

#### SD-WAN

* [Silver Peak](https://www.silver-peak.com/) - SD-WAN solution (commercial).

#### Switching

* [snabb](https://github.com/snabbco/snabb) - Fast packet networking toolkit.

#### VPN

* [PiVPN](https://www.pivpn.io/) - Simple OpenVPN setup for Raspberry Pi.

#### Network Services

* [Pi-Hole](https://pi-hole.net/) - Network-wide ad blocking.

#### Network Simulators and Traffic Generators

* [GNS3](https://www.gns3.com/) - Network emulator combining virtual and real devices.
* [Mininet](http://mininet.org/) - Instant virtual network.
* [WANem](http://wanem.sourceforge.net/) - Wide Area Network emulator.
* [Ostinato](https://ostinato.org/) - Packet crafter and traffic generator.
* [SIPp](http://sipp.sourceforge.net/index.html) - SIP traffic generator.
* [StarTrinity SIP Tester™](https://startrinity.com/VoIP/SipTester/SipTester.aspx) - VoIP testing tool.
* [Multi-Generator (mgen)](https://github.com/USNavalResearchLaboratory/mgen) - IP network performance testing.
* [Network-Conditions-Emulator](https://github.com/marty90/Network-Conditions-Emulator) - Simulate bandwidth/delay/loss.
* [snabb](https://github.com/snabbco/snabb) - Packet networking toolkit.
* [vqfx10k-vagrant](https://github.com/juniper/vqfx10k-vagrant) - Vagrant files for Juniper virtual QFX.
* [Packet Communication Investigator](https://github.com/michoo/pci) - Import network traffic into a graphtool for analysis.
* [SafePcap](https://omnipacket.com/safepcap) - GDPR and NISTIR 8053 compliance for PCAP files.
* [Arkime](https://github.com/arkime/arkime) - Store and index network traffic (PCAP).
* [pyNTM](https://pyntm.readthedocs.io/en/latest/index.html) - Network traffic modeler in Python 3.

### Network Operations

#### Network Change Management

* [Batfish](https://github.com/batfish/batfish) - Network configuration analysis.
* [Oxidized](https://github.com/ytti/oxidized) - Device configuration backup (RANCID replacement).
* [Netshot](http://www.netfishers.onl/netshot) - Configuration and compliance management.
* [Jazigo](https://github.com/udhos/jazigo) - Retrieve configurations for multiple devices.
* [fetchconfig](https://github.com/udhos/fetchconfig) - Perl script for retrieving device configurations.
* [sweet](https://github.com/AppliedTrust/sweet) - Config backups and change alerts.
* [stockpiler](https://github.com/lykinsbd/stockpiler) - Gather configurations into a local Git repo.

### Network Automation

* [Napalm](https://napalm-automation.net/) - Vendor-neutral API to network devices.
* [netmiko](https://github.com/ktbyers/netmiko) - Simplify SSH connections to devices.
* [trigger](https://github.com/trigger/trigger) - Python network automation toolkit.
* [Ansible](https://github.com/ansible/ansible) - IT automation platform (SSH-based).
* [nornir](https://github.com/nornir-automation/nornir) - Pluggable multi-threaded automation framework.
* [CNaaS-NMS](https://github.com/SUNET/cnaas-nms) - Campus Network-as-a-Service management.
* [pyats](https://developer.cisco.com/pyats/) - Stateful device validation for network engineers.
* [Itential](https://www.itential.com/) - Low-code automation (commercial).
* [AWX](https://github.com/ansible/awx) - Upstream project for Ansible Tower.
* [Unimus](https://unimus.net/) - Network automation and config management (commercial).

### Network Monitoring

* [perfSONAR](https://www.perfsonar.net/) - Federated network measurement toolkit.
* [UDPing](https://github.com/yahoo/UDPing) - Measure latency and packet loss.
* [Vaping](https://github.com/20c/vaping) - Alternative to smokeping.
* [veryflow](https://www.veriflow.net/) - Continuous network verification.
* [Forward Networks](https://www.forwardnetworks.com/) - Network behavior analysis (commercial).
* [ToDD](https://github.com/toddproject/todd) - Distributed testing-on-demand.
* [pmacct](http://www.pmacct.net/) - Passive network monitoring tools (Netflow/IPFIX).
* [LibreNMS](https://www.librenms.org/) - Auto-discovery and alerting.
* [Observium](https://observium.org/) - Auto-discovering monitoring platform.
* [Elastiflow](https://github.com/robcowart/elastiflow) - Netflow collector and reporting.

### Security Monitoring

* [cPacket](https://www.cpacket.com/) - Performance monitoring (commercial).
* [Proxmox Mail Gateway](https://www.proxmox.com/en/proxmox-mail-gateway) - Email security solution.
* [FastNetMon](https://fastnetmon.com/) - DDoS detection (open source/commercial).
* [PyREBox](https://github.com/Cisco-Talos/pyrebox) - Reverse engineering sandbox based on QEMU.
* [Canary](https://canary.tools/) - Honeypot solution (commercial).
* [CanaryTokens](https://canarytokens.org/generate) - Free honeytoken generator.
* [Malcolm](https://github.com/idaholab/Malcolm) - Network traffic analysis suite for PCAP and Zeek logs.
* [Zeek](https://zeek.org/) - Network security monitoring.
  * [zeek2es](https://github.com/corelight/zeek2es) - Zeek log to Elastic/OpenSearch converter.

### Network Inventory

* [phpipam](https://phpipam.net/) - Open-source IPAM.
* [nsot](https://github.com/dropbox/nsot) - Network Source of Truth (IPAM/inventory).
* [netbox](https://github.com/digitalocean/netbox) - IPAM and DCIM tool.
* [ipfabric](https://ipfabric.io/product/network-mapping) - Topology mapping & visualization (commercial).
* [drawthe.net](https://github.com/cidrblock/drawthe.net) - Draw network diagrams from text files.

### Networking Labs

* [VIRL](https://learningnetworkstore.cisco.com/virlfaq) - Cisco Virtual Internet Routing Lab.
* [dCloud](https://dcloud.cisco.com/) - Scripted cloud environments (free).
* [Cisco DevNet Labs / Sandbox](https://developer.cisco.com/site/sandbox/) - Cisco sandboxes and labs.

## Related resources

### DevNet Tools

* [Celery](http://www.celeryproject.org/) - Asynchronous task queue.
* [Ajenti](https://ajenti.org/) - Remote Linux management web UI.
* [ProxMox Virtualization Platform](https://www.proxmox.com/en/proxmox-ve) - KVM + LXC virtualization platform.
* [ops\_tcpdump\_handler](https://github.com/cerner/ops_tcpdump_handler) - Chef cookbook for network testing.
* [chromaterm](https://github.com/hSaria/ChromaTerm) - Terminal coloring tool.
* [telnetmyip.com](https://telnetmyip.com/) - Returns source IP info in JSON.
* [icanhaztraceroute.com](https://icanhaztraceroute.com/) - Returns a traceroute to your source IP.
* [Who is my ISP?](https://www.whoismyisp.org/) - Shows ISP for an IP.
* [NsLookup.io](https://www.nslookup.io/) - Shows DNS records for a domain.
* [netshoot](https://github.com/nicolaka/netshoot) - Docker/Kubernetes network troubleshooting container.

### DevNet Monitoring

* [netdata](https://github.com/firehol/netdata) - Real-time performance and health monitoring.
* [Grafana](https://grafana.com/) - Time series analytics platform.
* [monit](https://mmonit.com/monit/) - System monitoring and maintenance tool.
* [Prometheus](https://prometheus.io/) - Monitoring and alerting toolkit.
* [sensu](https://sensuapp.org/) - Monitoring platform (open source/commercial).
* ELK Stack:
  * [Elasticsearch](https://github.com/elastic/elasticsearch)
  * [LogStash](https://github.com/elastic/logstash)
  * [Kibana](https://github.com/elastic/kibana)
* [Graylog](https://www.graylog.org/) - Log parsing and enrichment (commercial / free tier).

#### DevNet Knowledgebase

* [ITGlue](https://www.itglue.com/) - IT documentation solution (commercial).

#### DevNet Inventory

* [Snipe IT](https://snipeitapp.com/) - Open source asset management tool.

#### Knowledge Resources

* [Packet Pushers Podcast](https://packetpushers.net/) - Data networking podcast.
* [Risky Business Podcast](https://risky.biz/) - Security news and commentary.
* [Software Gone Wild Podcast](https://www.ipspace.net/Podcast/Software_Gone_Wild/) - Networking architectures and technologies.
* [Cisco DevNet Basics](https://developer.cisco.com/video/net-prog-basics) - Network programmability basics.
* [Cisco Tools](https://www.cisco.com/c/en/us/support/web/tools-catalog.html) - Cisco-maintained tools list.

### License

MIT License & [cc](https://creativecommons.org/licenses/by/4.0/) license

[![Creative Commons License](../../.gitbook/assets/88x31.png)](http://creativecommons.org/licenses/by/4.0/)\
This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

To the extent possible under law, [Paul Veillard](https://github.com/paulveillard/) has waived all copyright and related or neighboring rights to this work.
