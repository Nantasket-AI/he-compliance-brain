---
name: myday
description: Generate a daily briefing with schedule, priorities, and context. Pulls from calendar, tasks, goals, and project state. Use first thing in the morning to plan the day.
---

# /the-brain:myday — Daily Briefing

Ships with the the-brain plugin; available wherever the plugin is enabled.

Generate a comprehensive daily plan. This skill works anywhere but is richer inside the Brain repo.

## Brain location

Determine the Brain directory using this priority order:
1. If the current working directory is a Brain (contains a `CLAUDE.md` with the Brain schema and has `wiki/`, `pm/`, and `planner/` subdirectories), use it.
2. Otherwise check the plugin setting `${user_config.brain_path}` and operate on that directory. If the setting is empty or appears as a literal unexpanded placeholder, treat it as unset and continue to step 3.
3. If neither applies, fall back to the **Outside the Brain repo** behavior at the bottom of this skill.

**Claude Cowork:** treat this as a project skill, scoped to the Cowork project it runs in. The project root is the Brain, found by step 1 — `brain_path` does not exist in Cowork and is always unset. If the Cowork project is not a Brain, use the step 3 fallback.

All Brain file paths below are relative to the Brain root once located.

## Hard Constraints

- **Never run code or scripts.** This skill must complete using only tool calls (Read, Edit, Write, Glob, Grep) and MCP connector queries. Parse all JSON, calendar responses, and Jira results directly — you are capable of reading structured data without executing code. If a connector returns data too large to fit in context, use the Agent tool to have a subagent read and summarize the file.
- **All times in user's primary timezone first, secondary timezone in parentheses.** Calendar connectors return UTC — always convert per the Timezone Convention in CLAUDE.md. See CLAUDE.md Timezone Convention.

## Inside the Brain repo

### Step 1: Gather context from the Brain (local knowledge)

Read local Brain state to understand what's active, what's pending, and what history exists:

- Read `pm/overview.md` — what projects are active and in-flight
- Read `pm/index.md` — identify all active projects and their recent meetings/notes
- Read each active project page in `pm/projects/` — pull current status, next milestones, open questions, risks, recent decision log entries, stakeholders
- Read recent meeting pages in `pm/meetings/` — outstanding action items (with owners and due dates), decisions that need follow-up, open questions raised
- Read `planner/tasks.md` — active, maintenance, and blocked tasks
- Read `planner/goals.md` — longer-term priorities and progress tracking
- Read `log.md` (recent entries) — yesterday's activity, what's been accomplished, what shifted
- Read yesterday's daily file in `planner/YYYY/MM/` if it exists — unfinished tasks, End-of-Day Summary, Activity Log
- Read entity pages (`wiki/entities/`) for people appearing in today's meetings — have their context ready

### Step 2: Gather live state from connectors

Query external systems for current data (this runs **after** `/the-brain:sync` in Step 3b, so project pages are already updated):

- **Outlook calendar**: today's events — time, attendees, subject, location
- **Jira**: tickets assigned to user — recent updates, approaching deadlines, sprint state
- Check if prep docs exist in `pm/prep/` for any of today's meetings
- Check if there are relevant project pages in `pm/projects/` for each meeting (match via attendee overlap with project stakeholders, subject keywords, or explicit project links)

### Step 3: Synthesize

Before generating the daily plan, build a **picture of the day** by combining Brain knowledge with live data:

- **Map each meeting → its project**: via attendee overlap, subject match, or existing Brain meeting page links. Pull that project's current state, open questions, and recent decisions.
- **Classify all tasks into three buckets** (used in Step 4 and Step 7):
  1. **Due Today / Overdue** — tasks with an explicit date of today or earlier (look for date markers like `(2026-04-14)` in task text), plus open action items from meeting pages with today's or past due dates. Flag overdue items prominently.
  2. **Upcoming This Week** — tasks tied to meetings or milestones later this week: prep tasks whose prerequisite meeting falls Mon–Fri of this week, action items from meeting pages due later this week, project milestone tasks with this-week deadlines.
  3. **All Outstanding** — every other open task from `planner/tasks.md` and open meeting action items not captured above. This is the full backlog view.
- **Set priorities**: derive top 3–5 priorities from the synthesis of project state, task urgency, meeting prep needs, and goal alignment.
- **Flag concerns**: overdue items, unfinished work from yesterday, stale projects, un-ingested meetings, upcoming deadlines this week.

### Step 3b: Daily sync + day-of-week maintenance

**Every day (Mon–Fri)**: Invoke `/the-brain:sync` first, before anything else.
- **`/the-brain:sync`**: Query live connectors (Jira, calendar, Teams) for all active projects. Flag drift between connector state and Brain pages. Update project pages to match.
- This ensures all subsequent steps (plan generation, dashboard, briefing) use current data.

Then check today's day of the week for additional maintenance:

