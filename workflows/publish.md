---
description: Batch schedule approved posts to Buffer and update all tracking files.
---

# /publish — Schedule to Buffer

**Goal**: Push all `approved` posts to Buffer in one batch, update the editorial calendar and frontmatter, and move files to `published/`.

## Status Lifecycle

```
draft → approved → scheduled
```

- **`draft`** — post created (via /atomize, /write-article, manual, etc.). Lives in `linkedin/drafts/`
- **`approved`** — user has reviewed and approved the final version. Still in `drafts/`, ready to push
- **`scheduled`** — pushed to Buffer with a date. File moved to `linkedin/published/`

Buffer handles everything after scheduling — no `published` status needed in our system.

## Prerequisites

- `editorial-calendar.md` has posts with status `approved` and assigned dates
- Corresponding draft files exist in `linkedin/drafts/`
- `.env` has a valid `BUFFER_ACCESS_TOKEN`

## Steps

// turbo-all

### Step 1: Find Approved Posts

Read `editorial-calendar.md`. For each weekly schedule table, find rows where Status = `approved`.

For each match, resolve the actual date:
- The week header (e.g., `## Week of 2026-04-06`) gives the Monday date
- The Day column (`Mon`=+0, `Tue`=+1, `Wed`=+2, `Thu`=+3, `Fri`=+4) gives the offset
- Calculate the full ISO date

Find the corresponding draft file. Check both locations:
1. `linkedin/drafts/` — look for files matching the slug (e.g., `*-information-overload.md`)
2. `linkedin/published/` — some posts may have been moved early

If no file is found for a slug, flag it as missing and skip.

### Step 2: Preview the Batch

Display a confirmation table:

```
📅 Publish to Buffer — X posts

  # | Date       | Post                 | Pillar        | File
  1 | 2026-04-07 | information-overload | Ops & CX      | ✅ found
  2 | 2026-04-08 | ceo-ai-adoption      | AI Agents     | ✅ found
  3 | 2026-04-14 | ai-not-the-problem   | AI Agents     | ✅ found

Confirm? (go / cancel)
```

### Step 3: Push to Buffer

For each post in the batch:

1. Run: `node scripts/buffer-publish.js <file-path> --date <YYYY-MM-DD>T08:00:00-06:00`
2. Capture the Buffer post ID from the output
3. Display result inline:

```
  ✅ information-overload → Buffer (2026-04-07)
  ✅ ceo-ai-adoption → Buffer (2026-04-08)
  ❌ ai-not-the-problem → Error: [message]
```

If any post fails, continue with the rest. Report failures at the end.

### Step 4: Update Tracking

For each successfully scheduled post:

1. **Update frontmatter**: Set `status: scheduled` and add `buffer_date: YYYY-MM-DD`
2. **Move file**: If in `linkedin/drafts/`, move to `linkedin/published/`
3. **Update calendar**: Change status from `approved` → `scheduled` in `editorial-calendar.md`

For failed posts, leave status as `approved` so they can be retried.

### Step 5: Summary

```
✅ Publish complete

  Scheduled: X posts (through YYYY-MM-DD)
  Failed:    X posts (remain as approved)

  Buffer queue: run `node scripts/buffer-publish.js --pending` to verify
```

## Buffer Script Reference

```bash
# List connected channels
node scripts/buffer-publish.js --channels

# Preview what would be sent (no actual post)
node scripts/buffer-publish.js <draft.md> --dry-run

# Schedule for a specific date
node scripts/buffer-publish.js <draft.md> --date 2026-04-07T08:00:00-06:00

# Add to next queue slot
node scripts/buffer-publish.js <draft.md> --queue

# Post immediately
node scripts/buffer-publish.js <draft.md> --now

# Show pending posts in Buffer queue
node scripts/buffer-publish.js --pending
```

## Notes

- All posts are scheduled at **8:00 AM Mountain** by default. Adjust the time in the command if needed.
- First-comments are NOT part of this workflow. Use `/comment` daily when posts go live.
- If `editorial-calendar.md` doesn't exist or has no `approved` posts, exit with a message.
- Buffer API token expires (check duration at regeneration). Regenerate at https://publish.buffer.com/settings/api
- The `/publish` workflow does NOT assign dates. Dates come from the editorial calendar, which is built intentionally before this step.
