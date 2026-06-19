# brain-daily

Daily review: what was captured recently, open action items, and what needs attention today.

## Instructions

**Step 1 — Find recent captures**

Use the Glob tool to list all `.md` files in `<brain-root>/**/*.md`, then filter for files whose filenames start with a date from the past 7 days.

**Step 2 — Scan for open action items**

Read the most recent meeting notes. Extract all unchecked `- [ ]` items.

**Step 3 — Present the daily briefing**

```
## Brain Daily Review — <today's date>

### Captured This Week (<N> notes)
| Date | Type | Title |
|---|---|---|
| <date> | meetings/readings/decisions/people | <title> |

### Open Action Items
- [ ] <action> — from: <meeting title> (<date>)

### Decisions to Revisit
<Decisions from recent notes with approaching revisit conditions>

### People to Follow Up With
<Open items from people notes>

### Suggested Focus
<Based on this week's captures, what looks highest priority for today?>
```

**Step 4 — Offer**

- "Want to dive into any topic? `/brain-retrieve <topic>`"
- "Ready to capture something? `/brain-capture`"
