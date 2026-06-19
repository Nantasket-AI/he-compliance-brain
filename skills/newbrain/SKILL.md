---
name: newbrain
description: Bootstrap a new Brain in a target folder. Creates the directory structure, installs the Brain schema (CLAUDE.md) and page templates, configures timezone and connectors, and scaffolds all starter files. Run once per new Brain.
---

# /the-brain:newbrain — Agent Instructions

**You are bootstrapping a new Brain for the user.** Read this file completely, then execute every step in order. The user should only need to answer a few questions — you handle everything else.

Skills ship with the plugin — you do not install or copy any skill files. Your job is to create the Brain's directory structure, install the schema and templates from the plugin's assets, gather configuration from the user, and scaffold the starter files.

**NEVER modify the plugin install directory** (`${CLAUDE_PLUGIN_ROOT}`). All writes go to the target folder only.

---

## Step 1: Determine Target Folder

If `$ARGUMENTS` was provided, use it as the target path. Otherwise default to the current working directory.

Confirm the resolved absolute path with the user before proceeding. Use the **AskUserQuestion tool** (single question, header "Target folder"):

> Scaffold a new Brain at `/absolute/path/to/target`?

Options: **"Yes, scaffold here"** / **"No — I'll give a different path"** (the built-in "Other" option lets them type a path directly).

**Create the folder if it does not exist.**

**REFUSE to scaffold and explain why if either of these is true:**

1. The target already contains a Brain — it has a `CLAUDE.md` whose content includes the Brain schema markers (e.g., the text "The Brain is a personal knowledge system") OR it already contains any of `wiki/`, `pm/`, or `planner/` directories. Tell the user: "A Brain already exists at that path. Use `/the-brain:lint` to check its health or choose a different target folder."

2. The target is the plugin install directory itself — it contains `.claude-plugin/plugin.json`. Tell the user: "That path is the plugin install directory. Pick a separate folder for your Brain."

---

## Step 2: Create Directory Structure

Create all of these directories (skip any that already exist):

```
wiki/concepts/
wiki/entities/
wiki/sources/
wiki/analysis/
pm/projects/
pm/meetings/
pm/notes/
pm/prep/
pm/reports/
planner/
raw/
```

---

## Step 3: Install Schema and Templates

Copy the Brain schema and page templates from the plugin's assets into the target folder root:

```
${CLAUDE_PLUGIN_ROOT}/skills/newbrain/assets/CLAUDE.md  →  <target>/CLAUDE.md
${CLAUDE_PLUGIN_ROOT}/skills/newbrain/assets/templates.md  →  <target>/templates.md
```

Read both files after copying to confirm they landed correctly before proceeding. These are the permanent Brain schema and template files — do not modify them until Step 4.

---

## Step 4: Gather User Configuration

Gather all configuration with **one AskUserQuestion tool call** containing the four questions below, so the user answers everything in a single questionnaire. Every question automatically gets an "Other" option for free-text answers — rely on it for anything that doesn't fit the listed choices. If the invocation already supplied configuration (e.g., a scripted/non-interactive run that passed timezone and connector answers in the arguments), skip the questionnaire and use those values.

### Question 1: Timezone (header: "Timezone")

> **What timezone are you in, and what secondary timezone should I show alongside it?** (All Brain times display as primary first, secondary in parentheses, e.g. `9:30 AM CT (10:30 AM ET)`.)

Options (single-select): **"CT, with ET secondary"** / **"ET, with CT secondary"** / **"PT, with ET secondary"** / **"My timezone only — no secondary"**. Any other pair comes in via "Other".

Use the answer to fill in the Timezone Convention section of `CLAUDE.md`. Replace the placeholder comment and generic text with their specific timezone pair, UTC offsets (accounting for daylight saving if relevant), and a concrete format example like `9:30 AM CT (10:30 AM ET)`.

### Question 2: Connectors (header: "Connectors", multiSelect: true)

