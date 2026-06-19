---
name: project
description: View or create a project in the PM brain. Shows compiled project state with live connector data. Use when checking project status, creating new projects, or getting a project briefing.
argument-hint: "<project-name> or 'new <project-name>'"
---

# /the-brain:project — Project Operations

View, create, or list projects in the PM brain. Each mode synthesizes Brain knowledge with live connector data to give a complete picture.

## Mode: View (argument is an existing project name)

### Step 1: Gather from the Brain

1. Read `pm/index.md` — find the project section, note all associated meetings and notes
2. Read the project page in `pm/projects/` — pull status, milestones, open questions, risks, decision log, stakeholders, architecture, codebase references, Live Context
3. Read all meeting pages linked from the project — pull outstanding action items (with owners and due dates), recent decisions, open questions raised in meetings
4. Read entity pages for project stakeholders in `wiki/entities/` — roles, relationships, key facts
5. Read any related concept pages referenced from the project (e.g., architecture patterns, strategy context)
6. Check `planner/tasks.md` for tasks linked to this project
7. Check `planner/goals.md` for goals related to this project

### Step 2: Gather live state from connectors

Query connectors using metadata from the project page:

- **Jira** (if `jira_project` is set): Search for recent issues using JQL `project = KEY ORDER BY updated DESC`. Get current sprint status. Check for tickets the Brain doesn't know about. Check for status changes (tickets closed that Brain shows open, or vice versa). Check for new comments or updates on tracked tickets.
- **Outlook calendar**: Search for upcoming meetings related to this project (by attendee overlap or subject match). Flag any meetings not yet tracked in the Brain.
- **Teams**: Check project group chat (if a chat ID is listed in Live Context) for recent messages, async decisions, or action items discussed outside of meetings.
- **Outlook email**: Search for recent emails involving project stakeholders.
- **SharePoint**: Check for recently modified documents related to the project.
- **Confluence**: If Confluence page IDs are referenced, query for current content.
- **Codebase** (if `repo` is set): Note the repo path and key files from `repo_docs`. Suggest reading codebase docs for technical questions.

### Step 3: Detect drift

Compare Brain state with connector state:
- **Status drift**: Brain says "Discovery" but Jira shows "Build", or vice versa
- **Timeline drift**: target dates changed in Jira but not in Brain
- **New information**: tickets, meetings, messages, documents the Brain hasn't processed
- **Stale action items**: action items past due date and still open
- **Stakeholder changes**: new people on Jira tickets not in Brain's stakeholder list

Flag drift with `> [!conflict]` callouts showing Brain state vs. connector state.

### Step 4: Present unified briefing

Output a compiled project briefing that synthesizes everything:

- **Overview**: project purpose, current phase/status, timeline
- **Recent decisions**: from meeting pages, with `[[meeting#heading]]` links
- **Open questions and risks**: from project page and recent meetings
- **Outstanding action items**: aggregated from all meeting pages, with owners and due dates. Flag overdue items.
- **Live connector state**: current Jira sprint, open tickets, recent activity
- **Drift warnings**: anything where Brain and connectors disagree
- **Stakeholders**: with `[[wiki/entities/...]]` links and roles
- **Codebase**: repo path and key files to read for technical context (if applicable)
- **What's next**: upcoming meetings, approaching deadlines, planned work

### Step 5: Offer updates

Ask if any updates should be made to the project page based on drift or new information discovered. If the user approves:
- Update the project page
- Update related meeting/entity pages if needed
- Update `pm/index.md` rollup summary if scope changed
- Append to `log.md`:

```
## [YYYY-MM-DD] system | Project briefing: Project Name
Drift found: [summary]. Updated: [pages list]. Action items overdue: N.
```

---

## Mode: Create (argument starts with "new")

### Step 1: Gather project information

Ask the user about the project (or infer from context if they've already provided details):

- **What is it?** — purpose, scope, problem being solved
- **Who's involved?** — stakeholders with roles (customer, lead, team members)
- **Jira project key?** — if tracked in Jira (check with connector if unsure)
- **Repository?** — local path and/or GitHub URL. Key files to read (CLAUDE.md, README.md, etc.)
- **Timeline?** — start date, target date, key milestones
- **Current phase?** — discovery, design, build, testing, etc.
- **Any initial context?** — decisions already made, constraints, architecture choices, meeting notes to reference
- **Related projects?** — links to other Brain projects that overlap or depend on this one

### Step 2: Query connectors for existing data

Before creating, check if data already exists:
- **Jira**: search for the project key or name — pull existing epic/story details, descriptions, assignees
- **Outlook calendar**: search for recurring meetings related to this project
- **Teams**: search for group chats or channels about this project
- **Confluence**: search for existing documentation
- **SharePoint**: search for related documents (PRDs, presentations, etc.)

### Step 3: Create pages

1. Create the project page in `pm/projects/` using the **Project template** from `templates.md`
   - Fill all frontmatter fields: title, type, status, stakeholders, started, target_date, jira_project, repo, repo_docs
   - Populate Overview, Status & Timeline, Stakeholders, Decision Log, Architecture/Design, Open Questions, Risks & Blockers, Live Context, Related Pages
   - Live Context should include Jira references, calendar entries, Teams chat links, Confluence page references — all discovered from connectors

2. Create entity pages in `wiki/entities/` for each stakeholder not already in the Brain
   - Use the Entity template from `templates.md`
   - Include role, email, relationships, and sources

3. Cross-reference: link the project page from entity pages (Relationships section) and from any related concept pages

### Step 4: Update indexes and overviews

1. Add the project section to `pm/index.md` — include the project page link, any initial meeting pages, and a rollup summary
2. Update `pm/overview.md` — add the new project to the active projects narrative
3. Update `wiki/index.md` — add any new entity pages created

### Step 5: Log

Append to `log.md`:

```
## [YYYY-MM-DD] system | Created project: Project Name
New project page: [[pm/projects/project-slug]]. Stakeholders: [list with entity links]. Jira: KEY. Entity pages created: [list]. Indexes updated.
```

### Step 6: Present

Output a summary of everything created, with `[[wikilinks]]` to each page. Suggest next steps (schedule a meeting, ingest existing notes, set up Jira tickets).

---

## Mode: List (no argument)

1. Read `pm/index.md` — present all projects organized by status (active, paused, completed)
2. For each active project, include: name, status, phase, last updated date, next milestone or meeting
3. Flag any projects that haven't been updated in 2+ weeks
4. Suggest running `/the-brain:sync` if any projects look stale
