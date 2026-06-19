# brain-ingest-sharepoint

Pull a SharePoint document or page into the second brain.

## Instructions

**Step 1 — Get the content**

Ask the user for one of:
- A SharePoint URL to fetch
- Pasted document content (if they can't share the URL or it's behind auth)
- Both a URL (for reference) and pasted content

If $ARGUMENTS contains a URL or title, use it.

**Step 2 — Fetch the content (if URL provided)**

Use the WebFetch tool to retrieve the URL. SharePoint pages often render as HTML — extract the readable text content and ignore navigation chrome.

If the document is a Word/PDF file and WebFetch returns binary, ask the user to copy-paste the text content instead.

**Step 3 — Structure the reading note**

```markdown
---
type: reading
date: <today>
title: "<document title>"
source_type: sharepoint
reference: "<sharepoint url>"
author: "<document author if visible>"
tags: [sharepoint]
---

## Source
- **Title:** <title>
- **Location:** <SharePoint site / library path>
- **URL:** <url>
- **Author:** <author>
- **Last Modified:** <date if visible>

## The Big Idea
<What is this document about and why does it matter?>

## Key Points
1. <point>
2. <point>

## Notable Sections
<Summarize the most important sections or findings>

## How This Connects
<How does this relate to existing work, regulations, or open questions?>

## Action Items or Follow-ups
- [ ] <anything this document requires>

## Full Content
<extracted text of the document>
```

Show the formatted note. Ask: "Anything to adjust or add?"

**Step 4 — Save**

Write to `<brain-root>/readings/YYYY-MM-DD-sharepoint-<slug>.md` using the Write tool.

Confirm the save.
