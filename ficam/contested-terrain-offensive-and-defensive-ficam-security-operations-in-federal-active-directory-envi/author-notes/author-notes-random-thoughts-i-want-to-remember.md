# Author Notes - Random Thoughts I Want to Remember

<details>

<summary><strong>Outrageous RFCs</strong></summary>

The Directory is a "collection of open systems cooperating to provide directory services" \[X.500]. A directory user, which may be a human or non-person entity (NPE), accesses the Directory through a client (or Directory User Agent (DUA)). The client, on behalf of the directory user's authorized and authenticated login, interacts with one or more servers (or Directory System Agents (DSA)). Clients therefore interact with servers using a directory access protocol.\
This section details the protocol elements of the Lightweight Directory Access Protocol (LDAP), along with its semantics. Following the description of protocol elements, it describes the way in which the protocol elements are encoded and transferred across infrastructure.\
Key Words\
Transport Connection. Refers to the underlying transport services used to carry the protocol exchange over the network, as well as the associations established by these services.\
SASL Layer. Refers to Simply Authentication and Security Layer (SASL) services used in providing security services, as well as the associations established by these services.\
LDAP Message Layer. Refers to the LDAP Message Protocol Data Unit (PDU) services used in providing directory services, as well as the associations established by these services.\
LDAP Session. Refers to combined services (transport connection, TLS layer, SASL layer, LDAP message layer) as well as their associations.\
LDAP Protocol Model\
The general model adopted by this protocol is one of clients performing protocol operations against network servers, both on-premises an, cloud, and hybrid environments. In this model, a client transmits a protocol request describing the operation to be performed to a server. The server is then responsible for performing the necessary operation(s) in the Directory. Upon completion of an operation, the server typically returns a response containing appropriate data to the requesting client.\
Protocol operations are generally independent of one another. Each operation is processed as an atomic action, leaving the directory in a consistent state.\
Although servers are required to return responses whenever such responses are explicitly defined in the protocol to do so, there is no mandatory requirement for synchronous behavior on the part of either clients or servers. Requests and responses for multiple operations generally may be exchanged between a client and a server in any order. If required, synchronous behavior may be controlled by client applications.\
Operation and LDAP Message Layer Relationship\
Protocol operations are exchanged at the LDAP message layer. When the transport connection is closed, any uncompleted operations at the LDAP message layer are then abandoned (when possible) or are completed without transmission of the response (when abandoning them is not possible). Also, when the transport connection is closed, the client must not assume that any uncompleted update operations have either succeeded or failed.\
Mind Control and Cognitive Networking\
RFC 1097 (1989) - TELNET Subliminal-Message Option: A protocol allowing server administrators to inject subconscious visual frames directly into a user's terminal to subtly influence their behavior during a session.\
Classic Joke and Experimental RFCs\
RFC 1149: Standard for the Transmission of IP Datagrams on Avian Carriers (proposing data transfer via carrier pigeon, which was actually implemented as a real test in 1999).\
RFC 2324: Hyper Text Coffee Pot Control Protocol (HTCPCP/1.0) for controlling, monitoring, and diagnosing coffee pots.\
RFC 2795: The Infinite Monkey Protocol Suite (IMPS), outlining how to use an infinite number of monkeys at typewriters to reproduce the works of Shakespeare.\
RFC 3251: Electricity over IP (EoIP), detailing how to transmit electrical power straight through ethernet cables to run household appliances.\
RFC 3514: The Evil Bit, proposing a single 1-bit flag in IPv4 headers to let packets explicitly declare if they are sent with malicious intent.

🕊️ The Avian Carrier Trilogy (IP over Homing Pigeons)\
RFC 1149 (1990) – IP on Avian Carriers: Explains how to print a packet hex dump, roll it around a pigeon's leg, and unleash it into the air. (Famously implemented in Norway in 2000; it successfully transferred 4 packets with 55% packet loss and a ping time of \~5,000,000 milliseconds).\
RFC 2549 (1999) – IP on Avian Carriers with Quality of Service: An upgrade to the protocol adding QoS flags. It technically handles "multi-cast" (releasing multiple pigeons) and details a major bug: native predators (hawks), which act as a physical layer firewall.\
RFC 6214 (2011) – Adaptation of RFC 1149 for IPv6: Standardizes the pigeon protocol to accommodate the much larger IPv6 address headers, noting that the physical weight of printing a larger header may limit the pigeon's flight velocity.

