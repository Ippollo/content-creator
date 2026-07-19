# Content Configuration

This file is the one place your machine-specific paths live. **Edit the two paths below** (or run
the `content-setup` skill, which fills them in for you). Everything else in the plugin refers to
these via tokens and never hardcodes an absolute path.

## Paths

- **Vault Path** (`vault_root`): `C:\Projects\KB`
- **Content Path** (`content_root`): `C:\Projects\KB\Content`
- **Access Method** (`access_method`): filesystem

> **`{vault_root}`** — your shared knowledge/identity folder. This plugin reads only your voice and
> house-style from here (see below). Other toolkits may share it too, so it is treated as read-only.
>
> **`{content_root}`** — where *this plugin's* working data lives: pillars, swipe file, editorial
> calendar, drafts, and published posts. This is the folder the plugin reads and writes. Defaults to
> `{vault_root}\Content`, but it can live anywhere — set it to any folder you like.
>
> **`{plugin_root}`** — the plugin's own bundled, read-only files: `skills/`, `commands/`,
> `knowledge/` (generic reference: platform algorithms, SEO guidelines), and `templates/` (seeds
> copied into `{content_root}` at setup). Claude Code exposes it as `${CLAUDE_PLUGIN_ROOT}`;
> pre-install it resolves to the `content-creator/` directory. **Never store user data here** — it
> is replaced on every plugin update.

## What this plugin reads from `{vault_root}` (shared identity — read-only)

- `{vault_root}\40_Knowledge\voice-guide.md` — voice fingerprint.
- `{vault_root}\99_System\house-style.md` — publishable-content rules; read before shipping.

> Solo adopters: you can keep these two files anywhere. If you'd rather not run a separate vault,
> point both `vault_root` and `content_root` at the same folder and place `voice-guide.md` /
> `house-style.md` at its root — the setup skill offers this.

## `{content_root}` layout (owned and managed by this plugin)

```
{content_root}\
  strategy\pillars.md            content pillars (canonical)
  strategy\personal-story-ideas.md, revenue-biz-ideas.md
  swipe-file\{linkedin,blog,x,case-studies}\
  calendar\editorial-calendar-{month}-{year}.md   (+ archive\)
  sources\
  drafts\{articles,linkedin,x,case-studies}\
  published\{articles,linkedin,case-studies}\
  assets\                        images and other media
```

Run `content-setup` on first use to scaffold this tree and copy the seed templates in.

## Optional: related toolkits (independence-preserving)

This plugin installs and works **standalone**. If the sibling `hq-board` plugin is also present, the
two share the same `{vault_root}\40_Knowledge\voice-guide.md` and `{vault_root}\99_System\house-style.md`
so outputs stay on-voice across both — but that is a convenience, never a hard dependency.
