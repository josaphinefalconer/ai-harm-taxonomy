# Data Files

This directory contains the AI Harm Taxonomy in two formats. Both files represent the same dataset. Choose the format that fits your workflow.

---

## Files

### `ai-harm-taxonomy.json`
Structured JSON with full nested hierarchy. Best for programmatic access, building applications, or integrating the taxonomy into pipelines.

### `ai-harm-taxonomy.csv`
Flat tabular format with one row per harm type. Best for analysis in Excel, Google Sheets, Pandas, or R — and for filtering, sorting, and building visualizations without writing a parser.

---

## Schema

Both files share the same fields:

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique harm identifier, e.g. `CAT-01-003` |
| `category_id` | string | Parent category identifier, e.g. `CAT-01` |
| `category` | string | Category name, e.g. `Harassment` |
| `harm_type` | string | Specific harm type name |
| `severity` | string | `Critical`, `High`, or `Medium` |
| `reversibility` | string | `None`, `Low`, `Partial`, `High`, or `Unknown` |
| `description` | string | Concise definition of the harm |
| `warning_behavior_1` | string | First observable warning indicator |
| `warning_behavior_2` | string | Second observable warning indicator |
| `warning_behavior_3` | string | Third observable warning indicator |

> In the JSON file, `warning_behavior_1/2/3` are stored as a `warning_behaviors` array. In the CSV they are split into three separate columns for easier filtering.

---

## Categories

| Category ID | Name | Harm Types |
|---|---|---|
| CAT-01 | Harassment | 9 |
| CAT-02 | Misinformation | 10 |
| CAT-03 | Persuasion | 10 |
| CAT-04 | Self-Harm | 9 |
| CAT-05 | Exploitation | 14 |
| CAT-06 | Surveillance | 9 |
| CAT-07 | Discrimination | 9 |
| CAT-08 | Endangerment | 11 |

**Total: 81 harm types across 8 categories**

---

## Severity & Reversibility Values

### Severity
- `Critical` — Potential for irreversible, large-scale, or life-threatening harm
- `High` — Significant harm to individuals or groups with meaningful long-term impact
- `Medium` — Moderate harm; limited in scope or recoverable with intervention

### Reversibility
- `None` — Harm cannot be undone once it occurs
- `Low` — Largely permanent; partial remediation possible at high cost
- `Partial` — Can be reduced or mitigated but not fully reversed
- `High` — Temporary or fully correctable
- `Unknown` — Cannot be determined (e.g. novel AI misalignment scenarios)

---

## Quick Usage

**Python — load CSV**
```python
import pandas as pd

df = pd.read_csv("ai-harm-taxonomy.csv")

# All critical harms
critical = df[df["severity"] == "Critical"]

# Filter to a single category
persuasion = df[df["category"] == "Persuasion"]

# All warning behaviors as a flat list
warnings = pd.concat([
    df[["id", "harm_type", "warning_behavior_1"]].rename(columns={"warning_behavior_1": "warning"}),
    df[["id", "harm_type", "warning_behavior_2"]].rename(columns={"warning_behavior_2": "warning"}),
    df[["id", "harm_type", "warning_behavior_3"]].rename(columns={"warning_behavior_3": "warning"}),
])
```

**Python — load JSON**
```python
import json

with open("ai-harm-taxonomy.json") as f:
    taxonomy = json.load(f)

# All harms where reversibility is None
irreversible = [
    harm
    for cat in taxonomy["categories"]
    for harm in cat["harms"]
    if harm["reversibility"] == "None"
]
```

**R — load CSV**
```r
library(tidyverse)

df <- read_csv("ai-harm-taxonomy.csv")

# Severity distribution by category
df %>%
  count(category, severity) %>%
  arrange(category, severity)
```

---

For methodology and framework alignment rationale, see [`docs/METHODOLOGY.md`](../docs/METHODOLOGY.md)
