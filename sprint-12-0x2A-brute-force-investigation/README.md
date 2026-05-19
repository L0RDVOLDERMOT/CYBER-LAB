# Sprint 12 — IR Triage: WordPress Brute Force Investigation

**Analyst:** Chibuike Ojukwu  
**Date:** 2025-08-25  
**Source:** ModSecurity CRS on Apache  
**Alert ID:** ZgUGhV1CEwAABx43AYAAAAAB  
**Severity:** HIGH  
**Disposition:** True Positive (TP)  

---

## Initial Findings

- **Incident type:** Brute-force authentication against WordPress `/wp-login.php` from **192.168.100.20** using **Mozilla/5.0 (Hydra)** user agent.
- **Scope (confirmed):** Traffic between attacker **192.168.100.20** and web server **192.168.100.2** only. Four successful logins for user **elliot**.
- **Key proof points:**
  - PCAP shows multiple POSTs to `/wp-login.php`
  - **Four** server responses are **HTTP/1.0 302 Found** with **Location: /wp-admin/** (success indicator)
  - The T6b 302 in attack1.pcap redirects to `/wp-login.php` (not success) and is excluded

---

## Incident Summary

### Time Bounds (UTC)

| Field | Value |
|---|---|
| **Start** | 2025-04-10 15:42:22.305094 (attack2.pcap, pkt 647, stream 18) |
| **End** | 2025-04-10 15:48:41.992074 (attack1.pcap, pkt 10694, stream 595) |
| **Duration** | 379.687 seconds (~6 min 19.687 s) |

### Timeline of Key Events

| Time (UTC) | Event | Evidence |
|---|---|---|
| 15:42:22.305094 | **Attack start** — GET /wp-login.php (Hydra UA) | attack2.pcap pkt 647, stream 18 |
| 15:42:28.553779 | **Successful login #1** — 302 → /wp-admin/ | attack2.pcap pkt 8446, stream 513 |
| 15:42:37.947010 | **Successful login #2** — 302 → /wp-admin/ | attack2.pcap pkt 17040, stream 1082 |
| 15:42:47.540769 | **Successful login #3** — 302 → /wp-admin/ | attack2.pcap pkt 25948, stream 1646 |
| 15:42:56.170667 | **Successful login #4** — 302 → /wp-admin/ | attack2.pcap pkt 34575, stream 2239 |
| 15:48:41.439508 | 302 redirect to /wp-login.php (not success) | attack1.pcap pkt 9809, stream 539 |
| 15:48:41.992074 | **Attack end** — last 200 OK to /wp-login.php | attack1.pcap pkt 10694, stream 595 |

### Scope

- **Attacker host:** 192.168.100.20
- **Target host/service:** 192.168.100.2 — WordPress login over HTTP/80 (WP version 6.7.2 per login page assets)
- **Accounts affected:**
  - **elliot** — 4 successful authentications
  - **admin** — credentials observed in PCAP (`Triple10.`) but no successful login evidenced
- **Post-login actions:** Unknown — no WP activity logs or Apache access logs post-login available

### Impact

- Verified compromise of one WordPress user account (**elliot**) via four successful logins
- Credentials exposed in **cleartext over HTTP** for both elliot and admin during attempts
- No evidence of lateral movement or content/admin changes — post-login activity not observable with current artifacts

---

## SIEM Corroboration (Splunk / Zeek)

Representative Zeek event from `index=client0 source=http.log sourcetype=zeek_json`:

```
index=client0 sourcetype=zeek_json
| search src_ip=192.168.100.20 dest_ip=192.168.100.2
| search uri="/wp-login.php" user_agent="Mozilla/5.0 (Hydra)"
| stats count by status_code, src_ip, dest_ip
```

**Analyst note:** Zeek `http.log` typically does **not** record the Location header, so Splunk alone cannot distinguish success (302 → /wp-admin/) from non-success (302 → /wp-login.php). **PCAP is ground truth** for confirming compromise.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force: Password Guessing | T1110.001 |
| Command & Control | Application Layer Protocol: Web | T1071.001 |

---

## Recommended Actions

### IR / Containment (Immediate)
1. **Reset credentials** for elliot and admin. Invalidate active sessions/cookies for elliot.
2. **Force HTTPS** — disable HTTP on the WordPress site. Obtain/enable TLS. Add HSTS to prevent credential leakage.
3. **Temporary WAF rate-limiting** and IP reputation / geo-AS throttling for `/wp-login.php`.
4. **Review post-login behavior** — pull Apache access/error logs and WP activity/audit logs from 15:42:28–15:43:30 UTC to determine actions taken after each successful login.

### Prevention (Infrastructure)
1. Enforce **account lockout / slowdown** and/or **CAPTCHA** on login after N failed attempts.
2. Require **MFA** for WordPress (editor/admin roles minimum; ideally all users).
3. Keep WordPress and plugins current. Restrict `/xmlrpc.php` if not needed.
4. Hide verbose authentication errors.

### Detection / SOC Improvements
1. Splunk correlation: failed attempts from source followed by 302(s) to `/wp-admin/` within short window → raise priority.
2. Maintain Zeek pivot above as saved search for Hydra UA against `/wp-login.php`.
3. Add pcap-driven validation (or reverse proxy logs with Location) to programmatically distinguish success vs non-success 302s.

### Policy / Process
1. Require TLS-only for any authentication surface. No exceptions.
2. Document quick triage SOP for WordPress brute force (filters, stream IDs, success criteria = 302 → /wp-admin/).

---

## Evidence Appendix

| Fact | How to Re-obtain |
|---|---|
| Attack start | attack2.pcap → `tcp.stream == 18` → earliest GET /wp-login.php = pkt 647, 15:42:22.305094 UTC |
| Successful logins | attack2.pcap streams 513, 1082, 1646, 2239 — all HTTP/1.0 302 + Location: /wp-admin/ |
| Non-success 302 | attack1.pcap pkt 9809, stream 539 → Location: /wp-login.php |
| Attack end | attack1.pcap → `http.response.code == 200` → last match pkt 10694, stream 595 |
| Credentials exposed | attack2.pcap streams 513/1082/1646/2239: `log=elliot&pwd=...` | attack1.pcap stream 539: `log=admin&pwd=Triple10.` |

---

*TripleTen Sprint 12 — IR Triage Module*