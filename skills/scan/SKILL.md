---
name: scan
description: Proactive weekly compliance gap scan. Runs across all compliance domains, the risk register, deadlines, training, policy, investigations, and evidence — then surfaces only what is new, worsening, or needs attention this week. Produces a ranked priority list and saves a scan record for delta comparison. Designed to run every Monday as part of myday. Use when you need a fresh read on the full program without knowing what to look for.
argument-hint: "[mode:full|quick|domain:<code>] — e.g. 'full' or 'quick' or 'domain:RESEARCH'"
---

# /compliance-brain:scan — Proactive Weekly Compliance Gap Scan

You are performing a proactive sweep of the compliance program on behalf of the VP of Compliance. This skill answers the question the VP shouldn't have to ask: *"What do I need to know about right now that I haven't thought to check?"*

This is not a deep audit of any single domain. It is a wide, fast scan across every dimension of the compliance program — looking for what is new, what is worsening, and what has crossed a threshold that warrants attention this week. It produces a single ranked priority list and saves a scan record so next week's scan can show what changed.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `full` if not specified:
  - `full` — complete scan across all domains and sub-brains
  - `quick` — high-severity items only (Critical risks, overdue deadlines, at-risk investigations); under 1 page
  - `domain:<code>` — scan a single compliance domain (REG, ACCRED, CLINICAL, RESEARCH, PRIVACY, HR, GOV, FINANCE)

---

## Step 2: Read the last scan record

Before scanning current state, read the most recent prior scan:

- `wiki/compliance/dashboards/scans/` — find the most recent `YYYY-MM-DD-scan.md` file
- Extract: scan date, gap count by severity, risk count by level, training completion rates, deadline status counts, project statuses, investigation count, evidence sufficiency summary
- Calculate days since last scan — flag if > 10 days (scan is overdue)

If no prior scan exists, note this and proceed with a baseline scan (no delta comparison possible yet).

---

## Step 3: Scan current state — read fast, read wide

Read each source below. **Do not run full domain skills** — read the indexed outputs and key registry files directly. Speed matters; this scan should feel like a brief, not a research project.

### Risk Register
- `wiki/compliance/risk-register.md`
- Extract: total risks by level; risks with no treatment plan (score ≥ 12); risks with overdue treatment; risks where `effort_to_remediate` is Low and score ≥ 12 (quick wins)
- Flag: any risk that was added since last scan date, or whose score increased

### Compliance Calendar
- `wiki/compliance/compliance-calendar-YYYY.md`
- Extract: overdue deadlines; deadlines due in the next 14 days; deadlines due in 15–30 days; unowned deadlines
- Flag: any deadline that crossed into "overdue" since last scan; any deadline with no owner

### Training Compliance
- `wiki/compliance/training-register.md` (or equivalent)
- Extract: overall completion rate; populations below 80%; populations below 90% with a federal requirement; certifications expiring in 30 days
- Flag: any population whose rate dropped since last scan; any expiring certification newly in the 30-day window

### Policy Registry
- `wiki/compliance/` — any policy inventory or tracking file
- Extract: policies past their review date; policies without an owner; policies flagged as requiring regulatory update
- Flag: policies whose review date passed since the last scan

### Project Portfolio
- `pm/overview.md` and `pm/index.md`
- Extract: active project count; projects marked At Risk or Off Track; projects with no update in > 14 days (stale); projects with a milestone due in the next 14 days
- Flag: any project that changed status since last scan; any project newly stale

### Investigations
- `investigations/index.md`
- Extract: active matter count by type; any matter with `deadline_at_risk: true`; any matter where a required step is past due
- Flag: any new matter opened since last scan; any matter that moved to a higher-risk status

### Evidence Locker
- `evidence/index.md`
- Extract: artifacts with Weak or Missing sufficiency; artifacts expired or expiring in 30 days; domains with no evidence coverage
- Flag: artifacts that expired since last scan; new gaps since last scan

