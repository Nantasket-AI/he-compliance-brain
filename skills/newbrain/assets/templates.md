# Page Templates

Referenced by skills when creating new pages. Each template shows expected frontmatter and section structure.

---

## Connector Reference Stub (raw/)

Used for Outlook emails, Teams chats/channel messages, and Teams meeting transcripts. Per data governance policy, these sources are **never stored verbatim** in `raw/`. A `.ref.md` stub is saved instead, providing retrieval keys so the content can be re-fetched via connector. Derived Brain pages (meeting pages, notes, decisions) point their `raw_source:` frontmatter at this stub.

**File naming**: `raw/YYYY-MM-DD-descriptive-slug.ref.md`

```markdown
---
title: <subject> — Connector Reference
type: connector-reference
source_system: teams-transcript | outlook-email | teams-chat
date: YYYY-MM-DD
# System-specific retrieval keys (include whichever apply):
meeting_subject: ""
organizer: ""
attendees: []
event_id: ""
online_meeting_id: ""
recording_url: ""
chat_deep_link: ""
message_id: ""
email_search_query: ""
---

# <subject> — Connector Reference

**This is a reference stub — content is NOT stored here, per data governance policy.**

**To retrieve:** <exact connector tool + ID/URI/search query to re-pull the content>
**Fallback:** <e.g. search Outlook calendar for "<subject>" on <date>; ask the user to paste>
**Retention note:** source content expires per the source system's retention policy; once expired, rely on the derived Brain pages below.

**Derived pages:** [[pm/meetings/YYYY-MM-DD-meeting-slug]]
```

---

## Wiki: Entity

```markdown
---
title: Entity Name
type: entity
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [entity, category]
---

# Entity Name

Brief summary of who/what this entity is.

## Key Facts

- Fact with source ([[wiki/sources/source-name#relevant-heading]])
- Another fact ([[pm/meetings/meeting-name#heading]])

## Relationships

- Role/connection to [[wiki/entities/other-entity]]
- Involved in [[pm/projects/project-name]]

## Sources

- [[wiki/sources/source-name]]
- [[raw/YYYY-MM-DD-source.ext]]
```

---

## Wiki: Concept

```markdown
---
title: Concept Name
type: concept
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [concept, domain]
---

# Concept Name

One-paragraph definition.

## Key Aspects

### Aspect One

Explanation with source ([[wiki/sources/source-name#heading]]).

### Aspect Two

Explanation with source.

## Related Concepts

- [[wiki/concepts/related-concept]] — how they relate
- [[wiki/concepts/another-concept]] — contrast or connection

## Sources

- [[wiki/sources/source-name]]
```

---

## Wiki: Source Summary

```markdown
---
title: "Source Title"
type: source
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [source, domain]
raw_source: raw/YYYY-MM-DD-slug.ext
---

# Source Title

Source: [[raw/YYYY-MM-DD-slug.ext]]

**Author:** Name | **Date:** YYYY-MM-DD | **Type:** article/paper/report

One-paragraph summary of what this source covers and why it matters.

## Key Findings

### Finding One

Detail with context. This is a linkable anchor — other pages reference [[wiki/sources/this-page#finding-one]].

### Finding Two

Detail with context.

### Finding Three

Detail with context.

## Detailed Notes

Deeper notes organized by topic. Each section is a stable heading anchor.

## Related Pages

- [[wiki/concepts/concept]] — connection
- [[wiki/entities/entity]] — mentioned in source
- [[pm/projects/project]] — relevant to
```

---

## Wiki: Analysis

```markdown
---
title: Analysis Title
type: analysis
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [analysis, domain]
---

# Analysis Title

## Question / Framing

What question is this analysis addressing? What prompted it?

## Synthesis

The answer, with claim-level citations:

- Claim one ([[wiki/sources/source#heading]])
- Claim two ([[pm/meetings/meeting#heading]])

## Evidence

### Supporting Evidence

- Evidence point ([[source#heading]])

### Contradicting Evidence

- Counter-evidence ([[source#heading]])

## Conclusion

Summary judgment with confidence level and what would change it.

## Related Pages

- [[wiki/concepts/concept]]
- [[pm/projects/project]]
```

---

## PM: Project

```markdown
---
title: Project Name
type: project
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [project, domain]
status: active
stakeholders: ["[[wiki/entities/person]]"]
started: YYYY-MM-DD
target_date: YYYY-MM-DD
jira_project: KEY
repo: /path/to/repo
repo_docs: ["CLAUDE.md", "README.md"]
---

# Project Name

## Overview

What this project is, why it exists, and what success looks like.

## Status & Timeline

Current status, key milestones, and upcoming deadlines.

## Codebase

**Repo**: `/path/to/repo` (and/or GitHub URL)

Key files for technical context:
- `CLAUDE.md` — architecture, hard constraints, module map, data flows
- `README.md` — setup, prerequisites, getting started

**Reading guidance**: For technical questions, read the codebase docs directly — they are the ground truth. This project page provides the narrative (why, decisions, stakeholders); the codebase docs provide the technical detail (how, constraints, APIs).

## Stakeholders

- [[wiki/entities/person]] — role on this project

## Decision Log

Chronological. Each entry links to the meeting where the decision was made.

### YYYY-MM-DD — Decision Title

Decision description ([[pm/meetings/meeting-name#decision-heading]]).

## Architecture / Design

Technical details, diagrams, key design choices and their rationale.

## Open Questions

- Question with context and who needs to answer

## Risks & Blockers

- Risk/blocker with severity and mitigation plan

## Live Context

- Jira: `KEY` project — query for current sprint/tickets
- Repo: `org/repo` — query for recent PRs/activity

## Related Pages

- [[wiki/concepts/concept]] — relevant technology/methodology
- [[pm/meetings/meeting]] — related meetings
```

