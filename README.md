# How To Explain Marketplace

This repository is a Codex plugin marketplace containing the `how-to-explain` plugin.

`how-to-explain` is an audience-aware explanation skill for Codex. It helps Codex turn facts, code, systems, philosophy, debugging results, and technical decisions into goal-driven explanations that a user can understand, approve, redirect, and remember.

## Install

Add this marketplace to Codex:

```bash
codex marketplace add RPD123-byte/how-to-explain-marketplace
```

Then restart Codex if the marketplace does not appear immediately, open the plugin marketplace, and install or enable `how-to-explain`.

If editing `~/.codex/config.toml` directly, the enabled plugin entry is:

```toml
[plugins."how-to-explain@how-to-explain-marketplace"]
enabled = true
```

## Update

Plugin updates are regular git updates. The publisher updates this repository by committing and pushing changes.

Users who installed the marketplace from GitHub should refresh or update their local marketplace checkout when they want the latest version. If Codex does not pick up the update immediately, restart Codex.

For now, keep the plugin version in `plugins/how-to-explain/.codex-plugin/plugin.json` in sync with meaningful releases. Tagging releases is optional, but useful:

```bash
git tag v0.1.0
git push origin v0.1.0
```

## Notion Dependency

The plugin works without Notion by using local fallback references. For full behavior, recreate the Notion `Tools` database documented in:

`plugins/how-to-explain/docs/tools-db-dependency.md`

Then update the `User Preferences` URL in:

- `plugins/how-to-explain/skills/how-to-explain/SKILL.md`
- `plugins/how-to-explain/skills/how-to-explain/references/user-profile.md`

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/how-to-explain/.codex-plugin/plugin.json
plugins/how-to-explain/skills/how-to-explain/SKILL.md
plugins/how-to-explain/docs/tools-db-dependency.md
```
