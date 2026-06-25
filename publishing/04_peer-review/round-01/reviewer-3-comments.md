# Reviewer 3 — comments (verbatim)

> Transcribed verbatim from the MDPI review report form. Don't paraphrase or edit this block.

**Received:** 2026-06-21 (date of this review)
**Reviewer identity:** anonymous

## Review report form

**Quality of English Language:** The English is fine and does not require any improvement.

| Question | Yes | Can be improved | Must be improved | Not applicable |
|---|---|---|---|---|
| Does the introduction provide sufficient background and include all relevant references? | | x | | |
| Is the research design appropriate? | | | x | |
| Are the methods adequately described? | | | x | |
| Are the results clearly presented? | | | x | |
| Are the conclusions supported by the results? | | x | | |
| Are all figures and tables clear and well-presented? | | | x | |

---

1. This paper neither proposes a new data compression algorithm nor introduces a new edge computing scheduling theory or network communication protocol, so it lacks the theoretical depth required for academic research.

2. The author refers to the difference in data flow between high-speed electromechanical signals and low-speed biochemical signals as "impedance mismatch" and claims that traditional methods are difficult to synchronize. Suggest that the author provide additional descriptions and relevant literature to support this argument.

3. The author repeatedly emphasizes the low-latency and high scalability characteristics of their system in the abstract and conclusion, but they have not been compared and validated with established mature methods.

---

## Internal triage

Points numbered **R3.1 … R3.3** so they cross-reference cleanly in the rebuttal letter and commit messages.

| Point | One-line summary | Disposition | Effort |
|---|---|---|---|
| R3.1 | Claims the paper lacks theoretical depth (no new compression algorithm / edge-scheduling theory / network protocol) | Push-back — reframe as a systems-architecture / integration contribution; sharpen the stated contribution rather than invent theory | M |
| R3.2 | Support the "impedance mismatch" framing (high-speed electromechanical vs low-speed biochemical signals, synchronization difficulty) with descriptions and literature | Accept | M |
| R3.3 | Low-latency / high-scalability claims in abstract & conclusion are not compared/validated against established mature methods | Partial — temper absolute claims; add comparison/benchmark context where feasible (overlaps R2.3) | M |
