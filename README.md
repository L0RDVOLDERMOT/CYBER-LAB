<div align="center">

# CYBER-LAB

### TripleTen Cybersecurity Bootcamp · Project Portfolio

[![Security+](https://img.shields.io/badge/CompTIA-Security%2B-E3261F?style=flat-square&logo=comptia&logoColor=white)](#)
[![CEH](https://img.shields.io/badge/EC--Council-CEH-005A8E?style=flat-square)](#)
[![CySA+](https://img.shields.io/badge/CompTIA-CySA%2B%20In%20Progress-FF6B00?style=flat-square&logo=comptia&logoColor=white)](#)
[![TripleTen](https://img.shields.io/badge/TripleTen-Cybersecurity%20Bootcamp-6C3483?style=flat-square)](#)

**Tools:** Metasploit · WPScan · Nmap · Wireshark · Splunk · Zeek · Sysmon · ModSecurity · Hydra · Burp Suite

</div>

---

13 sprints of real offensive and defensive cybersecurity work performed against simulated enterprise environments. Each sprint folder contains the full report: methodology, evidence, MITRE ATT&CK mapping, IOCs, and remediation.

This portfolio demonstrates the **full attack lifecycle**: from reconnaissance and exploitation (offensive sprints) through detection, triage, and incident response (defensive sprints).

---

## Sprint Progression

| # | Project | Domain | Tools | Key Outcome |
|---|---|---|---|---|
| 01 | [Network Configuration](./sprint-01-network-configuration/) | Foundations | Topology, IP planning | Baseline network design |
| 02 | [MegaQuagga Recon](./sprint-02-megaquagga-recon/) | Offensive | Nmap, ARP, DNS | Internal host & service enumeration |
| 03 | [RCI Analysis (0x2A)](./sprint-03-rci-analysis/) | GRC / Risk | Risk register, recommendations | Cybersecurity recommendations |
| 04 | [Threat Modeling: Xibalba Interactive](./sprint-04-threat-modeling-xibalba/) | Defensive Design | STRIDE, DFD, threat worksheet | Threat model deliverable |
| 05 | [Incident Response Plan: Capybara Unlimited](./sprint-05-incident-response-capybara/) | IR Planning | NIST IR lifecycle | Full IR plan document |
| 06 | [Network Modernization: Yagé Botanicals](./sprint-06-yage-botanicals-network/) | Network Security | Architecture proposal | Secure network proposal |
| 08 | [MegaQuagga Vulnerability Assessment](./sprint-08-megaquagga-vuln-assessment/) | Offensive | OpenVAS-style VA, remediation list | VA + executive summary |
| 09 | [MegaQuagga Pentesting Report](./sprint-09-megaquagga-pentest-report/) | **Offensive (Pentest)** | WPScan, Metasploit, Meterpreter | **Full RCE + post-exploitation** |
| 10 | [MegaQuagga Remediation Report](./sprint-10-remediation-report/) | Defensive | PCAP analysis, remediation | Mitigation roadmap |
| 11 | [Plan Proposal](./sprint-11-plan-proposal/) | Strategy | Security program plan | Forward roadmap |
| 12 | [0x2A Incident Investigation — Brute Force](./sprint-12-0x2A-brute-force-investigation/) | **Defensive / SOC** | PCAP, Zeek, Splunk | **Hydra brute force triage** |
| 13 | [0x2A Incident Investigation — Ransomware](./sprint-13-0x2A-ransomware-investigation/) | **Defensive / IR** | Sysmon, WinRegistry, stream:http | **Ransomware kill chain analysis** |
| 14 | [Complex Attack Investigation](./sprint-14-complex-attack/) | **Defensive / Threat Hunt** | Multi-source correlation | Multi-stage attack triage |

---

## Capability Coverage

### Offensive Security
`Reconnaissance` `Web App Pentesting` `Vulnerability Assessment` `Exploitation` `Post-Exploitation` `CVE Research`

### Defensive Security / SOC
`PCAP Triage` `SIEM Threat Hunting` `IR Triage` `IOC Extraction` `Timeline Reconstruction` `MITRE Mapping`

### Tools & Platforms
`Metasploit` `WPScan` `Nmap` `Wireshark` `Splunk` `Zeek` `Sysmon` `ModSecurity` `Hydra` `Burp Suite` `Kali Linux`

### Frameworks
`MITRE ATT&CK` `NIST IR Lifecycle` `OWASP Top 10` `Cyber Kill Chain` `STRIDE`

---

## MITRE ATT&CK Coverage

| ID | Technique | Sprint |
|---|---|---|
| T1190 | Exploit Public-Facing Application | 09 |
| T1078 | Valid Accounts | 09, 12 |
| T1059 | Command & Scripting Interpreter | 09, 13 |
| T1059.003 | Windows Command Shell | 13 |
| T1059.005 | VBScript | 13 |
| T1071.001 | Application Layer Protocol: Web | 12, 13 |
| T1105 | Ingress Tool Transfer | 13 |
| T1110.001 | Brute Force: Password Guessing | 12 |
| T1204.002 | User Execution: Malicious File | 13 |
| T1486 | Data Encrypted for Impact | 13 |
| T1595 | Active Scanning | 02 |
| T1046 | Network Service Discovery | 02 |

---

## Highlight Reports

- **[Sprint 9 — MegaQuagga Pentest](./sprint-09-megaquagga-pentest-report/)**: Full pentest against internal WordPress 5.3 deployment. Identified outdated core (CVE-2019-17671, CVE-2020-28032) and vulnerable wp-file-upload plugin (CVE-2020-10385). Achieved RCE via Metasploit wp_admin_shell_upload, upgraded to Meterpreter for post-exploitation.

- **[Sprint 12 — Hydra Brute Force Triage](./sprint-12-0x2A-brute-force-investigation/)**: PCAP-driven investigation. Identified 4 successful logins on user "elliot" from 192.168.100.20 across 379.687 seconds. Distinguished success (302 → /wp-admin/) from failure (302 → /wp-login.php) using PCAP ground truth where Zeek http.log was insufficient.

- **[Sprint 13 — VBScript Ransomware Investigation](./sprint-13-0x2A-ransomware-investigation/)**: Sysmon-based investigation. Traced wscript.exe → 24249.vbs → cmd.exe → 121214.tmp execution chain. Correlated USB device (MIRANDA_PRI), C2 domain (solidaritedeproximite.org), HTTP payload delivery, and 401 .txt files encrypted (T1486).

---

<div align="center">
<sub>Built by <a href="https://linkedin.com/in/clement-ojukwu">Chibuike Ojukwu Clement</a> · CompTIA Security+ · CEH · CySA+ In Progress · TripleTen Bootcamp Graduate</sub>
</div>