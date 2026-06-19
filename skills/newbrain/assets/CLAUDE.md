# The Brain — Schema & Operating Manual

This file is the Brain's self-awareness. Any LLM session — with zero prior memory — reads this file and immediately understands the full system: how to navigate, how to operate, what the rules are. The LLM changes; the schema stays.

## System Model

The Brain is a personal knowledge system organized as three specialized sub-brains, each owning a distinct domain. The user never writes Brain pages directly — the LLM writes and maintains everything. The user curates sources, directs analysis, asks questions, and thinks about what it all means.

### Sub-Brains

**`wiki/` — The Scholar.** General-purpose knowledge. Concepts, entities, source summaries, analysis. Long-term semantic memory — what you know about the world. Lookup-oriented, domain-agnostic. "What is X?", "How does Y work?", "What are the tradeoffs between A and B?"

**`pm/` — The Project Manager.** Business, product, and project knowledge. Active projects with decision logs, architecture, stakeholders, timelines. Meeting notes and summaries. Institutional memory — what's happening, what was decided, and why. Synthesizes meeting transcripts, notes, and live connector data into compiled project narratives. Does NOT store raw tickets or code — stores the understanding.

**`planner/` — The Executive Assistant.** Day-to-day operations organized in a date hierarchy (`planner/YYYY/MM/YYYY-MM-DD.md`). Each daily file serves as both a prospective plan (schedule, priorities, talking points) and a retrospective activity log (`/the-brain:log` appends throughout the day). Also holds the dashboard, weekly reflections, and task lists. Executive function — reads from the other two sub-brains and from connectors, produces actionable output.

### Layers

**Memory** — the three sub-brains above. Each maintains its own pages, indexes, and internal structure. Cross-references between sub-brains are where the real intelligence lives.

**Self-awareness** — this file (CLAUDE.md). The Brain's knowledge of itself.

**Agency** — skills shipped with the **the-brain plugin**, invoked as `/the-brain:<skill>`. Named workflows that orchestrate across sub-brains and connectors.

**Raw sources** (`raw/`) — immutable source dump. Articles, PDFs, images, notes, and connector-reference stubs for Outlook/Teams content. The LLM never modifies anything in `raw/`. Every derived page links back to its raw source or stub.

**Connectors** — live external systems. The Brain synthesizes and references connector data; it does not duplicate it.

### Available Connectors

- **Jira**: issues, projects, JQL search, transitions, Confluence, Compass
- **Outlook**: email search, calendar search, meeting availability
- **Teams**: chat message search
- **SharePoint**: document and folder search
- **Postman**: collections, specs, mocks

---

## How to Navigate the Brain

Follow this sequence. Navigate like a tree search — top-down, skipping irrelevant branches. Never scan exhaustively.

1. **Read this file** (CLAUDE.md) — you're doing this now.
2. **Orient**: read each sub-brain's `overview.md` to decide which brain(s) are relevant. Skip irrelevant brains entirely.
3. **Find specifics**: read the relevant brain's `index.md`. Read category/project rollup summaries first, identify the right branch, then drill into individual pages.
4. **For project questions**: go straight to `pm/index.md`, find the project's section (which groups the project page, all its meetings, and all its notes together).
5. **For current state**: read `log.md` (recent operations) and `planner/dashboard.md` (current priorities).
6. **To trace a claim to its source**: follow the inline `[[wikilink#heading]]` to the specific section, then follow `raw_source` frontmatter or `Source: [[raw/filename]]` to the raw file. Two clicks max from any claim to primary source.

---

## Conventions

### Linking

- **ALL internal links use Obsidian-style `[[wikilinks]]`.** Never markdown-style `[text](path)`. Non-negotiable.
- Link to another brain page: `[[page-name]]` or `[[page-name|Display Text]]`
- Link to a raw source: `[[raw/filename.md]]`
- Link across sub-brains: `[[pm/projects/project-alpha]]`, `[[wiki/concepts/distributed-consensus]]`
- Link to a specific section: `[[page-name#heading-text]]`

### Raw-First Rule

All external sources that the Brain derives knowledge from must be represented in `raw/` — either as a verbatim file (static sources) or a connector-reference stub (Outlook/Teams sources). Three explicit tiers govern how each type is handled.

---

#### Tier 1 — Static sources → saved verbatim to `raw/`

