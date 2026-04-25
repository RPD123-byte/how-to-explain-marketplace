# Notion Tools Database Dependency

The `how-to-explain` skill works best when it can use Notion as a durable user model. In the source environment, that dependency is a Notion data source named `Tools`.

Fetched from Notion on 2026-04-25:

- Data source name: `Tools`
- Data source URL: `collection://2cded17c-d109-80ef-8f01-000bbffd166e`
- Database URL: `https://www.notion.so/2cded17cd1098051bc02da6d695fc9a5`
- Required seed page: `User Preferences`

## Minimum Seed Page

Create a page named `User Preferences` in the `Tools` database.

Recommended properties:

- `Name`: `User Preferences`
- `Creator`: `AI`
- `Domain`: `Knowledge`
- `Type`: `Mental Model`
- `Executable`: unchecked
- `Affordances`: `Central user-model repository for explanation goals, preference retrieval, Notion grounding, and links to lower-level preference pages.`
- `Tool Content`: `Use this page as the central high-level user preference repository. Search it and adjacent Notion material before choosing explanation goals, anchors, and journey structure.`

Recommended body:

```markdown
# Purpose
AI: [This page is the central high-level repository for user preferences that should guide explanation, collaboration, and future Codex behavior.]

# Explanation Preferences
AI: [Bias toward explanation over bare factual rendering. The user wants to understand, approve, and collaborate on work, not merely receive completed actions.]
AI: [A good explanation should choose a goal based on the user's current knowledge, emotional state, and task context; map the gap between current state and target state; then take the user through a coherent journey that preserves retention.]

# Notion As User Model
AI: [Before important explanations, search Notion for the target concept and adjacent concepts the user has already written about. Use those notes as anchors for choosing the explanation goal, the assumed current state, and the comparison path.]

# Updating Notion
AI: [When Codex updates non-database page content, mark AI-authored additions by prefixing the section with "AI:" and wrapping AI-authored text in square brackets.]
```

After creating your own page, replace the source URL in:

- `skills/how-to-explain/SKILL.md`
- `skills/how-to-explain/references/user-profile.md`

## SQLite Schema From Notion MCP

The Notion MCP returned this SQLite table definition for the source data source:

```sql
CREATE TABLE IF NOT EXISTS "collection://2cded17c-d109-80ef-8f01-000bbffd166e" (
  url TEXT UNIQUE,
  createdTime TEXT,
  "Related Anti-Patterns" TEXT,
  "Creator" TEXT,
  "Type" TEXT,
  "Domain" TEXT,
  "Tool Content" TEXT,
  "Related Problems" TEXT,
  "Extends" TEXT,
  "n8n Workflow ID" TEXT,
  "Related Media" TEXT,
  "Output Schema" TEXT,
  "Executable" TEXT,
  "Affordances" TEXT,
  "Children" TEXT,
  "Constraints" TEXT,
  "File Path" TEXT,
  "Input Schema" TEXT,
  "Origin" TEXT,
  "Name" TEXT
);
```

## Notion Property Schema

Recreate these properties in a Notion database:

| Property | Type | Notes |
| --- | --- | --- |
| `Name` | Title | Required title property. |
| `Affordances` | Text | What capabilities the tool or concept unlocks. |
| `Tool Content` | Text | Operational content or explanation content. |
| `Creator` | Select | Options: `Human` pink, `AI` orange. |
| `Domain` | Select | Options: `Physics`, `Math`, `AI`, `Philosophy`, `Self-Care`, `Finance`, `Knowledge`, `Business`, `Computer Science`, `Neuroscience`, `Biology`. |
| `Type` | Select | Options: `State of Mind`, `Mental Model`, `Executable`, `Heuristic`, `Technique`, `Prompt`. |
| `Executable` | Checkbox | Whether the entry describes an executable tool. |
| `File Path` | Text | Optional path for local tool or skill files. |
| `Input Schema` | Text | Optional input contract. |
| `Output Schema` | Text | Optional output contract. |
| `Origin` | Text | Optional source or provenance. |
| `n8n Workflow ID` | Text | Optional workflow link. |
| `Related Media` | Files | Optional attachments. |
| `Extends` | Relation | Self-relation to `Tools`, limited to one parent. |
| `Children` | Relation | Reciprocal self-relation from `Extends`. |
| `Full Affordances` | Formula | Inherits parent affordances through `Extends`, then appends local `Affordances`. |
| `Full Tool Content` | Formula | Inherits parent tool content through `Extends`, then appends local `Tool Content`. |
| `Related Anti-Patterns` | Relation | Optional relation to an anti-patterns database. |
| `Related Problems` | Relation | Optional relation to a problems database. |
| `Constraints` | Relation | Optional relation to a constraints database. |

