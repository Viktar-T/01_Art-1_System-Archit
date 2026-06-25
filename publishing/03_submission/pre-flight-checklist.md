# Pre-flight checklist — run immediately before submission

If any box is unchecked, **do not submit**. Fix or escalate.

## 1. Manuscript

- [x] `quarto render article.qmd` is green (0 errors, 0 warnings). ✅ 2026-05-28
- [x] Latest `article.pdf` is the version about to be uploaded. ✅ 2026-05-28
- [x] All `<!-- @TODO -->`, `<!-- gap: -->`, `<!-- suspect: -->` markers and `# Scratch` content resolved or intentionally retained with a reason in `Logs/`. ✅ 2026-05-28
- [x] Title, abstract, keywords reviewed by ALL authors in the last 7 days. ✅ 2026-05-28
- [x] Abstract ≤ 200 words (counted). ✅ 2026-05-28

## 2. Required sections present (in `article.qmd`)

- [x] Title, Author list (with affiliations + corresponding author marker) ✅ 2026-05-28
- [x] Abstract ✅ 2026-05-28
- [x] Keywords (3–10) ✅ 2026-05-28
- [x] Introduction ✅ 2026-05-28
- [x] Materials and Methods (including **AI use disclosure**) ✅ 2026-05-28
- [x] Results ✅ 2026-05-28
- [x] Discussion ✅ 2026-05-28
- [x] Conclusions ✅ 2026-05-28
- [x] Supplementary Materials list ✅ 2026-05-28
- [x] Author Contributions (CRediT) ✅ 2026-05-28
- [x] Funding ✅ 2026-05-28
- [x] Data Availability Statement ✅ 2026-05-28
- [x] Acknowledgments (including the **AI Acknowledgments block**) ✅ 2026-05-28
- [x] Conflicts of Interest ✅ 2026-05-28
- [x] References ✅ 2026-05-28

## 3. Pre-submission packet (in `../02_pre-submission/`)

- [x] `cover-letter.md` — no `[FILL]` markers left. ✅ 2026-05-28
- [x] `suggested-reviewers.md` — 3 verified Polish entries with conflict check. ✅ 2026-05-28 (could add 1–2 international backups; 3 is acceptable to MDPI)
- [x] `conflicts-of-interest.md` — completed per author (no conflicts). ✅ 2026-05-28
- [x] `author-contributions-credit.md` — completed, copied into `article.qmd` as `authorcontributions:`. ✅ 2026-05-28
- [x] `funding-statement.md` — Fundacja PGE looked up in Crossref (not registered; documented) + APC funder identified (WKSiR, ≥140 pkt MEiN rule). ✅ 2026-05-28
- [x] `data-availability-statement.md` — Path B chosen; Zenodo DOI 10.5281/zenodo.20415136 minted. ✅ 2026-05-28
- [x] `graphical-abstract.png` — 2400×1200 PNG produced. ✅ 2026-05-28
- [x] `highlights.md` — 5 highlights drafted from the abstract. ✅ 2026-05-28
- [x] `copyright-permissions.md` — audit complete, no permissions needed. ✅ 2026-05-28
- [ ] `data-availability-statement.md` — chosen variant pasted into `article.qmd`.
- [ ] `graphical-abstract-brief.md` — image produced, exported at right size.
- [ ] `highlights.md` — 3–5 bullets ready.

## 4. MDPI requirements (`../01_mdpi-requirements/`)

- [ ] `author-guidelines-checklist.md` — every box ticked.
- [ ] `manuscript-formatting-checks.md` — every box ticked.
- [ ] `ethics-statements.md` — every section addressed (or N/A with reason).
- [ ] `ai-use-disclosure.md` — Methods + Acknowledgments blocks match exactly.
- [ ] `article-processing-charges.md` — APC funding plan recorded.

## 5. File package

- [ ] LaTeX source ZIP built and named `ihrke-template-v1.zip`. Contains `article.qmd` / `article.tex`, `bibliography.bib`, all `pics/`, and is reproducible by MDPI on their LaTeX system.
- [ ] PDF included in the ZIP, also uploaded separately as the editorial PDF.
- [ ] Total package ≤ 120 MB.
- [ ] Each figure ≥ 600 dpi, in PNG/JPEG/TIFF.
- [ ] Graphical abstract ≥ 560 × 1100 px.

## 6. Portal mechanics

- [ ] Logged in as the corresponding author at https://susy.mdpi.com.
- [ ] Selected journal: *Energies*, section A1.
- [ ] All co-authors entered with verified emails + ORCID.
- [ ] Suggested + excluded reviewers entered in their portal fields (not in cover letter).
- [ ] Cover letter pasted.
- [ ] Funding entered into portal fields (deposits to FundRef on acceptance).

## 7. Snapshot

- [ ] Final upload set copied into `v1-submitted/`.
- [ ] `sha256sum * > SHA256SUMS.txt` recorded in `v1-submitted/`.
- [ ] `submission-record.md` filled with date + SHA-256s **after** clicking Submit.

## 8. Sign-off

- [ ] Corresponding author (V.T.) confirms: "I am clicking Submit now." (date/time)
- [ ] All co-authors emailed with a heads-up that submission was completed.
