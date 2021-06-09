# Bluesyn

Looks like I found another attack with a false title, there is NO SYN in this capture at all; not even legitmate traffic. Anyways, let's get to the attack.


This attack looks to be based off the [random-tcp-flag.pcap](https://github.com/vucixc/DDoS-Research/blob/main/tcp-flag.md), well in terms of the TCP Flags being using; I also noticed this had a consistent packet length, unlike [random-tcp-flag.pcap](https://github.com/vucixc/DDoS-Research/blob/main/tcp-flag.md). The length mainly stays at ``9039``, I applied a simple conversation filter to this capture, this ruled out 1 packet showing a known hex decimal. I matched that with the packets containing ACK, I made a simple rule to block this attack; and it has worked perfectly! As it says, this is a very simple attack; so a long detailed explanation is not necessary.

## Putting the correct rule into practice 

``iptables -A PREROUTING -t raw -p tcp -m length --length 9039 -m bpf --bytecode "7,48 0 0 0,84 0 0 240,21 0 3 64,48 0 0 28,53 0 1 1,6 0 0 65535,6 0 0 0 " -m comment --comment "bluesyn" -j DROP``
