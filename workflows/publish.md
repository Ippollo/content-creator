---
description: Batch scheduling session — serve queued posts one-by-one for LinkedIn scheduling, then update all files and calendar on completion.
---

# /publish — Batch Scheduling Session

**Goal**: Schedule 1-4 weeks of content on LinkedIn in one sitting, then update all tracking files automatically.

## Prerequisites

- `editorial-calendar.md` exists with scheduled posts (use the `content-calendar` skill to create one first)
- Posts in `linkedin/drafts/` have been reviewed and approved

## Steps

// turbo-all

### Step 1: Show the Queue

Read `editorial-calendar.md` for all posts with status `scheduled` (or `draft` if nothing is scheduled yet).

Display them in chronological order:

```
📅 Scheduling Session — X posts queued

1. Mon Mar 17 | tyranny-of-urgent       | Ops & CX
2. Tue Mar 18 | interruption-tax        | Ops & CX
3. Thu Mar 20 | custom-ai-advisor       | AI Agents
...

Ready? I'll serve them one at a time. Say "next" to advance, "skip" to skip one, or "done" to end the session.
```

### Step 2: Serve Posts One-by-One

For each post in the queue:

1. Read the full post from `linkedin/drafts/[slug].md`
   - **If file not found**: Display "⚠️ [slug] not found in drafts — skipping" and auto-advance
2. Copy the post body (everything below the frontmatter `---`) to clipboard
3. Display the post text for reference
4. Wait for user input:
   - **"next"** → mark this post as served, advance to the next
   - **"skip"** → skip this post (stays in drafts, not marked as served)
   - **"done"** → end the session early

```
Post 1/8 — tyranny-of-urgent — copied to clipboard ✅

[post text displayed here]

→ next / skip / done
```

### Step 3: Close Session

When the user says "done" or all posts have been served:

1. **Move files**: For each served (non-skipped) post, move from `linkedin/drafts/` to `linkedin/published/`
2. **Update frontmatter**: Add `status: published` and `scheduled_date: YYYY-MM-DD` to each moved file
3. **Update calendar**: Change status from `scheduled` → `published` in `editorial-calendar.md`
4. **Update vault notes**: For each moved post, check `source_note` frontmatter and add to the vault note's `## Published` section if not already there

Display summary:

```
✅ Session complete

Scheduled: X posts through [last date]
Skipped:   X posts (remain in drafts)
Remaining: X unscheduled drafts in backlog

Next session: You have content through [date].
```

## Notes

- First-comments are NOT part of this workflow. Use `/comment` daily when posts go live.
- If `editorial-calendar.md` doesn't exist or is empty, suggest running the `content-calendar` skill first.
- Posts are served in the order they appear in the calendar (chronological).
