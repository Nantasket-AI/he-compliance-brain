---
name: prep
description: Assemble a briefing for an upcoming meeting or event. Pulls project state, recent meetings, entity context, and live connector data. Use before any meeting.
argument-hint: <meeting or topic name>
---

# /the-brain:prep — Meeting Preparation

Ships with the the-brain plugin; available wherever the plugin is enabled.

Assemble a comprehensive briefing for an upcoming meeting or event.

## Brain location

Determine the Brain directory using this priority order:
1. If the current working directory is a Brain (contains a `CLAUDE.md` with the Brain schema and has `wiki/`, `pm/`, and `planner/` subdirectories), use it.
2. Otherwise check the plugin setting `${user_config.brain_path}` and operate on that directory. If the setting is empty or appears as a literal unexpanded placeholder, treat it as unset and continue to step 3.
3. If neither applies, fall back to the **Outside the Brain repo** behavior at the bottom of this skill.

**Claude Cowork:** treat this as a project skill, scoped to the Cowork project it runs in. The project root is the Brain, found by step 1 — `brain_path` does not exist in Cowork and is always unset. If the Cowork project is not a Brain, use the step 3 fallback.

All Brain file paths below are relative to the Brain root once located.

## Step 1: Identify the meeting

- If argument provided, search for it:
  - Check Outlook calendar for matching events
  - Check `pm/index.md` for related projects
- If no argument, check Outlook calendar for the next upcoming meeting
- Determine: what is this meeting about? Who's attending? Which project(s)?

## Step 2: Gather context (inside Brain repo)

**From PM brain:**
- Read the relevant project page(s) in `pm/projects/`
- Read recent meeting pages for the same project/attendees
- Note recent decisions, open questions, and action items

**From Scholar brain:**
- Read entity pages for attendees (who are they, what's their role)
- Read relevant concept pages if the meeting covers technical topics

**From Planner brain:**
- Check `planner/tasks.md` for tasks related to this project/meeting
- Check for existing prep docs in `pm/prep/`

**From connectors:**
- Jira: current sprint status, recently closed/opened tickets for the project
- Outlook: recent email threads with attendees on this topic
- Teams: recent messages in relevant channels
- SharePoint: recently modified documents related to the project

## Step 3: Identify what changed

If this is a recurring meeting, find the last meeting page for the same group/project:
- What decisions were made last time?
- What action items were assigned? Are they done?
- What's new since then?

## Step 4: Generate prep document

Create `pm/prep/YYYY-MM-DD-meeting-slug.md` using the Prep template:
- **Context**: what this meeting is about, with `[[project]]` and `[[entity]]` links
- **Recent Changes**: what's happened since the last meeting, with claim-level links
- **Open Questions to Raise**: unresolved items from project pages and past meetings
- **Suggested Talking Points**: data-backed topics drawn from the Brain
- **Live State**: current Jira sprint, recent PRs, any drift

## Step 5: Update planner

- Add prep doc link to today's daily log if it exists
- Update `pm/index.md` (prep section) with the new prep doc

## Step 6: Log

Append to `log.md`:
```
## [YYYY-MM-DD] prep | Meeting Name
Prep doc: [[pm/prep/YYYY-MM-DD-meeting-slug]]. Project(s): [list]. Key topics: [list].
```

## Step 7: Present

Output the briefing to the user. This should be a 5-minute skim that fully prepares them for the meeting.

## Outside the Brain repo

When no Brain directory is found (neither cwd nor `${user_config.brain_path}` resolves to a Brain), fall back to connector data only:
- Pull calendar event details
- Query Jira for project status
- Search recent emails/messages for context
- Output a lighter briefing to chat (no files created)
