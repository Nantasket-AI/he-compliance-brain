# brain-capture-person

Add or update a note on a person — colleague, regulator, vendor, board member, or key contact.

## Instructions

**Step 1 — Identify the person**

Ask (or infer from $ARGUMENTS): full name, role / title / org, and why you're capturing this now.

**Step 2 — Check for an existing note**

Use the Glob tool to search `<brain-root>/people/` for a file matching the person's name. If found, read it and ask: "I found an existing note for this person — should I update it or keep a separate entry?"

**Step 3 — Gather details**

Collect what's available (skip what's unknown):
- Contact info (email, phone, LinkedIn)
- Relationship to the user
- Key background (expertise, priorities, communication style)
- History of interactions
- Things to remember (preferences, commitments made, sensitivities)
- Open items or next steps

**Step 4 — Format the note**

```markdown
---
type: person
date: <YYYY-MM-DD>
title: "<person name>"
organization: "<org>"
role: "<role>"
tags: []
---

## Person
- **Name:** <name>
- **Title / Role:** <title>
- **Organization:** <org>
- **Contact:** <email / phone / LinkedIn>

## Relationship
<How do you know them and in what capacity?>

## Background
<Expertise, priorities, what they care about>

## Interaction Log
| Date | Context | Key Outcome |
|---|---|---|
| <date> | <context> | <outcome> |

## Things to Remember
- <preference, commitment, sensitivity>

## Open Items
- [ ] <follow-up or outstanding item>
```

Show the note. Ask: "Anything missing or to adjust?"

**Step 5 — Save**

Write to `<brain-root>/people/<person-name-slug>.md`. For people notes, omit the date prefix in the filename — use just the name slug so updates stay in one file.

If updating an existing note, use the Edit tool to merge new interaction log rows and open items into the existing file rather than overwriting.

Confirm the save.
