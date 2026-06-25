# AI use disclosure — MDPI rules + our text

MDPI requires disclosure of substantive GenAI use. **Superficial editing** (grammar, spelling, punctuation, formatting) does not need disclosure. Anything more does.

## What MDPI requires

1. **GenAI tools cannot be listed as authors.** Period. (`article.qmd` author list must contain only humans.)
2. If GenAI was used to **generate text, data, or graphics**, or to **assist in study design, data collection, analysis, or interpretation**, this must be disclosed in **two places**:
   - **Methods section** — with concrete description of how it was used.
   - **Acknowledgments section** — using MDPI's required wording (below).
3. The standard Acknowledgments wording (verbatim from MDPI):

> During the preparation of this manuscript/study, the author(s) used [tool name, version information] for the purposes of [description of use]. The authors have reviewed and edited the output and take full responsibility for the content of this publication.

## Our actual use (must match what is in the manuscript)

Tool: **Claude (Anthropic)** — versions across the drafting period:
- Claude Sonnet 4.x (April–May 2026): section drafting, prose refactoring.
- Claude Opus 4.x (May 2026): bibliography auditing, MDPI reviewer-style critique, publishing scaffold.

Uses to disclose:
- Drafting prose under tight source-binding (per `docs/ai-first-art-writing-concept.md`).
- Structural editing of sections.
- Figure-source generation (e.g. mermaid → SVG → PDF figures in `pics/`).
- Bibliography auditing via the `bib-auditor` subagent.
- Internal "reviewer-2" critique via the `reviewer-r2` and `reviewer-mdpi-full` subagents.

Uses **not** disclosed (because superficial):
- Spell-check, grammar tightening, punctuation.

## Exact text to paste into `article.qmd`

### In Methods (after methodology subsections, before Results)

> **Use of generative AI.** During the preparation of this manuscript, the authors used Anthropic Claude (Sonnet 4.x and Opus 4.x) for source-bound section drafting, structural editing, figure-source generation, and bibliography auditing, under the workflow documented in the project repository. All technical claims about the KIOZE Edu-Bad architecture were independently verified against the system specification document. All citations were independently verified against the cited sources. The authors reviewed and edited every AI output and take full responsibility for the content of this publication.

### In Acknowledgments

> During the preparation of this manuscript, the authors used Anthropic Claude (Sonnet 4.x and Opus 4.x) for the purposes of source-bound section drafting, structural editing, figure-source generation, and bibliography auditing. The authors have reviewed and edited the output and take full responsibility for the content of this publication.

## Verification before submission

- [x] Both blocks above appear verbatim in `ihrke-template/article.qmd`. ✅ 2026-05-28 — Methods block at end of §5.1; Acknowledgments block in YAML `acknowledgments:`
- [x] No GenAI tool is listed as an author or contributor in the front matter. ✅ 2026-05-28 — author list contains only V.T. and K.G.M.K.
- [x] The CRediT statement (`02_pre-submission/author-contributions-credit.md`) attributes "Writing — Original Draft" to humans, not AI. ✅ 2026-05-28 — "Writing — Original Draft Preparation, V.T. and K.G.M.K."
