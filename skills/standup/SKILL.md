---
name: standup
description: Generate a standup summary. Reviews yesterday's activity, completed and in-progress tasks, and blockers. Produces a concise update for your next standup meeting plus a plan for today.
---

# /the-brain:standup — Standup Summary

Ships with the the-brain plugin; available wherever the plugin is enabled.

Generate a clean three-part standup update. Output to chat only — no files created. The output should be concise enough to paste into Slack or read aloud in under 60 seconds, but grounded in the full picture from the Brain and connectors.

## Brain location

Determine the Brain directory using this priority order:
1. If the current working directory is a Brain (contains a `CLAUDE.md` with the Brain schema and has `wiki/`, `pm/`, and `planner/` subdirectories), use it.
2. Otherwise check the plugin setting `${user_config.brain_path}` and operate on that directory. If the setting is empty or appears as a literal unexpanded placeholder, treat it as unset and continue to step 3.
3. If neither applies, fall back to the **Outside the Brain repo** behavior at the bottom of this skill.

**Claude Cowork:** treat this as a project skill, scoped to the Cowork project it runs in. The project root is the Brain, found by step 1 — `brain_path` does not exist in Cowork and is always unset. If the Cowork project is not a Brain, use the step 3 fallback.

All Brain file paths below are relative to the Brain root once located.

## Inside the Brain repo

### Step 1: Gather from the Brain

Read local Brain state to build a complete picture of yesterday and today:

- Read yesterday's daily file in `planner/YYYY/MM/` — Activity Log, End-of-Day Summary, tasks that were planned
- Read `log.md` entries from yesterday — every operation that changed the Brain (ingests, syncs, queries, system changes)
- Read today's daily file in `planner/YYYY/MM/` if `/the-brain:myday` already ran — today's planned tasks and priorities
- Read `planner/tasks.md` — active tasks (what's in progress), blocked tasks (what's stuck), maintenance tasks
- Read `planner/goals.md` — check if any goal milestones were hit or are approaching
- Read `pm/overview.md` — active project state for framing
- Read active project pages in `pm/projects/` — check for action items due yesterday or today, status changes, approaching deadlines
- Read recent meeting pages in `pm/meetings/` — decisions made yesterday, action items assigned to you

### Step 2: Gather live state from connectors

Augment Brain knowledge with current connector data:

- **Jira**: tickets updated yesterday (resolved, commented, transitioned), tickets assigned for today, sprint progress, any tickets newly assigned since yesterday
- **Outlook calendar**: meetings attended yesterday (for accomplishment list), meetings today (for plan)
- **Teams**: any notable project chat activity from yesterday that's worth mentioning

### Step 3: Synthesize the three parts

Build the standup by synthesizing Brain knowledge and connector data:

**Yesterday** — what was actually accomplished (not just what was planned):
- Specific accomplishments: meetings attended and key outcomes, decisions made, tasks completed, sources ingested, pages created/updated, Jira tickets moved
- Pull from yesterday's daily file Activity Log section, `log.md` entries, and Jira activity
- If yesterday's plan existed, note what was planned vs. what actually happened — highlight anything that shifted

**Today** — what's planned and why:
- Tasks to tackle: from today's daily plan and `planner/tasks.md`, ordered by priority
- Meetings to attend: from calendar, with project context (what each meeting is about)
- Deadlines approaching: Jira due dates, project milestones this week
- Key focus: the single most important thing to accomplish today

**Blockers** — anything preventing progress:
- Blocked tasks from `planner/tasks.md` with explanation of what's blocking them
- Open risks from project pages that are actively impeding work
- External dependencies: waiting on someone, waiting on access, waiting on a decision
- If no blockers, say "None"

### Step 4: Format output

```
**Yesterday:**
- Accomplished item 1
- Accomplished item 2

**Today:**
- Planned item 1
- Planned item 2

**Blockers:**
- Blocker description (or "None")
```

**Formatting rules:**
- Each bullet is **one concise line** — no multi-sentence bullets
- Be specific: "Ingested sprint review transcript, created meeting page" not "Worked on Brain"
- Be specific: "Closed PROJ-117, posted Jira description" not "Did Jira work"
- Use project names to provide context: "Prepped for quarterly review presentation (Wed)" not "Did presentation prep"
- Maximum 3–5 bullets per section — this is a standup, not a status report
- Formatted for pasting into Slack or reading aloud in under 60 seconds

### Step 5: Log (optional)

If the user asks, append to `log.md`:

```
## [YYYY-MM-DD] system | Standup generated
Yesterday: [count] items. Today: [count] items. Blockers: [count or "none"].
```

Standup logging is optional since the standup itself doesn't change the Brain — it's a read-only synthesis.

## Outside the Brain repo

When no Brain directory is found (neither cwd nor `${user_config.brain_path}` resolves to a Brain), fall back to connector data only:
- **Jira**: tickets updated yesterday, tickets assigned for today, sprint status
- **Outlook calendar**: meetings attended yesterday, meetings scheduled today
- **Outlook email**: notable emails from yesterday
- Present a simple three-part standup to chat (no files created, no Brain pages read)
