# Data Availability Statement

MDPI requires a DAS on every article. Pick one of the canned statements below (closest match), customise, then paste into the manuscript.

## MDPI's canned statements (use one)

1. **Data contained within the article / supplementary material:**
   > The data presented in this study are available within the article.

2. **Data publicly archived:**
   > The data presented in this study are openly available in [name of repository], reference number [reference number] at [DOI or URL].

3. **Data archived but restricted:**
   > The data presented in this study are available on request from the corresponding author due to [state the reason — privacy, ongoing study, etc.].

4. **Third-party data:**
   > Restrictions apply to the availability of these data. Data were obtained from [third party] and are available [from the authors / at URL] with the permission of [third party].

5. **No new data:**
   > No new data were created or analyzed in this study. Data sharing is not applicable to this article.

## What applies to this manuscript

This paper is primarily architectural — it describes the **MING+React telemetry pipeline** for the KIOZE Edu-Bad. The empirical content typically includes:

- The system specification artefact (in this repo at `docs/pl-Edu-Bad-specification/IoT_Data_Arch-JSON-MQTT.md`).
- Reference configuration files for Mosquitto / InfluxDB / Node-RED / Grafana.
- Optionally, a sample telemetry trace illustrating the canonical data model.
- GitHub repo https://github.com/Viktar-T/plat-edu-bad-data-mvp.git

Decide together what we are publishing as data and pick the matching template.

## Decision: Path B — publicly archived (chosen 2026-05-27)

Repository made public and tagged release archived on Zenodo. MDPI canned statement **2** ("Data publicly archived") applies.

### Archive coordinates

| Field | Value |
|---|---|
| Primary repository | https://github.com/Viktar-T/plat-edu-bad-data-mvp |
| Release tag | `v1.0-mdpi-submission` |
| Release title | MING+React Telemetry Pipeline v1.0 (Supplementary Archive for "Architecting the Digital RES Learning Factory") |
| Archive (Zenodo) | https://doi.org/10.5281/zenodo.20415136 |
| Zenodo concept DOI / record | `10.5281/zenodo.20415136` |
| Licence (code) | as declared in the repository (verify on GitHub before submission) |
| Licence (Zenodo metadata) | should match the GitHub LICENSE; verify on the Zenodo record page |

### What the archive contains (verify before submission)

- The system specification artefact (`docs/pl-Edu-Bad-specification/IoT_Data_Arch-JSON-MQTT.md` equivalent in the repo).
- Reference configuration files for Mosquitto, InfluxDB, Node-RED, Grafana.
- Canonical data model schema(s).
- Optionally, a sample telemetry trace illustrating the canonical data model.
- React frontend source code.

## Final paragraph for the manuscript

Paste this verbatim into `article.qmd` under "Data Availability Statement":

> **Data Availability Statement:** The platform source code, reference configurations, and canonical data model schemas supporting the architecture presented in this study are openly available on GitHub at https://github.com/Viktar-T/plat-edu-bad-data-mvp (release `v1.0-mdpi-submission`) and permanently archived on Zenodo at https://doi.org/10.5281/zenodo.20415136.

## In-text reference (optional but recommended)

In the Methods section or wherever the implementation is first described, add a one-line pointer so the archive is discoverable from the body of the paper:

> The full reference implementation (Mosquitto, InfluxDB, Node-RED, Grafana, and React frontend) is openly available [@kanchipogu2026platedubad].

Then add a Software citation to `bibliography.bib`:

```bibtex
@software{kanchipogu2026platedubad,
  author    = {Kanchipogu, Kelvyn George Melcheizedek and Taustyka, Viktar},
  title     = {{MING+React Telemetry Pipeline v1.0 (Supplementary Archive for ``Architecting the Digital RES Learning Factory'')}},
  year      = {2026},
  version   = {v1.0-mdpi-submission},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20415136},
  url       = {https://doi.org/10.5281/zenodo.20415136}
}
```

(Author order in the citation should match the manuscript's final author order — adjust once the corresponding-author / name-format decisions in `../03_submission/submission-record.md` are resolved.)

## Pre-submission checklist

- [x] Decision recorded: **Path B — Data publicly archived**.
- [x] GitHub repository made public (`Viktar-T/plat-edu-bad-data-mvp`).
- [x] Zenodo deposit created with DOI **10.5281/zenodo.20415136**.
- [x] Release tag **v1.0-mdpi-submission** linked to the Zenodo record.
- [ ] Repository `README.md` contains a one-paragraph project description plus a "Cite this archive" block referencing the manuscript and the Zenodo DOI.
- [ ] Repository `LICENSE` present and compatible with manuscript publication (MIT / Apache 2.0 / CC-BY common choices).
- [ ] Zenodo record metadata: title, authors (with ORCIDs), CC-BY 4.0 (matches MDPI), keywords, and "Related identifiers" → `isSupplementTo` the eventual manuscript DOI (add after acceptance).
- [ ] Sensitive credentials, API keys, internal hostnames scrubbed from the repo (a "git secret scan" pass before considering this done).
- [ ] Final paragraph (above) pasted into `article.qmd` under "Data Availability Statement".
- [ ] `@kanchipogu2026platedubad` BibTeX entry added to `bibliography.bib`; in-text reference inserted in the Methods section.
- [ ] DOI URL `https://doi.org/10.5281/zenodo.20415136` resolves to the correct record (test in an incognito window — Zenodo can take a few minutes after upload).
