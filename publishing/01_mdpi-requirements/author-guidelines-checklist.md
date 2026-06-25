# Author guidelines checklist — MDPI *Energies*

Derived from https://www.mdpi.com/journal/energies/instructions (synced 2026-05-27). Each item must be **TRUE** before pressing Submit.

## A. Manuscript content (front matter)

- [x] **Title** is concise, specific, and free of running-title / short-title prefixes. ✅ 2026-05-28
- [x] **Author list** uses full first + last names; initials acceptable for middle names. ✅ 2026-05-28
- [x] **Affiliations** use PubMed/MEDLINE format (street/dept, city, ZIP, country). ✅ 2026-05-28 — both ZUT and Karunya entries contain dept, street, postal code, city, country in the YAML
- [x] At least one author is marked as **corresponding** with a working email. ✅ 2026-05-28
- [x] **Abstract** ≤ 200 words, single paragraph, follows Background/Methods/Results/Conclusion structure (no headings). ✅ 2026-05-28
- [x] **Keywords**: 3–10, specific to the article. ✅ 2026-05-28

## B. Manuscript content (body)

- [x] **Introduction** places the work in context and states the aim explicitly. ✅ 2026-05-28 — §1 explicitly states the Impedance Mismatch problem and the three contributions C1–C3
- [x] **Materials and Methods** are reproducible; software versions named. ✅ 2026-05-28 — §3 + §5.1; Claude versions named in Acknowledgments + AI disclosure block; full reference implementation archived on Zenodo (DOI 10.5281/zenodo.20415136)
- [x] **Results** are presented before / separate from **Discussion** (or combined intentionally). ✅ 2026-05-28 — §5 Validation / §5.3 Performance Results precede §6 Discussion
- [x] **Conclusions** section present (optional but used here). ✅ 2026-05-28 — §7 Conclusions
- [x] **SI Units** throughout. Imperial / US units converted. ✅ 2026-05-28 — units throughout are SI / SI-derived: RPM, Nm, kW, kV, V, A, Hz, kPa, °C, pH, mg/L, m/s, ms
- [ ] **Acronyms** defined on first use in (a) abstract, (b) main text, (c) first figure or table. — *requires manual line-by-line check, not auto-verifiable*

## C. Back matter (mandatory blocks)

- [x] **Supplementary Materials** — N/A (no in-paper supplementary items; reference implementation is publicly archived on Zenodo and pointed to from the Data Availability Statement and §3.1). ✅ 2026-05-28
- [x] **Author Contributions** — full CRediT statement in YAML `authorcontributions:` block, matches `../02_pre-submission/author-contributions-credit.md`. ✅ 2026-05-28
- [x] **Funding** — Fundacja PGE (agreement 2025/VII/29) + APC by WKSiR ZUT; named in YAML `fundingstatement:`. Crossref Funder Registry has no entry for Fundacja PGE (documented). ✅ 2026-05-28
- [x] **Data Availability Statement** — Path B (Zenodo DOI 10.5281/zenodo.20415136 + GitHub repo) in YAML `dataavailability:`. ✅ 2026-05-28
- [x] **Acknowledgments** — GenAI disclosure block present in YAML `acknowledgments:` matching `ai-use-disclosure.md`. ✅ 2026-05-28
- [x] **Conflicts of Interest** — "The authors declare no conflicts of interest. The sponsors had no role…" in YAML `conflictsofinterest:`. ✅ 2026-05-28
- [x] **References** — 27 entries in `bibliography.bib`, all cited (0 orphans, 0 missing), 27/27 with DOI. Quarto + MDPI bst handles appearance ordering automatically. ✅ 2026-05-28

## D. Figures, tables, schemes

- [x] Resolution ≥ 600 dpi; PNG / JPEG / TIFF; RGB 8-bit. ✅ 2026-05-28 — body figures are vector PDFs (resolution-independent); graphical abstract is 2400×1200 PNG, 8-bit RGB
- [x] Figures placed near first citation in body. ✅ 2026-05-28 — Fig 1 at line 132 (cited line 130); Fig 2 at line 150 (cited line 136); Fig 3 at line 286 (cited line 282)
- [x] Captions complete; any special markers (`*`, `**`, `#`) explained. ✅ 2026-05-28
- [x] No imported copyrighted material without permission noted in caption. ✅ 2026-05-28 — see `copyright-permissions.md`; all content original
- [x] **Graphical abstract**: ≥ 560 × 1100 px, PNG/JPEG/TIFF, no "Graphical Abstract" text in image, not identical to any in-body figure. ✅ 2026-05-28 — 2400×1200 PNG, no heading, distinct flow view (different from layer/OODA diagrams)

## E. File package

- [x] LaTeX source assembled into a single ZIP including all `.tex`, `.bib`, figure files. ✅ 2026-05-28 — `ihrke-template-v1.zip` (588 KB, 36 files: qmd/tex/bib/figures/cls/bst/_extensions)
- [x] Compiled PDF included in the ZIP for editorial use. ✅ 2026-05-28 — `article.pdf` inside the ZIP, and separately as the editorial PDF
- [x] Supplementary files in common, non-proprietary formats where possible. ✅ 2026-05-28 — N/A in the upload (supplementary materials are hosted on Zenodo); JSON/YAML/MD inside the Zenodo archive
- [x] **Total upload ≤ 120 MB.** ✅ 2026-05-28 — total upload package is **1.24 MB**

## F. Cover letter & portal fields

- [x] Cover letter explains significance and scope fit for *Energies* / Section A1. ✅ 2026-05-28
- [x] Cover letter includes the **two mandatory statements**:
  - "We confirm that neither the manuscript nor any parts of its content are currently under consideration for publication with or published in another journal." ✅
  - "All authors have approved the manuscript and agree with its submission to *Energies*." ✅
- [ ] Suggested + excluded reviewers entered **in the submission system fields**, NOT in the cover letter. — *submission-day action*
- [x] Any prior MDPI submission acknowledged with prior MS ID. ✅ 2026-05-28 — N/A, no prior MDPI submission of this manuscript

## G. Authorship & ethics

- [x] All listed authors meet MDPI's authorship criteria. ✅ 2026-05-28
- [x] **No GenAI tool is listed as an author.** ✅ 2026-05-28 — only V.T. and K.G.M.K. in author block; Claude disclosed as a tool in Methods + Acknowledgments only
- [ ] All authors have approved the submission and read MDPI's Instructions for Authors. — *human attestation required*
- [x] If equal contribution: superscript † used and explained. ✅ 2026-05-28 — N/A, no equal-contribution claim (K.G.M.K. first author, V.T. senior + corresponding)

## H. Misc

- [ ] ORCID iDs attached to authors in the portal. — *submission-day action* (both ORCIDs already in `article.qmd`: 0009-0000-7377-6027 and 0000-0002-0567-267X)
- [x] If posted as a preprint, link disclosed in cover letter. ✅ 2026-05-28 — N/A, manuscript not posted as preprint
- [ ] Author biography (300–1500 chars) prepared and posted to SciProfiles (optional). — *optional*
