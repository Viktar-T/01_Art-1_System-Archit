# Citation tracker

Quarterly check on who's citing the paper. 10 minutes per quarter.

## Sources to check (rank by reliability)

1. **Google Scholar** — broadest coverage, includes preprints; least curated.
2. **Scopus** — institution login required; cleaner.
3. **Web of Science** — institution login required; cleanest.
4. **MDPI's own citation count** (on the article page).
5. **Dimensions.ai** — free, includes policy docs.

## Quarterly log

| Quarter | Date checked | GS | Scopus | WoS | MDPI | Dimensions | New citers (notable) |
|---------|--------------|----|--------|-----|------|------------|----------------------|
| Q[N] [YEAR] | [FILL] | | | | | | |

## Notable citers — context

When something interesting cites us:

- Date: [FILL]
- Citing work: [FILL — author, title, venue, DOI]
- Context: [FILL — did they extend the work, refute it, apply it, just list it?]
- Action: [FILL — read it, reach out to authors, mention in follow-up work, none]

## Setting up the recurring check

Use the `mcp__scheduled-tasks__create_scheduled_task` tool (or any calendar reminder) to schedule:

> "Quarterly citation check for the *Energies* paper — open `publishing/06_post-publication/citation-tracker.md` and log the latest counts from Google Scholar, Scopus, Web of Science, and MDPI's article page."

Cron expression: `0 9 1 1,4,7,10 *` (09:00 on the 1st of Jan / Apr / Jul / Oct).
