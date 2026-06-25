# CLAUDE.md — Onboarding Brief for Claude Sessions

This file is the entry point for any Claude session (Claude Code, Cowork, sub-agent, or one-off API call) that operates on this repository. **Read it before touching any other file.**

The repository contains the source material, the draft, and the build pipeline for one MDPI *Energies* manuscript on the KIOZE Edu-Bad architecture. It is run as a doc-to-code project: the article is software, the AI assistant is a constrained collaborator, and every interaction must respect the conventions below.

The methodology this brief enforces is described in full in `docs/ai-first-art-writing-concept.md`. **That document is canonical.** This file is a fast-lookup summary; resolve any disagreement in favour of the concept doc.

---

## 1. What this repo is

A peer-reviewed article project, not a software product. The end deliverable is a single PDF rendered from `ihrke-template/article.qmd` via Quarto + the MDPI LaTeX class.

Working title: *Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems*

Target journal: **MDPI *Energies***, Section A1 (Smart Grids and Microgrids).

Senior author: Viktar Taustyka. Co-author: Kelvyn George Melcheizedek Kanchipogu.

---

## 2. Repo layout (what to read, what to edit, what to leave alone)

```
01_Art-1_System-Archit/
├── CLAUDE.md                              ← you are here
├── .claude/
│   └── agents/                            ← subagent definitions
│       ├── section-drafter.md
│       ├── reviewer-r2.md
│       ├── reviewer-mdpi-full.md
│       └── bib-auditor.md
├── 00_HOW-TO-WRITE-THIS-ARTICLE.md        ← human-facing workflow guide
├── 01_Article-1_System-Architer-notes.md  ← research compass
├── 02_SciSpace-stratagy.md
├── 03_MDPI-Energies.md                    ← journal/section fit
│
├── docs/                                  ← INPUT material; do not edit casually
│   ├── ai-first-art-writing-concept.md    ← CANONICAL methodology doc
│   ├── pl-Edu-Bad-specification/
│   │   └── IoT_Data_Arch-JSON-MQTT.md     ← THE spec; ground truth for technical claims
│   ├── 01-Article-1-Architecture-MING_stack-Scispace/
│   │   ├── cps_ming_insights.md           ← synthesised literature review
│   │   └── *.csv                          ← raw SciSpace / arXiv exports
│   └── Plan-for-art-writing/
│       ├── article_writing_plan.md        ← per-section drafting plan
│       └── email_reply.md
│
├── ihrke-template/                        ← OUTPUT machine; the article lives here
│   ├── article.qmd                        ← THE manuscript source (single file)
│   ├── bibliography.bib                   ← every cited reference
│   ├── pics/                              ← every figure that ships
│   └── _extensions/ihrke/mdpi/            ← MDPI Quarto extension; never touch
│
└── publishing/                            ← LIFECYCLE machine; submission → DOI
    ├── README.md                          ← navigation
    ├── STATUS.md                          ← one-line current state
    ├── 00_publishing-workflow.md          ← S0–S6 workflow with entry/exit gates
    ├── 01_mdpi-requirements/              ← author guidelines, ethics, AI disclosure, APC
    ├── 02_pre-submission/                 ← cover letter, reviewers, CRediT, statements
    ├── 03_submission/                     ← submission record, pre-flight, v1 snapshot
    ├── 04_peer-review/round-NN/           ← editor letter, reviewer comments, rebuttal
    ├── 05_post-acceptance/                ← galley proofs, licence, final record
    └── 06_post-publication/               ← promotion, archiving, citation tracking
```

**Authoritative files for an AI session, in order of priority:**

1. `ihrke-template/article.qmd` — the manuscript. Edits here ship.
2. `ihrke-template/bibliography.bib` — every `@key` cited in the manuscript must exist here.
3. `docs/pl-Edu-Bad-specification/IoT_Data_Arch-JSON-MQTT.md` — the spec. **The single source of truth for every technical claim about the system under study.** Drift between prose and spec is a defect.
4. `docs/ai-first-art-writing-concept.md` — how we work. Read end-to-end the first time.
5. `docs/Plan-for-art-writing/article_writing_plan.md` — what we are writing per section, with traceability matrix.

