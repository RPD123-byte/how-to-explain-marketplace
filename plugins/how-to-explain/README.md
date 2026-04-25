# How To Explain Plugin

This plugin packages the `how-to-explain` Codex skill so other people can install it as a local plugin and use it as a reusable explanation workflow.

The skill is designed for goal-driven explanations: it chooses an explanation goal, infers the user's current model, searches for relevant anchors, walks the missing bridge, and compresses the result into a reusable mental model.

## Contents

- `skills/how-to-explain/SKILL.md`: the skill instructions.
- `skills/how-to-explain/references/`: local fallback references used when Notion is unavailable.
- `docs/tools-db-dependency.md`: the Notion `Tools` database schema and the inheritance-property formulas needed to recreate the dependency.

## Dependency: Notion Tools Database

For full behavior, the skill expects access to a Notion database named `Tools`, with a page named `User Preferences`. That database is used as a durable user-model repository for preference retrieval, explanation anchors, and adjacent concepts.

This dependency is portable: recreate the database using `docs/tools-db-dependency.md`, then update `skills/how-to-explain/references/user-profile.md` and `skills/how-to-explain/SKILL.md` with your own `User Preferences` page URL.

If Notion tools are unavailable, the skill falls back to the bundled reference files.

## Sharing

This plugin is published through the marketplace repository that contains this folder.

The native Codex install path is:

```bash
codex marketplace add RPD123-byte/how-to-explain-marketplace
```

If recipients only receive this plugin folder directly, they can place it under their own marketplace root at `plugins/how-to-explain`, then add a marketplace entry like:

```json
{
  "name": "how-to-explain",
  "source": {
    "source": "local",
    "path": "./plugins/how-to-explain"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Productivity"
}
```
