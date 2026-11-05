---
schema_version: 1.0
name: content-week-preflight
description: "Week-level preflight gate for a scheduled week of posts before publishing. Use when locking a week's editorial calendar, before running /publish, or when the user asks to check a week before it goes out. Catches cross-post failures that single-post review cannot see: duplicate openers, stale time references, repeated arguments, and unverified news pegs. For single-post scoring, see content-reviewer. For scheduling, see content-calendar."
metadata:
  pattern: reviewer
---

# Content Week Preflight

Per-post review catches per-post problems. This skill catches the failures that only appear when a **whole scheduled week is examined at once**: two posts opening the same way, two posts making the same argument, a stale news peg, or a claim that was true when drafted and is no longer true on the publish date.

Run after every post in a week is individually approved, and before `/publish`.

## Anti-Patterns

- **Reviewing posts one at a time** - that is `content-reviewer`'s job and it already happened. Every check here is a comparison *between* posts, or against the publish date. Reading one draft in isolation produces false passes.
- **Treating prior approval as evidence** - approval covers content quality. These checks cover conditions that changed after approval, or that only exist across posts. A post can be well-written and out of date at the same time.
- **Marking a check PASS that did not run** - use UNVERIFIED and say why. A silent pass on a currency check is how stale claims ship.
- **Fixing content during preflight** - this is a gate. Flag the issue, name the fix, let the author decide.
- **Running before the week is fully drafted** - a partial week cannot be checked for duplicates.

## Why This Exists

Every check below is derived from a real failure that passed single-post review and was caught by the author instead:

- Two posts in the same week opened with an identical line, because the same temporal fix was applied to both in one editing pass.
- A post drafted during a prior life stage (a job search) was scheduled for a week after that stage ended, describing it in the present.
- A draft whose own frontmatter said "timed for September, needs a full quarter of tenure" sat scheduled for July.
- Two atoms from the same source article were scheduled two days apart making near-identical arguments.
- A news-pegged post flagged for a currency check reached `approved` without the check ever running.

None of these are visible when reviewing one draft.

## Prerequisites

Read before scoring:

1. **Current calendar**: `{content_root}\calendar\editorial-calendar-{month}-{year}.md` - the week's post list and any open items
2. **Every draft in the week**: `{content_root}\drafts\linkedin\` (or the relevant platform directory)
3. **Voice guide**: the author's voice profile, for any temporal-anchoring or opener conventions it defines
4. **Strategy**: `{content_root}\strategy\pillars.md` - pillar definitions and weekly mix rules

Read all drafts for the week before running any check.

## The Checks

### 1. Duplicate and near-duplicate openers

Compare the first two lines of every post in the week.

- **Fail** on identical or near-identical opening constructions, even when the rest of the post differs.
- Watch specifically for a shared time anchor ("earlier this year," "while I was between jobs," a date range). These collide most often, because the same temporal fix gets applied across several drafts in a single editing pass.
- **Fix**: change both the wording *and* the position. One post carries the anchor in the hook; another carries it mid-post.

### 2. Temporal accuracy against the publish date

For each post: is every time-bound claim true on the day it publishes, not the day it was drafted?

Three failure modes:

- **Life-stage drift** - a draft written under prior circumstances (a job search, a former employer, a completed project) that reads as current. Past tense alone does not fix this. "My stack ran on \$42 a month" still reads as a live setup to a scrolling reader. The period must be named.
- **Tenure claims** - "every call I've run this quarter," "in my first year here." Check against the actual start date.
- **Self-dated drafts** - check each draft's frontmatter `notes` for a stated intended publish window. A draft that says it was written for a later month does not go out early because a slot opened.

### 3. News-peg currency

For any post resting on an external report, statistic, or news event:

- Find the source date in frontmatter (`source`, `notes`).
- If the peg is more than roughly four weeks old at publish time, verify the claim still holds.
- If verification is not possible in the session, report UNVERIFIED explicitly. Do not let it pass silently.

### 4. Repeated arguments across the week

Posts atomized from the same source article are the usual culprit, but any two can collide.

- Compare the **core claim**, not the topic. Two posts can share a topic and make different arguments (fine). Two posts can differ in topic and land the same takeaway (not fine).
- **Fail** if two posts would leave a reader with the same conclusion.
- **Fix**: pull one to the backlog rather than rewriting it into a weaker version of itself.

### 5. Pillar balance and adjacency

- No two consecutive days from the same pillar.
- Flag any pillar exceeding roughly half the week.
- When a pillar is overweight because no alternative draft is ready, say so explicitly. A documented tradeoff is fine; an imbalance presented as a plan is not.

### 6. Batched mechanical sweep

Cheap across all posts at once, and catches drift introduced by late edits:

- Em dashes in post bodies
- Hashtags
- Character count against the platform range (LinkedIn: 800-1,300)
- Emoji in any first line
- External links in post bodies (belong in first comments)

Late-round edits reintroduce these regularly. Re-run after **any** content change, including changes made in response to author feedback.

## Output

\`\`\`markdown
## Week Preflight: [week of DATE]

| # | Check | Result | Detail |
|---|-------|--------|--------|
| 1 | Duplicate openers | PASS/FAIL | [posts + colliding text] |
| 2 | Temporal accuracy | PASS/FAIL | [post + the untrue-on-publish claim] |
| 3 | News-peg currency | PASS/FAIL/UNVERIFIED | [post + source date] |
| 4 | Repeated arguments | PASS/FAIL | [the two posts + shared takeaway] |
| 5 | Pillar balance | PASS/FAIL | [distribution + adjacency] |
| 6 | Mechanical sweep | PASS/FAIL | [post + violation] |

**Verdict**: Clear to publish | N blockers
\`\`\`

List blockers as numbered, actionable instructions with file and line references.

## Related Skills

- **Runs after**: `content-reviewer` - single-post scoring must be complete first
- **Reads from**: `content-calendar` - the week's schedule and open items
- **Runs before**: `/publish`
