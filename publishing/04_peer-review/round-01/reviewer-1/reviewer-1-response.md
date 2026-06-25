# Response to Reviewer 1 — Round 1

> **Manuscript:** *Energies* — energies-4374418. **Round:** 1.
> Format follows the MDPI point-by-point response template.
> **Before sending:** (1) replace every `[…]` placeholder; (2) mark all manuscript revisions **in red** in the resubmitted files; (3) for each change cite the exact location in the *revised* PDF — **page number, paragraph, and line**; (4) delete every *(plan: …)* hint — those are internal notes from `revision-plan.md`, not for the editor.
> Comments below are reproduced **verbatim** from `reviewer-1-comments.md`. Comment numbers map 1:1 to triage IDs R1.1–R1.14.

---

We thank the reviewer for the careful and constructive review and for the kind remark that *"the topic belongs to the scope of the Journal"* and that *"the paper has an attractive title and the proposal is really interesting."* We have addressed every point below. Reviewer comments are quoted verbatim; our responses follow each comment, and the corresponding changes are highlighted in red in the revised manuscript.

---

**Comments 1:** Among the keywords, "open-source" is desirable from this humble reviewer viewpoint.

**Response 1:** *(plan: Accept — Keywords; R1.1)* Thank you for pointing this out. We agree with this comment. Therefore, we have [added "open-source" to the keyword list]. (Revised manuscript: [page X, keywords block, line Z].)

---

**Comments 2:** Some abbreviations are directly used without the required initial decomposition, such as SCADA or JSON.

