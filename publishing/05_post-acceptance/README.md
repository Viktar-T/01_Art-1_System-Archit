# 05_post-acceptance/ — from acceptance email to DOI live

This phase is short (typically 1–3 weeks at MDPI) but easy to mishandle. The deadlines from MDPI Production are real and often tight (48–72 h for galley proof corrections).

## Files

- `galley-proofs-log.md` — every proof correction, by proof page number.
- `copyright-license-tracking.md` — CC-BY licence, copyright forms, APC invoice/payment.
- `final-published-record.md` — DOI, citation, vol/issue, publication date, archived PDF.

## Workflow

1. Save the acceptance email (and any conditional-acceptance items) outside the repo; just record the date here.
2. Sign the MDPI CC-BY licence — log in `copyright-license-tracking.md`.
3. Receive Galley A — review carefully, log every correction in `galley-proofs-log.md`, return within MDPI's stated window.
4. Receive Galley B (if MDPI iterates) — repeat.
5. Approve final proof. Capture the DOI, URL, citation in `final-published-record.md`.
6. Move `STATUS.md` to S6.

## Discipline

- **Read every page of the proof, not just the diff.** MDPI's typesetters can introduce subtle errors (e.g. dropped subscripts, broken equation references).
- **Verify every citation in the typeset version.** Numbering can shift.
- **Verify your name, affiliation, ORCID, and corresponding-author email.** These are very hard to correct after publication.
- **Verify every URL / DOI in the bibliography resolves.** Proofreaders rarely click links.
