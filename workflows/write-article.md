---
description: "Write an original blog article from scratch — research, outline, draft, review, save. Use when the user wants to create a new long-form article targeting a keyword, expanding on a topic, or turning a vault note into publishable content. Not for case studies (use /write-case-study) or LinkedIn posts (use /atomize from an existing article)."
---

# /write-article — Blog Article Origination

Orchestrates the full origination pipeline for a new blog article: topic → research → outline approval → draft → review → save → next steps.

## Anti-Patterns

- **Starting the draft before outline approval** — the outline gate exists to align on keyword, archetype, and structure before any writing happens. Skipping it wastes a full draft.
- **Writing from memory** — always read the voice profile and 2–3 swipe file examples before drafting. Tone drift is invisible until it's already in the draft.
- **Treating a case study as a blog article** — real project outcomes with before/after metrics belong in `/write-case-study`. Blog articles are thought leadership, not proof-of-work.
- **Asking too many questions upfront** — one focused clarifying question max. The keyword and angle can emerge through the outline proposal; don't interrogate the user before seeing their reaction to an option.

## Prerequisites

Before starting, silently load:

1. `c:\HQ\content-creator\skills\blog-writer\SKILL.md` — writing workflow and rules
2. `c:\HQ\content-creator\skills\content-reviewer\SKILL.md` — scoring and rewrite protocol
3. `c:\HQ\content-creator\voice\voice-guide.md` — voice fingerprint
4. `c:\HQ\content-creator\strategy\pillars.md` — content pillars and positioning
5. `c:\HQ\content-creator\strategy\seo-guidelines.md` — SEO rules
6. 2–3 examples from `c:\HQ\content-creator\swipe-file\blog\` — hook and structure patterns

## Input

The user provides a topic, keyword, or rough idea. Examples:
- "Write an article on how AI changes ops hiring"
- "I want to target the keyword 'fractional ops consultant'"
- "Turn my note about firefighting mode into an article"

## Steps

### 1. Clarify (if needed)

If the topic is ambiguous, ask **one** focused question. Don't barrage the user — gather the minimum needed to proceed.

If the user provides a vault note as source material, read it and extract the core thesis before proceeding.

### 2. Invoke `blog-writer`

Follow the `blog-writer` skill workflow end to end:

1. **Research and Angle** — identify search intent, target keyword, reader outcome, archetype
2. **Outline** — present H2 skeleton for user approval before drafting
3. **Draft** — write the full article (1,500–2,500 words)
4. **Self-Review** — run through `content-reviewer` (Voice, Structure, SEO rubrics; quality bar: 9/10; max 3 passes)
5. **Present** — show final article with score and review notes

### 3. Save

On user approval, save to:

```
c:\HQ\content-creator\articles\drafts\YYYY-MM-DD-[slug].md
```

Use full YAML frontmatter per `blog-writer` skill reference doc.

### 4. Suggest Next Steps

After saving, suggest:
- `/atomize [file path]` — break the article into LinkedIn posts
- `/publish` — when ready to schedule
