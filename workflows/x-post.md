---
description: "Draft an X post about something you just shipped — a feature, system, workflow, or tool. Build-in-public format. Use when you've completed work and want to capture it as a short X post. Not for LinkedIn (use /atomize) or long-form content (use /write-article)."
---

# /x-post — Build in Public

Draft a short X post about something you just shipped. Fast, punchy, builder-energy.

## Anti-Patterns

- **Writing a LinkedIn post for X** — no hooks-and-CTA formula, no engagement questions, no emoji bullets. X is terse and direct.
- **Over-explaining** — the reader should get it in one pass. If you need to explain the context, you've scoped too wide.
- **Corporate voice** — "Excited to announce" or "Thrilled to share" are instant credibility kills on build-in-public X.
- **Threads by default** — default to a single post. Only thread if there's a genuine step-by-step or before/after that needs space.

## Prerequisites

Before drafting, silently load:

1. `c:\HQ\content-creator\voice\voice-guide.md` — voice fingerprint (adapt for X: shorter, more casual)
2. `c:\HQ\content-creator\strategy\pillars.md` — confirm the topic maps to a content pillar

## Input

The user describes what they shipped. This can be:

- A feature name and what it does ("Just built a Discord bot that lets me control Antigravity from my phone")
- A quick summary of the outcome ("Automated my LinkedIn publishing workflow end-to-end")
- A link to a commit, PR, or file that was just created
- A problem → solution arc ("Was spending 10 min per post scheduling. Built a /publish workflow that does it in 30 seconds")

## Steps

### 1. Understand the Ship

If the input is vague, ask **one** clarifying question. Otherwise, identify:

- **What was built**: The specific feature, system, or tool
- **Why it matters**: The problem it solves or the outcome it enables
- **What's interesting**: The angle that makes this worth posting — a surprising metric, an unconventional approach, a before/after contrast

### 2. Draft the Post

Write a single X post (≤ 280 characters) following these X-specific rules:

**Format**:
- Default: Single post, ≤ 280 characters
- If the idea genuinely needs more room: short thread (2–3 posts max), each ≤ 280 characters
- Line breaks are pacing tools, same as LinkedIn — but fewer of them

**Voice adaptation** (from the voice guide, tuned for X):
- Even shorter sentences than LinkedIn. Fragments are fine.
- First-person, present tense: "Just shipped..." / "Built a..." / "New workflow:"
- Concrete and specific — name the tool, the metric, the before/after
- Casual but not sloppy. No hashtags unless genuinely useful for discovery.
- Screenshots or short videos strongly encouraged — mention this in the draft notes

**What makes a good build-in-public post**:
- Shows the work, not just the result ("Built X using Y" > "X is now live")
- Shares a specific detail that signals real building ("280 lines of workflow YAML" / "3 MCP servers wired together")
- Invites curiosity without begging for engagement

**Structure options** (pick whichever fits):
- **The Ship Log**: "Just shipped [thing]. [One sentence on what it does]. [One sentence on why]."
- **The Before/After**: "[Problem in one line]. Built [solution]. [Result]."
- **The Stack Note**: "New [thing] in my [system]: [what it does]. Built with [tools/approach]."
- **The Lesson**: "TIL while building [thing]: [specific insight]."

### 3. Present Draft

Show the user:

```
## X Post Draft

[The post text]

---

**Characters**: [count]/280
**Visual suggestion**: [screenshot idea, if applicable]
**Thread**: No / Yes (N posts)
```

Wait for user approval. The user may edit, request a rewrite, or approve as-is.

### 4. Save

On approval, save to:

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

### 5. Wrap Up

Confirm the file was saved and remind the user to:
- Post it manually on X
- Attach any screenshots or screen recordings
- Come back and set `posted: true` in the frontmatter after posting (or don't — it's optional tracking)
