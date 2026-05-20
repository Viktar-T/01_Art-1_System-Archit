# Traceability and Truth-Drift Tracker

This file tracks the active discrepancies and technical drifts between the **Manuscript Draft** (`article.qmd`), the **Technical Specification** (`IoT_Data_Arch-JSON-MQTT.md`), and the **Actual Source Code** (`plat-edu-bad-data-mvp/`).

---

## 1. Active Discrepancy Matrix

| Feature / Element | Manuscript Draft (`article.qmd`) | Technical Spec (`IoT_Data_Arch-JSON-MQTT.md`) | Source Code (`plat-edu-bad-data-mvp/`) | Drift Status & Description |
| :--- | :--- | :--- | :--- | :--- |
| **Engine ID** | `engine_bench_1` | `Engine_bench-R121` | `engine_bench_1` (topic / station_id) | **Active Spec Drift.** The manuscript and codebase utilize `engine_bench_1` for consistency. The specification contains the outdated `Engine_bench-R121`. |
| **Algae ID** | `inside_farm_r121` | `Algae-inside-farm-R121` | `inside_farm_r121` (topic / station_id) | **Active Spec Drift.** The manuscript and codebase use lowercase Snake-Case `inside_farm_r121`. The spec uses Pascal-Kebab formatting. |
| **Measurement** | `algae_farm` (payload `device_type`) | `algae-farm-1` | `algae_telemetry` (InfluxDB) | **Active Ingestion Drift.** The payload identifies the device as `algae_farm`, but the ingestion gateway writes data to `algae_telemetry`. |
| **Simulation Logic** | `Strict Corridor (±2%)` | **ABSENT** | `Math.abs(prevVal) * 0.02` | **Active Grounding Gap.** The manuscript and code implement a stochastic recursive random walk. This algorithm is completely missing in the specification. |
| **Engine Category** | `engine_bench` | `engine` | `engine_bench` (topic) / `engine_bench_telemetry` | **Active Spec Drift.** The spec outlines the category level as `engine`, whereas code and manuscript use `engine_bench`. |

---

## 2. Technical Ground Truth Details (Extracted from Code)

### Stochastic Corridor Algorithm
- **Formula**: `newVal = prevVal + ((Math.random() - 0.5) * 2 * (prevVal * 0.02))`
- **Enforcement**: Applied in the Node-RED middleware flows to simulate physical inertia across all 12 energy vectors.

### Ingested Database Tags (InfluxDB 2.x)
- `station_id`: Parsed dynamically from the 4th element of the topic path (e.g., `inside_farm_r121`, `engine_bench_1`).
- `category`: Parsed dynamically from the 3rd element of the topic path (e.g., `algae`, `engine_bench`).
- `site_id`: Hardcoded to `"wksir_kioze"`.
- `device_model`: Extracted from payload (`incoming.device_type` or `incoming.device_model`).
- `connection_type`: Extracted from payload (`mqtt_telemetry`).
- *Omission Note*: The payload key `device_id` is parsed but dropped by the ingestion flow and not saved as an InfluxDB tag.
