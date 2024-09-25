---
{"dg-publish":true,"permalink":"/content/packet-capture/","tags":["file","packet","forensics","ctf"],"created":"2024-09-16T19:04:02.900-07:00","updated":"2024-09-16T19:04:46.880-07:00"}
---

### pcap, pcapng

- pcap inspection in Wireshark (GUI) or `tshark` (CLI)
- `tcpdump` captures packets in real time
- `tcpflow` is like `tcpdump` but it also saves the data
- both Wireshark and `tcpdump` are based on `libpcap`
- file extraction: Xplico, tcpxtract, Network Miner, Foremost, Snort
- online analysis: https://lab.dynamite.ai/
- `ngrep` is grep but for packets
- pcap/pcapng repair: https://f00l.de/hacking/pcapfix.php
- pcapng is newer and may need to be converted to pcap if unsupported
- Python usage: 
	- `dpkt` package for packet manipulation
	- Wirepy for interfacing Wireshark