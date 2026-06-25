# 04_peer-review/ — one folder per round

MDPI normally returns reviewer comments in 2–4 weeks. Each decision letter starts a new round.

## Round structure

Each `round-NN/` folder is independent and follows the same layout:

> The editor's decision letter is stored verbatim under `comms/editorial-office/` (filename `yyyy-mm-dd-name`), not in this folder. This folder holds the reviewer reports and our working/response documents.

```
round-NN/
├── reviewer-1-comments.md      ← reviewer #1, verbatim
├── reviewer-2-comments.md      ← reviewer #2, verbatim
├── reviewer-3-comments.md      ← (if assigned) reviewer #3, verbatim
├── revision-plan.md            ← internal triage: accept / partial / push-back per point
├── response-to-reviewers.md    ← the rebuttal letter (point-by-point)
├── changes-summary.md          ← what changed in the manuscript, by section
└── uploaded/                   ← snapshot of files uploaded for this revision
    ├── article.pdf
    ├── article-tracked-changes.pdf   (if requested by MDPI)
    ├── ihrke-template-rNN.zip
    └── SHA256SUMS.txt
```

## Workflow inside a round

1. Drop the editor's letter verbatim into `comms/editorial-office/` (filename `yyyy-mm-dd-name`).
2. Split reviewer blocks into `reviewer-N-comments.md` files (one file per reviewer, including the editor's own comments if any).
3. Triage every point in `revision-plan.md`:
   - **Accept** — we'll change the manuscript as asked.
   - **Partial** — change but not exactly as asked; document the reasoning.
   - **Push back** — explain why we disagree; refer to evidence.
4. Implement the changes in `ihrke-template/article.qmd`. **One reviewer point per commit** with prefix `C?-rev:`.
5. Write `response-to-reviewers.md` — point-by-point, quoting the reviewer, our response, the resulting change with line numbers.
6. Fill `changes-summary.md` — high-level digest by section.
7. Re-render. Re-run `bib-auditor`. Re-run `reviewer-mdpi-full` for an internal red-team pass.
8. Submit revision via portal. Snapshot files into `uploaded/` with `SHA256SUMS.txt`.

## Discipline

- **Never edit `reviewer-N-comments.md` (or the editor's letter in `comms/editorial-office/`) after capture.** They are evidence.
- The rebuttal letter should be **calm, point-by-point, evidence-led, never combative**. Reviewers are doing volunteer work.
- If a reviewer is mistaken, push back politely with a citation; don't surrender just to be agreeable, but don't argue without evidence either.
- Track line numbers using the freshly rendered PDF for the revision, not the v1 PDF.
