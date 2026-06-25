# Graphical Abstract — generation prompt for an AI agent

Self-contained prompt to (re)generate the graphical abstract for the manuscript *"Architecting the Digital RES Learning Factory: A Scalable MING+React Telemetry Pipeline for Multi-Vector Energy Systems"* (MDPI *Energies*, Section A1 — Smart Grids and Microgrids).

**Authoritative sources** the agent should consult before drawing anything:
- Specification: `D:\Life-OS\130-V-RESEARCH\70_outputs\Digital-KIOZE\01_Articles\01_Art-1_System-Archit\docs\pl-Edu-Bad-specification\IoT_Data_Arch-JSON-MQTT.md`
- Manuscript: `D:\Life-OS\130-V-RESEARCH\70_outputs\Digital-KIOZE\01_Articles\01_Art-1_System-Archit\ihrke-template\article.qmd`
- MDPI graphical-abstract rules: `D:\Life-OS\130-V-RESEARCH\70_outputs\Digital-KIOZE\01_Articles\01_Art-1_System-Archit\publishing\02_pre-submission\graphical-abstract-brief.md`

---

## 1. Headline message (one sentence)

> An open-source MING+React pipeline normalises **fast mechanical-electrical** and **slow biological/thermal/chemical** telemetry from **seven** KIOZE Edu-Bad asset categories into a single **Canonical Data Model at the edge**, and serves it to a reproducible React operator UI.

The graphical abstract must communicate this in one glance, without copying any in-body figure of the manuscript.

## 2. The "Impedance Mismatch" — the paper's central concept

This is the conceptual hook the GA must depict. The paper's contribution is the resolution of a **speed-class mismatch** between two families of energy vectors:

- **Fast vectors (mechanical / electrical), 1000 ms ingest interval, six parameters.** Engine Speed (RPM), Torque (Nm), Active Power (kW), Grid Voltage (V), Grid Current (A), Grid Frequency (Hz).
- **Slow vectors (biological / thermal / chemical), 5000 ms ingest interval, six parameters.** pH, Dissolved Oxygen (mg/L), Optical Density (OD₅₆₀nm), Gas Pressure (kPa), Methane Concentration (%), Medium Temperature (°C).

Together: 12 vectors, 6 fast + 6 slow. The fast/slow contrast must be visually obvious — different shape, position, label, or accent treatment.

## 3. Multi-Vector Assets — the SEVEN categories (use these exact labels)

The KIOZE Edu-Bad platform integrates **seven technology categories** (not five, not "Electrolyser"). The GA must show all seven. Order them left to right or top to bottom, grouped by speed class so the fast/slow contrast is legible.

| # | Category (label in GA) | Sub-stations (do not list all in GA — too crowded) | Speed class | Icon hint |
|---|---|---|---|---|
| 1 | **Photovoltaic (PV)** | Solar Charger (PV-Hulajnogi), PV Panels (PV-Rotate, PV-Agro-small) | Fast electrical | Solar grid / panel |
| 2 | **Wind** | VAWT (Big Vertical Storage), HAWT (Solar-Wind Hybrid) | Fast mechanical-electrical | Turbine on pole |
| 3 | **Engine Bench** | Engine-bench-R121 (eddy-current dynamometer) | Fast mechanical-electrical | Piston / dyno / gear |
| 4 | **Energy Storage** | Converter & Storage (LiFePO₄ pack, grid-forming inverter) | Fast electrical | Battery + inverter |
| 5 | **Biogas** | Anaerobic digester (Biogas-Plant) | Slow biochemical | Digester tank with CH₄ bubbles |
| 6 | **Heat / Stirling** | Stirling engine + Phase-Change-Material TES (Heat-Boiler / Sterling-Storage) | Slow thermal | Heat exchanger / piston in furnace |
| 7 | **Algae Photobioreactor (PBR)** | Indoor LED (Algae-Farm-1), Outdoor solar (Algae-Farm-2) | Slow biochemical | Tubular bioreactor with green medium |

