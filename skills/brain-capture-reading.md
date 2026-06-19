# brain-capture-reading

Capture reading notes, highlights, and takeaways from any source.

## Instructions

**Step 1 — Gather source info**

Ask (or infer from $ARGUMENTS):
- Source title and author / publication
- Source type: article / regulation / report / book / email / other
- URL or document reference (optional)
- Highlights or passages to preserve — have the user paste them in

**Step 2 — Structure the notes**

```markdown
---
type: reading
date: <YYYY-MM-DD>
title: "<source title>"
author: "<author or publisher>"
source_type: <article|regulation|report|book|email|other>
reference: "<url or doc ref>"
tags: []
---

## Source
- **Title:** <title>
- **Author/Publisher:** <author>
- **Type:** <type>
- **Reference:** <url or doc ref>

## The Big Idea
<One paragraph: the core argument or finding>

## Key Takeaways
1. <takeaway>
2. <takeaway>

## Notable Quotes / Passages
> "<quote>"

## How This Connects
<How does this relate to existing work, open questions, or other notes?>

## My Questions & Reactions
<Your own thoughts and follow-up questions>

## Raw Highlights
<original highlights unchanged>
```

Show the note. Ask: "Anything to add or change?"

**Step 3 — Save**

Write the file to `<brain-root>/readings/YYYY-MM-DD-<slug>.md` using the Write tool.

Confirm the save and suggest 1-2 related topics to search with `/brain-retrieve`.
