---
name: dashboard
description: Compliance program dashboard. Produces a single-pane-of-glass view of the institution's compliance program health — open risks, upcoming deadlines, training gaps, active project statuses, audit findings, and regulatory action items. Use at the start of each week, before board meetings, or any time the VP of Compliance needs a complete program status view.
argument-hint: "[mode:full|quick|risks|calendar|projects|training] — e.g. 'full' or 'quick' or 'risks' or 'projects'"
---

# /compliance-brain:dashboard — Compliance Program Dashboard

You are producing the VP of Compliance's unified program dashboard. This is the single view that answers the question: *What is the state of our compliance program right now?* It synthesizes risk posture, deadline exposure, project progress, training status, and audit standing into a decision-ready briefing.

Run this skill weekly (Monday morning with `/compliance-brain:myday`), before every board meeting, and any time an executive asks "where do we stand?"

---

## Step 1: Parse the request

From the user's input, determine the dashboard mode — default to `full` if not specified:

- `full` — complete program dashboard (all sections)
- `quick` — executive snapshot: top risks, next 30 days, critical alerts only (under 1 page)
- `risks` — risk register focus: current risk distribution, critical/high risks, treatment status
- `calendar` — deadline focus: next 90 days, overdue items, unowned deadlines
- `projects` — project portfolio focus: all active projects, status, milestones, owners
- `training` — training compliance focus: completion rates, gaps, overdue populations

---

## Step 2: Gather from the Brain

Read the following in parallel — you need all of it to produce the dashboard:

### Risk Register
- `wiki/compliance/risk-register.md` — full risk register; count by severity; identify critical/high risks with no treatment plan or overdue treatment

### Compliance Calendar
- `wiki/compliance/compliance-calendar-YYYY.md` (current year) — deadlines in the next 90 days, overdue items
- `planner/tasks.md` — deadline-related tasks; flag tasks with due dates in the next 30 days

### Project Portfolio
- `pm/overview.md` — active projects narrative and overall status
- `pm/index.md` — all projects organized by status
- `pm/projects/` — read each active project page for current phase, next milestone, owner, risks/blockers

### Training Status
- `wiki/compliance/training-register.md` or equivalent training tracker — completion rates by population and requirement; overdue populations; expiring certifications

### Audit Standing
- `pm/reports/` — most recent audit or review reports; any open corrective action plans (CAPs); findings not yet closed
- `wiki/compliance/` — any active audit response pages

### Regulatory Actions
- `wiki/compliance/reg-monitor/` — most recent regulatory intelligence brief; action items pending response
- `planner/tasks.md` — tasks tagged regulatory or with regulatory owners

### Active Investigations
- `investigations/index.md` — count of active matters by type; any matters with deadlines in the next 14 days; any matter with a missed deadline
- `investigations/active/` — scan for cases flagged `deadline_at_risk: true`

### Evidence Locker
- `evidence/index.md` — count of artifacts by sufficiency; count of expired or expiring artifacts (next 90 days); domains with gaps

### Intelligence Alerts
- `intel/index.md` — High-relevance items filed in the last 30 days that have action items not yet completed

### Daily/Weekly Context
- Today's daily file in `planner/YYYY/MM/` — any flagged alerts or priorities from today's plan
- `planner/goals.md` — check if any compliance program goals are off-track or approaching milestones

---

## Step 3: Gather live state from connectors

Augment Brain knowledge with current connector data:

- **Jira**: sprint status for active compliance projects; tickets past due; new high-priority tickets created since last dashboard
- **Outlook calendar**: board meetings, accreditor site visits, submission deadlines in the next 30 days that the Brain may not have captured
- **Outlook email / Teams**: any compliance alerts, regulatory emails, or accreditor communications received this week not yet ingested

---

## Step 4: Compute program health indicators

Calculate these indicators from the gathered data:

### Risk Health
- Count risks by severity: Critical 🔴 / High 🟠 / Medium 🟡 / Low 🟢
- Count risks with no treatment plan and score ≥ 12
- Count risks with overdue treatment (treatment_due in the past)
- **Risk Signal**: 🔴 if any Critical risks exist or ≥ 3 High risks untreated | 🟠 if High risks exist with treatment in progress | 🟡 if only Medium/Low | 🟢 if all High+ have active treatment plans on track

### Deadline Health
- Count deadlines due in next 30 days
- Count overdue deadlines (past due, unconfirmed complete)
- Count unowned deadlines
- **Deadline Signal**: 🔴 if any overdue hard federal/accreditor deadlines | 🟠 if overdue optional deadlines or ≥ 3 items due in 14 days | 🟡 if items due in 30 days but covered | 🟢 if all deadlines tracked and owned

### Project Health
- Count active projects by status (On Track / At Risk / Off Track / Stalled)
- Count projects with no update in > 2 weeks
- **Project Signal**: 🔴 if any critical project is Off Track | 🟠 if any project is At Risk with no mitigation | 🟡 if projects are delayed but managed | 🟢 if all active projects on track

