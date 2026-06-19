---
name: board-report
description: Board and compliance committee reporting. Assembles a comprehensive compliance report for the Board of Trustees or a Board Compliance/Audit Committee. Synthesizes the risk register, regulatory intelligence, audit status, training compliance, and accreditation posture into an executive-level report with recommended actions. Use before each Board or Committee meeting, for quarterly compliance updates, or when the Board requests a compliance status briefing.
argument-hint: "<period> [mode:full|brief|risk-only|audit-only|quarter] — e.g. 'Q3-2026 full' or 'Q2-2026 risk-only' or 'annual brief'"
---

# /the-brain:board-report — Board & Compliance Committee Reporting

You are preparing a compliance report for the Board of Trustees or its Audit/Compliance Committee on behalf of the VP of Compliance. Board-level compliance reporting has a specific purpose: giving the Board enough information to fulfill its fiduciary and oversight duties without overwhelming it with operational detail. The Board needs to know what risks exist, what the institution is doing about them, what has changed since the last report, and what decisions or approvals it is being asked to make.

Every assertion in a board report must be defensible with documented evidence. Do not include metrics or status claims that cannot be substantiated by Brain content or connected system data.

---

## Step 1: Parse the request

From the user's input, determine:

- **Period**: the reporting period (quarter, year, or specific date range)

- **Mode**: output format — default to `full` if not specified:
  - `full` — complete board compliance report: executive summary, risk register summary, regulatory intelligence, audit status, accreditation posture, training compliance, and recommended actions
  - `brief` — condensed 1–2 page board brief (executive summary + top 5 risks + actions)
  - `risk-only` — risk register section only, formatted for board presentation
  - `audit-only` — audit response status only, formatted for board presentation
  - `quarter` — standard quarterly compliance update, focused on changes from the prior quarter

---

## Step 2: Gather compliance data from the Brain

Pull content from across the Brain to assemble the report. For each section, pull from the most recent available data — note when data is stale (> 90 days for regulatory/audit; > 12 months for accreditation).

### Risk Register
Read `wiki/compliance/risk-register.md` — extract:
- Total risks and distribution by level
- All Critical (🔴) and High (🟠) risks
- Changes from last quarter (new, escalated, de-escalated, closed)
- Risks with overdue treatment

### Regulatory Intelligence
Read most recent `wiki/compliance/reg-monitor/` briefs — extract:
- High-relevance regulatory developments
- Action-required items and their status
- Horizon items relevant to board awareness

### Audit Status
Read `pm/reports/` for audit CAPs — extract:
- Active external audits with open findings
- Response deadlines and status
- Recently closed audits and outcomes

### Accreditation Posture
Read from `wiki/compliance/` accreditation pages, recent gap analyses:
- Current accreditation status for MSCHE, LCME, ACGME
- Open conditions, AFIs, or citations
- Upcoming site visits or interim report deadlines

### Training Compliance
Read most recent `wiki/compliance/training-status*.md` — extract:
- Completion rates for high-risk/legally required programs
- Populations out of compliance
- Programs recently launched or completed

### Policy Health
Read most recent `wiki/compliance/policy-registry*.md` — extract:
- Count of overdue policy reviews
- Missing required policies

### Incident/Investigations (if applicable)
Read `pm/notes/` and `pm/reports/` for any open or recently closed compliance incidents:
- Note number and category only — no identifying details in the board report
- Note whether legal counsel is involved

---

## Step 3: Produce output by mode

---

### Mode: `full` — Complete Board Compliance Report

