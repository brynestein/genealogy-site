# genealogy-site

Placeholder scaffold for James Grant's family-history site. Astro 5 + JSON-data convention so the Site Manager AI Editor can read and write content directly.

## Stack

- Astro 5
- `@astrojs/sitemap`
- No CSS framework — system fonts, single `--brand` accent in `src/layouts/Layout.astro` so the layout can be repainted in one AI-Editor turn

## Pages

- `/` — landing stub
- `/about`
- `/contact`

Genealogy-specific sections (family tree, surnames, places, sources) are intentionally absent. James will iterate from reference sites via the AI Editor.

## Data

- `src/data/business.json` — name, tagline, contact (placeholder values)
- `src/data/seo.json` — per-page title + description
- `src/data/tracking.json` — GTM / GA4 / Clarity toggles (all off by default)

## Local dev

```
npm install
npm run dev
```
