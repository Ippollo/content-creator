# Article Review Rubric

The canonical scoring system for long-form article drafts. All ad-hoc reviews and `/review-content` invocations use this rubric. No improvised dimensions, no alternative scales.

## Scale

Every dimension is scored `/10`. The final score is the unweighted average across all scored dimensions.

| Score | Meaning | Action Required |
|---|---|---|
| 10 | Exemplary — could go in the voice guide as a positive example | None |
| 9 | Publishable as-is | None |
| 8 | Publishable with minor edits (word-level fixes) | Optional polish |
| 7 | Needs revision in this dimension (paragraph-level rewrites) | Required fixes listed |
| 6 | Significant issues (section-level restructuring) | Required fixes listed |
| ≤5 | Fundamental problems (thesis, voice, or evidence architecture) | Required fixes listed |

**Quality bar**: 8.0 average = publishable with minor edits. 9.0 average = publishable as-is.

**Required fixes**: Any dimension scoring **≤7** must include specific, actionable fix instructions with line references. Fixes are instructions, not suggestions. The reviewer does NOT rewrite the draft.

---

## Prerequisites

The reviewer must load these files before scoring:

| File | What it provides |
|---|---|
| `voice/voice-guide.md` | Anti-pattern blacklist, article content-type lens (lines 42-57), signature moves, editorial process |
| `strategy/seo-guidelines.md` | SEO checks: keyword placement rules, meta description spec, heading hierarchy, E-E-A-T signals |

---

## Dimensions

### 1. Voice (X/10)

Does this sound like the author? Check against the voice fingerprint, not against generic "good writing."

**Specific checks**:
- Sentence length matches fingerprint: medium sentences with logical connectors, short punchy lines for emphasis
- Vocabulary is plain-spoken and accessible — technical terms used naturally, zero corporate-speak
- Tone is direct, confident, practical — operator explaining, not consultant presenting
- Anti-pattern blacklist scan (all items from voice guide):
  - No "Not X, but Y" correlative constructions
  - No hedges: "actually," "maybe," "just," "simply" (unless genuine intellectual hedging)
  - No throat-clearing: "It's worth noting that..." / "Interestingly..."
  - No summary endings that recap the post
  - No abstract analysis without personal stakes
  - No generic transitions: "That said," "Moreover," "Furthermore"
  - No boilerplate authority: "Studies show," "Experts agree"
  - Em dashes used sparingly (one per paragraph max)
  - No stacked adjectives: "innovative, cutting-edge, transformative"
  - No rhetorical questions as filler
  - No false profundity: "At the end of the day..." / "In today's rapidly evolving landscape..."
- Voice consistency: first two paragraphs and last body section sound like the same person wrote both
- No drift into consultant mode (passive voice increasing, abstract process language, methodology-deck phrases)

**Score anchors**:
- 10: Every sentence passes the "read it aloud" test. Zero blacklist violations. Unmistakably the author's voice throughout
- 7: 2-3 minor blacklist flags (editorializing adjective, one hedge). Voice is recognizable but not locked in
- 5: Consistent voice drift in one or more sections. Multiple blacklist violations. Reads like "good writing" but not like this specific author

### 2. Structure (X/10)

Does the article build an argument, or does it stack parallel points?

**Specific checks**:
- **Hook quality**: Opens with a specific number, scenario, or bold claim in the first 2-3 lines. Stakes clear by line 2. Not a question or abstraction
- **One idea**: The article serves a single thesis. No bolted-on second ideas
- **Argument progression (the reorder test)**: Could any two H2 sections swap positions without breaking the logic? If yes, the article has parallel sections, not progressive discovery. Each section must build on the previous one's conclusion
- **Section hand-offs**: The last sentence of each section raises the question the next section answers. No explicit transitions ("Furthermore," "That said," "Now let's look at...")
- **Section length**: No H2 section exceeds 300 words. Flag sections that need H3 subdivision
- **Paragraph length**: 2-4 sentences. Heavy whitespace
- **Closing quality**: One-line reframe or question. Never a summary paragraph. Never a recap. The question IS the conclusion
- **Sub-headers as hooks**: Each H2/H3 makes the reader want to read the section
- **Cascading lists**: Any lists create a visual slope — items progressively shorter or longer
- **Whitespace is intentional**: Paragraph breaks are pacing decisions, not random formatting

**Score anchors**:
- 10: Evidence Ladder executed perfectly. Every section builds on the previous. Reorder test: impossible to rearrange without breaking the argument
- 7: Structure is sound but one hand-off is weak, or two sections cover overlapping ground
- 5: Parallel sections that could be reordered. Hook is generic. Closing summarizes instead of reframing

### 3. Evidence (X/10)

Are claims anchored in named sources and personal proof points, or just asserted?

