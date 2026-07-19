---
schema_version: 1.0
name: content-setup
description: "First-run setup and onboarding for the content plugin. Use when the user says 'set up the content plugin', 'onboard me', 'get started with content', when a content skill reports the workspace is missing, or when voice-guide.md / pillars.md do not yet exist. Chooses the content folder, scaffolds the layout, seeds templates, and interviews the user to build their voice guide."
metadata:
  pattern: onboarding
---

# Content Setup Skill

You onboard a new user (or a new machine) so every other content skill has what it needs: a
configured `{content_root}`, the folder layout, seeded templates, and a real voice guide. Be
friendly and concrete — this is someone's first impression of the plugin.

**Never overwrite existing user data.** For every file below, create it only if it is missing. If a
file already exists, leave it and say so.

## Workflow

### 1. Read current config

Read `{plugin_root}\config.md`. Note the current `vault_root` and `content_root`. If both already
resolve to real folders that contain `voice-guide.md` and `strategy\pillars.md`, tell the user setup
looks complete and ask whether they want to re-run any step (voice interview, add pillars) or stop.

### 2. Confirm the two paths

Ask the user to confirm or change:

- **`vault_root`** — their shared knowledge folder (holds `voice-guide.md`, `house-style.md`). If
  they don't keep a separate vault, they can set this to the same folder as `content_root`.
- **`content_root`** — where this plugin's data lives. Default: `{vault_root}\Content`.

Do not invent an absolute path. Use the user's answers.

### 3. Scaffold the content folder

Create this tree under `{content_root}` (skip any dir that exists):

```
{content_root}\strategy\
{content_root}\swipe-file\linkedin\   \blog\   \x\   \case-studies\
{content_root}\calendar\archive\
{content_root}\sources\
{content_root}\drafts\articles\   \linkedin\   \x\   \case-studies\
{content_root}\published\articles\   \linkedin\   \case-studies\
```

### 4. Seed templates (only if the destination is missing)

Copy from `{plugin_root}\templates\` into place:

| Template | Destination |
|---|---|
| `pillars.template.md` | `{content_root}\strategy\pillars.md` |
| `swipe-file-README.md` | `{content_root}\swipe-file\README.md` |
| `voice-guide.template.md` | `{vault_root}\40_Knowledge\voice-guide.md` |
| `house-style.template.md` | `{vault_root}\99_System\house-style.md` |

> If `vault_root` and `content_root` are the same folder (solo setup), place `voice-guide.md` and
> `house-style.md` at `{content_root}\voice-guide.md` and `{content_root}\house-style.md` instead,
> and record those locations in `config.md`'s "reads from vault" section.

### 5. Build the voice guide (the highest-value step)

The seeded `voice-guide.md` is a template full of `[brackets]`. Turn it into a real profile:

- **If the user has writing samples**: ask them to paste 3–5 of their best posts/articles (or point
  you at files/URLs). Analyze sentence length, vocabulary, tone, hook style, structure, and recurring
  phrases. Fill in the fingerprint and at least one content-type lens.
- **If they don't**: run a short interview — 6–8 questions covering who they write for, their
  professional identity, tone they want, formats they publish, and phrases/words they love or ban.
  Draft the voice guide from their answers.

Write the result to the `voice-guide.md` created in step 4. Show the user the filled-in guide and
invite edits.

### 6. Offer to draft pillars

Ask if they want help turning `strategy\pillars.md` from template into real content pillars (niche,
3–4 topic clusters, keywords). If yes, interview briefly and fill it in. If not, leave the template.

### 7. Persist paths to config

Update `{plugin_root}\config.md` so `Vault Path` and `Content Path` reflect the confirmed values.

> **Note:** `config.md` lives in the plugin package, which is replaced on plugin update. If the user
> reinstalls/updates the plugin, they may need to re-run this step to restore their paths. (Tracked
> as a follow-up to move resolved config out of the package.)

### 8. Confirm and hand off

Summarize what was created and where. Then point the user at their first action, e.g.:

- *"Write a LinkedIn post about [topic]"*
- *"Write a blog post about [topic]. Target the keyword '[keyword]'."*
- `/scout [url]` to evaluate an external source

## Related Skills

- **linkedin-writer / blog-writer / x-writer / case-study-writer** — the writers that depend on this
  setup; they route back here if the workspace is missing.
- **content-calendar** — start scheduling once you have drafts.
