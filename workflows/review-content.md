---
description: Review and score a content draft against the standardized rubric. Use when asked to "review," "score," "rate," or "evaluate" any article, case study, or long-form draft.
---

# /review-content — Content Quality Review

Scores a draft against the canonical rubric for its content type. Review-only — does not rewrite the draft. Produces a standardized scorecard with required fix instructions for any dimension scoring ≤7.

## Anti-Patterns

- **Inventing rubric dimensions** — use the canonical rubric for the content type. No ad-hoc categories, no alternative scales.
- **Scoring on a different scale** — every dimension is scored /10. Not /13, not /100, not pass/fail. The rubric file defines the scale.
- **Rewriting the draft during review** — this workflow diagnoses. It does not fix. Fix instructions tell the user what to change; the user decides when and how.
- **Inflating scores** — if the evidence is thin, score it honestly. A 7 with clear fix instructions is more useful than a generous 9 that hides problems.
- **Skipping line references** — every observation and fix instruction must reference specific lines in the draft.
- **Running a subtraction pass but not reporting it** — if the draft would benefit from cutting, name what to cut and why.

## Prerequisites

Before scoring, ensure you are in the root of your `content-creator` repository. All paths listed below are relative to the repository root. Silently load:

1. **Voice guide**: `voice/voice-guide.md` — fingerprint, anti-patterns, content-type lenses, signature moves
2. **Rubric**: Load the rubric matching the content type (see Rubric Selection below)
3. **Strategy file** (content-type-specific):
   - Articles & Case Studies: `strategy/seo-guidelines.md`
   - LinkedIn posts: `strategy/algorithm.md`

## Rubric Selection

Detect content type from the draft's frontmatter or file path:

| Signal | Content Type | Rubric Path |
|---|---|---|
| `pillar` field present, file in `articles/` | Article | `skills/content-reviewer/rubrics/article.md` |
| File in `case-studies/` | Case Study | `skills/content-reviewer/rubrics/case-study.md` |
| File in `linkedin/` | LinkedIn Post | `skills/content-reviewer/rubrics/linkedin.md` |

If no rubric file exists for the detected content type, default to the **article** rubric and note this in the review output.

## Steps

### 1. Read the Draft

Read the full draft file. Note the frontmatter fields, word count, section structure, and source count.

### 2. Read the Rubric

Load the matching rubric file. This defines the exact dimensions, specific checks, scoring guidance, and output format. Follow it exactly.

### 3. Score Each Dimension

For each dimension in the rubric:
1. Run every specific check listed for that dimension
2. Note specific observations with line references
3. Assign a score using the rubric's score anchors and scale definitions
4. For any dimension scoring ≤7, draft the required fix instruction (what to change, where, why)

### 4. Compute the Average

Average all scored dimensions. If any dimension is N/A (e.g., SEO with missing frontmatter), average across the remaining dimensions and note the exclusion.

### 5. Determine the Verdict

Map the average score to the verdict using the rubric's verdict mapping table.

### 6. Present the Scorecard

Output the review using the **exact output format** defined in the rubric file. No deviations.

Dimension names vary by content type:
- **Articles & Case Studies**: Voice, Structure, Evidence, SEO, Editorial
- **LinkedIn**: Voice, Structure, Algorithm, Specificity, Editorial

The format is always:

```
## Review: [Title]

**Score: X.X / 10** ([Dim1]: X | [Dim2]: X | [Dim3]: X | [Dim4]: X | [Dim5]: X)
**Verdict**: [from verdict mapping]

### Dimension Breakdown
[Per-dimension observations with line references]

### Required Fixes
[For dimensions ≤7: specific, actionable instructions with line references]
```

Do not summarize the draft content in chat. The scorecard IS the output.

## Scope

This workflow covers review of a single draft per invocation. For batch reviews, invoke once per draft.

## Related

- **Uses**: `content-reviewer` skill rubrics (`rubrics/article.md`, etc.)
- **Complements**: `/write-article` — that workflow creates drafts; this one reviews them
- **Voice reference**: `voice-guide.md` — the source of truth for voice fingerprint and anti-patterns
