# Session Notes & Handover — 2026-07-25

## Site Details
- **Site:** Genealogy Site
- **Live URL:** https://byrne-genealogy.pages.dev
- **Repo:** brynestein/genealogy-site

## Carried Over From Previous Session (Site Manager AI Editor)

### What Was Accomplished
1. Agreed 21-column data structure for `people.json`
2. Agreed slug format — firstname-lastname-id
3. All ~220 people added to `people.json` directly via GitHub by the user
4. Data structure agreed (see below)

### Agreed Data Structure (21 fields + photo)

| Field | Notes |
|---|---|
| ID | Unique number |
| Gender | M / F / U |
| First name | |
| Last name | Maiden name for females |
| Married name | Married surname females only |
| Date of birth | |
| Place of birth | |
| Baptism | |
| Life Status | Date of death, "Alive" or blank |
| Place of death | |
| Cause of death | |
| Place of burial | |
| Occupation | |
| Death Informant | ID if on list, free text if not |
| Notes | |
| Mother | ID number |
| Father | ID number |
| Spouse | ID number |
| Spouse 2 | ID number |
| Marriage Date | For Spouse 1 only |
| Outlier | Yes / No |
| Photo | Filename e.g. james-grant-1.jpg |

### Technical Issues (previous session)
- Site Manager hit a GitHub API 401 error and lost its GitHub connection mid-session
- Large file proposals were failing to deliver
- Workaround: user edited `people.json` directly in GitHub

## This Session (Claude Code)

- Confirmed GitHub write access works from this environment (no 401 issue here)
- Verified `people.json`: 221 records, all 21 agreed fields present plus `slug`
- No missing slugs, no duplicate slugs
- **Found:** slugs didn't match the agreed `firstname-lastname-id` (lowercase-hyphenated) format — mixed-case with underscores, some with spaces from multi-part first names (e.g. `Mary Jane_Boyle_99`). Andrew chose to normalize all slugs now (PR #2, merged) — all 221 slugs rewritten to lowercase-hyphenated, no collisions, only the `slug` field touched.
- Built `src/pages/people/[slug].astro` (PR #3, merged) — dynamic route generating a profile page per person: hero (name incl. married/maiden name, gender-tinted photo placeholder or real photo if `photo` is set, birth/death dates and places), facts grid (born, status/died, occupation, baptism, burial, direct/extended family badge from `outlier`), family section (mother/father/spouse resolved and linked by numeric ID, spouse 2 shown as free text since it's never an ID in current data, marriage date, auto-generated children list via mother/father ID lookup), and an additional-details section (cause of death, death informant, notes). Matching CSS added to `theme.css`.
- Wrapped the homepage's "Recently added" people grid in a `<details>` accordion, collapsed by default (PR #3) — it now renders all 221 people instead of a handful, per Andrew's request.
- Created `public/images/people/` (empty, `.gitkeep`) for future photos — no photos exist yet, so every person currently shows the gender-tinted placeholder disc.
- Removed the orphaned `mary-catherine-byrne.astro` demo page + its one-off JSON (PR #4, merged) — leftover from before `people.json` had real data, unlinked from anywhere, superseded by the new dynamic route.
- All four PRs (#1–#4) merged to `master`; Cloudflare Pages build green throughout (`npm run build`: 224 pages, no errors).

## Known Follow-Ups (not urgent)

1. The homepage accordion's cards still reference `p.name` / `p.dates` / `p.note` — fields that don't exist in the current `people.json` schema (real fields are `first_name`/`date_of_birth`/etc.), so expanded cards show blank text under the avatar. Pre-existing bug, more visible now that it's one click away instead of always-on.
2. Person id 214 ("Heather", no surname) has slug `heather--214` (double hyphen) — cosmetic, from a missing surname in the source data.
3. No photos exist in `people.json` yet — every profile page renders the placeholder disc. Add real filenames to the `photo` field and drop images into `public/images/people/` when ready.

## What Needs To Be Done Next Session

1. Fix or decide what to do with the homepage accordion's blank cards (item 1 above) — likely needs the card markup updated to the real 21-field schema, or a smaller "recent additions" subset instead of all 221.
2. Add real photos as they become available.
