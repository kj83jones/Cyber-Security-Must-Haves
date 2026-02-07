# Network Security

## Why This Matters

The network is where attackers move. Whether it's lateral movement after initial compromise, command-and-control (C2) traffic, or data exfiltration — if you have visibility into your network, you can catch it.

## Network Security Checklist

### Firewall Configuration
- [ ] Default deny on inbound rules
- [ ] Outbound filtering (don't allow all outbound — this is how C2 and exfil happen)
- [ ] Segment networks (separate IT, OT, IoT, guest, servers)
- [ ] Review firewall rules quarterly — remove rules no one can justify
- [ ] Log allowed AND denied traffic
- [ ] Geo-block countries you don't do business with (inbound at minimum)

### DNS Security
- [ ] Use DNS filtering (Cisco Umbrella, Quad9, Cloudflare Gateway)
- [ ] Log all DNS queries — DNS is one of the best sources for detecting C2
- [ ] Block DNS over HTTPS (DoH) at the network level to maintain visibility
- [ ] Monitor for DNS tunneling (unusually long subdomain queries)
- [ ] Sinkhole known malicious domains

### Network Monitoring
- [ ] Deploy IDS/IPS (Suricata or Snort) at network boundaries
- [ ] Capture NetFlow/sFlow data for traffic analysis
- [ ] Monitor for beaconing patterns (regular interval callbacks to external IPs)
- [ ] Alert on large outbound transfers to unusual destinations
- [ ] Monitor east-west traffic, not just north-south

### Segmentation
- [ ] Critical servers in a separate VLAN from user workstations
- [ ] IoT devices on an isolated network
- [ ] Development/test environments separated from production
- [ ] Guest Wi-Fi on a completely separate network
- [ ] Limit inter-VLAN routing to only what's necessary

## Common Network Attacks to Detect

### ARP Spoofing / Man-in-the-Middle
- **What**: Attacker poisons ARP tables to intercept traffic
- **Detect**: Monitor for ARP anomalies, use Dynamic ARP Inspection (DAI)
- **Prevent**: 802.1X port authentication, static ARP entries for critical systems

### DNS Exfiltration
- **What**: Data encoded in DNS queries sent to attacker-controlled domains
- **Detect**: Look for unusually long DNS queries, high volume of queries to single domain
- **Prevent**: DNS filtering, monitor query length and frequency

### Lateral Movement
- **What**: Attacker moves from compromised host to other systems
- **Detect**: Unusual SMB, RDP, WinRM, or SSH between workstations
- **Prevent**: Network segmentation, limit admin protocols to jump servers

### C2 Beaconing
- **What**: Malware calling home at regular intervals
- **Detect**: Look for periodic outbound connections (jitter analysis)
- **Prevent**: Outbound filtering, SSL inspection, DNS filtering

## Useful Network Commands for Investigations

```bash
# Check active connections on a Linux system
ss -tunapl

# Check active connections on Windows
netstat -ano

# DNS lookup
nslookup <domain>
dig <domain>

# Quick port scan with Nmap
nmap -sV -sC -p- <target>

# Capture packets with tcpdump
tcpdump -i eth0 -w capture.pcap

# Analyze pcap with tshark (CLI Wireshark)
tshark -r capture.pcap -Y "http.request"
```

## Recommended Network Security Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| Suricata | IDS/IPS | Rule-based network threat detection |
| Zeek | Network monitoring | Creates detailed logs of network activity |
| Wireshark | Packet analysis | GUI-based deep packet inspection |
| tcpdump | Packet capture | Command-line packet capture |
| Nmap | Network scanning | Discovery and security auditing |
| Arkime (Moloch) | Full packet capture | Indexed, searchable pcap storage |
| NetworkMiner | Forensic analysis | Extract files and images from pcaps |
| Rita | Beacon detection | Detects C2 communication patterns |
