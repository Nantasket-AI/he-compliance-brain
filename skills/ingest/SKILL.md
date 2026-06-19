---
name: ingest
description: Process a raw source into the Brain. Handles articles, meeting transcripts, handwritten notes, images, PDFs, and data files. Auto-detects type and routes to the right sub-brain(s). Use when adding any new source material.
argument-hint: <filename or path in raw/>
allowed-tools: Read Write Edit Bash(mv *) Bash(cp *) Bash(ls *)
---

# /the-brain:ingest — Source Intake

You are processing a new source into the Brain. Follow the workflow in CLAUDE.md precisely.

## Connector-Reference Stub Template

Used for Outlook emails, Teams chats/channel messages, and Teams meeting transcripts (see routing logic below). Save as `raw/YYYY-MM-DD-slug.ref.md`:

```markdown
---
title: <Subject / Thread Title> — Connector Reference
type: connector-reference
source_system: teams-transcript | outlook-email | teams-chat
date: YYYY-MM-DD
# teams-transcript additional fields:
meeting_subject: <subject>
attendees: [<Name (email)>, ...]
organizer: <Name (email)>
event_id: <calendar event ID>
online_meeting_id: <Teams online meeting ID>
recording_url: <URL or "none">
# outlook-email additional fields:
email_subject: <subject>
from: <sender>
to: [<recipients>]
email_search_query: <Outlook search query to re-find this email>
# teams-chat additional fields:
chat_type: chat | channel
chat_deep_link: <Teams deep link URL>
channel: <channel name, if applicable>
---
# <Subject> — Connector Reference

**This is a reference stub — content is NOT stored here, per data governance policy.**

**To retrieve:** <exact connector tool + ID/URI/search query to re-pull the content>
**Fallback:** <e.g. search Outlook for "<subject>" on <date>; ask the user to paste>
**Retention note:** Source content expires per the source system's retention policy; once expired, rely on the derived Brain pages below.

**Derived pages:** [[pm/meetings/...]] or [[pm/notes/...]] or [[wiki/sources/...]]
```

## Step 1: Locate and read the source

**Raw-first rule**: every external source must land in `raw/` (or have a stub there) before the Brain can reference it.

