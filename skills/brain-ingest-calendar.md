# brain-ingest-calendar

Capture context and prep notes from a calendar event or meeting invite.

## Instructions

**Step 1 — Get the event details**

Ask the user to paste the calendar invite or event details. Accept:
- An Outlook meeting invite (copy-pasted)
- A manually described meeting ("Tomorrow at 2pm with the audit committee about Q3 controls")
- An agenda document

If $ARGUMENTS contains a description, use it as a starting point.

**Step 2 — Parse the event**

Extract:
- Meeting title / subject
- Date, time, duration
- Organizer and attendees
- Location or video link
- Agenda or description
- Any attached files mentioned

**Step 3 — Build a pre-meeting brief**

```markdown
---
type: meeting
date: <event date>
title: "<meeting title>"
participants: "<organizer and attendees>"
tags: [calendar, upcoming]
---

## Meeting Brief
- **Title:** <title>
- **Date / Time:** <date> at <time> (<duration>)
- **Organizer:** <name>
- **Attendees:** <names / roles>
- **Location / Link:** <location or video URL>

## Agenda
<parsed or reconstructed agenda>

## Background
<What is this meeting about? What's the context?>

## What I Need to Know Going In
<Key facts, history, or context the user should have>

## My Goals for This Meeting
<What do I want to achieve or decide?>

## Questions to Ask
- <question>

## Materials to Prepare
- [ ] <prep item>

## Notes
<space for live notes during the meeting — leave blank>

## Action Items
<space to fill in after the meeting>
```

Show the brief. Ask: "Anything to add — goals, questions, prep items?"

**Step 4 — Save**

Write to `<brain-root>/meetings/YYYY-MM-DD-<slug>.md` using the Write tool.

After the meeting, the user can run `/brain-capture-meeting` to fill in outcomes and action items, referencing this file.
