---
name: reflect
description: Generate a reflection on recent activity. Reviews daily logs, wiki changes, and task completions. Promotes genuine insights into permanent knowledge. Use at end of day or week.
argument-hint: "<day|week>"
---

# /the-brain:reflect — Metacognition

You are generating a reflection on recent Brain activity.

## Mode: Day (default, or argument is "day")

### Step 1: Gather context

- Read today's daily log in `planner/YYYY/MM/` (if it exists)
- Read `planner/tasks.md` for completed and active tasks
- Read recent entries in `log.md` (today's entries)
- Check connectors for today's activity:
  - Jira: tickets updated today
  - Outlook: meetings attended today

### Step 2: Generate daily reflection

Create or update `planner/YYYY/MM/YYYY-MM-DD.md` using the Daily template:
- Fill in the **End-of-Day Summary** section: what was accomplished today (specific — pages created, meetings attended, decisions made, sources ingested), what happened, what shifted, what was learned

### Step 3: Prune tasks

- Move completed tasks out of `planner/tasks.md`
- Record them as accomplishments in the daily log
- This keeps `tasks.md` lean — only the active working set

### Step 4: Check for promotable insights

Review the day's work for insights worth promoting to permanent knowledge:
- Did a meeting reveal something that should update a wiki concept page?
- Did a project decision change the understanding of a broader topic?
- Did you learn something that transcends the specific project context?

If yes, offer to promote: create or update the relevant page in `wiki/` or `pm/` and link back to the daily log as the source.

## Mode: Week (argument is "week")

### Step 1: Gather context

- Read all daily logs from the current week in `planner/YYYY/MM/`
- Read `log.md` entries from the current week
- Read `planner/tasks.md` for task status
- Read `planner/goals.md` for progress tracking

### Step 2: Generate weekly reflection

Create `planner/YYYY/MM/week-WW.md` using the Weekly template (filed under the month that the week's Monday falls in):
- **Accomplished**: aggregate of the week's achievements
- **Learned**: key insights from the week
- **Carrying Over**: unfinished tasks and why
- **Insights to Promote**: genuine insights worth permanent filing

### Step 3: Archive daily logs

Mark daily logs from this week as `status: archived` in their frontmatter.
Update `planner/index.md`: move this week's dailies under "Past Weeks."

### Step 4: Promote insights

For each insight in "Insights to Promote":
- Create or update the relevant page in `wiki/` or `pm/`
- Link back to the weekly reflection
- Update indexes

### Step 5: Log

Append to `log.md`:
```
## [YYYY-MM-DD] reflect | daily (or weekly)
Reflection filed: [[planner/YYYY/MM/YYYY-MM-DD]] (or [[planner/YYYY/MM/week-WW]]). Tasks pruned: N. Insights promoted: N.
```
