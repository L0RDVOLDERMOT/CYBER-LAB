<div align="center">

# CYBER-LAB

### Offensive & Defensive Cybersecurity Portfolio

[![Security+](https://img.shields.io/badge/CompTIA-Security%2B-E3261F?style=flat-square&logo=comptia&logoColor=white)](https://github.com/L0RDVOLDERMOT/CYBER-LAB)
[![CEH](https://img.shields.io/badge/EC--Council-CEH-005A8E?style=flat-square)](https://github.com/L0RDVOLDERMOT/CYBER-LAB)
[![CySA+](https://img.shields.io/badge/CompTIA-CySA%2B%20In%20Progress-FF6B00?style=flat-square&logo=comptia&logoColor=white)](https://github.com/L0RDVOLDERMOT/CYBER-LAB)
[![TripleTen](https://img.shields.io/badge/TripleTen-Cybersecurity%20Bootcamp-6C3483?style=flat-square)](https://github.com/L0RDVOLDERMOT/CYBER-LAB)

**Tools:** Metasploit · WPScan · Nmap · Wireshark · Splunk · Hydra · Burp Suite · Netcat

</div>

---

Real-world attack and defense work performed across simulated enterprise environments. Each project folder contains a full writeup: methodology, tools, findings, MITRE ATT&CK mapping, and remediation.

---

## Repository Structure

```
CYBER-LAB/
├── 01-wordpress-pentest/        # Web app exploitation — MegaQuagga target
├── 02-pcap-soc-analysis/        # PCAP triage — Hydra brute-force detection
├── 03-splunk-o365-investigation/ # SIEM threat hunting — OneDrive audit logs
└── 04-network-recon/            # Network reconnaissance — Nmap methodology
```

---

## Project Portfolio

| # | Project | Domain | Tools | MITRE Techniques | Status |
|---|---|---|---|---|---|
| 01 | [WordPress Pentest — MegaQuagga](./01-wordpress-pentest/) | Offensive | WPScan, Nmap, Metasploit | T1190, T1078, T1059 | ✅ Complete |
| 02 | [PCAP SOC Analysis — Brute Force Detection](./02-pcap-soc-analysis/) | Defensive / SOC | Wireshark, Hydra | T1110, T1071 | ✅ Complete |
| 03 | [Splunk O365 Audit Investigation](./03-splunk-o365-investigation/) | Threat Hunting | Splunk, O365 Audit | T1078, T1566 | ✅ Complete |
| 04 | [Network Reconnaissance Lab](./04-network-recon/) | Offensive | Nmap, Netcat | T1595, T1046 | ✅ Complete |

---

## Skills Demonstrated

**Offensive**
`WPScan` `Nmap` `Metasploit` `Netcat` `Hydra` `CVE Exploitation` `Credential Harvesting`

**Defensive / SOC**
`Wireshark` `PCAP Analysis` `Splunk SPL` `O365 Audit Logs` `IOC Identification` `Alert Triage`

**Frameworks**
`MITRE ATT&CK` `Cyber Kill Chain` `NIST CSF`

---

## MITRE ATT&CK Coverage

| Technique ID | Name | Project |
|---|---|---|
| T1190 | Exploit Public-Facing Application | WordPress Pentest |
| T1078 | Valid Accounts | WordPress Pentest, O365 Investigation |
| T1059 | Command & Scripting Interpreter | WordPress Pentest |
| T1110 | Brute Force | PCAP SOC Analysis |
| T1071 | Application Layer Protocol | PCAP SOC Analysis |
| T1566 | Phishing (initial access context) | O365 Investigation |
| T1595 | Active Scanning | Network Recon |
| T1046 | Network Service Discovery | Network Recon |

---

<div align="center">
<sub>Built by <a href="https://linkedin.com/in/clement-ojukwu">Chibuike Ojukwu Clement</a> · CompTIA Security+ · CEH · CySA+ In Progress</sub>
</div>