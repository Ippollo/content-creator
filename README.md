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
  blog-writer/           — Long-form SEO blog articles
  linkedin-writer/       — LinkedIn posts (standalone or atomized)
  case-study-writer/     — Case studies from real project experience
  content-multiplier/    — Orchestrates atomize/expand flows
  content-reviewer/      — Platform-agnostic quality scoring
  content-calendar/      — Editorial calendar, scheduling, pillar balance

strategy/
  pillars.md             — Niche, topic clusters, positioning
  algorithm.md           — LinkedIn algorithm rules
  seo-guidelines.md      — Blog SEO playbook

voice/                   — Your voice fingerprint and writing style

swipe-file/
  linkedin/              — Curated LinkedIn post examples
  blog/                  — Curated blog article examples
  case-studies/          — Curated case study examples

editorial-calendar.md    — Persistent publishing schedule (managed by content-calendar)

articles/
  drafts/                — Blog article drafts
  published/             — Published blog articles

linkedin/
  drafts/                — LinkedIn post drafts
  published/             — Published LinkedIn posts

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

### Grab today's first-comment
```
/comment
```

The agent reads your voice profile, strategy, SEO guidelines, and swipe files automatically via the appropriate skill.
