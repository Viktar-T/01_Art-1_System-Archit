# Revision plan — round 1

Single source of truth for what we'll change in response to round 1. Fill this **before** editing `article.qmd`. Update as work progresses.

**Status:** 1 of N review reports in (Reviewer 1). No formal decision yet — editorial office awaiting remaining reviewers (see `comms/editorial-office/2026-06-16-leroy-liu_round-01-review-report-and-reference-issues.md`). We may begin Reviewer 1 + reference fixes now; hold the rebuttal letter until the decision and any further reports arrive.
**Owner of manuscript edits:** Kelvyn George (K.G.M.K.). **Coordinator / rebuttal author:** V.T.

## Master table

> One row per point. IDs are stable; they appear in commit messages and in the rebuttal letter. **R1.x** = Reviewer 1. **EO.x** = editorial-office technical check (from Leroy Liu's e-mail).

| ID | Source | Summary | Disposition | Section(s) | Files to edit | Effort | Owner | Status |
|----|--------|---------|-------------|------------|---------------|--------|-------|--------|
| R1.1 | R1 | Add "open-source" to keywords | Accept | Keywords | `article.qmd` | S | K.G.M.K. | Pending |
| R1.2 | R1 | Expand abbreviations at first use (SCADA, JSON, and any others) | Accept | Throughout | `article.qmd` | S | K.G.M.K. | Pending |
| R1.3 | R1 | Strengthen intro with recent open-source / Node-RED / Grafana energy refs | Accept | §1 Introduction | `article.qmd`, `bibliography.bib` | M | K.G.M.K. | Pending |
| R1.4 | R1 | State MQTT is the de-facto standard protocol for IoT ecosystems | Accept | § (MQTT/protocol) | `article.qmd` | S | K.G.M.K. | Pending |
| R1.5 | R1 | Four-layer architecture (Fig. 1) endorsed — add citation acknowledging prior use | No action / minor | § (architecture) | `article.qmd`, `bibliography.bib` | S | K.G.M.K. | Pending |
| R1.6 | R1 | Add block diagram / scheme of data communication flows & networks | Accept | § (architecture, near Fig. 2) | `article.qmd`, new figure | M | K.G.M.K. | Pending |
| R1.7 | R1 | Fix broken reference at line 125 | Accept | Refs / line 125 | `article.qmd`, `bibliography.bib` | S | K.G.M.K. | Pending |
| R1.8 | R1 | Rename §5.1 — "experimental setup" misleading for a simulation framework | Accept | §5.1 | `article.qmd` | S | K.G.M.K. | Pending |
| R1.9 | R1 | Add compute environment (CPU, RAM, OS) | Accept | §5.1 | `article.qmd` | S | K.G.M.K. | Pending |
| R1.10 | R1 | Add Node-RED flow screenshot (interconnected nodes) | Accept | § (implementation) | `article.qmd`, new figure | M | K.G.M.K. | Pending |
| R1.11 | R1 | Add Grafana dashboard images — **acceptance-critical** | Accept | § (application layer) | `article.qmd`, new figure(s) | M | K.G.M.K. | Pending |
| R1.12 | R1 | Note browser-based edition/configuration benefit of Node-RED + InfluxDB + Grafana | Accept | § (stack rationale) | `article.qmd` | S | K.G.M.K. | Pending |
| R1.13 | R1 | Merge limitations in §6.2 and §7.2 into a single text | Accept | §6.2, §7.2 | `article.qmd` | S | K.G.M.K. | Pending |
| R1.14 | R1 | Provide more results of the conducted simulations | Accept | § (results) | `article.qmd`, figures/tables | L | K.G.M.K. | Pending |
| EO.1 | Editorial office | Ref 5 — author name incorrect | Accept | References | `bibliography.bib` | S | K.G.M.K. | Pending |
| EO.2 | Editorial office | Ref 11 — DOI incorrect | Accept | References | `bibliography.bib` | S | K.G.M.K. | Pending |
| EO.3 | Editorial office | Ref 12 — conference name incorrect | Accept | References | `bibliography.bib` | S | K.G.M.K. | Pending |
| EO.4 | Editorial office | Ref 15 — conference name incorrect | Accept | References | `bibliography.bib` | S | K.G.M.K. | Pending |
| EO.* | Editorial office | Re-verify **all** references (office asked us to check every entry, not just the examples) | Accept | References | `bibliography.bib` | M | K.G.M.K. | Pending |

## Themes (efficient editing passes)

- **Theme A — Prove the implementation visually (acceptance-critical):** R1.10 (Node-RED flow screenshot), R1.11 (Grafana dashboards), R1.6 (data-flow / network block diagram). These directly answer the reviewer's "prove the successful implementation" demand.
- **Theme B — More results:** R1.14. Expand the reported simulation results (additional plots / tables / scenarios). Highest effort; plan early.
- **Theme C — Framing & clarity:** R1.8 (rename §5.1), R1.13 (merge limitations), R1.2 (abbreviations), R1.1 (keyword), R1.4 (MQTT note), R1.12 (browser-based benefit).
- **Theme D — References:** R1.7 (line-125 ref), R1.3 (add 2 suggested refs + others), EO.1–EO.4 and a full reference re-audit. Run `bib-auditor` after edits.
- **Theme E — Positioning:** R1.3 (recent open-source/energy literature), R1.5 (acknowledge four-layer architecture prior art).

## Push-backs (the risky moves)

None planned. Reviewer 1's comments are constructive and all are accepted in full or in part. If a later reviewer conflicts, document the defence here before writing it into the rebuttal.

## Out-of-scope requests

None from Reviewer 1. "More results" (R1.14) is in scope — expand existing simulation outputs rather than running new field validation.

## Suggested references (R1.3) — verify before citing

- *Implementation and Experimental Application of Industrial IoT Architecture Using Automation and IoT Hardware/Software.* Sensors 2024 — https://doi.org/10.3390/s24248074
- *Design and Implementation of Node-Red Based Open-Source SCADA Architecture for a Hybrid Power System.* Energies 2023 — https://doi.org/10.3390/en16052092

## Schedule (provisional — no MDPI deadline issued yet)

- Reference audit (Theme D, EO.1–EO.4 + full check): [FILL]
- Editing block 1 (Theme A — visuals): [FILL]
- Editing block 2 (Theme B — more results): [FILL]
- Editing block 3 (Theme C/E — framing & positioning): [FILL]
- Re-render + `bib-auditor`: [FILL]
- Internal red-team pass (`reviewer-mdpi-full`): [FILL]
- Hold rebuttal + submission until the formal decision and any further reviewer reports arrive.
