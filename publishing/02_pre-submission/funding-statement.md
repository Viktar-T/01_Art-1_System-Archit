# Funding statement

This text goes into the **Funding** section of the manuscript AND into the portal's funding fields (MDPI deposits this to FundRef where it can).

## MDPI's required pattern

Use one of:

> This research was funded by [name of funder], grant number [xxx]. The APC was funded by [XXX].

Funder names **must match** the Crossref Funder Registry where possible: https://search.crossref.org/funding

## Our funding source

Project: **Edu-Bad — Educational–Research Online Platform for Integrated Renewable Energy Sources and Energy Storage Systems** (`D:\Life-OS\FUND-GRANT\30_projects\EduBad_PGE_2025`). The donation underwrote the build-out of the platform reported in this manuscript (MING+React stack, KIOZE Edu-Bad facility).

| Funder | Funder canonical name | Instrument | Agreement / ID | Period | Amount | What it supported |
|---|---|---|---|---|---|---|
| Fundacja PGE (PGE Foundation), Warsaw, Poland — the corporate foundation of PGE Polska Grupa Energetyczna S.A. | Fundacja PGE | Donation (*darowizna*) to ZUT | **2025/VII/29** | 2025-09-12 to 2025-11-30 (closed) | **20,000 PLN** | Build-out of the educational–research IoT platform (telemetry stack, dashboards, integration of RES and storage data sources). |

**Crossref Funder Registry note.** Fundacja PGE is **not currently listed** in the Crossref Funder Registry (verified 2026-05-27 via `api.crossref.org/funders?query=Fundacja+PGE`). The funder name will still appear correctly in the manuscript and the MDPI portal; FundRef simply will not auto-link it. This is normal for many regional/national foundations and does not affect publication. **No need to invent an ID.**

**APC funder: Faculty of Environmental Management and Agriculture (WKSiR), ZUT — under standing faculty policy.** The Faculty operates an internal regulation under which the APC is covered for articles published in journals scored **≥ 140 punktów** in the Polish ministerial list (MEiN journal ranking). *Energies* is listed at **140 punktów**, so this manuscript qualifies automatically. No per-article approval letter is required — the entitlement flows from the faculty regulation. The PGE donation (2025/VII/29, closed 2025-11-30) is unrelated to the APC and was earmarked for the platform build.

## Final paragraph for the manuscript

Paste this into `article.qmd` under "Funding". Resolve the APC placeholder before submission.

> **Funding:** This research was supported by a donation from Fundacja PGE (PGE Foundation, Poland), agreement number 2025/VII/29, awarded to the Department of Renewable Energy Sources Engineering (KIOZE) at the West Pomeranian University of Technology in Szczecin. The donation supported the development of the educational–research platform for integrated renewable energy sources and energy storage systems described in this manuscript. The APC was funded by the Faculty of Environmental Management and Agriculture (Wydział Kształtowania Środowiska i Rolnictwa), West Pomeranian University of Technology in Szczecin.

> Notes on the APC funder line (do NOT paste these into the manuscript):
> - **No markdown links in the manuscript text.** The above paragraph is plain.
> - The Faculty's funding entitlement rests on its internal regulation covering APCs for journals scored ≥ 140 punktów MEiN. *Energies* meets the threshold (140 pkt). Save a copy of the regulation locally (e.g. under `D:\Life-OS\122-Edu-ZUT\...` or this repo's `Logs/`) and reference it on the APC invoice when it arrives — it is the document the Faculty's accounting will quote when processing the payment.
> - **MEiN points are revised periodically.** Re-verify *Energies* still sits at ≥ 140 pkt on the **current** MEiN journal list at the time of submission (https://www.gov.pl/web/edukacja-i-nauka — search "wykaz czasopism naukowych"). If the score has been revised downward between drafting and submission, the entitlement does not apply and an alternative APC source must be identified.
> - Faculty reference page (for our records, not the manuscript): https://wksir.zut.edu.pl/aktualnosci/informacje-biezace.html

## Portal field guidance (susy.mdpi.com)

When the submission form asks for funding:
- **Funder name:** *Fundacja PGE* (do not abbreviate to "PGE Foundation" alone — Polish funders are indexed by their legal Polish name).
- **Grant / award number:** *2025/VII/29*.
- **Funder type:** Foundation / charity (not a government agency, not a commercial entity).
- **Award description:** Donation supporting the Edu-Bad educational–research platform at ZUT KIOZE.
- **APC:** enter the eventual APC funder separately when known.

## Sponsor influence on the work

MDPI requires explicit declaration of any sponsor role in design, execution, interpretation, writing, or decision to publish. Per `conflicts-of-interest.md` (already filled): **No sponsor influence.** That declaration is already in the manuscript's Conflicts of Interest block and does not need to be repeated in Funding. Worth noting for the author's own awareness: Fundacja PGE is the foundation of a Polish state-controlled electricity producer, so even though it acted as a charitable donor here, an attentive reviewer may scan for the standard "no sponsor role" statement — which is exactly what we have. No additional disclosure needed.

## Cross-check before submission

- [x] Funder legal name verified against the donation agreement (2025/VII/29).
- [x] Funder lookup attempted in Crossref Funder Registry — no match (documented above).
- [ ] Agreement number `2025/VII/29` re-verified against the signed PDF in `D:\Life-OS\FUND-GRANT\30_projects\EduBad_PGE_2025\10_scope\`.
- [x] APC funder identified — Faculty of Environmental Management and Agriculture (Wydział Kształtowania Środowiska i Rolnictwa), ZUT.
- [x] APC commitment secured under standing WKSiR regulation for ≥ 140 punktów MEiN journals (no per-article letter required).
- [ ] **Re-verify *Energies* at ≥ 140 pkt on the current MEiN list at submission time.**
- [ ] Local copy of the WKSiR APC regulation saved (path: `[FILL]`).
- [ ] Final paragraph (above) pasted into `article.qmd` under "Funding".
- [ ] Funding fields completed in the susy.mdpi.com portal during submission.

## Sources

- Project record: `D:\Life-OS\FUND-GRANT\30_projects\EduBad_PGE_2025\EduBad_PGE_2025.md`
- Project EN summary: `D:\Life-OS\FUND-GRANT\30_projects\EduBad_PGE_2025\EduBad-current-stage-main-info.EN.md`
- Crossref Funder Registry lookup (no match): https://api.crossref.org/funders?query=Fundacja+PGE
- KIOZE platform page: https://oze.zut.edu.pl/projects/platforma-edu-research/
- Live platform: http://edubad.zut.edu.pl