**If Monday** (after sync): Invoke `/the-brain:lint`, then `/the-brain:plot`.
1. **`/the-brain:lint`**: Perform the full lint health check (index integrity, orphans, broken anchors, stale content, overdue action items, cross-brain gaps, archive candidates). Apply auto-fixes. Resolve any errors before proceeding. Carry unresolved issues forward as tasks.
2. **`/the-brain:plot`**: Generate or update planner daily files for the full Mon–Fri work week. Synthesizes Brain knowledge (project state, action items, tasks, entity context) with live connector data (calendar, Jira, Teams, email). Distributes tasks across the week, maps meetings to projects, flags dependencies.
3. Then proceed with regular `/the-brain:myday` steps (Step 4 onward) for today.
4. Note in the briefing: "🔄 Sync ran. 🔧 Lint ran — N issues, N fixed. 📅 Week plotted (Mon–Fri)."

**If Tuesday–Thursday** (after sync): No extra steps.
- Proceed directly with regular `/the-brain:myday` steps (Step 4 onward).
- Note in the briefing: "🔄 Sync ran."

**If Friday** (after sync): Invoke `/the-brain:reflect` after generating the daily plan (Step 4), before updating the dashboard (Step 5).
- **`/the-brain:reflect`**: Review the week's activity from `log.md` and the week's daily files. Prune completed tasks from `planner/tasks.md`. Promote genuine insights to permanent wiki/pm knowledge. Generate the weekly reflection entry in `planner/YYYY/MM/week-WW.md`.
- Note in the briefing: "🔄 Sync ran. 🪞 Reflect ran — tasks pruned, insights filed."

### Execution order summary

| Day | Order |
|-----|-------|
| Monday | /the-brain:sync → /the-brain:lint → /the-brain:plot → /the-brain:myday |
| Tue–Thu | /the-brain:sync → /the-brain:myday |
| Friday | /the-brain:sync → /the-brain:myday → /the-brain:reflect |

### Step 4: Generate daily plan

Create or update `planner/YYYY/MM/YYYY-MM-DD.md` using the Daily template. The plan should be a **synthesis** of Brain knowledge and live connector data — not just a calendar dump:

- **Schedule**: today's meetings with times, attendees (wikilinked to `[[wiki/entities/...]]`), location, and which project each meeting connects to (`[[pm/projects/...]]`)
- **Priorities**: top 3–5 items derived from the synthesis step — project urgency, task deadlines, meeting prep needs, goal alignment. Each with context explaining *why* it's a priority today.
- **Tasks**: Show all tasks in three clearly labeled sections (never collapse or omit any section even if empty):
  - **Due Today / Overdue** — tasks explicitly dated today or earlier; open action items from meeting pages due today or past due. Mark overdue items with ⚠️.
  - **Upcoming This Week** — tasks tied to this week's meetings, milestones, or deadlines. Include which day/meeting they're tied to.
  - **All Outstanding** — the complete open task backlog from `planner/tasks.md` and open meeting action items not listed above. Full list, no filtering.
- **Meeting Prep**: per-meeting subsections with:
  - Attendee entity links and roles
  - Project context: current status, what's changed since last meeting, recent decisions
  - Open questions to raise (from project pages and meeting pages)
  - Talking points drawn from Brain knowledge
  - Link to existing prep doc if one exists in `pm/prep/`
- **Looking Ahead**: table of rest-of-week events, deadlines, and dependencies
- **Activity Log**: placeholder (appended by `/the-brain:log`)
- **End-of-Day Summary**: placeholder (filled by `/the-brain:reflect`)

Use `[[wikilinks]]` throughout — every person links to their entity, every meeting links to its project, every task links to its source.

### Step 5: Update dashboard

Regenerate `planner/dashboard.md` with today's unified view:
- Today's schedule
- Top priorities
- Tasks — three labeled sections: **Due Today / Overdue**, **Upcoming This Week**, **All Outstanding**
- Project status summaries
- Any warnings (overdue tasks, stale projects, un-ingested meetings)

### Step 6: Log

Append to `log.md`:
```
## [YYYY-MM-DD] system | Daily plan generated
Meetings: N. Active tasks: N. Priorities: [top 3].
```

### Step 7: Present

Output the daily briefing to the user. Highlight:
- What needs prep before meetings
- What's most urgent
- Any flags from yesterday (unfinished tasks, follow-ups)
- **Task view — always show all three labeled sections:**
  - **Due Today / Overdue** — act on these first; ⚠️ flag anything past due
  - **Upcoming This Week** — context for planning the rest of the week; note which day/meeting each is tied to
  - **All Outstanding** — the full open backlog; nothing hidden

## Outside the Brain repo

When no Brain directory is found (neither cwd nor `${user_config.brain_path}` resolves to a Brain), fall back to connector data only:
- Query Outlook calendar for today's events
- Query Jira for assigned tickets
- Present a simple daily briefing to chat (no files created)