> **Which connectors do you already have set up in Claude Code?** (It's fine if the answer is none — the Brain works without them, and we can add them later.)

Options (multi-select): **"Microsoft 365 (Outlook, Teams, SharePoint)"** / **"Atlassian (Jira, Confluence, Compass)"** / **"GitHub"** / **"None yet / not sure"**. Postman and anything else comes in via "Other" (describe).

**After the user answers:**

- Update the "Available Connectors" section of `CLAUDE.md` to list only what the user has. Add any they mention that aren't in the default list. Remove any they don't have.
- **If the user wants help setting up a connector**, walk them through it:
  - **Atlassian (Jira/Confluence)**: Configured as an MCP connector in Claude Code. Check Settings → Integrations or Connectors. Uses OAuth — no API key typically needed.
  - **Microsoft 365 (Outlook/Teams/SharePoint)**: MCP integration via Claude Code settings. Requires Microsoft account authentication. Covers email, calendar, Teams chat, and SharePoint in one connection.
  - **Postman**: MCP connector that requires a Postman API key from `https://go.postman.co/settings/me/api-keys`. Key goes in Claude Code MCP settings.
  - **GitHub**: Often available as a built-in Claude Code integration. May need a GitHub personal access token (GitHub → Settings → Developer settings → Personal access tokens).
  - **Other connectors**: Help the user search for MCP integrations or configure custom ones based on what they describe.
- **If the user says "None yet / not sure"**: Attempt to call a connector tool (e.g., search Outlook calendar for today's events). Report which connectors responded vs. errored. Update CLAUDE.md with what actually works.

### Question 3: Primary Brain (header: "Primary brain")

> **Is this your primary Brain?** Your primary Brain is the one the anywhere-skills (`/log`, `/myday`, `/standup`, `/prep`) operate on when you run them outside a Brain folder.

Options (single-select): **"Yes — make this my primary Brain (Recommended)"** / **"No — this is a secondary Brain"** (description: "brain_path is left untouched; this Brain's skills work whenever you're inside its folder, and the anywhere-skills keep following your primary Brain").

- **Yes** → run Step 7 (set `brain_path` automatically).
- **No** → **skip Step 7 entirely** — do not read or modify `brain_path`. This lets users keep separate secondary Brains (a team Brain, an experiment, a per-client Brain) without affecting where the anywhere-skills point.

### Question 4: External Systems (header: "Ext. systems")

> **Should the Brain reference external work systems** (Jira project keys, Confluence spaces, Azure DevOps, dashboards, specific repos, team channels)?

Options (single-select): **"No — skip for now"** / **"Yes — I'll list them"**.

If they choose yes (or supply details via "Other"), follow up conversationally for the specifics:

> - Confluence — space names or key pages (e.g., `ENG` for Engineering wiki)
> - Azure DevOps — org/project names
> - GitHub — org/repo names you work in regularly
> - PowerBI or other dashboards — names or URLs
> - Jira — project keys you work with (e.g., `PROJ`, `BACKEND`)
> - Specific repos you'll want the Brain to track — local paths or GitHub URLs
> - Team Slack/Teams channels relevant to your projects
> - Anything else the Brain should know how to find

Use their answer to:
1. Fill in the "External Reference Conventions" section of `CLAUDE.md`. Replace every `<!-- CUSTOMIZE -->` comment with their specific system details. Remove any systems they don't use.
2. Note any Jira project keys, repo paths, Confluence space names, or other identifiers — these will be useful when the user creates their first project with `/the-brain:project new`.

---

## Step 5: Apply Configuration

Apply **everything** gathered in Step 4 to the Brain's `CLAUDE.md`. No placeholder, comment tag, or generic text should survive this step.

### 5a: Update CLAUDE.md

1. **Timezone Convention** section — replace the generic text and `<!-- CUSTOMIZE -->` comment with the user's specific timezone pair. Write it in the same authoritative style as the rest of the document. Include:
   - The primary timezone name and abbreviation
   - The secondary timezone name and abbreviation (if applicable)
   - The UTC offsets for both (accounting for daylight saving if relevant)
   - A concrete format example: `9:30 AM PT (12:30 PM ET)`
   - Remove all `<!-- CUSTOMIZE -->` comments from this section

2. **Available Connectors** section — replace the bullet list with only the connectors the user confirmed. For each, keep the brief description of what it provides. Remove connectors they don't have. Add any new ones they mentioned.

3. **External Reference Conventions** section — replace all `<!-- CUSTOMIZE -->` comments with the user's specific system details:
   - Confluence: add their space names and what each contains
   - Jira: note their project keys
   - GitHub: note their org/repo names
   - ADO: note their org/project names
   - Dashboards: note names/URLs
   - Remove any systems they don't use from this section entirely

### 5b: Final placeholder sweep

Scan `CLAUDE.md` and `templates.md` for any remaining placeholders or template markers:

- `<!-- CUSTOMIZE`
- `<YOUR_BRAIN_PATH>`
- `<BRAIN>`
- `<BRAIN_ROOT>`
- Any other `<PLACEHOLDER>` pattern (angle-bracket-wrapped uppercase words)

If any are found in `CLAUDE.md` (which is now the user's live schema, not a template), resolve them using what you know from the user's answers. If a placeholder refers to something the user didn't address, ask now rather than leaving it unresolved.

`templates.md` legitimately uses `YYYY-MM-DD` and `[[wikilink]]` patterns — leave those alone, they are instructional content for future page creation.

---

## Step 6: Create Scaffold Files

Create each of these files with the exact content shown. Replace `YYYY-MM-DD` with today's actual date.

### `wiki/overview.md`

```markdown
---
title: Scholar Overview
type: overview
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Scholar — Overview

The Scholar brain is currently empty. It will grow as sources are ingested and knowledge is built up.

## Current State

No content yet. Use `/the-brain:ingest` to add your first source.
```

### `wiki/index.md`

```markdown
---
title: Scholar Index
type: index
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Scholar Index

## Concepts

*No concepts yet.*

## Entities

*No entities yet.*

## Sources

*No sources yet.*

## Analysis

*No analyses yet.*
```

### `pm/overview.md`

```markdown
---
title: PM Overview
type: overview
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Project Manager — Overview

The PM brain is currently empty. It will grow as projects are created and meetings are ingested.

## Active Projects

No active projects yet. Use `/the-brain:project new <name>` to create your first project.
```

### `pm/index.md`

```markdown
---
title: PM Index
type: index
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# PM Index

## Active Projects

*No projects yet.*

## Meetings

*No meetings yet.*

## Prep Docs

*No prep docs yet.*

## Archived

*Nothing archived yet.*
```

### `planner/index.md`

```markdown
---
title: Planner Index
type: index
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Planner Index

## Current Week

*No daily files yet. Run `/the-brain:myday` to generate today's plan.*

## Past Weeks

*No archived weeks yet.*
```

### `planner/dashboard.md`

```markdown
---
title: Dashboard
type: dashboard
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Dashboard

## Today

*Run `/the-brain:myday` to populate.*

## Priorities

*No priorities set yet.*

## Tasks

*No tasks yet.*
```

### `planner/tasks.md`

```markdown
---
title: Tasks
type: task
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Tasks

## Active

*No active tasks.*

## Blocked

*No blocked tasks.*

## Maintenance

*No maintenance tasks.*
```

### `planner/goals.md`

```markdown
---
title: Goals
type: goals
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Goals

*No goals set yet. Add your quarterly or monthly goals here.*
```

### `log.md` (in Brain root)

```markdown
# Brain Operations Log

Chronological record of operations that change the Brain.
Format: `## [YYYY-MM-DD] verb | Subject`

## [YYYY-MM-DD] system | Brain bootstrapped
Fresh Brain scaffolded via /the-brain:newbrain. Sub-brains: wiki, pm, planner. Schema and templates installed from plugin. Ready for first ingest.
```

---

## Step 7: Set the brain_path Plugin Setting

**Only run this step if the user answered "Yes" to the Primary Brain question in Step 4.** If they answered "No", skip straight to Step 8 and leave `brain_path` completely untouched.

Configure the plugin's `brain_path` setting automatically so the anywhere-skills (`/the-brain:log`, `/the-brain:myday`, `/the-brain:standup`, `/the-brain:prep`) can find this Brain from any directory. The setting lives in the user's `~/.claude/settings.json` under `pluginConfigs`.

1. Read `~/.claude/settings.json`. If the file does not exist, treat it as `{}`.
2. Find the plugin's config key inside `pluginConfigs`: look for an existing key that starts with `the-brain@` (normally `the-brain@the-brain`). If none exists, use `the-brain@the-brain`.
3. Act based on the current value of `pluginConfigs.<key>.options.brain_path`:
   - **Unset or empty** → set it to the absolute path of the new Brain. Create the `pluginConfigs.<key>.options` structure if needed. Preserve every other key in the file exactly as-is and write back valid JSON.
   - **Already set to this Brain's path** → nothing to do.
   - **Set to a different path** → the user has another Brain configured. Ask before changing:
     > Your `brain_path` currently points to `<existing path>`. Should I repoint it to this new Brain at `<target path>`, or leave it as-is? (The anywhere-skills follow whichever Brain `brain_path` points to.)
     Apply whichever the user chooses.
4. If `~/.claude/settings.json` cannot be written (permissions, sandbox), do not fail the bootstrap — note it and tell the user to run `/plugin configure the-brain@the-brain` instead.

Record what happened (set automatically / already set / kept existing / manual fallback / skipped — secondary Brain) for the welcome message in Step 8.

---

## Step 8: Welcome the User

Print a welcome message that covers:

**What just happened:**
- Brain directory structure created at the confirmed target path
- Brain schema (`CLAUDE.md`) and page templates installed from the plugin
- `CLAUDE.md` customized with their timezone, connectors, and external systems
- All scaffold files created, all placeholders resolved — the Brain is ready

**Quick start — what to do first:**

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `/myday` | Morning briefing — schedule, priorities, tasks | Every morning |
| `/project new <name>` | Create a project page with full context | Great first step |
| `/met <meeting description>` | Pull a Teams transcript and process it | After your next meeting |
| `/ingest` | File a source (article, notes, PDF) into the Brain | Whenever you read something worth keeping |
| `/ask <question>` | Query the Brain with cited sources | Works better as the Brain grows |
| `/log` | Log what you're working on | Throughout the day |
| `/standup` | Generate a standup summary | Before your next standup |
| `/prep <meeting>` | Meeting prep briefing | Before any important meeting |

(Short names work as long as no other plugin defines a skill with the same name; the fully-qualified form is `/the-brain:<skill>`.)

**How it grows:**
- The Brain starts empty and compounds over time. Every meeting ingested, every project created, every source filed makes all future interactions richer.
- `/myday` on Mondays automatically runs health checks and plots your week.
- Don't worry about getting things wrong — `/lint` finds problems, `/sync` catches drift.

**One habit to build:** Run `/myday` every morning. Everything else flows from there.

**Important — configure brain_path (Claude Code only):**
If you use this Brain in **Claude Code**, set the `brain_path` plugin setting for **the-brain** to `<absolute path to this Brain>`. This lets `/the-brain:log`, `/the-brain:myday`, `/the-brain:standup`, and `/the-brain:prep` find this Brain from any directory — not just when your working directory is the Brain root. Without this setting, those skills only work when you are already inside the Brain folder.

If you use the Brain through **Claude Cowork**, skip this step — Cowork sessions are already rooted in the Brain folder, and plugin settings like `brain_path` are not available there. The skills will find the Brain via the working directory instead.
**brain_path status:**
If applicable (Claude Code, NOT Cowork), report the Step 7 outcome — e.g. "`brain_path` was set automatically to `<absolute path to this Brain>`, so `/log`, `/myday`, `/standup`, and `/prep` will find this Brain from any directory. Change it anytime with `/plugin configure the-brain@the-brain`." If the user chose **secondary Brain** in Step 4, say instead: "`brain_path` was left untouched — this is a secondary Brain. Its skills work whenever you're inside this folder; the anywhere-skills keep following your primary Brain." If Step 7 fell back to manual configuration or the user kept a different Brain's path, say that and explain that the anywhere-skills follow `brain_path` when run outside a Brain folder.
