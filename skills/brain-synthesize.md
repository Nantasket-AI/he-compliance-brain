# brain-synthesize

Pull together everything in the second brain on a topic and produce a polished synthesis document.

## Instructions

**Step 1 — Get the topic**

Use $ARGUMENTS as the topic. If empty, ask: "What topic should I synthesize across your notes?"

**Step 2 — Collect all relevant notes**

Use the Grep tool to find all notes mentioning this topic across the entire brain root. Read every relevant file. Aim to pull from multiple types — meetings, decisions, readings, people — to get the full picture.

**Step 3 — Write the synthesis**

```markdown
# <Topic> — Knowledge Synthesis
*Generated: <date> | Sources: <N notes>*

## Executive Summary
<3-5 sentences: what you know, what has happened, where things stand>

## Background & Context
<How did this topic arise? What's the history in your notes?>

## Key Findings & Insights
### <Subtopic 1>
<Narrative synthesis — connect ideas across sources, don't just list>

### <Subtopic 2>
...

## Decisions Made
| Decision | Date | Owner | Status |
|---|---|---|---|
| <decision> | <date> | <owner> | Active / Revisit |

## Key People
| Name | Role | Notes |
|---|---|---|
| <name> | <role> | <what to remember> |

## Open Questions & Gaps
- <unresolved item>
- <missing information>

## Recommended Next Actions
1. <action>
2. <action>

## Sources Used
| Note | Type | Date |
|---|---|---|
| <title> | <type> | <date> |
```

**Step 4 — Confirm and optionally save**

Show the synthesis and ask: "Save this as a note for future reference?"

If yes, write it to `<brain-root>/readings/YYYY-MM-DD-synthesis-<topic-slug>.md` with frontmatter:
```
type: reading
date: <today>
title: "Synthesis — <topic>"
tags: [synthesis]
```
