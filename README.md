# Content Creator

Agent-powered content multiplier system. Write once, publish everywhere.

## How It Works

Start with a **pillar article** (long-form SEO blog post), then **atomize** it into shorter platform-specific posts. Or go the other direction — expand a strong LinkedIn post into a full article. **Case studies** follow the same multiplier model: write the case study, then atomize the strongest angles into LinkedIn posts.

```
Blog Article (pillar) ──→ LinkedIn Post 1 (atom)
                      ──→ LinkedIn Post 2 (atom)
                      ──→ Future Platforms

Case Study ──→ LinkedIn Post 1 (atom)
           ──→ LinkedIn Post 2 (atom)

LinkedIn Post ──→ Blog Article (expand)
```

## Structure

```
skills/
  blog-writer/           — Long-form SEO blog articles (argument architecture, checklist gate, persona review)
  linkedin-writer/       — LinkedIn posts (standalone or atomized)
  case-study-writer/     — Case studies from real project experience (SCAR framework, persona review)
  x-writer/              — X/Twitter posts (build-in-public, algorithm-informed)
  content-multiplier/    — Orchestrates atomize/expand flows
  content-reviewer/      — Platform-agnostic quality scoring (long-form editorial checks)
    rubrics/
      article.md         — Article scoring rubric (Voice, Structure, Evidence, SEO, Editorial)
      case-study.md      — Case study scoring rubric (SCAR structure, operational evidence, persona tests)
      linkedin.md        — LinkedIn scoring rubric (Algorithm, Specificity replace SEO, Evidence)
  content-calendar/      — Editorial calendar, scheduling, pillar balance

strategy/
  pillars.md             — Niche, topic clusters, positioning
  algorithm.md           — LinkedIn algorithm rules
  x-algorithm.md         — X algorithm rules (from open-source code)
  seo-guidelines.md      — Blog SEO playbook

voice/                   — Your voice fingerprint and writing style (multi-format)

workflows/
  write-article.md       — Full blog article pipeline (research → outline → draft → review)
  write-case-study.md    — Case study pipeline (intake → SCAR outline → draft → review)
  review-content.md      — Standalone review and scoring against canonical rubrics
  atomize.md             — Break pillar content into platform-specific posts
  publish.md             — Batch publish approved posts to Buffer
  comment.md             — Grab today's first-comment from the editorial calendar
  x-post.md              — Draft X posts for build-in-public updates

swipe-file/
  linkedin/              — Curated LinkedIn post examples
  blog/                  — Curated blog article examples
  case-studies/          — Curated case study examples
  x/                     — Curated X post examples

editorial-calendar.md    — Persistent publishing schedule (managed by content-calendar)

articles/
  drafts/                — Blog article drafts
  published/             — Published blog articles

linkedin/
  drafts/                — LinkedIn post drafts
  published/             — Published LinkedIn posts

x/
  drafts/                — X post drafts

case-studies/
  sources/               — Raw project notes, briefs, evidence
  drafts/                — Case study drafts
  published/             — Published case studies
```

## Usage

### Write a blog article
```
Write a blog post about [topic]. Target the keyword "[keyword]".
```

### Write a case study
```
Write a case study about [project]. Here's what happened: [brief description].
```

### Atomize into LinkedIn posts
```
Take my latest article and create LinkedIn posts from it.
```

### Expand a LinkedIn post
```
Expand my post about [topic] into a full blog article.
```

### Write a standalone LinkedIn post
```
Write a LinkedIn post about [topic].
```

### Schedule posts
```
Propose a schedule for my draft posts for the next 2 weeks.
```

### Batch publish
```
/publish
```

### Review and score a draft
```
Review and score [draft file]
```
or
```
/review-content
```
Loads the canonical rubric for the content type (article, case study, or LinkedIn) and produces a standardized scorecard. Five dimensions, each scored /10. Review-only — does not rewrite the draft.

### Grab today's first-comment
```
/comment
```

## Scoring System

All content review uses canonical rubrics in `skills/content-reviewer/rubrics/`. Each rubric defines:
- **5 dimensions** scored `/10` (dimension names vary by content type)
- **Score anchors** for 10, 7, and 5 to calibrate scoring
- **Required fixes** for any dimension scoring ≤7
- **Locked output format** — same structure every time

| Content Type | Rubric | Dimensions |
|---|---|---|
| Article | `rubrics/article.md` | Voice, Structure, Evidence, SEO, Editorial |
| Case Study | `rubrics/case-study.md` | Voice, Structure, Evidence, SEO, Editorial |
| LinkedIn | `rubrics/linkedin.md` | Voice, Structure, Algorithm, Specificity, Editorial |

Each rubric references its source-of-truth strategy file (articles/case studies → `seo-guidelines.md`, LinkedIn → `algorithm.md`) rather than restating rules inline.

The agent reads your voice profile, strategy, SEO guidelines, and swipe files automatically via the appropriate skill.
