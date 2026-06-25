# Submission record — round 1 (initial submission)

> Fill on the day of submission. This is the audit trail.

## Identity

| Field | Value |
|---|---|
| Manuscript title | Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems |
| Manuscript ID (MDPI) | **energies-4374418** (assigned 2026-05-28) |
| Journal | *Energies* (MDPI) |
| Section | A1 — Smart Grids and Microgrids |
| Article type | Article (original research) |
| Special Issue? | [FILL — Yes/No; if yes, SI title + editor] |

## Authors (as submitted)

> Values match `ihrke-template/article.qmd` author block as of 2026-05-27 update, with K.G.M.K.'s metadata expanded from his IAESTE nomination form (Ref. PL-2025-ZUT044).

| # | Full name (manuscript spelling) | Affiliation(s) | Institutional email | ORCID | Role |
|---|---|---|---|---|---|
| 1 | Kelvyn George Melcheizedek Kanchipogu | (a) Department of Renewable Energy Sources Engineering, Faculty of Environmental Management and Agriculture, West Pomeranian University of Technology in Szczecin, ul. Pawła VI 1, 71-459 Szczecin, Poland — *IAESTE trainee, internship Mar–May 2026*; (b) Department of Computer Science and Engineering (Artificial Intelligence), Karunya Institute of Technology and Sciences, Karunya Nagar, Coimbatore, Tamil Nadu 641114, India — *home institution* | kanchipogukelvyn@karunya.edu.in | 0009-0000-7377-6027 | First author |
| 2 | Viktar Taustyka | Department of Renewable Energy Sources Engineering, Faculty of Environmental Management and Agriculture, West Pomeranian University of Technology in Szczecin, ul. Pawła VI 1, 71-459 Szczecin, Poland | viktar.taustyka@zut.edu.pl | 0000-0002-0567-267X | Senior and **corresponding author**; project lead |

### K.G.M.K. — extended profile (source: IAESTE nomination PL-2025-ZUT044, 28 April 2025)

| Field | Value |
|---|---|
| Full legal name | KANCHIPOGU, Kelvyn George Melcheizedek (family name: Kanchipogu; given names: Kelvyn George Melcheizedek) |
| Manuscript spelling (current) | Kelvyn George Melcheizedek Kanchipogu |
| Western academic ordering | Kelvyn George Melcheizedek Kanchipogu (given names first, family name last) — *see "Open inconsistencies" below* |
| Self-signed form (preferred) | Kelvyn G Melcheizedek Kanchipogu |
| Nationality | Indian |
| Date of birth | 17 December 2005 |
| Home institution | Karunya Institute of Technology and Sciences, Coimbatore, Tamil Nadu, India |
| Programme | B.Tech Computer Science and Engineering, specialisation: Artificial Intelligence |
| Years completed at time of nomination | 1.5 / 4 (expected graduation 2028) |
| CGPA at nomination | 9.42 |
| Institutional email (Karunya) | kanchipogukelvyn@karunya.edu.in |
| Phone (India) | +91 9652464080 |
| Home address (India) | 35-6-45/A, Durgam Satyam Street, Giripuram, Vijayawada, NTR District, PIN 520010, Andhra Pradesh |
| English level | C1 (per IAESTE language certificate) |
| Internship | West Pomeranian University of Technology in Szczecin — Department of Renewable Energy Sources Engineering, **02 March 2026 – 29 May 2026** (preferred period); max availability 01 March – 30 June 2026 |
| Internship reference | IAESTE Ref. No. **PL-2025-ZUT044** |
| ORCID iD | **0009-0000-7377-6027** (already in `article.qmd`; verify it resolves to him) |

### Open inconsistencies — RESOLUTION LOG (closed 2026-05-27)

1. ✅ **Corresponding author — V.T.** `article.qmd` now sets `corresponding: true` on V.T. (matching the cover letter, CLAUDE.md, and this file). K.G.M.K. remains first author. Conventional senior-researcher-as-corresponding pattern.

2. ✅ **K.G.M.K.'s institutional email.** Manuscript now uses `kanchipogukelvyn@karunya.edu.in` (Karunya institutional, per IAESTE form). Personal `kelvyn6612@gmail.com` retired from the author block.

3. 🟡 **Name format & CRediT initials — kept as "Kelvyn George Melcheizedek Kanchipogu" with abbreviation K.G.M.K.** Family-name-first ordering retained for now since it is what K.G.M.K. has used in the manuscript and all downstream files. ORCID `0009-0000-7377-6027` is authoritative — the ORCID record's preferred form is what MDPI will index. **Before submission, confirm with K.G.M.K. personally** which ordering he wants in print and that his ORCID record matches. If he prefers Western order ("Kelvyn George Melcheizedek Kanchipogu"), swap globally and update CRediT initials.

4. ✅ **K.G.M.K.'s Karunya affiliation added.** `article.qmd` `affiliations:` block now contains both ZUT (id 1) and Karunya (id 2); K.G.M.K.'s `affiliations:` lists both refs. V.T. only references ZUT.

5. ✅ **CRediT roles reconciled.** `article.qmd` author `roles:` arrays now mirror `02_pre-submission/author-contributions-credit.md`: V.T. on Conceptualization / Supervision / Project administration / Funding acquisition (alone) plus every role he shares with K.G.M.K.; K.G.M.K. on the 11 shared roles. A consolidated CRediT paragraph is now in `authorcontributions:` for the manuscript's Back Matter.

