# How to Write This Article: Doc-to-Code Workflow Guide

---

## 1. The Mental Model

"Doc-to-code" means you treat your article exactly like a software project.

- The `.qmd` file is your **source code** — the single thing you actually edit.
- Quarto is your **compiler** — it reads the `.qmd` and produces a publication-ready MDPI PDF.
- Git is your **version control** — every meaningful writing session gets committed, so you can always roll back, compare drafts, or branch off to try a different argument structure.
- Your `docs/` folder is your **research database** — raw material you pull from, not something you edit.

The payoff: when you submit, you have a clean PDF produced automatically from plain text, a full history of every draft decision, and zero manual formatting work.

---

## 2. Your Repo Structure (What Goes Where)

```
01_Art-1_System-Archit/
│
├── 00_HOW-TO-WRITE-THIS-ARTICLE.md   ← this file
├── 01_Article-1_System-Architer-notes.md  ← your research compass (keep updating)
├── 02_SciSpace-stratagy.md           ← journal targeting notes
├── 03_MDPI-Energies.md               ← section fit analysis
│
├── docs/
│   └── 01-Article-1-Architecture-MING_stack-Scispace/
│       ├── cps_ming_insights.md      ← your main literature synthesis (GOLD)
│       ├── CPS_MING_Renewable_...Survey.md
│       ├── *.csv                     ← raw SciSpace/arXiv exports
│       └── paper_table_*.csv         ← architectural comparison tables
│
└── ihrke-template/                   ← YOUR WRITING LIVES HERE
    ├── ihrke-template.qmd            ← THE article source file (rename this)
    ├── bibliography.bib              ← all references go here
    └── _extensions/ihrke/mdpi/      ← MDPI formatting engine (don't touch)
```

**Rule of thumb:** everything outside `ihrke-template/` is input material. Everything inside it is your output machine.

---

## 3. First-Time Setup (Do This Once)

### Rename the template to your article
Rename `ihrke-template.qmd` → `article.qmd` (or a short slug like `ming-pipeline.qmd`). This makes git diffs cleaner and avoids confusion.

### Update the YAML front matter
Open `article.qmd` and replace the placeholder metadata at the top:

```yaml
---
title: "Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems"
runningtitle: MING RES Learning Factory
mdpi_journal: energies          # change from behavsci
article_type: article
article_status: submit

author:
  - name: Viktar Taustyha        # your name
    corresponding: true
    email: taustyka.viktar@gmail.com
    role:
      - Conceptualization
      - Writing - original draft
    affiliations:
      - name: "Your Institution"
        city: Your City
        country: Your Country

abstract: |
  (write last)

keywords: [MING stack, CPS, learning factory, renewable energy, telemetry, edge-to-cloud]
bibliography: bibliography.bib
---
```

### Set the target journal
In `03_MDPI-Energies.md` you already identified **Section A1: Smart Grids and Microgrids** as the best fit. Set `mdpi_journal: energies` in the YAML.

---

## 4. The Daily Writing Loop

This is the core rhythm. Each session follows the same four steps:

### Step 1 — Pull (if collaborating)
```bash
git pull origin main
```

### Step 2 — Write in the `.qmd` file
Write one section at a time in plain Markdown. Add citations using the `@key` syntax — they auto-render into the MDPI reference format. Example:

```markdown
The MING stack has been validated in on-premises IIoT deployments
where Node-RED acts as a protocol adapter at the edge layer [@key2024].
```

### Step 3 — Compile to PDF (spot-check your work)
```bash
cd ihrke-template
quarto render article.qmd
```
This produces `article.pdf` in MDPI format. Open it to check layout, figure placement, and reference formatting. You do **not** need to do this after every paragraph — once per session is enough.

### Step 4 — Commit with a meaningful message
```bash
git add .
git commit -m "C3-draft: Section 2 Literature Review — CPS layers"
git push origin main
```

Use a consistent commit naming convention. Suggested prefix system:
- `C0-` / `C1-` — setup commits (already done)
- `Cx-draft:` — new prose added
- `Cx-rev:` — revision of existing prose
- `Cx-ref:` — bibliography/reference work
- `Cx-fig:` — figures added or changed

---

## 5. How to Use Your Existing Research Material

You already have high-quality synthesized material. Don't start from a blank page — mine it.

**`cps_ming_insights.md`** is your richest asset. It contains a fully synthesized literature review organized into the exact sections you need: CPS layers, MING component mapping, sensor integration, orchestration, benchmarks. When writing Section 2, open this file alongside your `.qmd` and pull arguments directly from it, rewriting in your own voice.

**`paper_table_architectural_*.csv`** files contain extracted tables from surveyed papers. These are ready-made data for a comparison table in your Related Work or Results section. Load them in a spreadsheet, merge/clean, then format as a Markdown table in the `.qmd`.

**`combined_cps_renewable_learning_factory_final.csv`** is your full paper corpus. Use it to report your literature screening process in the Methodology section (e.g., "X papers were identified from SciSpace and arXiv, of which Y were selected based on...").

---

## 6. Reference Management (bibliography.bib)

All citations go into `ihrke-template/bibliography.bib` in BibTeX format. The fastest workflow:

1. Find a paper in Google Scholar or SciSpace.
2. Click "Cite" → "BibTeX" → copy the entry.
3. Paste it into `bibliography.bib` and give it a clean key (e.g., `author2024keyword`).
4. Use `@author2024keyword` in the `.qmd`.

Quarto handles everything else — numbering, formatting, the reference list at the end.

---

## 7. Article Structure to Write Toward

Based on your research question and the MDPI Energies format, your sections should be:

1. **Introduction** — the problem (heterogeneous data in RES labs), the gap, your contribution
2. **Related Work** — CPS reference architectures, MING stack deployments, learning factories
3. **System Architecture** — your proposed MING+React pipeline design (the core contribution)
4. **Canonical Data Model** — how you normalize Engine Bench vs. Algae Photobioreactor data
5. **Validation / Results** — simulated JSON payload comparison, pre-validation logic
6. **Discussion** — scalability, edge cases, comparison to existing approaches
7. **Conclusions** — summary, limitations, future work

---

## 8. Efficient Writing Tips for This Workflow

**Write sections out of order.** Start with Section 3 (Architecture) — it's the most concrete and will anchor everything else. Introduction and Abstract come last.

**Keep a scratch section at the bottom of the `.qmd`.** Add a `# Scratch` heading at the end where you dump ideas, half-formed arguments, and quotes from papers. Move polished content up into proper sections.

**One commit = one section or one clear revision.** Never commit a half-finished thought mid-paragraph. Commit when a section is at a stable state, even if rough.

**Use Quarto cross-references.** Label figures and tables so you can refer to them by label, not by number — Quarto auto-numbers everything:
```markdown
![MING Stack Architecture](figs/ming-architecture.png){#fig-ming}

As shown in @fig-ming, the pipeline...
```

**Track open questions inline.** Use a consistent marker for things to resolve later:
```markdown
<!-- TODO: add latency benchmark from InfluxData paper -->
```

---

## 9. Your Next Three Actions

1. Rename `ihrke-template.qmd` → `article.qmd` and update the YAML front matter with your real metadata.
2. Copy your 7-section outline into the `.qmd` as empty headings with one-line placeholder descriptions.
3. Commit: `C2-structure: article scaffold with section headings`

After that, you're writing — not setting up.