Articles, PDFs, images, voice memos, handwritten notes, SharePoint document exports, user-provided files. These are static after capture and belong in `raw/` as-is.

**Workflow**: external source → save to `raw/` as `YYYY-MM-DD-slug.ext` → create/update Brain pages that reference `[[raw/filename]]`. This ensures:
1. A complete archive of static sources the Brain has consumed
2. Every claim traces back to `raw/` (provenance chain is never broken)
3. External data doesn't disappear when links break
4. The Brain can be audited — `raw/` is the evidence for static content

---

#### Tier 2 — Outlook/Teams content → connector-reference stubs in `raw/`

**Outlook emails, Teams chats/channel messages, and Teams meeting transcripts are NEVER copied verbatim into `raw/`.** Rationale: the source systems own retention (90-day email deletion, 180-day Teams transcript retention); the Brain must not become a parallel archive that outlives them.

Instead, each such source gets a **connector-reference stub** in `raw/`, named `YYYY-MM-DD-slug.ref.md`:

```markdown
---
title: <subject> — Connector Reference
type: connector-reference
source_system: teams-transcript | outlook-email | teams-chat
date: YYYY-MM-DD
# plus system-specific retrieval keys, e.g.: meeting_subject, attendees, organizer,
# event/meeting ID, chat deep link, message ID, email search query, recording URL
---
# <subject> — Connector Reference

**This is a reference stub — content is NOT stored here, per data governance policy.**

**To retrieve:** <exact connector tool + ID/URI/search query to re-pull the content>
**Fallback:** <e.g. search Outlook calendar for "<subject>" on <date>; ask the user to paste>
**Retention note:** source content expires per the source system's retention policy; once expired, rely on the derived Brain pages below.

**Derived pages:** [[pm/meetings/...]]
```

- Provenance chain is **preserved**: project page claim → `[[pm/meetings/meeting#heading]]` → `[[raw/YYYY-MM-DD-slug.ref.md]]` → connector fetch.
- `raw_source:` frontmatter on derived pages points at the stub.
- Downstream synthesized pages (meeting pages, notes, decisions, limited quotes) are fully allowed and exempt from retention policy.
- **Paste rule**: if the user pastes a transcript or email body, process it in-context to build derived pages + a stub; the verbatim body is never written to disk.
- **Decline-verbatim-save rule**: if the user explicitly asks to save a verbatim Outlook/Teams copy, decline, explain the data governance policy, and offer the stub + a richer derived page instead.

When a skill or workflow encounters Outlook/Teams data (e.g., `/the-brain:prep` reads a relevant email), it saves a connector-reference stub to `raw/` and builds derived pages from the in-context content.

---

#### Tier 3 — Live systems → deep links / frontmatter / connector queries only

Jira tickets/epics, Confluence pages, ADO boards, dashboards, calendars. These are living documents — never saved to `raw/` at all. (Teams chats are Tier 2: read them live via the Teams connector — `read_resource` with a `teams:///` URI — or a deep link; save a `.ref.md` stub only when the Brain derives knowledge from a specific chat.)

- **Jira tickets/epics**: query via connector; reference via frontmatter fields like `jira_project`, `jira_epic`.
- **Confluence pages**: reference by URL or page ID; query via Atlassian connector.
- **Other live-state systems** (ADO boards, dashboards, calendars, etc.).

These are referenced in project pages via frontmatter, Live Context sections, and inline deep links. Any LLM session can query the connector directly for current content.

---

Quick-reference connector queries for live state (e.g., "what's the current sprint status?", "what are the open Jira tickets?") do not need to be saved.

### Claim-Level Provenance

Every factual claim in the Brain must be traceable to its primary source. This operates at the **fact level**, not the document level.

- Inline wikilinks sit **next to the fact**, not in a "Sources" section at the bottom:
  `The latency budget is 200ms ([[pm/meetings/2026-04-05-perf-review#latency-decision]]).`
- The chain is always: **Answer → wiki/pm page (specific heading) → raw source.** Two clicks max.
- When answering queries, cite with clickable `[[page#heading]]` links to the specific section where the knowledge originated.

### Heading Anchors Are Stable Identifiers

Headings that other pages link to via `[[page#heading]]` are **stable anchors**. They must not be renamed without updating all inbound references. Before changing any heading text:

