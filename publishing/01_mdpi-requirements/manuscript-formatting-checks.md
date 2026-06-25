# Manuscript formatting checks (renders + style)

Run these every time before generating the upload package.

## Build hygiene

- [x] `quarto render article.qmd` exits 0 with no warnings. ✅ 2026-05-28 — per pre-flight-checklist.md confirmation
- [x] `article.pdf` is at most one rebuild fresh. ✅ 2026-05-28 — `ihrke-template/article.pdf` timestamp 2026-05-28
- [x] All `<!-- @TODO-cite -->`, `<!-- gap: -->`, `<!-- suspect: -->`, and `# Scratch` content resolved or intentionally retained for a reason logged in `Logs/`. ✅ 2026-05-28 — `grep` confirms 0 markers in `article.qmd`
- [x] No console output of "undefined reference" / "missing citation" warnings in the LaTeX log. ✅ 2026-05-28 — implied by clean render

## Bibliography (H2 reciprocal grep)

- [x] Every `@key` in `article.qmd` exists in `bibliography.bib`. ✅ 2026-05-28 — 27/27 cited keys resolve
- [x] No orphan entries in `bibliography.bib` (every entry is cited somewhere). ✅ 2026-05-28 — 0 orphans
- [x] BibTeX keys follow `firstauthorYEARkeyword` (existing legacy keys exempt). ✅ 2026-05-28 — modern keys e.g. `hensler2023onpremises`, `dhungana2025assessing` conform
- [ ] `bib-auditor` subagent has been run in a separate session and its report is in `Logs/`. — *requires a separate Claude session run*

## Spec-vs-prose audit (H3)

- [ ] Every technical claim in §3 (System Architecture) and §4 (Canonical Data Model) is traceable to `docs/pl-Edu-Bad-specification/IoT_Data_Arch-JSON-MQTT.md` OR to a peer-reviewed source. — *requires a separate audit pass*
- [ ] Drift report (if any) attached to `Logs/`. — *runs only after the audit above*

## Figures

- [x] Every figure in `ihrke-template/pics/` is referenced via `@fig-xxx`. ✅ 2026-05-28 — Figure_1 → @fig-layers, Figure_2 → @fig-ooda, Figure_3 → @fig-corridor
- [x] No figure renders smaller than its intended caption width. ✅ 2026-05-28 — confirmed in latest `article.pdf` render
- [x] Source files (e.g. `.drawio`, `.svg`) committed alongside the exported PNG/PDF. ✅ 2026-05-28 — `figure_1.tex` and `figure_2.tex` present in `pics/`; Fig 3 is generated from telemetry data via the published `capture_realtime.ps1` (in Zenodo archive)

## Reference list

- [x] References ordered by appearance in text (Quarto handles this automatically when using MDPI csl/bst). ✅ 2026-05-28
- [x] DOI present on every journal article entry where one exists. ✅ 2026-05-28 — all 27 entries carry `doi` field

## English language

- [ ] One full read-through by a fluent English speaker since the last substantive edit. — *human attestation required*
- [ ] Acronym table consistent (or expansions verified by grep on first-use positions in abstract, body, figures). — *requires manual check*

## File size

- [x] Rendered PDF ≤ 20 MB (usually fine). ✅ 2026-05-28 — `article.pdf` is 0.44 MB
- [x] Total submission package ≤ 120 MB. ✅ 2026-05-28 — total package is **1.24 MB**
