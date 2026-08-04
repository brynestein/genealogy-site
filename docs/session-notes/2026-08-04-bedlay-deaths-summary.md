# Session Notes — 2026-08-04

## Site Details
- **Site:** Genealogy Site
- **Live URL:** https://byrne-genealogy.pages.dev
- **Repo:** brynestein/genealogy-site

## This Session (Claude Code)

Andrew uploaded `Draft_Bedlay_Miner_Deaths.xlsx` (a working list of fatalities at Bedlay
Colliery, Lanarkshire) and asked for a deduplicated, spreadsheet-ready summary. No repo
files were touched — this was a standalone data-cleanup task, output delivered directly
to Andrew as a new `.xlsx` (not committed).

### What was done
- Source file: 62 rows, one per person, each with the same death re-described 2-4 times
  across `Notes 1`-`Notes 4` (different original sources: Inspector of Mines reports, the
  Durham Mining Museum database, newspaper cuttings, a narrative retelling).
- Consolidated to one clean row per person (Date, Name, Age, Occupation, Cause of Death
  summary, Notes/Sources), preserving all distinct facts (quotes, weights/distances/times,
  named colleagues, citation markers) while dropping repeated phrasing.
- Result: 59 named individuals + 1 aggregate incident note (the May 1973 coalface
  collapse — 5 killed, 4 injured, names not given in the source data).
- Merged one true duplicate: an "unnamed repairer, 1929" row and **George Ratcliffe**
  (15 Sep 1929, Repairer) describe the identical incident — merged into the Ratcliffe row.
- Flagged, but did **not** merge, a second possible duplicate (see below) since the
  data didn't support a confident call either way.

### Open item: Henry Dunn / Henry Turnbull Dunn — possible duplicate, unresolved

Two entries in the source data:
- **Henry Dunn**, 19 May 1941, age 37, Coal Stripper, "stone fell from roof"
- **Henry Turnbull Dunn**, 19 May 1944, age 39, Coal Stripper, "stone fell from roof"

Same day/month, same job, same cause, but different years and ages, and one has a
distinguishing middle name. Could be the same man recorded with a wrong year, or two
(possibly related) men.

Andrew asked me to check this against census records. I couldn't — logged here so the
next session doesn't waste time retrying the same blocked routes:
- `dmm.org.uk` and `scottishmining.co.uk` (the likely original sources for these rows,
  per citation style used elsewhere in the sheet) are both **blocked at the network
  policy level** for this Claude Code session — proxy CONNECT returns 403. Not a
  retry-able error.
- `web.archive.org` is blocked outright for this session (no cached-snapshot fallback).
- FreeCEN also 403'd.
- Scottish census records (1911 and 1921 are the only relevant public releases —
  1931 was destroyed, 1951 isn't released yet) live solely behind ScotlandsPeople.gov.uk,
  a paid/registered National Records of Scotland service. No free public index exists,
  and this session has no credentials for it.

**Recommended next step (needs Andrew, not Claude Code):** a free *name search* (not an
image purchase) on ScotlandsPeople for statutory death registrations — "Henry Dunn,"
New Monkland/Cadder registration district, 1941 and 1944. The index alone (district, age
at death, whether there are one or two distinct entries) should be enough to resolve this
without buying a certificate image.

## Known Follow-Ups (not urgent)
1. Resolve the Henry Dunn / Henry Turnbull Dunn duplicate question once Andrew has run
   the ScotlandsPeople name search above.
2. If/when the Bedlay Colliery deaths data is to become site content, it belongs in
   `src/data/*.json` per the JSON-data convention — it currently exists only as the
   delivered summary `.xlsx`, not in the repo.
