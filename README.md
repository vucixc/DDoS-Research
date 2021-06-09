# DDoS-Research
My Personal Research On Known DDoS Attacks, Using BPF

# Getting Started 

I have these attack captures thanks to [scaredos](https://github.com/scaredos). They can be found at [ddos.studio](http://www.ddos.studio/pkts)

I'll be going over what stood out to me. Lets first begin to talk about common DDoS, as most of you know; DDoS can be really annoying, and some attacks can be really hard to break down. This is the main reason I am doing this today, to help the community against more-advanced floods. If you want direct contact just add me on Discord, or follow my instagram. I try my best to stay active on these platforms \\ discord = spencer'#1044 | [instagram](https://instagram.com/vucixc). Now, let's get started!

# Capture #1

## random-tcp-flags.pcap

This is a pretty simple attack, but I'll put it in here. As the title says, it uses random TCP flags in each attack; such as ACK, RST, PSH. It contains mainly malformed packets with a length of 0, I also saw some ECN, CWR; but no SYN. I will not classify this attack as a TCP Reflection. I noticed this attack puts strain on the conntrack module, just like a TCP Reflection. I came up with a simple patch using the conversation packets involved, I then looked at the hex-decimal output and came up with a BPF application using netfilters. I matched the byte starting at the IP header offset, after that; I implemented the hex output to the IP header offset syntax. I set no packet-length value to this as it was a consistent ZERO!

`` iptables -A PREROUTING -t raw -p tcp -m bpf --bytecode "12,48 0 0 0,84 0 0 240,21 0 8 64,48 0 0 9,21 0 6 6,40 0 0 6,69 4 0 8191,177 0 0 0,80 0 0 13,21 0 1 2048,6 0 0 65535,6 0 0 0 " -m comment --comment "random-tcp" -j ACCEPT``

# Capture #2

## bluesyn.pcap

 Placeholder


