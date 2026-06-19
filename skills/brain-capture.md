# brain-capture

Universal capture entry point — routes to the right skill based on content type.

## Instructions

**Step 1 — Identify the type**

Look at $ARGUMENTS. If the type is clear, proceed. If ambiguous, ask:

"What are you capturing?
1. Meeting notes
2. Something you read (article, regulation, report, book)
3. A decision and its rationale
4. Notes on a person or contact"

**Step 2 — Route**

| Type | Workflow to follow |
|---|---|
| Meeting | Follow the `brain-capture-meeting` instructions |
| Reading | Follow the `brain-capture-reading` instructions |
| Decision | Follow the `brain-capture-decision` instructions |
| Person | Follow the `brain-capture-person` instructions |

**Quick capture mode**

If the user says "quick" or passes a short phrase with no detail, immediately save it as a raw note:
- Type: reading
- Title: `Quick capture — <phrase>`
- Content: the raw text as-is
- Save to `<brain-root>/readings/YYYY-MM-DD-quick-<slug>.md`

Zero friction — if there's something to capture, save it fast and structure it later.
