---
name: delta
description: Compliance program change detection. Compares the current Brain state against prior scan snapshots to show exactly what moved — risks up or down, deadlines slipped or cleared, projects changed status, training rates shifted, new intelligence filed. Shows trend lines across multiple scans. Use weekly after running scan, before board meetings, or any time the VP needs to know what changed rather than what exists.
argument-hint: "[mode:compare|trend|snapshot] [period:1w|2w|1mo|3mo] — e.g. 'compare' or 'trend 3mo' or 'snapshot'"
---

# /compliance-brain:delta — Compliance Program Change Detection

You are showing the VP of Compliance what changed, not what exists. The dashboard shows the current state. The delta shows the direction of travel — whether the program is improving, holding steady, or slipping. Direction matters more than absolute position for managing a complex compliance program.

**The delta is grounded in scan records** saved by `/compliance-brain:scan`. It does not re-scan the Brain; it reads saved scan records and computes the differences. Run `/compliance-brain:scan` first if scan records are stale.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `compare` if not specified:
  - `compare` — compare today's scan vs. the prior scan (1-week delta); the standard weekly view
  - `trend` — multi-point trend lines across N scans; shows whether metrics are improving or worsening over time
  - `snapshot` — force-save a current-state snapshot now (useful before a board meeting or audit to anchor a baseline)

- **Period** (for `trend` mode):
  - `1w` — last 2 scans (one week)
  - `2w` — last 3 scans (two weeks)
  - `1mo` — last ~5 scans (one month)
  - `3mo` — last ~13 scans (quarter)
  - Default: `1mo`

---

## Step 2: Read scan records

Read scan files from `wiki/compliance/dashboards/scans/`:

- For `compare`: read the two most recent scan files
- For `trend`: read as many scan files as cover the requested period
- For `snapshot`: read current Brain state and write a new scan record (skip Steps 3–4; go to Step 5)

Sort scan files by date descending. Extract the structured frontmatter from each.

If fewer than 2 scan records exist: note this, explain that at least 2 weekly scans are needed for delta comparison, and suggest running `/compliance-brain:scan full` now to create the first or second record.

---

## Step 3: Compute deltas (compare mode)

Compare the most recent scan (`current`) against the prior scan (`prior`) field by field:

### Change indicators

| Symbol | Meaning |
|--------|---------|
| 🔺 N | Increased by N (worse) |
| 🔻 N | Decreased by N (better) |
| → | Unchanged |
| 🆕 | New since prior scan |
| ✅ | Resolved since prior scan |

### Fields to delta

| Metric | Prior | Current | Change | Direction |
|--------|-------|---------|--------|-----------|
| Critical risks | N | N | ±N | 🔺/🔻/→ |
| High risks | N | N | ±N | 🔺/🔻/→ |
| Untreated High+ risks | N | N | ±N | 🔺/🔻/→ |
| Overdue deadlines | N | N | ±N | 🔺/🔻/→ |
| Deadlines due in 14 days | N | N | ±N | 🔺/🔻/→ |
| Unowned deadlines | N | N | ±N | 🔺/🔻/→ |
| Training overall rate | N% | N% | ±N% | 🔺/🔻/→ |
| Populations below 80% | N | N | ±N | 🔺/🔻/→ |
| Projects at risk / off track | N | N | ±N | 🔺/🔻/→ |
| Stale projects | N | N | ±N | 🔺/🔻/→ |
| Active investigations | N | N | ±N | 🔺/🔻/→ |
| Investigations at deadline risk | N | N | ±N | 🔺/🔻/→ |
| Evidence weak/missing | N | N | ±N | 🔺/🔻/→ |
| Evidence expired | N | N | ±N | 🔺/🔻/→ |
| High-relevance intel (unactioned) | N | N | ±N | 🔺/🔻/→ |
| New critical findings this week | N | N | ±N | 🔺/🔻/→ |
| Quick wins identified | N | N | ±N | 🔺/🔻/→ |
| Items resolved | N | N | ±N | 🔺/🔻/→ |

### Overall program direction

Compute a simple program direction score:
- +1 for each metric that improved (🔻 in a "lower is better" metric, 🔺 in a "higher is better" metric)
- -1 for each metric that worsened
- 0 for unchanged