**If the source is an Outlook email, Teams chat/channel message, or Teams meeting transcript** (whether via connector fetch, an exported file on disk, or pasted text):
1. Fetch or read the content **into context only** — do not write the verbatim body to any file.
2. Create a `YYYY-MM-DD-slug.ref.md` connector-reference stub in `raw/` using the template above, populated with all available retrieval metadata (IDs, URIs, search queries, deep links).
3. Proceed with all downstream processing (Steps 3–8) using the in-context content.
4. **Never write the verbatim body to raw/.** If given an exported file on disk containing an email or transcript, process it from the file, create the stub, and recommend the user delete the export file.
5. **If the user explicitly asks to save the verbatim body to raw/**: decline. Explain that Nelnet data governance policy prohibits storing verbatim emails, Teams chats, or Teams transcripts in the Brain. Offer a connector-reference stub (already created) plus richer derived pages as the alternative.

**If an argument is a file already in `raw/`** — read it directly.

**If an argument is a file elsewhere on disk** (and it is not an Outlook email or Teams export) — read it, then copy it to `raw/`.

**If an argument is a URL, Teams meeting link, or external reference**:
- For Teams transcripts or Outlook emails: fetch via connector into context; create a stub (see Outlook/Teams branch above).
- For all other URLs/references: fetch the content, export as markdown to `raw/`, then read from `raw/`.

**If an argument is pasted content with no file**:
- If it is an email, Teams chat, or transcript: process in-context; create a stub; do not save the pasted body.
- For all other pasted content: save it to `raw/` as a new markdown file first.

**If no argument** — ask what source to ingest.

Read the source content (from file or in-context). For images, describe what you see. For PDFs, extract text.

**Connector exports**: SharePoint documents and other static non-Outlook/Teams sources should be exported in full to `raw/` as markdown, with a metadata header at the top (source URL, date, author, etc.) so the raw file is self-documenting. Outlook emails and Teams transcripts/chats get stubs only (see above). Jira tickets and Confluence pages are never saved to `raw/` — query them via connector and reference by ID/URL.

## Step 2: Auto-rename to convention

If the file doesn't follow the `YYYY-MM-DD-descriptive-slug.ext` (or `.ref.md`) convention:
- Determine an appropriate slug from the content (lowercase, hyphens, no special chars)
- Use today's date if the source date is unclear
- Rename the file in `raw/`: `mv raw/old-name.ext raw/YYYY-MM-DD-slug.ext`
- All subsequent references use the new filename

## Step 3: Discuss with user

Present key takeaways from the source. Ask if there's anything specific to emphasize or de-emphasize before filing. Wait for user input before proceeding.

## Step 4: Detect source type and route

Determine what the source contains and route accordingly:

**Article / paper / report / general knowledge:**
1. Create source summary in `wiki/sources/` using the Source Summary template from `templates.md`
2. Use **granular headings** for each key finding — these are stable anchors other pages will link to
3. Create or update entity pages in `wiki/entities/` for significant people/orgs/tools mentioned
4. Create or update concept pages in `wiki/concepts/` for significant ideas/frameworks
5. On entity/concept pages, link claims back to the source using `[[wiki/sources/source-name#heading]]`

**Meeting transcript:**

The meeting page is a **synthesis** — the transcript (fetched via connector or provided in-context) is the **primary source**. Every factual claim in the meeting page must trace back to the in-context transcript content. Because the transcript may expire from the source system, the meeting page must be a **faithful, sufficiently detailed synthesis** — it may be the only durable record of what was decided and discussed.

The provenance chain is always: **project page decision → `[[pm/meetings/meeting#heading]]` → `[[raw/YYYY-MM-DD-slug.ref.md]]` → connector fetch**. Two clicks max from any claim to the re-fetch pointer.

1. Create meeting page in `pm/meetings/` using the Meeting template from `templates.md`
   - Frontmatter MUST include `raw_source:` pointing to the connector-reference stub (e.g., `raw/YYYY-MM-DD-slug.ref.md`). If both notes and a transcript stub exist, include `raw_transcript:` pointing to the stub as well.
   - Near the top of the page, add `Source: [[raw/YYYY-MM-DD-slug.ref.md]]` (and `Notes: [[raw/notes-filename]]` if applicable)
   - If a recording URL exists (SharePoint VOD), add `teams_vod:` in frontmatter and an inline link
2. Use **granular headings per decision and per topic** — these are stable anchors project pages will link to. Each Topic Discussed subsection should cite the stub inline: include `([[raw/YYYY-MM-DD-slug.ref.md]])` after key factual claims so a reader can trace any statement to the re-fetch pointer (and from there, re-pull the original transcript via connector).
3. Update the relevant project page(s) in `pm/projects/`:
   - Add decisions to the Decision Log with `[[pm/meetings/meeting-name#decision-heading]]` links
   - Update status, open questions, risks as needed
   - The project page cites the meeting page heading, which cites the stub — the full chain stays intact
4. Create/update entity pages in `wiki/entities/` for attendees if they don't exist
5. **Back-link entities**: For each attendee's entity page, add the new meeting to their **Meetings** section (create the section if it doesn't exist). Format: `- [[pm/meetings/meeting-name]] — brief context (date). Key contribution or role in this meeting.` This ensures bidirectional navigation: meeting → entity AND entity → meeting.
6. Extract action items → add to `planner/tasks.md` with `[[pm/meetings/meeting-name]]` links

**When invoked by `/the-brain:met`**: The connector-reference stub is already saved to `raw/` with correct naming and metadata. The transcript text is in context. Skip Steps 1-2 (locate source, auto-rename) and start at Step 3 (discuss with user).

**Handwritten notes / voice memo / quick capture:**
1. Create note page in `pm/notes/` using the Note template from `templates.md`
2. If project-related, update the relevant project page(s)
3. Extract any tasks → `planner/tasks.md`
4. If contains general knowledge insights, also create/update `wiki/` pages

**For ALL types:**
- Every generated page MUST have `raw_source:` in frontmatter AND `Source: [[raw/filename]]` inline — stub paths (`raw/YYYY-MM-DD-slug.ref.md`) are valid `raw_source` targets
- Every factual claim MUST link to its source at the heading level: `[[page#heading]]`
- Cross-reference aggressively across sub-brains

## Step 5: Update indexes

For each sub-brain that was touched:
1. Read the current `index.md`
2. Add new page entries under the correct category
3. Update category rollup summaries if the scope changed
4. If this is a project-related ingest, ensure the project section in `pm/index.md` groups the new page with the project

## Step 6: Update overview (if significant)

If this ingest meaningfully shifts what the Brain knows, update the relevant `overview.md` file(s).

## Step 7: Log

Append to `log.md`:
```
## [YYYY-MM-DD] ingest | Source Title
Summary of what was created/updated. Pages touched: [list].
```

## Step 8: Report

Print a summary of all pages created or updated across all sub-brains, with `[[wikilinks]]` to each.
