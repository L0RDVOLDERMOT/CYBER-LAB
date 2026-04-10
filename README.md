# CHIBUIKE CLEMENT — THREAT HUNTING PORTFOLIO

![Threat Hunting](https://img.shields.io/badge/Focus-Threat%20Hunting-blue?style=for-the-badge)
![SIEM](https://img.shields.io/badge/SIEM-Splunk-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Seeking-brightgreen?style=for-the-badge)

Cybersecurity portfolio demonstrating **threat detection, investigation, and detection engineering** across simulated enterprise environments.

Focused on identifying **attack patterns, anomalous behavior, and adversary techniques** using SIEM, network traffic analysis, and log correlation.

---

## 🧠 CORE CAPABILITIES

* Threat Hunting & Hypothesis-Driven Investigation
* SIEM Analysis (Splunk — SPL Query Development)
* Network Traffic Analysis (PCAP, Wireshark)
* Incident Triage & Escalation
* Attack Pattern Identification (Brute Force, Enumeration)
* MITRE ATT&CK Mapping & Adversary Behavior Analysis

---

## 📁 PROJECT PORTFOLIO

### 🔴 THREAT HUNTING & DETECTION ENGINEERING (PRIMARY FOCUS)

#### Threat Hunt: Brute Force Detection Across Logs

* Developed SPL queries to detect repeated authentication failures
* Identified abnormal login patterns across multiple events
* Tuned detection to reduce false positives
* Mapped activity to **MITRE ATT&CK T1110 (Brute Force)**

**Detection Logic:**

* High volume login attempts from single source
* Repeated failed authentication events
* Suspicious user-agent patterns

---

#### Detection Engineering: Suspicious User-Agent Activity

* Built detection queries for malicious tools (e.g., Hydra)
* Parsed HTTP logs to identify automation patterns
* Correlated request frequency and headers

**Outcome:**

* Identified automated attack behavior
* Created reusable detection logic

---

### 🟠 INCIDENT RESPONSE & INVESTIGATION

#### WordPress Brute Force Attack Investigation

* Analyzed PCAP data to identify authentication attack
* Source: `192.168.100.20` → Target: `192.168.100.2`
* Detected repeated POST requests to `/wp-login.php`
* Confirmed Hydra-based brute force activity

**Analysis Techniques:**

* Packet inspection (Wireshark)
* HTTP request correlation
* Timeline reconstruction

---

### 🔵 OFFENSIVE SECURITY (ADVERSARY SIMULATION)

#### Network Scanning & Enumeration

* Identified open ports and exposed services using Nmap
* Performed service fingerprinting and OS detection
* Mapped attack surface for exploitation planning

---

#### Exploitation & Post-Exploitation

* Executed attacks using Metasploit
* Conducted post-exploitation enumeration
* Documented attack paths and system access

---

## 🛠️ DETECTION LIBRARY (CRITICAL SECTION)

### Brute Force Detection (Splunk SPL)

```spl
index=* sourcetype=auth_logs
| stats count by src_ip, user
| where count > 20
```

---

### Suspicious User-Agent Detection

```spl
index=* sourcetype=http_logs
| search user_agent="*Hydra*"
```

---

## 📊 SAMPLE THREAT HUNT WORKFLOW

1. Define hypothesis (e.g., brute force activity present)
2. Identify relevant log sources
3. Develop SPL queries
4. Analyze patterns and anomalies
5. Validate findings
6. Document results and detection logic

---

## 🏆 CERTIFICATIONS

* CompTIA Security+
* CompTIA CySA+
* Certified Ethical Hacker (CEH)

---

## 📌 CURRENT FOCUS

* Detection Engineering (Splunk SPL Development)
* Threat Hunting Methodologies
* Active Directory Attack Simulation

---

## 📜 DISCLAIMER

All activities conducted in controlled lab environments.
