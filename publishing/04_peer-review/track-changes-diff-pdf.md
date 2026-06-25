# Track-changes / diff PDF — how we mark revisions for MDPI

When we resubmit a revised manuscript, MDPI expects the changes to be **visibly marked** so the editor and reviewers can see what moved, alongside the point-by-point response letters. Because our manuscript is generated (Quarto → LaTeX → PDF), we do **not** hand-colour text. Instead we generate a **track-changes / diff PDF** with `latexdiff`. This document explains what it is, why it fits our workflow, and exactly how to produce it.

---

## 1. What it is

A track-changes / diff PDF is a single PDF that shows, inline, what changed between two versions of the manuscript:

- **Added** text appears in one colour (by default blue, underlined).
- **Removed** text appears in another colour (by default red, struck through).

It is the LaTeX-world equivalent of Microsoft Word's "Track Changes". The tool is **`latexdiff`** (ships with TeX Live / TinyTeX): given the *old* `.tex` and the *new* `.tex`, it emits a combined `.tex` with the changes marked up, which we compile to `article-tracked-changes.pdf`. MDPI accepts this as the marked-up revision.

## 2. Why this fits our repository / AI / doc-to-code approach

- **Reproducible (P3).** It is a build step — one command, deterministic — not manual marking.
- **Clean source.** `article.qmd` stays clean; the diff is *generated*, never committed as colour markup that we'd later have to strip.
- **AI-runnable.** An agent can produce the diff PDF end-to-end without human judgement on every edit.
- **Git-native.** It mirrors what git already tracks at the source level, but turns it into a reader-facing PDF for reviewers.
- **We already have what it needs:** we render with `keep-tex: true` (so the `.tex` exists) and we snapshotted v1 (`publishing/03_submission/v1-submitted/`), so the baseline exists.

## 3. Prerequisites

- Quarto CLI + a working LaTeX install (TinyTeX or TeX Live). `latexdiff` is bundled with TeX Live/TinyTeX — check with `latexdiff --version`.
- The **baseline** (submitted v1) `article.tex`, and the **revised** `article.tex` from the current render.

## 4. Procedure (Windows / PowerShell)

Run from the repository root unless noted. Adjust paths if your snapshot differs.

### Step 1 — Get the baseline `.tex` (submitted v1)

Either extract it from the submitted snapshot:

```powershell
# Extract the submitted v1 LaTeX source into a temporary baseline folder
Expand-Archive -Path "publishing/03_submission/v1-submitted/ihrke-template-v1.zip" -DestinationPath "publishing/04_peer-review/round-01/_diff/v1" -Force
# -> baseline TeX expected at publishing/04_peer-review/round-01/_diff/v1/article.tex
```

…or, equivalently, check out the submitted commit/tag and render it. Use whichever baseline is authoritative.

### Step 2 — Render the revised manuscript to `.tex`

```powershell
cd ihrke-template
quarto render article.qmd --to mdpi-pdf   # keep-tex: true produces article.tex
cd ..
Copy-Item "ihrke-template/article.tex" "publishing/04_peer-review/round-01/_diff/v2/article.tex" -Force
```

### Step 3 — Run `latexdiff`

```powershell
latexdiff `
  "publishing/04_peer-review/round-01/_diff/v1/article.tex" `
  "publishing/04_peer-review/round-01/_diff/v2/article.tex" `
  > "publishing/04_peer-review/round-01/_diff/article-diff.tex"
```

### Step 4 — Compile the diff `.tex` with the MDPI class

Compile inside `ihrke-template/` so the MDPI `.cls`, `.bst`, and `_extensions/` assets resolve. Copy the diff in, build, and move the PDF out:

```powershell
Copy-Item "publishing/04_peer-review/round-01/_diff/article-diff.tex" "ihrke-template/article-diff.tex" -Force
cd ihrke-template
latexmk -pdf article-diff.tex   # or: pdflatex article-diff && bibtex && pdflatex x2
cd ..
Copy-Item "ihrke-template/article-diff.pdf" "publishing/04_peer-review/round-01/uploaded/article-tracked-changes.pdf" -Force
```

### Step 5 — Clean up

Remove the scratch `_diff/` folder and the `article-diff.*` build files from `ihrke-template/` (they are intermediates, not source). Keep only `uploaded/article-tracked-changes.pdf`.

## 5. What to upload at resubmission

1. **Clean revised manuscript** — the normal `article.pdf` (and the LaTeX source ZIP).
2. **Marked-up manuscript** — `article-tracked-changes.pdf` (this file).
3. **Response letters** — the per-reviewer responses in `reviewer-N/reviewer-N-response.md`, each citing the change location (page / paragraph / line) in the **revised** PDF.

## 6. Caveats (budget ~10–20 min of tidy-up)

`latexdiff` is excellent on prose but can be **noisy around tables, code listings, figures, and math**, and because Quarto *regenerates* the `.tex`, cosmetic formatting differences can show up as fake "changes". Mitigations:

- Try `latexdiff --flatten` if the source pulls in includes.
- For math/listings noise, see `latexdiff --math-markup=whole` and `--config` options, and `--append-safecmd` / `--append-textcmd` for MDPI-specific custom commands that confuse the parser.
- If a region is hopelessly noisy, you can wrap it with `%DIF < ... > ` controls or fall back to manually noting that block's change in the response letter.
- Keep edits between v1 and the revision **as structural-minimal as possible** (don't reflow whole paragraphs you didn't change) to keep the diff readable.

## 7. One-command future

If we run this every round, it is worth wrapping Steps 1–5 in a script (e.g. `publishing/scripts/make-diff.ps1`) so the marked-up PDF is a single command. Ask if you want that wired up.
