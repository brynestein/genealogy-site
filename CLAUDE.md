# CLAUDE.md — genealogy-site

> Project contract for any Claude Code session in this repo.
> Read this file first. Everything below is a hard rule unless explicitly overridden in the current conversation.

## 0. Identity

- **User:** Andrew Byrne (`brynestein` on GitHub, `andrewjjbyrne1973@gmail.com`)
- **Project:** `genealogy-site` — a family-history site for **James Grant** (Byrne + Grant families). Astro 5, built on the **JSON-data convention** so the **Site Manager AI Editor** can read and write content directly.
- **Production:** Cloudflare Pages — `https://byrne-genealogy.pages.dev` (per `astro.config.mjs` `site:`).

## 1. Protocols (do not skip)

1. **Andrew approves all commits and pushes.** Draft, check, then **stop and ask**.
2. **Code review before presenting non-trivial changes** — run [.claude/agents/code-reviewer.md](.claude/agents/code-reviewer.md) (or apply its checklist) and surface concerns *with* the diff, in plain English.
3. **Never** `--no-verify`, `--force`, `--amend`, `git reset --hard`, `git clean -fd`.
4. **Never expose secrets** or paste `.env*` contents.
5. **Content lives in JSON, not markup.** Page copy/data belongs in `src/data/*.json` so the AI Editor can edit it in one turn. Don't move content into `.astro` files — that breaks the editing model.

## 2. Start-of-session ritual

1. Read the most recent [docs/session-notes/](docs/session-notes/).
2. Read any relevant [docs/patterns/](docs/patterns/).
3. `git status` and `git log --oneline -5`.

## 3. End-of-session ritual

1. Write a dated `docs/session-notes/YYYY-MM-DD-<slug>.md`.
2. Add/update `docs/patterns/` for any non-obvious data-shape or AI-Editor learning.
3. Tell Andrew the summary; **do not commit**.

## 4. Stack snapshot

- **Framework:** Astro 5 + `@astrojs/sitemap`.
- **Styling:** no CSS framework — system fonts, a single `--brand` accent in `src/layouts/Layout.astro` so the whole site can be repainted in one AI-Editor turn.
- **Content model:** `src/data/*.json` (about, contact, home, nav, people, stories, gallery, seo, …) read by the pages and read/written by the Site Manager AI Editor.
- **Deploy:** Cloudflare Pages (`byrne-genealogy.pages.dev`).
- **Related:** the `client-site-patterns` skill (Astro + Cloudflare + Site-Manager conventions).

## 5. What lives where

- `src/data/*.json` — all editable content (the AI Editor's surface).
- `src/data/people/` + `people.json` — the genealogy people data.
- `src/pages/` — `index`, `about`, `contact`, `people/` (thin; render from JSON).
- `src/components/` — `Header.astro`, `Footer.astro`.
- `src/layouts/Layout.astro` — shell + the single `--brand` accent.
- `public/` — images/assets. `docs/patterns/` + `docs/session-notes/` — notes + dated logs.

## 6. Permissions

[.claude/settings.json](.claude/settings.json) (if present) pre-approves safe commands; destructive ops stay denied. Widening is an explicit Andrew decision.

## 7. Memory layer (cross-project)

Cross-project auto-memory at `~/.claude/projects/<repo-slug>/memory/MEMORY.md` (cross-cutting Andrew-context). `docs/patterns/` holds project-specific knowledge. No duplication.

## 8. Things to never assume

- **Don't hardcode content in `.astro`** — it must stay in `src/data/*.json` for the AI Editor. Pages render from JSON; they don't carry copy.
- Don't add a CSS framework or extra accent colours — the single `--brand` token is deliberate (one-turn repaint).
- Genealogy-specific sections (family tree, surnames, places, sources) are intentionally minimal/absent at scaffold; James iterates via the AI Editor — don't pre-build speculative structure.
- **Repo hygiene:** there's a stray empty directory literally named `C:Usersandregenealogy-sitesrcpagespeople` at the repo root (a botched-path artifact). It's junk — remove it (flag to Andrew first).

## 9. House style

- Terse. No emoji in code or commit messages. Comments explain *why*, not *what*.
- Prefer editing existing files / JSON; don't add abstractions on the first call site.
- Keep pages thin — data in JSON, presentation in components/layout.
