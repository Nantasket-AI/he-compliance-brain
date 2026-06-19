---
name: plot
description: Generate planner daily files for the full Mon–Fri work week. Synthesizes Brain knowledge (projects, action items, tasks, entity context) with live connector data (calendar, Jira, Teams, email) into rich, context-aware daily plans.
---

# /the-brain:plot — Plot the Week

Generate or update planner daily files for every day of the current Mon–Fri work week. This skill synthesizes **local Brain knowledge** (project state, decisions, action items, entity context, tasks, goals) with **live connector data** (Outlook calendar, Jira, Teams, email) to produce daily plans that are aware of the full project narrative — not just calendar events.

## Argument

`<week-offset>` (optional) — `0` for current week (default), `1` for next week. Allows plotting ahead.

## Step 1: Determine the work week

Calculate the Mon–Fri dates for the target week based on today's date (or next week if offset = 1).

## Step 2: Gather week-wide context

Do all information gathering up front, once, before generating any files.

### From the Brain (local knowledge)

- Read `pm/overview.md` — what's active and in-flight
- Read `pm/index.md` — identify all active projects, their meetings, and notes
- Read each active project page in `pm/projects/` — pull:
  - Current status and phase
  - Next milestones and target dates
  - Open questions and risks
  - Recent decision log entries
  - Stakeholder list (with entity links)
  - Upcoming meetings (from Live Context / calendar sections)
- Read recent meeting pages in `pm/meetings/` — pull:
  - Outstanding action items with owners and due dates
  - Decisions that need follow-up
  - Open questions raised
- Read `planner/tasks.md` — active, maintenance, and blocked tasks
- Read `planner/goals.md` — longer-term priorities and progress tracking
- Read `log.md` (recent entries) — what's already been accomplished, what shifted
- Read entity pages (`wiki/entities/`) for stakeholders who appear in this week's meetings — have their context ready

### From connectors (live external state)

- **Outlook calendar**: Query the full Mon–Fri range for all events (meetings, all-day events, OOO markers)
- **Jira**: Query for tickets assigned to user — recent updates, approaching deadlines, sprint state, new tickets since last sync
- **Teams**: Check project group chats (listed in project page Live Context sections) for recent unread messages or async decisions
- **Outlook email**: Scan for relevant emails (project-related threads, stakeholder communications from this week)

## Step 3: Synthesize and distribute across the week

Before generating individual day files, build a **week-level picture**:

- **Map meetings → projects**: Match each calendar event to its project via attendee overlap with project stakeholder lists, subject keyword match, or explicit `projects:` links in existing Brain meeting pages.
- **Map action items → due dates**: Place each outstanding action item on its due date. If due date is past, place on the earliest upcoming day as overdue.
- **Identify milestones**: Project milestones and Jira deadlines landing this week — place on appropriate days.
- **Distribute tasks**: Take tasks from `planner/tasks.md` and distribute them across days based on:
  - Hard deadlines (put before the deadline)
  - Meeting dependencies ("must prepare X before Thursday's meeting")
  - Available deep-work time (prefer days with fewer meetings)
  - Priority level
- **Flag meeting load**: Identify heavy meeting days vs. deep-work-available days.
- **Note dependencies**: Cross-day dependencies like "Must do X before Wednesday's meeting with Y" or "Prep for Thursday's presentation should happen Tuesday/Wednesday."

## Step 4: Generate/update each day (Mon–Fri)

For each day in the work week, apply the following logic:

### Past days (before today) with existing daily files
**Skip** — do not overwrite the Activity Log or End-of-Day Summary that `/the-brain:reflect` may have filled in. Exception: if calendar events have changed (cancellations, new meetings), update only the Schedule section.

### Today
Create or update the daily file with **full detail** — equivalent to `/the-brain:myday` output:
- **Schedule**: all calendar events with times, attendees (wikilinked to `[[wiki/entities/...]]`), location
- **Priorities**: top 3–5 items drawn from tasks, project state, and deadlines
- **Tasks for Today**: specific tasks distributed from the week-level picture
- **Meeting Prep**: detailed per-meeting sections with project context, recent decisions, open questions, talking points, attendee entity links
- **Looking Ahead**: table of remaining week
- **Activity Log**: placeholder (appended by `/the-brain:log` throughout the day)
- **End-of-Day Summary**: placeholder (filled by `/the-brain:reflect`)

### Future days
Create or update the daily file with **forward-looking detail**:
- **Schedule**: calendar events with attendees (wikilinked), times, location
- **Project context per meeting**: which project each meeting relates to (`[[pm/projects/...]]`), what's changed since last meeting for that project, key decisions pending, open questions to raise
- **Tasks for the day**: distributed from the week-level picture — what to work on, what's due, what to prepare for upcoming meetings
- **Action item follow-ups**: any action items from previous meetings due on or before this day
- **Meeting prep notes**: attendee entity links, project state summary, what to prepare, talking points drawn from Brain knowledge (recent decisions, open questions, risks). Lighter than today's prep but enough to see at a glance what's coming.
- **Dependencies**: things that must be done before this day's meetings
- **Flags**: deadlines, presentations, all-day events, heavy meeting load, OOO markers

### Daily file format

All daily files use the standard template:

```yaml
---
title: "YYYY-MM-DD"
type: daily
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily, planner]
---
```

Sections: Schedule, Priorities, Tasks for Today, Meeting Prep (subsection per meeting), Looking Ahead This Week, Activity Log (placeholder), End-of-Day Summary (placeholder).

Use `[[wikilinks]]` throughout — entity pages, project pages, meeting pages, concept pages. Every meeting links to its project. Every person links to their entity. Every task links to its source.

## Step 5: Update planner index

Update `planner/index.md` — ensure all five daily files for the week are listed under "Current Week" with:
- `[[planner/YYYY/MM/YYYY-MM-DD]]` wikilink
- Day of week
- Meeting count
- One-line summary (key events, deadlines)

## Step 6: Update dashboard

Regenerate the "Upcoming This Week" section of `planner/dashboard.md` with the full week's events, milestones, deadlines, and distributed tasks.

## Step 7: Log

Append to `log.md`:

```
## [YYYY-MM-DD] system | Week plotted (Mon DD – Fri DD)
Days generated: N new, N updated, N skipped (past with existing content). Meetings this week: N. Key deadlines: [list]. Action items due this week: [count].
```

## Step 8: Present summary

Output a **week-at-a-glance** to the user:

- Each day's meeting count, key events, and deadlines
- Distributed tasks per day
- Cross-day dependencies highlighted
- Heavy vs. light meeting days flagged
- Any warnings (overdue action items, unconfirmed meetings, conflicts)