1. Grep for `[[page-name#heading-text]]` across all sub-brains
2. Update every inbound reference in the same pass
3. The `/the-brain:lint` skill verifies no broken heading anchors remain

### Codebase References

Codebases are **primary sources** for an AI engineer. Every project with a code repository must include a **Codebase** section in its project page with:

1. **Repo path** — the local filesystem path (and/or GitHub URL) so any LLM session can navigate there
2. **Key entry-point files** — the specific files to read first for technical understanding. At minimum: the repo's `CLAUDE.md` (if it exists), `README.md`, and any architecture docs. Listed in `repo_docs` frontmatter AND in the Codebase section body.
3. **Reading guidance** — what each file gives you (e.g., "CLAUDE.md has full architecture, hard constraints, and module map")

This means a future LLM session — with zero prior memory — can read the project page, see the codebase path and key files, and immediately go read those files to get full technical context. The project page provides the *narrative* (why, decisions, stakeholders); the codebase docs provide the *technical ground truth* (how, constraints, APIs).

**Convention**: When answering technical questions about a project, always read the codebase's own documentation (CLAUDE.md, README, etc.) for current truth rather than relying solely on the Brain's project page. The project page may lag behind the code.

### Timezone Convention

<!-- CUSTOMIZE: Replace PRIMARY_TZ and SECONDARY_TZ with your timezone pair. -->
<!-- Example: CT/ET, PT/CT, ET/GMT, etc. Update the UTC offsets accordingly. -->

**All times are shown in the user's primary timezone first, followed by a secondary timezone in parentheses.** Outlook/Teams calendar events report times in UTC — always convert to the user's local timezone and show the secondary timezone alongside.

Format: `9:30 AM CT (10:30 AM ET)` *(adjust to your timezone pair)*

This applies to all Brain pages: daily plans, meeting pages, project Live Context sections, dashboards, and briefing output. Never show UTC-only times. Never let timezone misalignment create phantom meetings or incorrect schedules.

### Raw File Naming

Files in `raw/` follow the convention: `YYYY-MM-DD-descriptive-slug.ext`

- Slug = lowercase, hyphens for spaces, no special characters
- Example: `2026-04-10-api-review-meeting-transcript.md`
- The `/the-brain:ingest` skill auto-renames files to this convention when processing
- **Connector-reference stubs** (Tier 2 sources) use the suffix `.ref.md`: `YYYY-MM-DD-descriptive-slug.ref.md`
  - Example: `2026-04-10-api-review-meeting.ref.md`

### Page Conventions

All pages use YAML frontmatter. Minimum fields: `title`, `type`, `created`, `updated`, `tags`.

Pages derived from raw sources additionally have:
- `raw_source:` path to file in `raw/` — this may point to a verbatim raw file (Tier 1 static sources) OR a `.ref.md` connector-reference stub (Tier 2 Outlook/Teams sources)
- Inline wikilink near the top: `Source: [[raw/filename.ext]]` (or `Source: [[raw/YYYY-MM-DD-slug.ref.md]]` for stub-backed pages)

**Wiki page types:** `entity`, `concept`, `source`, `analysis`

**PM page types:** `project`, `meeting`, `note`, `prep`
- Projects add: `status` (active/paused/completed), `stakeholders`, `started`, `target_date`, `jira_project`, `repo`, `repo_docs` (list of key files to read)
- Meetings add: `date`, `attendees`, `projects` (linked), `action_items` (list with owner/status)
- Notes add: `date`, `projects` (if applicable), `context`

**Planner page types:** `daily`, `weekly`, `task`
- Daily files (`planner/YYYY/MM/YYYY-MM-DD.md`) serve dual duty: morning plan (schedule, priorities, prep notes) and activity log (`/the-brain:log` appends work entries throughout the day)

See `templates.md` for full page templates. Skills reference templates when creating pages.

### Index Conventions

Indexes are **hierarchical reasoning trees**, not flat catalogs. Three levels:

1. **Root summary** (2-3 sentences) — what this sub-brain currently contains. Updated on every ingest. An LLM reads this first to decide if the brain is even relevant.
2. **Category/cluster summaries** — one rollup per logical grouping. Wiki: by category. PM: **by project** (each project groups its page, meetings, and notes). Planner: by time period.
3. **Individual page entries** — nested under their category: `[[wikilink]]`, one-line summary, type, last updated.

