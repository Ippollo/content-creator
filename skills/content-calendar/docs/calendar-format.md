# Calendar File Format

The editorial calendar lives at `c:\HQ\content-creator\editorial-calendar.md`.

## Structure

```markdown
# Editorial Calendar

## Week of YYYY-MM-DD

| Day | Post | Pillar | Status |
|-----|------|--------|--------|
| Mon | slug | Pillar Name | draft / approved / scheduled |
| Tue | slug | Pillar Name | draft / approved / scheduled |
| Thu | slug | Pillar Name | draft / approved / scheduled |
| Fri | slug | Pillar Name | draft / approved / scheduled |

## Backlog

| Post | Pillar | Source Note |
|------|--------|------------|
| slug | Pillar Name | note name |
```

## Status Lifecycle

```
draft → approved → scheduled
```

- `draft` — post created, not yet reviewed
- `approved` — user has reviewed and approved the final version, ready to push to Buffer
- `scheduled` — pushed to Buffer with a scheduled date. File moved to `linkedin/published/`

Buffer handles actual publishing. No `published` status tracked in our system.

## Pillar Mapping

Map draft `cluster` frontmatter values to pillars:

| Cluster Value | Pillar |
|---------------|--------|
| `ai-agents` | AI Agents & Automation |
| `operations-cx` | Operations & Client Lifecycle |
| `revenue-biz` | Revenue & Business Impact |
| `career` | Career & Professional Growth |
