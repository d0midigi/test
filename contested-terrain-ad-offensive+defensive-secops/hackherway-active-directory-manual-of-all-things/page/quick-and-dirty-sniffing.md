# Quick and Dirty Sniffing

Social Engineering is the most powerful attack tool when it comes to manipulating and exploiting human emotions and vulnerability requires no equipment or technology, and often minimal expense. Only proper user education and awareness can prevent it and even then, a faltered judgment can then be further leveraged for further exploitation.

### Methods for Defeating a Switch

* **Admin the Switch ‣** If the password for the switch can be guessed, a port can be placed into monitor mode
* **MAC Spoofing** Set the MAC address of a NIC to the same value as another
* **MAC Flooding** Overwhelm the _**Content Addressable Memory (CAM)**_ table of the switch so it converts to hub mode
* **ARP Poisoning** Inject incorrect information into the ARP caches of two or more endpoints

### Wireshark Command-Line Tools

* **tshark** Command-line version of Wireshark
* **dumpcap** Captures traffic
* **capinfos** Reads a saved captured file and returns statistics about it
* **editcap** Edit and/or translate the format of capture files
* **mergecap** Merges multiple capture files into one
* **text2pcap** Generates a capture file from an ASCII hexdump of packets
* **tcpflow** Extracts data streams from dump files
* **tcptrace** Analyzes TCP conversations
* **tcpreplay** Can resent captured packets

### TCPDump Capture Files

#### K.I.S.S. pcap

* **Keep It Simple Sweetheart**: Keep your capture files simple on the test. They look just like plaintext messages; however, depending on the aggressiveness of how often your SIEM or log solution is scheduled to dump files as they can drastically add up in no time, and some of them will contain innocuous or unimportant information which you can discard rather than read to have take up time spent elsewhere.

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/0 (65).png>)

1. Host www.example.com and not (port 80 or port 25)
2. Port not 53 and not arp
3. IP proto 1
4. (tcp\[2:2] > 1500 and tcp (2:2) < 1550

The provided Wireshark pcap filter expressions do the following:

1. **Host www.example.com and not (port 80 or port 25)**
   1. This expression is used to filter network packets based on specific criteria:
      1. **Host www.example.com:** Capture packets where the source or destination IP address matches **www.example.com.**
      2. **and not (port 80 or port 25):** Exclude packets where the source or destination port is 80 (HTTP) or 25 (SMTP).
2. **Port 53 and net arp**
   1. This expression filters packets based on port number and ARP (Address Resolution Protocol):
      1. **Port not 53:** Exclude packets where the source or destination port is 53 (DNS).
      2. **and not arp:** Exclude packets that use the Address Resolution Protocol (ARP).
3. **IP proto 1**
   1. This expression filters packets based on the IP (Internet Protocol) number:
      1. **IP proto 1:** Capture packets where the IP protocol number is 1, which corresponds to ICMP (Internet Control Message Protocol, or _‘ping’_).
4. **(tcp\[2:2] > 1500 and tcp\[2:2] < 1550)**
   1. This expression filters TCP packets based on specific bytes within the packet header:
      1. **tcp\[2:2]:** This specifies a range of bytes in the TCP header. It means _“take 2 bytes starting at the 2nd byte of the TCP header.”_ In the TCP header, the 2nd byte is part of the source port field.
      2. **> 1500:** Capture packets where the value of the selected bytes is greater than 1500.
      3. **and tcp \[2:2] < 1550:** Additionally, ensure the value of the selected bytes is less than 1550.

Let’s now take a look at what each filter does and how they might be used in an ethical hacking security engagement:

1. Host www.example.com and not (port 80 or port 25):
   * Capture packets to/from **www.example.com**
   * Exclude HTTP (port 80) and SMTP (port 25) traffic
2. Port not 53 and not arp:
   * Exclude DNS (port 53) and ARP traffic
3. IP proto 1:
   * Capture only ICMP packets (e.g., ping requests/replies)
4. (tcp\[2:2] > 1500 and tcp\[2:2] < 1550:
   * Capture TCP packets where the source port field (interpreted as an integer from bytes 2-3 of the TCP header) is between 1500 and 1550.

### Practical Usage in Tools

#### Wireshark

In Wireshark, these filters would be applied separately in the filter bar; however, for combined complex filtering, Wireshark uses slightly different syntax and capabilities. Here’s how you could apply them:

#### Host Filter

![A black box with white text

Description automatically generated](<../.gitbook/assets/1 (49).png>)

ip.addr == www.example.com && !(tcp.port == 80 || tcp.port == 25)

#### Port and ARP Filter

![A close-up of a black box

Description automatically generated](<../.gitbook/assets/2 (42).png>)

!(udp.port == 53 || arp)

#### ICMP Filter

![A close-up of a logo

Description automatically generated](<../.gitbook/assets/3 (31).png>)

ip.prot = = 1

#### TCP Header Byte Ranger Filter

Wireshark does not support direct byte filtering in display filters; you might need custom dissectors or advanced capture filters instead).

#### tcpdump

In tcpdump, you can use these filters as follows:

![A screenshot of a computer

Description automatically generated](<../.gitbook/assets/4 (34).png>)

\# Combined command might look like this, but note it might not make practical sense to combine all as shown:

tcpdump host www.example.com and not (port 80 or port 25) and not port 53 and not arp and ip proto 1 and tcp\[2:2] > 1500 and tcp\[2:2] < 1550
