<div align="center">

# CYBER-LAB

### TripleTen Cybersecurity Bootcamp · Project Portfolio

[![Security+](https://img.shields.io/badge/CompTIA-Security%2B-E3261F?style=flat-square&logo=comptia&logoColor=white)](#)
[![CEH](https://img.shields.io/badge/EC--Council-CEH-005A8E?style=flat-square)](#)
[![CySA+](https://img.shields.io/badge/CompTIA-CySA%2B%20In%20Progress-FF6B00?style=flat-square&logo=comptia&logoColor=white)](#)
[![TripleTen](https://img.shields.io/badge/TripleTen-Cybersecurity%20Bootcamp-6C3483?style=flat-square)](#)

Tools used: Metasploit, WPScan, Nmap, Wireshark, Splunk, Zeek, Sysmon, ModSecurity, Hydra, Burp Suite

</div>

---

Thirteen sprints of offensive and defensive work against simulated enterprise environments. Each sprint folder contains the full report: methodology, evidence, MITRE ATT&CK mapping, IOCs, and remediation. The original PDF deliverable from each sprint sits alongside the README.

## Sprint Progression

| # | Project | Domain | Tools | Outcome |
|---|---|---|---|---|
| 01 | [Network Configuration](./sprint-01-network-configuration/) | Foundations | Topology, IP planning | Baseline network design |
| 02 | [MegaQuagga Recon](./sprint-02-megaquagga-recon/) | Offensive | Nmap, ARP, DNS | Internal host and service enumeration |
| 03 | [RCI Analysis (0x2A)](./sprint-03-rci-analysis/) | GRC / Risk | Risk register | Cybersecurity recommendations |
| 04 | [Threat Modeling: Xibalba Interactive](./sprint-04-threat-modeling-xibalba/) | Defensive Design | STRIDE, DFD | Threat model deliverable |
| 05 | [Incident Response Plan: Capybara](./sprint-05-incident-response-capybara/) | IR Planning | NIST 800-61 | Full IR plan |
| 06 | [Network Modernization: Yagé Botanicals](./sprint-06-yage-botanicals-network/) | Network Security | Architecture proposal | Secure network proposal |
| 08 | [MegaQuagga Vulnerability Assessment](./sprint-08-megaquagga-vuln-assessment/) | Offensive | VA, remediation list | VA plus executive summary |
| 09 | [MegaQuagga Pentesting Report](./sprint-09-megaquagga-pentest-report/) | Offensive (Pentest) | WPScan, Metasploit, Meterpreter | Full RCE and post-exploitation |
| 10 | [MegaQuagga Remediation Report](./sprint-10-remediation-report/) | Defensive | PCAP analysis | Mitigation roadmap |
| 11 | [Plan Proposal](./sprint-11-plan-proposal/) | Strategy | Security program plan | Forward roadmap |
| 12 | [0x2A Incident Investigation: Brute Force](./sprint-12-0x2A-brute-force-investigation/) | Defensive / SOC | PCAP, Zeek, Splunk | Hydra brute force triage |
| 13 | [0x2A Incident Investigation: Ransomware](./sprint-13-0x2A-ransomware-investigation/) | Defensive / IR | Sysmon, WinRegistry | Ransomware kill chain analysis |
| 14 | [Complex Attack Investigation](./sprint-14-complex-attack/) | Defensive / Threat Hunt | Multi-source correlation | Multi-stage attack triage |

## Capability Coverage

Offensive Security
`Reconnaissance` `Web App Pentesting` `Vulnerability Assessment` `Exploitation` `Post-Exploitation` `CVE Research`

Defensive Security and SOC
`PCAP Triage` `SIEM Threat Hunting` `IR Triage` `IOC Extraction` `Timeline Reconstruction` `MITRE Mapping`

Tools and Platforms
`Metasploit` `WPScan` `Nmap` `Wireshark` `Splunk` `Zeek` `Sysmon` `ModSecurity` `Hydra` `Burp Suite` `Kali Linux`

Frameworks
`MITRE ATT&CK` `NIST IR Lifecycle` `OWASP Top 10` `Cyber Kill Chain` `STRIDE`

## MITRE ATT&CK Coverage

| ID | Technique | Sprint |
|---|---|---|
| T1190 | Exploit Public-Facing Application | 09 |
| T1078 | Valid Accounts | 09, 12 |
| T1059 | Command and Scripting Interpreter | 09, 13 |
| T1059.003 | Windows Command Shell | 13 |
| T1059.005 | VBScript | 13 |
| T1071.001 | Application Layer Protocol: Web | 12, 13 |
| T1105 | Ingress Tool Transfer | 13 |
| T1110.001 | Brute Force: Password Guessing | 12 |
| T1204.002 | User Execution: Malicious File | 13 |
| T1486 | Data Encrypted for Impact | 13 |
| T1595 | Active Scanning | 02 |
| T1046 | Network Service Discovery | 02 |

## Highlight Reports

Sprint 9 (MegaQuagga Pentest). Pentest against internal WordPress 5.3 deployment. Identified outdated core (CVE-2019-17671, CVE-2020-28032) and vulnerable wp-file-upload plugin (CVE-2020-10385). Achieved RCE via the Metasploit wp_admin_shell_upload module, then upgraded to Meterpreter for post-exploitation as www-data.

Sprint 12 (Hydra Brute Force Triage). PCAP-driven investigation. Identified four successful logins on user "elliot" from 192.168.100.20 across 379.687 seconds. Used PCAP as ground truth to distinguish success (302 to /wp-admin/) from failure (302 to /wp-login.php) because Zeek http.log does not record the Location header.

Sprint 13 (VBScript Ransomware Investigation). Sysmon-based investigation. Traced wscript.exe to 24249.vbs to cmd.exe to 121214.tmp execution chain. Correlated USB device (MIRANDA_PRI), C2 domain (solidaritedeproximite.org), HTTP payload delivery, and 401 .txt files encrypted (T1486).

---

<div align="center">
<sub>Chibuike Ojukwu Clement · CompTIA Security+ · CEH · CySA+ In Progress · TripleTen Bootcamp Graduate</sub>
</div>