### Training Health
- Overall completion rate across all mandatory training
- Count populations with < 80% completion
- Count individuals with overdue certifications (if tracked)
- **Training Signal**: 🔴 if any federally required training < 80% complete | 🟠 if accreditor-required training gaps | 🟡 if gaps in recommended training | 🟢 if all mandatory training ≥ 90%

### Audit Health
- Count open corrective action plans (CAPs)
- Count CAP items past due
- Days since last internal compliance review
- **Audit Signal**: 🔴 if CAP items overdue and regulator notified | 🟠 if open CAP items past due | 🟡 if CAP in progress on schedule | 🟢 if no open CAPs

---

## Step 5: Produce output by mode

---

### Mode: `full` — Complete Program Dashboard

```markdown
---
title: Compliance Program Dashboard
date: YYYY-MM-DD
prepared_for: VP of Compliance
---

# Compliance Program Dashboard
## [Institution Name] — [Day, Month DD, YYYY]

---

## Program Health Overview

| Domain | Signal | Status Summary |
|--------|--------|---------------|
| Risk Register | 🔴/🟠/🟡/🟢 | [N Critical, N High, N untreated] |
| Compliance Calendar | 🔴/🟠/🟡/🟢 | [N overdue, N due in 30 days] |
| Active Projects | 🔴/🟠/🟡/🟢 | [N on track, N at risk, N stalled] |
| Training Compliance | 🔴/🟠/🟡/🟢 | [N% overall completion, N gaps] |
| Audit Standing | 🔴/🟠/🟡/🟢 | [N open CAPs, N overdue items] |

**Overall Program Signal**: 🔴/🟠/🟡/🟢

> [1-2 sentence plain-language summary of the program's overall posture right now. Be direct: what is the most important thing the VP needs to know this morning?]

---

## 🚨 Requires Immediate Attention

[List only items that need action TODAY or THIS WEEK — overdue deadlines, untreated critical risks, stalled audit responses. If nothing is immediate, say "No immediate action items — see priority items below."]

| # | Item | Category | Due / Overdue By | Owner | Recommended Action |
|---|------|----------|-----------------|-------|--------------------|
| 1 | [item] | [Risk/Deadline/Audit/Project] | [date or N days overdue] | [owner or ⚠️ Unowned] | [specific action] |

---

## 📊 Risk Register Summary

**Current Risk Distribution**

| Level | Count | Untreated (score ≥ 12) | Treatment Overdue |
|-------|-------|----------------------|------------------|
| 🔴 Critical (20–25) | N | N | N |
| 🟠 High (12–19) | N | N | N |
| 🟡 Medium (6–11) | N | — | — |
| 🟢 Low (1–5) | N | — | — |
| **Total** | **N** | **N** | **N** |

**Top Risks Requiring Attention**

| ID | Risk | Domain | Score | Treatment Status | Owner | Treatment Due |
|----|------|--------|-------|-----------------|-------|--------------|
| RISK-NNN | [title] | [domain] | N | [status] | [owner] | [date] |
[List up to 5 highest-priority risks]

*[Run `/compliance-brain:risk` for full register and treatment planning.]*

---

## 📅 Upcoming Compliance Deadlines — Next 90 Days

**🔴 Overdue**
| Deadline | Was Due | Owner | Authority |
|----------|---------|-------|-----------|
[If none: "No overdue deadlines confirmed — verify completions for items without documentation."]

**🟠 Due in the Next 30 Days**
| Deadline | Due Date | Days Left | Owner | Status |
|----------|----------|-----------|-------|--------|
| [deadline] | YYYY-MM-DD | N | [owner] | [submitted/in progress/not started] |

**🟡 Due in 31–90 Days**
| Deadline | Due Date | Owner | Notes |
|----------|----------|-------|-------|

⚠️ **Unowned Deadlines**: [N] deadlines have no assigned owner — see full calendar.

*[Run `/compliance-brain:calendar 90` for complete deadline view.]*

---

## 🗂️ Active Project Portfolio

| Project | Phase | Status | Next Milestone | Owner | Last Updated |
|---------|-------|--------|---------------|-------|-------------|
| [project] | [phase] | 🟢 On Track / 🟡 At Risk / 🔴 Off Track | [milestone — date] | [owner] | [date or ⚠️ Stale] |
[List all active projects]

**Projects Needing Attention**:
[Flag: stalled projects, At Risk/Off Track projects, projects with no update in > 2 weeks]

*[Run `/compliance-brain:project <name>` for full project briefing with connector data.]*

---

## 🎓 Training Compliance

| Requirement | Population | Due | Completion Rate | Status |
|-------------|-----------|-----|-----------------|--------|
| [training name] | [who is required] | [cycle] | N% (N/N) | 🟢/🟡/🟠/🔴 |
[List all mandatory training requirements]

**Training Gaps**:
- [Population / department] has [N%] completion on [requirement] — [N] individuals overdue
[If no gaps: "All mandatory training requirements are meeting minimum thresholds."]

*[Run `/compliance-brain:training` for detailed compliance report.]*

---

## 🔍 Audit & Review Standing

| Review | Conducted | Findings | Open CAP Items | Next Due |
|--------|-----------|----------|---------------|----------|
| [audit/review name] | YYYY-MM-DD | N findings | N open (N overdue) | YYYY-MM-DD |

**Open Corrective Action Items**:
| Finding | CAP Item | Owner | Due | Status |
|---------|----------|-------|-----|--------|
[If none: "No open corrective action items."]

---

## 📡 Regulatory Watch

**Pending Action Items from Regulatory Intelligence**:
| Development | Agency | Action Required | Deadline | Owner |
|-------------|--------|-----------------|----------|-------|
[List action-required regulatory items; if none: "No action-required regulatory items at this time."]

**On the Horizon** (next 90 days):
[1–3 bullets on significant anticipated regulatory developments]

*[Run `/compliance-brain:reg-monitor all scan` for full regulatory intelligence.]*

---

## ⚖️ Active Investigations

| Active Matters | Types | Deadlines in 14 Days | At-Risk Deadlines |
|---------------|-------|---------------------|-------------------|
| N | [Title IX: N, Research Misconduct: N, HIPAA: N, Other: N] | N | N 🔴 |

[If deadline_at_risk cases exist]: **⚠️ [N] matter(s) at risk of missing a required deadline — review `investigations/active/` immediately.**

*Full details restricted — run `/compliance-brain:investigate review` for case-level status.*

---

## 🗄️ Evidence Locker Status

| Total Artifacts | Strong | Adequate | Weak | Expired/Missing |
|----------------|--------|----------|------|----------------|
| N | N | N | N | N |

**Domains with evidence gaps**: [list domains where Weak or Missing > 0]

*Run `/compliance-brain:evidence gap all` for full gap analysis.*

---

## 📡 Intelligence Alerts

**High-relevance items requiring action (last 30 days)**:
[List INTEL items with relevance: High and action_required: true, if any]
[If none: "No unactioned High-relevance intelligence items in the last 30 days."]

---

## 📌 This Week's Priorities

[Pull from today's daily plan if run, or synthesize from the dashboard data above]

1. [Top priority — with rationale from dashboard data]
2. [Second priority]
3. [Third priority]

---

*Dashboard generated: [YYYY-MM-DD HH:MM]. Data current as of Brain sync and connector queries above. Run `/compliance-brain:sync` to refresh project state.*
```

