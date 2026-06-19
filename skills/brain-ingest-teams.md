# brain-ingest-teams

Capture a Microsoft Teams conversation, chat, or meeting transcript into the second brain.

## Instructions

**Step 1 — Get the content**

Ask the user what they have:
1. A Teams channel conversation (copy-pasted from Teams)
2. A Teams chat (1:1 or group DM)
3. A meeting transcript (from Teams recording)
4. A meeting recap / summary (from Teams Copilot)

Ask them to paste the content. If $ARGUMENTS contains a description, use it as the title.

**Step 2 — Determine the capture type**

| Source | Route to |
|---|---|
| Meeting transcript or recap | Treat as meeting notes → follow `brain-capture-meeting` format |
| Channel conversation | Treat as a discussion thread → use reading format below |
| 1:1 or group DM | Treat as a conversation note |

**Step 3 — Format a channel/chat conversation**

```markdown
---
type: reading
date: <date of conversation>
title: "Teams: <channel or chat name> — <topic>"
source_type: teams
participants: "<comma-separated participant names>"
tags: [teams]
---

## Conversation Summary
<What was discussed? What was the outcome or conclusion?>

## Channel / Chat
- **Location:** <Teams channel name or "DM between X and Y">
- **Date range:** <start> → <end>
- **Participants:** <names>

## Key Points
- <point>

## Decisions & Action Items
- [ ] <action> — Owner: <name> — Due: <date or TBD>

## Links & Files Shared
- <link or file name mentioned>

## Full Conversation
<pasted Teams content>
```

**For meeting transcripts**, extract:
- Speaker-by-speaker key contributions
- Decisions made
- Action items
- Then save in the meetings format (see `brain-capture-meeting`)

Show the formatted note. Ask: "Anything to adjust?"

**Step 4 — Save**

Write to `<brain-root>/meetings/YYYY-MM-DD-teams-<slug>.md` for meeting transcripts, or `<brain-root>/readings/YYYY-MM-DD-teams-<slug>.md` for conversations, using the Write tool.

Confirm the save and surface action items.
