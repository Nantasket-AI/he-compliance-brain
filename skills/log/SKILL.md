---
name: log
description: Log what you've been working on to today's daily plan. Reads your description and the current conversation to build a rich activity log entry. Works from any Claude Code or Claude Cowork session.
argument-hint: <description of what you worked on (optional)>
---

# /the-brain:log — Activity Log

Ships with the the-brain plugin; available wherever the plugin is enabled.

Update today's daily planner file with a summary of what was worked on. Reads the user's description AND the current Claude Code conversation context to build a rich, specific log entry. This makes daily files serve as both prospective plans and retrospective logs — useful for `/the-brain:standup`, `/the-brain:reflect`, and general accountability.

## Brain location

Determine the Brain directory using this priority order:
1. If the current working directory is a Brain (contains a `CLAUDE.md` with the Brain schema and has `wiki/`, `pm/`, and `planner/` subdirectories), use it.
2. Otherwise check the plugin setting `${user_config.brain_path}` and operate on that directory. If the setting is empty or appears as a literal unexpanded placeholder, treat it as unset and continue to step 3.
3. If neither applies, fall back to the **Outside the Brain repo** behavior below.

**Claude Cowork:** treat this as a project skill, scoped to the Cowork project it runs in. The project root is the Brain, found by step 1 — `brain_path` does not exist in Cowork and is always unset. If the Cowork project is not a Brain, use the step 3 fallback.

All Brain file paths below are relative to the Brain root once located.

## Inside the Brain repo

### Step 1: Determine today's file

Calculate today's date and resolve the file path: `planner/YYYY/MM/YYYY-MM-DD.md`.

- If the directory (`planner/YYYY/MM/`) doesn't exist, create it.
- If the daily file doesn't exist yet (e.g., `/the-brain:myday` hasn't run today), create a minimal stub:

```yaml
---
title: "YYYY-MM-DD"
type: daily
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily, planner]
---

# Day-of-week, YYYY-MM-DD

## Activity Log
```

- If the daily file exists but has no `## Activity Log` section, add one before the `## End-of-Day Summary` section (or at the end if that section doesn't exist either).

### Step 2: Read existing context

Read the current daily file to understand what was already planned and logged:
- What was on today's schedule?
- What tasks were planned?
- What's already been logged (to avoid duplicating entries)?

Also read for cross-referencing:
- `planner/tasks.md` — to check off completed tasks
- `pm/overview.md` — to map work to projects

### Step 3: Build the log entry

Synthesize a log entry from **two sources**:

**Source A — User's description** (from the skill argument):
- What the user says they've been working on
- May be brief ("worked on the API project") or detailed
- If no argument provided, rely entirely on Source B

**Source B — Conversation context** (from the current Claude Code session):
- Scan the full conversation for work artifacts:
  - **Files read, edited, or created** — which files, what changed, why
  - **Commands run** — builds, tests, deployments, git operations
  - **Connector interactions** — Jira tickets updated, emails sent, calendar changes, Teams messages
  - **Decisions made** — architectural choices, approach changes, problem resolutions
  - **Problems encountered and solved** — bugs found, blockers hit, workarounds applied
  - **Skills invoked** — `/the-brain:ingest`, `/the-brain:sync`, `/the-brain:lint`, etc. and their outcomes
  - **Brain operations** — pages created, indexes updated, knowledge filed
  - **Code written** — features implemented, refactors completed, tests added
- If the conversation was in a **different repo** (not the Brain), note the repo and what was done there

**Synthesis rules:**
- Be **specific**: "Created meeting page for API design review, updated project page and pm/index.md" not "Updated Brain pages"
- Be **concise**: this is a log entry, not a transcript. 3–8 bullet points per entry.
- **Don't duplicate**: if a previous log entry already covers something, skip it
- **Attribute to projects**: connect work to `[[pm/projects/...]]` when applicable
- **Note the repo/context**: if working outside the Brain, note where (e.g., "In my-service repo: fixed validation bug")

### Step 4: Append to the Activity Log section

Add a timestamped entry to the `## Activity Log` section of today's file:

```markdown
### HH:MM — Brief descriptive title

- What was done (specific: files, pages, tickets, decisions)
- What was done (another item)
- Context: which project, what prompted this work
- Outcome: what changed, what's next, what's still open
```

Use `[[wikilinks]]` throughout:
- `[[pm/projects/project-name]]` for project context
- `[[wiki/entities/person-name]]` for people involved
- `[[pm/meetings/YYYY-MM-DD-slug]]` for meeting pages created or referenced
- `[[wiki/concepts/concept]]` for concepts explored

### Step 5: Update tasks (if applicable)

Check if work done in this session completed any tasks from `planner/tasks.md`:
- If a task is complete, mark it `[x]` in tasks.md
- If new tasks emerged from the work, add them to the Active section
- If a task is now blocked, move it to Blocked with an explanation

### Step 6: Update the daily file's metadata

Update the `updated:` field in the daily file's frontmatter to today's date.

### Step 7: Log to log.md (only if Brain pages were changed)

`log.md` is the Brain's **operational changelog** — it only records operations that change Brain pages (not personal work activity). The activity log entry in the daily file is NOT a Brain operation.

- **If tasks.md was updated** (tasks marked done or added), append to `log.md`:
  ```
  ## [YYYY-MM-DD] system | Tasks updated via /the-brain:log
  Tasks completed: N. Tasks added: N. Updated [[planner/tasks]].
  ```
- **If no Brain pages were changed** (only the daily file's Activity Log was appended to), do NOT append to `log.md`. The daily file update is a personal log, not a Brain structural change.

### Step 8: Confirm

Output a brief confirmation to the user:
- What was logged (summary)
- Which file was updated
- Any tasks marked complete or added
- Reminder: "Run `/the-brain:reflect` at end of day to synthesize plan vs. actual."

## Outside the Brain repo

When no Brain directory is found (neither cwd nor `${user_config.brain_path}` resolves to a Brain):

1. Still build the log entry from conversation context + user description (Steps 3's synthesis)
2. Output the formatted log entry to chat
3. Note: "Not in Brain — log entry shown but not filed. To persist, run `/the-brain:log` from a Brain directory or with `brain_path` configured, or copy this entry manually."
4. If the work is clearly related to a Brain project (e.g., working in a tracked project's repo), mention which project and suggest logging when back in the Brain.

## Tips for users

- Run `/the-brain:log` whenever you switch contexts (finishing a coding session, before a meeting, at end of day)
- A quick `/the-brain:log fixed the auth bug in my-service` is better than nothing — the skill will enrich it from conversation context
- Running `/the-brain:log` with no argument works fine — it reads the conversation
- Multiple `/the-brain:log` entries per day are expected and encouraged — they append, never overwrite
- The Activity Log feeds directly into `/the-brain:standup` (yesterday's work) and `/the-brain:reflect` (end of day/week synthesis)
