# 04 — Network Reconnaissance Lab

**Type:** Network Recon & Service Enumeration  
**Tools:** Nmap · Netcat · OS Fingerprinting  
**MITRE Techniques:** T1595 · T1046  

---

## Objective

Perform structured network reconnaissance against a simulated enterprise target range. Map the attack surface, identify live hosts, enumerate services, fingerprint OS, and document findings for exploitation planning.

---

## Methodology

### Phase 1 — Host Discovery
```bash
# ICMP sweep to identify live hosts
nmap -sn 192.168.1.0/24

# ARP scan (local segment)
nmap -PR -sn 192.168.1.0/24
```

### Phase 2 — Port Scanning
```bash
# Full TCP port scan
nmap -p- --min-rate 5000 -T4 <target>

# Top 1000 UDP ports
nmap -sU --top-ports 1000 <target>
```

### Phase 3 — Service & Version Enumeration
```bash
# Version detection + default scripts on open ports
nmap -sV -sC -p <open_ports> <target>
```

### Phase 4 — OS Fingerprinting
```bash
nmap -O --osscan-guess <target>
```

### Phase 5 — Banner Grabbing with Netcat
```bash
nc -nv <target> 22
nc -nv <target> 80
nc -nv <target> 21
```

---

## Sample Findings

| Port | Service | Version | Notes |
|---|---|---|---|
| 22 | SSH | OpenSSH 7.6 | Default port — check for outdated version CVEs |
| 80 | HTTP | Apache 2.4.29 | HTTP headers leak server info |
| 443 | HTTPS | Apache 2.4.29 | TLS config review needed |
| 3306 | MySQL | MySQL 5.7 | Should not be externally exposed |
| 8080 | HTTP | Tomcat 9.0 | Admin panel may be accessible |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Reconnaissance | Active Scanning — IP Blocks | T1595.001 |
| Discovery | Network Service Discovery | T1046 |
| Discovery | System Information Discovery | T1082 |

---

## Remediation Recommendations

- Close all non-essential external-facing ports
- Remove version information from HTTP headers (ServerTokens Prod)
- Restrict MySQL to localhost binding only
- Disable ICMP responses at network perimeter if stealth is required
- Implement port knocking or firewall rules to restrict SSH access

---

*Environment: TripleTen Cybersecurity Bootcamp — Network Penetration Testing Module*