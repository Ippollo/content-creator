# Calendar File Format

The editorial calendar lives at `c:\HQ\content-creator\editorial-calendar.md`.

## Structure

```markdown
# Editorial Calendar

## Week of YYYY-MM-DD

| Day | Post | Pillar | Status |
|-----|------|--------|--------|
| Mon | slug | Pillar Name | draft / scheduled / published |
| Tue | slug | Pillar Name | draft / scheduled / published |
| Thu | slug | Pillar Name | draft / scheduled / published |
| Fri | slug | Pillar Name | draft / scheduled / published |

## Backlog

| Post | Pillar | Source Note |
|------|--------|------------|
| slug | Pillar Name | note name |
```

## Status Meanings

- `draft` — proposed but not yet scheduled on LinkedIn
- `scheduled` — scheduled on LinkedIn, awaiting go-live
- `published` — live on LinkedIn

## Pillar Mapping

Map draft `cluster` frontmatter values to pillars:

| Cluster Value | Pillar |
|---------------|--------|
| `ai-agents` | AI Agents & Automation |
| `operations-cx` | Operations & Client Lifecycle |
| `revenue-biz` | Revenue & Business Impact |
| `career` | Career & Professional Growth |
