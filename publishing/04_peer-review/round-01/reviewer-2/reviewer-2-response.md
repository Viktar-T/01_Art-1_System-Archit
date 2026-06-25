# Response to Reviewer 2 — Round 1

> **Manuscript:** *Energies* — energies-4374418. **Round:** 1.
> Format follows the MDPI point-by-point response template.
> **Before sending:** (1) replace every `[…]` placeholder; (2) mark all manuscript revisions **in red** in the resubmitted files; (3) for each change cite the exact location in the *revised* PDF — **page number, paragraph, and line**; (4) delete every *(plan: …)* hint — internal notes from `revision-plan.md`, not for the editor.
> Comments below are reproduced **verbatim** from `reviewer-2-comments.md`. Comment numbers map 1:1 to triage IDs R2.1–R2.5.
> Note: Reviewer 2 rated the English as "could be improved" — run a language-polishing pass over the revised text and mention it in the opening paragraph.

---

We thank the reviewer for the constructive comments, which have improved the manuscript. We have also carefully revised the language throughout for clarity. Our point-by-point responses follow; reviewer comments are quoted verbatim, and the corresponding changes are highlighted in red in the revised manuscript.

---

**Comments 1:** The novelty of the proposed MING+React telemetry pipeline should be clarified more explicitly against existing open-source SCADA, MING, and IIoT monitoring architectures.

**Response 1:** *(plan: Accept — §1 / §2; R2.1)* Thank you for pointing this out. We agree with this comment. Therefore, we have [added an explicit "contribution and scope" statement that positions the MING+React pipeline against existing open-source SCADA, MING, and IIoT monitoring architectures, sharpening contributions C1–C3 and contrasting them with the cited prior art]. (Revised manuscript: [§1, page X, ¶Y, lines Z; §2.x, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 2:** The validation is mainly based on a local simulation environment, so the authors should add experiments with physical devices or real multi-vector energy system data.

**Response 2:** *(plan: Partial / Push-back — scope; future work; R2.2, overlaps R1.14)* We thank the reviewer for this important point. [State the scope clearly: this paper presents and validates the **architecture and edge-middleware pipeline** under a controlled, high-fidelity simulation; physical-hardware multi-vector validation is the explicit subject of the planned follow-up work and is beyond the scope of the present contribution.] To address the spirit of the comment within scope, we have [expanded the simulation evidence and strengthened the limitations/future-work text to state precisely what physical deployment will add]. (Revised manuscript: [§5.x and §6/§7 limitations, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 3:** The claimed 100% packet integrity and 100% null-pruning accuracy need stronger statistical support and should be tested under larger-scale and longer-duration scenarios.

**Response 3:** *(plan: Partial — add runs + temper claims; R2.3, overlaps R1.14)* Agree. We have, accordingly, [reported additional larger-scale and longer-duration runs with sample sizes, variance, and percentiles, and re-cast the "100%" statements as bounded, simulation-scoped results (e.g., "over N = … packets under simulated conditions")]. (Revised manuscript: [§5.x results and Table X, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 4:** Figure 3 appears inconsistent because the plot label refers to engine speed, while the caption describes normalized active power, so this should be corrected.

**Response 4:** *(plan: Accept — Fig. 3; R2.4)* Thank you for catching this inconsistency. We agree with this comment. Therefore, we have [corrected Figure 3 so the plot label and caption agree (normalized active power), and re-checked all other figure labels/captions for the same issue]. (Revised manuscript: [Figure 3, page X; caption on page X].) "[updated text in the manuscript if necessary]"

---

**Comments 5:** The limitations regarding loopback-only testing, physical network latency, packet loss, and scalability should be more directly reflected in the conclusion.

**Response 5:** *(plan: Accept — conclusion; R2.5, overlaps R1.13)* Agree. We have, accordingly, [reflected the loopback-only testing, physical network latency, packet loss, and scalability limitations directly in the conclusion, consistent with the consolidated limitations section]. (Revised manuscript: [§7 Conclusions, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

We thank the reviewer once again for the time and care given to our manuscript.