```markdown
---
title: Compliance Report to the Board of Trustees
prepared_by: Office of Compliance
presented_to: Board of Trustees / Audit and Compliance Committee
date: YYYY-MM-DD
period: <reporting period>
confidential: true
---

# Compliance Report
## <Institution Name>
## <Committee Name> — <Meeting Date>

---

## I. Executive Summary

[5–7 sentences covering: overall compliance posture for the period, most significant risks or developments, material changes from the prior report, any immediate decisions or approvals requested of the Board. Tone: direct and honest — the Board cannot govern what it cannot see.]

**Overall Compliance Posture**: 🔴 Elevated | 🟠 Heightened | 🟡 Moderate | 🟢 Sound
[Select one and provide a one-sentence rationale]

---

## II. Compliance Risk Register

**Total Risks Tracked**: N | Critical 🔴: N | High 🟠: N | Medium 🟡: N | Low 🟢: N

### Critical and High Risks

| ID | Risk | Domain | Score | Control Status | Treatment Status | Due |
|----|------|--------|-------|---------------|-----------------|-----|
| RISK-NNN | [title] | [domain] | N | Weak / Adequate / Strong | In Progress / Not Started | YYYY-MM-DD |
...

### Risk Movement This Quarter

| ID | Risk | Change | Reason |
|----|------|--------|--------|
| RISK-NNN | [title] | ↑ Escalated to High | [reason — regulatory change, audit finding, etc.] |
| RISK-NNN | [title] | ↓ Reduced to Medium | [reason — treatment completed, control strengthened] |
| RISK-NNN | [title] | ✅ Closed | [reason] |

### New Risks This Period
[List any newly identified risks with initial scoring]

---

## III. Regulatory Intelligence

### Significant Regulatory Developments

| Development | Agency | Date | Impact | Action Status |
|-------------|--------|------|--------|--------------|
| [title] | [agency] | YYYY-MM-DD | [High/Med/Low] | [Not started / In progress / Complete / No action needed] |

### Items Requiring Board Awareness

[Narrative of 2–3 most significant regulatory developments, written for a non-specialist board audience — plain language, institutional impact, what the institution is doing]

### Horizon Items
[Regulatory or accreditation changes anticipated in the next 12 months that the Board should be aware of]

---

## IV. External Audit Status

### Active Audits

| Audit | Source | Finding Date | Response Due | # Open Findings | Status |
|-------|--------|-------------|-------------|----------------|--------|
| [audit name] | [agency] | YYYY-MM-DD | YYYY-MM-DD | N | In Progress |

### Recently Closed Audits
| Audit | Source | Outcome | Closed Date |
|-------|--------|---------|------------|
| [audit name] | [agency] | [Resolved / Resolution Agreement / No Finding] | YYYY-MM-DD |

### Audit Risk Summary
[1–2 sentences: are there any audits at risk of non-closure or that may escalate?]

---

## V. Accreditation Posture

| Accreditor | Current Status | Open Findings | Next Event | Date |
|-----------|---------------|--------------|-----------|------|
| MSCHE | Accredited | N recommendations | [Monitoring report / Decennial review] | YYYY-MM |
| LCME | Accredited | N AFIs / N Conditions | [Interim report / Site visit] | YYYY-MM |
| ACGME | [N programs accredited] | N open citations | [CLER visit / AIR] | YYYY-MM |

[Narrative paragraph for any accreditor with open findings or an event within 18 months]

---

## VI. Training Compliance

| Training Program | Required Population | Completion Rate | Status | Action |
|-----------------|---------------------|----------------|--------|--------|
| HIPAA Privacy | All workforce | N% | 🟢/🟡/🔴 | [action if below target] |
| Title IX — Coordinator | Coordinator(s) | N% | | |
| CSA Training | All CSAs | N% | | |
| FCOI Training | Investigators | N% | | |
| IRB / CITI | Study teams | N% | | |
| Harassment Prevention | All employees | N% | | |
...

[Flag any program below 90% completion for legally required training]

---

## VII. Policy Health

- **Total Policies in Registry**: N
- **Current / In Compliance**: N (N%)
- **Stale / Overdue for Review**: N
- **Missing Required Policies**: N

[List any policy stale by > 12 months in a high-risk domain, or any missing required policy]

---

## VIII. Open Investigations / Incidents

[Number of open compliance investigations or incidents: N total — N regulatory, N research, N civil rights]
[No identifying details. Note involvement of Legal Counsel and whether any require Board notification under institutional bylaws or legal obligations.]

---

## IX. Compliance Program Updates

[Operational updates relevant to the Board: new staff, new systems, program initiatives, new policies approved, completed training launches, audit responses submitted]

---

## X. Recommended Board Actions

[List only items that require the Board's decision, approval, or acknowledgment. Be explicit.]

1. **[Action]** — [What you are asking the Board to do and why] — Recommended by: VP of Compliance
2. ...

---

## Appendices (Available Upon Request)

- Full compliance risk register with treatment plans
- Active audit corrective action plans
- Accreditation gap analysis reports
- Training completion detail reports
- Regulatory intelligence brief (full)

---

*Report prepared by the Office of Compliance, [Institution]. Confidential — Board/Committee distribution only.*
```

