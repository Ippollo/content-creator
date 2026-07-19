# Content Creator

Agent-powered content multiplier. Write once, publish everywhere — on your own voice.

Start with a **pillar article** (long-form SEO blog post), then **atomize** it into shorter
platform-specific posts. Or go the other direction — expand a strong LinkedIn post into a full
article. **Case studies** follow the same model.

```
Blog Article (pillar) ──→ LinkedIn Post 1 (atom)
                      ──→ LinkedIn Post 2 (atom)
Case Study ──────────────→ LinkedIn Post(s) (atom)
LinkedIn Post ───────────→ Blog Article (expand)
```

## Install & set up

1. Install the plugin (from a marketplace, or add the `.plugin` package in your client).
2. Run setup — just ask: **"set up the content plugin"** (the `content-setup` skill). It will:
   - ask where your content should live (defaults to `<your-vault>\Content`),
   - scaffold the folder layout,
   - copy the seed templates in,
   - interview you to build your **voice guide**, and
   - fill in `config.md` for you.
3. Start writing: *"Write a LinkedIn post about …"* / *"Write a blog post about …"*.

You can also edit `config.md` by hand — it holds just two paths (`vault_root`, `content_root`).
See [config.md](config.md) for the full contract.

## Where things live

**In the plugin package** (read-only, ships to everyone, replaced on update):

```
skills/        the writers, reviewer, scout, calendar, multiplier, and content-setup
commands/      slash commands (scout, write-article, atomize, publish, …)
knowledge/     generic reference — linkedin-algorithm.md, x-algorithm.md, seo-guidelines.md
templates/     seeds copied into your content folder at setup
```

**In your content folder** (`{content_root}`, created and managed for you — *your* data):

```
strategy/pillars.md            content pillars (canonical)
strategy/personal-story-ideas.md, revenue-biz-ideas.md
swipe-file/{linkedin,blog,x,case-studies}/
calendar/editorial-calendar-{month}-{year}.md   (+ archive/)
sources/                       bookmarked scout reports
drafts/{articles,linkedin,x,case-studies}/
published/{articles,linkedin,case-studies}/
```

**In your vault** (`{vault_root}`, shared identity — read-only to this plugin):

```
40_Knowledge/voice-guide.md    your voice fingerprint
99_System/house-style.md       publishable-content rules (checked before shipping)
```

> Prefer not to run a separate vault? Point `vault_root` and `content_root` at the same folder;
> setup will offer to place `voice-guide.md` / `house-style.md` at its root.

## Usage

| Goal | How |
|---|---|
| Scout external content | `/scout [url] [url2 …]` |
| Write a blog article | *"Write a blog post about [topic]. Target the keyword '[keyword]'."* |
| Write a case study | *"Write a case study about [project]. Here's what happened: …"* |
| Atomize into posts | *"Take my latest article and create LinkedIn posts from it."* |
| Expand a post | *"Expand my post about [topic] into a full blog article."* |
| Standalone LinkedIn post | *"Write a LinkedIn post about [topic]."* |
| Schedule posts | *"Propose a schedule for my draft posts for the next 2 weeks."* |
| Batch publish | `/publish` |
| Review & score a draft | `/review-content` or *"Review and score [draft file]"* |
| Grab today's first-comment | `/comment` |

## Scoring system

All content review uses canonical rubrics in `skills/content-reviewer/rubrics/`. Each defines 5
dimensions scored `/10`, score anchors for 10/7/5, required fixes for anything ≤7, and a locked
output format.

| Content Type | Rubric | Dimensions |
|---|---|---|
| Article | `rubrics/article.md` | Voice, Structure, Evidence, SEO, Editorial |
| Case Study | `rubrics/case-study.md` | Voice, Structure, Evidence, SEO, Editorial |
| LinkedIn | `rubrics/linkedin.md` | Voice, Structure, Algorithm, Specificity, Editorial |

Rubrics reference their source-of-truth in `knowledge/` (articles/case studies →
`seo-guidelines.md`, LinkedIn → `linkedin-algorithm.md`) rather than restating rules inline. The
agent reads your voice profile, pillars, guidelines, and swipe files automatically.
