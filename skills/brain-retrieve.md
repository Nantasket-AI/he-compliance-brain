# brain-retrieve

Search the second brain by topic or keyword and surface what's most relevant.

## Instructions

**Step 1 — Get the query**

Use $ARGUMENTS as the search query. If empty, ask: "What topic or question are you looking for?"

**Step 2 — Search across all notes**

Use the Grep tool to search the brain root for the query terms:

```
pattern: <query terms>
path: <brain-root>
glob: **/*.md
output_mode: content
```

Run multiple searches if needed — one per key term. Look across all subdirectories (meetings, readings, decisions, people).

**Step 3 — Read top matches**

Identify the most relevant files from the grep results. Read up to 5 of them using the Read tool to get full context.

**Step 4 — Synthesize and present**

Do not dump raw notes. Present a synthesized answer:

```
## What I Found: <query>

### Key Points
- <most relevant insight>
- <next insight>

### From Your Notes
| Note | Date | Relevant Excerpt |
|---|---|---|
| <title> | <date> | <excerpt> |

### Connections
<How do these notes relate to each other? Patterns or contradictions?>

### Gaps
<What's missing that the user probably wants to know?>
```

**Step 5 — Offer next steps**

- "Want a full synthesis? Use `/brain-synthesize <topic>`"
- "Something missing? Capture it with `/brain-capture`"
