# Graphical Abstract — design brief

MDPI displays the graphical abstract (GA) beneath the text abstract online. It must be **attention-grabbing and self-contained**.

## MDPI's rules (verbatim summary)

- Must NOT be identical to any in-body figure, or a simple superposition of subfigures, or text-abstract + picture.
- Must be original, unpublished artwork — no copyrighted material, no postage stamps / currency / trademarks.
- File format: **PNG, JPEG, or TIFF**.
- Minimum size: **560 × 1100 pixels (height × width)**.
- Fonts: Times, Arial, Courier, Helvetica, Ubuntu, or Calibri.
- Use decimal points, not commas, in numbers.
- Avoid large text blocks and large blank areas.
- Do NOT include "Graphical Abstract" as a heading inside the image.

## Design brief for THIS paper

**Core message in one sentence:**
> An open-source MING+React pipeline turns heterogeneous multi-vector microgrid telemetry into a single canonical data model, from sensor to dashboard, at the edge.

**Required visual elements:**
- Left → Right flow: physical assets → edge gateway → MING stack → React dashboard.
- Physical assets: small icons for PV, wind, electrolyser, battery, thermal store.
- Edge gateway: visibly distinct (e.g. small box at the edge) — this is where the canonical data model is applied.
- MING stack: four small labelled blocks (Mosquitto / InfluxDB / Node-RED / Grafana). Optionally collapse into one labelled "MING" block.
- React dashboard: small UI sketch on the right.
- A subtle "canonical data model" arrow / label between the gateway and the stack — this is the paper's key contribution.

**Avoid:**
- Architecture-diagram-level detail (that's Figure 1 in the manuscript, GA must be different).
- Vendor logos.
- More than one accent colour.

## Production checklist

- [ ] Sketch approved by co-authors. — *human attestation*
- [x] Built in **hand-coded SVG** (no drawio/figma needed); source committed to `publishing/02_pre-submission/graphical-abstract.svg`. ✅ 2026-05-28
- [x] Exported as PNG at **2400 × 1200 px** (well above the 1100 × 560 minimum) and stored at `publishing/02_pre-submission/graphical-abstract.png`. ✅ 2026-05-28
- [ ] Final image visually scanned at 200 px wide (the thumbnail size on MDPI's listing pages) — still legible? — *human visual check*
- [x] Spell-check passed on all in-image text. ✅ 2026-05-28
- [x] No trademarked logos, no copyrighted images, no currency, no stamps. ✅ 2026-05-28 — see `../01_mdpi-requirements/copyright-permissions.md`
