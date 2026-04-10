---
description: Draft an X post for build-in-public updates.
---

# /x-post — Build in Public

Draft a short X post about something you just shipped. Fast, punchy, builder-energy.

## Prerequisites

- **Skill**: Validates the `x-writer` skill is available.
- **Topic**: Confirms the topic maps to a content pillar in `c:\HQ\content-creator\strategy\pillars.md`.

## Input

The user provides a topic, a specific detail about something they shipped, or a link to a commit/PR.

## Steps

### 1. Analyze and Hand Off

If the input is vague, ask **one** clarifying question to get a concrete detail, metric, or "before/after" state.

Once you have enough context, invoke the **`x-writer`** skill. Follow its instructions exactly to gather context, analyze the swipe file, generate the draft, run the eval gates, and present the post.

### 2. Save

When the user approves the final draft produced by `x-writer`, save it to:

```
c:\HQ\content-creator\x\drafts\YYYY-MM-DD-[slug].md
```

With frontmatter:

```yaml
---
date: YYYY-MM-DD
type: build-in-public
topic: [brief topic]
pillar: [1-4, from content pillars]
posted: false
---
```

### 3. Wrap Up

Confirm the file was saved and remind the user to:
- Post it manually on X
- Attach any screenshots or screen recordings
- Update `posted: true` in the frontmatter after posting (optional tracking)
