# Traceability and Truth-Drift Tracker

This file tracks the alignment and discrepancies between the **Manuscript Draft**, the **Technical Specification** (Single Source of Truth), and the **Actual Source Code** (Implementation). 

**Usage**: Update this file whenever a new section is drafted or a technical claim is made. Use this to ensure the article remains grounded in reality even if the spec is outdated.

---

## 1. Active Discrepancy Matrix

| Feature / Element | Manuscript Draft (`article.qmd`) | Technical Spec (`docs/pl-Edu-Bad/`) | Source Code (`plat-edu-bad-mvp/`) | Alignment Status |
| :--- | :--- | :--- | :--- | :--- |
| **Engine ID** | `engine_bench_1` | `Engine_bench-R121` | `engine_bench_1` | ✅ **Grounded in Code.** Spec is outdated. |
| **Algae ID** | `inside_farm_r121` | `Algae-inside-farm-R121` | `inside_farm_r121` | ✅ **Grounded in Code.** Spec uses Pascal-Kebab. |
| **Measurement** | `algae_farm` | `algae-farm-1` | `algae_farm` | ✅ **Grounded in Code.** Spec enforces numbering. |
| **Simulation Logic** | `Strict Corridor (±2%)` | **ABSENT** | `Math.abs(prevVal) * 0.02` | ⚠️ **Grounding Gap.** Algorithm exists in Code but not in Spec. |

---

## 2. Implementation Details (Extracted from Code)

### Stochastic Corridor Algorithm
- **Definition**: Each data point is constrained to a window relative to its predecessor.
- **Formula**: `newVal = prevVal + ((Math.random() - 0.5) * 2 * (prevVal * 0.02))`
- **Enforcement**: Applied globally across all simulation flows (Engine, Algae, Wind, PV) in the Node-RED middleware.

### Metadata Tags (Confirmed from InfluxDB Ingestion)
- `device_id`: Hardcoded per flow.
- `device_type`: Matches Category name.
- `location`: e.g., `site_e`, `site_f`.
- `status`: e.g., `operational`, `Generating`.
