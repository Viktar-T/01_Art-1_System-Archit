# Round 1 — Action Plan

> **The decision is settled: we proceed with a Major Revision.** This document is the *action plan* for round 1 — what to do, in what order, and the two risks to watch while doing it. The underlying go/no-go reasoning is retained below (§2–§5) as the rationale, but the operative content is the prioritised work in **§6**.
>
> Inputs: `article.qmd`, `reviewer-1/2/3-comments.md`, the editorial-office e-mail (`comms/editorial-office/2026-06-16-leroy-liu_round-01-review-report-and-reference-issues.md`), `revision-plan.md`. All three reviews are in; the academic editor has **not** yet issued a formal decision, and the per-reviewer accept/minor/major/reject recommendations are **not** in our transcripts (only the quality-form ratings are).
>
> **Updated 2026-06-25:** reconciled with the editorial-office e-mail in `comms/editorial-office/` (see §0); reframed from a go/no-go memo into the round-1 action plan — the conclusion to proceed is unchanged, the emphasis is now on execution.

---

## 0. Editorial status — what the editor has actually said (`comms/editorial-office/2026-06-16-leroy-liu_round-01-review-report-and-reference-issues.md`)

The only editorial communication on file is an **interim progress e-mail** (logged **2026-06-16**) from **Leroy Liu (Assistant Editor, leroy.liu@mdpi.com)** on manuscript **energies-4374418** — **not** the formal decision letter:

- It transmitted **Reviewer 1's report early** and explicitly asked us to **"start to revise your paper if possible."**
- **No verdict** (accept / major / minor / reject) and **no revision deadline** have been issued; the academic editor decides once all reports are in.
- The office's **technical check** flagged reference defects — **Ref 5** author, **Ref 11** DOI, **Refs 12 & 15** conference names — and asked us to re-check **all** references. These are **editorial-office requirements**, not merely reviewer asks (tracked Tier 0 / EO.1–EO.4).
- **Timing caveat (do not over-read the friendly tone):** the 16 Jun e-mail was written when **only Reviewer 1** had returned — it predates **Reviewer 3** (review dated 21 Jun) and roughly coincides with Reviewer 2 (9 Jun). So the editor's encouraging "start revising" posture reflects the **warm Reviewer 1 alone**, *not* a judgement that already absorbs the harsher R3. The decisive signal — the editor weighing R3 — is still ahead.

**Implications for this memo (recommendation unchanged, now better grounded):**
1. The editor has effectively **green-lit starting the decision-independent revision now** (Themes A–E) → proceed.
2. The **binding uncertainty — how hard the editor weights R3.1 — is still open**, because the formal decision has not been issued → continue to **hold the rebuttal wording and resubmission** until it arrives.

---

## 1. Decision & immediate next action

**Decision: proceed — commit to a Major Revision.** Nothing in the three reports is a hard reject, and the single genuinely dangerous comment (Reviewer 3.1, "lacks theoretical depth") is a **journal-fit / framing argument, not a fixable defect we are failing to fix**. For MDPI *Energies* — an applied energy-systems journal that routinely publishes monitoring-architecture and open-source SCADA papers — that argument is rebuttable on scope grounds. The cost is real (it is a major revision, and two of the asks we cannot fully satisfy this round), but submitting a strong revision clearly beats withdrawing.

**Start now (do not wait for the formal decision):** the editor explicitly invited early revision, so begin the decision-independent work in **§6** immediately — Tier 0 integrity fixes, Tier 1 visuals, Tier 2 more results. **Hold only** the rebuttal wording and resubmission until the formal first decision lands, because the tone on R3.1 must match what the editor actually says.

**Confidence:** medium-high that a competent revision survives to a second round; lower that it is accepted without a second major-revision cycle. The binding uncertainty is the editor's synthesis of R3, which we cannot see yet.

---

## 2. Severity read, reviewer by reviewer

| Reviewer | Form signal | Tone | Verdict |
|---|---|---|---|
| **R1** | English fine; mostly "can be improved", 2× "must be improved" (results, figures) | Constructive, specific, explicitly likes the title/proposal | **Minor–Major. Friendly.** All 14 points accepted; visuals + more results are the price of admission. |
| **R2** | English "could be improved"; **all six dimensions "can be improved"** | Terse but fair; no scope attack | **Major, survivable.** 5 points; one hard (physical validation), rest are writing/stats/figure fixes. |
| **R3** | English fine; **design, methods, results, figures all "must be improved"** | Dismissive on novelty | **Major, hostile.** 3 points; one is an existential framing attack (R3.1). This is the report the decision hinges on. |

Crucially, **R1 and R2 are not asking for different work than we already planned** — they converge on the same two themes (visual proof of implementation, more/longer results). R3 is the outlier.

---

## 3. The critical issues we *cannot* simply "fix"

Be honest about the two things that are not closable by better writing alone. These are the real reasons to deliberate.

