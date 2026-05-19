# 02 — PCAP SOC Analysis: Brute Force Detection

**Type:** SOC Tier 1/2 — Network Traffic Analysis & Incident Triage  
**Tools:** Wireshark · PCAP Analysis  
**MITRE Techniques:** T1110 · T1071  

---

## Objective

Analyze a provided PCAP capture from a simulated enterprise environment. Identify attack patterns, extract IOCs, and produce a triage report suitable for escalation.

---

## Investigation Summary

| Field | Value |
|---|---|
| Capture Period | Simulated enterprise window |
| Internal IPs | 192.168.100.2, 192.168.100.20 |
| Suspicious URI | /wp-login.php |
| Attack Tool Identified | Hydra |
| MITRE Classification | T1110 — Brute Force |

---

## Analysis Methodology

### Step 1 — Initial Triage
- Opened PCAP in Wireshark
- Applied `http` filter to isolate application layer traffic
- Sorted by timestamp to establish event timeline

### Step 2 — Volume Analysis
- Identified abnormally high POST request count to `/wp-login.php`
- Single source IP generating hundreds of authentication attempts in seconds
- Pattern consistent with automated credential stuffing

### Step 3 — IOC Extraction

```
Source IP:    192.168.100.20
Target IP:    192.168.100.2
Target URI:   /wp-login.php
HTTP Method:  POST
Tool Pattern: Hydra user-agent string identified in HTTP headers
Request Rate: ~350 requests/minute
```

### Step 4 — Payload Inspection
- Examined POST body contents — credential pairs cycling through wordlist
- Confirmed Hydra brute-force pattern via user-agent string
- No successful 200 OK responses observed (attack did not achieve authentication)

### Step 5 — Timeline Reconstruction

```
[T+0:00]  First POST to /wp-login.php from 192.168.100.20
[T+0:02]  Request rate escalates — automated pattern confirmed
[T+0:08]  Peak volume — ~350 req/min
[T+1:12]  Traffic stops — attack concluded or interrupted
```

---

## Key Findings

| IOC | Value | Significance |
|---|---|---|
| Attacker IP | 192.168.100.20 | Internal — possible compromised host or insider |
| Target | 192.168.100.2:/wp-login.php | WordPress admin login endpoint |
| Attack Type | Credential brute-force | T1110 |
| Tool | Hydra | Identified via UA string |
| Impact | No confirmed breach | Attack did not succeed in PCAP window |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force | T1110 |
| Command & Control | Application Layer Protocol (HTTP) | T1071.001 |

---

## Recommendations

- Block 192.168.100.20 immediately and isolate for forensic review
- Implement account lockout policy after 5 failed attempts on wp-login.php
- Deploy WAF rule rate-limiting POST requests to authentication endpoints
- Enable SIEM alert for >10 failed auth attempts/minute from single source
- Rotate WordPress admin credentials

---

*Environment: TripleTen Cybersecurity Bootcamp — SOC Analyst Training Module*