Rules:
- When a page is created or deleted, update its index in the same operation
- When an ingest changes the scope of a category/project, update the rollup summary
- An LLM should be able to navigate: CLAUDE.md → overview.md → index.md → specific page, top-down

### Log Conventions

**`log.md`** is the Brain's **operational changelog** — it records operations that change the Brain itself (page creates, index updates, ingests, syncs, lints, refactors, schema changes). It does NOT record personal work activity (what the user worked on during the day). That goes in the daily file's Activity Log section via `/the-brain:log`.

**Rule of thumb**: if it changed a Brain page, it goes in `log.md`. If it's about what you did at work, it goes in `planner/YYYY/MM/YYYY-MM-DD.md` Activity Log.

Format: `## [YYYY-MM-DD] verb | Subject`

Verbs: `ingest`, `query`, `lint`, `reflect`, `prep`, `sync`, `system`

Greppable: `grep "^## \[" log.md | tail -10`

### Contradiction Handling

When new data contradicts an existing claim, the page gets a callout with both versions and sources:

```markdown
> [!conflict] Contradicts previous understanding
> Previously: latency budget was 200ms ([[pm/meetings/2026-04-05-perf-review#latency-decision]])
> Updated: latency budget revised to 150ms ([[pm/meetings/2026-04-10-perf-followup#revised-budget]])
```

Resolve conflicts when possible by marking one as superseded. Keep the callout until explicitly resolved.

### Archive Strategy

Files stay in place (wikilinks never break). Archival is metadata + index, not file moves.

- **Projects**: `status: completed` → section collapses to one line under "Archived" in `pm/index.md`
- **Daily files**: after weekly reflection is written, dailies (`planner/YYYY/MM/YYYY-MM-DD.md`) get `status: archived`, removed from active index
- **Tasks**: completed tasks are pruned from `tasks.md` by `/the-brain:reflect` → become accomplishments in daily/weekly logs
- **Meeting pages**: archive with their project

The `/the-brain:lint` skill flags archival candidates.

---

## Workflows

### Ingest (article/paper/general source)

1. Read source content
2. Discuss key takeaways with user
3. Auto-rename raw file to `YYYY-MM-DD-slug.ext` if needed
4. Create source summary page in `wiki/sources/` with `Source: [[raw/filename]]` and granular headings per key finding
5. Create or update relevant entity/concept pages with claim-level `[[source#heading]]` links
6. Update `wiki/index.md` (add entries, update rollup summaries)
7. Update `wiki/overview.md` if the ingest shifts the big picture
8. Append to `log.md`

(For Outlook emails encountered during `/the-brain:prep` or similar: save a `.ref.md` connector-reference stub, derive insight directly into the prep doc — do not save verbatim email body.)

### Ingest (meeting transcript / handwritten notes)

For **Teams meeting transcripts**: the transcript is fetched via connector and processed **in-context** — the verbatim body is never written to disk. A `.ref.md` connector-reference stub is saved to `raw/` with retrieval keys so the transcript can be re-fetched. For **handwritten notes or images**: static content, treat as Tier 1 (save verbatim to `raw/`).

1. Read input (if image, describe; if transcript, parse speakers from connector or pasted text)
2. For Teams transcripts: save a `YYYY-MM-DD-slug.ref.md` stub to `raw/` with retrieval keys. For handwritten notes: auto-rename and save the verbatim file to `raw/`.
3. Route by content type:
   - Meeting → `pm/meetings/` page with granular headings per decision/topic
   - Project notes → `pm/notes/`
   - General knowledge → `wiki/sources/`
4. Update corresponding `pm/projects/` pages — decisions flow upward with `[[meeting#heading]]` links
5. Create/update entity pages in `wiki/entities/` for people mentioned — **back-link the meeting**: add the new meeting to each attendee's Meetings section so entity → meeting navigation works bidirectionally
6. Extract action items → `planner/tasks.md` with `[[wikilinks]]` back to source
7. Update relevant indexes
8. Append to `log.md`

### Query (top-down reasoning)

1. Read `overview.md` for each sub-brain → decide which are relevant
2. Read relevant brain's `index.md` → identify the right branch
3. Drill into individual pages within that branch
4. For project questions, optionally query connectors for live state
5. Synthesize answer with claim-level `[[page#heading]]` citations
6. Offer to file substantive answers as new pages

### Lint

