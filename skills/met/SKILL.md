---
name: met
description: Meeting transcript acquisition. Finds a meeting in Outlook/Teams by description, pulls the transcript via connector, processes it in-context, saves a connector-reference stub to raw/, and invokes /the-brain:ingest processing. Use after any meeting you want captured.
argument-hint: <brief meeting description — name, person, date, any identifying detail>
---

# /the-brain:met — Meeting Transcript Acquisition + Ingest

Given a brief description of a meeting (e.g., "design review call last Thursday", "my 1:1 with Alex today", "the standup from yesterday"), locate it in Outlook/Teams, fetch the transcript into context, create a connector-reference stub in `raw/`, and invoke `/the-brain:ingest` to process it into the Brain.

This skill is the **acquisition layer** — it handles finding and fetching. The transcript stays **in-context only** and feeds ingest processing; it is never written to disk. A lightweight connector-reference stub (not the transcript body) is what lands in `raw/`.

**Data governance**: Nelnet policy prohibits storing verbatim Teams transcripts, Outlook emails, or Teams chat content in `raw/` or any other Brain file. The stub is the archival record; the synthesized meeting page is the permanent knowledge artifact.

## Step 1: Parse the user's description

Extract search clues from the argument:
- **Who**: person names, team names → will become calendar attendee/query filters
- **What**: meeting subject keywords → calendar query string
- **When**: natural language dates ("last Thursday", "today", "yesterday", "April 9") → date range for calendar search. Default to the last 2 weeks if no date given.

## Step 2: Find the meeting in Outlook

Use `outlook_calendar_search` with the extracted keywords and date range:
- Search by subject keywords and/or attendee email
- Limit to a reasonable range (default: last 14 days)

**If multiple matches**: present the top candidates to the user with subject, date, time, and attendees. Ask which one.

**If no matches**: broaden the search (wider date range, different keywords). If still nothing, ask the user for more details.

**If one clear match**: confirm with the user: "Found: [Subject] on [Date] with [Attendees]. Is this the one?"

From the match, extract:
- Meeting subject, date, time, duration
- Full attendee list (names and emails)
- Organizer name and email
- Calendar event URI (`calendar:///events/{eventId}`)
- Whether it's a Teams meeting (location field)

## Step 3: Get full meeting details

Use `read_resource` with the calendar event URI to get the complete event record:
- Full attendee list with emails and response status
- Teams meeting join URL
- Online meeting ID
- Recording URL (SharePoint link, if meeting was recorded)
- Transcript URL / meeting-transcript URI (if available in the event data)
- Any meeting body/description text

Note the meeting ID and any transcript/recording URIs — these are needed for the stub and transcript retrieval.

## Step 4: Check if already ingested

Before fetching the transcript, check if this meeting has already been ingested:
- Search `raw/` for files matching the meeting date and subject slug — look for both old-style transcript files (`YYYY-MM-DD-...-transcript.md`) and connector-reference stubs (`YYYY-MM-DD-....ref.md`)
- Search `pm/meetings/` for an existing meeting page covering this date and attendees
- If found: tell the user "This meeting was already ingested — see [[pm/meetings/existing-page]]." Offer to re-ingest if they want (e.g., transcript was updated, or they want a fresh synthesis).

## Step 5: Extract the transcript (into context only)

**Primary path — MCP connector:**
- Use `read_resource` with `meeting-transcript:///{meetingId}` URI (meeting ID from Step 3), or use `GetOnlineMeetingTranscripts` if available
- If this returns transcript text, hold it in context — **do not write it to any file**. Proceed to Step 6.

