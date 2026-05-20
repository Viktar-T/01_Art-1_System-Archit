# Manuscript Forensic Audit: Discrepancy Resolution Log

This log documents the resolutions implemented in `ihrke-template/article.qmd` to resolve the citation, architectural, and technical discrepancies cataloged in `Logs/Audit_Discrepancies.md`.

---

## 1. Citation Reconciliations (Evidentiary Discipline)

### 1.1. The "Strict Corridor Algorithm" Attribution
*   **Resolution:** Rephrased the prose in Section 5.1 to present the "Strict Corridor Algorithm" explicitly as a custom simulation model developed in this work to validate the pipeline. Citations were adjusted so that `@costa2022focuser` is cited generally for fog/sensor-ranking filtering paradigms, and `@velasquez2021monitoring` in Section 6.2 is cited for standard sensor noise monitoring in renewable energy environments.
*   **Prose Changes:**
    *   *Section 5.1:* Changed from "...strict corridor algorithm to mimic physical inertia and sensor noise, validating the edge-level filtering strategies evaluated in fog and sensor-ranking systems [@costa2022focuser]" to "To validate the pipeline under realistic conditions, we developed a custom simulation model utilizing a strict corridor algorithm to mimic physical inertia and sensor noise. This custom model provides a baseline for evaluating edge-level filtering strategies similar to the fog-based sensor-ranking paradigms discussed generally in [@costa2022focuser]."
    *   *Section 6.2:* Changed from "...may require dynamic adjustment to account for real-world sensor noise [@velasquez2021monitoring]" to "...was designed to preserve physical inertia in our simulation; however, transitioning to physical assets may require dynamic threshold adjustments to handle the stochastic sensor noise characteristics observed in real-world renewable energy monitoring architectures [@velasquez2021monitoring]."

### 1.2. The "42.5 ms Latency Baseline" Comparison
*   **Resolution:** Qualified the comparison against `@caiza2023digitaltwin` in Section 5.3. Clarified that the >100 ms latency in Caiza's study is driven by immersive 3D/AR synchronization rendering, whereas our 42.5 ms benchmark measures a lightweight, local API loopback database query.
*   **Prose Changes:**
    *   *Section 5.3:* Changed from "...representing a significant latency reduction compared to similar industrial virtualized environments that report responses over 100 ms [@caiza2023digitaltwin]" to "While similar virtualized digital twin environments report latencies exceeding 100 ms [@caiza2023digitaltwin] due to the heavy synchronization overhead of immersive 3D and Augmented Reality (AR) front-ends, our 42.5 ms benchmark represents a lightweight, local API loopback database query focusing strictly on data persistence and retrieval."

### 1.3. The "Universal Translator & CDM" Citations
*   **Resolution:** Clarified in Section 4.1 and Section 4.2 that the CDM and "Universal Translator" JSON schema are novel designs introduced in this paper, decoupling them from being direct features of `@massaad2023industry` (general protocol comparison) and `@magadan2022lowcost` (low-cost motor vibration gateway).
*   **Prose Changes:**
    *   *Section 4.1:* Changed from "...thereby synchronizing the streams [@magadan2022lowcost; @massaad2023industry]" to "...thereby synchronizing the streams. While our specific CDM structure is a novel contribution of this work, the conceptual benefits of protocol decoupling and low-cost gateway standardization are grounded in the M2M and IIoT monitoring platforms evaluated in [@massaad2023industry] and [@magadan2022lowcost]."
    *   *Section 4.2:* Changed from "...implementing a protocol-independent data contract akin to low-cost IIoT monitoring platforms [@magadan2022lowcost]" to "...This implementation achieves a protocol-independent data contract, drawing architectural inspiration from the simplified message formats used in low-cost IIoT monitoring platforms [@magadan2022lowcost]."

### 1.4. The Sustainability Mapping Study Misalignment
*   **Resolution:** Rephrased the citation in Section 1 to align `@gutierrez2023toward` with its actual scope of compiling sustainability and design integration criteria for CPS architectures, while framing database telemetry pollution as a specific data-quality challenge addressed in this work.
*   **Prose Changes:**
    *   *Section 1:* Changed from "...highlighting the design gaps in legacy CPS architectures identified in systematic mapping studies [@gutierrez2023toward]" to "While systematic mapping studies have identified broad sustainability and architectural integration challenges in legacy Cyber-Physical Systems (CPS) frameworks [@gutierrez2023toward], our work specifically addresses the vulnerability of the persistence layer to time-series data corruption."

---

## 2. Structural & Architectural Reconciliation

### 2.1. The "Decide Phase" vs. "Payload Schema" Contradiction
*   **Resolution:** Rephrased Section 3.2.3 to make it clear that the separation of tags and fields is performed dynamically by the middleware (Node-RED) during the ingestion process, rather than being an inherent nested structure within the raw JSON schema payload.
*   **Prose Changes:**
    *   *Section 3.2.3:* Changed from "By separating tags from fields, the middleware guarantees that the schema remains consistent across all 12 measurements." to "By separating root-level metadata keys into InfluxDB tags and raw telemetry parameters into fields, the middleware dynamically ensures schema consistency across all 12 measurements prior to database write."

---

## 3. Database Performance Revisions

### 3.1. InfluxDB Index Cardinality Risk
*   **Resolution:** Appended a new paragraph in Section 6.2 (Limitations and Open Challenges) discussing the potential risk of an index cardinality explosion when scaling the MING stack to hundreds of devices if dynamic metadata attributes are mapped to tags, and proposed mitigation strategies (such as tag whitelisting, static site hierarchies, or indexing in relational databases).
*   **Prose Changes:**
    *   *Section 6.2 (New Paragraph):* "Furthermore, scaling the MING stack to support hundreds of physical devices introduces a significant risk of an index cardinality explosion in InfluxDB. Because the middleware dynamically maps root-level metadata keys (such as `device_id`) to InfluxDB tags—which are indexed in-memory using an inverted index structure—an unbounded growth in the number of unique tags would degrade query performance. To mitigate this risk, future deployments must enforce strict tag whitelisting, limit dynamic tag generation, or utilize relational databases to manage high-cardinality metadata separately."

---

## 4. Compilation Status
*   **Status:** **SUCCESSFUL**
*   **Command Run:** `quarto render article.qmd` in `ihrke-template/`
*   **Compiler Output:** PDF compiled successfully with no compilation errors. All cross-references and bibliography linkages resolved cleanly.
