---
name: ticket
description: "Create or update a Jira ticket grounded in Brain knowledge. Pulls project context, meeting decisions, and action items to draft a well-structured ticket. Always presents a draft for approval before creating/updating in Jira."
argument-hint: "<action> <description> — e.g. 'create story for webhook integration' or 'update PROJ-117 with discovery findings'"
---

# /the-brain:ticket — Draft a Jira Ticket from Brain Context

Create or update a Jira ticket that is grounded in the Brain's accumulated knowledge — project decisions, meeting outcomes, action items, architecture context, and live connector state. The ticket should be thorough enough that any team member can understand the work without digging through meetings or chat history.

**CRITICAL**: This skill NEVER creates or updates a Jira ticket without explicit user approval. It ALWAYS presents a complete draft first. Only after the user confirms ("create it", "looks good", "go ahead") does it interact with Jira.

## Step 1: Parse the request

Determine from the user's input:

- **Action**: `create` (new ticket) or `update` (existing ticket)
- **For updates**: the ticket key (e.g., `PROJ-117`) — if not provided, search for it
- **Project**: which Jira project (use the `jira_project` field from the relevant Brain project page)
- **Summary**: what the ticket is about — one-line title
- **Type**: Story, Task, Bug, Feature, Spike, Epic, Sub-task — infer from context or ask
- **Parent**: if this is a child of an epic or story, identify the parent ticket
- **Context**: which Brain project(s), meeting(s), or decision(s) this ticket relates to

If the request is ambiguous (e.g., unclear whether it's a Story or Task, or which project it belongs to), ask the user to clarify before proceeding.

## Step 2: Gather Brain context

Navigate the Brain to collect all relevant information:

1. **Project page** (`pm/projects/`): current status, architecture decisions, open questions, stakeholders, repo reference, existing Jira tickets. This establishes *why* this ticket exists and how it fits into the project.
2. **Meeting pages** (`pm/meetings/`): if the ticket stems from a meeting decision or action item, pull the specific decision and its context. Reference the meeting heading for provenance.
3. **Decision log**: find the specific decisions that motivate this ticket — these become the ticket's rationale.
4. **Action items**: check `planner/tasks.md` and meeting pages for action items that this ticket formalizes.
5. **Technical context**: if the project has a `repo` reference, note relevant architecture constraints or codebase references that should be in the ticket.
6. **Entity context**: who should be assigned? Who are the stakeholders? Check entity pages for roles.

## Step 3: Gather live state from Jira

Query the Jira connector to understand the current ticket landscape:

- **For creates**: search for existing tickets in the project to avoid duplicates. Check the epic structure. Get available issue types for the project (`getJiraProjectIssueTypesMetadata`).
- **For updates**: read the current ticket state (`getJiraIssue`) — current description, status, fields. Understand what's changing vs. what's staying.
- **Parent/child relationships**: if the ticket should be a child of an epic, verify the parent exists and get its key.
- **Available transitions**: if the update includes a status change, get valid transitions (`getTransitionsForJiraIssue`).

## Step 4: Draft the ticket

### For new tickets, draft:

- **Project**: Jira project key
- **Type**: issue type (Story, Task, Bug, etc.)
- **Summary**: clear, specific, action-oriented title (under 100 chars)
- **Description**: structured markdown with:
  - **Context/Background**: why this ticket exists — reference the project, meeting decisions, or stakeholder needs that motivate it. Include Brain wikilinks for internal traceability (these won't render in Jira but serve as a breadcrumb).
  - **Objective**: what "done" looks like — concrete deliverables
  - **Scope / Acceptance Criteria**: bullet list of specific requirements. Derived from Brain project pages, meeting decisions, and technical context.
  - **Technical Notes** (if applicable): architecture constraints, relevant codebase references, dependencies
  - **Open Questions** (if any): unresolved items that may affect implementation
  - **References**: links to relevant Jira tickets, Confluence pages, SharePoint docs, or other external resources
- **Parent**: epic or story key (if applicable)
- **Assignee**: suggest based on Brain context (resolve name to Jira account ID via `lookupJiraAccountId`)
- **Priority**: suggest based on urgency signals from Brain (deadlines, stakeholder emphasis)
- **Labels**: suggest based on project tags and content
- **Additional fields**: any custom fields the project uses

### For updates, draft:

- **Ticket key**: the existing ticket to update
- **Fields to change**: show current value → proposed value for each field
- **Description changes**: show a clear diff — what's being added, removed, or modified
- **Status transition** (if applicable): current status → target status, with transition ID
- **Comment** (if applicable): a comment summarizing why the update is happening, grounded in Brain context

## Step 5: Present the draft for approval

Display the draft clearly:

```
**Action**: [Create / Update]
**Project**: [PROJECT-KEY]
**Type**: [Story / Task / etc.]
**Parent**: [PROJ-115 (if applicable)]
**Assignee**: [Name]
**Priority**: [Medium]

**Summary**: [One-line title]

**Description**:
[Full formatted description]

**Brain Context**: Grounded in [[project-page]], [[meeting-page#decision-heading]].
```

Then ask: **"Ready to create/update in Jira, or want changes?"**

## Step 6: Execute (only after approval)

### For creates:
Use `createJiraIssue` with all drafted fields. Use `contentFormat: "markdown"` for the description.

If a parent is specified, include it in the `parent` field.

After creation, report the new ticket key and URL.

### For updates:
Use `editJiraIssue` for field updates. Use `transitionJiraIssue` for status changes. Use `addCommentToJiraIssue` for comments.

After update, report what changed.

## Step 7: Update the Brain

After successful Jira interaction:

1. **Update the project page** (`pm/projects/`): add the new ticket to the Live Context section. If the ticket represents a decision, add it to the decision log.
2. **Update tasks**: if the ticket formalizes an action item from `planner/tasks.md` or a meeting page, mark that action item as done (linked to the new ticket).
3. **Update indexes** if a new project-level artifact was created.

Append to `log.md`:

```
## [YYYY-MM-DD] system | /the-brain:ticket — [created/updated] [TICKET-KEY]
[Created/Updated] [issue type] in [project]. Summary: "[title]". Grounded in [[project-page]], [[meeting-page]]. [Assigned to: Name].
```