**Response 2:** *(plan: Accept — throughout; R1.2)* Thank you for pointing this out. We agree with this comment. Therefore, we have [expanded all abbreviations at first use, including SCADA, JSON, and a full pass for others]. (Revised manuscript: [first-use locations — page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 3:** The contextualization provided in the introductory section is well conducted but there are recently published papers that also deal with open-source software such as Node-RED, Grafana, and energy-related systems. Therefore, this reviewer strongly suggests enhancing this aspect in order to emphasize the relevance and opportunity of the reported research. Some publications that the authors could consider are now given, if they agree with the suggestion: *Implementation and Experimental Application of Industrial IoT Architecture Using Automation and IoT Hardware/Software.* Sensors 2024, https://doi.org/10.3390/s24248074 — *Design and Implementation of Node-Red Based Open-Source SCADA Architecture for a Hybrid Power System.* Energies 2023, https://doi.org/10.3390/en16052092

**Response 3:** *(plan: Accept — §1 Introduction; R1.3)* Agree. We thank the reviewer for these references. We have, accordingly, [strengthened the introduction with recent open-source / Node-RED / Grafana energy literature, including the two suggested papers and others as appropriate]. (Revised manuscript: [§1, page X, ¶Y, lines Z]; new entries in the reference list.) "[updated text in the manuscript if necessary]"

---

**Comments 4:** MQTT is a good choice. It is recommended to mention that it is the standard protocol for IoT ecosystems.

**Response 4:** *(plan: Accept — §3 Network Layer / MQTT; R1.4)* Thank you for pointing this out. We agree with this comment. Therefore, we have [noted that MQTT is the de-facto standard protocol for IoT ecosystems, with a supporting citation]. (Revised manuscript: [§3.x, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 5:** The four layers architecture presented in figure 1 has been profusely proposed in previous literature and is also a good choice to orchestrate the proposal.

**Response 5:** *(plan: No action / positive — add prior-art citation; R1.5)* We thank the reviewer for this positive assessment. To acknowledge the prior use of the four-layer architecture, we have [added citation(s) recognising its established use in the literature]. (Revised manuscript: [§3.1, page X, ¶Y, lines Z].)

---

**Comments 6:** The function topology depicted in figure 2 is illustrative. However, at least a block diagram or scheme to represent the data communication flows and networks should be included.

**Response 6:** *(plan: Accept — new figure near Fig. 2; R1.6)* Agree. We have, accordingly, [added a new block diagram / scheme depicting the data communication flows and network topology]. (Revised manuscript: [new Figure X, page X; described in §3.x, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 7:** In line 125 there is some issue with a reference.

**Response 7:** *(plan: Accept — refs / line 125; R1.7)* Thank you for catching this. We agree with this comment. Therefore, we have [corrected the broken reference (the Zenodo `@software` entry that rendered as "[?]") and re-verified surrounding citations]. (Revised manuscript: [page X, ¶Y, line Z].) "[updated text in the manuscript if necessary]"

---

**Comments 8:** The authors refer to experimental setup in the title of the subsection 5.1. This could cause certain misleading to the reader given the fact that it is a simulation framework.

**Response 8:** *(plan: Accept — §5.1 heading; R1.8)* Agree. We have, accordingly, [renamed §5.1 to reflect that it is a simulation framework rather than a physical experimental setup, and checked the surrounding wording for the same issue]. (Revised manuscript: [§5.1 heading, page X, line Z].) "[updated text in the manuscript if necessary]"

---

**Comments 9:** In a similar sense, what are the main features of the computers where the developed system is executed? For example, the CPU, RAM and operative system should be briefly mentioned. This could be placed in the subsection 5.1.

**Response 9:** *(plan: Accept — §5.1; R1.9)* Thank you for this suggestion. We agree with this comment. Therefore, we have [added the compute environment (CPU, RAM, operating system, container runtime) in §5.1]. (Revised manuscript: [§5.1, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 10:** The authors report the JSON and JavaScript codes programmed in Node-RED. Nonetheless, a screenshot of the nodes that have been interconnected within the designed flow could be provided for a better visualization and comprehension of the developed software.

**Response 10:** *(plan: Accept — new figure; R1.10)* Agree. We have, accordingly, [added a screenshot of the interconnected Node-RED flow]. (Revised manuscript: [new Figure X, page X; referenced in §5.x, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 11:** Even more, the software Grafana is supposed to be used to create dashboards for data visualization in the application layer. However, there are no images of any of the developed dashboards. If the authors want to prove the successful implementation of their proposal, this aspect needs to be solved.

**Response 11:** *(plan: Accept — acceptance-critical; new figure(s); R1.11)* Thank you for pointing this out. We agree with this comment. Therefore, we have [added image(s) of the developed Grafana dashboard(s) demonstrating the implemented application layer]. (Revised manuscript: [new Figure X (and Y), page X; referenced in §3.x / §5.x, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 12:** The authors could indicate a benefit of using the Node-RED, InfluxDB and Grafana that relies in the use of web browsers for the edition and configuration of these suites.

**Response 12:** *(plan: Accept — stack rationale; R1.12)* Agree. We have, accordingly, [noted the benefit that Node-RED, InfluxDB, and Grafana are edited and configured through standard web browsers, lowering deployment and maintenance friction]. (Revised manuscript: [§3.x, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 13:** The main limitations of the work are commented in the subsection 6.2. In addition, in subsection 7.2 there are also limitations of the study. Perhaps, both subsections could be integrated in a single text for a clearer structure of the manuscript.

**Response 13:** *(plan: Accept — §6.2 + §7.2; R1.13)* Thank you for this structural suggestion. We agree with this comment. Therefore, we have [consolidated the limitations from §6.2 and §7.2 into a single, coherent limitations text]. (Revised manuscript: [merged into §X.X, page X, ¶Y, lines Z].) "[updated text in the manuscript if necessary]"

---

**Comments 14:** The paper has an attractive title and the proposal is really interesting. However, once read the manuscript, this reviewer misses more results of the conducted simulations.

**Response 14:** *(plan: Accept — results; R1.14, overlaps R2.3)* We thank the reviewer for the encouraging assessment. Agree. We have, accordingly, [expanded the reported simulation results — additional vectors plotted, longer-duration and higher-concurrency runs, latency distributions, and supporting tables/figures]. (Revised manuscript: [§5.x, page X, ¶Y, lines Z; new Figure(s)/Table(s) X].) "[updated text in the manuscript if necessary]"

---

We thank the reviewer once again for the time and care given to our manuscript.
