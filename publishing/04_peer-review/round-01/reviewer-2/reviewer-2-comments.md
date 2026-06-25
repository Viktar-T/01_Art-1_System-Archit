# Reviewer 2 — comments (verbatim)

> Transcribed verbatim from the MDPI review report form. Don't paraphrase or edit this block.

**Received:** 2026-06-09 (date of this review)
**Reviewer identity:** anonymous

## Review report form

**Quality of English Language:** The English could be improved to more clearly express the research.

| Question | Yes | Can be improved | Must be improved | Not applicable |
|---|---|---|---|---|
| Does the introduction provide sufficient background and include all relevant references? | | x | | |
| Is the research design appropriate? | | x | | |
| Are the methods adequately described? | | x | | |
| Are the results clearly presented? | | x | | |
| Are the conclusions supported by the results? | | x | | |
| Are all figures and tables clear and well-presented? | | x | | |

---

The novelty of the proposed MING+React telemetry pipeline should be clarified more explicitly against existing open-source SCADA, MING, and IIoT monitoring architectures.

The validation is mainly based on a local simulation environment, so the authors should add experiments with physical devices or real multi-vector energy system data.

The claimed 100% packet integrity and 100% null-pruning accuracy need stronger statistical support and should be tested under larger-scale and longer-duration scenarios.

Figure 3 appears inconsistent because the plot label refers to engine speed, while the caption describes normalized active power, so this should be corrected.

The limitations regarding loopback-only testing, physical network latency, packet loss, and scalability should be more directly reflected in the conclusion.

---

## Internal triage

Points numbered **R2.1 … R2.5** so they cross-reference cleanly in the rebuttal letter and commit messages.

| Point | One-line summary | Disposition | Effort |
|---|---|---|---|
| R2.1 | Clarify novelty of MING+React pipeline explicitly vs existing open-source SCADA / MING / IIoT monitoring architectures | Accept | M |
| R2.2 | Add experiments with physical devices or real multi-vector energy data (validation is local-simulation only) | Partial / Push-back — out of scope for an architecture paper; reframe scope + state as future work (overlaps R1.14) | L |
| R2.3 | Provide stronger statistical support for 100% packet integrity / 100% null-pruning, with larger-scale and longer-duration tests | Partial — add longer/larger runs and statistics where feasible; temper absolute claims | M |
| R2.4 | Fix Figure 3 inconsistency (plot label "engine speed" vs caption "normalized active power") | Accept | S |
| R2.5 | Reflect limitations (loopback-only testing, physical network latency, packet loss, scalability) directly in the conclusion | Accept (overlaps R1.13 limitations merge) | S |
