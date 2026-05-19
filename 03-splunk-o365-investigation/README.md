# 03 — Splunk O365 Audit Investigation: OneDrive Exfiltration Hunt

**Type:** SIEM Threat Hunting — Insider Threat / Data Exfiltration  
**Tools:** Splunk · Office 365 Unified Audit Log  
**MITRE Techniques:** T1078 · T1566 · T1048  

---

## Objective

Hunt for evidence of unauthorized data access or exfiltration within Office 365 audit logs using Splunk. Identify compromised accounts, suspicious file access, and abnormal sharing behavior.

---

## Environment

```
Splunk Index:    index="client3"
Sourcetype:      o365:management:activity
Scope:           OneDrive for Business audit events
```

---

## Hunting Methodology

### Query 1 — Establish Baseline: All O365 Activity
```spl
index="client3" sourcetype="o365:management:activity"
| stats count by Operation, UserId
| sort -count
```

### Query 2 — File Access Anomaly Detection
```spl
index="client3" sourcetype="o365:management:activity" Operation=FileAccessed
| stats count by UserId, SiteUrl, SourceFileName
| where count > 50
| sort -count
```

### Query 3 — External Sharing Detection
```spl
index="client3" sourcetype="o365:management:activity" Operation=SharingSet
| eval shared_externally=if(match(TargetUserOrGroupType,"Guest|External"), "YES", "NO")
| where shared_externally="YES"
| table _time, UserId, SourceFileName, TargetUserOrGroupName
```

### Query 4 — Suspicious Download Volume
```spl
index="client3" sourcetype="o365:management:activity" Operation=FileDownloaded
| bucket _time span=1h
| stats count by _time, UserId, ClientIP
| where count > 100
```

### Query 5 — Account Activity Outside Business Hours
```spl
index="client3" sourcetype="o365:management:activity"
| eval hour=strftime(_time, "%H")
| where hour < 6 OR hour > 22
| stats count by UserId, Operation, ClientIP
| sort -count
```

---

## Key Findings

| Finding | Detail | MITRE |
|---|---|---|
| High-volume file access | One account accessed 200+ files in 30 min window | T1078 |
| External sharing event | Internal file shared to non-org email domain | T1048 |
| Off-hours activity | Account active at 02:00 — no business justification | T1078 |
| New ClientIP | Activity from IP with no prior history in org | T1078 |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Initial Access | Valid Accounts | T1078 |
| Collection | Data from Cloud Storage | T1530 |
| Exfiltration | Exfiltration Over Web Service | T1048 |

---

## Recommendations

- Disable flagged account pending HR and legal review
- Block external sharing to non-approved domains in O365 DLP policy
- Set Splunk alert for >50 file access events per user per hour
- Implement Conditional Access Policy blocking off-hours sign-ins from new IPs
- Review all files accessed by flagged account in the 30-day window

---

*Environment: TripleTen Cybersecurity Bootcamp — SIEM & Threat Hunting Module*