Scan all three sub-brains for: orphan pages, missing index entries, concepts mentioned but lacking a page, stale project pages, overdue action items, weak cross-references, broken `[[#heading]]` anchors, archival candidates. Also scan `raw/` for governance violations — verbatim Outlook email bodies, Teams chat exports, or Teams transcript files (i.e., non-stub files whose content appears to be raw message/transcript data) — and flag them for the user to delete or have summarized and replaced with a `.ref.md` stub + richer derived pages. Report issues, auto-fix simple ones (missing index entries), create tasks for the rest.

### Sync

For each active project in `pm/projects/`: query connectors → compare with project page state → flag drift → update project pages → append to log.

### Reflect

Review recent activity → generate daily or weekly reflection in `planner/` → prune completed tasks from `tasks.md` into the reflection → promote genuine insights into Scholar or PM brains as permanent knowledge.

### Plot (week planning)

Gather context from Brain (project pages, meeting pages, action items, tasks, goals, entity pages) and connectors (full week calendar, Jira, Teams, email). Synthesize a week-level picture: map meetings to projects, distribute tasks across days by deadline and meeting-free time, flag cross-day dependencies. Generate or update `planner/YYYY/MM/YYYY-MM-DD.md` for each day Mon–Fri. Update planner index and dashboard.

### Prep (meeting briefing)

Before a meeting: gather project state, recent meeting history, entity context for attendees, and live connector data (Jira sprint, recent emails, Teams messages). Produce a prep doc in `pm/prep/` with context, recent changes, open questions, talking points, and live state. Any relevant emails read during prep are referenced via connector (not saved verbatim); save a `.ref.md` stub if the email is important enough to anchor a project decision.

### Log (activity tracking)

Run `/the-brain:log` from any Claude Code session. Read the user's description and the current conversation context. Synthesize a concise activity log entry. Append to today's daily file (`planner/YYYY/MM/YYYY-MM-DD.md`) Activity Log section. Update `planner/tasks.md` if work completed or created tasks.

### Met (meeting transcript acquisition)

User provides a brief description of a meeting → search Outlook calendar → get full event details → fetch transcript via Teams connector (fallback: ask user to paste) → process transcript **in-context** to build derived pages → save a `.ref.md` connector-reference stub to `raw/` with retrieval keys (never the verbatim transcript body) → invoke `/the-brain:ingest` for full processing (meeting page, project updates, entity back-links, action items). The provenance chain is always: project page decision → `[[pm/meetings/meeting#heading]]` → `[[raw/YYYY-MM-DD-slug.ref.md]]` stub → connector fetch.

### Daily Orchestration (/the-brain:myday)

The `/the-brain:myday` skill orchestrates the daily workflow with day-of-week branching:

| Day | Order |
|-----|-------|
| Monday | `/the-brain:sync` → `/the-brain:lint` → `/the-brain:plot` → generate daily plan |
| Tue–Thu | `/the-brain:sync` → generate daily plan |
| Friday | `/the-brain:sync` → generate daily plan → `/the-brain:reflect` |

Every day: sync runs first (connector freshness), then the daily plan is generated by synthesizing Brain knowledge + live connector data. Monday adds a health check and full week plot. Friday closes the week with a reflection.

---

## Skill Catalog

### Plugin Skills (`the-brain` plugin)

All skills ship with the **the-brain plugin** and are invoked as `/the-brain:<skill>`. The four anywhere-skills (myday, standup, prep, log) work from any directory via the plugin's `brain_path` setting — they do not require the Brain to be the current working directory. `brain_path` applies to Claude Code only: Claude Cowork sessions are already rooted in the Brain folder, so Cowork users do not need (and cannot set) this setting.

