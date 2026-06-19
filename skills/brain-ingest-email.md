# brain-ingest-email

Capture an important email or email thread into the second brain.

## Instructions

**Step 1 — Get the email content**

Ask the user to paste the email or thread. Accept any of:
- A single email (headers + body)
- A forwarded thread (multiple emails in sequence)
- A plain text dump from Outlook

If $ARGUMENTS contains a subject line or description, use it to prime the capture.

**Step 2 — Parse the email(s)**

Extract from the pasted content:
- Subject / thread topic
- Date(s)
- From / To / CC participants
- Key points from each message in the thread
- Any decisions, commitments, or action items mentioned
- Attachments referenced (note the names; you cannot read them unless also pasted)

**Step 3 — Format the capture**

```markdown
---
type: reading
date: <date of most recent email>
title: "Email: <subject>"
source_type: email
participants: "<from, to, cc>"
tags: [email]
---

## Thread Summary
<2-3 sentences: what this email exchange is about and the outcome>

## Participants
- **From:** <name / email>
- **To:** <names>
- **CC:** <names>
- **Date range:** <first email date> → <last email date>

## Key Points
- <point from the thread>

## Decisions & Commitments Made
- <decision or commitment> — by <name>

## Action Items
- [ ] <action> — Owner: <name> — Due: <date or TBD>

## Attachments Referenced
- <attachment name> (not captured)

## Full Thread
<paste the original email thread here>
```

Show the formatted capture. Ask: "Anything to adjust before saving?"

**Step 4 — Save**

Write to `<brain-root>/readings/YYYY-MM-DD-email-<slug>.md` using the Write tool.

Confirm the save and surface any action items.
