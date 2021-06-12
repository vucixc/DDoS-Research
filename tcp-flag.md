# random-tcp-flags.pcap

This is a pretty simple attack, but I'll put it in here. As the title says, it uses random TCP flags in each attack; such as ACK, RST, PSH. It contains mainly malformed packets with a length of 0, I also saw some ECN, CWR; but no SYN. I will not classify this attack as a TCP Reflection. I noticed this attack puts strain on the conntrack module, just like a TCP Reflection. I came up with a simple patch using the conversation packets involved, I then looked at the hex-decimal output and came up with a BPF application using netfilters. I matched the byte starting at the IP header offset, after that; I implemented the hex output to the IP header offset syntax. I set no packet-length value to this as it was a consistent ZERO!

## Putting the rule into proper place
> iptables -A PREROUTING -t raw -p tcp -m bpf --bytecode "12,48 0 0 0,84 0 0 240,21 0 8 64,48 0 0 9,21 0 6 6,40 0 0 6,69 4 0 8191,177 0 0 0,80 0 0 13,21 0 1 2048,6 0 0 65535,6 0 0 0 " -m comment --comment "random-tcp" -j ACCEPT
