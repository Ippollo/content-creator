# LinkedIn Post Review Rubric

The canonical scoring system for LinkedIn post drafts. All ad-hoc reviews and `/review-content` invocations for LinkedIn posts use this rubric. No improvised dimensions, no alternative scales.

## Scale

Every dimension is scored `/10`. The final score is the unweighted average across all scored dimensions.

| Score | Meaning | Action Required |
|---|---|---|
| 10 | Exemplary — could go in the voice guide as a positive example | None |
| 9 | Publishable as-is | None |
| 8 | Publishable with minor edits (word-level fixes) | Optional polish |
| 7 | Needs revision in this dimension (paragraph-level rewrites) | Required fixes listed |
| 6 | Significant issues (structural rewrite) | Required fixes listed |
| ≤5 | Fundamental problems (hook, voice, or core concept) | Required fixes listed |

**Quality bar**: 8.0 average = publishable with minor edits. 9.0 average = publishable as-is.

**Required fixes**: Any dimension scoring **≤7** must include specific, actionable fix instructions with line references. Fixes are instructions, not suggestions. The reviewer does NOT rewrite the draft.

---

## Prerequisites

The reviewer must load these files before scoring:

| File | What it provides |
|---|---|
| `voice/voice-guide.md` | Anti-pattern blacklist, LinkedIn content-type lens (lines 25-38), signature moves (especially Pattern Interrupt, Before/After) |
| `strategy/algorithm.md` | Algorithm dimension checks: suppressed patterns, engagement signals, format guidelines, banned formats |

---

## Dimensions

### 1. Voice (X/10)

Does this sound like the author? Same fingerprint, compressed for short-form.

**Specific checks**:
- All shared anti-pattern blacklist checks (correlatives, hedges, throat-clearing, false profundity, etc.)
- No em dashes (—) — they read as AI-generated. Use a period, comma, or restructure
- No "I" as a lazy opener ("I think...", "I've been reflecting..."). Leading with "I" + specific credible action is valid ("I built...", "I tracked...")
- No emojis in the first line
- Vocabulary is plain-spoken — if a word wouldn't come up in conversation with a friend, replace it (except domain-specific technical terms)
- Tone is direct, confident, practical — operator energy, not thought leader polish
- No corporate-speak or AI tells

**Voice guide lens reference** (lines 25-38):
- Hook style: pattern interrupt or bold claim in first 1-2 lines
- Transition phrase: "Here's how..." or "Here's what..." to bridge hook to body
- Paragraph length: 1-2 sentences per paragraph, heavy whitespace
- Specificity: concrete numbers, tools, timelines — never vague
- Second person: addresses reader directly
- Closing: ends abruptly on mic-drop thought or reframe. No engagement questions. No CTAs

**Score anchors**:
- 10: Every sentence passes the "read it aloud" test. Zero blacklist violations. Unmistakably the author. Plain language throughout
- 7: 1-2 minor blacklist flags (one hedge, one slightly formal word choice). Voice recognizable but not locked in
- 5: Multiple blacklist violations. Reads like a polished ghostwriter, not the specific author. Corporate-speak present

### 2. Structure (X/10)

Does the post stop the scroll, deliver one idea, and land the ending?

**Specific checks**:
- **Character count**: 800-1,300 characters unless explicitly specified otherwise
- **Hook stops the scroll**: First 1-2 lines use a pattern interrupt, bold claim, surprising number, or contradiction. The reader must need to click "See more"
- **Paragraph shape**: 1-3 sentences max per paragraph. Blank lines between paragraphs
- **Visual variety**: Mix of single-line statements, 2-sentence paragraphs, and labeled blocks. No monotonous paragraph rhythm
- **Cascading lists**: Any emoji-bullet lists create a visual slope — items progressively shorter or longer. Logical/narrative order takes priority; rewrite items to hit the cascade
- **Scan test**: Post has visible rhythm when viewed as a shape — not a uniform block of text
- **Diagnosis OR solution**: The post either diagnoses a problem or presents a solution. Not both. If the solution requires jargon, let the post be the diagnosis
- **One idea**: Single core argument. No bolted-on second ideas
- **Closing quality**: Mic-drop thought or reframe. No engagement questions. No CTAs. No summary. State the final insight and stop
- **No stacked paraphrases**: If two consecutive paragraphs say the same thing in different words, cut one
- **Concrete anchor**: At least one specific number, named tool, timeline, or dollar amount

**Score anchors**:
- 10: Hook forces a "See more" click. Visual rhythm is excellent. One clean idea, mic-drop close. Within character count
- 7: Hook works but isn't a true pattern interrupt (more of a setup than a contradiction). Structure sound but one paragraph could be cut. Within character count
- 5: Hook is generic or buried. Wall of text with no visual variety. Tries to diagnose AND solve. Closing fades out or wraps up neatly

### 3. Algorithm (X/10)

