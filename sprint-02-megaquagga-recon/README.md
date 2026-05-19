# Sprint 2: MegaQuagga Reconnaissance

Type: Offensive Recon, Pre-engagement Information Gathering  
Target: MegaQuagga internal network (192.168.100.0/24)

## Objective

Perform structured reconnaissance against the MegaQuagga internal environment to identify live hosts, exposed services, and viable attack surface for downstream pentest phases (sprints 8 and 9).

## Methodology

### Host Discovery
```bash
# ICMP sweep
for i in {1..254}; do ping -c 1 192.168.100.$i; done

# ARP scan
arp-scan 192.168.100.0/24
```

### Service Enumeration
```bash
nmap -sV -sC -p- 192.168.100.2
nmap -O 192.168.100.2
```

### DNS Confirmation
Confirmed www.megaquagga.local resolves to 192.168.100.2. Internal name resolution operational.

## Findings Summary

| Host | Role | Notable Services |
|---|---|---|
| 192.168.100.1 | Gateway | Routing |
| 192.168.100.2 | Web Server (WordPress) | 22/SSH, 80/HTTP, 443/HTTPS, 8080, 3389 |
| 192.168.100.254 | Network Device | Management |

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Reconnaissance | Active Scanning, IP Block Scanning | T1595.001 |
| Discovery | Network Service Discovery | T1046 |
| Discovery | System Information Discovery | T1082 |

TripleTen Sprint 2, Reconnaissance Module. Feeds into Sprint 8 and Sprint 9.