---
description: Write a case study from real project experience.
---

# /write-case-study — Case Study Origination

Orchestrates the full case study pipeline: intake → confidentiality → SCAR outline approval → draft → review → save → atomization suggestion.

## Anti-Patterns

- **Skipping the confidentiality check** — client names, revenue figures, and internal metrics must be flagged before outlining. Anonymization decisions shape the whole narrative; you can't bolt them on after drafting.
- **Starting the draft before outline approval** — the SCAR outline gate is where the user confirms the story arc, before any writing happens. Skipping it produces a draft that often needs full restructuring.
- **Treating one engagement as multiple case studies** — each case study is one transformation story. If the user describes three separate problems they solved, that's three case studies. Flag it and confirm scope before starting.
- **Dumping all intake questions at once** — overwhelming the user with a 12-question intake form kills momentum. Ask in three conversational rounds: context → action → results. If raw notes are provided, extract answers first and only ask about confirmed gaps.
- **Letting the user be the hero** — case studies are about the outcome, not the operator. Every section should be answerable by the reader asking "so what?" If a passage can't pass that test, cut it.

## Prerequisites

Before starting, silently load:

1. `c:\HQ\content-creator\skills\case-study-writer\SKILL.md` — intake, SCAR workflow, and review protocol
2. `c:\HQ\content-creator\skills\content-reviewer\SKILL.md` — scoring and rewrite protocol
3. `c:\HQ\content-creator\voice\voice-guide.md` — voice fingerprint
4. `c:\HQ\content-creator\strategy\pillars.md` — content pillars and positioning

## Input

The user provides a project to write about. Examples:
- "Write a case study on the client onboarding overhaul at [company]"
- "I want to document the ops automation project I ran last year"
- Raw notes, a project brief, or a vault note

## Steps

### 1. Invoke `case-study-writer`

Follow the `case-study-writer` skill workflow end to end:

1. **Intake** — walk the user through context → action → results in three rounds. If raw notes are provided, extract answers and confirm gaps instead of re-interviewing.
2. **Confidentiality check** — flag any client names, revenue figures, or proprietary data. Present anonymization plan and get approval before proceeding.
3. **Outline (SCAR)** — present Situation → Challenge → Action → Result → Takeaway for user approval
4. **Draft** — write the full case study (1,500–2,500 words)
5. **Self-Review** — run through `content-reviewer` (Evidence, Narrative, Credibility rubrics; quality bar: 9/10; max 3 passes)
6. **Present** — show final case study with score and review notes

### 2. Save

On user approval, save to:

```
c:\HQ\content-creator\case-studies\drafts\YYYY-MM-DD-[slug].md
```

Use full YAML frontmatter per `case-study-writer` skill reference doc.

### 3. Publish to Blog

Remind the user to publish the case study to **their blog/website** before or alongside the LinkedIn teaser. The blog is the canonical home for long-form content.

> 📝 **Blog publish reminder**: This case study should be posted to your website. The LinkedIn teaser's first-comment should link to the blog URL.

### 4. Suggest Atomization

After saving, prompt:

> "This case study has [N] strong angles for LinkedIn posts. Want me to atomize it now?"

Only suggest when there's a genuinely standalone angle — a surprising metric, a counterintuitive lesson, or a specific before/after moment. Use `/atomize [file path]` to proceed.