\
☕ Smart Home & Kitchen Protocols\
RFC 2324 (1998) – Hyper Text Coffee Pot Control Protocol (HTCPCP): Formally defines how to request coffee over the network. It gave birth to the internet’s favorite error message: HTTP 418 I'm a teapot, which states a teapot must refuse to brew coffee.\
RFC 7168 (2014) – HTCPCP Extended for Tea: An essential correction to the original coffee pot protocol, expanding the error structures to adequately handle loose-leaf tea, milk variants, and steeping times.\
🎭 Hardware, Physics, and Sci-Fi Extensions\
RFC 1925 (1996) – The Twelve Networking Truths: While humorous, this is actually a deeply respected list of fundamental computer truths. Fundamental Truth #1: "It has to work." Fundamental Truth #4: "With sufficient thrust, pigs fly just fine."\
RFC 2795 (2000) – The Infinite Monkey Protocol Suite: A comprehensive framework for managing and routing traffic generated by an infinite array of monkeys typing at keyboards to create Shakespearean text.\
RFC 3251 (2002) – Electricity over IP (EoIP): Explains how to break down high-voltage alternating current into discrete internet packets, allowing you to power your microwave through an Ethernet connection.\
RFC 9564 (2024) – Faster-Than-Light (FTL) Encapsulation: Addresses the issue of networking over warp drive, providing a framework for packets that arrive at their destination before they are sent.\
⚖️ Human Behavior, Moods, and Social Media\
RFC 2482 (1999) – Language Tags in Data Transmission: Standardizes how to transmit "sarcasm" over a network line so computers don't interpret it literally.\
RFC 4824 (2007) – The Semaphore Flag Signaling System (SFSS): Adapts IP packets for transmission using maritime hand-held flags, tracking what happens when the flag-waver gets tired (packet degradation).\
RFC 5514 (2009) – IPv6 over Social Networks: Proposes a way to map IPv6 architecture entirely into user profile structures on social networks, utilizing "pokes" and status updates as transport mechanics.\
RFC 5841 (2010) – TCP Option to Denote Packet Mood: Adds an emotional element to packets. Packet headers could be structurally flagged as 0x10 (Happy), 0x11 (Sad), or 0x14 (Anxious), allowing routers to prioritize "depressed" packets to cheer them up.

\
&#x20;

### 🛑Security, Paranoia, and The "Evil Bit"



\*RFC 3514 (2003) – The Security Flag in the IPv4 Header (The Evil Bit): Solves all of cybersecurity by suggesting a 1-bit flag in every internet packet. If a packet is sent by a hacker with malicious intent, the bit is flipped to 1. If it's a good packet, it's 0. Firewalls would simply drop all packets with the "Evil Bit" enabled.\
RFC 3751 (2004) – Omniscience Protocol Requirements: Explores the networking prerequisites required if the IETF were to build a standard for an all-knowing, telepathic network infrastructure.\
RFC 6592 (2012) – The Null Packet: Standardizes a packet that contains absolutely nothing—no header, no payload, no footprint—and discusses how to properly handle a packet that doesn't exist.\
📜 Pre-1990s Historical Anomalies\
RFC 527 (1973) – ARPAWOCKY: The oldest known joke RFC. Written by R. Merryman, it is a complete parody of Lewis Carroll’s nonsense poem "Jabberwocky", rewritten to complain about the ARPANET host protocols.\
RFC 748 (1978) – Telnet Randomly-Lose Option: A proposal for a Telnet server option that randomly discards data during a session to keep user attention sharp.\
RFC 968 (1985) – 'Twas the Night Before Start-up: Written by Vint Cerf (one of the "fathers of the internet"), this is a complete rewrite of the classic Christmas poem about trying to get a network node online before morning.

</details>
