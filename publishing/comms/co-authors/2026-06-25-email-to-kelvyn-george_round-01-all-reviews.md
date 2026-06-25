# Email to Kelvyn George — round-1 all reviews received

| Field | Value |
|---|---|
| Direction | Outgoing (V.T. → co-author) |
| To | Kelvyn George Melcheizedek Kanchipogu — kanchipogukelvyn@karunya.edu.in |
| From | Viktar Taustyka — viktar.taustyka@zut.edu.pl |
| Date drafted | 2026-06-25 |
| Re | Energies, MS energies-4374418 — round-1 review (all three reports now in) |
| Status | DRAFT — ready to send |

---

**Subject:** Energies (energies-4374418) — all three review reports are in, please action the revisions

Hi Kelvyn,

Thank you again for your work on the first reviewer report. I have not checked your work yet, because all the reviewer reports have now arrived and I decided it would be better to address them all at the same time, as they have some points in common.

All three reviewer reports are now available on https://susy.mdpi.com/, and I have copied them into the repository so we can work from a single source of truth:

- `publishing/04_peer-review/round-01/reviewer-1/`
- `publishing/04_peer-review/round-01/reviewer-2/`
- `publishing/04_peer-review/round-01/reviewer-3/`

Based on the reports, I have created an action plan at `publishing/04_peer-review/round-01/round-01-action-plan.md`. Feel free to correct the plan.

Could you please take the lead on the revisions and make the relevant updates in two places:

1. **Our codebase on GitHub** — the implementation evidence the reviewers are asking for (see below), and a fresh release when the revisions are done so we can cite it in the responses.
2. **The manuscript** (`ihrke-template/article.qmd`) — the text, figures, tables, and references.

Then please write our answers directly into the per-reviewer response files (each one already has the reviewer's comments pre-filled verbatim, with placeholders for our response, the exact location of each change — page/paragraph/line — and a short note on the planned approach):

- `publishing/04_peer-review/round-01/reviewer-1/reviewer-1-response.md`
- `publishing/04_peer-review/round-01/reviewer-2/reviewer-2-response.md`
- `publishing/04_peer-review/round-01/reviewer-3/reviewer-3-response.md`


The response files contain internal *(plan: …)* hints for our own use — please delete those before we submit, and reference the exact location of each change (page / paragraph / line) in the revised PDF.

On marking the changes: MDPI wants a revised manuscript with the changes visibly marked. You can do it by marking all manuscript changes in red, and reference the exact location of each change in the revised PDF.
But since our manuscript is generated (Quarto → LaTeX → PDF), we do **not** hand-colour text in red. Instead we produce a **track-changes / diff PDF** with `latexdiff` (old `.tex` vs revised `.tex` → `article-tracked-changes.pdf`). This keeps `article.qmd` clean, is reproducible, and is exactly the kind of step our repo/AI workflow handles well. I've written up the how-to (what it is, why it fits us, and the exact commands) here: `publishing/04_peer-review/track-changes-diff-pdf.md`. So at resubmission we upload the clean revised PDF + the diff PDF + the response letters — no manual red-pen needed.

There is no MDPI deadline yet, so let's do the visuals and the extra results thoroughly rather than minimally. I'll coordinate and assemble the final rebuttal.

Thank you.

Best regards,
Dr. Viktar Taustyka