---

### Mode: `quick` — Executive Snapshot

```markdown
# Compliance Snapshot — [Month DD, YYYY]

## Program Signal: 🔴/🟠/🟡/🟢

**[1-sentence plain-language summary]**

## 🚨 Needs Action Now
- [item 1]
- [item 2]
[If none: "Nothing requires immediate escalation."]

## Risk: 🔴/🟠/🟡/🟢
[Critical: N | High: N | N untreated]

## Deadlines: 🔴/🟠/🟡/🟢
[Overdue: N | Due in 30 days: N]

## Projects: 🔴/🟠/🟡/🟢
[At Risk/Off Track: N of N active]

## Training: 🔴/🟠/🟡/🟢
[Lowest completion: N% on [requirement]]
```

---

### Mode: `risks` — Risk Focus

Present the full risk register table from `wiki/compliance/risk-register.md`, sorted by score descending. Highlight:
- Untreated High/Critical risks
- Overdue treatment plans
- Risks added since last review

Then offer: run `/compliance-brain:risk all treat` to develop treatment plans.

---

### Mode: `calendar` — Deadline Focus

Delegate to `/compliance-brain:calendar 90` logic and present the result directly. Include the annual view summary for context.

---

### Mode: `projects` — Project Portfolio Focus

For each active project, present a one-row summary plus a brief status narrative. Flag any project that:
- Has status "At Risk" or "Off Track"
- Has not been updated in > 2 weeks
- Has a milestone due in the next 14 days

Offer: run `/compliance-brain:project <name>` for full briefing.

---

### Mode: `training` — Training Focus

Delegate to `/compliance-brain:training` logic for the full training compliance report.

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save dashboard** — write to `wiki/compliance/dashboards/YYYY-MM-DD-dashboard.md`
2. **Create priority tasks** — add immediate action items to `planner/tasks.md`
3. **Board report** — package this dashboard into a board-ready report via `/compliance-brain:board-report`
4. **Full risk review** — run `/compliance-brain:risk all register` to review the complete risk register
5. **Regulatory scan** — run `/compliance-brain:reg-monitor all scan` for fresh regulatory intelligence
6. **Sync** — run `/compliance-brain:sync` to update project pages with live connector data

---

## Quality Rules

- **The dashboard is only as good as the Brain** — if the risk register, training tracker, or project pages are stale, the dashboard will misrepresent the program. Flag staleness explicitly rather than presenting outdated data as current.
- **Program Signal is the VP's early warning** — err toward 🔴/🟠 when data is ambiguous or incomplete; a false alarm costs less than a missed risk.
- **Quantify everything** — "N risks untreated" not "some risks untreated"; "N% training completion" not "good completion." Precision is what separates a useful dashboard from a narrative.
- **Never manufacture data** — if the Brain has no training register or the risk register doesn't exist yet, say so clearly and offer to run the relevant skill to build it.
- **Overdue items always surface** — no matter which mode is requested, if anything is overdue, it appears. Overdue compliance items are never silenced.
