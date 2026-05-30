# Case Study Review Rubric

The canonical scoring system for case study drafts. All ad-hoc reviews and `/review-content` invocations for case studies use this rubric. No improvised dimensions, no alternative scales.

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
| `voice/voice-guide.md` | Anti-pattern blacklist, case study content-type lens (lines 62-76), case study checklist (lines 283-287), signature moves (especially Constraint-First Frame, Bridge and Burn, Operator's Confession) |
| `strategy/seo-guidelines.md` | SEO checks: keyword placement rules, meta description spec, heading hierarchy, E-E-A-T signals |

---

## Dimensions

### 1. Voice (X/10)

Does this sound like the author? Case studies have specific voice requirements beyond the shared fingerprint.

**Specific checks**:
- All shared anti-pattern blacklist checks (same as article rubric — correlatives, hedges, throat-clearing, false profundity, etc.)
- Tone is deliberate and methodical — slower pacing than articles. The reader should feel like they're watching someone think through a complex problem in real time
- **Action section voice consistency**: The most common drift point in case studies. The Situation reads like a story, the Challenge builds tension, then the Action section shifts to consultant-speak ("We implemented a phased rollout with cross-functional stakeholders..."). Flag any section where the register shifts from operator to consultant
- Opening uses analytical vulnerability — factual, not emotional. States what happened without self-pity or bravado
- Em dashes used sparingly (one per paragraph max)
- No corporate-speak, no methodology-deck language

**Voice guide lens reference** (lines 62-76):
- Deliberate, methodical tone throughout
- Honest reflection: at least one "here's what I'd do differently" or "here's where I was wrong" — always brief, specific, analytical
- Vulnerability is analytical, never performative

**Score anchors**:
- 10: Consistent operator voice from opening to close. Action section sounds like the same person who wrote the Situation. Zero blacklist violations. Vulnerability is analytical
- 7: Minor voice drift in Action section (one or two consultant-mode phrases). Blacklist mostly clean with 1-2 minor flags
- 5: Clear voice drift — Action section reads like a different author. Multiple blacklist violations. Vulnerability is performative or absent

### 2. Structure (X/10)

Does the case study follow the SCAR framework and build progressive discovery?

**Specific checks**:
- **SCAR framework compliance**: Situation → Challenge → Action → Result → Takeaway. All sections present and in order
- **Constraints shown before solution**: The constraint set appears early and prominently. It explains *why* decisions were made a certain way. "A $2,500/month ceiling immediately rules out a Zendesk Enterprise upgrade"
- **Diagnostic depth**: Shows the thinking, not just the result. Root cause analysis with specific data, named patterns, and evidence chains. "Everything in the data collapsed into four distinct problems"
- **"What I Would Not Build" section**: Explicit section showing restraint. Each "no" includes reasoning — not just "I chose not to" but "here's why the obvious choice was wrong in this context"
- **Argument progression (the reorder test)**: Could any two major sections swap without breaking the narrative? Each section must build on what came before
- **Section hand-offs**: The last sentence of each section raises the question the next section answers
- **Section length**: No section exceeds 300 words without H3 subdivision
- **Closing generalizes beyond the project**: The broader pattern — what this case teaches beyond itself. "Bad data. Every time."
- **Hook quality**: Opens with personal framing — why this exists, what was at stake. Not a generic problem statement

**Voice guide checklist reference** (lines 283-287):
- Constraints shown? ✓
- "What I didn't build" included? ✓
- Honest reflection? ✓

**Score anchors**:
- 10: Full SCAR with constraints before solution, restraint section with reasoning, diagnostic chain shown step by step, closing generalizes to a principle
- 7: SCAR structure present but constraints are buried in the Action section, or "What I Didn't Build" is thin (listed without reasoning)
- 5: Missing SCAR sections. Jumps from problem to solution without showing diagnostic thinking. No constraints or restraint section. Closing restates instead of generalizing

### 3. Evidence (X/10)

Are claims anchored in specific operational artifacts, not vague assertions?

Case study evidence is different from article evidence. Articles need named research sources. Case studies need named operational artifacts — the specific data, tools, metrics, and diagnostic chains from the real project.

**Specific checks**:
- **Before/after metrics**: Specific, quantified transformation. "Cut project delivery from 10+ weeks to under 4" — not "improved efficiency"
- **Named tools and systems**: Specific tools, platforms, and technologies mentioned by name
- **Timelines**: How long things took. Project duration, implementation phases, time-to-result
- **Diagnostic chains**: data → root cause → decision → outcome. Each step shown with specific evidence. "Everything in the data collapsed into four distinct problems" followed by the four problems with data
- **Contextualized numbers**: Numbers always include context. "$780,000 in annual attrition cost at ~$13,000 per departure" — not just "$780,000"
- **No vague metrics**: "Improved efficiency" is a failure. "Reduced onboarding from 45 days to 15" is the bar
- **Directional ranges acceptable**: When exact numbers aren't available, use ranges and say so. "Reduced by roughly 40-60%" is honest. "Significantly improved" is not
- **No fabricated data**: Every number must be from the actual project

**Score anchors**:
- 10: Full diagnostic chains on every major claim. Before/after metrics with context. Named tools and timelines throughout. Reader can reconstruct the project from the evidence alone
- 7: Most claims have evidence, but one diagnostic chain skips a step (jumps from data to decision without showing root cause). Metrics present but one lacks context
- 5: Vague metrics ("improved," "reduced," "streamlined"). No diagnostic chains. Claims asserted without operational evidence

### 4. SEO (X/10)

Will this case study perform in search? Same mechanical checks as articles — case studies are published to the blog.

> **Source of truth**: `strategy/seo-guidelines.md` defines the detailed rules. This dimension scores compliance against those rules.

**Specific checks** (from seo-guidelines.md):
- **Target keyword**: Present in title, first 100 words, at least 2 H2s, and the conclusion
- **Supporting keywords**: Distributed naturally through body sections
- **Meta description**: 145-155 characters, includes target keyword, compelling enough to click
- **Heading hierarchy**: Single H1 (the title), logical H2/H3 structure, no skipped levels
- **Readability**: Short paragraphs, sub-300 word sections, varied sentence length
- **E-E-A-T signals**: Experience (real project), Expertise (within declared pillars), Authoritativeness (specific evidence), Trustworthiness (honest reflection, gap acknowledgment)
- **Frontmatter completeness**: title, slug, target_keyword, supporting_keywords, meta_description, pillar, archetype, status, date fields present

**If frontmatter is missing or incomplete**: Score as "N/A — incomplete frontmatter" and average across the remaining four dimensions.

**Score anchors**:
- 10: Keyword placement natural and complete, meta description compelling, heading hierarchy clean, E-E-A-T signals strong (case studies naturally excel at Experience and Trustworthiness), frontmatter fully populated
- 7: Keyword present in most locations, meta description exists but is generic, one heading issue
- 5: Keyword missing from title or intro, no meta description, broken heading hierarchy

### 5. Editorial (X/10)

Has the draft been through a quality editing pass? Includes persona tests specific to case studies.

**Specific checks**:
- **Second-idea detection**: Does any section introduce a new transformation story rather than supporting the primary one? One case study = one core transformation. If you solved three problems, that's three case studies
- **Over-explanation**: State the point, give evidence, move on. Trust the reader
- **Subtraction quality**: Does the draft feel tight? Would cutting 10% improve it?
- **Repetition**: Does the same evidence or argument appear in multiple sections?
- **Confidentiality compliance**: No client names, proprietary data, or internal metrics published without explicit permission. Anonymization applied correctly where needed
- **Persona tests**:
  - **The Hiring Manager**: Would a VP of Operations want to call this person after reading? Does the diagnostic chain feel earned? Is the restraint credible?
  - **The Peer Operator**: Does this feel real? Are there enough specific details (tool names, ticket counts, timelines)? Does the Action section acknowledge constraints, false starts, or compromises?

**Score anchors**:
- 10: Tight throughout. Single transformation story. Both persona tests pass cleanly — Hiring Manager says "I'd call," Peer Operator says "this is real"
- 7: One minor redundancy. Persona tests pass but Peer Operator notes the Action section is slightly too clean (no constraints or compromises mentioned)
- 5: Multiple transformation stories competing. Hiring Manager says "generic." Peer Operator says "doesn't feel real — too polished"

---

## Output Format

Every case study review produces this exact structure:

```markdown
## Review: [Case Study Title]

**Score: X.X / 10** (Voice: X | Structure: X | Evidence: X | SEO: X | Editorial: X)
**Verdict**: [Publishable as-is | Publishable with minor edits | Needs revision | Needs restructuring]

### Dimension Breakdown

#### Voice (X/10)
[2-3 specific observations with line references. Note any Action section voice drift]

#### Structure (X/10)
[SCAR compliance, constraints placement, restraint section quality, diagnostic depth]

#### Evidence (X/10)
[Before/after metric count, diagnostic chain assessment, named tools/timelines]

#### SEO (X/10)
[Keyword placement check, meta description assessment, frontmatter status]

#### Editorial (X/10)
[Single-story check, persona test results (Hiring Manager + Peer Operator)]

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
