# Reviewer 1 — comments (verbatim)

> Transcribed verbatim from `Comments and Suggestions for Authors.pdf` (the report attached to Leroy Liu's 2026-06-16 e-mail). Don't paraphrase or edit this block.

**Received:** 2026-06-16 (with editor's interim e-mail)
**Reviewer identity:** anonymous

## Review report form

**Quality of English Language:** The English is fine and does not require any improvement.

| Question | Yes | Can be improved | Must be improved | Not applicable |
|---|---|---|---|---|
| Does the introduction provide sufficient background and include all relevant references? | | x | | |
| Is the research design appropriate? | x | | | |
| Are the methods adequately described? | | x | | |
| Are the results clearly presented? | | | x | |
| Are the conclusions supported by the results? | | x | | |
| Are all figures and tables clear and well-presented? | | | x | |

---

Development and deployment of microgrid and the associated measurement and data acquisition systems constitute a relevant research arena nowadays. In addition, the topic belongs to the scope of the Journal. Some comments are given to enhance the manuscript.

Among the keywords, "open-source" is desirable from this humble reviewer viewpoint.

Some abbreviations are directly used without the required initial decomposition, such as SCADA or JSON.

The contextualization provided in the introductory section is well conducted but there are recently published papers that also deal with open-source software such as Node-RED, Grafana, and energy-related systems. Therefore, this reviewer strongly suggests enhancing this aspect in order to emphasize the relevance and opportunity of the reported research. Some publications that the authors could consider are now given, if they agree with the suggestion:

- Implementation and Experimental Application of Industrial IoT Architecture Using Automation and IoT Hardware/Software. Sensors 2024, https://doi.org/10.3390/s24248074
- Design and Implementation of Node-Red Based Open-Source SCADA Architecture for a Hybrid Power System. Energies 2023, https://doi.org/10.3390/en16052092

MQTT is a good choice. It is recommended to mention that it is the standard protocol for IoT ecosystems.

The four layers architecture presented in figure 1 has been profusely proposed in previous literature and is also a good choice to orchestrate the proposal.

The function topology depicted in figure 2 is illustrative. However, at least a block diagram or scheme to represent the data communication flows and networks should be included.

In line 125 there is some issue with a reference.

The authors refer to experimental setup in the title of the subsection 5.1. This could cause certain misleading to the reader given the fact that it is a simulation framework.

In a similar sense, what are the main features of the computers where the developed system is executed? For example, the CPU, RAM and operative system should be briefly mentioned. This could be placed in the subsection 5.1.

The authors report the JSON and JavaScript codes programmed in Node-RED. Nonetheless, a screenshot of the nodes that have been interconnected within the designed flow could be provided for a better visualization and comprehension of the developed software.

Even more, the software Grafana is supposed to be used to create dashboards for data visualization in the application layer. However, there are no images of any of the developed dashboards. If the authors want to prove the successful implementation of their proposal, this aspect needs to be solved.

The authors could indicate a benefit of using the Node-RED, InfluxDB and Grafana that relies in the use of web browsers for the edition and configuration of these suites.

The main limitations of the work are commented in the subsection 6.2. In addition, in subsection 7.2 there are also limitations of the study. Perhaps, both subsections could be integrated in a single text for a clearer structure of the manuscript.

The paper has an attractive title and the proposal is really interesting. However, once read the manuscript, this reviewer misses more results of the conducted simulations.

---

## Internal triage (details in `revision-plan.md`)

Points numbered **R1.1 … R1.14** so they cross-reference cleanly in the rebuttal letter and commit messages.

| Point | One-line summary | Disposition | Effort |
|---|---|---|---|
| R1.1 | Add "open-source" to the keywords | Accept | S |
| R1.2 | Expand abbreviations at first use (SCADA, JSON, …) | Accept | S |
| R1.3 | Strengthen intro with recent open-source / Node-RED / Grafana energy refs (2 DOIs suggested) | Accept | M |
| R1.4 | Note MQTT is the de-facto standard protocol for IoT ecosystems | Accept | S |
| R1.5 | Four-layer architecture (Fig. 1) endorsed as a good choice | No action (positive) — add a citation acknowledging prior use | S |
| R1.6 | Add a block diagram / scheme of data communication flows & networks (beyond Fig. 2) | Accept | M |
| R1.7 | Broken reference at line 125 | Accept (overlaps Zenodo `@software` "[?]" + EO ref check) | S |
| R1.8 | Rename §5.1 — "experimental setup" is misleading for a simulation framework | Accept | S |
| R1.9 | State compute environment in §5.1 (CPU, RAM, OS) | Accept | S |
| R1.10 | Add a Node-RED flow screenshot (interconnected nodes) | Accept | M |
| R1.11 | Add Grafana dashboard images — acceptance-critical ("prove successful implementation") | Accept | M |
| R1.12 | Note browser-based edition/configuration benefit of Node-RED + InfluxDB + Grafana | Accept | S |
| R1.13 | Merge limitations in §6.2 and §7.2 into a single text | Accept | S |
| R1.14 | Provide more results of the conducted simulations | Accept | L |