### Intelligence Feed
- `intel/index.md` — items filed since last scan date with relevance 🔴 High
- Extract: any High-relevance intel items filed since last scan with `action_required: true`
- Flag: these directly (they are new by definition if filed since last scan)

### Regulatory Monitor
- `wiki/compliance/reg-monitor/` — most recent brief
- Extract: any action-required items not yet completed; any comment periods closing in the next 30 days

---

## Step 4: Classify every finding

For each finding from Step 3, assign:

| Classification | Criteria |
|---------------|---------|
| 🔴 **New Critical** | Appeared since last scan AND severity Critical or overdue federal deadline or missed investigation deadline |
| 🟠 **Worsening** | Existed at last scan but severity increased, or deadline moved from "due soon" to "overdue," or project moved from On Track to At Risk |
| 🟡 **Watch** | Existed at last scan, unchanged, but approaching a threshold (30 days to a deadline, 14 days to a milestone) |
| 🟢 **Resolved / Improving** | Present at last scan but now closed, completed, or risk score reduced |
| ⚡ **Quick Win** | Risk score ≥ 12 AND `effort_to_remediate: Low` — high value, low effort |

---

## Step 5: Rank all findings

Sort findings into a single ranked list:

1. 🔴 New Critical (highest urgency — appeared since last scan)
2. ⚡ Quick Wins with score ≥ 16 (high-impact, actionable now)
3. 🟠 Worsening (trending wrong direction)
4. ⚡ Quick Wins with score 12–15
5. 🟡 Watch (approaching threshold — not yet critical)
6. 🟢 Resolved / Improving (positive — include for completeness)

Within each tier, sort by severity (risk score descending, days overdue descending).

---

## Step 6: Produce scan output

```markdown
---
title: Compliance Gap Scan
date: YYYY-MM-DD
mode: full | quick | domain
prior_scan: YYYY-MM-DD (or "first scan")
days_since_last_scan: N
---

# Compliance Gap Scan — [Day, Month DD, YYYY]

**Prior scan**: [YYYY-MM-DD — N days ago] | **Scope**: [full / domain]

## Program Signal: 🔴/🟠/🟡/🟢

> [One sentence: what the scan found overall. E.g., "Two new critical items since Monday and one project moved off track — investigation deadline risk is the most urgent issue today."]

---

## 🔴 New Since Last Scan — Act Now

*Items that did not exist or were not flagged at the prior scan.*

| # | Finding | Domain | Severity | Days Until / Overdue | Owner | Recommended Action |
|---|---------|--------|----------|---------------------|-------|--------------------|
| 1 | [finding] | [domain] | [severity] | [N days] | [owner or ⚠️ Unowned] | [specific action] |
...

[If none: "No new critical items since last scan."]

---

## ⚡ Quick Wins — High Impact, Low Effort

*Risks scoring ≥ 12 that can be substantially remediated in days to weeks.*

| Risk ID | Risk | Score | Effort | What to Do |
|---------|------|-------|--------|-----------|
| RISK-NNN | [title] | N | Low | [specific remediation action] |
...

[If none: "No quick wins identified at this time."]

---

## 🟠 Worsening Since Last Scan

*Items that existed before but are trending in the wrong direction.*

| Finding | Domain | Change | From | To | Recommended Action |
|---------|--------|--------|------|----|--------------------|
| [finding] | [domain] | [what changed] | [prior state] | [current state] | [action] |
...

[If none: "No items worsened since the last scan."]

---

## 🟡 Approaching Threshold — Watch This Week

*Not yet critical but will be if not addressed.*

| Finding | Domain | Threshold | Days Until | Owner |
|---------|--------|-----------|-----------|-------|
| [finding] | [domain] | [what threshold] | N days | [owner] |
...

---

## 🟢 Resolved / Improved Since Last Scan

| Item | What Closed / Improved | Date |
|------|----------------------|------|
| [item] | [how it resolved] | YYYY-MM-DD |

[If none: "No items closed or improved since the last scan."]

---

## 📋 This Week's Top 5 Priorities

*Derived from the scan findings above — ordered by urgency × impact × feasibility.*

1. **[Priority]** — [one sentence on what to do and why it's #1]
2. **[Priority]** — [one sentence]
3. **[Priority]** — [one sentence]
4. **[Priority]** — [one sentence]
5. **[Priority]** — [one sentence]

---

## Scan Coverage Summary

| Domain / Area | Items Found | New | Worsening | Resolved |
|--------------|------------|-----|-----------|---------|
| Risk Register | N | N | N | N |
| Compliance Calendar | N | N | N | N |
| Training | N | N | N | N |
| Policy | N | N | N | N |
| Projects | N | N | N | N |
| Investigations | N | N | N | N |
| Evidence | N | N | N | N |
| Intelligence | N | N | N | N |
| **Total** | **N** | **N** | **N** | **N** |

*Next scan recommended: [YYYY-MM-DD — 7 days from now]*
```