| Skill | Description |
|-------|-------------|
| `/the-brain:newbrain` | Bootstrap a new Brain in a target folder. Creates directory structure, index files, overviews, CLAUDE.md, and templates. |
| `/the-brain:ingest` | Process a raw source into the Brain. Auto-detects type (static file vs. Outlook/Teams → stub), routes to correct sub-brain(s). |
| `/the-brain:ask` | Query the Brain's knowledge with cited, claim-level sources. |
| `/the-brain:project` | View or create a project in the PM brain with live connector data. |
| `/the-brain:sync` | Sync PM brain against live connectors. Flag drift, update pages. |
| `/the-brain:lint` | Health-check the entire Brain. Find orphans, stale content, broken links, and raw/ governance violations. |
| `/the-brain:reflect` | Generate daily/weekly reflection. Prune tasks, promote insights. |
| `/the-brain:plot` | Plot the work week. Generate Mon–Fri daily planner files from Brain knowledge + live connectors. |
| `/the-brain:met` | Meeting transcript acquisition. Find meeting in Outlook/Teams, fetch transcript in-context, save .ref.md stub to raw/, invoke /the-brain:ingest. |
| `/the-brain:compose` | Compose a message (email, Teams, Slack, etc.) grounded in Brain context. Always drafts first — never sends without approval. |
| `/the-brain:ticket` | Create or update a Jira ticket from Brain context. Pulls project decisions, meeting outcomes, action items. Always drafts first — never creates without approval. |
| `/the-brain:myday` | Morning briefing: schedule, priorities, context. Works anywhere, richer inside the Brain. |
| `/the-brain:standup` | Standup summary: yesterday, today, blockers. Formatted for Slack or reading aloud. |
| `/the-brain:prep` | Meeting prep briefing: project state, recent changes, talking points. |
| `/the-brain:log` | Activity log: update today's daily file with what you worked on. Reads conversation context. |

---

## Principles

1. **An LLM with zero memory can operate this Brain.** CLAUDE.md → overviews → indexes → pages. Top-down, never exhaustive.
2. **Every index must always be current.** Create/delete a page → update its index in the same pass.
3. **Every operation that changes a sub-brain must append to log.md.** No exceptions.
4. **Every claim links to its source at the fact level.** `[[page#heading]]`, not just `[[page]]`.
5. **Headings are stable anchors.** Never rename without updating all inbound references.
6. **Decisions flow upward.** Meeting decisions propagate to project pages. You never dig through meetings.
7. **The Brain synthesizes; connectors provide live data.** Don't duplicate Jira or Git.
8. **Cross-reference aggressively across sub-brains.** The connections are where the intelligence lives.
9. **Ask before making big changes.** If an ingest would significantly revise an existing page, show the diff first.
10. **The schema is a living document.** If a new convention works, add it here.
11. **Corrections update the Brain immediately.** When the user corrects a fact mid-conversation, update all affected pages (project, wiki, overview, index) in the same response before continuing. Never carry a known-wrong fact forward.
12. **The Brain is the only memory system.** Do not use Claude Code's external memory (`~/.claude/projects/.../memory/`) for anything related to this project. All knowledge, feedback, conventions, and learned preferences belong inside the Brain itself — in CLAUDE.md (schema/conventions), wiki pages (knowledge), pm pages (project context), or planner pages (operational). The Brain must be fully self-contained.
13. **Sync is read-only; external systems are the source of truth.** When syncing (calendar, Jira, Confluence, etc.), the Brain only *reads* from connectors — it never writes back. If the Brain's state conflicts with a connector, the connector wins. Update the Brain page to match, not the other way around.
14. **Confluence and other living docs are referenced externally, not ingested to raw/.** Like Jira, Confluence pages are living documents that change. Reference them by URL or Confluence page ID in Brain pages (e.g., in a References section or frontmatter). Do not save them to `raw/`. The Brain can query Confluence via the Atlassian connector for current content at any time.

### External Reference Conventions

Three tiers govern how external content is handled — see the Raw-First Rule section for full detail.

**Tier 1 (save verbatim to `raw/`)**: Articles, PDFs, images, voice memos, handwritten notes, SharePoint document exports, user-provided files.

**Tier 2 (`.ref.md` connector-reference stub in `raw/`)**: Outlook emails, Teams chats/channel messages, Teams meeting transcripts. Content is never stored verbatim; a stub with retrieval keys is saved instead.

**Tier 3 (deep links / frontmatter / connector queries only — nothing in `raw/`)**:

- **Jira**: Reference via frontmatter (`jira_project`, `jira_epic`) and Live Context sections. Query via connector.
- **Confluence**: Reference via URL or page ID in a References section. Query via Atlassian connector (`getConfluencePage`).
  <!-- CUSTOMIZE: Add your key Confluence spaces here, e.g. Key spaces: `ENG` (Engineering), `PROD` (Product). -->
- **ADO / Azure DevOps**: Reference via project name. Query via relevant connector or stakeholder.
- **PowerBI / Dashboards**: Reference by dashboard name/URL.