Will LinkedIn's algorithm distribute this post? Check against suppressed patterns and format guidelines.

> **Source of truth**: `strategy/algorithm.md` defines the detailed rules. This dimension scores compliance against those rules — it does not restate them. Load the file before scoring.

**Specific checks** (from algorithm.md):

Suppression checks (binary — any violation is a significant deduction):
- **No hashtags** — no longer a distribution lever, actively suppressed
- **No em dashes** — widely recognized AI pattern, suppressed
- **No external links in post body** — links suppress reach. Use first-comment for links
- **No ugcPost reshares** — always convert to original content (banned format)
- **No standalone third-party story hooks** — gets reach but near-zero engagement (banned format)
- **No pure AI-trend commentary** — without personal experience attached (banned format)

Distribution checks (quality gradient):
- **Topic clarity** — post clearly communicates what it's about and who it's for
- **Niche consistency** — aligned with declared expertise (pillars)
- **Dwell-friendly formatting** — structured for reading depth, not just scanning
- **Problem-solving value** — solves a specific problem, shares a framework, or breaks down a process

**Score anchors**:
- 10: Zero suppressed patterns. Topic clear, niche-aligned, structured for dwell time. Reader would save or comment
- 7: Zero suppressed patterns. Topic clear but niche alignment is loose (pillar-adjacent, not pillar-direct). Formatting is fine but not optimized for dwell
- 5: One or more suppressed patterns present (hashtags, em dashes, or link in body). Or: uses a banned format (reshare, third-party story, pure AI commentary)

### 4. Specificity (X/10)

Does the post anchor its claims in concrete details, or operate in abstractions?

LinkedIn posts don't need 3-5 research sources like articles. They need one concrete anchor that makes the post feel real and specific.

**Specific checks**:
- **Concrete anchor present**: At least one specific number, named tool, timeline, or dollar amount. "47 employees" not "many employees." "2 hours a day" not "a lot of time." Every top-performing post in the analytics includes a concrete anchor
- **No unverified stats**: If a number or statistic appears, it must be attributable to a named source. If you can't name the source, rewrite without the number
- **No vague claims**: "Most companies struggle with X" needs either a source or a specific story. In short-form, a specific story is usually stronger than a citation
- **Personal proof point**: If the post claims an insight, does it anchor in personal experience? "I built..." / "I tracked..." / "In my portfolio of 75 clients..." Not required for every post, but preferred
- **Case study hooks use transformation, not setup**: Don't open with situation ("I took over a chaotic process"). Lead with the delta ("The team had been shipping late for 6 months. After 3 weeks, we cut delivery time by 60%")

**Score anchors**:
- 10: Strong concrete anchor. Claims grounded in personal experience with specific details. No vague assertions
- 7: Concrete anchor present but thin (one number without context). One claim could be more specific
- 5: No concrete anchor. Operates in abstractions ("many companies," "significant improvement"). Reads like a template filled with plausible generalizations

### 5. Editorial (X/10)

Has the draft been through a quality editing pass?

**Specific checks**:
- **Second-idea detection**: Does the post try to make two separate points? If a section introduces a new argument thread, flag it. Good LinkedIn posts have one core argument
- **Over-explanation**: If a line makes a point and the next line re-explains it in different words, the second line should be cut. Trust the reader
- **Stacked paraphrases**: "You become the memory" followed by "you become the integration layer" — cut one. Each paragraph must advance the argument
- **Subtraction quality**: Does the post feel tight? Could any paragraph be removed without losing the core argument?
- **First-comment check** (atomize mode only): If the post has a first-comment, does it add context or tease depth? Is the `[LINK]` placeholder present? Is it relevant to the post's specific angle, not generic?
- **Formatting compliance**: No hashtags in the body, no emojis in the first line, no em dashes (cross-check with Algorithm dimension)

**Score anchors**:
- 10: Tight throughout. Every paragraph advances the argument. Zero redundancy. Subtraction pass would find nothing to cut
- 7: One paragraph is slightly redundant or one over-explanation. Could be tightened by one line
- 5: Visible bloat. Two or more stacked paraphrases. Second idea bolted on. Could cut 20%+ without losing the argument

---

## Output Format

Every LinkedIn post review produces this exact structure:

```markdown
## Review: [Post Title or First Line]

**Score: X.X / 10** (Voice: X | Structure: X | Algorithm: X | Specificity: X | Editorial: X)
**Verdict**: [Publishable as-is | Publishable with minor edits | Needs revision | Needs restructuring]

### Dimension Breakdown

#### Voice (X/10)
[2-3 specific observations with line references]

#### Structure (X/10)
[Hook quality, character count, visual rhythm, closing quality]

#### Algorithm (X/10)
[Suppression pattern check, distribution signal assessment]

#### Specificity (X/10)
[Concrete anchor assessment, claim grounding]

#### Editorial (X/10)
[Second-idea check, over-explanation scan, tightness assessment]

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