### CRIT-1 — "Lacks the theoretical depth required for academic research" (R3.1) — *the only near-existential comment*
The reviewer says we propose **no new compression algorithm, no edge-scheduling theory, no new network protocol**. This is **true and unfixable by design**: the contribution is a systems-integration architecture (CDM translation layer + edge null-pruning + MING+React orchestration), not a new algorithm. P2 forbids us from inventing a theoretical kernel we do not have.

- **Why it is not fatal:** This is a category objection, not a quality defect. *Energies* and *Sensors* publish exactly this class of paper (the reviewer-1-suggested DOIs — `s24248074`, `en16052092` — are themselves open-source SCADA/IIoT *implementation* papers in MDPI journals). The standard for an applied architecture paper is *reproducibility, soundness, and demonstrated feasibility*, not theoretical novelty.
- **What we can actually do:** Reframe and *sharpen the contribution claim* (we already have C1–C3). Lead with the engineering-contribution framing explicitly in the abstract and intro; cite comparable accepted applied papers to establish the genre; do **not** pretend to a theory we don't have.
- **Residual risk:** If the academic editor personally weights "theoretical novelty" heavily, no rebuttal saves it. This is the one scenario where we would re-target the venue rather than keep revising — but it is the editor's call, not the reviewer's, and *Energies*' scope is on our side.

### CRIT-2 — Validation is simulation-only / loopback-only (R2.2, R3.3, and the deep half of R1.14)
Three reviewers circle the same hole from different angles:
- R2.2: "add experiments with physical devices or real multi-vector energy system data."
- R3.3: low-latency/scalability claims "not compared and validated with established mature methods."
- R1.14: "misses more results of the conducted simulations."

- **What we cannot do this round:** Stand up the physical KIOZE rig and produce real-hardware multi-vector telemetry, or run a controlled head-to-head benchmark against a "mature" commercial SCADA stack. That is out of scope for this article (per `CLAUDE.md`: the MING stack/rig lives elsewhere; this repo is architecture + sim MVP) and likely not available on the revision clock.
- **What we *can* do (and it is substantial):** (a) Expand the simulation results — longer runs, more vectors plotted, latency distributions, concurrency sweeps — which fully answers R1.14 and most of R2.3; (b) **temper the absolute claims** ("100% integrity", "low latency") into bounded, simulation-qualified statements with stated N and variance; (c) add a *qualitative* comparison table against published open-source SCADA stacks (R3.3) using literature figures rather than a same-bench benchmark; (d) the manuscript **already discloses** loopback-only honestly (§Limitations, §Conclusions) — strengthen and consolidate that.
- **Residual risk:** R2/R3 may insist on physical data in round 2. Our defence is scope: this is the *architecture* paper; physical validation is the explicitly-stated next paper. That defence is credible only if we (i) frame it up front and (ii) do not overclaim.

> Everything else across the three reports is genuinely solvable and mostly already on the plan (visuals, abbreviations, keyword, §5.1 rename, merge limitations, Fig. 3 label bug, reference fixes, impedance-mismatch citations).

---

## 4. "Is Reviewer 3 unsolvable?" — direct answer

**No — but it is the report we must respect, not dismiss.** Decompose it:

| Point | Solvable? | How |
|---|---|---|
| **R3.1** lacks theoretical depth | **Not by adding theory** — solvable only by *reframing* as an applied-systems contribution + journal-fit defence | Sharpen C1–C3; cite peer applied papers; refuse to fabricate theory (P2). |
| **R3.2** "impedance mismatch" needs support | **Yes** | Add 1–2 paragraphs + citations grounding the metaphor (multi-time-scale / multi-rate sensor fusion literature). Currently the term is asserted, leaning on `@balogh2023digitaltwins` only — this is a legitimate weak spot. |
| **R3.3** claims not compared to mature methods | **Partially** | Qualitative comparison table from literature + tempered claims. A true benchmark is out of scope. |

So R3 is **2 of 3 solvable** and the third is a defensible framing fight, not a wall. The danger is not any single point — it is that R3's "must be improved ×4" signals a reviewer leaning **reject/major**, and if the editor defers to the harshest reviewer we get a major-revision-then-reject trajectory. That is a *probability* cost, not a certainty.

---

## 5. Why we proceed — and the two watch-outs

**Reasons to proceed (dominant):**
1. No explicit reject in any report; R1 is warm, R2 is neutral-fair.
2. The expensive asks (R1.10/R1.11 visuals, R1.14/R2.3 more results) are **producible** — we have a real, open-sourced implementation (GitHub + Zenodo DOI) and can screenshot Grafana/Node-RED and re-run longer sims today.
3. The two "cannot fix" items are both *scope/framing* issues with credible, honest defences — not data we faked or claims we cannot support.
4. Sunk position is favourable: manuscript ID assigned, APC funded, honest gap disclosure already in the text, AI-use disclosure compliant.
5. The editorial office has **explicitly invited early revision** ("start to revise your paper if possible"), so the decision-independent work (Themes A–E) cannot be wasted and shortens the revision clock.

