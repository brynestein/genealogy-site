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
- **Found:** slugs don't match the agreed `firstname-lastname-id` (lowercase-hyphenated) format — actual values are mixed-case with underscores, and some contain spaces from multi-part first names (e.g. `Mary Jane_Boyle_99`, `Anne Patricia Barbara_Grant_61`). Spaces in slugs will produce ugly URL-encoded links (`%20`) if used as-is in Astro routes.
- Asked Andrew how to handle this before building the person page template; awaiting decision (options: normalize all slugs now, keep as-is and URL-encode at render time, or build the template first and revisit later).

## What Needs To Be Done Next Session

1. Resolve the slug format decision (see above)
2. Build `src/pages/people/[slug].astro` — individual person page template showing:
   - Name, gender, dates, places
   - Photo (or gender silhouette placeholder if no photo)
   - Father, Mother — clickable links to their pages
   - Spouse / Spouse 2 — clickable links
   - Marriage Date
   - Children — auto-generated list of clickable links
   - Occupation, Baptism, Cause of death, Death Informant, Notes
   - Outlier badge (direct family / extended family)
3. Update the people list page to use the new fields
4. Create `public/images/people/` folder for photos
