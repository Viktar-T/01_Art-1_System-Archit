# publishing/ — submission & lifecycle management for MDPI *Energies*

This folder is the workbench for everything that happens **around** the manuscript: cover letter, reviewer lists, journal checklists, peer-review correspondence, galley proofs, and post-publication tracking. The manuscript itself still lives in `ihrke-template/article.qmd`; nothing under `publishing/` ever goes into the rendered PDF.

Target venue: **MDPI *Energies*** — https://www.mdpi.com/journal/energies
Target section: **A1 — Smart Grids and Microgrids** (rationale in `../docs/03_MDPI-Energies.md`).

## Layout

```
publishing/
├── README.md                       ← this file (navigation + status)
├── STATUS.md                       ← single-line current state of the submission
├── 00_publishing-workflow.md       ← end-to-end workflow (S0 → S6) and entry checklist
│
├── 01_mdpi-requirements/           ← what MDPI requires; non-negotiable
│   ├── README.md
│   ├── author-guidelines-checklist.md
│   ├── manuscript-formatting-checks.md
│   ├── ethics-statements.md
│   ├── ai-use-disclosure.md
│   └── article-processing-charges.md
│
├── 02_pre-submission/              ← what we hand to the editor at S2
│   ├── README.md
│   ├── cover-letter.md
│   ├── suggested-reviewers.md
│   ├── conflicts-of-interest.md
│   ├── author-contributions-credit.md
│   ├── funding-statement.md
│   ├── data-availability-statement.md
│   ├── graphical-abstract-brief.md
│   └── highlights.md
│
├── 03_submission/                  ← record of the act of submitting
│   ├── README.md
│   ├── submission-record.md        ← MS ID, dates, portal account, files uploaded
│   ├── pre-flight-checklist.md     ← run this immediately before "Submit"
│   └── v1-submitted/               ← snapshot of files actually uploaded (PDF, zip, supp.)
│
├── 04_peer-review/                 ← one folder per round
│   ├── README.md
│   ├── round-01/
│   │   ├── reviewer-1-comments.md
│   │   ├── reviewer-2-comments.md
│   │   ├── reviewer-3-comments.md
│   │   ├── revision-plan.md
│   │   ├── response-to-reviewers.md
│   │   └── changes-summary.md
│   └── round-02/                   ← duplicate round-01 layout if needed
│
├── 05_post-acceptance/             ← from acceptance email through online publication
│   ├── README.md
│   ├── galley-proofs-log.md
│   ├── copyright-license-tracking.md
│   └── final-published-record.md   ← DOI, URL, vol/issue/page, publication date
│
└── 06_post-publication/            ← long-tail
    ├── README.md
    ├── promotion-plan.md           ← ORCID, SciProfiles, ResearchGate, social, talks
    ├── archiving.md                ← Zenodo / institutional repo / preprint
    └── citation-tracker.md
```

## Conventions

- **Living docs over snapshots.** Every file under `publishing/` is a working document — edit in place, commit small. Snapshots (e.g. the exact PDF that was uploaded) live under `03_submission/v1-submitted/`.
- **Truth from the journal page first.** When MDPI updates its instructions, refresh `01_mdpi-requirements/` from https://www.mdpi.com/journal/energies/instructions and date the change.
- **No fabricated metadata.** Never invent a manuscript ID, DOI, reviewer name, or date. Leave a `<!-- TODO -->` until the real value lands.
- **Commit prefix.** Use `Cx-pub:` for changes inside `publishing/` so they don't get confused with manuscript revisions (`Cx-draft:` / `Cx-rev:`).

## Status

See `STATUS.md` for the one-line state. Full workflow gates are in `00_publishing-workflow.md`.