---

## PM: Meeting

```markdown
---
title: "Meeting Title — YYYY-MM-DD"
type: meeting
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [meeting, project-tag]
date: YYYY-MM-DD
attendees: ["Person A", "Person B"]
projects: ["[[pm/projects/project-name]]"]
action_items:
  - task: "Description"
    owner: "Person"
    due: YYYY-MM-DD
    status: open
# For Teams meetings: raw_source points to the .ref.md connector-reference stub (never the verbatim transcript).
# For in-person/phone meetings with handwritten notes: raw_source points to the verbatim notes file.
raw_source: raw/YYYY-MM-DD-meeting-slug.ref.md
---

# Meeting Title — YYYY-MM-DD

# For Teams meetings, Source points to the connector-reference stub:
Source: [[raw/YYYY-MM-DD-meeting-slug.ref.md]]

**Attendees:** Person A, Person B | **Projects:** [[pm/projects/project-name]]

## Summary

2-3 sentence overview of what the meeting covered and the key outcome.

## Decisions Made

### Decision Title

What was decided, with rationale. This heading is a stable anchor — project pages link here via [[pm/meetings/this-page#decision-title]].

### Another Decision

Details.

## Action Items

- [ ] Task description — **Owner:** Person — **Due:** YYYY-MM-DD — [[pm/projects/project-name]]

## Open Questions

- Question raised but not resolved — who will follow up

## Topics Discussed

### Topic One

Discussion details, arguments for and against.

### Topic Two

Discussion details.
```

---

## PM: Note

```markdown
---
title: "Note Title"
type: note
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [note, domain]
date: YYYY-MM-DD
projects: ["[[pm/projects/project-name]]"]
context: "What prompted this note"
raw_source: raw/YYYY-MM-DD-note-slug.ext
---

# Note Title

Source: [[raw/YYYY-MM-DD-note-slug.ext]]

## Content

Cleaned-up content from the raw note. Organized with granular headings.

### Key Point One

Detail with context.

### Key Point Two

Detail with context.

## Extracted Insights

- Insight linked to [[wiki/concepts/concept]] or [[pm/projects/project]]

## Tasks Extracted

- [ ] Task — **Owner:** Person — filed in [[planner/tasks]]
```

---

## Planner: Daily

**Location:** `planner/YYYY/MM/YYYY-MM-DD.md` (e.g., `planner/2026/04/2026-04-13.md`)

Daily files are dual-purpose: they start the day as a **plan** (schedule, priorities, tasks) and accumulate an **activity log** throughout the day as `/the-brain:log` appends entries. At end of day, `/the-brain:reflect` fills the summary.

```markdown
---
title: "YYYY-MM-DD"
type: daily
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily, planner]
---

# YYYY-MM-DD

## Schedule

- HH:MM — Event ([[pm/prep/prep-doc]] if exists)

## Priorities

1. Priority with context and links

## Tasks for Today

- [ ] Task from [[planner/tasks]]

## Meeting Prep

- [[pm/prep/event-name]] — key points

## Activity Log

(Appended by /the-brain:log throughout the day — timestamped entries of what was worked on)

## End-of-Day Summary

(Filled by /the-brain:reflect — what happened, what shifted, what you learned)
```

---

## Planner: Weekly

**Location:** `planner/YYYY/MM/week-WW.md` (e.g., `planner/2026/04/week-16.md`). Filed under the month of the week's Monday.

```markdown
---
title: "YYYY-Www"
type: weekly
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [weekly, planner]
---

# Week of YYYY-MM-DD to YYYY-MM-DD

## Accomplished

- What was completed, with links to relevant pages

## Learned

- Insights worth remembering, with links

## Carrying Over

- What didn't get done and why — links to tasks

## Insights to Promote

(Genuine insights that should be promoted from Planner into Scholar or PM as permanent knowledge)
```

---

## PM: Prep

**Location:** `pm/prep/` (e.g., `pm/prep/event-name.md`). Indexed in `pm/index.md`.

```markdown
---
title: "Prep — Event Name"
type: prep
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [prep, pm]
event_date: YYYY-MM-DD
---

# Prep — Event Name

**Date:** YYYY-MM-DD | **Project:** [[pm/projects/project-name]]

## Context

What this meeting is about, pulled from [[pm/projects/project-name]] and recent [[pm/meetings/...]].

## Recent Changes Since Last Meeting

- What's changed — decisions, new info, completed tasks

## Open Questions to Raise

- Question with context

## Suggested Talking Points

1. Topic with supporting data from the Brain

## Live State

- Current Jira sprint status (from connector)
- Recent PRs/commits (from connector)
```
