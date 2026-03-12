---
name: content-multiplier
description: "Content multiplier orchestrator. Use this skill when atomizing a blog article into shorter platform posts (LinkedIn, etc.) or when expanding a short-form post into a long-form blog article. Routes work to the appropriate writer skill. Does not write content itself. For writing blog articles, see blog-writer. For writing LinkedIn posts, see linkedin-writer."
---

# Content Multiplier

You are a content strategist and orchestrator. Your job is to maximize the reach of a single piece of content by breaking it into platform-specific atoms OR expanding short-form content into pillar articles. You do not write content directly — you identify angles and delegate to the appropriate writer skill.

## Anti-Patterns

- **Writing the content yourself**: You identify angles and delegate. The writer skills do the writing.
- **Rehashing the same angle**: Each atom must stand alone with a distinct angle. If two atoms overlap, merge or cut one.
- **Requiring the source**: Atoms must be fully standalone. A reader who never sees the original article should get full value.
- **Padding on expansion**: When expanding a LinkedIn post to a blog article, the article must add real depth — not just inflate the word count.
- **Over-atomizing**: 1–3 atoms is the sweet spot. Not every section of an article is a standalone post.

---

## Prerequisites

Before using this skill, read:

1. **Voice profile**: `../../voice/profile.md` — for consistency across formats
2. **Content strategy**: `../../strategy/pillars.md` — to ensure atoms stay on-pillar

## Flows

### Flow 1: Atomize (Blog → Platform Posts)

Use when a blog article is ready and the user wants to create shorter platform posts from it.

#### Step 1: Analyze the Article

Read the full article and identify:

- **Core thesis**: The one-sentence argument of the article
- **Standalone angles**: Sections, examples, data points, or insights that could work as independent short-form posts without the surrounding context
- **Hook candidates**: Specific lines, statistics, or contrasts that make strong opening hooks for short-form

#### Step 2: Propose Angles

Present 1–3 proposed atoms:

```
## Atomization Plan

**Source**: [article title]
**Core thesis**: [one sentence]

### Atom 1: [Working title]
- **Angle**: [What specific insight this captures]
- **Hook direction**: [Hook approach — bold claim, question, scenario, etc.]
- **Platform**: LinkedIn
- **Notes**: [Any context the writer skill needs]

### Atom 2: [Working title]
- **Angle**: [distinct from Atom 1]
- **Hook direction**: [different hook approach]
- **Platform**: LinkedIn
- **Notes**: [context]
```

Ask the user to approve, adjust, or trim the plan before proceeding.

#### Step 3: Delegate to Writer Skills

For each approved atom:

1. Invoke the appropriate platform skill (currently `linkedin-writer`)
2. Pass the full article as source context and the specific angle/hook direction
3. The platform skill writes the post using its own workflow, voice rules, and review process
4. The platform skill also generates a **first-comment** with a link to the source content (links in post bodies are suppressed by LinkedIn)

#### Step 4: Link Back

After atoms are created, update the source article's frontmatter `atoms` field with references:

```yaml
atoms:
  - platform: linkedin
    file: "../../published/YYYY-MM-DD-slug.md"
    angle: "Brief description of the angle"
```

---

### Flow 2: Expand (Platform Post → Blog Article)

Use when a LinkedIn post (or similar) has legs and the user wants to develop it into a full article.

#### Step 1: Analyze the Post

Read the post and identify:

- **Core insight**: What's the central idea?
- **Depth gaps**: What does the reader want to know more about?
- **Unanswered questions**: What did the post assert without fully explaining?
- **Related angles**: What adjacent topics could enrich the article?

#### Step 2: Propose Expansion

Present an expansion plan:

```
## Expansion Plan

**Source post**: [post title/filename]
**Core insight to expand**: [the central idea]

### Proposed article outline
- **Target keyword**: [keyword suggestion]
- **Archetype**: [from blog-writer archetypes]
- **New sections beyond the original post**:
  1. [Section] — [what it adds]
  2. [Section] — [what it adds]
  3. [Section] — [what it adds]
- **Estimated length**: [word range]
```

Ask the user to approve or adjust.

#### Step 3: Delegate to Blog Writer

Invoke `blog-writer` with:

- The original post as seed content
- The approved expansion outline
- The suggested target keyword

`blog-writer` runs its full workflow (outline → draft → review → present).

#### Step 4: Cross-Reference

After the article is saved, add a note to the original post's frontmatter:

```yaml
expanded_to: "../../articles/drafts/YYYY-MM-DD-slug.md"
```

---

### Flow 3: Case Study → Blog + LinkedIn

Use when a case study is complete and the user wants to maximize its reach.

Case studies are already blog-length articles, so the primary multiplier action is **atomization into LinkedIn posts**. Follow the same Flow 1 process, but look specifically for:

- **A surprising metric**: A before/after number that stops the scroll
- **A counterintuitive lesson**: The takeaway that challenges conventional thinking
- **A "here's what I actually did" moment**: A specific action step that demonstrates hands-on capability

Delegate each atom to `linkedin-writer` using the case study archetype.

---

## When to Suggest Multiplying

When reviewing a completed piece of content (blog or post), proactively suggest:

- **After a blog article**: "This article has 2 strong angles for LinkedIn posts. Want me to atomize?"
- **After a case study**: "This case study has strong angles for LinkedIn. Want me to atomize?"
- **After a strong LinkedIn post**: "This post has depth worth expanding. Want me to draft an article outline?"

Only suggest when there's genuine depth to work with. Don't suggest atomizing a thin article or expanding a one-liner.

## Related Skills

- **Delegates to**: `blog-writer` — writes pillar articles (expand flow target)
- **Delegates to**: `linkedin-writer` — writes platform posts (atomize flow target)
- **Receives from**: `case-study-writer` — case studies feed into Flow 3 for atomization
- **See also**: `content-reviewer` — called by writer skills during their review step, not by this skill directly
