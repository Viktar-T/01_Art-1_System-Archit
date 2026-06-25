# Response to Reviewer 3 — Round 1

> **Manuscript:** *Energies* — energies-4374418. **Round:** 1.
> Format follows the MDPI point-by-point response template.
> **Before sending:** (1) replace every `[…]` placeholder; (2) mark all manuscript revisions **in red** in the resubmitted files; (3) for each change cite the exact location in the *revised* PDF — **page number, paragraph, and line**; (4) delete every *(plan: …)* hint — internal notes from `revision-plan.md`, not for the editor.
> Comments below are reproduced **verbatim** from `reviewer-3-comments.md`. Comment numbers map 1:1 to triage IDs R3.1–R3.3.
> Note: R3.1 is a **polite push-back** (we cannot invent theory we do not have — P2). Keep the tone respectful and evidence-led; do not "agree" to a defect that is actually a scope/framing point.

---

We thank the reviewer for the critical reading of our manuscript. We address each point below. Where we respectfully offer a clarification rather than a change, we explain our reasoning and support it with evidence; reviewer comments are quoted verbatim and the corresponding manuscript changes are highlighted in red.

---

**Comments 1:** This paper neither proposes a new data compression algorithm nor introduces a new edge computing scheduling theory or network communication protocol, so it lacks the theoretical depth required for academic research.

**Response 1:** *(plan: Push-back — clarify contribution & journal fit; R3.1. Do NOT fabricate theory.)* We thank the reviewer for this observation and we would like to respectfully clarify the nature and scope of the contribution. [State plainly that this is an **applied systems-architecture / integration** contribution, not a new algorithm or protocol: the novelty lies in C1 (the category-specific CDM translation layer implemented in Node-RED middleware), C2 (the automated edge-level null-pruning loop), and C3 (the empirical validation of temporal continuity and latency under concurrency).] [Note that this class of applied open-source monitoring-architecture work is squarely within the scope of *Energies* and comparable MDPI venues — for example the open-source SCADA/IIoT implementation papers cited in the revised introduction — where the evaluation standard is reproducibility, soundness, and demonstrated feasibility rather than new theory.] To make the contribution unmistakable, we have [added an explicit contribution-and-scope statement to the introduction and sharpened the abstract]. (Revised manuscript: [§1, page X, ¶Y, lines Z; abstract].) "[updated text in the manuscript if necessary]"

---

**Comments 2:** The author refers to the difference in data flow between high-speed electromechanical signals and low-speed biochemical signals as "impedance mismatch" and claims that traditional methods are difficult to synchronize. Suggest that the author provide additional descriptions and relevant literature to support this argument.

**Response 2:** *(plan: Accept — ground the framing; R3.2)* Agree. We have, accordingly, [added a fuller description of the "impedance mismatch" framing and grounded it with relevant literature on multi-rate / multi-time-scale sensor fusion and the synchronization difficulty between fast and slow physical domains, rather than relying on a single citation]. (Revised manuscript: [§1 and/or §4.1, page X, ¶Y, lines Z]; new entries in the reference list.) "[updated text in the manuscript if necessary]"

---

**Comments 3:** The author repeatedly emphasizes the low-latency and high scalability characteristics of their system in the abstract and conclusion, but they have not been compared and validated with established mature methods.

**Response 3:** *(plan: Partial — temper claims + add comparison context; R3.3, overlaps R2.3)* We thank the reviewer for this point. [Acknowledge that a same-bench head-to-head benchmark against a mature commercial stack is beyond the scope of this simulation-stage study.] To address the comment within scope, we have [tempered the low-latency and high-scalability statements in the abstract and conclusion to bounded, simulation-scoped claims, and added a qualitative comparison against published open-source/proprietary monitoring approaches using reported figures from the literature]. (Revised manuscript: [abstract; §6.x comparison, page X, ¶Y, lines Z; §7 Conclusions].) "[updated text in the manuscript if necessary]"

---

We thank the reviewer once again for the time and care given to our manuscript.
