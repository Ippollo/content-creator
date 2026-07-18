# Content Configuration

> Conforms to the **KB Access Contract** (Option A), same as the other HQ plugins. See
> `hq-cortex`'s `config.md` and the migration's `kb-access-contract.md` for the full schema.

- **Vault Path** (`vault_root`): C:\Projects\KB
- **Access Method** (`access_method`): filesystem  <!-- future: kb-mcp (Option B) -->

> **`{vault_root}` token.** Commands/skills refer to the vault as `{vault_root}` (e.g.
> `{vault_root}\40_Knowledge\voice-guide.md`) and never hardcode an absolute path. Resolve it to
> the Vault Path above — the single place the machine-specific vault path lives.
>
> **`{plugin_root}` token.** Refers to this plugin's own bundled files (skills, `strategy/`,
> `swipe-file/`, and the draft output dirs `articles/drafts/`, `linkedin/drafts/`) relative to the
> plugin's install directory — never an absolute install path. Claude Code exposes it as
> `${CLAUDE_PLUGIN_ROOT}`. Pre-install it resolves to the `content-creator/` directory.

## What this plugin reads from the vault

- `{vault_root}\40_Knowledge\voice-guide.md` — voice fingerprint (T5)
- `{vault_root}\99_System\house-style.md` — publishable-content rules (T8); read before shipping.

## Read-Only Zones

Inherits the contract: `20_Journal`, `50_Finance` are read-only. This plugin does not write to the
vault; it saves drafts to plugin-local `articles/drafts/` and `linkedin/drafts/`.