For the `how-to-explain` plugin, only these properties are required:

- `Name`
- `Creator`
- `Domain`
- `Type`
- `Affordances`
- `Tool Content`
- `Extends`
- `Children`
- `Full Affordances`
- `Full Tool Content`

## Inheritance Property Code

The source database uses a self-relation named `Extends` and reciprocal relation named `Children`. The formulas below recreate the intended inheritance behavior in Notion Formula 2.0.

### Relation DDL Pattern

When using the Notion MCP schema tools, create the self-relation in two steps. Replace `YOUR_TOOLS_DATA_SOURCE_ID` with your new data source ID.

```sql
ADD COLUMN "Extends" RELATION('YOUR_TOOLS_DATA_SOURCE_ID', DUAL 'Children' 'children');
ADD COLUMN "Children" RELATION('YOUR_TOOLS_DATA_SOURCE_ID', DUAL 'Extends' 'extends');
```

If your Notion UI already created the reciprocal relation when adding `Extends`, do not add `Children` a second time. Rename the reciprocal relation to `Children` instead.

### Full Affordances Formula

```notion
lets(
  parentText,
  prop("Extends")
    .map(current.prop("Full Affordances"))
    .filter(not empty(current))
    .join("\n\n"),
  ownText,
  prop("Affordances"),
  if(
    empty(parentText),
    ownText,
    if(empty(ownText), parentText, parentText + "\n\n" + ownText)
  )
)
```

### Full Tool Content Formula

```notion
lets(
  parentText,
  prop("Extends")
    .map(current.prop("Full Tool Content"))
    .filter(not empty(current))
    .join("\n\n"),
  ownText,
  prop("Tool Content"),
  if(
    empty(parentText),
    ownText,
    if(empty(ownText), parentText, parentText + "\n\n" + ownText)
  )
)
```

## Create Database DDL

The Notion MCP `create_database` tool accepts SQL-like DDL. This is a portable starting point for the required subset:

```sql
CREATE TABLE (
  "Name" TITLE,
  "Affordances" RICH_TEXT COMMENT 'What capabilities does this unlock?',
  "Tool Content" RICH_TEXT,
  "Creator" SELECT('Human':pink, 'AI':orange),
  "Domain" SELECT(
    'Physics':blue,
    'Math':purple,
    'AI':gray,
    'Philosophy':yellow,
    'Self-Care':default,
    'Finance':pink,
    'Knowledge':orange,
    'Business':red,
    'Computer Science':blue,
    'Neuroscience':brown,
    'Biology':green
  ),
  "Type" SELECT(
    'State of Mind':purple,
    'Mental Model':blue,
    'Executable':green,
    'Heuristic':red,
    'Technique':default,
    'Prompt':yellow
  ),
  "Executable" CHECKBOX,
  "File Path" RICH_TEXT,
  "Input Schema" RICH_TEXT,
  "Output Schema" RICH_TEXT,
  "Origin" RICH_TEXT,
  "n8n Workflow ID" RICH_TEXT,
  "Related Media" FILES
)
```

After the database exists, add the self-relation and formulas from the inheritance section.
