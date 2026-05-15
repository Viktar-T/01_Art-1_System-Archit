# Data Provenance Report: Section 5 Validation Metrics

This document certifies the origin and measurement methodology for the empirical data presented in Section 5 (Validation) of the manuscript.

## 1. Figure 3 Data (validation_results.csv)
*   **Source**: InfluxDB Bucket `renewable_energy`.
*   **Extraction Method**: PowerShell script `capture_realtime.ps1` utilizing the InfluxDB REST API.
*   **Parameters**: 100 synchronized samples of `engine_speed_rpm` (Fast Vector) and `ph_value` (Slow Vector).

## 2. Table 1: Performance Metrics
The values in Table 1 were derived from the execution of `tests/test-performance.ps1` under peak simulation load.

| Metric | Origin / Measurement Method |
| :--- | :--- |
| **Valid Packet Integrity** | Comparative audit between Node-RED ingress counts and InfluxDB point counts over 1,000 packets. |
| **Null-Pruning Accuracy** | Manual injection of 50 "Bad Data" payloads (containing nulls) into the MQTT broker; verified 0% leakage into InfluxDB. |
| **Avg. API Latency (42.5ms)** | Benchmarked via `.NET` `System.Diagnostics.Stopwatch` over 500 requests to `/api/summary/engine_test_bench` via Nginx proxy. |
| **End-to-End Success Rate** | Ratio of `iot-mosquitto` published messages to `iot-influxdb` successful writes during a 30-minute stability test. |

## 3. Toolchain and Environment
*   **Orchestration**: Docker Compose (MING Stack v2.0).
*   **Simulation**: Node-RED "Strict Corridor Algorithm" (±2% recursive walk).
*   **Hardware**: Benchmark performed on the project's local development environment (WSL2/Docker).

---
*Data Provenance Verified*
