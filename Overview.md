# AI Harm Taxonomy Library

A structured, behaviorally-grounded taxonomy of AI-enabled harms, designed to support AI safety research, policy development, platform trust & safety operations, and governance framework alignment.

---

## Overview

The AI Harm Taxonomy Library classifies harms type, **severity**, **reversibility**, **observable behavioral warning indicators**. 

The taxonomy covers **8 top-level harm categories** and **81 distinct harm types**, each documented with:

- **Severity** — Critical / High / Medium
- **Reversibility** — None / Low / Partial / High / Unknown
- **Description** — High-level definition of the harm
- **Top 3 Warning Behaviors** — Observable online signals that the harm may be actively occurring

### Framework Alignment

This taxonomy was developed with reference to:

| Framework | Relevance |
|---|---|
| [NIST AI RMF](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf) | Risk identification and measurement |
| [OECD AI Principles](https://oecd.ai/en/ai-principles) | Trustworthy AI and human-centered values |
| [ISO/IEC 42001](https://www.iso.org/standard/81230.html) | AI management system requirements |

---

## Harm Categories

| ID | Category | Harm Types |
|---|---|---|
| CAT-01 | [Harassment](#cat-01-harassment) | 9 |
| CAT-02 | [Misinformation](#cat-02-misinformation) | 10 |
| CAT-03 | [Persuasion](#cat-03-persuasion) | 10 |
| CAT-04 | [Self-Harm](#cat-04-self-harm) | 9 |
| CAT-05 | [Exploitation](#cat-05-exploitation) | 14 |
| CAT-06 | [Surveillance](#cat-06-surveillance) | 9 |
| CAT-07 | [Discrimination](#cat-07-discrimination) | 9 |
| CAT-08 | [Endangerment](#cat-08-endangerment) | 11 |

---

## Severity & Reversibility Reference

### Severity Levels

| Level | Definition |
|---|---|
| **Critical** | Potential for irreversible, large-scale, or life-threatening harm |
| **High** | Significant harm to individuals or groups; meaningful long-term impact |
| **Medium** | Moderate harm; limited in scope or recoverable with intervention |

### Reversibility Levels

| Level | Definition |
|---|---|
| **None** | Harm cannot be undone once it occurs |
| **Low** | Harm is largely permanent; partial remediation possible at high cost |
| **Partial** | Harm can be reduced or mitigated but not fully reversed |
| **High** | Harm is temporary or fully correctable |
| **Unknown** | Reversibility cannot be determined (e.g., novel AI misalignment scenarios) |

---


---

## Data Format

Each harm entry in `data/ai-harm-taxonomy.json` follows this schema:

```json
{
  "id": "CAT-01-001",
  "harm_type": "Harassment / Targeted Abuse",
  "severity": "High",
  "reversibility": "Partial",
  "description": "Repeated targeting of specific individuals with hostile or threatening content.",
  "warning_behaviors": [
    "Repeated @-mentions or replies with hostile language",
    "Screenshots of target shared in group chats or forums",
    "Use of multiple accounts to evade blocks"
  ]
}
```

---

## Usage

### Filter by severity

```python
import json

with open("data/ai-harm-taxonomy.json") as f:
    taxonomy = json.load(f)

critical_harms = [
    harm
    for cat in taxonomy["categories"]
    for harm in cat["harms"]
    if harm["severity"] == "Critical"
]
```

### Get all warning behaviors across categories

```python
all_warnings = [
    {"id": harm["id"], "harm_type": harm["harm_type"], "warning": wb}
    for cat in taxonomy["categories"]
    for harm in cat["harms"]
    for wb in harm["warning_behaviors"]
]
```

### Filter by category

```python
surveillance_harms = next(
    cat["harms"]
    for cat in taxonomy["categories"]
    if cat["name"] == "Surveillance"
)
```

---

## Intended Audiences

- **AI Safety Researchers** — Reference framework for harm classification and behavioral threat modeling
- **Policy Analysts** — Input for AI governance documentation and regulatory alignment
- **Trust & Safety Teams** — Operational signal library for detection rule development
- **AI Developers** — Pre-deployment risk checklist aligned to major governance frameworks

---

## Design Principles

**Behavioral grounding over technical abstraction.** Warning indicators are defined as observable human behaviors rather than technical system states, making them applicable across platforms and deployment contexts.

**Severity-weighted, not binary.** Harm classification acknowledges gradations of impact and the critical role of reversibility in risk prioritization.

**Governance-aligned.** Categories and definitions are mapped to NIST, OECD, and ISO frameworks to support regulatory and audit use cases.

---

