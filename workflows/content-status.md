---
description: Show content pipeline status across articles, LinkedIn posts, editorial calendar, and scouted sources. Read-only scan — no files modified.
quick_summary: "Scan content-creator directories and produce a pipeline snapshot with recommended next actions."
---

# /content-status — Content Pipeline Visibility

Scan the content-creator directory tree and produce a structured pipeline snapshot. The primary consumer is the AI assistant, so it can accurately answer "what should I work on today?" without manually cross-referencing five directories.

**This workflow is read-only. It never modifies files, sets status, or approves content.**

## When to Use

- Before any content work session — "what's closest to done?"
- When asked "what should I work on?" and content is in scope
- After a batch of `/scout`, `/write-article`, or `/atomize` runs — to see what changed
- Weekly content planning

## Prerequisites

Before starting, read:

1. The current editorial calendar (e.g., `c:\HQ\content-creator\editorial-calendar-{month}-{year}.md`)
2. `c:\HQ\content-creator\strategy\pillars.md` — for pillar context when recommending actions

## Steps

// turbo-all

### 1. Scan Article Pipeline

Read all files in `c:\HQ\content-creator\articles\drafts\` and `c:\HQ\content-creator\articles\published\`.

For each article, extract from frontmatter:
- `slug`
- `title`
- `status` — expected values: `draft`, `reviewed`, `approved`, `published`
- `pillar`
- `date`
- `atoms` array (if present) — list of linked LinkedIn/X posts with their status

**Status definitions for articles:**

| Status | Meaning |
|---|---|
| `draft` | First draft exists, not yet reviewed |
| `needs-review` | Draft complete, flagged for user review |
| `reviewed` | Has been through content-reviewer scoring |
| `approved` | Final — ready to publish to website |
| `published` | Live on strategicoperator.ca |

> [!IMPORTANT]
> `approved` ≠ `published`. An article with `status: approved` is final but not yet live on the website. Only mark as `published` when it's actually accessible at a URL.

### 2. Scan LinkedIn Pipeline

Read all files in `c:\HQ\content-creator\linkedin\drafts\` and `c:\HQ\content-creator\linkedin\published\`.

For each LinkedIn draft, extract from frontmatter:
- `slug`
- `title`
- `status` — expected values: `draft`, `approved`, `scheduled`
- `source_article` (if present — indicates this is an atom)
- `date`

Cross-reference each draft against the current editorial calendar to determine if it's scheduled.

Flag any drafts that:
- Are NOT on the editorial calendar (orphaned drafts)
- Have been in `draft` status for more than 30 days (aging inventory)

> [!TIP]
> Slug matching between filenames and calendar entries may not be exact (e.g., `meditation-made-me-better-operator` vs `meditation-made-me-operator`). Use fuzzy matching on the slug — strip date prefixes from filenames and match on the core slug.

### 3. Scan Editorial Calendar

Parse the current month's editorial calendar tables. For each week:
- Count posts by status: `draft`, `approved`, `scheduled`
- Flag any `TBD` slots
- Note the furthest-scheduled date (how much runway exists)

### 4. Scan Scouted Sources

Count files in `c:\HQ\content-creator\sources\` (excluding README.md).
List each source slug. These are bookmarked — not in active production.

### 5. Compute Velocity (lightweight)

Count:
- Total published articles (files in `articles/published/`)
- Total published LinkedIn posts (files in `linkedin/published/`)
- Total LinkedIn drafts backlog (files in `linkedin/drafts/`)

### 6. Produce Pipeline Report

Output a structured report in this format:

```markdown
## Content Pipeline — [Date]

### 📝 Articles

| Slug | Status | Pillar | Atoms (draft) | Atoms (published) | Next Action |
|---|---|---|---|---|---|
| [slug] | [status] | [pillar] | [count] | [count] | [action] |

### 📅 Editorial Calendar — [Month Year]

| Week | Scheduled | Approved | Draft | TBD |
|---|---|---|---|---|
| [week of date] | [n] | [n] | [n] | [n] |

**Runway**: Scheduled through [date]. [n] TBD slots remaining.

### 💬 LinkedIn Drafts — Off Calendar

| Slug | Source | Age (days) |
|---|---|---|
| [slug] | [standalone or atom of X] | [n] |

### 🔍 Scouted Sources

[n] bookmarked sources: [list slugs]

### 📊 Velocity

- Published articles: [n]
- Published LinkedIn posts: [n]
- LinkedIn drafts backlog: [n]

### ⚡ Recommended Next Actions

1. [Highest-leverage action — what's closest to done]
2. [Second action]
3. [Third action]
```

### 7. Generate Next Actions

Apply these priority rules when recommending actions:

1. **Approved articles not yet published to website** → "Publish [slug] to strategicoperator.ca"
2. **Published articles with draft atoms not yet scheduled** → "Schedule atoms for [slug]"
3. **Editorial calendar weeks with all `draft` status** → "Review and approve posts for week of [date]"
4. **TBD slots on the calendar** → "Fill TBD slots for week of [date]"
5. **Article drafts that haven't been reviewed** → "Review [slug] draft"
6. **Published articles with no atoms generated** → "Run /atomize on [slug]"
7. **Aging LinkedIn drafts (30+ days, off calendar)** → "Triage: schedule, revise, or archive [slug]"

> [!IMPORTANT]
> Never recommend setting status to `approved` — only the user approves content. Recommendations should be "Review [slug] draft" not "Approve [slug]."

Present at most 3 recommended actions to keep the output actionable.

## Output

The pipeline report is displayed inline — not saved to a file. It's a point-in-time snapshot, not a persistent artifact.

## Related

- **Upstream**: `/scout` — evaluates external sources, creates bookmarks in `sources/`
- **Upstream**: `/write-article` — creates article drafts
- **Upstream**: `/atomize` — creates LinkedIn atoms from articles
- **Downstream**: `/publish` — schedules approved posts to Buffer
- **See also**: `/daily` — separate workflow for daily priorities (not content-specific)
