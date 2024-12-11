## TCPDump

- Read pcap file: `tcpdump -n -r capture.pcap`
- Write to pcap file: `tcpdump -nvt -i eth0 -w output.pcap`
- Capture for a number of seconds: `tcpdump -nvt -i eth0 -t 60`
- Display hex content: `tcpdump -nx -r capture.pcap`
- Don't perform hostname lookups: `tcpdump -n -r capture.pcap`
- Verbose output: `tcpdump -nv -r capture.pcap`
- Display MAC Addresses: `tcpdump -ne -r capture.pcap`
- Listen on network interface: `tcpdump -n -i eth0`
- Filter based on header: `tcpdump -nvt -i eth0 ip[9]`
- Filter based on macro: `tcpdump -nvt -i etho0 port 22`
- Capture DNS queries: `tcpdump -nt -eth0 'dst port 53 and udp[10] & 0x80 = 0'`
- Capture DNS replies: `tcpdump -nt -eth0 'dst port 53 and udp[10] & 0x80 = 0x80'`

More details on BPF Filters can be found [here](https://www.ibm.com/docs/en/qsip/7.4?topic=queries-berkeley-packet-filters). 

### TCPDump Macros
- host
- net
- port
- src host
- dst host
- src net
- dst net
- src port
- dst port
- icmp
- tcp
- udp

*** 
[Return to home page](../README.md)