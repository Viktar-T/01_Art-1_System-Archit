# Copyright permission audit

MDPI requires authors to obtain permission to reproduce any published material (figures, schemes, tables, or extracts of text) that does not fall into the public domain or for which the authors do not hold copyright. Reference: https://www.mdpi.com/authors/rights

## Conclusion

**No copyright permission is required for this manuscript.** Every figure, table, listing, dataset, and significant text passage is original work by the authors. Standard scholarly citations (Author, Year) of prior work do not trigger MDPI's permission requirement.

---

## Audit (one row per piece of content)

| ID | Item | Source | Classification | Permission needed? |
|----|------|--------|---------------|---------------------|
| F1 | `@fig-layers` — *Structural mapping of the MING+React stack onto the 4-Layer CPS Model* (`pics/Figure_1_Layers.pdf`, also `pics/figure_1.tex`) | Authors' own TikZ/PDF diagram of THEIR architecture. The 4-Layer CPS model is a concept cited via `@hensler2023onpremises` and `@jiang2018improved`; the diagram itself is the authors' depiction of their stack laid onto that conceptual framework. | Original work | **No** |
| F2 | `@fig-ooda` — *Functional topology of the telemetry pipeline tracing the OODA Loop* (`pics/Figure_2_OODA.pdf`, also `pics/figure_2.tex`) | Authors' own TikZ/PDF diagram. The OODA loop (Boyd, 1976) is a generic conceptual framework — not subject to copyright as an idea; no figure of Boyd's is reproduced. The figure is the authors' depiction of THEIR pipeline mapped onto the OODA stages. | Original work (framework reuse only) | **No** |
| F3 | `@fig-corridor` — *Strict-corridor algorithm vs unfiltered noise* (`pics/Figure_3_Corridor_vs_Noise.pdf`) | Plot generated from the authors' own simulation data via the authors' own `capture_realtime.ps1` script against the InfluxDB instance they operate. | Original work + original data | **No** |
| GA | Graphical abstract (`publishing/02_pre-submission/graphical-abstract.png`, source `.svg`) | Original SVG drawn by/for the authors. No vendor logos, no third-party icons. | Original work | **No** |
| T1 | `@tbl-vectors` — *Listing of the 12 energy vectors mapped to the CDM* | Derived from the authors' own KIOZE platform specification (`docs/pl-Edu-Bad-specification/IoT_Data_Arch-JSON-MQTT.md`), which the authors wrote. | Original work | **No** |
| T2 | `@tbl-metrics` — *Summary of MING+React pipeline functional verification metrics* | Metrics computed from the authors' own simulation runs. | Original work + original data | **No** |
| L1 | `@lst-corridor-code` — Node-RED JavaScript implementation of the Strict-Corridor Algorithm | Authors' own code. Same code archived on Zenodo (DOI 10.5281/zenodo.20415136) and on GitHub (`Viktar-T/plat-edu-bad-data-mvp`). | Original work | **No** |
| J1–J5 | JSON payload schema examples (Engine bench, Algae PBR, PV, Wind, Storage, etc., embedded as fenced code blocks) | Reproduced from the KIOZE specification document authored by V.T. — i.e., the authors' own prior unpublished work, not a third-party publication. | Original work | **No** |
| Citations | All `@key` references in the body (Hensler, Jiang, Kychkin, Saad, Silva, Dani, Dhungana, Balogh, Gutierrez, etc.) | Standard academic citations — text references with author-year/numeric pointers, not reproductions of those authors' figures, tables, or extended text. | Citation only | **No** |
| Concept terms | "Impedance Mismatch", "Canonical Data Model", "Null-Pruning", "MING stack" | Authors' own terminology (where novel) or generic technical vocabulary. | Original / generic | **No** |
| Framework names | OODA loop, 4-Layer CPS Architecture, Industry 4.0 / 5.0, MQTT, OPC UA | Generic conceptual frameworks / open protocols / industry-standard nomenclature. Not copyrightable as concepts; no diagrams from those frameworks are reproduced. | Generic | **No** |
| Product names | Mosquitto, InfluxDB, Node-RED, Grafana, React, Docker, Quarto | Open-source project names used **nominatively** (i.e., to refer to the named software, which is the topic of discussion). No logos reproduced; no UI screenshots reproduced. | Nominative fair use | **No** |
| Polish institutional terminology | Wydział Kształtowania Środowiska i Rolnictwa (WKSiR), Katedra Inżynierii Odnawialnych Źródeł Energii (KIOZE), Zachodniopomorski Uniwersytet Technologiczny (ZUT) | Names of the authors' own institutions. | N/A | **No** |

## What we did NOT do (and which would have triggered a permission requirement)

- **No** screenshots of third-party software UIs (Grafana dashboards, Node-RED editor, etc.) — our React UI is shown only in the graphical abstract and as descriptions; any future inclusion of such screenshots would need permission unless the project's licence permits.
- **No** reproduced figures from cited papers (Jiang, Saad, Silva, Balogh, etc.) — those papers are cited textually but their figures are not reused.
- **No** reproduced tables, datasets, or benchmark numbers from cited papers without independent recalculation.
- **No** long verbatim quotations (>30 words) from any source.
- **No** logos (Mosquitto, MDPI, InfluxData, OpenJS Foundation, etc.) inside the body figures or graphical abstract.

## Self-declaration for the submission portal

If susy.mdpi.com asks during submission whether any reproduced material is included:

> All figures, tables, listings, and data presented in this manuscript are the original work of the authors. No third-party copyrighted material has been reproduced. Cited prior works are referenced textually only.

## Verification before submission

- [x] `pics/` folder reviewed — every file is either (a) the authors' own creation, or (b) MDPI-provided template asset (`logo-ccby.eps`, `logo-mdpi.eps`, `logo-orcid.pdf`, `logo-updates.eps`, `mdpi_screenshot.png`, `placeholder.png`). The template assets are part of the MDPI Quarto extension and are licensed for use in MDPI submissions. ✅ 2026-05-28
- [x] `bibliography.bib` reviewed — every `@key` is a textual citation, not a figure/table reuse. ✅ 2026-05-28
- [x] No screenshots, photos, schematics, or datasets have been added since this audit (2026-05-28). ✅ 2026-05-28
- [x] Graphical abstract uses only original SVG drawn for this article — no clip-art, no vendor logos. ✅ 2026-05-28

---

*Audit date: 2026-05-28. Re-run if any figure, table, or substantial text passage is added or modified before submission.*
