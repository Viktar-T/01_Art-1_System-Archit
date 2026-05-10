# Architecture and Universal Data Schemas for the KIOZE Edu-Bad Platform

## Table of Contents

- [Project Overview](#project-overview)
- [Architectural Principles and Data Ingestion Strategy](#architectural-principles-and-data-ingestion-strategy)
- [System Architecture Overview](#system-architecture-overview)
- [Deployment Environments](#deployment-environments)
- [Data Pipeline](#data-pipeline)
- [MQTT Security Configuration](#mqtt-security-configuration)
- [Rigorous MQTT Topic Taxonomy](#rigorous-mqtt-topic-taxonomy)
- [InfluxDB Schema Reference](#influxdb-schema-reference)
- [Category 1: Photovoltaic (PV) Systems](#category-1-photovoltaic-pv-systems)
- [Category 2: Wind Energy Systems](#category-2-wind-energy-systems)
- [Category 3: Biogas Systems](#category-3-biogas-systems)
- [Category 4: Heat (Stirling) Systems](#category-4-heat-stirling-systems)
- [Category 5: Algae Photobioreactors](#category-5-algae-photobioreactors)
- [Category 6: Engine Bench Systems](#category-6-engine-bench-systems)
- [Category 7: Energy Storage Systems](#category-7-energy-storage-systems)
- [API Layer](#api-layer)
- [Physical Device Onboarding Contract](#physical-device-onboarding-contract)
- [Implementation Notes & Known Gaps](#implementation-notes--known-gaps)

## Project Overview

The **KIOZE Edu-Bad** platform (`edubad.zut.edu.pl`) is an educational renewable-energy IoT monitoring system developed at the Wydział Kształtowania Środowiska i Rolnictwa (WKSIR), Zachodniopomorski Uniwersytet Technologiczny (ZUT). It ingests, stores, and visualises real-time telemetry from six renewable-energy technology categories—photovoltaic, wind, biogas, heat/Stirling, algae photobioreactors, and engine test benches—plus an energy-storage sub-system.

The platform runs entirely as Docker containers orchestrated via `docker-compose.yml`. The current deployment is a **simulation MVP**: all sensor data is generated synthetically inside Node-RED using physics-based mathematical models. The architecture is designed to accept real physical devices once the MQTT topic alignment and security hardening steps described in [Implementation Notes](#implementation-notes--known-gaps) are completed.

---

## Architectural Principles and Data Ingestion Strategy

The transition from physical sensor arrays to actionable, real-time analytics relies entirely on a standardized, predictable flow of data. The edge devices reading serial protocols must normalize the raw hexadecimal registers into structured, human-readable formats. The architectural constraint applied to this ingestion pipeline is the Canonical Data Model (CDM) approach. This dictates that a single, universal JSON "superset" template is utilized per device category, encompassing all possible parameters across all specific stations within that functional category. If a specific station lacks a particular sensor—for instance, an outdoor algae reactor lacking an optical density sensor—the edge device is programmed to transmit a null value for that specific field.

This superset approach is highly optimized for the internal mechanisms of InfluxDB. InfluxDB utilizes a Line Protocol that handles sparse data structures with extreme efficiency. When the Node-RED middleware receives the JSON payload, it executes a transformation script that dynamically strips any key containing a null value prior to constructing the database write operation. Consequently, storage capacity is not wasted on empty fields, yet the overarching measurement schema remains unified. This uniformity allows for unified Grafana dashboard variables, seamless cross-station aggregations, and the application of standardized machine learning models across the entire fleet of devices.

To manage InfluxDB cardinality effectively, the CDMs strictly differentiate between tags and fields. Tags contain metadata, such as the site identifier, device model, and connection type. These tags are indexed by the database, making them ideal for rapid GROUP BY queries and filtering operations. Conversely, fields contain the highly variable telemetry data, such as voltages, temperatures, and rotational speeds. Fields are not indexed, which prevents runaway cardinality that would otherwise degrade database write performance over time.

---

## System Architecture Overview

The platform is composed of seven containerised services that communicate over an internal Docker bridge network (`iot-network`, subnet `172.20.0.0/16`). A single Nginx reverse proxy exposes all services to the outside world on a single HTTP port.

```
┌───────────────────────────────────────────────────────────┐
│                  edubad.zut.edu.pl (:80)                  │
│                    Nginx Reverse Proxy                     │
│  /          → React Frontend  (Vite + Leaflet)            │
│  /api/      → Express.js API  (:3001 internal)            │
│  /grafana/  → Grafana         (:3000 internal)            │
│  /nodered/  → Node-RED        (:1880 internal)            │
│  /influxdb/ → InfluxDB UI     (:8086 internal)            │
└───────────┬───────────────────────────────────────────────┘
            │
 ┌──────────▼────────────────────────────────────────┐
 │              Docker Internal Network               │
 │                                                    │
 │  ┌─────────────┐    MQTT     ┌─────────────────┐  │
 │  │   Node-RED  │◄──────────►│   Mosquitto     │  │
 │  │  (10 flows) │  :1883/:9001│   MQTT Broker   │  │
 │  │  Simulation │            │   + ACL / passwd │  │
 │  │  + CDM Xfrm │            └─────────────────┘  │
 │  └──────┬──────┘                                  │
 │         │  InfluxDB Line Protocol                  │
 │  ┌──────▼──────────────────────────────────────┐  │
 │  │         InfluxDB 2.7                         │  │
 │  │   org: renewable_energy_org                  │  │
 │  │   bucket: renewable_energy  (30-day TTL)     │  │
 │  └──────┬──────────────┬──────────────┬────────┘  │
 │         │ Flux queries │              │            │
 │  ┌──────▼──────┐  ┌───▼──────┐  ┌───▼────────┐  │
 │  │   Grafana   │  │ Express  │  │  React /   │  │
 │  │  Dashboards │  │   API    │  │  Frontend  │  │
 │  └─────────────┘  └──────────┘  └────────────┘  │
 └────────────────────────────────────────────────────┘
```

### Container Summary

| Container | Image | Internal Port | External Port | Role |
| :---- | :---- | :---- | :---- | :---- |
| `iot-mosquitto` | eclipse-mosquitto:2.0.18 | 1883 (MQTT), 9001 (WS) | 40098 | MQTT broker |
| `iot-influxdb2` | influxdb:2.7 | 8086 | via Nginx | Time-series database |
| `iot-node-red` | node-red (custom) | 1880 | via Nginx `/nodered/` | Data processing & simulation |
| `iot-grafana` | grafana:10.2.0 | 3000 | via Nginx `/grafana/` | Dashboards |
| `iot-api` | node:20-alpine (custom) | 3001 | via Nginx `/api/` | REST API backend |
| `iot-frontend` | nginx-alpine (custom) | 80 | via Nginx `/` | React SPA |
| `iot-nginx` | nginx:alpine | 80, 443 | 80 (prod) | Reverse proxy |

---

## Deployment Environments

| Environment | Nginx Port | MQTT Port | Notes |
| :---- | :---- | :---- | :---- |
| Local development | 8080 | 1883 | `docker-compose.local.yml`; container suffix `-local` |
| Production (edubad) | 80 | 40098 | `docker-compose.yml`; hostname `edubad.zut.edu.pl` |
| Production (Mikrus VPS) | 20108 | 40098 | `docker-compose.mikrus.yml`; additional ports 40099–40101 |

---

## Data Pipeline

```
1. SIMULATE  Node-RED inject timer (every 3–5 s)
             → physics-based data generator function
             → fault-injection overlay (0.1 % probability)

2. PUBLISH   Node-RED MQTT-out node
             → topic: devices/<category>/<device_id>/telemetry
             → Mosquitto broker

3. SUBSCRIBE Node-RED MQTT-in node (same flow, wildcard)
             → devices/<category>/+/telemetry

4. VALIDATE  Node-RED switch/function node
             → range checks, type coercion
             → invalid path → error log

5. TRANSFORM Node-RED CDM transformer function
             → strip null fields
             → map to InfluxDB field/tag schema

6. PERSIST   Node-RED influxdb-out node
             → measurement: <see InfluxDB Schema Reference>
             → bucket: renewable_energy
             → org: renewable_energy_org
             → precision: ms

7. QUERY     Express.js API (Flux queries via InfluxDB client)
             Grafana (native InfluxDB 2.x datasource, Flux)

8. VISUALISE React frontend (via /api/summary/:machine)
             Grafana dashboards (5 provisioned panels)
```

---

## MQTT Security Configuration

The broker enforces username/password authentication via a password file (`mosquitto/config/passwd`). Anonymous connections are rejected (`allow_anonymous false`). An ACL file (`mosquitto/config/acl`) defines per-role permissions:

| Principal | Permission |
| :---- | :---- |
| Physical device (e.g. `pv_001`) | `write devices/<type>/<id>/data`, `write devices/<type>/<id>/status`, `read devices/<type>/<id>/commands` |
| Node-RED service | `read devices/+/+/data`, `read devices/+/+/status`, `write devices/+/+/commands`, `readwrite system/health/+`, `readwrite system/alerts/+` |
| Grafana service | `read devices/+/+/data`, `read devices/+/+/status`, `read system/#` |
| Admin | `readwrite #` (full access) |
| Monitor | `read #` (read-only) |

Broker limits: `max_connections 1000`, `max_queued_messages 100`, `max_inflight_messages 20`, persistence autosave every 1800 s.

---

## Rigorous MQTT Topic Taxonomy

A hierarchical, wildcard-friendly MQTT topic structure is paramount for efficient routing, payload segregation, and security management. The taxonomy adheres to the following strict spatial and logical hierarchy: `wksir/kioze/<category>/<specific_station>/<telemetry_group>`.

| Taxonomy Level | Description and Purpose | Example Values |
| :---- | :---- | :---- |
| **Root Tenant** | The overarching digital factory infrastructure identifier. | wksir |
| **Sub-Tenant** | Departmental identifier (Wydział Kształtowania Środowiska i Rolnictwa). | kioze |
| **Category** | The logical grouping of the equipment based on energy type. | pv, wind, biogas, heat, algae, engine, storage |
| **Station** | The exact physical device, testbed, or installation. | pv\_rotate, big\_vertical\_storage, small\_plan |
| **Telemetry Group** | Operational classification for backend routing segregation. | telemetry, status, alarms, cmd |

This structure allows the Node-RED flow dedicated to TSDB ingestion to subscribe efficiently to `wksir/kioze/+/+/telemetry`, capturing all time-series metrics while safely ignoring configuration commands or static status updates. Conversely, an alerting or fault-prediction engine can subscribe exclusively to `wksir/kioze/+/+/alarms` to trigger immediate maintenance notifications.

> **Implementation note:** The current Node-RED simulation flows and ACL use the alternate prefix `devices/<category>/<device_id>/telemetry`. See [Implementation Notes](#implementation-notes--known-gaps) for the full gap analysis.

---

## InfluxDB Schema Reference

All telemetry is written to a single bucket `renewable_energy` (organisation `renewable_energy_org`, 30-day retention). The Node-RED `influxdb out` nodes define the measurement name and tag template per flow.

| Node-RED Flow (Tab) | Measurement Name | Station / Device |
| :---- | :---- | :---- |
| Ładowarka słoneczna (Solar Charger) | `pv-hulajnogi` | PV-Hulajnogi-Outside-R06 |
| Panele fotowoltaiczne (PV Panels) | `pv-hybrid` | PV-Rotate / PV-Agro-small |
| Turbina wiatrowa VAWT | `wind-vawt` | Wind-Big-Vertical-Storage |
| Turbina wiatrowa HAWT | `wind-hawt-hybrid` | Solar-Wind Hybrid (HAWT) |
| Biogazownia | `biogas-plant` | Biogaz-KIOZE-small\_plan |
| Stirling-Ogniwo-Magazyn | `heat-boiler` | Heat-Stirling-Storage |
| Stanowisko silnika | `engine-test-bench` | Engine\_bench-R121 |
| Converter & Storage | `energy-storage` | Turbine\_IS (Energy Storage) |
| Farma Alg 1 | `algae-farm-1` | Algae-inside-farm-R121 |
| Farma Alg 2 | `algae-farm-2` | Algae-outside |

Tags written per measurement: `device_id`, `device_type`, `location`, `status`.

> **Naming convention issue:** Measurement names use hyphens (e.g. `pv-hybrid`) instead of underscores. Flux queries must quote these names with backticks: `` from(bucket:"renewable_energy") |> filter(fn: (r) => r._measurement == "pv-hybrid") ``. Future physical-device integration should adopt underscore names (e.g. `pv_hybrid`) to eliminate this quoting requirement.

---

## Category 1: Photovoltaic (PV) Systems

The photovoltaic ecosystem within the KIOZE facility comprises distinct sub-systems designed to test various modes of solar generation. These include standard grid-tied micro-installations (PV-Hulajnogi-Outside-R06), advanced solar tracking mechanisms (PV-Rotate), and agrophotovoltaic testbeds (PV-Agro-small). The superset data model must synthesize parameters from advanced string inverters alongside independent charge controllers and physical tracking actuators.

A detailed analysis of the primary inverter utilized in these installations, the SOFAR 1.1K\~3.3KTL-G3 series, reveals a complex Modbus RTU communication protocol mapping. The inverter utilizes specific hexadecimal registers to broadcast grid parameters, including protections for over-voltage (GridOVP, ID01), under-voltage (GridUVP, ID02), and over-frequency (GridOFP, ID03). The system continuously monitors the DC input generated by the PV array, filtering it through an input board that performs crucial diagnostic functions, such as the detection of insulation impedance, before the current reaches the power inversion board. The inverter's efficiency relies heavily on its Maximum Power Point Tracking (MPPT) algorithm, which scans for the optimal voltage-current ratio.

For the PV-Rotate station, mechanical tracking parameters must be incorporated. Solar trackers aim to maximize irradiance capture by ensuring the photovoltaic panels receive the sun's rays perpendicularly, which can theoretically increase yield by up to 30%. This introduces the need for telemetry regarding azimuth and elevation angles. Furthermore, hybrid or off-grid setups mandate the inclusion of battery state-of-charge (SOC) metrics, battery voltage, and specialized charge controller states.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Electrical (DC Input)** | PV Voltage, PV Current, Insulation Impedance. | SOFAR Modbus Registers. |
| **Electrical (AC Output)** | Grid Voltage, Grid Current, Grid Frequency, Active/Reactive Power. | Grid synchronization and fault detection. |
| **Energy Yield** | Energy Today, Total Energy. | Cumulated values for performance analysis. |
| **Mechanical Tracking** | Tracker Azimuth, Tracker Elevation. | Maximizing perpendicular irradiance. |
| **Battery Storage** | Battery Voltage, Charge Current, State of Charge (SOC). | Off-grid hybrid load balancing. |
| **Environmental** | Inverter Temperature, Panel Temperature, Irradiance. | Thermal derating and theoretical yield modeling. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Hulajnogi Telemetry** | wksir/kioze/pv/hulajnogi\_outside\_r06/telemetry |
| **Hulajnogi Alarms** | wksir/kioze/pv/hulajnogi\_outside\_r06/alarms |
| **Rotate Telemetry** | wksir/kioze/pv/rotate/telemetry |
| **Agro Small Status** | wksir/kioze/pv/agro\_small/status |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "pv_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "photovoltaic",
    "station_id": "pv_rotate",
    "device_model": "sofar_3.3ktl_g3",
    "connection_type": "hybrid_tracker"
  },
  "fields": {
    "pv_voltage_1_v": 315.4,
    "pv_current_1_a": 4.2,
    "pv_voltage_2_v": null,
    "pv_current_2_a": null,
    "insulation_impedance_mohm": 10.5,
    "grid_voltage_v": 232.1,
    "grid_current_a": 5.6,
    "grid_frequency_hz": 50.02,
    "active_power_kw": 1.3,
    "reactive_power_kvar": 0.1,
    "energy_today_kwh": 4.5,
    "energy_total_kwh": 1250.4,
    "inverter_temperature_c": 42.1,
    "battery_voltage_v": 24.5,
    "battery_charge_current_a": 12.0,
    "battery_soc_percent": 85.0,
    "tracker_azimuth_deg": 145.2,
    "tracker_elevation_deg": 35.5,
    "irradiance_w_m2": 650.0,
    "panel_temperature_c": 48.3
  },
  "timestamp": 1711627199000,
  "status": "Generating"
}
```

This superset schema successfully handles the SOFAR inverter's dual MPPT channel capabilities alongside the mechanical data points of the PV-Rotate station. In instances where the PV-Hulajnogi station (a static, grid-tied array) transmits data, fields such as `tracker_azimuth_deg` and `battery_voltage_v` will simply be transmitted as null, ensuring database consistency while accommodating hardware variations.

### Active Node-RED Implementation (Simulated Fields)

The `pv-hulajnogi` measurement (Solar Charger flow) simulates: `grid_voltage_v`, `grid_current_a`, `grid_frequency_hz`, `active_power_kw`, `reactive_power_kvar`, `energy_today_kwh`, `battery_soc_percent`.

The `pv-hybrid` measurement (PV Panels flow) simulates: `pv_voltage_1_v`, `pv_current_1_a`, `dc_power_w`, `grid_voltage_v`, `grid_frequency_hz`, `active_power_kw`, `inverter_temperature_c`, `irradiance_w_m2`, `energy_today_kwh`.

---

## Category 2: Wind Energy Systems

The wind energy infrastructure at KIOZE includes the Wind-Big-Vertical-Storage and the Solar-Wind Hybrid Station. These systems utilize Vertical Axis Wind Turbines (VAWT) and Horizontal Axis Wind Turbines (HAWT), presenting different specialized telemetry requirements.

### 2a. VAWT (Vertical Axis Wind Turbine)

Performance monitoring of a VAWT necessitates the precise correlation of environmental kinetic energy with mechanical translation and subsequent electrical generation. Critical parameters include meteorological data, rotor angular speed (RPM), tip-speed ratio, and bearing shaft vibration parameters—specifically displacement, velocity, and acceleration—as vital candidates for predictive maintenance algorithms.

### 2b. HAWT (Horizontal Axis Wind Turbine)

The Solar-Wind Hybrid station uses a conventional HAWT topology. Key differences from the VAWT include active blade-pitch control (pitch angle in degrees) and a higher rotor speed range. The HAWT variant is simulated by the "Turbina wiatrowa HAWT" flow and writes to the `wind-hawt-hybrid` measurement.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | VAWT | HAWT |
| :---- | :---- | :---- | :---- |
| **Meteorological** | Wind Speed (m/s), Wind Direction. | ✓ | ✓ |
| **Mechanical Dynamics** | Rotor Speed (RPM), Tip-Speed Ratio. | ✓ | ✓ |
| **Blade Control** | Blade Pitch (°). | — | ✓ |
| **Structural Integrity** | Vibration Displacement, Velocity, Acceleration. | ✓ | — |
| **Electrical Output** | Generator Frequency, DC Voltage, DC Current, Active Power. | ✓ | ✓ |
| **Thermal** | Generator Temperature. | — | ✓ |
| **Energy Storage** | Battery Voltage, Current, SOC. | ✓ | ✓ |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Vertical Storage Telemetry** | wksir/kioze/wind/big\_vertical\_storage/telemetry |
| **Vertical Storage Alarms** | wksir/kioze/wind/big\_vertical\_storage/alarms |
| **Hybrid Station Telemetry (HAWT)** | wksir/kioze/wind/solar\_wind\_hybrid/telemetry |
| **Hybrid Station Cmd** | wksir/kioze/wind/solar\_wind\_hybrid/cmd |

### Canonical Data Model — VAWT (JSON Superset)

```json
{
  "measurement": "wind_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "wind",
    "station_id": "big_vertical_storage",
    "device_model": "vawt_700w",
    "connection_type": "off_grid_storage"
  },
  "fields": {
    "wind_speed_m_s": 6.5,
    "wind_direction_deg": 180.0,
    "rotor_speed_rpm": 120.5,
    "generator_frequency_hz": 22.1,
    "dc_voltage_v": 48.2,
    "dc_current_a": 8.5,
    "active_power_w": 409.7,
    "vibration_acceleration_g": 0.02,
    "vibration_velocity_mm_s": 1.5,
    "vibration_displacement_mm": 0.05,
    "power_coefficient_cp": 0.35,
    "tip_speed_ratio_lambda": 2.1,
    "battery_voltage_v": 51.2,
    "battery_current_a": 7.8,
    "battery_soc_percent": 92.0
  },
  "timestamp": 1711627205000,
  "status": "Normal_Operation"
}
```

### Canonical Data Model — HAWT (JSON Superset)

```json
{
  "measurement": "wind_hawt_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "wind",
    "station_id": "solar_wind_hybrid",
    "device_model": "hawt_hybrid",
    "connection_type": "grid_tied"
  },
  "fields": {
    "wind_speed_m_s": 8.2,
    "rotor_speed_rpm": 1450.0,
    "blade_pitch_deg": 12.5,
    "active_power_w": 2100.0,
    "generator_temperature_c": 68.3,
    "efficiency_percent": 82.5
  },
  "timestamp": 1711627206000,
  "status": "Generating"
}
```

### Active Node-RED Implementation (Simulated Fields)

The `wind-vawt` measurement simulates: `wind_speed_m_s`, `rotor_speed_rpm`, `dc_voltage_v`, `dc_current_a`, `active_power_w`, `vibration_acceleration_g`, `tip_speed_ratio_lambda`, `battery_soc_percent`.

The `wind-hawt-hybrid` measurement simulates: `wind_speed_m_s` (→ `wind_speed`), `power_output_w`, `rotor_speed_rpm`, `blade_pitch_deg`, `generator_temperature_c`, `efficiency_percent`.

---

## Category 3: Biogas Systems

The biogas installations, comprising the Biogaz-KIOZE-small\_plan and Biogaz-KIOZE-Storage units, operate fundamentally differently from the facility's electro-mechanical systems. These systems rely on the delicate biochemical balance of anaerobic digestion, a highly sensitive process consisting of hydrolysis, acidogenesis, acetogenesis, and methanogenesis. Monitoring these biological reactors is critical, as poorly designed or mismanaged digesters can result in toxic gas accumulation, decreased biogas yields, and catastrophic biological system failures.

The telemetry ingestion layer must capture early warning indicators of process instability, such as sudden acidification or methanogen inhibition. Common early warning indicators include the concentrations of methane (CH4), carbon dioxide (CO2), and hydrogen sulfide (H2S), as well as volatile fatty acids (VFAs), total ammonia concentration (TAN), free ammonia concentration (FAN), and overall alkalinity (ALK). While parameters like VFAs and Alkalinity often require offline laboratory analysis, modern IoT sensor networks increasingly capture real-time proxies.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Thermal Dynamics** | Top Temperature, Bottom Temperature. | Ensuring uniform microbiological conditions. |
| **Biochemical State** | pH, Volatile Fatty Acids (VFA), Alkalinity (ALK), Ammonia (TAN/FAN). | Early warning indicators of digester failure. |
| **Gas Composition** | Methane (CH4), Carbon Dioxide (CO2), Hydrogen Sulfide (H2S). | Evaluating fuel quality and toxicity levels. |
| **Physical Dynamics** | Gas Pressure, Gas Flow Rate, Digester Water Level. | Monitoring production volumes and structural limits. |
| **Mechanical Support** | Agitator Speed (RPM), Feedstock Input Mass. | Optimizing substrate mixing and co-digestion rates. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Small Plan Telemetry** | wksir/kioze/biogas/small\_plan/telemetry |
| **Small Plan Status** | wksir/kioze/biogas/small\_plan/status |
| **Storage Telemetry** | wksir/kioze/biogas/storage/telemetry |
| **Storage Alarms** | wksir/kioze/biogas/storage/alarms |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "biogas_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "biogas",
    "station_id": "small_plan",
    "device_model": "anaerobic_digester_v1",
    "sensor_array": "custom_esp8266"
  },
  "fields": {
    "temperature_top_c": 37.5,
    "temperature_bottom_c": 36.8,
    "ph_value": 7.2,
    "methane_ch4_percent": 62.5,
    "carbon_dioxide_co2_percent": 35.0,
    "hydrogen_sulfide_h2s_ppm": 120.0,
    "volatile_fatty_acids_vfa_mg_l": null,
    "alkalinity_alk_mg_l": null,
    "total_ammonia_tan_mg_l": null,
    "gas_pressure_kpa": 12.5,
    "gas_flow_rate_l_min": 2.4,
    "storage_volume_m3": 1.2,
    "water_level_cm": 85.0,
    "agitator_speed_rpm": 15.0
  },
  "timestamp": 1711627210000,
  "status": "Mesophilic_Optimal"
}
```

By unifying chemical concentrations, biological indicators, and physical fluid dynamics into a single schema, the architecture enables advanced cross-correlation within Grafana. Parameters reliant on offline or manual laboratory input are intentionally included as native fields with null defaults to allow future automated sensor integration without altering the core database structure.

---

## Category 4: Heat (Stirling) Systems

The Heat-Stirling-Storage station is a complex testbed exploring external combustion kinematics combined with advanced thermal retention mechanisms. Stirling engines operate on a closed regenerative thermodynamic cycle, relying on the cyclic compression and expansion of a working fluid (such as air, helium, or hydrogen) at different temperature levels to convert thermal energy into mechanical work. When coupled with a Phase Change Material (PCM) or latent heat thermal energy storage (TES) system, the engine can continue to dispatch power long after the primary heat source is removed, vastly improving system flexibility.

The telemetry profile for such a system is highly specialized. It must map the extreme thermal gradients that drive the engine's displacer and power pistons. Telemetry must capture the average hot-side and cold-side temperatures of the engine's heat exchangers, the total mass and pressure of the working gas, and the resultant mechanical output (engine RPM and generated electrical power). The thermal storage component requires monitoring the mass flow rate of the heat transfer fluid and the core temperature of the PCM to monitor the freeze-thaw transition boundaries.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Thermodynamic Gradients** | Hot-Side Temperature, Cold-Side Temperature. | Determining the Carnot efficiency potential of the cycle. |
| **Working Fluid Dynamics** | Working Gas Pressure, Gas Mass, Dead Volume Ratio. | Evaluating the oscillating flow effects and internal losses. |
| **Mechanical/Electrical** | Engine Speed (RPM), Electrical Power Output. | Measuring the final conversion efficiency of the linear alternator. |
| **Thermal Storage (TES)** | PCM Core Temperature, Heat Input/Rejection Rates. | Monitoring the latent heat capacity and freeze-thaw state. |
| **System Flow** | Mass Flow Rate, Coolant Inlet/Outlet Temperatures. | Tracking the transport of thermal energy through the system. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Sterling Storage Telemetry** | wksir/kioze/heat/sterling\_storage/telemetry |
| **Sterling Storage Status** | wksir/kioze/heat/sterling\_storage/status |
| **Sterling Storage Cmd** | wksir/kioze/heat/sterling\_storage/cmd |
| **Sterling Storage Alarms** | wksir/kioze/heat/sterling\_storage/alarms |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "heat_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "heat",
    "station_id": "sterling_storage",
    "device_model": "kinematic_stirling_tes",
    "working_fluid": "helium"
  },
  "fields": {
    "temperature_hot_side_c": 550.0,
    "temperature_cold_side_c": 45.0,
    "working_gas_pressure_kpa": 1500.0,
    "working_gas_mass_kg": 0.15,
    "engine_speed_rpm": 1450.0,
    "electrical_power_output_w": 850.5,
    "mass_flow_rate_kg_s": 0.05,
    "heat_input_rate_w": 3000.0,
    "heat_rejection_rate_w": 2000.0,
    "pcm_core_temperature_c": 320.5,
    "dead_volume_ratio": 0.45,
    "thermal_efficiency_percent": 28.3,
    "coolant_inlet_temperature_c": 35.0,
    "coolant_outlet_temperature_c": 45.0
  },
  "timestamp": 1711627215000,
  "status": "Running_Steady_State"
}
```

This data model provides a comprehensive thermodynamic snapshot. By capturing `temperature_hot_side_c` and `temperature_cold_side_c` concurrently with `electrical_power_output_w`, analytical models in the Node-RED backend can continuously calculate real-time thermal efficiencies.

---

## Category 5: Algae Photobioreactors

The cultivation of microalgae within controlled photobioreactors (PBRs)—such as the Algae-inside-farm-R121 and Algae-outside stations—represents a sophisticated convergence of fluid dynamics, optics, and microbiology. The primary objective of these systems within renewable energy contexts is often carbon dioxide bio-sequestration and rapid biomass generation for biofuels, requiring absolute precision in environmental control.

The telemetry ingestion layer must accommodate a suite of bio-optical and physico-chemical sensors. Essential parameters include the exact temperature of the medium, as microalgae like *Chlorella* have specific temperature requirements (e.g., controlled between 26.8°C and 27.2°C for optimal cell division and photosynthesis). The pH of the medium is regulated automatically by the injection of CO2 gas. Monitoring Dissolved Oxygen (DO) levels alongside dissolved CO2 is mandatory. Optical parameters, notably the light intensity provided by LED panels (PPFD/PAR), must be dynamically regulated based on the actual concentration of biomass tracked via an Optical Density (OD) sensor at 560 nm.

The two operational stations differ in light source:
- **Algae-inside-farm-R121** — indoor, LED-panel illuminated, full process-control instrumentation.
- **Algae-outside** — outdoor, solar-driven; `ambient_light_lux` replaces the LED PPFD metric; the OD sensor is optional.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Physico-Chemical** | pH, Medium Temperature, Salinity. | Fundamental parameters for cell survival and division. |
| **Dissolved Gases** | Dissolved Oxygen (DO), Dissolved CO2. | Monitoring photosynthetic output and preventing DO toxicity. |
| **Bio-Optical** | Light Intensity (PPFD/PAR), Optical Density (OD). | Driving photosynthesis and tracking biomass concentration. |
| **Process Control** | Nutrient Flow Rate, Circulation Pump Speed. | Maintaining interphase contact and preventing culture stagnation. |
| **Environmental Context** | Ambient Temperature, Ambient Light (Lux). | Providing baseline data for outdoor, solar-driven PBR variations. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Inside Farm Telemetry** | wksir/kioze/algae/inside\_farm\_r121/telemetry |
| **Inside Farm Alarms** | wksir/kioze/algae/inside\_farm\_r121/alarms |
| **Outside PBR Telemetry** | wksir/kioze/algae/outside/telemetry |
| **Outside PBR Status** | wksir/kioze/algae/outside/status |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "algae_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "algae",
    "station_id": "inside_farm_r121",
    "device_model": "tubular_pbr_v2",
    "culture_strain": "chlorella_vulgaris"
  },
  "fields": {
    "ph_value": 7.15,
    "temperature_medium_c": 27.0,
    "dissolved_oxygen_do_mg_l": 8.5,
    "dissolved_co2_mg_l": 31.0,
    "co2_injection_valve_state": 1,
    "light_intensity_ppfd_umol_m2_s": 450.0,
    "optical_density_od_560nm": 0.85,
    "salinity_ppt": 5.0,
    "nutrient_flow_rate_ml_min": 12.5,
    "circulation_pump_speed_rpm": 120.0,
    "medium_level_cm": 95.0,
    "ambient_temperature_c": 22.5,
    "ambient_light_lux": 500.0
  },
  "timestamp": 1711627220000,
  "status": "Cultivating"
}
```

The PBR superset anticipates the distinct differences between indoor and outdoor reactors. For the `inside_farm_r121` station, the `light_intensity_ppfd_umol_m2_s` metric maps the controlled LED panel output. Conversely, for the `algae_outside` station, the `ambient_light_lux` and `ambient_temperature_c` fields capture the stochastic nature of environmental exposure.

### Active Node-RED Implementation (Simulated Fields)

Both `algae-farm-1` and `algae-farm-2` measurements simulate: `ph_value`, `temperature_medium_c`, `dissolved_oxygen_do_mg_l`, `optical_density_od_560nm`, `light_intensity_ppfd_umol_m2_s`, `nutrient_flow_rate_ml_min`, `circulation_pump_speed_rpm`.

---

## Category 6: Engine Bench Systems

The Engine\_bench-R121 serves as a highly dynamic test stand for internal combustion and biofuel analysis. Unlike the relatively slow-moving time-series data of a biogas digester, an engine dynamometer produces high-frequency, highly volatile telemetry. The system architecture must capture the complex interactions between mechanical loading, fluid consumption, and exhaust gas emissions to optimize performance, understand volumetric efficiency, and evaluate alternative fuels like ethanol blends or bio-diesel.

An analysis of typical 16 kW eddy current dynamometers (capable of up to 12,000 RPM) reveals strict parameters required for combustion analysis and steady-state engine mapping. Mechanical metrics include precise engine speed (RPM) and torque (Nm), from which total power is derived mathematically. For rigorous emissions tuning, the exhaust gas composition—specifically CO, unburned Hydrocarbons (HC), and Nitrogen Oxides (NOx)—as well as the lambda (air-fuel ratio) must be integrated into the telemetry payload.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Mechanical Performance** | Engine Speed (RPM), Torque (Nm), Measured Power (kW). | Core performance figures used to plot the engine's power curve. |
| **Fuel & Thermodynamics** | Fuel Consumption Rate, Intake Air Temp/Pressure. | Calculating specific fuel consumption and assessing volumetric efficiency. |
| **Thermal Profiling** | Exhaust Temperature, Spark Plug/Coolant Temperature. | Monitoring combustion quality and preventing thermal degradation. |
| **Emissions & Combustion** | Lambda (Air/Fuel Ratio), CO, HC, NOx concentrations. | Optimizing the engine for alternative fuels and minimizing pollutants. |
| **Control Inputs** | Throttle Position, Exhaust Gas Recirculation (EGR) valve state. | Tracking the primary control parameters affecting dynamic system behavior. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Bench Telemetry** | wksir/kioze/engine/bench\_r121/telemetry |
| **Bench Status** | wksir/kioze/engine/bench\_r121/status |
| **Bench Alarms** | wksir/kioze/engine/bench\_r121/alarms |
| **Bench Cmd** | wksir/kioze/engine/bench\_r121/cmd |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "engine_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "engine_bench",
    "station_id": "bench_r121",
    "device_model": "eddy_current_dyno_16kw",
    "fuel_type": "bioethanol_blend"
  },
  "fields": {
    "engine_speed_rpm": 3500.0,
    "torque_nm": 45.2,
    "measured_power_kw": 16.5,
    "fuel_consumption_rate_kg_h": 4.2,
    "specific_fuel_consumption_g_kwh": 254.5,
    "intake_air_temperature_c": 25.4,
    "intake_manifold_pressure_kpa": -45.0,
    "exhaust_temperature_c": 650.0,
    "exhaust_pressure_kpa": 15.2,
    "spark_plug_temperature_c": 210.0,
    "lambda_air_fuel_ratio": 1.02,
    "emissions_co_percent": 0.5,
    "emissions_hc_ppm": 120.0,
    "emissions_nox_ppm": 450.0,
    "throttle_position_percent": 85.0,
    "engine_coolant_temperature_c": 90.0,
    "exhaust_gas_recirculation_percent": 12.5
  },
  "timestamp": 1711627225000,
  "status": "Dynamic_Load_Test"
}
```

The density of this JSON schema provides researchers with the required depth to perform advanced power analysis, steady-state engine mapping, and continuous emissions monitoring. By standardizing the field naming conventions (e.g., `_kpa` for pressure, `_c` for temperature), the subsequent visualization layer in Grafana can utilize unified threshold overrides across the entire dashboard array.

---

## Category 7: Energy Storage Systems

The energy-storage sub-system (`Converter & Storage` station, identifier `turbine_is`) represents the grid-side power conditioning and battery buffer that underpins the hybrid renewable configuration. Unlike the generation-side categories, this sub-system's primary KPIs are State of Charge (SOC), round-trip efficiency, and degradation trajectory over charge/discharge cycles.

The simulation applies a physics-based battery model that accounts for:
- **Temperature dependence** — voltage and current are adjusted using a `tempFactor` coefficient relative to the 25°C baseline.
- **Degradation** — capacity retention is reduced by calendar aging (0.01 %/day), cycle count (0.01 %/cycle), and elevated temperature (0.1 %/°C above 30°C).
- **Diurnal SOC cycle** — charging from solar/wind between 06:00–18:00 (+0.5 %/interval), discharging for peak demand 19:00–23:00 (−1.0 %/interval), slow overnight top-up (+0.1 %/interval).

Four fault scenarios are modelled at 0.1 % probability: cell imbalance, temperature fault, capacity loss, and communication fault.

### Parameter Extraction Summary

| Telemetry Group | Extracted Parameters | Data Source / Justification |
| :---- | :---- | :---- |
| **Electrical** | Battery Voltage (V), Charge/Discharge Current (A), Instantaneous Power (W). | Core energy-balance parameters for inverter control loops. |
| **State Estimation** | State of Charge — SOC (%), Usable Capacity (kWh). | Dispatch planning and degradation-aware load scheduling. |
| **Health & Aging** | Capacity Retention / Degradation Factor, Cycle Count. | Predictive replacement triggers and warranty tracking. |
| **Thermal** | Cell/Pack Temperature (°C). | Thermal management system (TMS) activation and safety interlocks. |
| **Conversion Efficiency** | Round-Trip Efficiency (%). | Evaluating inverter/converter losses across load profiles. |

### Recommended MQTT Topic Structure

| Data Stream | Recommended MQTT Topic |
| :---- | :---- |
| **Storage Telemetry** | wksir/kioze/storage/turbine\_is/telemetry |
| **Storage Status** | wksir/kioze/storage/turbine\_is/status |
| **Storage Alarms** | wksir/kioze/storage/turbine\_is/alarms |
| **Storage Cmd** | wksir/kioze/storage/turbine\_is/cmd |

### Canonical Data Model (JSON Superset)

```json
{
  "measurement": "energy_storage_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "energy_storage",
    "station_id": "turbine_is",
    "device_model": "lifepo4_100kwh_pack",
    "connection_type": "grid_forming_inverter"
  },
  "fields": {
    "battery_voltage_v": 51.8,
    "battery_current_a": 18.4,
    "battery_power_w": 953.1,
    "battery_soc_percent": 72.5,
    "battery_capacity_kwh": 98.7,
    "battery_temperature_c": 27.3,
    "degradation_factor": 0.987,
    "cycle_count": 142.3,
    "efficiency_percent": 91.2,
    "converter_output_voltage_v": null,
    "converter_output_current_a": null,
    "converter_output_power_w": null,
    "grid_frequency_hz": null,
    "fault_type": null
  },
  "timestamp": 1711627230000,
  "status": "Charging"
}
```

### Active Node-RED Implementation (Simulated Fields)

The `energy-storage` measurement (InfluxDB name) simulates: `temperature` (→ `battery_temperature_c`), `state_of_charge` (→ `battery_soc_percent`), `voltage` (→ `battery_voltage_v`), `current` (→ `battery_current_a`), `power` (→ `battery_power_w`), `capacity` (→ `battery_capacity_kwh`), `degradation` (→ `degradation_factor`), `efficiency` (→ `efficiency_percent`).

> **Known issue:** The current `station_id` tag value is `"turbine_is"` — a semantically incorrect leftover from an earlier naming pass. This should be corrected to `"turbine_is_storage"` or `"es_main"` when the real device is onboarded.

---

## API Layer

The Express.js API (`api/src/index.js`) exposes simplified HTTP endpoints that the React frontend and any third-party integration can consume. Internally it issues Flux queries against InfluxDB via the `@influxdata/influxdb-client` library.

### Endpoints

| Method | Path | Description |
| :---- | :---- | :---- |
| `GET` | `/api/health` | Service health check |
| `GET` | `/api/summary/:machine` | Latest telemetry for a named machine (last 2 min by default) |
| `POST` | `/api/query` | Execute an arbitrary Flux query |

### Machine Identifiers (`/api/summary/:machine`)

| Machine Key | InfluxDB Measurement | Category |
| :---- | :---- | :---- |
| `charger` | `pv-hulajnogi` | PV Solar Charger |
| `pv_panels` | `pv-hybrid` | PV Panels |
| `big_turbine` | `wind-vawt` | Wind VAWT |
| `wind_turbine` | `wind-hawt-hybrid` | Wind HAWT |
| `biogas` | `biogas-plant` | Biogas |
| `heat_boiler` | `heat-boiler` | Heat/Stirling |
| `engine_test_bench` | `engine-test-bench` | Engine Bench |
| `storage` | `energy-storage` | Energy Storage |
| `algae_farm_1` | `algae-farm-1` | Algae Farm 1 (indoor) |
| `algae_farm_2` | `algae-farm-2` | Algae Farm 2 (outdoor) |

All queries apply a dual filter: `r._measurement == "<name>"` **and** `r.station_id == "<id>"` to prevent cross-measurement bleed in future multi-tenant configurations.

---

## Physical Device Onboarding Contract

This section defines the minimum contract a real PLC, microcontroller, gateway, or edge computer must satisfy before it is allowed to publish production telemetry into the platform. It is intentionally stricter than the current simulation flows so that physical-device integration does not inherit the MVP shortcuts.

### Device Identity

Every physical publisher must have a stable identity that appears consistently in three places:

| Identity Element | Required Format | Example |
| :---- | :---- | :---- |
| MQTT username | short device or gateway account | `pv_rotate_gateway` |
| MQTT topic station segment | snake_case station identifier | `pv_rotate` |
| JSON `tags.station_id` | same value as topic station segment | `pv_rotate` |

The ingestion flow must reject messages when the topic station and payload `tags.station_id` disagree. This prevents a misconfigured device from writing valid-looking data into the wrong station series.

### Required Telemetry Envelope

Each telemetry message must be valid JSON encoded as UTF-8. The topic identifies the routing context; the payload identifies the measurement, tags, fields, timestamp, and operational status.

```json
{
  "measurement": "pv_telemetry",
  "tags": {
    "site_id": "wksir_kioze",
    "category": "photovoltaic",
    "station_id": "pv_rotate",
    "device_model": "edge_gateway_v1",
    "connection_type": "modbus_rtu"
  },
  "fields": {
    "pv_voltage_1_v": 315.4,
    "pv_current_1_a": 4.2,
    "grid_frequency_hz": 50.02,
    "active_power_kw": 1.3
  },
  "timestamp": 1711627199000,
  "status": "Generating"
}
```

Required top-level keys: `measurement`, `tags`, `fields`, `timestamp`, and `status`.

Required tags: `site_id`, `category`, `station_id`, and `device_model`. Optional tags are allowed only when they describe low-cardinality metadata such as `connection_type`, `fuel_type`, `culture_strain`, or `working_fluid`. Sensor values, error text, serial numbers, request IDs, and firmware build hashes must not be written as tags.

### Field Naming and Units

Telemetry field names must follow the pattern `<signal>_<unit>` where practical, for example `battery_voltage_v`, `temperature_medium_c`, `wind_speed_m_s`, and `emissions_nox_ppm`. Boolean or enumerated process states may use explicit names such as `co2_injection_valve_state` or `fault_type`.

Rules:

| Rule | Rationale |
| :---- | :---- |
| Use snake_case for all keys | Keeps Flux queries, dashboard variables, and schema validation predictable. |
| Put units in field names | Prevents silent mixing of volts, kilovolts, Celsius, Kelvin, percent, and fractions. |
| Send unavailable optional sensors as `null` | Allows the CDM transformer to remove sparse fields before InfluxDB writes. |
| Send missing required sensors as an alarm, not as `null` | A broken core sensor is an operational event, not normal sparsity. |
| Keep numeric values numeric | Do not send numbers as strings; `"42.1"` must be rejected for numeric fields. |

### Validation and Rejection Path

The dedicated ingestion flow should validate messages in the following order:

1. Decode payload as JSON.
2. Parse the MQTT topic into `root`, `tenant`, `category`, `station`, and `stream`.
3. Verify topic pattern equals `wksir/kioze/<category>/<station>/telemetry`.
4. Verify `tags.category` and `tags.station_id` match the parsed topic.
5. Verify `measurement` is one of the approved CDM measurements.
6. Verify required tags and required fields for the category are present.
7. Verify field types and value ranges.
8. Drop all `null` fields before writing to InfluxDB.
9. Route rejected messages to `wksir/kioze/<category>/<station>/alarms`.

Rejected messages should not be written to the telemetry measurement. Instead, Node-RED should publish a compact alarm payload and optionally write it to a dedicated `ingestion_errors` measurement.

```json
{
  "severity": "error",
  "error_code": "SCHEMA_VALIDATION_FAILED",
  "category": "photovoltaic",
  "station_id": "pv_rotate",
  "source_topic": "wksir/kioze/pv/pv_rotate/telemetry",
  "reason": "field grid_frequency_hz must be a number between 45 and 55",
  "timestamp": 1711627199000
}
```

### MQTT Delivery Semantics

| Stream | QoS | Retain | Notes |
| :---- | :---- | :---- | :---- |
| `telemetry` | 0 or 1 | false | Use QoS 0 for high-frequency streams and QoS 1 for lower-rate critical measurements. |
| `status` | 1 | true | Retained status gives dashboards the latest known device state after reconnect. |
| `alarms` | 1 | true for active alarms | Clear retained alarms by publishing an empty retained message after acknowledgement. |
| `cmd` | 1 | false | Commands must include a unique command ID and timeout. |

Telemetry messages should be small and periodic. Large diagnostics, firmware metadata, calibration files, and binary payloads should not be embedded in MQTT telemetry. If needed, publish a reference ID and store the large object elsewhere.

### Time Handling

Physical devices should publish timestamps in Unix epoch milliseconds. Node-RED may replace timestamps only when the device does not have a valid clock. The ingestion flow should flag device timestamps that are more than five minutes in the future or more than one day in the past, because those values can distort Grafana panels and retention policies.

### Onboarding Checklist

| Step | Acceptance Criteria |
| :---- | :---- |
| Create MQTT account | Device account exists in `passwd`; anonymous access remains disabled. |
| Add ACL entry | Device can write only its own `telemetry`, `status`, and `alarms` topics and can read only its own `cmd` topic. |
| Register station mapping | Topic category/station maps to one approved measurement and one API machine key where applicable. |
| Validate payload sample | Sample JSON passes schema validation and range checks. |
| Run shadow ingest | Device publishes to a test topic or staging bucket for at least 24 hours. |
| Compare dashboards | Grafana and `/api/summary/:machine` display expected values without Flux errors. |
| Promote to production | Device is moved to canonical topic and monitored for ingestion errors. |

---

## Implementation Notes & Known Gaps

The following gaps exist between this specification and the current MVP simulation implementation. They must be resolved before onboarding physical devices.

### Gap 1 — MQTT Topic Mismatch (Critical)

| Aspect | Specification (this document) | Current Implementation |
| :---- | :---- | :---- |
| Topic prefix | `wksir/kioze/<category>/<station>/` | `devices/<category>/<device_id>/` |
| Telemetry suffix | `/telemetry` | `/telemetry` |
| ACL data suffix | `/telemetry` | `/data` |

A physical device publishing to `wksir/kioze/pv/rotate/telemetry` hits **no** subscriber in the current Node-RED flows. Data is silently dropped. **Resolution:** Update all Node-RED MQTT-in subscription patterns and ACL entries to use `wksir/kioze/+/+/telemetry`, or update the spec to adopt the `devices/` prefix consistently.

### Gap 2 — Loopback-Only Simulation Architecture

Each Node-RED tab is self-contained: it generates → publishes to MQTT → subscribes to itself. There is no dedicated ingestion-only flow listening for external publishers. External devices would be received only if they use the `devices/` prefix, which contradicts the spec. **Resolution:** Add a dedicated ingestion flow subscribed to the canonical `wksir/kioze/+/+/telemetry` pattern that only contains MQTT-in → validate → transform → InfluxDB-write nodes, with no simulation logic.

### Gap 3 — No Input Validation or Schema Enforcement

The CDM transformer trusts whatever JSON arrives. A physical device sending malformed payloads, out-of-range values, or extra fields passes straight to InfluxDB without rejection or alerting. **Resolution:** Add a JSON schema validation step (e.g. using the `node-red-contrib-json-schema` node or a custom function) that routes invalid payloads to an alarm topic and logs a structured error.

### Gap 4 — Measurement Naming (Minor)

Current measurement names use hyphens (`pv-hybrid`, `biogas-plant`). The CDM schema examples in this document use underscores (`pv_telemetry`, `biogas_telemetry`). Hyphens require backtick-quoting in every Flux query and are visually inconsistent. **Resolution:** Rename measurements to use underscores when next re-provisioning InfluxDB (requires re-creating the bucket or using a migration script).

### Gap 5 — Energy Storage `station_id` Tag

The current `station_id` tag for energy storage is `"turbine_is"` (a naming artefact). It should be corrected to a semantically accurate value (e.g., `"es_main"` or `"bess_turbine_is"`) to align with the MQTT station hierarchy.

### Implementation Readiness Summary

| Area | Status |
| :---- | :---- |
| CDM null-deletion transformer | ✅ Operational across all 10 flows |
| Tag / field separation | ✅ Correct in all flows |
| Unified `renewable_energy` bucket | ✅ Confirmed |
| Grafana dashboards (5 panels) | ✅ Remapped to CDM fields |
| API dual-filter Flux queries | ✅ `_measurement` + `station_id` |
| MQTT topic alignment to spec | ❌ Gap 1 — `devices/` vs `wksir/kioze/` |
| Dedicated external ingestion flow | ❌ Gap 2 — loopback only |
| Input validation / schema guard | ❌ Gap 3 — missing |
| Measurement name convention | ⚠️ Gap 4 — hyphens, not underscores |
| Energy storage `station_id` | ⚠️ Gap 5 — semantically incorrect value |
