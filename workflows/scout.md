---
description: Evaluate external content (articles, videos, podcasts, posts) for content creation potential. Use when reviewing a URL or pasted content to decide if it's worth writing about.
quick_summary: "Ingest external source, score against pillars and prior art, produce Scout Report with proposed angles."
requires_mcp: []
recommends_mcp: [firecrawl-mcp]
---

# /scout — External Content Evaluation

Evaluate one or more external content sources against your content pillars, positioning, and existing published/draft work. Produces a scored Scout Report with a verdict (Write, Bookmark, or Pass) and proposed angles.

## When to Use

- You found an article, video, podcast, or post and want to know if there's content to create from it
- You want to batch-evaluate multiple sources at once
- You want a consistent, rubric-based evaluation instead of ad-hoc analysis

## Prerequisites

Before starting, load these skills (do NOT scan directories, paths are fixed):

1. `c:\HQ\content-creator\skills\content-scout\SKILL.md` — evaluation rubric and output template
2. `c:\HQ\content-creator\voice\voice-guide.md` — voice fingerprint (for angle credibility assessment)

For YouTube sources, also load:
3. The global `youtube-review` skill — for transcript extraction

## Input

The user provides one or more of:
- URLs (articles, YouTube videos, Perplexity pages, LinkedIn posts, X posts)
- Pasted text (podcast transcripts, copied content)
- A mix of both

## Steps

// turbo-all

### 1. Parse Input

Identify each source and detect its type:

| URL Pattern | Type |
|---|---|
| `youtube.com/watch` or `youtu.be/` | YouTube |
| `perplexity.ai/page/` | Web Article |
| `linkedin.com/posts/` or `linkedin.com/feed/` | LinkedIn Post |
| `x.com/` or `twitter.com/` | X Post |
| Any other URL | Web Article |
| Raw pasted text | Paste |

### 2. Route: Single vs. Batch

- **1 source**: Run Steps 3-6 inline. No subagents needed.
- **2+ sources**: Spin up one subagent per source for parallel processing (Steps 3-5). The parent handles Step 6 (Aggregate) after all subagents return.

When launching batch subagents, each subagent should:
- Read the `content-scout` skill
- Perform ingestion + normalization + evaluation for its assigned source
- Return the completed Scout Report

### 3. Ingest

Extract content from the source. Method varies by type:

| Type | Ingestion Method |
|---|---|
| **YouTube** | Use `youtube-review` skill to extract transcript and produce a summary with key ideas |
| **Web Article / Perplexity** | Use Firecrawl MCP `firecrawl_scrape` with `formats: ["markdown"]` and `onlyMainContent: true`. If Firecrawl is unavailable, fall back to `read_url_content` (may fail on some sites) |
| **LinkedIn / X Post** | Use Firecrawl MCP `firecrawl_scrape`. If unavailable or blocked, ask user to paste the content |
| **Paste** | Use the text as-is |

> [!TIP]
> Perplexity Pages return 403 on `read_url_content`. Always prefer Firecrawl for these URLs.

### 4. Normalize

Extract a standard set of fields from the ingested content, regardless of source type:

```yaml
title: "[Source title or first line]"
url: "[URL if applicable]"
type: "[Article | YouTube | Podcast | LinkedIn Post | X Post | Other]"
date: "[Publication date if available]"
content: "[Full text / transcript / post body]"
```

### 5. Evaluate

Load the `content-scout` skill and run its evaluation workflow:

1. Load prior art context (published articles, drafts, editorial calendar, LinkedIn drafts)
2. Score the 5 rubric dimensions (/5 each)
3. Determine verdict (Write / Bookmark / Pass)
4. If Write: run the decision gate and propose an angle
5. Produce the Scout Report using the exact output template from the skill

### 6. Aggregate (batch only)

After all subagents return their Scout Reports:

1. **Collect** all reports in a single artifact
2. **Cross-reference across sources**:
   - Flag overlapping angles ("Sources 1 and 3 both point at the same thesis")
   - Surface compound angles ("Sources 1 and 3 together support a stronger argument than either alone")
   - Deduplicate prior art checks (if multiple sources overlap with the same published article, note it once)
3. **Present** a unified summary at the top:

```markdown
## Scout Summary — [Date]

**Sources evaluated**: X
**🟢 Write**: X | **🟡 Bookmark**: X | **🔴 Pass**: X

### Quick View
| # | Source | Score | Verdict | Pillar |
|---|---|---|---|---|
| 1 | [Title] | X/25 | 🟢/🟡/🔴 | [Pillar] |
| 2 | [Title] | X/25 | 🟢/🟡/🔴 | [Pillar] |

### Cross-Reference Notes
- [Any overlaps, compound angles, or deduplication notes]

---

[Full Scout Reports below, one per source]
```

### 7. Hand Off

Based on the user's decision:

- **🟢 Write (long-form)**: Suggest running `/write-article` with the proposed angle and source as input
- **🟢 Write (short-form)**: Invoke `linkedin-writer` with the proposed angle
- **🟢 Write (update)**: Open the existing article and suggest specific additions with citations from the source
- **🟡 Bookmark**: Save the Scout Report to `c:\HQ\content-creator\sources\[slug].md` with YAML frontmatter:

```yaml
---
date: YYYY-MM-DD
source_url: "[URL]"
source_type: "[type]"
score: X
pillar: "[pillar]"
verdict: bookmark
tags: [scout, content-source]
---
```

- **🔴 Pass**: No action. Acknowledge and move on.

## Usage

```
/scout https://example.com/article
/scout https://youtube.com/watch?v=xxx
/scout https://perplexity.ai/page/topic-id https://example.com/article
/scout [paste content directly]
```

## Key Principles

- **Rubric, not vibes**: Every evaluation uses the same 5-dimension scoring. No ad-hoc analysis.
- **Prior art is mandatory**: The cross-reference step is what prevents rehashing published content. Never skip it.
- **Flag, don't block**: Missing personal proof gets flagged in Notes, not auto-rejected.
- **Scout reports are artifacts**: They should be consistent enough to compare across sessions.

## Related

- **Uses**: `content-scout` skill — the evaluation rubric and output template
- **Uses (YouTube)**: `youtube-review` skill — transcript extraction for video sources
- **Hands off to**: `/write-article`, `linkedin-writer`, `x-writer`
- **Complements**: `content-multiplier` — scout finds sources upstream; multiplier distributes content downstream
- **Future**: Daily Briefing System will use `content-scout` for automated source evaluation