---

### Mode: `brief` — Condensed Board Brief (1–2 pages)

```markdown
---
title: Compliance Brief — Board of Trustees
date: YYYY-MM-DD
period: <period>
---

# Compliance Brief — <Institution> — <Period>

## Overall Posture: 🔴/🟠/🟡/🟢

[2 sentences: where things stand and what changed this period]

## Top 5 Compliance Risks

| # | Risk | Score | Status |
|---|------|-------|--------|
| 1 | [title — domain] | N/25 (🔴/🟠) | [treatment status] |
...

## Key Regulatory Developments
1. **[Development]** — [Agency] — [Impact and action status]
2. ...

## Audit & Accreditation Status
- Active audits with open findings: N
- Accreditation conditions or AFIs outstanding: N (MSCHE: N, LCME: N, ACGME: N)
- Next accreditation event: [event] — [date]

## Training Compliance Highlight
[One sentence on the highest-urgency training gap, or "All legally required programs at target completion" if compliant]

## Actions Requested of the Board
1. [Specific action] — [deadline if any]
```

---

### Mode: `quarter` — Standard Quarterly Update

Use the `full` format but restrict the narrative to **what changed since the prior quarter**:
- New risks added or risk scores that changed
- Regulatory developments since the last quarter
- Audit status changes (new audits opened, findings closed, deadlines approaching)
- Training completion changes
- Policy updates approved or outstanding

Begin with a single paragraph comparing the current quarter to the prior quarter ("This quarter's compliance posture is [better/worse/unchanged] compared to Q[N] [YYYY] because...").

---

## Step 4: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write report to `pm/reports/board-report-YYYY-MM-DD.md`
2. **Log** — append summary to `log.md`
3. **Create follow-up tasks** — add any Board-requested actions to `planner/tasks.md`
4. **Update dashboard** — note Board meeting date and report filed in `planner/dashboard.md`
5. **Source documents** — offer to pull the full versions of any component (risk register, reg monitor brief, audit CAP) as appendices

---

## Step 5: Log

Append to `log.md`:

```
## [YYYY-MM-DD] board-report | <mode> | <period>
Report prepared for [Board/Committee name] — [meeting date]. Mode: <mode>. Period: <period>. Risks reported: <N Critical, N High>. Audit findings: N open. Accreditation events: [list]. Actions requested: N. Filed: [[pm/reports/board-report-YYYY-MM-DD]].
```

---

## Quality Rules

- **Board members are not compliance professionals** — every risk, regulatory development, and audit finding must be translated into plain language with the institutional consequence stated clearly. Do not assume the Board knows what LCME Standard 3.6 means.
- **Overall posture rating must be justified** — if you rate posture as 🔴 Elevated, a critical risk or serious audit finding must support it; do not use the highest rating routinely.
- **Never fabricate metrics** — if completion rates, risk scores, or audit counts are not available from the Brain or connected systems, say "data not available" rather than estimating.
- **Investigations require legal privilege review** — if the board report includes information about ongoing investigations or litigation, the VP of Compliance should confirm with General Counsel what can be included and whether attorney-client privilege applies.
- **Board actions must be specific** — "For the Board's information" is not an action; distinguish clearly between items the Board must decide, items requiring approval, and items provided for awareness only.
- **Confidentiality matters** — board compliance reports contain sensitive information; note the distribution restriction on every page and do not file in any Brain location accessible to general staff.
