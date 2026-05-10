# AI-First Article Writing — Concept and Workflow

This document formalises the *AI-first* working method I (Viktar) use to author the MDPI *Energies* manuscript on the KIOZE Edu-Bad architecture. It is a methodological companion to `article_writing_plan.md`. Where the plan answers *what* we will write and *when*, this document answers *how* we will write it — and what role human and AI co-authors play at each step.

The AI-first attitude does **not** mean the AI writes the paper. It means every stage of the pipeline — research, drafting, editing, code, configuration, figures, reference management — is designed around tight human-AI loops that exploit AI's strengths (synthesis, formatting, code generation, consistency checks) while preserving full human authorial responsibility for argument, evidence, and final wording.

---

## Table of Contents

1. [Principles](#1-principles)
2. [Author Roles and Responsibilities](#2-author-roles-and-responsibilities)
3. [Tech Stack](#3-tech-stack)
4. [Repository as the Single Source of Truth](#4-repository-as-the-single-source-of-truth)
5. [The AI-First Writing Loop](#5-the-ai-first-writing-loop)
6. [Drafting with AI](#6-drafting-with-ai)
7. [Editing and Revision with AI](#7-editing-and-revision-with-ai)
8. [Code, Configuration, and Schema Generation with AI](#8-code-configuration-and-schema-generation-with-ai)
9. [Figures and Diagrams with AI](#9-figures-and-diagrams-with-ai)
10. [Bibliography and Citation Hygiene with AI](#10-bibliography-and-citation-hygiene-with-ai)
11. [Markdown / Quarto File Management](#11-markdown--quarto-file-management)
12. [Prompt Templates](#12-prompt-templates)
13. [Verification and Anti-Hallucination Discipline](#13-verification-and-anti-hallucination-discipline)
14. [Ethics, Disclosure, and MDPI Policy Alignment](#14-ethics-disclosure-and-mdpi-policy-alignment)

---

## 1. Principles

The workflow rests on five non-negotiable principles.

**P1 — Human authorship is final.** The AI drafts, suggests, refactors, and checks; the humans (Viktar, Kelvyn) decide what is published. Every paragraph that ships is read, understood, and editorially approved by a human author.

**P2 — Source-grounded prose only.** No claim enters the manuscript without a traceable source: a peer-reviewed reference, a primary specification (`IoT_Data_Arch-JSON-MQTT.md`), an actual configuration file, or a recorded experimental observation. AI is never asked to "invent plausible facts."

**P3 — Doc-to-code discipline.** The manuscript is treated like software: plain-text source (`.qmd` / `.md` / `.bib`), version control (git), reproducible build (Quarto + MDPI extension), automated rendering, and structured commit messages — exactly as documented in `00_HOW-TO-WRITE-THIS-ARTICLE.md`.

**P4 — AI is a collaborator on the workspace, not on a paste board.** AI tools operate directly on the repository — reading the actual files, editing the actual `.qmd`, generating diagrams that land in `ihrke-template/pics/` — instead of producing fragments in chat windows that humans then re-paste. The repository is the workspace; the chat is the reasoning layer.

**P5 — Verifiable over fluent.** Where AI fluency conflicts with verifiable correctness, correctness wins. We accept clunkier prose if it is faithful to the spec; we never accept smooth prose that overstates the implementation.

## 2. Author Roles and Responsibilities

| Actor                                    | Role                                               | Responsibilities                                                                                                |
| :--------------------------------------- | :------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| **Viktar (senior author)**               | Architect of method and argument                   | Sets research question, approves outline, owns framing, performs final editorial pass, signs submission.        |
| **Kelvyn (co-author / student)**         | Implementation and primary drafter                 | The first draft.                                                                                                |
| **AI assistant (Claude in Cowork mode)** | Reasoning, drafting, refactoring, checking partner | Executes the loops described below; never makes irreversible decisions; surfaces uncertainty explicitly.        |
| **Reviewer-style AI (separate session)** | Independent critique                               | Spawned as a second-opinion pass with no memory of the drafting session, briefed only on the draft + checklist. |

The two AI roles are intentionally separated: the *drafting* assistant tends to confirm its own framings, so a *reviewer* assistant is invoked from a clean context to challenge them.

## 3. Tech Stack

The full toolchain we standardise on for this article — chosen because every component is text-first, scriptable, and AI-operable.

| Layer | Tool | Role |
| :---- | :---- | :---- |
| **Authoring** | Quarto (`.qmd`) | Source format; one file = one article |
| | Markdown (`.md`) | All planning, notes, and supporting docs |
| | MDPI LaTeX class (`mdpi.cls`) | Final typesetting via Quarto extension `ihrke/mdpi` |
| **Build** | Quarto CLI | `quarto render article.qmd` → MDPI-formatted PDF |
| | LaTeX (TinyTeX / TeX Live) | PDF compilation |
| | Pandoc (bundled with Quarto) | Markdown ↔ LaTeX conversion |
| **Version control** | Git | Local + remote; per-section commits |
| | GitHub / GitLab | Remote, shared between Viktar and Kelvyn |
| **Bibliography** | BibTeX (`bibliography.bib`) | Single bib file; `@key` citations in `.qmd` |
| | Zotero (optional) | For BibTeX export of harvested literature |
| | SciSpace, arXiv | Literature discovery (CSV exports already in repo) |
| **AI assistant** | Claude (Cowork mode) | Primary drafting, editing, code generation, repo-aware operations |
| | Claude API / Sonnet | Long-context synthesis and reviewer-style critique |
| **Code & config** | Docker Compose | Architecture under study; reproducible MVP |
| | Node-RED flows (`*.json`) | Subject of §3 in the article |
| | InfluxDB 2.x, Mosquitto, Grafana | Components of the MING stack (subject) |
| | Python (occasional) | Quick payload-comparison scripts; figure generation |
| **Diagrams** | Mermaid (in `.qmd`) | First-pass architecture flowcharts |
| | Excalidraw / draw.io | Hand-shaped architecture diagrams, exported SVG |
| | TikZ (LaTeX) | Final journal-grade figures when full vector control needed |
| | PlantUML | Sequence/component diagrams |
| | Inkscape | SVG cleanup and PDF export |
| **Quality** | Grammarly | Sentence-level grammar |
| | LanguageTool | Style and false-positive cross-check |
| | Claude editorial pass | Argument-level critique |
| **Project mgmt** | Markdown-based plan files (this folder) | All planning lives in repo; no external trackers |

Everything in this table is text-first and reproducible. There is no proprietary `.docx` or vendor cloud locking the manuscript away from version control.

## 4. Repository as the Single Source of Truth

The article repository (`01_Art-1_System-Archit/`) is the *only* place where article state lives. The mental model:

- **`ihrke-template/article.qmd`** — the article. Single file. Authoritative.
- **`ihrke-template/bibliography.bib`** — every cited reference, ever.
- **`ihrke-template/pics/`** — every figure, in the format that ships.
- **`docs/`** — research substrate (SciSpace exports, the architecture spec, literature insights).
- **`docs/Plan-for-art-writing/`** — meta layer: this concept doc, the writing plan, correspondence drafts.

If something is not in the repo, it does not exist for the purposes of this article. AI assistants read and write *into the repo*; we never tolerate "the latest draft is in the chat."

## 5. The AI-First Writing Loop

Every drafting session follows the same six-step loop. It is an explicit ritual, not implicit habit, because explicit rituals are AI-promptable.

```
1. SCOPE     Decide one section or one paragraph cluster as the unit of work.
2. GROUND    Re-read the source material (spec, insights, prior section) into the AI context.
3. DRAFT     Ask the AI to produce candidate prose with explicit constraints
             (length, tone, citation skeleton, no invented facts).
4. EDIT      Human reads, marks weak claims, marks places needing citations,
             corrects framing. AI rewrites against the marked-up version.
5. RENDER    `quarto render` to confirm the LaTeX compiles and the section
             reads in MDPI layout, not just in markdown preview.
6. COMMIT    `Cx-draft:` or `Cx-rev:` commit with a message describing
             what changed and why.
```

Steps 1, 2, 4 are predominantly human; steps 3, 5, 6 can be AI-executed but are human-supervised. The render step is non-negotiable: an unrendered draft is not a draft.

## 6. Drafting with AI

Drafting prompts are constrained, never open-ended.

**Constrained drafting prompt skeleton:**
> *"Draft Section X.Y of the manuscript. Use only the following sources: \[paths]. Target ~N words. Cite using `@key` placeholders where a citation is needed; mark each placeholder with `@TODO-cite` and a short note about what to cite. Do not invent technical claims; if the source is silent on a point, leave a `<!-- gap -->` HTML comment in place rather than fabricate."*

The two non-obvious clauses — *only the following sources* and *leave a gap rather than fabricate* — are the spine of the practice. They convert the AI from a generative engine into a controlled rewriter.

The first draft is always rough. It is meant to give the human a structured object to react to, not a finished section.

## 7. Editing and Revision with AI

Editing happens in three distinguishable passes, each with its own prompt style.

**Pass 1 — Structural edit.** "Read this section. Identify any paragraph that does not advance the argument stated in the topic sentence, any claim that lacks a source, any acronym that is used before being expanded, any sentence longer than 35 words." The AI returns a numbered list of issues; the human approves the fix list before any rewriting.

**Pass 2 — Sentence-level edit.** Grammarly + LanguageTool first (mechanical), then a Claude pass for clarity and rhythm: "Tighten without changing meaning; do not introduce new claims; preserve all citations exactly."

**Pass 3 — Editorial critique (reviewer-style).** A fresh AI session with no drafting history is given the section plus a critique brief: *"You are MDPI reviewer 2. Find three weaknesses in this section that an actual reviewer would flag."* This is the cheapest way to catch the failure mode of *plausible-but-shallow* AI prose.

## 8. Code, Configuration, and Schema Generation with AI

The article is *about* code and configuration (Node-RED flows, MQTT topics, JSON CDM, docker-compose). AI is helpful here because the artefacts are syntactically rigid.

We use AI to:

- Generate **payload diff scripts** (Python) that produce the comparison data backing Figure 5 / Table in §5.
- Validate that the **JSON examples** in the manuscript parse and conform to the CDM described in the spec — by asking AI to round-trip a JSON sample through a Python schema check before it is pasted into `article.qmd`.
- Generate **mermaid / plantuml** diagram source from the spec ASCII art for §3 figures.
- Refactor **docker-compose snippets** into the shorter forms that fit a journal column.
- Surface **internal inconsistencies** between the spec, the qmd, and the running flows — by asking AI to read all three and report disagreements.

In every case the rule of P5 holds: AI may generate, but the human runs the artefact (renders the diagram, executes the script, parses the JSON) before it lands in the manuscript.

## 9. Figures and Diagrams with AI

Figure quality is one of the most common revision triggers in MDPI reviews. We use a tiered diagram pipeline that maximises AI participation while preserving journal quality.

**Tier 1 — Mermaid in `.qmd`.** First-pass diagrams written as Mermaid blocks directly inside the manuscript source. AI-generated from spec text in seconds. Used during drafting and internal review only.

**Tier 2 — Excalidraw or draw.io SVG.** Hand-shaped intermediate diagrams when the layout matters. AI helps generate the underlying structure (nodes, edges, labels) as JSON / XML, which is then opened in the editor for visual refinement. SVG is the export format.

**Tier 3 — TikZ or polished SVG → PDF.** Final journal figures. TikZ is preferred for figures that must match the body-text font and line widths exactly; SVG is preferred for component / topology diagrams. AI generates the TikZ source from a verbal specification; human compiles, inspects, iterates.
	[Ti_k_Z](https://en.wikipedia.org/wiki/PGF/TikZ) is probably the most complex and powerful tool to create graphic elements in LaTeX.

**Tier 4 — Real screenshots (Grafana, Node-RED).** Captured at high resolution, post-processed in Inkscape to crop, anonymise, and replace browser chrome with clean borders. AI is *not* used to alter the captured images — that would be a research-integrity violation.

For all tiers, the deliverable in the repo is: (a) the source (Mermaid / SVG / TikZ / PNG), (b) the rendered PDF, and (c) the figure caption written as a self-contained paragraph.

Constraints we enforce on every figure regardless of tier:

- Vector format (PDF or SVG) preferred; PNG only at ≥300 DPI for screenshots.
- Same font family as the body text (Charter or the MDPI default).
- Monochrome-readable: never rely on colour alone to convey meaning.
- ≤300 dpi raster fallback when vector is impossible.
- Caption is a paragraph, not a label; it states what the figure shows *and* what conclusion the reader should draw.

## 10. Bibliography and Citation Hygiene with AI

`bibliography.bib` is treated like code: linted, sorted, deduplicated. AI helps maintain it.

Workflow:

1. Harvest candidate references from SciSpace / arXiv / Google Scholar.
2. Paste BibTeX into `bibliography.bib` with a key that follows the convention `firstauthorYEARkeyword` (e.g., `lim2020digital`).
3. Ask AI: *"Audit this `.bib` for missing fields (DOI, year, journal), duplicate entries, and inconsistent key formats. Report only; do not edit yet."*
4. Apply the fixes manually or via a confirmed AI edit pass.
5. Ask AI to grep `article.qmd` for `@key` references and report any keys cited but not in the bib (or vice versa).

This catches the most common Quarto build failures (missing keys, malformed entries) before the render step.

## 11. Markdown / Quarto File Management

The plain-text discipline is what makes the AI-first loop possible. Concrete file-management rules:

- One section per logical commit. Never mix structural and prose changes in one commit.
- Use HTML comments for AI hand-off notes: `<!-- @claude: tighten the next paragraph; replace placeholder citation -->`.
- Use Quarto cross-refs (`{#sec-foo}`, `{#fig-bar}`, `@sec-foo`, `@fig-bar`) consistently — they survive renumbering and section moves.
- Keep a `# Scratch` heading at the bottom of `article.qmd` as the dumping ground for fragments AI generates that aren't ready to integrate.
- Run `quarto render` before every commit. A broken render is a broken commit.

## 12. Prompt Templates

We standardise three reusable prompt templates so quality is reproducible across sessions.

**T1 — Section drafting:**
> *"Acting as an MDPI Energies senior author, draft `Section X.Y` of `article.qmd`. Source material: \[list paths]. Target ~N words. MDPI style: numbered, IMRaD discipline, no first-person plural in Methods. Cite every empirical claim with a `@key` placeholder; mark gaps as `<!-- @TODO-cite: ... -->`. Do not invent technical details. Output only the section text, no commentary."*

**T2 — Editorial critique:**
> *"You are MDPI reviewer 2 reading `Section X` for the first time. Identify (a) the three weakest empirical claims; (b) any acronyms used before expansion; (c) any place where the description of the implementation contradicts `IoT_Data_Arch-JSON-MQTT.md`; (d) any figure referenced but not described. Be terse and specific."*

**T3 — Diagram generation:**
> *"Convert the architecture description in §X of `IoT_Data_Arch-JSON-MQTT.md` into Mermaid diagram source. Components must use the canonical names from the spec. Output only the Mermaid block."*

These templates live in this document so any author (or any AI session) can reuse them without reinventing the prompt.

## 13. Verification and Anti-Hallucination Discipline

The single largest risk of AI-first writing is the hallucinated citation, the invented benchmark, or the smoothed-over implementation gap. We mitigate with three habits.

**H1 — Source-bound drafting.** Drafting prompts always restrict source material to listed files (P2).

**H2 — Reciprocal grep.** After every drafting session, the human greps the manuscript for new `@key` citations and verifies each exists in `bibliography.bib` and corresponds to a real, accessible publication.

**H3 — Spec-vs-prose audit.** Before each section is marked done, an AI session is asked specifically to compare the section's technical claims against `IoT_Data_Arch-JSON-MQTT.md` and report disagreements. This catches drift between aspirational prose and the actual MVP.

We also keep a running `# Scratch` block of any AI-generated claim we *suspect* is fabricated, so we can later confirm or remove it.

## 14. Ethics, Disclosure, and MDPI Policy Alignment

MDPI requires authors to disclose substantive use of generative AI. We will:

- Acknowledge AI assistance in the *Acknowledgments* section (e.g., *"The authors used Claude (Anthropic) for drafting assistance, structural editing, figure source generation, and bibliography auditing. All technical claims, citations, and final wording were reviewed and verified by the authors."*).
- Not list the AI as an author. Authorship requires accountability AI cannot bear.
- Retain in the repository every prompt-and-response interaction that materially shaped a section — so that, if asked, we can demonstrate the human-AI process honestly.
- Keep all empirical numbers (latencies, payload sizes, container counts) traceable to the spec or a real measurement, never to AI generation.

The final responsibility for every word in the submitted manuscript rests with the human authors.

---

*End of concept.*
