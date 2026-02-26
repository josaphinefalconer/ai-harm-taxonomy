# Methodology & Design Rationale

## Overview

This document describes the design principles, classification logic, and framework alignment underlying the AI Harm Taxonomy Library.

---

## Classification Approach

### Why Behavioral Indicators?

Most AI harm taxonomies focus on technical system properties (model outputs, training data characteristics, or deployment configurations). This taxonomy takes a different approach: **harm is defined by observable behavioral outcomes**, not system internals.

This matters for several reasons:

1. **Platform-agnostic applicability.** Warning behaviors can be observed by trust & safety teams, researchers, and policymakers without model access.
2. **Early intervention.** Behavioral signals often precede harm materialization, enabling proactive rather than reactive response.
3. **Regulatory relevance.** Governance frameworks (NIST, OECD, ISO) focus on outcomes and impacts, not implementation details. Behavioral grounding supports direct regulatory mapping.

### Severity Calibration

Severity ratings reflect the potential maximum harm magnitude under foreseeable conditions, not average-case outcomes. This is consistent with precautionary approaches in safety-critical systems and with NIST AI RMF guidance on impact assessment.

| Severity | Calibration Rationale |
|---|---|
| Critical | Potential for loss of life, irreversible societal harm, or harm at population scale |
| High | Significant individual or group harm; meaningful long-term consequences |
| Medium | Moderate impact; harm is bounded in scope or remediable |

### Reversibility as a Risk Dimension

Reversibility is treated as an independent risk dimension, not a sub-component of severity. A harm may be medium-severity but irreversible (e.g., Historical Revisionism), requiring different risk treatment than a high-severity but recoverable harm.

---

## Framework Alignment

### NIST AI Risk Management Framework (AI RMF 1.0)

The taxonomy supports NIST AI RMF across the **Map**, **Measure**, and **Manage** functions:

| NIST Function | Taxonomy Application |
|---|---|
| **Map** | Harm categories provide structured risk context for AI system deployment |
| **Measure** | Severity and reversibility ratings support quantitative impact assessment |
| **Manage** | Warning behaviors enable detection thresholds and response triggers |

### OECD AI Principles

The taxonomy directly supports principles 1.3 (Transparency and explainability), 1.4 (Robustness, security and safety), and 1.5 (Accountability) by providing structured harm documentation that supports auditable AI governance.

### ISO/IEC 42001

The taxonomy supports Clause 6 (Planning) and Clause 8 (Operation) by providing a pre-structured harm identification library for AI management system risk assessments.

---

## Category Design Decisions

### Why 8 Categories?

The 8-category structure reflects a balance between specificity and usability:

- **Too few categories** (e.g., 3–4) collapse meaningfully distinct harm pathways
- **Too many categories** (e.g., 20+) creates overlap and reduces practical applicability

The 8 categories were derived by clustering harm types along two axes: **who bears the harm** (individual vs. group vs. society) and **what mechanism produces it** (deception, coercion, surveillance, etc.).

### Category Boundaries

Some harms appear related across categories. Key boundary decisions:

- **Misinformation vs. Persuasion**: Misinformation harms arise from false beliefs; Persuasion harms arise from exploitation of behavioral vulnerabilities regardless of truth value.
- **Harassment vs. Exploitation**: Harassment is primarily relational/emotional harm; Exploitation involves material extraction or systemic abuse of power.
- **Surveillance vs. Discrimination**: Surveillance is the data collection mechanism; Discrimination is the outcome. A surveillance harm may enable a discrimination harm but is categorized by its primary mechanism.

---

## Warning Behavior Methodology

Warning behaviors were selected using three criteria:

1. **Observable without model access** — signals that can be detected by platform operations, researchers, or affected individuals
2. **Temporally upstream of harm** — indicators that precede or accompany harm onset, not retrospective markers
3. **Specific enough to act on** — concrete enough to inform detection rules or policy triggers, not generic risk factors

Each harm type has exactly 3 warning behaviors to enforce prioritization discipline and maintain operational usability.

---

## Limitations

- **Static snapshot**: AI harm patterns evolve rapidly. This taxonomy represents a point-in-time assessment and should be reviewed periodically.
- **Western-centric framing**: Some harm categories and warning behaviors reflect regulatory and cultural contexts primarily from North America and Europe.
- **No quantitative thresholds**: Warning behaviors are qualitative indicators (as of now). Unique I.D. mapping to capture, track, and predict harms for upstream data collection is a project I am currently working on and very interested in. 
- **Emergent harms not fully captured**: Novel harm types arising from new AI capabilities may not fit cleanly into existing categories.

---

*For questions about methodology or framework alignment, open an issue in this repository.*
