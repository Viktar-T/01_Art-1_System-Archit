# v1-submitted/ — snapshot of the initial submission

Drop the **exact files uploaded to susy.mdpi.com** here, then run:

```bash
sha256sum * | tee SHA256SUMS.txt
```

and paste the digests into `../submission-record.md`.

## Expected contents (typical)

- `article.pdf` — the editorial PDF.
- `ihrke-template-v1.zip` — the LaTeX source bundle.
- `graphical-abstract.png` — the GA image.
- `cover-letter.pdf` — exported from `../../02_pre-submission/cover-letter.md`.
- `supplementary-S1.zip` — supplementary materials (configs, schemas, sample traces).
- `SHA256SUMS.txt` — hash digest of every file above.

## Discipline

- **Never edit a file inside this folder after submission.** It is a fixed snapshot.
- If MDPI's editorial office requests replacement files during initial QC, snapshot the *replacement set* as `../v1-submitted-2026MMDD-replacement/` — leave this folder untouched.
- For revision rounds, snapshot under `../../04_peer-review/round-NN/uploaded/` instead.
