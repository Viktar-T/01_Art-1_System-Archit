# ACM CCS 2012 classification codes

Generated 2026-05-28 via the ACM CCS concept selector at https://dl.acm.org/ccs for the manuscript *"Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems"* (MDPI *Energies*, Section A1).

## The three concepts (all significance 500 — primary topic)

| # | Concept ID (numeric) | Concept path |
|---|---|---|
| 1 | `10010520.10010553` | Computer systems organization → Embedded and cyber-physical systems |
| 2 | `10010520.10010521.10010537.10003100` | Computer systems organization → Cloud computing |
| 3 | `10002951.10002952.10002953` | Information systems → Database design and models |

Significance 500 = "high importance" (primary topic). ACM CCS allows 300 (medium) and 100 (low) for secondary concepts; we elected to mark all three as primary because each maps to a separate core contribution (CPS/IIoT framing, edge-to-cloud delivery, canonical data model).

## What to paste into the MDPI portal

MDPI's submission form (susy.mdpi.com) has a single **Code** field beside the "CCS (ACM Computing Classification System)" row. Paste **one of the following two equivalents**:

**Option A — description paths (preferred, human-readable):**

```
Computer systems organization~Embedded and cyber-physical systems; Computer systems organization~Cloud computing; Information systems~Database design and models
```

**Option B — numeric IDs (fallback if the parser rejects Option A):**

```
10010520.10010553; 10010520.10010521.10010537.10003100; 10002951.10002952.10002953
```

## What NOT to paste into MDPI

The block below is **for the ACM LaTeX class only** (used when submitting to ACM venues such as *Communications of the ACM*, ACM conferences, etc.). MDPI's `mdpi.cls` does **not** define `\ccsdesc` or `\begin{CCSXML}`. Do not paste this into `article.qmd` or the MDPI portal.

Kept here as a reference in case the manuscript is later submitted or re-purposed for an ACM venue.

```latex
\begin{CCSXML}
<ccs2012>
<concept>
<concept_id>10010520.10010553</concept_id>
<concept_desc>Computer systems organization~Embedded and cyber-physical systems</concept_desc>
<concept_significance>500</concept_significance>
</concept>
<concept>
<concept_id>10010520.10010521.10010537.10003100</concept_id>
<concept_desc>Computer systems organization~Cloud computing</concept_desc>
<concept_significance>500</concept_significance>
</concept>
<concept>
<concept_id>10002951.10002952.10002953</concept_id>
<concept_desc>Information systems~Database design and models</concept_desc>
<concept_significance>500</concept_significance>
</concept>
</ccs2012>
\end{CCSXML}
\ccsdesc[500]{Computer systems organization~Embedded and cyber-physical systems}
\ccsdesc[500]{Computer systems organization~Cloud computing}
\ccsdesc[500]{Information systems~Database design and models}
```

## Other classification rows on the MDPI form — leave blank

Per the analysis in chat:

- **MSC** (Mathematics Subject Classification) — N/A, no novel mathematics
- **PACS** (Physics & Astronomy Classification Scheme) — retired in 2010; leave blank
- **AGRICOLASCC** — not agriculture
- **JEL** — not economics
- **MESH** — not biomedical

## Rationale per concept

- **Embedded and cyber-physical systems** (`10010520.10010553`) — the manuscript's framing is explicitly CPS/IIoT (4-Layer CPS Architecture cited; OODA loop applied; Edge Gateway is the central architectural contribution).
- **Cloud computing** (`10010520.10010521.10010537.10003100`) — the pipeline is edge-to-cloud, containerised via Docker Compose, with cloud-side time-series persistence and dashboards.
- **Database design and models** (`10002951.10002952.10002953`) — the Canonical Data Model is the paper's primary technical contribution. Database design and the InfluxDB schema (measurements, tags, fields) sit at the centre of the work.

## Source

- ACM 2012 CCS tree: https://dl.acm.org/ccs
- Codes generated for this manuscript on 2026-05-28.
