---
description: Grab today's first-comment from the editorial calendar and copy it to clipboard. Use daily when a scheduled post goes live on LinkedIn.
---

# /comment — First-Comment Grab

**Goal**: Quickly retrieve and copy the first-comment for today's live post.

## When to Use

- Your scheduled LinkedIn post just went live
- You need to paste the first-comment (which contains the link) as quickly as possible
- Called from a daily reminder, not during batch scheduling

## Steps

### Step 1: Find Today's Post

Read `editorial-calendar.md` and find the entry for today's date.

- **If no post today**: "No post scheduled for today."
- **If post found**: Continue to Step 2.

### Step 2: Get the First Comment

Read the post file from `linkedin/published/[slug].md` (or `linkedin/drafts/[slug].md` if not yet moved).

Look for `first_comment` in the frontmatter.

- **If no first_comment**: "Today's post ([slug]) has no first-comment."
- **If first_comment found**: Copy it to clipboard and display it.

### Step 3: Display

```
📝 First comment for: [slug]
📋 Copied to clipboard

[first-comment text]

→ Paste this as a comment on your live LinkedIn post.
```

## Notes

- This workflow makes no file changes. It just reads and copies.
- If multiple posts are scheduled today, show all and let the user pick.
- The first-comment typically contains a link to the source article or a call-to-action. LinkedIn suppresses links in post bodies, so the first-comment is the standard workaround.
