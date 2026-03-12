---
description: Atomize a blog article or case study into LinkedIn posts using content-multiplier → linkedin-writer → content-reviewer pipeline.
---

# /atomize — Content Atomization Workflow

Break a long-form piece (blog article or case study) into standalone LinkedIn posts that drive traffic back to the source.

## Prerequisites

Before starting, read these files (do NOT scan directories, paths are fixed):

1. `c:\HQ\content-creator\skills\content-multiplier\SKILL.md` — orchestration logic and angle identification
2. `c:\HQ\content-creator\skills\linkedin-writer\SKILL.md` — post writing rules and Atomize Mode
3. `c:\HQ\content-creator\skills\content-reviewer\SKILL.md` — scoring protocol and rubrics
4. `c:\HQ\content-creator\voice\profile.md` — voice fingerprint
5. `c:\HQ\content-creator\strategy\pillar.md` — content pillars and positioning
6. `c:\HQ\content-creator\strategy\algorithm.md` — LinkedIn algorithm rules
7. 2-3 relevant examples from `c:\HQ\content-creator\swipe-file\linkedin\` — for hook/structure patterns

## Input

The user provides a source file path to a blog article or case study.

## Steps

### 1. Analyze Source Content

Read the full source article/case study and identify:

- **Core thesis**: The one-sentence argument
- **Standalone angles**: Per `content-multiplier` Flow 3, look specifically for:
  - A **surprising metric** (a before/after number that stops the scroll)
  - A **counterintuitive lesson** (a takeaway that challenges conventional thinking)
  - A **"here's what I actually did" moment** (a specific action step that shows hands-on capability)
- **Hook candidates**: Lines, stats, or contrasts that make strong opening hooks

### 2. Propose Angles

Present 1-3 proposed atoms to the user using the format from `content-multiplier` Step 2:

```
## Atomization Plan

**Source**: [article/case study title]
**Core thesis**: [one sentence]

### Atom 1: [Working title]
- **Angle**: [specific insight]
- **Hook direction**: [bold claim, question, scenario, stat, etc.]
- **Platform**: LinkedIn
- **Notes**: [context for the writer]

### Atom 2: ...
### Atom 3: ...
```

**Wait for user approval** before proceeding. The user may cut, add, or adjust angles.

### 3. Write Posts

For each approved atom, invoke **`linkedin-writer` in Atomize Mode**:

- Pass the full source article as context
- Pass the specific angle and hook direction
- Follow all voice, structure, and algo rules
- Apply **cascading list pattern** to any bullet/emoji lists (logical order first; rewrite items to achieve the visual slope if needed)
- Generate a **first-comment** with a `[LINK]` placeholder that teases the source content from this post's specific angle
- Save each draft to `c:\HQ\content-creator\linkedin\drafts\YYYY-MM-DD-[slug].md`
- Include `first_comment` in the YAML frontmatter

### 4. Review Posts

Run each post through **`content-reviewer`** with the linkedin-writer rubrics:

```
rubrics:
  - name: Voice
    description: Matches voice profile. No corporate-speak, no AI tells, no over-explanation.
  - name: Structure
    description: Hook quality, paragraph length, CTA specificity, cascading lists, character count (800-1300), all structure rules.
  - name: Algo
    description: Clarity of topic, dwell-friendly formatting, no suppressed patterns (no hashtags, no em dashes, no in-post links).
quality_bar: 9
max_passes: 3
```

If any post scores below 9, rewrite and re-score (up to 3 passes). Present final scores.

### 5. Update Source Frontmatter

After all posts are drafted and reviewed, update the source article/case study's `atoms` field in its YAML frontmatter:

```yaml
atoms:
  - platform: linkedin
    file: "../../linkedin/drafts/YYYY-MM-DD-slug.md"
    angle: "Brief description of the angle"
```

### 6. Present Results

Present all posts to the user with:

- Final scores per post
- The first-comment text for each post
- A recommended publishing sequence (e.g., "Publish source article as LinkedIn Article first, then schedule atoms across 2 weeks")

## Output

When complete, the user will have:

- 1-3 LinkedIn post drafts in `c:\HQ\content-creator\linkedin\drafts\`
- Each post with a `first_comment` in frontmatter containing a `[LINK]` placeholder
- Source article frontmatter updated with atom cross-references
- Review scores for each post