**Watch-outs that would change the plan (escalate / re-target rather than keep grinding):**
1. Editor's decision letter foregrounds R3.1 "not enough novelty for the journal" → reconsider target (e.g., transfer to a more applied/implementation venue) rather than burn a revision cycle.
2. A reviewer makes physical-hardware validation a **hard precondition** for round 2 → we cannot meet it this round; negotiate scope or plan a longer timeline.

**Operating rule:** Execute the Major Revision **now** on everything that is independent of the editor's framing call (Themes A–E / §6 below), but **hold the rebuttal letter and resubmission** until the formal first decision arrives (consistent with current STATUS.md), because the rebuttal's tone on R3.1 must be calibrated to whatever the editor actually says.

---

## 6. What should be done — prioritised action plan

Ordered by leverage. R-IDs map to `reviewer-*-comments.md` and `revision-plan.md`.

### Tier 0 — Trivial integrity fixes (do first; cheap credibility)
- **R2.4** Fix Figure 3 label/caption mismatch (plot says *engine speed*, caption says *normalized active power*). This is an embarrassing inconsistency a hostile reviewer will weaponise — fix immediately.
- **EO.1–EO.4 + full reference re-audit** (Ref 5 author, Ref 11 DOI, Refs 12/15 conference names) — **editorial-office technical-check requirement, mandatory** — and **R1.7** broken ref at line 125 / Zenodo `[?]`. Run `bib-auditor`.
- **R1.1** add "open-source" keyword; **R1.2** expand SCADA/JSON/etc. at first use; **R1.8** rename §5.1 away from "experimental setup"; **R1.13/R2.5** merge the two limitations blocks and reflect loopback/latency/packet-loss/scalability limits in the Conclusions.

### Tier 1 — Acceptance-critical: prove the implementation visually (R1.10, R1.11, R1.6)
- Add **Grafana dashboard screenshots** (R1.11 — R1 ties the "successful implementation" claim to this; treat as mandatory).
- Add **Node-RED flow screenshot** of interconnected nodes (R1.10).
- Add a **data-flow / network block diagram** beyond Fig. 2 (R1.6).
- Add **compute environment** (CPU/RAM/OS) to the renamed §5.1 (R1.9).

### Tier 2 — More & deeper results (R1.14, R2.3)
- Extend simulation reporting: longer-duration and larger-scale runs, latency distributions/percentiles already partly present, concurrency sweep, more of the 12 vectors plotted.
- **Re-cast absolute claims** ("100% integrity", "100% null-pruning") as N-qualified, simulation-scoped results with variance and explicit scope ("under simulated conditions, N=…"). This simultaneously answers R2.3 and pre-empts R3.3.

### Tier 3 — Positioning & novelty defence (R2.1, R3.1, R3.2, R1.3, R1.4, R1.5, R1.12)
- **R3.1 / R2.1:** Add an explicit "Contribution & scope" framing in the intro: state plainly that this is an applied systems-architecture contribution (not a new algorithm), and cite comparable accepted applied papers — including the two R1-suggested MDPI DOIs (`10.3390/s24248074`, `10.3390/en16052092`) — to anchor the genre.
- **R3.2:** Ground the "impedance mismatch" framing with multi-rate/multi-time-scale sensor-fusion literature (1–2 paragraphs + citations); stop leaning on a single digital-twin cite.
- **R1.3/R1.4/R1.5/R1.12:** recent open-source/Node-RED/Grafana energy refs; MQTT-as-standard note; acknowledge four-layer architecture prior art; note browser-based config benefit.

### Tier 4 — Internal QA before resubmission
- `quarto render` clean; `reviewer-mdpi-full` red-team pass; reciprocal grep on new `@key`s; fill `response-to-reviewers.md` and `changes-summary.md`.

### Explicitly out of scope this round (state as future work, do not fake)
- Physical-hardware multi-vector validation (R2.2) and same-bench benchmark vs a mature commercial stack (R3.3). Defend on scope; commit to the follow-up paper.

---

## 7. One-paragraph recommendation for the authors

The reports are survivable. Reviewer 1 is on our side and Reviewer 2 is fair; both want the same thing — visual proof that the system runs and more results — which we can deliver from the existing open-source implementation. Reviewer 3 is the one to respect: we will never satisfy the "needs a new algorithm/theory" objection because the paper is deliberately an applied architecture, so we answer it by sharpening the contribution claim and standing on *Energies*' applied scope, not by inventing theory. The two things we genuinely cannot do this round — physical-device validation and a same-bench benchmark against mature systems — are already disclosed as limitations; we strengthen that disclosure, temper every absolute claim, and name the physical-validation paper as the next step. **Proceed with a thorough Major Revision; hold the rebuttal wording on R3.1 until the editor's formal decision tells us how hard that line actually is.**
