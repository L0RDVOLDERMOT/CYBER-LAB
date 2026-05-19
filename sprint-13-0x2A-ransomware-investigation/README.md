# Sprint 13 — IR Triage: VBScript Ransomware Investigation

**Analyst:** Chibuike Ojukwu  
**Date:** 2025-08-28  
**Source:** security@0x2asec.com  
**Alert ID:** UR-INT-20250603-0047  
**Severity:** HIGH  
**Disposition:** True Positive (TP)  

---

## Initial Findings

Host **we8105desk** (IP **192.168.250.100**) executed VBScript (`wscript.exe → 24249.vbs`) that spawned `cmd.exe` and staged `121214.tmp`.

### Process Lineage (Sysmon EventID 1)
```
wscript.exe
  └─ C:\Users\bob.smith.WAYNECORPINC\AppData\Roaming\24249.vbs
        └─ cmd.exe /C ... \121214.tmp
```

### Network Activity
- Contacted **solidaritedeproximite.org**
- HTTP GET `/mhtr.jpg` → **37.187.37.150**
- HTTP GET `/HeaderSlice.jpg` → **67.132.183.25**

### File System Activity
- **401 distinct `.txt` TargetFilename events** (Sysmon EventID 2) under `C:\Users\bob.smith.WAYNECORPINC\...` during 2016-08-24 00:00 – 2016-08-25 00:00 UTC
- Pattern consistent with mass file encryption

### Initial Vector Indicator
- WinRegistry USBSTOR records show removable device labeled **MIRANDA_PRI** with last_seen 2016-08-24 16:42:17 UTC

### Lateral Movement Check
- SMB telemetry from 192.168.250.100 shows highest volume to 192.168.250.20
- No second-host impact established from evidence provided

**Disposition rationale:** True Positive — host executed scriptable content and contacted a domain identified as malicious in this project. Severity High — impact confirmed on a single endpoint (script execution + large volume of file events). No evidence of spread beyond we8105desk.

---

## Incident Summary

### Confirmed Time Bounds (UTC)

| Time | Event |
|---|---|
| 2016-08-24 16:42:17 | USB artifact MIRANDA_PRI last seen (WinRegistry) |
| 2016-08-24 16:43:21 | Process lineage: wscript.exe → 24249.vbs → cmd.exe → 121214.tmp (Sysmon EID 1) |
| 2016-08-24 16:48:12 | First DNS query to solidaritedeproximite.org |
| 2016-08-24 16:48:13 | HTTP GET /mhtr.jpg → 37.187.37.150 |
| 2016-08-24 16:56:55 | HTTP GET /HeaderSlice.jpg → 67.132.183.25 |
| 2016-08-24 00:00 – 2016-08-25 00:00 | 401 distinct .txt TargetFilename events under user profile (Sysmon EID 2) |

### Scope

- **Endpoint:** we8105desk (192.168.250.100)
- **User context:** bob.smith.WAYNECORPINC
- **Network:** outbound HTTP to 37.187.37.150 and 67.132.183.25; SMB primarily to 192.168.250.20
- No evidence of lateral movement or encryption on additional hosts at time of triage

### Impact

- **Data availability degraded** on we8105desk due to encryption of at least 401 text files
- No confirmed exfiltration
- Business impact limited to single endpoint at this time

---

## MITRE ATT&CK TTPs Observed

| ID | Technique | Evidence |
|---|---|---|
| T1204.002 | User Execution: Malicious File | VBScript via wscript.exe |
| T1059.005 | Command & Scripting Interpreter: VBScript | 24249.vbs execution |
| T1059.003 | Command & Scripting Interpreter: Windows Command Shell | cmd.exe spawn |
| T1105 | Ingress Tool Transfer | HTTP GET of payloads disguised as images |
| T1071.001 | Application Layer Protocol: Web | HTTP C2 |
| T1486 | Data Encrypted for Impact | 401 .txt files encrypted |

---

## Indicators of Compromise (IOCs)

### Domains/Hosts
- `solidaritedeproximite.org`

### IPs
- `37.187.37.150`
- `67.132.183.25`

### Artifacts / Filenames
- `24249.vbs` — initial dropper
- `121214.tmp` — staged payload
- `mhtr.jpg` — disguised payload #1
- `HeaderSlice.jpg` — disguised payload #2

### USB / Hardware
- USB label: **MIRANDA_PRI** (potential initial vector)

---

## Recommended Actions

### Containment / IR
1. **Isolate** host **we8105desk** from the network immediately
2. **Preserve evidence:** collect disk and memory images; retain `24249.vbs`, `121214.tmp`, relevant Prefetch, and Sysmon/Windows event logs
3. **Reset credentials** for the affected user account; invalidate active sessions/tokens
4. **Reimage and restore** from known-good backups after forensic analysis

### Infrastructure Prevention
1. **Block IOCs** (domain and IPs) at egress controls
2. **Constrain script interpreters** on user endpoints — policy to restrict or approve use of `wscript.exe` / `cscript.exe` via AppLocker/WDAC
3. **Harden USB policy** — restrict removable media, disable autorun, enforce device control

### Detection Improvements
1. Add rule for `wscript.exe` (or `cscript.exe`) → `cmd.exe` parent/child chains with user-profile paths in command line
2. Correlate image downloads (`*.jpg`) + VBS execution + temp staging within short time windows
3. Add rule for first-time contact to newly seen domains followed by script execution on same host
4. Expand SMB anomaly detection for post-encryption lateral writes (early warning if scope expands)

---

*TripleTen Sprint 13 — IR Triage Module · 0x2A Security Investigation*