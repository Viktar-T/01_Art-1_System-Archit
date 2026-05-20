# Manuscript Forensic Audit: Active Discrepancies

This document tracks verified citation misalignments, architectural contradictions, and technical risks in the manuscript `ihrke-template/article.qmd`.

---

## 1. Citation Misalignments & "Stretching" Discrepancies

These are instances where the manuscript prose attributes specific project characteristics, metrics, or algorithms to cited academic literature that does not support them.

### 1.1. The "Strict Corridor Algorithm" Attribution
*   **Location:** Section 5.1 (line 200) and Section 6.2 (line 239)
*   **Manuscript Claims:** 
    *   *Claim 1:* The simulation produces data following a *"strict corridor algorithm to mimic physical inertia and sensor noise, validating the edge-level filtering strategies evaluated in fog and sensor-ranking systems [@costa2022focuser]"*.
    *   *Claim 2:* The strict ±2% corridor *"may require dynamic adjustment to account for real-world sensor noise [@velasquez2021monitoring]"*.
*   **Source Literature Reality:** 
    *   `costa2022focuser` (FOCUSeR) describes an online contextual-ranking method for active sensors in fog to reduce transmission bandwidth.
    *   `velasquez2021monitoring` evaluates a monitoring architecture for renewable energy systems using standard FIWARE Orion Context Broker components.
    *   **Verification:** Neither paper describes, names, or validates a "Strict Corridor Algorithm". This corridor-based random-walk algorithm is a proprietary simulation element designed specifically for this project.

### 1.2. The "42.5 ms Latency Baseline" Comparison
*   **Location:** Section 5.3 (line 214)
*   **Manuscript Claim:** Benchmarks an average API response latency of 42.5 ms and claims this is a *"significant latency reduction compared to similar industrial virtualized environments that report responses over 100 ms [@caiza2023digitaltwin]"*.
*   **Source Literature Reality:** 
    *   `caiza2023digitaltwin` evaluates an ISO 23247-compliant digital twin framework integrating Augmented Reality (AR) front-end rendering.
    *   **Verification:** The comparison is unequal. The >100 ms latency in Caiza's study is driven by immersive 3D/AR synchronization and rendering pipelines, whereas the project's 42.5 ms benchmark measures a lightweight, local API loopback backend database query.

### 1.3. The "Universal Translator & CDM" Citations
*   **Location:** Section 4.1 (line 125) and Section 4.2 (line 148)
*   **Manuscript Claims:** 
    *   *Claim 1:* Mapping every sensor to a key-value contract eliminates custom ingestion logic, citing `@magadan2022lowcost` and `@massaad2023industry`.
    *   *Claim 2:* The `Object.entries` null-filtering loop implements a *"protocol-independent data contract akin to low-cost IIoT monitoring platforms [@magadan2022lowcost]"*.
*   **Source Literature Reality:** 
    *   `massaad2023industry` (Cavalcanti et al.) evaluates standard M2M protocols (MQTT vs. OPC UA PubSub) on the shop floor.
    *   `magadan2022lowcost` (Magadán et al.) describes a low-cost, Wi-Fi-based gateway designed explicitly for capturing and transmitting electric motor vibration telemetry.
    *   **Verification:** Neither paper references or outlines a generalized "Canonical Data Model (CDM)" or an object-level "Universal Translator" JSON schema.

### 1.4. The Sustainability Mapping Study Misalignment
*   **Location:** Section 1 (line 48)
*   **Manuscript Claim:** Argues that legacy database systems are vulnerable to "Bad Data" corruption, *"highlighting the design gaps in legacy CPS architectures identified in systematic mapping studies [@gutierrez2023toward]"*.
*   **Source Literature Reality:** 
    *   `gutierrez2023toward` is a systematic mapping study compiling broad conceptual guidelines for integrating environmental, economic, and social sustainability criteria into CPS design.
    *   **Verification:** The paper does not address database telemetry pollution, data cleansing layers, or time-series data purity at the database layer.

---

## 2. Internal Architectural Contradictions

These are logical inconsistencies in how the telemetry pipeline's operations are described across different sections.

### 2.1. The "Decide Phase" vs. "Payload Schema" Contradiction
*   **Location:** Section 3.2.3 (Decide Phase, line 100) vs. Section 4.4 (Payload Analysis, line 194)
*   **Contradiction:** 
    *   *Section 3.2.3:* States that *"By separating tags from fields, the middleware guarantees that the schema remains consistent across all 12 measurements."*
    *   *Section 4.4:* Explains that the raw JSON payloads are flat and *do not* contain tags or fields in their structure (*"These example payloads do not nest metadata keys under a parent tags object. Instead, metadata fields... are published at the root level... The Node-RED ingestion gateway dynamically maps these root-level keys into InfluxDB tags"*).
    *   **Verification:** The description in Section 3.2.3 is ambiguous. It implies that tag-versus-field separation is a property of the data model schema itself, whereas it is actually Node-RED that parses the flat JSON payload and maps root-level metadata keys into InfluxDB tags prior to formatting the Line Protocol write.

---

## 3. Database Performance / Cardinality Risks

### 3.1. InfluxDB Index Cardinality Risk
*   **Location:** Section 6.1 (Scalability, line 233) vs. Section 6.2 (Limitations, line 237)
*   **Technical Risk:** 
    *   Section 6.1 claims that query times will remain stable under horizontal scalability because metadata attributes (like `device_id` and `location`) are stored as InfluxDB tags rather than fields.
    *   Section 6.2 discusses horizontal scaling to "hundreds" of distinct publishers.
    *   **Verification:** If the whitelist parsing loop dynamically maps unique, high-velocity metadata keys to tags across hundreds of virtual/physical devices, the system faces an InfluxDB **index cardinality explosion**. InfluxDB indexes tag values in-memory using an inverted index structure. High-cardinality values degrade query performance significantly, a major engineering risk that is currently unmentioned in the manuscript's Discussion.

---

## 4. Syntax & Format Verification (Resolved / Clean)

### 4.1. MQTT Topic Taxonomy Syntax
*   **Location:** Section 3.3.1 (line 112)
*   **Status: Resolved.** 
    *   The topic definition is written as: `` `wksir/kioze/{category}/{device_id}/{stream}` ``. 
    *   **Verification:** The variable uses the correct closing curly bracket `}`, and there are no mismatched parentheses `)` in the current codebase layout on disk.
