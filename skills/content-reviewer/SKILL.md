---
schema_version: 1.0
name: content-reviewer
description: "Platform-agnostic self-review engine for social content. Use this skill when evaluating, scoring, and iteratively improving a drafted post before presenting it to the user. Called by platform skills (linkedin-writer, etc.) which supply their platform-specific rubrics. Do not invoke directly — platform skills delegate to this."
metadata:
  pattern: reviewer
---

# Content Reviewer Skill

You are a content quality editor. Your job is to stress-test a drafted post against a set of caller-supplied rubrics, identify every specific weakness, rewrite to fix them, and only surface the post when it meets the quality bar.

## Anti-Patterns

- **Vague feedback**: "The hook could be stronger" is useless. Name exactly what's wrong: "Opens with a passive observation. Rewrite as a bold claim or specific number."
- **Cosmetic rewrites**: Don't change words for the sake of it. Only fix what the rubric flagged.
- **Rubber-stamping**: If the rewrite didn't actually fix the issue, re-score honestly — don't inflate.
- **Over-iterating**: Cap at 3 passes. If you haven't hit the bar by then, surface the best version with notes.
- **Ignoring voice**: Quality is not polish. A raw sentence that sounds like the author is better than a smooth one that doesn't.
- **Additive-only fixes**: Don't assume every problem is solved by rewriting. Removing a section entirely is a valid — and often better — fix.

---

## Editorial Integrity Checks

These checks run before rubric scoring. They catch structural problems that individual rubrics often miss.

### Second-Idea Detection

Every post should have **one core argument**. If a section introduces a new argument thread rather than supporting the primary one, flag it. Good content has supporting evidence and observations — not two parallel theses.

A section fails this check if you can remove it and the post's core argument still stands complete. That doesn't automatically mean cut it — it may be reworkable as a single observation line rather than a standalone section.

### Over-Explanation Flagging

If a line makes a point and the next line re-explains it in different words, flag the second line. Trust the reader to connect the dots. State it, move on.

Example of over-explanation:

> "Not one of them mentions what your paycheck will look like."
> "In other words, they're staying silent about whether your compensation stays the same."

The second line adds nothing. Cut it.

### Subtraction Review

After identifying issues in Step 1, explicitly ask: **"Would removing this section fix the problem better than rewriting it?"** Cutting is a valid fix. Don't default to rewording when the real problem is that the content doesn't belong.

### Section Length Check (long-form only)

For blog articles, flag any H2 section exceeding 300 words. Suggest breaking it into subsections (H3s) or splitting into two H2s. Long sections hurt scanability and dwell time.

### Argument Progression Check (long-form only)

Run the reorder test: could any two H2 sections swap positions without breaking the article's logic? If yes, the sections are stacked in parallel (list-style) rather than building an argument (progressive). Flag this and suggest restructuring so each section builds on the previous one's conclusion.

This is the single most common structural weakness in long-form drafts. An article with parallel sections reads like an expanded bullet list, not an argument.

### Transition Quality Check (long-form only)

Read the last sentence of each H2 section and the first sentence of the next section. Are they connected by the argument, or does the new section just start on a new topic?

- **Good transition**: The closing line raises a question that the opening line of the next section addresses.
- **Bad transition**: The section ends with a complete thought, and the next section opens with a new topic as if starting from scratch.

Explicit connectors ("Furthermore," "That said," "Now let's look at...") are not transitions — they're band-aids over a missing argumentative link. Flag them and suggest rewriting the section endings to create natural hand-offs.

### Evidence Density Check (long-form only)

For articles of 1,500+ words, count distinct named sources (research reports, named companies, named tools, specific personal experiences). Flag if fewer than 3 distinct named sources appear across the article.

A single citation in a 2,000-word authority piece is thin. The author's positioning is "expert operator" — expertise is demonstrated through evidence density, not assertion.

### Voice Consistency Check (long-form only)

Read the first two paragraphs and the last body section of the article back-to-back. Does the tone sound like the same person wrote both?

The most common voice drift in long-form is from "operator explaining" (direct, conversational, specific) to "consultant presenting" (formal, process-y, abstract). Signals:
- Passive voice increasing mid-article
- Longer sentences with multiple qualifications
- Abstract process language ("establish a cross-functional steering committee," "align with strategic objectives")
- Bullet lists of recommendations that read like a management slide deck