The first four are **fast** (group together visually). The last three are **slow** (group together visually). Use the fast/slow grouping to make the "Impedance Mismatch" visible at a glance.

**Do not draw**:
- "Electrolyser" — not part of the KIOZE Edu-Bad system.
- "Hydrogen production" — not part of the system.
- Generic unlabelled "Thermal" — be specific: Heat/Stirling.

## 4. The middle: Edge Gateway + Canonical Data Model

The Edge Gateway is the paper's central architectural contribution. Render it as a single visually-dominant block in the middle of the composition with:
- Primary label: **Edge Gateway**
- Subtitle / secondary label: **Canonical Data Model** (CDM)
- Three bullet annotations inside or next to the block:
  - **CDM translation layer** — maps every sensor to a fixed `measurement / tags / fields / timestamp / status` JSON contract
  - **Null-Pruning loop** — guarantees 100 % data purity before storage
  - **Metadata separation** — tags vs. fields kept distinct so InfluxDB cardinality stays bounded

Show converging arrows from all seven asset categories into the Edge Gateway. Show one outgoing arrow from the Edge Gateway to the MING stack, captioned **"normalise at the edge — before storage"** (this captures the "before storage rather than at query time" delta from the cover letter).

## 5. The right side: MING stack and React UI

After the Edge Gateway, the data flows through the four MING-stack components, then to a React operator UI.

### MING stack — four labelled components

Render as four small labelled blocks (any compact layout — 2×2 grid, vertical column, or row works). The mnemonic is **M-I-N-G** (Mosquitto, InfluxDB, Node-RED, Grafana), but **functionally** the order is **M → N → I → G**:

| Letter | Component | Role | Layer |
|---|---|---|---|
| M | **Mosquitto** | MQTT broker (pub/sub, topic taxonomy `wksir/kioze/<category>/<station>/telemetry`) | Network |
| N | **Node-RED** | Middleware: CDM translation, null-pruning, ingestion flows | Middleware |
| I | **InfluxDB** | Time-series database (bucket `renewable_energy`, 30-day retention) | Persistence |
| G | **Grafana** | Native dashboards over InfluxDB (Flux datasource) | Application |

It is acceptable to render them as **M I / N G** in a 2×2 grid for compactness (this matches the MING acronym layout the reader expects), or as **M → N → I → G** in a row to show the data flow.

### React Operator UI — terminal block

Render as a browser-frame card titled with the production URL **edubad.zut.edu.pl** containing one or two mock telemetry tiles (e.g. `PV power: 12.5 kW`, `Wind: 3.8 kW`) and one or two mock chart shapes (a line chart for fast vectors, a bar or area chart for slow vectors). Use decimal points, not commas.

## 6. Optional bottom strip — the takeaway

A single horizontal pill-shaped strip across the bottom, teal-on-white text, communicating the elevator pitch in one line. Suggested text:

> Heterogeneous multi-vector telemetry → normalised at the edge → reproducible (Zenodo DOI 10.5281/zenodo.20415136)

The DOI mention is optional; include only if it doesn't crowd the strip.

## 7. Visual style and design rules

