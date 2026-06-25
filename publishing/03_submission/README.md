# 03_submission/ — the act of pressing Submit

This folder captures **what was actually submitted, when, and how**. Once submitted, this becomes evidence: which exact files reached the editor, with which SHA-256s.

## Files

- `submission-record.md` — manuscript ID, dates, portal account, what was uploaded.
- `pre-flight-checklist.md` — run line-by-line immediately before submission. Every box must be ticked, or stop.
- `v1-submitted/` — snapshot of the files uploaded (PDF, source ZIP, supplementary, cover letter).

## Discipline

- **Never overwrite `v1-submitted/`.** If the editor lets you replace files during initial check, snapshot the *new* set as `v1-submitted-2026MMDD-replacement/` rather than mutating the original.
- For each subsequent round of revision, create `04_peer-review/round-NN/uploaded/` snapshots.
- Record SHA-256 of every uploaded file in `submission-record.md`. Quick command:
  ```bash
  cd publishing/03_submission/v1-submitted
  sha256sum * | tee SHA256SUMS.txt
  ```