**Specific checks**:
- **Source count**: 3-5 distinct named sources for articles of 1,500+ words. A single citation in a 2,000-word authority piece is thin
- **Source specificity**: Named reports, specific years, specific numbers. "Deloitte surveyed 3,235 leaders" is the bar. "Studies show" is a failure
- **Operational Proof Chain**: Three beats per major claim: (1) named research source, (2) personal experience anchor, (3) reader implication. Two beats feels thin. Three beats feels authoritative
- **No unanchored claims**: Any assertion over one sentence needs either a named source or a personal proof point. "Most companies struggle with X" requires a citation or specific story
- **Source quality at bottom**: Sources section uses named reports with years, not vague references. Cited inline by name and year, collected at the bottom in italics
- **No fabricated stats**: If a number appears, it must be attributable to a named source

**Score anchors**:
- 10: 4+ named sources, full proof chains on every major claim, source section is publication-grade
- 7: 2-3 named sources, proof chains present but one claim has only two beats, source section exists but is loosely cited
- 5: Single source or unnamed sources ("studies show"), multiple unanchored claims, no source section

### 4. SEO (X/10)

Will this article perform in search? Check mechanical placement and structural optimization.

> **Source of truth**: `strategy/seo-guidelines.md` defines the detailed rules. This dimension scores compliance against those rules — it does not restate them. Load the file before scoring.

**Specific checks** (from seo-guidelines.md):
- **Target keyword**: Present in title, first 100 words, at least 2 H2s, and the conclusion
- **Supporting keywords**: Distributed naturally through body sections (not stuffed)
- **Meta description**: 145-155 characters, includes target keyword, compelling enough to click
- **Heading hierarchy**: Single H1 (the title), logical H2/H3 structure, no skipped levels
- **Readability**: Short paragraphs, sub-300 word sections, varied sentence length
- **E-E-A-T signals**: Experience (real projects), Expertise (within declared pillars), Authoritativeness (concrete data, frameworks), Trustworthiness (honest about limitations)
- **FAQ placement**: After conclusion, before sources. Never mid-article
- **Frontmatter completeness**: title, slug, target_keyword, supporting_keywords, meta_description, pillar, archetype, search_intent, status, date fields present

**If frontmatter is missing or incomplete**: Score as "N/A — incomplete frontmatter" and average across the remaining four dimensions. Note specifically which fields are missing.

**Score anchors**:
- 10: Keyword placement is natural and complete, meta description is compelling, heading hierarchy is clean, E-E-A-T signals strong, frontmatter fully populated
- 7: Keyword present in most required locations, meta description exists but is generic, one heading hierarchy issue
- 5: Keyword missing from title or intro, no meta description, broken heading hierarchy, no E-E-A-T signals

### 5. Editorial (X/10)

Has the draft been through a quality editing pass? This catches what the other dimensions don't.

**Specific checks**:
- **Second-idea detection**: Does any section introduce a new argument thread rather than supporting the primary one? A section fails if you can remove it and the core argument still stands complete
- **Over-explanation**: If a line makes a point and the next line re-explains in different words, the second line should be cut
- **Subtraction quality**: Does the draft feel tight, or is there visible bloat? Would cutting 10% improve it?
- **Repetition**: Does the same argument appear in multiple sections phrased differently? (This is distinct from callbacks, which are intentional)
- **Named specifics density**: Does the draft include real tools, timelines, metrics, or named frameworks? Or does it operate in abstractions?
- **Persona tests**:
  - The Skeptical Reader: Does this article prove its thesis with evidence, or just assert it repeatedly?
  - The Skim Reader: Can someone read just the H2s, first sentences, and closing and get the core argument?

**Score anchors**:
- 10: Tight throughout. Zero bloat. Every section earns its place. Both persona tests pass cleanly
- 7: One section is slightly redundant or one over-explanation instance. Persona tests pass with minor notes
- 5: Visible bloat, repeated arguments across sections, skim reader can't follow the argument from headers alone

---

## Output Format

Every review produces this exact structure. No ad-hoc tables, no invented categories, no alternative formats.

```markdown
## Review: [Article Title]

**Score: X.X / 10** (Voice: X | Structure: X | Evidence: X | SEO: X | Editorial: X)
**Verdict**: [Publishable as-is | Publishable with minor edits | Needs revision | Needs restructuring]

### Dimension Breakdown

#### Voice (X/10)
[2-3 specific observations with line references]

#### Structure (X/10)
[2-3 specific observations with line references]

#### Evidence (X/10)
[Named source count, proof chain assessment, source section quality]

#### SEO (X/10)
[Keyword placement check, meta description assessment, frontmatter status]

#### Editorial (X/10)
[Second-idea detection, over-explanation scan, persona test results]

### Required Fixes
[For any dimension scoring ≤7, list specific, actionable fix instructions]

1. **[Dimension]** — [Exact issue with line reference] → [Exact instruction to fix it]
2. **[Dimension]** — [Exact issue with line reference] → [Exact instruction]
3. [Continue as needed]

[If all dimensions score ≥8, this section reads: "No required fixes. Minor polish opportunities noted above."]
```

### Verdict Mapping

| Average Score | Verdict |
|---|---|
| ≥ 9.0 | Publishable as-is |
| 8.0 – 8.9 | Publishable with minor edits |
| 6.0 – 7.9 | Needs revision |
| < 6.0 | Needs restructuring |
