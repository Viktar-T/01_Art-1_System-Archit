# 00 — Publishing workflow for MDPI *Energies*

End-to-end map from "draft is good enough" to "DOI is live". Each phase has an **entry condition**, the **work to do**, and an **exit gate** that must be true before moving on.

The phases are S0–S6. Update `STATUS.md` as you cross each gate.

---

## S0 — Draft is ready for external review

**Entry condition.** The manuscript exists in `ihrke-template/article.qmd`, renders to a clean PDF, and the human authors believe it is broadly publication-quality.

**Work.**
- Run the `bib-auditor` subagent against `bibliography.bib`.
- Run the `reviewer-mdpi-full` subagent against the rendered PDF; capture output under `docs/art-review/self-review/`.
- Run a fresh human read-through.
- Open `01_mdpi-requirements/manuscript-formatting-checks.md` and tick every box.

**Exit gate.**
- `quarto render article.qmd` produces a clean PDF with no warnings.
- All `<!-- @TODO-cite -->` and `<!-- gap: -->` markers are resolved or explicitly accepted.
- No orphan or broken `@key` references.
- Human authors sign off in writing on the draft (in repo, e.g. a `Logs/` note).

---

## S1 — Pre-submission preparation

**Entry condition.** S0 exit gate cleared.

**Work.** Fill in every template under `02_pre-submission/`:
- `cover-letter.md` — significance, scope fit, mandatory statements.
- `suggested-reviewers.md` — 3–5 candidates with rationale and non-conflict justification.
- `conflicts-of-interest.md` — one statement per author.
- `author-contributions-credit.md` — CRediT taxonomy lines.
- `funding-statement.md` — exact funder names from https://search.crossref.org/funding.
- `data-availability-statement.md` — pick the matching MDPI canned statement.
- `graphical-abstract-brief.md` — design brief; deliver the PNG into `ihrke-template/pics/`.
- `highlights.md` — 3–5 bullet points (optional but recommended).

Also confirm:
- `01_mdpi-requirements/ai-use-disclosure.md` is reflected in the manuscript's Acknowledgments and Methods.
- `01_mdpi-requirements/article-processing-charges.md` has a real funding plan.

**Exit gate.** Every file in `02_pre-submission/` is no longer a template (no `[FILL]` markers).

---

## S2 — Submission

**Entry condition.** S1 exit gate cleared.

**Work.**
1. Walk through `03_submission/pre-flight-checklist.md`. Every box must be checked.
2. Go to https://susy.mdpi.com and submit. Choose section **A1 — Smart Grids and Microgrids**.
3. Upload the LaTeX source as a single ZIP (entire `ihrke-template/` minus `_extensions/` build cruft) **plus** the rendered PDF.
4. Paste the cover letter; paste suggested/excluded reviewers into the portal fields (not the cover letter — MDPI is explicit about this).
5. Record everything in `03_submission/submission-record.md`: MS ID, date, portal username, files uploaded with their SHA-256s.
6. Snapshot the uploaded files into `03_submission/v1-submitted/` so we can prove what we sent.

**Exit gate.**
- MS ID is assigned and recorded.
- `STATUS.md` advanced to S3.

---

## S3 — Under peer review

**Entry condition.** Submission acknowledged; MS ID assigned.

**Work.** Mostly waiting. While waiting:
- Resist editing the manuscript in `ihrke-template/article.qmd`. If urgent fixes are found, log them in `Logs/post-submission-defects.md` to apply during revision.
- Pre-build a draft `04_peer-review/round-01/response-to-reviewers.md` skeleton — most rebuttal letters reuse the same scaffolding.

**Exit gate.** Editor's first-round decision letter arrives.

---

## S4 — Revisions (one cycle per round)

**Entry condition.** Decision is *Major Revision*, *Minor Revision*, or *Reject & Resubmit*.

**Work.**
1. Save the editor's letter verbatim into `comms/editorial-office/` (filename `yyyy-mm-dd-name`).
2. Save each reviewer's verbatim comments into `reviewer-N-comments.md` (one file per reviewer).
3. Build `revision-plan.md`: for every reviewer point, decide *accept* / *partial* / *push back* + plan.
4. Implement the manuscript edits in `ihrke-template/article.qmd`, **one reviewer point per commit** with prefix `C?-rev:`.
5. Write `response-to-reviewers.md` — the rebuttal letter (one block per point, quoting the reviewer, then the response, then the line numbers changed).
6. Fill `changes-summary.md` — what changed in the manuscript, by section, with line ranges.
7. Re-render. Re-run the bib audit. Re-run the MDPI reviewer subagent for self-check.
8. Submit revision via the portal. Snapshot uploaded files into `04_peer-review/round-NN/uploaded/`.

**Exit gate.** Next decision letter arrives. If it's another revision, create `round-(NN+1)/`. If acceptance — S5.

---

## S5 — Post-acceptance, pre-publication

**Entry condition.** Acceptance email received.

**Work.**
- Sign the MDPI CC-BY licence (track in `05_post-acceptance/copyright-license-tracking.md`).
- Handle the APC: either confirm waiver/discount or initiate payment (record details, never the card number, in `article-processing-charges.md`).
- Receive galley proofs from MDPI production. Log every requested correction in `05_post-acceptance/galley-proofs-log.md` with the proof page number. Return proofs within MDPI's stated window (usually 48–72 h).

**Exit gate.** MDPI publishes the article online with a DOI.

---

## S6 — Published

**Entry condition.** DOI resolves.

**Work.**
- Capture final metadata in `05_post-acceptance/final-published-record.md`: DOI, full citation, vol/issue/article number, publication date.
- Execute `06_post-publication/promotion-plan.md` (ORCID, SciProfiles, ResearchGate, social, institutional press, conference reuse).
- Archive in Zenodo / institutional repo per `06_post-publication/archiving.md`.
- Start `06_post-publication/citation-tracker.md`; set a quarterly reminder.

**Exit gate.** None — this phase runs for the life of the paper.

---

## Roles & subagents in the publishing phase

- **Human authors (P1).** Sign off cover letter, reviewer list, every reviewer response, galley proofs, final published record. AI never decides these.
- **`reviewer-mdpi-full` subagent.** Run before every submission/resubmission as an internal red-team pass.
- **`bib-auditor` subagent.** Run before every submission/resubmission.
- Drafting subagents (e.g. `section-drafter`) may be invoked for rebuttal-letter scaffolding under explicit prompts, but never for final wording (P1).

## Disclosure obligation reminder

MDPI requires AI disclosure (see `01_mdpi-requirements/ai-use-disclosure.md`). The disclosure block in `article.qmd` Acknowledgments must mirror that file exactly. **Do not delete or soften it.**