**Program Direction**: 🔺 Deteriorating / → Stable / 🔻 Improving

---

## Step 4: Produce output by mode

---

### Mode: `compare` — Weekly Delta Report

```markdown
---
title: Compliance Program Delta
date: YYYY-MM-DD
compared_to: YYYY-MM-DD
period: N days
---

# Compliance Program Delta — [Date] vs. [Prior Date]

## Program Direction: 🔺 Deteriorating / → Stable / 🔻 Improving

> [One sentence: what the delta shows. E.g., "The program improved on 6 of 18 metrics this week — training completion rose and one High risk was remediated, but two projects moved to At Risk and an investigation deadline is now flagged."]

---

## What Got Worse 🔺

| Metric | Was | Now | Change | Implication |
|--------|-----|-----|--------|-------------|
| [metric] | N | N | 🔺 N | [why this matters — what the VP should do] |
...

[If nothing worsened: "Nothing worsened this period. Program is holding or improving across all tracked metrics."]

---

## What Got Better 🔻

| Metric | Was | Now | Change | What Closed It |
|--------|-----|-----|--------|---------------|
| [metric] | N | N | 🔻 N | [what action produced the improvement] |
...

[If nothing improved: "No metrics improved this period."]

---

## Unchanged →

| Metric | Value | Note |
|--------|-------|------|
| [metric] | N | [flag if "unchanged but still critical"] |
...

---

## Notable Changes — Detail

### 🆕 New Items Since Last Scan

[List each new finding from the current scan's new_critical field, with one-line description]

### ✅ Resolved Since Last Scan

[List each item resolved, with one-line description of how]

### ⚠️ Items Flagged for Second Consecutive Scan

[Any item that appeared in both the prior and current scan's "worsening" category — chronic issues that are not improving deserve escalation]

| Item | Consecutive Scans Flagged | Recommended Escalation |
|------|--------------------------|----------------------|
| [item] | N weeks | [escalate to President? Board? External counsel?] |

---

## Metric Scorecard

| Metric | [Prior Date] | [Current Date] | Δ | Direction |
|--------|------------|--------------|---|-----------|
| Critical risks | N | N | ±N | 🔺/🔻/→ |
| High risks | N | N | ±N | 🔺/🔻/→ |
| Untreated High+ risks | N | N | ±N | 🔺/🔻/→ |
| Overdue deadlines | N | N | ±N | 🔺/🔻/→ |
| Due in 14 days | N | N | ±N | 🔺/🔻/→ |
| Training <80% populations | N | N | ±N | 🔺/🔻/→ |
| Projects at risk/off track | N | N | ±N | 🔺/🔻/→ |
| Active investigations | N | N | ±N | 🔺/🔻/→ |
| Investigation deadline risk | N | N | ±N | 🔺/🔻/→ |
| Evidence weak/missing | N | N | ±N | 🔺/🔻/→ |
| Unactioned intel (High) | N | N | ±N | 🔺/🔻/→ |
| **Items improved** | — | **N** | — | 🔻 |
| **Items worsened** | — | **N** | — | 🔺 |
```

---

### Mode: `trend` — Multi-Period Trend Lines

For each metric, show a sparkline-style trend across all scans in the period:

