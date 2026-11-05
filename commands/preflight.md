---
description: Run week-level preflight checks on a scheduled week before publishing. Catches duplicate openers, stale time references, repeated arguments, and unverified news pegs across posts. Read-only gate - flags issues, does not fix them.
disable-model-invocation: true
---

# /preflight - Week-Level Publish Gate

Run the `content-week-preflight` skill against the current (or specified) scheduled week.

**This workflow is read-only. It flags blockers; it never edits drafts, changes status, or publishes.**

## When to Use

- After every post in a week has been individually approved, before `/publish`
- When locking a week on the editorial calendar
- After any late-round content edits, since those reintroduce mechanical violations

## Steps

1. Read the current editorial calendar and identify the target week. If the user did not name a week, use the next unpublished one.
2. Read every draft scheduled in that week. Do not proceed on a partial read - the checks are comparisons between posts.
3. Invoke the `content-week-preflight` skill and run all six checks.
4. Present the scorecard in the exact format the skill defines.
5. If there are blockers, list them as numbered instructions with file references and stop. Do not offer to publish.
6. If clear, state that the week is clear to publish and name `/publish` as the next step.

## Scope

One week per invocation. For multi-week checks, invoke once per week - cross-week duplicate detection is deliberately out of scope, since openers may legitimately repeat across a month.

## Related

- **Uses**: `content-week-preflight` skill
- **Complements**: `/review-content` - that workflow scores a single draft; this one gates a whole week
- **Precedes**: `/publish`
