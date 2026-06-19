---
name: sync
description: Sync Brain's project knowledge with live connector state. Compares PM brain against Jira, GitHub, and other connectors. Flags drift and updates project pages. Use periodically to keep institutional memory honest.
argument-hint: "<project-name> (optional, syncs all if omitted)"
---

# /the-brain:sync — Environmental Awareness Check

You are syncing the Brain's project knowledge against live connector state.

## Step 1: Identify projects to sync

- If a project name was provided, sync only that project
- If no argument, read `pm/index.md` and sync all active projects

## Step 2: For each project

Read the project page from `pm/projects/`. Note:
- `jira_project` key
- `repo` reference
- Current status, open questions, risks
- Decision log (what the Brain thinks is true)

## Step 3: Query connectors

**Jira** (if `jira_project` is set):
- Search for recent issues using JQL: `project = KEY ORDER BY updated DESC`
- Get current sprint status
- Check for tickets the Brain doesn't know about
- Check for status changes (tickets closed that Brain shows open, etc.)

**Outlook/Teams** (for recent activity):
- Search for recent emails/messages mentioning the project
- Check for meetings not yet ingested

**SharePoint** (if applicable):
- Search for recently modified documents related to the project

## Step 4: Compare and flag drift

For each piece of connector data, compare with the Brain's state:
- **New information**: tickets, PRs, messages the Brain hasn't processed
- **State drift**: things the Brain says are open but connectors show closed (or vice versa)
- **Timeline drift**: deadlines changed in Jira but not in the Brain

## Step 5: Update

- Update project pages with current connector state in the "Live Context" section
- Flag significant drift with `> [!conflict]` callouts showing Brain state vs connector state
- If new meetings or significant messages are found, suggest ingesting them
- Add new tasks to `planner/tasks.md` if connector reveals untracked work

## Step 6: Report and log

Present a sync report per project:
- What was updated
- What drift was found
- What needs user attention (e.g., un-ingested meeting transcripts)

Append to `log.md`:
```
## [YYYY-MM-DD] sync | Project Name (or "all projects")
Synced N project(s). Drift found: [summary]. Updated: [pages list].
```
