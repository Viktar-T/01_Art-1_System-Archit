# Cover letter to the Editor-in-Chief, *Energies*

> Draft. Replace every `[FILL — ...]` before submission. Keep to ~ 300–400 words.

---

28 May 2026

Editor-in-Chief
*Energies*, MDPI
St. Alban-Anlage 66, 4052 Basel, Switzerland

**Re: Submission of manuscript "Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems" to *Energies*, Section A1 — Smart Grids and Microgrids.**

Dear Editor,

We are pleased to submit the enclosed manuscript for consideration as an **original research article** in *Energies*, targeted at **Section A1 — Smart Grids and Microgrids**.

The paper presents an end-to-end edge-to-cloud telemetry architecture for a multi-vector renewable energy "learning factory" — the KIOZE Edu-Bad facility. Specifically, the work contributes:

1. A reference architecture combining the **MING stack** (Mosquitto, InfluxDB, Node-RED, Grafana) with a React-based operator dashboard, designed to replace legacy SCADA-style data plumbing in research and educational microgrids.
2. A **canonical data model** that normalises heterogeneous sensor and converter streams (PV, wind, electrolyser, battery, thermal) at the edge, enabling cross-vector analytics and downstream digital-twin / AI use.
3. A **reproducibility-oriented design**: every architectural claim is traceable to a published specification artefact, and the entire telemetry stack is built from open-source components.

The work fits Section A1's explicit scope of "Multi-Energy Microgrids," "ICT Applications," and "Big Data, Cloud Computing, IoT Applications for Smart Grids." It addresses the well-documented gap in scalable, vendor-neutral data architectures for the next generation of multi-vector smart grids.

Most prior open-source telemetry pipelines for renewable-energy systems address a narrow vector scope — a single energy cyber-physical system (Saad et al., 2020) or PV plus battery storage (Silva et al., 2022) — and the few framework-level proposals for energy IoT data management (Dhungana et al., 2025) stop short of a reproducible end-to-end implementation. This work contributes the first MING+React reference architecture spanning a fully multi-vector microgrid (PV, wind, electrolyser, battery, thermal) and introduces an edge-side canonical data model that normalises heterogeneous device streams before storage rather than at query time.

We believe this contribution will be of interest to the *Energies* readership working on smart-grid ICT, multi-energy system integration, and educational/research microgrid platforms.

**Required statements.**

- We confirm that neither the manuscript nor any parts of its content are currently under consideration for publication with or published in another journal.
- All authors have approved the manuscript and agree with its submission to *Energies*.

The corresponding author for this submission is Viktar Taustyka (on behalf of all authors)
viktar.taustyka@zut.edu.pl, 0000-0002-0567-267X.

We look forward to your editorial decision.

Sincerely,

Viktar Taustyka
On behalf of all authors