```markdown
---
title: Compliance Trend Analysis
date: YYYY-MM-DD
period: [1w | 2w | 1mo | 3mo]
scans_included: N
---

# Compliance Trend Analysis — [Period]
## [N] weekly scans: [earliest date] → [latest date]

## Program Direction Trend

| Week | [Date] | [Date] | [Date] | [Date] | [Date] | Trend |
|------|--------|--------|--------|--------|--------|-------|
| Direction score | +N | -N | +N | +N | -N | 🔺/🔻/→ |

---

## Metric Trend Table

| Metric | [W-4] | [W-3] | [W-2] | [W-1] | [Now] | 4-Week Trend |
|--------|-------|-------|-------|-------|-------|-------------|
| Critical risks | N | N | N | N | N | 🔺 Rising / 🔻 Falling / → Flat |
| High risks | N | N | N | N | N | |
| Untreated High+ | N | N | N | N | N | |
| Overdue deadlines | N | N | N | N | N | |
| Training <80% pops | N | N | N | N | N | |
| Projects at risk | N | N | N | N | N | |
| Active investigations | N | N | N | N | N | |
| Evidence weak/missing | N | N | N | N | N | |
| Resolved this week | N | N | N | N | N | |

---

## Trend Narratives

### 🔺 Consistently Worsening

[Any metric that worsened in 3 or more of the N scans — this is a chronic problem, not a blip]

| Metric | Trend | Weeks Worsening | Risk if Unaddressed |
|--------|-------|----------------|-------------------|
| [metric] | N → N | N of N weeks | [consequence] |

### 🔻 Consistently Improving

[Any metric that improved in 3 or more of the N scans — evidence that effort is working]

| Metric | Trend | Weeks Improving | What's Driving It |
|--------|-------|----------------|-----------------|
| [metric] | N → N | N of N weeks | [likely cause] |

### → Stubbornly Flat

[Metrics that haven't moved in 3+ weeks despite being at a concerning level — stuck problems]

| Metric | Value | Weeks Flat | Why It May Be Stuck | Suggested Intervention |
|--------|-------|-----------|--------------------|-----------------------|
| [metric] | N | N | [hypothesis] | [suggestion] |

---

## Quarter-to-Date Summary

| Quarter Start | [Date] | Today | [Date] | Net Change | Direction |
|--------------|--------|-------|--------|-----------|-----------|
| Critical risks | N | N | ±N | 🔺/🔻/→ |
| High risks | N | N | ±N | |
| Overdue deadlines | N | N | ±N | |
| Projects at risk | N | N | ±N | |

**Quarter narrative**: [2-3 sentences: how the program has moved over the quarter, what's driving the biggest changes]
```

---

### Mode: `snapshot` — Force-Save a Baseline

When the user wants to anchor a specific moment — before a board meeting, before an audit, at fiscal year start:

1. Run the equivalent of a scan across all Brain source files (same reads as `/compliance-brain:scan` Step 3)
2. Save a scan record to `wiki/compliance/dashboards/scans/YYYY-MM-DD-scan.md` with the full structured frontmatter
3. Add a note field: `snapshot_label: "Board meeting baseline"` or whatever the user provides

Output:
```
Snapshot saved: wiki/compliance/dashboards/scans/YYYY-MM-DD-scan.md
Label: [user label]
Metrics captured: [list key values]
Next delta comparison will use this as the baseline.
```

---

## Step 5: Offer follow-up actions

After any mode, offer:
1. **Full scan** — if the delta shows worsening trends, run `/compliance-brain:scan full` for a fresh ranked priority list
2. **Risk prioritize** — for any rising risk metric, run `/compliance-brain:risk all prioritize` to see which risks to address first
3. **Board report** — if preparing for a board meeting, the trend data makes a compelling program narrative via `/compliance-brain:board-report`
4. **Create tasks** — for any "consistently worsening" metric, offer to create a targeted remediation task in `planner/tasks.md`

Append to `log.md`:
```
## [YYYY-MM-DD] delta | [compare/trend/snapshot] | [period]
Program direction: [Improving/Stable/Deteriorating]. Metrics worsened: N. Metrics improved: N. [Notable: top 1-2 changes.]
```

---

## Quality Rules

- **Delta is meaningless without consistent scan cadence** — the VP should run `/compliance-brain:scan` every Monday. A two-week gap produces a coarser delta. A month gap produces a useless one. Flag gap in scan cadence at the top of every delta report.
- **Consecutively flagged items need escalation** — an item that appeared in two or more consecutive weekly scans without resolution is not being managed. Surface these as chronic issues requiring a different intervention, not just another task.
- **Direction matters more than absolute values** — a program with 5 Critical risks that went from 7 last month is improving. A program with 2 Critical risks that went from 0 is deteriorating. Context is everything.
- **"Stubbornly flat" is a management signal** — a metric that won't move despite apparent effort usually means the root cause isn't being addressed, the owner isn't resourced, or the metric is measuring the wrong thing. Flag it.
- **The snapshot is a commitment device** — when the VP saves a pre-board snapshot, they are anchoring accountability. The next delta will show exactly what moved (or didn't) since that moment.
