# brain-capture-meeting

Capture structured meeting notes into the second brain.

## Instructions

**Step 1 — Gather context**

Ask the user for:
- Meeting title or topic (or use $ARGUMENTS if provided)
- Date (default: today's date)
- Participants
- Raw notes or transcript to paste in

**Step 2 — Structure the notes**

From the raw input, extract and format this document:

```markdown
---
type: meeting
date: <YYYY-MM-DD>
title: "<title>"
participants: "<comma-separated names>"
tags: []
---

## Summary
<2-3 sentences: what was discussed and decided>

## Key Discussion Points
- <point>

## Decisions Made
- <decision> — Owner: <name>

## Action Items
- [ ] <action> — Owner: <name> — Due: <date or TBD>

## Open Questions
- <unresolved question>

## Raw Notes
<original notes unchanged>
```

Show the formatted note. Ask: "Does this look right, or anything to change?"

**Step 3 — Save**

Determine the brain root:
- Check if environment variable `BRAIN_PATH` is set; if so, use that path
- Otherwise default to `~/brain`

Write the file to `<brain-root>/meetings/YYYY-MM-DD-<slug>.md` where slug is the title lowercased with spaces replaced by hyphens.

Use the Write tool to create the file with the formatted content above.

Confirm the path saved and list any action items extracted so the user can follow up on them.