- **Single accent colour.** Teal `#0f766e` (primary), `#ccfbf1` or `#f0fdfa` (subtle fills). Avoid second accent colours.
- **Text colour.** Body labels in `#1f2937` (dark slate); secondary labels in `#475569`; on-teal text in `#ccfbf1` or pure white.
- **Background.** Pure white `#ffffff`. No gradients, no photographic backgrounds.
- **Shapes.** Rounded rectangles (corner radius 8–14 px). Thin strokes (1.5–2 px). No drop shadows.
- **Icons.** Original geometric line-art, no clip-art, no vendor logos, no copyrighted material. Each asset card needs a small unambiguous icon (≤ 60 × 60 px) so the category is recognisable without reading the label.
- **Typography.** One of: Arial, Helvetica, Calibri, Ubuntu, Times, Courier (MDPI's allowed list). Use a sans-serif (Arial/Helvetica) for clarity. Weight hierarchy: section headers 700, asset names 600, sub-labels 400.
- **Numbers.** Decimal points only, never commas (per MDPI rule).
- **No "Graphical Abstract" heading inside the image** (MDPI rule).
- **No large text blocks, no large blank areas.**
- **Original work only** — no copyrighted images, no postage stamps, no currency, no trademarks (including no MING component logos: render letter monograms instead).

## 8. MDPI output requirements (HARD CONSTRAINTS)

- **Format:** PNG (preferred), JPEG, or TIFF.
- **Minimum size:** 560 px height × 1100 px width (MDPI minimum). **The agent should render at higher resolution — recommend 1200 × 2400 px or 1240 × 2480 px (~2× the minimum) for crisp rendering.**
- **Aspect ratio:** landscape, approximately 2:1 (width:height). Do not use portrait or square.
- **Maximum file size:** 200 MB (this is not a binding constraint at the recommended resolution — typical output will be 100–300 KB).
- **Colour space:** RGB, 8-bit per channel.
- **Must not be identical to any in-body figure of the manuscript** (especially not @fig-layers, the 4-Layer CPS diagram, and not @fig-ooda, the OODA loop diagram).

## 9. File outputs

The agent must produce, into `D:\Life-OS\130-V-RESEARCH\70_outputs\Digital-KIOZE\01_Articles\01_Art-1_System-Archit\publishing\02_pre-submission\`:

1. `graphical-abstract.svg` — vector source (editable, version-controlled).
2. `graphical-abstract.png` — rasterised at 1200 × 2400 px or 1240 × 2480 px, 8-bit RGB.

Optional but recommended: also copy the PNG to `ihrke-template/pics/graphical-abstract.png` if the manuscript references it from the body.

## 10. Self-check checklist (the agent must verify before declaring done)

Tick every box. If any is unchecked, iterate.

- [ ] All **seven** asset categories present and correctly named (PV, Wind, Engine Bench, Energy Storage, Biogas, Heat/Stirling, Algae PBR).
- [ ] Fast vs. slow grouping is visually apparent (different position, label, or accent treatment).
- [ ] **Edge Gateway** block is the visual centre with the **Canonical Data Model** label clearly visible.
- [ ] Three CDM annotations present: translation layer, null-pruning, metadata separation.
- [ ] Converging arrows from all seven assets into the Edge Gateway, one outgoing arrow to the MING stack, one outgoing arrow to the React UI.
- [ ] MING stack present as four labelled components (Mosquitto / Node-RED / InfluxDB / Grafana).
- [ ] React UI block titled `edubad.zut.edu.pl` with at least one tile and one chart shape.
- [ ] No "Electrolyser", no "Hydrogen", no generic "Thermal" — replaced with the real categories.
- [ ] No "Graphical Abstract" heading in the image.
- [ ] No vendor logos, no copyrighted material, no postage stamps / currency / trademarks.
- [ ] Single accent colour (teal `#0f766e` family).
- [ ] Decimal points only.
- [ ] Output PNG ≥ 1100 px wide and ≥ 560 px tall, landscape orientation.
- [ ] SVG source saved alongside PNG.
- [ ] Image reads cleanly at 200 px wide (MDPI thumbnail) — large labels survive shrinkage even if small ones don't.

## 11. Implementation hint (for an SVG-building agent)

The most direct way to deliver this is:

1. Compose an SVG with `viewBox="0 0 2400 1200"` (clean 2:1 ratio).
2. Lay it out in five horizontal bands: section headers (top), main flow (middle), takeaway strip (bottom). Within the main flow, four vertical zones: (1) seven asset cards stacked or grouped 4-fast / 3-slow, (2) Edge Gateway block centred, (3) MING stack 2×2 grid, (4) React UI browser frame.
3. Render to PNG with `cairosvg.svg2png(url=..., write_to=..., output_width=2400, output_height=1200)`.
4. Verify the output dimensions with `file graphical-abstract.png`.
5. Tick the self-check checklist.

The previous iteration of this graphical abstract (already in the folder before this prompt was written) used only five asset categories and included a non-existent "Electrolyser". This new iteration must correct that — refer to §3 above for the canonical seven-category list.
