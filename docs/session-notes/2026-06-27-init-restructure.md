# 2026-06-27 — init / lock-down restructure

## What was scaffolded
- `CLAUDE.md` (root) — identity, protocols, Astro 5 / JSON-content stack, AI-Editor content model, gotchas.
- `.claude/agents/code-reviewer.md` — read-only reviewer tuned for this repo (content-in-JSON-not-markup, single `--brand` token, JSON-shape correctness).
- `docs/patterns/` + `docs/session-notes/` created.

## Moved
- Nothing — no orphan handover/spec docs at root.

## Production state
- Unchanged (no code touched). Deploy: Cloudflare Pages — `https://byrne-genealogy.pages.dev`.

## Open items
- **Stray junk directory at repo root** literally named `C:Usersandregenealogy-sitesrcpagespeople` (a botched-path artifact, empty). Should be removed — flagged to Andrew, not auto-deleted.

## Next-session opener
Remove the stray junk directory, then continue James's content via the AI Editor (data stays in `src/data/*.json`).