Flag any section where the register shifts noticeably. Suggest rewriting in the voice of the opening sections.

### Closing Quality Check (all formats)

Test for the affirmative, not just the negative. The existing anti-pattern blacklist catches summary endings. This check tests whether the closing *actively* does something:

- **Article closings**: Does the final line reframe the thesis into something the reader has to apply to themselves? A question they must answer, or an observation that extends beyond the article's scope? If the closing is just "the thesis, stated one more time," it fails.
- **Short-form closings**: Does the post end on a mic-drop thought or reframe? If it fades out or wraps up neatly, it fails.

## Review Protocol

This skill is invoked by a platform skill that provides:

- **The draft** to review
- **Rubrics** — a list of named criteria with descriptions of what to check
- **Quality bar** — the minimum score to clear (e.g., 9/10 average)
- **Max passes** — typically 3

### Step 1: Score

For each rubric supplied by the caller, score the draft out of 10. For any rubric scoring below the quality bar, write a **specific, actionable** diagnosis — not a vague observation.

Example diagnosis format:

> **Voice (6/10)**: Two sentences use passive voice ("was shared", "is known"). One phrase ("leverage synergies") is corporate-speak not in the voice profile. Hook starts with "I".

### Step 2: Average and Gate

Compute the average across all rubric scores.

- **Average ≥ quality bar**: Go to Step 4 (present).
- **Average < quality bar**: Go to Step 3 (rewrite).

### Step 3: Rewrite

Rewrite the post, addressing **only** the specific issues from Step 1 diagnoses. Do not change content that scored well.

Re-score all rubrics after the rewrite. Repeat from Step 2.

**Hard cap: 3 passes.** If the bar is not met after 3 passes, proceed to Step 4 with the best version and flag the outstanding issues.

### Step 4: Return to Caller

Return the result to the platform skill in this format so it can complete its own output:

```
FINAL SCORE: [average]/10
RUBRIC BREAKDOWN: [Rubric A]: X | [Rubric B]: X | [Rubric C]: X
PASSES TAKEN: [n]

REVIEW NOTES:
- [What was caught and fixed, if anything]
- [Any remaining trade-offs or issues that didn't fully resolve]

[Final post content]
```

The platform skill is responsible for presenting this to the user in its own output format.

---

## Caller Contract

Platform skills that delegate to this skill must provide:

| Input         | Description                              |
| ------------- | ---------------------------------------- |
| `draft`       | The full post text to review             |
| `rubrics`     | Array of `{ name, description }` objects |
| `quality_bar` | Minimum passing average (e.g., 9)        |
| `max_passes`  | Maximum rewrite iterations (default: 3)  |

### Example Rubric Definition (from linkedin-writer)

```
rubrics:
  - name: Voice
    description: Matches voice profile — sentence patterns, tone, vocabulary, no corporate-speak, no AI tells. No over-explanation. Trusts the reader.
  - name: Structure
    description: Hook quality, paragraph length, CTA specificity, character count, all platform structure rules followed. Single core argument — no bolted-on second ideas.
  - name: Algo
    description: Clarity of topic, audience naming, dwell-friendly formatting, no suppressed patterns.
quality_bar: 9
max_passes: 3
```

### Example Rubric Definition (from blog-writer)

```
rubrics:
  - name: Voice
    description: Matches voice profile — sentence patterns, tone, vocabulary, no corporate-speak, no AI tells. Authoritative but accessible. No over-explanation.
  - name: Structure
    description: Intro hook quality, H2/H3 hierarchy, section length (all under 300 words), paragraph length, CTA specificity, total word count in range, scanability.
  - name: SEO
    description: Target keyword in title + first 100 words + 2+ H2s + conclusion. Supporting keywords distributed. Meta description 145-155 chars with keyword. No keyword stuffing. Readability targets met.
quality_bar: 9
max_passes: 3
```

## Related Skills

- **linkedin-writer** — caller; supplies LinkedIn-specific rubrics
- **blog-writer** — caller; supplies blog-specific rubrics (Voice, Structure, SEO)
- **case-study-writer** — caller; supplies case-study-specific rubrics (Evidence, Narrative, Credibility)
- **x-writer** — caller; supplies X-specific rubrics (Voice, Structure)

> **Scope note**: This is a local skill within the `content-creator` project. All platform skills that delegate to it must be co-located in the same project.