**Fallback path — if primary fails** (meeting wasn't recorded, no transcript available, permissions issue, connector error):
- Tell the user clearly what happened: "Transcript not available via connector — [reason]."
- Offer alternatives:
  1. "Open the meeting in Teams → Recap tab → click the transcript → copy all text and paste it here"
  2. "If you have an exported transcript file, give me the file path"
  3. "If there's no transcript, I can create a meeting stub page from the calendar metadata alone (attendees, subject, date) — you can fill in notes manually"
- Wait for the user to provide content before proceeding
- **If the user pastes the transcript**: process it in-context just as you would a connector-fetched transcript. Note in the stub (Step 6) that content was user-provided. **Do not write the pasted body to any file.**

## Step 6: Create connector-reference stub in raw/

Create a stub file — **not the transcript** — in `raw/` following Brain naming convention:
- **Filename**: `YYYY-MM-DD-meeting-slug.ref.md` where date = meeting date, slug = lowercase-hyphenated meeting subject

```markdown
---
title: <Meeting Subject> — Connector Reference
type: connector-reference
source_system: teams-transcript
date: YYYY-MM-DD
meeting_subject: <full subject from calendar>
attendees: [<Name (email)>, ...]
organizer: <Name (email)>
event_id: <calendar event ID>
online_meeting_id: <Teams online meeting ID>
recording_url: <SharePoint recording URL, or "none">
---
# <Meeting Subject> — Connector Reference

**This is a reference stub — transcript content is NOT stored here, per data governance policy.**

**To retrieve:** Use `read_resource` with `meeting-transcript:///{online_meeting_id}` or `GetOnlineMeetingTranscripts` with meeting ID `<online_meeting_id>`. Alternatively, search Outlook calendar for "<meeting_subject>" on <date> to get the full event record, then fetch the transcript URI.
**Fallback:** Search Outlook calendar for "<meeting_subject>" on <date>; or ask the user to open the Teams Recap tab and paste the transcript text.
**Retention note:** Transcript content expires per Teams' retention policy; once expired, rely on the derived Brain pages below for meeting knowledge.

**Derived pages:** [[pm/meetings/YYYY-MM-DD-slug]]
```

If the transcript was provided by user paste (fallback path), note it: add a line `**Content source:** Transcript was provided by user paste; re-pull via connector if needed.`

**Do not write the transcript body to raw/ or any other file.** The stub is the only artifact written to disk.

## Step 7: Invoke /the-brain:ingest

Hand off to the `/the-brain:ingest` skill. The stub file is already created and correctly named (Steps 1-2 of `/the-brain:ingest` can be skipped). The transcript text is in context.

**Context to pass**: The stub is at `raw/YYYY-MM-DD-slug.ref.md`. The source type is a meeting transcript. The attendee list and meeting metadata are in the stub. The transcript content is in context — start at `/the-brain:ingest` Step 3 (discuss with user) and proceed with processing using the in-context transcript.

The `/the-brain:ingest` skill handles all downstream processing:
- Creates `pm/meetings/YYYY-MM-DD-slug.md` with decisions, topics, action items
- Updates relevant `pm/projects/` pages (decisions flow upward)
- Creates/updates `wiki/entities/` for attendees (with Meetings back-links)
- Extracts action items → `planner/tasks.md`
- Updates all indexes (`pm/index.md`, `wiki/index.md`)
- Appends to `log.md`

**Provenance chain**: project page decision → `[[pm/meetings/meeting#heading]]` → `[[raw/YYYY-MM-DD-slug.ref.md]]` → connector fetch. The meeting page itself must be a **faithful, sufficiently detailed synthesis** since it may outlive the source transcript once it expires.

## Step 8: Add meeting-specific metadata

After `/the-brain:ingest` completes, add metadata that `/the-brain:ingest` doesn't handle:
- Add the **Teams recording URL** to the meeting page (as `teams_vod:` in frontmatter and as an inline link) if a recording exists
- Add the **Teams meeting join URL** for reference
- Verify the meeting page's `attendees:` frontmatter matches the full calendar attendee list (ingest may have used only the transcript's speaker list, which can miss non-speaking attendees)

## Step 9: Confirm

Output a summary to the user:
- Meeting identified: [subject, date, attendees]
- Connector-reference stub created: `[[raw/YYYY-MM-DD-slug.ref.md]]`
- Brain pages created/updated: list with `[[wikilinks]]`
- Action items extracted: count and list
- Recording link: [URL if available]

## Edge Cases

**Meeting with no transcript and no recording:**
- Create a connector-reference stub from calendar metadata alone (no transcript URI to record — note this in the stub's "To retrieve" field)
- Create a meeting stub page from calendar metadata (date, subject, attendees, duration)
- Mark it with `> [!note] No transcript available — this page was created from calendar metadata only. Add notes manually.`
- Still update entity pages with the meeting reference and extract any known action items from the user's description

**Recurring meetings (e.g., weekly standup):**
- Each occurrence gets its own stub in `raw/` and its own meeting page: `pm/meetings/YYYY-MM-DD-meeting-slug.md`
- The project page's Live Context section should reference the recurring series, not individual occurrences

**Meeting already partially ingested (e.g., notes ingested but not transcript):**
- Check what already exists in `pm/meetings/` and `raw/`
- If a meeting page exists from notes, enrich it with transcript content rather than creating a duplicate
- Add the connector-reference stub as an additional raw source: `raw_transcript:` in frontmatter alongside existing `raw_source:`, pointing to the new `.ref.md` stub

**User asks to save the verbatim transcript to raw/:**
- Decline. Explain that Nelnet data governance policy prohibits storing verbatim Teams transcripts in the Brain.
- Offer instead: a connector-reference stub (already done) plus a richer, more detailed meeting page synthesized from the in-context transcript.
