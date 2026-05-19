# Sprint 14 — Complex Attack Investigation

**Type:** Multi-stage Attack Triage  
**Source:** Multi-source SIEM (Sysmon, network logs, registry artifacts)  
**Deliverables:** IR Triage Report · Investigation Notes · Obfuscation Worksheet  

---

## Objective

Investigate a complex, multi-stage attack scenario combining obfuscation techniques, multiple TTPs, and correlation across multiple data sources. Reconstruct the attack timeline, identify all affected assets, and document IOCs.

---

## Investigation Approach

### Multi-source Correlation
- **Sysmon** — process lineage, file operations, registry modifications
- **Network logs** — DNS, HTTP, SMB telemetry
- **Registry artifacts** — persistence and configuration changes
- **Obfuscation analysis** — decoded encoded payloads/commands

### Obfuscation Handling
Tracked obfuscated artifacts on dedicated worksheet:
- Base64-encoded command strings
- Hex-encoded payloads
- Variable name and string mangling
- Layered obfuscation requiring iterative deobfuscation

### Timeline Reconstruction
Cross-referenced timestamps across Sysmon EventIDs, network flow records, and registry hive last-write times to build authoritative attack timeline.

---

## Deliverables

- **IR Triage Report** — analyst-facing summary with disposition, scope, impact, MITRE mapping, and recommendations
- **Investigation Notes** — full evidence trail, raw queries, intermediate findings (42 MB document — extensive)
- **Obfuscation Worksheet** — decoded artifacts with original/decoded pairs and analysis notes

---

## Skills Demonstrated

`Multi-source SIEM Correlation` `Obfuscation Analysis` `Process Lineage Investigation` `Timeline Reconstruction` `MITRE TTP Mapping` `Sysmon Forensics`

---

## Related Work

This sprint builds on Sprint 12 (brute force triage) and Sprint 13 (ransomware investigation) — extending IR capability to handle multi-stage, obfuscated attacker behavior typical of advanced threats.

---

*TripleTen Sprint 14 — Advanced Threat Investigation Module*