---

## Step 7: Save the scan record

Write a structured scan record to `wiki/compliance/dashboards/scans/YYYY-MM-DD-scan.md`:

```markdown
---
scan_date: YYYY-MM-DD
mode: full
total_findings: N
new_critical: N
quick_wins: N
worsening: N
watch: N
resolved: N
risk_counts:
  critical: N
  high: N
  medium: N
  low: N
  untreated_high_plus: N
calendar:
  overdue: N
  due_14_days: N
  unowned: N
training:
  overall_rate: N%
  below_80_pct: N
  expiring_30_days: N
projects:
  active: N
  at_risk: N
  off_track: N
  stale: N
investigations:
  active: N
  deadline_at_risk: N
evidence:
  weak_missing: N
  expired: N
---
```

This structured record is what `/compliance-brain:delta` reads to compute program trends over time.

Append to `log.md`:
```
## [YYYY-MM-DD] scan | Full compliance gap scan
New critical: N. Quick wins: N. Worsening: N. Resolved: N. Top priority: [#1 finding]. Saved: [[wiki/compliance/dashboards/scans/YYYY-MM-DD-scan]].
```

---

## Step 8: Offer follow-up actions

After producing output, offer:
1. **Create tasks** — add all "Act Now" and Quick Win items to `planner/tasks.md` with owners and deadlines
2. **Risk prioritize** — run `/compliance-brain:risk all prioritize` to see the full effort-adjusted priority stack
3. **Delta view** — run `/compliance-brain:delta` to see how metrics are trending over multiple scans
4. **Domain deep dive** — for any domain with multiple new/worsening items, offer to run the domain skill in `gap` mode
5. **Remind check** — run `/compliance-brain:remind check` to ensure all approaching deadlines have reminder chains

---

## Integration with myday

When `/compliance-brain:myday` runs on Monday, it calls this skill automatically with `mode: quick`. The quick-mode output is inserted into the Monday briefing's "Program Alerts" section. The full scan record is still saved for delta tracking.

---

## Quality Rules

- **The scan is only as good as the Brain** — if the risk register hasn't been updated in 6 weeks, the scan will miss things. Flag stale source data explicitly rather than presenting it as current.
- **New is more urgent than existing** — a Critical risk that was there last week is being managed. A Medium risk that appeared since Monday may not be. Surface new items first regardless of severity tier.
- **Quick Wins are the VP's leverage** — a risk that can be substantially remediated in a week but is scoring High is more actionable than a Critical risk requiring 6 months of work. Surface quick wins prominently.
- **Five priorities, not fifteen** — the scan's job is to focus, not to produce a comprehensive to-do list. If everything is a priority, nothing is. The top 5 should be genuinely the five most important things.
- **The scan record must be machine-readable** — the structured frontmatter in Step 7 is what makes `/compliance-brain:delta` work. Never skip it.