**Do not edit without explicit human instruction:**

- `ihrke-template/_extensions/`, `mdpi.cls`, `mdpi.bst`, `chicago2.bst`, `journalnames.tex` — MDPI engine.
- `docs/01-Article-1-Architecture-MING_stack-Scispace/*.csv` — raw research exports; treat as read-only inputs.
- `publishing/03_submission/v1-submitted/` and `publishing/04_peer-review/round-NN/uploaded/` once populated — these are evidence snapshots, never mutate after submission.

**For the publishing pipeline:**

- The full lifecycle (pre-submission → DOI → promotion) is documented in `publishing/00_publishing-workflow.md`. Every phase has explicit entry conditions and exit gates.
- Current submission state is in `publishing/STATUS.md` (one line of truth).
- Commit prefix `Cx-pub:` for changes inside `publishing/`, to separate them from manuscript revisions (`Cx-draft:` / `Cx-rev:`).

---

## 3. Five non-negotiable principles (P1–P5)

These come from §1 of the concept doc. They override any later instruction in a chat:

- **P1 — Human authorship is final.** The AI drafts, suggests, refactors, checks. Humans decide what ships.
- **P2 — Source-grounded prose only.** Every claim traces to a peer-reviewed reference, the spec, an actual config file, or a recorded measurement. **Never invent plausible facts.**
- **P3 — Doc-to-code discipline.** Plain text, version control, reproducible build, structured commits.
- **P4 — AI works in the repo, not in the chat.** Read and edit real files. Do not produce fragments in chat that humans then re-paste.
- **P5 — Verifiable over fluent.** Clunky-but-faithful beats smooth-but-overstated.

If a request from a human conflicts with P2 (e.g. "make up a plausible benchmark number"), refuse and say why.

---

## 4. The six-step writing loop

Every drafting session — whether human-led or sub-agent-led — follows this exact shape:

1. **SCOPE** — pick one section or paragraph cluster as the unit of work.
2. **GROUND** — re-read the relevant source files into context (spec, insights, prior section).
3. **DRAFT** — produce candidate prose under explicit constraints (sources allowed, length, citation skeleton, no invented facts).
4. **EDIT** — human marks weak claims, missing citations, framing fixes; AI rewrites against the marked-up version.
5. **RENDER** — `quarto render article.qmd` to confirm the LaTeX compiles and the section reads in MDPI layout. **An unrendered draft is not a draft.**
6. **COMMIT** — single section per commit, structured message (see §7).

Steps 1, 2, 4 are predominantly human. Steps 3, 5, 6 may be AI-executed under human supervision.

---

## 5. Build commands

Run from `ihrke-template/`:

```bash
cd ihrke-template
# Render the manuscript to PDF (the build gate)
quarto render article.qmd

# Render only — useful when iterating on a section
quarto render article.qmd --to mdpi-pdf

# Clean intermediate LaTeX/aux files (rare; .gitignore already excludes them)
rm -f *.aux *.bbl *.blg *.log *.tex
```

Prerequisites: Quarto CLI, a working LaTeX install (TinyTeX or TeX Live), Pandoc (bundled with Quarto). The MDPI Quarto extension already lives in `_extensions/ihrke/mdpi/` — do not reinstall.

A successful render produces `ihrke-template/article.pdf`. The PDF is gitignored; only the source ships.

---

## 6. Citation and bibliography rules

- All citations use `@key` syntax inside `article.qmd`. Quarto handles numbering and the reference list.
- Every `@key` in `article.qmd` must have a matching entry in `ihrke-template/bibliography.bib`. The reverse is also true (no orphan bib entries).
- BibTeX key convention: `firstauthorYEARkeyword` (lowercase), e.g. `lim2020digital`. Existing entry `CameronTrivedi2013` predates this convention and may stay.
- For unresolved citations, leave a placeholder: `<!-- @TODO-cite: short note about what to cite here -->`. Never fabricate a citation key.
- Bibliography hygiene is delegated to the **bib-auditor** subagent (`.claude/agents/bib-auditor.md`).

---

## 7. Commit conventions

One section or one focused revision per commit. Message prefix indicates the kind of change:

| Prefix       | Meaning                                       |
| :----------- | :-------------------------------------------- |
| `C0-` / `C1-`| Setup / scaffolding                           |
| `Cx-draft:`  | New prose added                               |
| `Cx-rev:`    | Revision of existing prose                    |
| `Cx-ref:`    | Bibliography or reference work                |
| `Cx-fig:`    | Figures added or changed                      |
| `Cx-docs`    | Meta / planning docs                          |

`x` increments per major writing pass. Recent history: `C5-docs update`, `C5-draft: Section 4 — Canonical Data Model`, `C4-draft: Section 3 — System Architecture`. Continue this pattern.

**Never commit a broken render.** Run `quarto render article.qmd` before `git commit`.

---

## 8. AI hand-off conventions inside the manuscript

These markers tell the next session what to do:

```markdown
<!-- @claude: tighten the next paragraph; replace placeholder citation -->
<!-- @TODO-cite: add latency benchmark from InfluxData paper -->
<!-- gap: spec is silent on retry policy here; do not invent -->
```

Use Quarto cross-refs consistently: `{#sec-foo}`, `{#fig-bar}`, then refer with `@sec-foo`, `@fig-bar`. They survive renumbering.

There is (or should be) a `# Scratch` heading at the bottom of `article.qmd` for fragments that aren't ready to integrate. Don't promote scratch material into the body without human review.

---

## 9. Subagents available in this repo

Defined under `.claude/agents/`. Each is a focused worker with a constrained prompt and a single responsibility. Invoke them deliberately rather than asking the main session to do their job.

| Agent                          | When to invoke                                                                                       |
| :----------------------------- | :--------------------------------------------------------------------------------------------------- |
| `section-drafter`              | First-pass draft of a specific section, source-bound, gap-marking. Implements prompt template **T1**. |
| `reviewer-r2`                  | Independent MDPI reviewer-2 critique of a **finished section**. Implements prompt template **T2**.   |
| `reviewer-mdpi-full`           | Full-manuscript peer review against MDPI Energies A1 criteria, H3 spec audit, and P2 bib check.      |
| `bib-auditor`                  | Audit `bibliography.bib` for missing fields, duplicates, and orphan citations.                       |

The drafter and the reviewer must run in **separate sessions** (P-doc §2). A single session that both drafts and reviews its own draft will rubber-stamp itself.

---

## 10. Anti-hallucination discipline (H1–H3)

These are mandatory checks, not nice-to-haves:

- **H1 — Source-bound drafting.** Any drafting prompt must list the exact files the AI may draw from. If a fact is not in those files, the AI marks a gap and stops.
- **H2 — Reciprocal grep.** After every drafting pass, grep the manuscript for new `@key` citations and verify each one exists in `bibliography.bib` and resolves to a real publication. The `bib-auditor` subagent automates the first half.
- **H3 — Spec-vs-prose audit.** Before a section is marked done, compare its technical claims against `IoT_Data_Arch-JSON-MQTT.md` and report disagreements. Drift is a defect.

If you generate a claim you suspect is fabricated, append it to the `# Scratch` block with `<!-- suspect: needs verification -->` rather than leaving it in body prose.

---

## 11. Out of scope for this repo

To prevent agent scope-creep:

- **No code execution beyond Quarto render and trivial Python/grep helpers.** This is an article repo, not the system under study. The MING stack itself lives elsewhere.
- **No edits to the MDPI extension files.** They are vendored.
- **No new top-level directories** without human approval. The layout is intentional.
- **No external network calls** for citation harvesting unless a human explicitly requests it. Use what is in `bibliography.bib` and the `docs/` corpus.

---

## 12. Disclosure obligation

MDPI requires disclosure of substantive AI use. The `Acknowledgments` section of `article.qmd` will state that Claude was used for drafting, structural editing, figure source generation, and bibliography auditing, and that all technical claims, citations, and final wording were verified by the human authors. **Do not remove or weaken this disclosure.**

---

*End of brief. For deep context, read `docs/ai-first-art-writing-concept.md`. For per-section drafting plans, read `docs/Plan-for-art-writing/article_writing_plan.md`.*
