# Sprint 4 — Threat Modeling: Xibalba Interactive

**Type:** Application Threat Modeling  
**Client:** Xibalba Interactive  
**Deliverables:** Threat Modeling Worksheet · Threat Model Report  

---

## Objective

Apply structured threat modeling methodology to Xibalba Interactive's application architecture. Identify threats systematically, evaluate them, and recommend mitigations.

---

## Methodology

Applied **STRIDE** threat classification:

| Letter | Threat | Property Violated |
|---|---|---|
| S | Spoofing | Authentication |
| T | Tampering | Integrity |
| R | Repudiation | Non-repudiation |
| I | Information Disclosure | Confidentiality |
| D | Denial of Service | Availability |
| E | Elevation of Privilege | Authorization |

### Process

1. **Decompose** the application — Data Flow Diagrams (DFD)
2. **Identify trust boundaries** between components
3. **Enumerate threats** per element using STRIDE
4. **Rate threats** by likelihood and impact
5. **Define mitigations** mapped to specific controls

---

## Deliverables

- **Threat Modeling Worksheet** — per-element STRIDE enumeration with severity scoring
- **Threat Model Report** — executive summary, DFD, identified threats, and mitigation recommendations

---

*TripleTen Sprint 4 — Threat Modeling Module*