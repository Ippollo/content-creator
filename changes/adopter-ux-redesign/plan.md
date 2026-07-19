# Content Plugin — Adopter-UX Redesign

**Status:** in progress · **Branch:** `content-adopter-ux-redesign`

**Goal:** make `hq-content` a clean, distributable plugin that works well for anyone who installs it,
while still serving Chris's own multi-plugin setup.

## Resolved decisions
1. **Scope:** full — Phases 1–4, including relocating Chris's own data and repackaging.
2. **`content_root` default:** `{vault_root}\Content` (solo adopters configure one path; the rest derives).
3. **house-style.md:** wire it into the writer skills as a pre-publish check; ship `house-style.template.md`.
4. **Site-specific SEO skills** (website-copywriter, schema-markup, seo-audit, page-cro,
   site-architecture): keep excluded from the package (gitignored, hardcoded to a personal site).

## Two-root model
`board` also reads `voice-guide.md` + `house-style.md` from the vault, so those are a **shared
identity layer**, not content data.

| Token | Holds | Default | Shared |
|---|---|---|---|
| `{vault_root}` (keep) | `voice-guide.md`, `house-style.md` | user's vault | with board |
| `{content_root}` (new) | calendar, drafts, swipe-file, pillars, sources | `{vault_root}\Content` | no |

## Target layout
Package (`{plugin_root}`, read-only, ships to everyone): `skills/`, `commands/`, new `knowledge/`
(linkedin-algorithm.md, x-algorithm.md, seo-guidelines.md), new `templates/` (voice-guide,
pillars, house-style, swipe-file-README), `config.md`, `README.md`.

Content data (`{content_root}`, created per-user): `strategy/pillars.md` (+ story/revenue ideas),
`swipe-file/{linkedin,blog,x,case-studies}/`, `calendar/` (+ `archive/`), `sources/`,
`drafts/{articles,linkedin,x,case-studies}/`, `published/{articles,linkedin,case-studies}/`.

## Token rewrites
- `{plugin_root}\strategy\pillars.md` (+ `pillar.md` typo) → `{content_root}\strategy\pillars.md`
- `{plugin_root}\swipe-file\*` → `{content_root}\swipe-file\*`
- `{plugin_root}\articles\drafts|published\*` → `{content_root}\drafts|published\articles\*`
- `{plugin_root}\linkedin\drafts|published\*` → `{content_root}\drafts|published\linkedin\*`
- `{plugin_root}\x\drafts\*` → `{content_root}\drafts\x\*`
- `{plugin_root}\case-studies\drafts\*` → `{content_root}\drafts\case-studies\*`
- `{plugin_root}\sources\*` → `{content_root}\sources\*`
- `{plugin_root}\editorial-calendar*.md` → `{content_root}\calendar\editorial-calendar-{month}-{year}.md`
- `{plugin_root}\strategy\algorithm.md` → `{plugin_root}\knowledge\linkedin-algorithm.md`
- `{plugin_root}\strategy\seo-guidelines.md` → `{plugin_root}\knowledge\seo-guidelines.md`
- `{plugin_root}\skills\...\SKILL.md` → unchanged (code)
- `{vault_root}\40_Knowledge\voice-guide.md` → unchanged (shared)
- `{vault_root}\40_Knowledge\content-pillars.md` → `{content_root}\strategy\pillars.md` (collapses 3-name mess)

## Phases
0. Change record + working branch. *(this file)*
1. Refactor package: knowledge/ + templates/, token rewrites, config.md + README.md rewrite, .gitignore.
2. Onboarding: `content-setup` skill + first-run detection in writers; wire house-style.md.
3. Relocate Chris's data into `KB\Content`; dedupe pillars.
4. Repackage (`git archive`), verify in Cowork, update maintenance memory.

## Bugs fixed along the way
- Pillars referenced under three names/paths (`content-pillars.md`, `strategy/pillars.md`, `pillar.md`).
- `house-style.md` declared in config but wired into zero skills.
