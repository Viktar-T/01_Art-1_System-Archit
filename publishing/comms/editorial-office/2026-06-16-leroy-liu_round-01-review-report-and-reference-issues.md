# Incoming — Leroy Liu: round-1 review report + reference issues

| Field | Value |
|---|---|
| Direction | Incoming (Editorial Office → V.T.) |
| From | Mr. Leroy Liu, Assistant Editor — leroy.liu@mdpi.com |
| To | Viktar Taustyka (corresponding author) |
| Date logged | 2026-06-16 (confirm exact receipt date) |
| Re | *Energies*, Manuscript ID **energies-4374418** — first review report (round 1) |
| Decision | No decision yet — interim update. First decision to follow once all reports are in and the academic editor has decided. |
| Deadline for revision | Not set yet (no formal revision invitation issued). |
| Attachment | `Comments and Suggestions for Authors.pdf` → captured in `04_peer-review/round-01/reviewer-1/` |

---

## Summary

- **One** review report returned (Reviewer 1). Other reviewers' reports still pending; the academic editor's **first decision will follow** once all reports are in.
- Editorial office's technical check flagged **reference problems**: Ref 5 (author name), Ref 11 (DOI), Refs 12 & 15 (conference names) — and asked us to **check and correct all references**.
- We may begin revising now.

## Full e-mail (verbatim)

> Interim progress e-mail — **not** the formal decision letter. [Highly Cited Paper Recommendations and MDPI footer omitted — not part of the editorial content.]

Dear Dr. Taustyka,

I hope this email finds you well.

We have received one review report now. In order to let you know your paper's every progress and shorten the article processing time, we would like to send you this review report. Please check the attachment and start to revise your paper if possible.

Additionally, during the editorial office's technical check of your manuscript, it was found that some of the references in your manuscript have issues. For example: the author name in Reference 5 is incorrect, the DOI in Reference 11 is incorrect, and the conference names in References 12 and 15 are incorrect. While revising the content of your manuscript, please also check and correct all the references.

Please note that we are still waiting for other reviewers' review reports. We will send the first decision to you soon after we receive all review reports and get our academic editor's decision on your manuscript. Should you have any questions, please let me know.

Kind regards,
Mr. Leroy Liu
Assistant Editor
E-Mail: leroy.liu@mdpi.com

## Related artifacts

- Reviewer 1 report verbatim → `04_peer-review/round-01/reviewer-1/reviewer-1-comments.md` (attachment `Comments and Suggestions for Authors.pdf` in the same folder).
- Triage of all points + reference fixes → `04_peer-review/round-01/revision-plan.md`.

## Internal notes (not for MDPI)

- **Reviewer count so far:** 1 returned (Reviewer 1 — see `04_peer-review/round-01/reviewer-1/reviewer-1-comments.md`). Reviewer 2 / 3 reports still pending at the time of this e-mail; no formal decision yet.
- **Editorial-office reference issues (technical check), to be corrected during revision:**
  - **Ref 5** — author name incorrect.
  - **Ref 11** — DOI incorrect.
  - **Ref 12** — conference name incorrect.
  - **Ref 15** — conference name incorrect.
  - The office asks us to **check and correct all references**, not only these examples. Tracked as EO.1–EO.4 in `revision-plan.md`.
- **Headline themes from Reviewer 1:**
  - **Prove the implementation visually** — Grafana dashboard images and a Node-RED flow screenshot are the strongest requests (reviewer ties acceptance of the "successful implementation" claim to these).
  - **More simulation results** — the reviewer "misses more results of the conducted simulations."
  - **Framing/clarity** — rename §5.1 (it's a simulation, not an "experimental setup"), merge the two limitations subsections (6.2 + 7.2), define abbreviations (SCADA, JSON), add "open-source" keyword.
  - **Positioning** — add recent open-source / Node-RED / Grafana energy references (two specific DOIs suggested).
  - **One broken reference at line 125** — overlaps with the known Zenodo `@software` entry that renders as "[?]".
- **Risk assessment:** No decision is locked yet, so the biggest threat is treating R1 as the whole picture and being surprised by R2/R3. R1 itself is constructive (Minor/Major-revision tone, no rejection signal). The acceptance-critical items are the missing dashboard/flow visuals and "more results" — these should be done thoroughly, not minimally.
- **Owner of manuscript fixes:** Kelvyn George (K.G.M.K.) — review handed off 2026-06-16 (see `comms/co-authors/2026-06-16-email-to-kelvyn-george_round-01-review.md`). V.T. coordinates and writes the rebuttal.

## Action taken

- Status moved to **S3 — under peer review (round 1)**.
- Review handed off to **Kelvyn George (K.G.M.K.)** for fixing → `comms/co-authors/2026-06-16-email-to-kelvyn-george_round-01-review.md`.

## Open

- No reply to the editor required yet — wait for the formal first decision before submitting the revision and rebuttal.