6. ✅ **Department name standardised — "Department of Renewable Energy Sources Engineering"** (the literal translation of KIOZE = Katedra Inżynierii Odnawialnych **Źródeł** Energii). `funding-statement.md` and this file have been updated to match the manuscript.

## Submission portal

| Field                               | Value                                                   |
| ----------------------------------- | ------------------------------------------------------- |
| Portal URL                          | https://susy.mdpi.com                                   |
| Manuscript status page              | https://susy.mdpi.com/user/manuscripts/status           |
| Submitting account (username/email) | viktar.taustyka@zut.edu.pl (V.T., corresponding author) |
| Submission date                     | **2026-05-28**                                          |
| Submission time (UTC)               | *[FILL once known]*                                     |
| Portal confirmation email received? | *[FILL — Yes/No, with timestamp]*                       |

## Files uploaded

> After upload, run `sha256sum` on each file from the local copy in `v1-submitted/` and paste the digest here.

| File | Role | Size | SHA-256 |
|---|---|---|---|
| `article.pdf` | Editorial PDF | 444 702 B | `a49d42de894932003cb21017154a5fc3316c084bebdb32919aef99dc45367d61` |
| `ihrke-template-v1.zip` | LaTeX source bundle (qmd, tex, bib, figures, MDPI engine, _extensions) | 601 768 B | `492642da5025ce524af2ae531b010439508c6f788c1c70ce4fd45dff910ecb07` |
| `graphical-abstract.png` | Graphical abstract (2400×1200 px) | 201 128 B | `28154486f88ab600d38416a1529a8d50afea7079287e05e2849cd53e0af64b43` |
| `cover-letter.pdf` | Cover letter (rendered from cover-letter.md via pandoc/xelatex) | 49 023 B | `a90f4b7cf39f143d2e9727513b18b8c5dcac2a566f179d848e4bbc2d159eaf93` |
| Supplementary materials | Hosted publicly on Zenodo (DOI 10.5281/zenodo.20415136) and GitHub — no separate upload zip needed; the DAS in the manuscript already points at the archive | — | — |

**Total upload package:** 1.24 MB (well under MDPI's 120 MB cap). SHA-256 digests also captured in `v1-submitted/SHA256SUMS.txt`.

## Portal-field content (paste verbatim)

### Cover letter
*(pasted in full from `../02_pre-submission/cover-letter.md`)*

### Suggested reviewers
*(from `../02_pre-submission/suggested-reviewers.md` — 3–5 entries)*

### Excluded reviewers
*(from `../02_pre-submission/suggested-reviewers.md` — usually none)*

### Funding
*(from `../02_pre-submission/funding-statement.md`)*

## Post-submission tracking

- [x] **Submission confirmed by portal.** MS ID **energies-4374418** displayed at https://susy.mdpi.com/user/manuscripts/status on 2026-05-28.
- [x] Confirmation email received. Date / sender: 2026-05-28 / Energies Editorial Office (energies@mdpi.com).
- [x] Initial QC by Editorial Office complete (no file replacements requested): passed — manuscript recommended to Preprints.org after initial screening; no file replacements requested.
- [x] Editor assigned. Date / name: by 2026-06-02 / **Leroy Liu**, Assistant Editor (leroy.liu@mdpi.com).
- [ ] First decision letter received. Date:

> **Pre-review editorial queries open (received by 2026-06-02) — awaiting V.T. reply to Leroy Liu:**
> 1. **Author order / corresponding author discrepancy.** System lists "Viktar Taustyka \*, Kelvyn George Melcheizedek Kanchipogu"; manuscript order is **Kanchipogu (1st), Taustyka (2nd, corresponding)**. Reply: correct order = Kanchipogu 1st, Taustyka 2nd; corresponding = V. Taustyka. Ask the office to re-order the system record to match the manuscript.
> 2. **Open Peer Review confirmation.** Office flags that OPR (review reports + responses published alongside the paper) was selected and is distinct from Open Access. **Decision needed from V.T.** — keep or deselect.
> 3. **APC confirmation.** 2600 CHF − 10% IOAP (ZUT) = **2340 CHF**. Confirm amount + invoice address at the APC link; confirm open-access support / agreement to pay if accepted. NOTE: invoice address in the email reads *al. Piastów 17, 70-310 Szczecin* (ZUT central) vs the manuscript's department address *ul. Pawła VI 1, 71-459 Szczecin* — verify which the Faculty/Dziekanat WKSiR wants on the invoice.
> 4. ✅ **Preprints.org.** Posted post-submission via MDPI recommendation. Online **2026-06-10** — Preprints ID **10.20944/preprints202606.0245.v1**; DOI https://doi.org/10.20944/preprints202606.0245.v1; page https://www.preprints.org/manuscript/202606.0245/v1 (see `06_post-publication/archiving.md`, `comms/preprints/2026-06-10-preprints-org-online-notification.md`).
- [ ] Decision: [Major / Minor / Reject & Resubmit / Accept]
- [ ] Moved to `04_peer-review/round-01/`.

## Replacements (if any) during initial check

If the Editorial Office requests file replacements during initial QC, record here:

| Date | Files replaced | Reason | New SHA-256(s) |
|---|---|---|---|
| | | | |
