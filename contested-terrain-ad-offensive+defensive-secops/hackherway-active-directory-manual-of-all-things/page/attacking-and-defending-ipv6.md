# Attacking and Defending IPv6

Attacking and Defending IPv6

Nearly all networked devices use the Internet Protocol (IP) for their communications. IP version 6 (IPv6) is the current version of IP and provides advantages over the legacy IP version 4 (IPv4). Most notably, the IPv4 address space is inadequate to support the increasing number of networked devices, requiring routable IP addresses, whereas IPv6 provides a vast address space to meet current and future needs.

While some technologies, such as network infrastructure, are more affected by IPv6 than others, nearly all networked hardware and software are affected in some way as well. As a result, IPv6 has broad impact on cybersecurity that organizations should address with due diligence.

IPv6 security issues are quite similar to those from IPv4. That is, the security methods used with IPv4 should typically be applied to IPv6 with adaptations as required to address the differences with IPv6. Security issues associated with an IPv6 implementation will generally surface in networks that are new to IPv6, or in early phases of the IPv6 transition.

These networks lack maturity in IPv6 configurations and security tools. More importantly, they lack overall experience by the administrators in the IPv6 protocol. Dual stacked networks (that run both iPv4 and IPv6 simultaneously) have additional security concerns, so further countermeasures are needed to mitigate these risks due to the increased attack surface of having both IPv4 and IPv6.

Today, many networks continue to transition to full IPv6-based networks, moving from legacy IPv4 to IPv6 only. During this transition, IPv4 is continued to be used, and many networks will operate dual stacked (running both IPv4 and IPv6 protocols simultaneously) as an interim solution toward an IPv6-only end state; however, operating dual stack increases operational burden and the attack surface. System owners and administrators should implement cybersecurity mechanisms on both IP protocols to protect the network.

The network architecture and knowledge of those who configure and manage an IPv6 implementation have a big impact on the overall security of the network. As a result, the actual security posture of an IPv6 implementation can vary.

IPv6 Security Concerns and Recommendations

To get a good start in implementing IPv6 networks and having a firm understanding of their potential security concerns, some recommendations include the following:

Auto-Configuration

Stateless address auto-configuration (SLAAC) is an automatic method to self-assign an IPv6 address to a host. In some cases, such as for important servers, static addresses may be preferred, but allowing devices to automatically self-assign or request an IPv6 address dynamically is easier in most cases. In SLAAC, a host configures its own network address based on a network prefix received from a router. The assigned IPv6 address incorporates Media Access Control (MAC) address information from the network interface and may allow for host identification via interface ID, Network Interface Card (NIC), or host vendor. This, in turn, leads to privacy concerns by linking movements to a specific device and deducing an individual associated with that equipment, as well as exposing the types of equipment used in a network.

It is recommended that assigning addresses to hosts via a Dynamic Host Configuration Protocol (DHCP) version 6 server to mitigate SLAAC privacy issues. Alternatively, this issue can also be mitigated by using a randomly generated interface ID _(RFC 4941 – Privacy Extensions for Stateless Address Auto-Configuration in IPv6)_ that changes over time, making it difficult to correlate activity while still allowing network defenders requisite visibility.

Automatic Tunnels

Tunneling is a transition technique that allows one protocol to be transported, or tunneled, within another protocol. For example, a tunnel can be used to transport IPv6 packets within IPv4 packets. A network might use tunneling for its Internet connection, and some devices or apps might be designed to tunnel IPv6 traffic. Some operating systems will automatically establish an IPv6 tunnel when a client connects to a server, potentially causing an unwanted entry point to the host.

Unless transition tunnels are required, it is recommended to avoid tunneling to reduce complexities and the attack surface. Configure perimeter security devices to detect and block tunneling protocols that are used as transition methods. In addition, disable tunneling protocols (6to4, ISATAP, Teredo) on all devices where possible. Tunneling protocols can be allowed if they are required during a transition, but they should be limited to only approved systems where their usage is well understood and where they are explicitly configured.

Dual Stack

A dual stack environment exists when devices run both IPv4 and IPv6 protocols simultaneously. This is a preferred method for staged IPv6 deployment, but it can be more expensive and tends to increase the attack surface. This approach provides a transition method to IPv6 because it allows devices to use IPv6 for communications that do not support IPv6. As IPv6 deployments increase, a dual stack environment will transition to IPv6-focused operations by increasing the use of IPv6 and decreasing the use of IPv4.

When deploying a dual stack network, organizations should implement IPv6 cybersecurity mechanisms that achieve parity with their IPv4 mechanisms or better. For any security mechanism implemented in IPv4, a corresponding security mechanism should be implemented for IPv6, with the IPv6 mechanisms addressing any differences for IPv6. For example, firewall rules that filter higher level protocols (such as TCP or UDP) should be applied to both IPv6 an
