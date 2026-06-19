# brain-capture-decision

Log a decision with full context: what was decided, why, who approved it, and what alternatives were considered.

## Instructions

**Step 1 — Gather the decision**

Ask (or infer from $ARGUMENTS):
- What exactly was decided?
- Who made or approved this decision, and when?
- What problem or question prompted it?
- What alternatives were considered and why rejected?
- What risks or tradeoffs were acknowledged?
- Under what conditions should this be revisited?
- Any references (policies, regulations, prior decisions)?

**Step 2 — Format the log**

```markdown
---
type: decision
date: <YYYY-MM-DD>
title: "<brief decision title>"
decision_owner: "<name or role>"
tags: []
---

## Decision
<Clear, precise statement of what was decided>

## Context
<What problem or situation prompted this?>

## Decision Maker(s)
- <Name / Role> — approved <date>

## Alternatives Considered
| Option | Why Rejected |
|---|---|
| <option> | <reason> |

## Risks & Tradeoffs Acknowledged
- <risk or tradeoff>

## Conditions for Revisiting
<When or under what circumstances should this be re-evaluated?>

## References
- <policy / regulation / prior decision>

## Notes
<Any other context>
```

Show the log. Ask: "Does this capture the decision accurately?"

**Step 3 — Save**

Write the file to `<brain-root>/decisions/YYYY-MM-DD-<slug>.md` using the Write tool.

Confirm the save. Remind the user this log is searchable via `/brain-retrieve`.
