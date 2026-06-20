---
name: risk
description: Compliance risk register management. Builds and maintains the institution's compliance risk register — identifies risks, rates each by likelihood × impact × effort to remediate, derives an effort-adjusted priority index, assesses controls, assigns owners, and tracks treatment plans. Produces a scored risk register, priority stack, heat map, and board-level summary. Use when building a new risk register, updating after an audit cycle, prioritizing what to work on this quarter, or preparing a board risk report.
argument-hint: "<scope> [all|domain:<domain>|risk:<id>] [mode:register|update|rate|treat|report|heat-map|prioritize] — e.g. 'all prioritize' or 'domain:RESEARCH rate' or 'risk:RISK-014 treat' or 'all heat-map'"
---

# /compliance-brain:risk — Compliance Risk Register

You are building and managing the institutional compliance risk register on behalf of the VP of Compliance. The risk register is the authoritative record of what could go wrong, how likely it is, how bad it would be, what controls exist to prevent it, and what the institution is doing about it. A well-maintained risk register is evidence of a mature compliance program — regulators and accreditors increasingly expect to see one.

Every entry must be grounded in actual evidence: identified risks come from domain skill gap analyses, audit findings, training gaps, or documented regulatory exposure. Never manufacture risks.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which risks to work with
  - `all` — the full institutional compliance risk register
  - `domain:<domain>` — risks within a specific compliance domain (see taxonomy below)
  - `risk:<id>` — a specific risk by its register ID (e.g., `RISK-014`)

- **Mode**: output format — default to `register` if not specified:
  - `register` — read and present the full risk register (or domain subset); identify stale or missing entries
  - `update` — add new risks or update existing ones based on user input or domain skill output
  - `rate` — score risks by likelihood × impact AND effort to remediate; produce the full rated register
  - `treat` — develop or update treatment plans for specific risks
  - `report` — produce a compliance risk summary formatted for executive or board reporting
  - `heat-map` — produce a narrative risk heat map (textual table grid, not graphical) grouped by severity
  - `prioritize` — rank the register by the effort-adjusted priority index; the VP's "what to work on first" view

---

## Risk Register Data Model

Each risk entry must contain:

| Field | Description |
|-------|-------------|
| `risk_id` | Sequential identifier: `RISK-NNN` |
| `domain` | Compliance domain code (see taxonomy) |
| `risk_title` | Short name: what could go wrong (10 words max) |
| `risk_description` | Full description: what happens if this risk materializes |
| `regulatory_basis` | The regulation, standard, or obligation that creates this risk |
| `source` | How this risk was identified: audit finding / gap analysis / regulatory change / incident / management judgment |
| `likelihood` | 1 (Rare) to 5 (Almost Certain) |
| `impact` | 1 (Negligible) to 5 (Critical) |
| `risk_score` | `likelihood × impact` (1–25) |
| `risk_level` | Derived from score: Critical (20–25) / High (12–19) / Medium (6–11) / Low (1–5) |
| `current_controls` | What controls, policies, or monitoring currently reduce this risk |
| `control_effectiveness` | Strong / Adequate / Weak / None |
| `residual_risk_level` | Risk level AFTER considering current controls |
| `risk_owner` | Role/office responsible for managing this risk |
| `treatment_plan` | Specific actions to reduce the risk |
| `treatment_owner` | Role responsible for implementing treatment |
| `treatment_due` | Target date for treatment completion |
| `treatment_status` | Not Started / In Progress / Complete / Accepted |
| `last_reviewed` | Date this entry was last reviewed |
| `next_review` | Date this entry should next be reviewed |
| `effort_to_remediate` | Low / Medium / High — estimated effort to substantially close this risk (see scale below) |
| `priority_index` | Derived from risk level + effort: 🔥 Act Now / ⚡ Quick Win / 📋 Plan / ⏳ Defer (see matrix below) |

---

## Compliance Domain Taxonomy

| Code | Domain |
|------|--------|
| `REG` | Regulatory (HIPAA, FERPA, Title IX, Clery, ADA) |
| `ACCRED` | Accreditation (LCME, MSCHE, ACGME) |
| `CLINICAL` | Clinical / Patient Care (TJC, CMS, DEA) |
| `RESEARCH` | Research Compliance (IRB, FCOI, export, misconduct) |
| `PRIVACY` | Privacy & Data Security |
| `HR` | Employment & HR |
| `GOV` | Governance & Institutional Integrity |
| `FINANCE` | Financial Compliance (Title IV, Uniform Guidance) |

---

## Risk Scoring Matrix

### Likelihood Scale

| Score | Label | Description |
|-------|-------|-------------|
| 5 | Almost Certain | Expected to occur in most circumstances; multiple prior incidents |
| 4 | Likely | Will probably occur; history of occasional occurrence |
| 3 | Possible | Could occur; has occurred at peer institutions |
| 2 | Unlikely | Not expected; would require unusual circumstances |
| 1 | Rare | Only in exceptional circumstances; no peer precedent |

### Impact Scale

| Score | Label | Description |
|-------|-------|-------------|
| 5 | Critical | Federal enforcement action; loss of Title IV or research funding; accreditation revocation; criminal exposure |
| 4 | Major | Significant financial penalty (>$100K); accreditation warning or probation; public enforcement letter; major reputational harm |
| 3 | Moderate | Financial penalty (<$100K); corrective action plan required; accreditation finding; manageable reputational impact |
| 2 | Minor | Administrative sanction; minor finding requiring response; limited external visibility |
| 1 | Negligible | Internal process correction; no regulatory consequence; minimal impact |

### Risk Level Thresholds

| Score | Risk Level | Treatment Urgency |
|-------|-----------|------------------|
| 20–25 | 🔴 Critical | Immediate action required; escalate to President and Board |
| 12–19 | 🟠 High | Active treatment plan required; VP of Compliance owns; quarterly review |
| 6–11 | 🟡 Medium | Treatment plan recommended; semi-annual review |
| 1–5 | 🟢 Low | Accept or monitor; annual review |

---

## Effort-to-Remediate Scale

How hard is it to substantially close this risk? Rate based on the most realistic treatment path — not the ideal one.

| Label | Timeframe | What It Typically Means |
|-------|-----------|------------------------|
| **Low** | Days to weeks | Policy update already drafted; training module exists; one role responsible; no capital required; no external dependency |
| **Medium** | 1–3 months | Requires cross-departmental coordination; some resourcing; new procedure development; vendor or system change; committee approval |
| **High** | Quarter or more | Requires new hire or significant staffing; capital investment; regulatory approval; multi-year culture change; accreditor notification; legal process |

**Rule**: When in doubt, rate effort one level higher. Underestimating effort is the most common mistake in compliance remediation planning.

---

## Priority Index Matrix

Derived automatically from `risk_level` + `effort_to_remediate`. This is the VP's "what to work on first" view — it answers a different question than the risk score alone.

|  | **Low Effort** | **Medium Effort** | **High Effort** |
|--|---------------|------------------|----------------|
| **🔴 Critical (20–25)** | 🔥 Act Now | 🔥 Act Now | 🔥 Act Now + Escalate |
| **🟠 High (12–19)** | 🔥 Act Now | ⚡ Quick Win | 📋 Plan & Resource |
| **🟡 Medium (6–11)** | ⚡ Quick Win | 📋 Plan | ⏳ Defer |
| **🟢 Low (1–5)** | ⚡ Easy Win | ⏳ Defer | ⏳ Defer |

**Priority index labels:**

| Label | Meaning | Default Timeframe |
|-------|---------|------------------|
| 🔥 **Act Now** | Severity demands action regardless of effort | This week to this month |
| ⚡ **Quick Win** | High value relative to effort — do these early for fast program improvement | This quarter |
| 📋 **Plan & Resource** | Significant risk but effort requires planning; put in next quarter's plan | Next quarter |
| ⏳ **Defer** | Low enough risk or high enough effort that deferral is defensible with monitoring | Annual review |

---

## Risk Identification Sources

Pull risks from the following sources in the Brain:

### Domain skill outputs
Run each domain skill in `gap` mode and extract findings rated 🔴 or 🟠 as candidate risk register entries:
- `/compliance-brain:compliance` — general regulatory risk
- `/compliance-brain:titleix` — Title IX compliance risks
- `/compliance-brain:clery` — Clery Act risks
- `/compliance-brain:coi` — FCOI/COI risks
- `/compliance-brain:research` — research compliance risks
- `/compliance-brain:acgme` — GME/ACGME risks
- `/compliance-brain:lcme` — LCME risks
- `/compliance-brain:msche` — MSCHE risks
- `/compliance-brain:training` — training compliance risks
- `/compliance-brain:policy` — policy gaps as governance risks

### Brain PM sub-brain
- `pm/reports/` — prior audit findings; each unresolved finding is a candidate risk
- `pm/projects/` — active compliance projects often map to open risks
- `pm/notes/` — compliance officer observations

### External signals
- `/compliance-brain:reg-monitor` output — new regulatory requirements = new or changed risks
- `/compliance-brain:audit` escalation outputs — audit responses reveal risk exposure

---

## Step 2: Search the Brain for the existing risk register

### 2a. Wiki sub-brain
- Check `wiki/compliance/risk-register.md` — the authoritative risk register file
- Check `wiki/compliance/` for any domain-specific risk assessments

### 2b. PM sub-brain
- `pm/reports/` — prior risk reports; prior board risk updates
- `pm/projects/` — active treatment plan projects

### 2c. Planner
- `planner/tasks.md` — open risk treatment actions

If no risk register exists in the Brain, note this and proceed to create one.

---

## Step 3: Produce output by mode

---

### Mode: `register` — Present the Risk Register

Read the risk register from `wiki/compliance/risk-register.md`. Present it as a structured table:

```markdown
---
title: Compliance Risk Register
date: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
---

# Compliance Risk Register

## Summary
- Total Risks: N
- Critical 🔴: N | High 🟠: N | Medium 🟡: N | Low 🟢: N
- Risks with No Treatment Plan: N
- Risks Overdue for Review: N

---

## Full Register

| ID | Domain | Risk Title | L | I | Score | Level | Effort | Priority | Owner | Status |
|----|--------|-----------|---|---|-------|-------|--------|----------|-------|--------|
| RISK-001 | REG | [title] | 3 | 4 | 12 | 🟠 High | Medium | ⚡ Quick Win | VP Compliance | In Progress |
...

## Risks Requiring Immediate Attention

| ID | Risk | Score | Priority | Treatment Due | Days Overdue |
|----|------|-------|----------|--------------|-------------|
```

Flag:
- Risks with no treatment plan and score ≥ 12 (🔴 or 🟠)
- Risks not reviewed in > 6 months
- Risks with treatment past due date
- Risks where treatment_status is "Not Started" and score ≥ 12
- Risks missing `effort_to_remediate` — prompt to rate them

---

### Mode: `update` — Add or Update Risks

For each risk to add or update:

1. Ask the user to describe the risk, or accept it from domain skill output
2. Map it to the risk data model (fill all required fields)
3. Show the draft entry and ask: "Does this look right?"
4. Write to `wiki/compliance/risk-register.md` — add new rows or update existing by `risk_id`

When adding multiple risks at once (e.g., from a domain gap analysis), batch them and present for review before writing.

---

### Mode: `rate` — Score All Risks

For each risk in the register:

1. Read the risk description and regulatory basis
2. Apply the likelihood and impact scales (reason through each explicitly)
3. Apply the effort-to-remediate scale — reason through: what is the most realistic treatment path? Who owns it? Are there external dependencies? How long has similar work taken at this institution?
4. Derive the priority index from the risk level + effort matrix
5. Present the scored register sorted by priority_index first (🔥 Act Now → ⚡ Quick Win → 📋 Plan → ⏳ Defer), then by risk_score descending within each tier
6. Flag any risk where the score changed significantly since last rating
7. Flag any risk missing an effort rating
8. Ask: "Do any of these ratings or effort assessments look off to you?"
9. Write updated ratings back to the register

---

### Mode: `treat` — Develop Treatment Plans

For the specified risks (by ID or all risks with no treatment plan):

For each risk:

```markdown
## Treatment Plan: <RISK-NNN> — <Risk Title>

**Risk Level**: 🔴/🟠/🟡/🟢 | **Score**: N/25

**Current Controls**: <what's already in place>
**Control Effectiveness**: Strong / Adequate / Weak / None

**Treatment Options**:
1. **Reduce** — [specific action that lowers likelihood or impact]
   - Owner: [role] | Cost/effort: [estimate] | Timeline: [YYYY-MM-DD]
2. **Transfer** — [contract, insurance, or shared responsibility]
3. **Accept** — [conditions under which accepting this risk is appropriate]

**Recommended Treatment**: Option N — [rationale]

**Treatment Actions**:
| # | Action | Owner | Due | Evidence of Completion |
|---|--------|-------|-----|----------------------|
| 1 | [action] | [role] | YYYY-MM-DD | [artifact] |

**Residual Risk After Treatment**: [projected score and level]
**Review Date**: YYYY-MM-DD
```

Write treatment plans back to the register entries.

---

### Mode: `report` — Executive Risk Summary

```markdown
---
title: Compliance Risk Summary
prepared_for: <Board Compliance Committee | VP of Compliance | President>
date: YYYY-MM-DD
period: <quarter or annual>
---

# Compliance Risk Summary
## <Institution> — <Period>

## Executive Summary
[3–5 sentences: overall risk posture, most significant risks, material changes since last report, and key actions underway]

## Risk Portfolio Overview
- Total Risks Tracked: N
- Critical (🔴): N | High (🟠): N | Medium (🟡): N | Low (🟢): N
- New Risks Added This Period: N
- Risks Closed/Mitigated This Period: N
- Risks with Overdue Treatment: N

## Critical and High Risks

| ID | Risk | Domain | Score | Treatment Status | Owner |
|----|------|--------|-------|-----------------|-------|
| RISK-NNN | [title] | [domain] | N | In Progress | [owner] |
...

## Risk Movements Since Last Report
| ID | Risk | Change | From | To | Reason |
|----|------|--------|------|----|--------|
| RISK-NNN | [title] | ↑ Increased / ↓ Decreased | 🟡 Med | 🟠 High | [reason] |

## Key Treatment Progress
[Narrative on treatment actions completed, in progress, and at risk of slipping]

## Emerging Risks
[Risks identified this period from regulatory changes, audit findings, or incidents that are not yet fully assessed]

## Recommended Board Actions
[Specific decisions or approvals requested of the Board or Committee]
```

---

### Mode: `heat-map` — Risk Heat Map (Narrative Table)

```markdown
# Compliance Risk Heat Map — <Date>

## Risk Distribution by Likelihood × Impact

|                 | Impact 1 (Negligible) | Impact 2 (Minor) | Impact 3 (Moderate) | Impact 4 (Major) | Impact 5 (Critical) |
|-----------------|----------------------|-----------------|--------------------|-----------------|--------------------|
| **L5 Almost Certain** | 🟡 5 | 🟡 10 | 🟠 15 | 🔴 20 | 🔴 25 |
| **L4 Likely**         | 🟢 4 | 🟡 8  | 🟠 12 | 🟠 16 | 🔴 20 |
| **L3 Possible**       | 🟢 3 | 🟡 6  | 🟡 9  | 🟠 12 | 🟠 15 |
| **L2 Unlikely**       | 🟢 2 | 🟢 4  | 🟡 6  | 🟡 8  | 🟠 12 |
| **L1 Rare**           | 🟢 1 | 🟢 2  | 🟢 3  | 🟢 4  | 🟡 5  |

## Risks Plotted

[List each risk at its L×I coordinates:]

**🔴 Critical Zone (Score 20–25)**
- RISK-NNN: [title] (L=N, I=N, Score=N) — [one-sentence description]

**🟠 High Zone (Score 12–19)**
- RISK-NNN: [title] (L=N, I=N, Score=N)
...

**🟡 Medium Zone (Score 6–11)**
...

**🟢 Low Zone (Score 1–5)**
...

## Domain Distribution
| Domain | Critical | High | Medium | Low |
|--------|---------|------|--------|-----|
| REG | N | N | N | N |
| ACCRED | N | N | N | N |
...
```

---

### Mode: `prioritize` — Effort-Adjusted Priority Stack

The VP's "what to work on first" view. Unlike the risk register sorted by score, this sorts by the priority index — combining severity with effort so the register reflects what is actually worth doing *now* versus what needs planning or resourcing.

```markdown
---
title: Risk Priority Stack
date: YYYY-MM-DD
---

# Compliance Risk Priority Stack
## [Date] — Sorted by Priority Index

---

## 🔥 Act Now
*High severity AND/OR low effort makes these non-negotiable this quarter.*

| ID | Risk | Domain | Score | Effort | Why Now | Treatment Status | Owner |
|----|------|--------|-------|--------|---------|-----------------|-------|
| RISK-NNN | [title] | [domain] | N | Low/Med/High | [one-line rationale] | [status] | [owner] |
...

**This week's top pick**: RISK-NNN — [title]
*[One sentence: the single most actionable risk the VP should personally push this week, considering score, effort, and current treatment status.]*

---

## ⚡ Quick Wins
*Medium-high severity with low effort — maximize program improvement per hour invested.*

| ID | Risk | Domain | Score | Effort | Specific Action | Timeline | Owner |
|----|------|--------|-------|--------|----------------|---------|-------|
| RISK-NNN | [title] | [domain] | N | Low | [what specifically to do] | [days] | [owner] |
...

**Total quick-win potential**: [N] risks that could be substantially closed in the next 30 days with focused effort.

---

## 📋 Plan & Resource
*High severity but significant effort — these need to be in next quarter's plan with assigned resources.*

| ID | Risk | Domain | Score | Effort | What's Blocking Faster Progress | Needed Resource |
|----|------|--------|-------|--------|---------------------------------|----------------|
| RISK-NNN | [title] | [domain] | N | High | [barrier] | [what's needed] |
...

---

## ⏳ Defer
*Low severity or very high effort relative to risk level — monitor but don't prioritize resources.*

| ID | Risk | Domain | Score | Effort | Next Review |
|----|------|--------|-------|--------|------------|
| RISK-NNN | [title] | [domain] | N | High | YYYY-MM-DD |
...

---

## Priority Summary

| Priority | Count | This Quarter's Focus |
|----------|-------|---------------------|
| 🔥 Act Now | N | [brief description of the theme] |
| ⚡ Quick Wins | N | [brief description] |
| 📋 Plan & Resource | N | [brief description] |
| ⏳ Defer | N | Accept with monitoring |

**Risks missing effort rating**: [N] — run `/compliance-brain:risk all rate` to complete the assessment.
```

---

## Step 4: Offer follow-up actions

After producing output, offer:
1. **Save register** — write/update `wiki/compliance/risk-register.md`
2. **Create treatment tasks** — add all 🔥 Act Now and ⚡ Quick Win treatment actions to `planner/tasks.md` with due dates and owners
3. **Board report** — run `/compliance-brain:board-report` to package this risk summary into a board compliance report
4. **Domain drill-down** — for any domain with multiple High/Critical risks, offer to run the domain skill in `gap` mode for a deeper look
5. **Calendar** — schedule the next quarterly risk review in `/compliance-brain:calendar`
6. **Scan integration** — run `/compliance-brain:scan full` to see how the risk register fits into the full program picture

---

## Quality Rules

- **The risk register is a living document** — it must be updated after every domain skill gap analysis, every audit finding, and every regulatory change. A static risk register is worse than none.
- **Risk score without a treatment plan is just a list of problems** — every risk at 🟠 High or above must have a treatment plan with an owner and due date.
- **Never conflate inherent risk with residual risk** — always record both: what the risk is before controls, and what it is after current controls are applied.
- **"Accepted" is a legitimate treatment status** — for Low and some Medium risks, formal acceptance with documentation is appropriate and more honest than a treatment plan no one will implement.
- **Risk owners must be roles, not individuals** — people change roles; the risk register must survive those transitions.
- **Regulatory changes automatically reopen risks** — when `/compliance-brain:reg-monitor` identifies a new or changed requirement, check whether it creates or modifies any existing risk register entries.
- **Effort ratings unlock the priority index** — a risk register without `effort_to_remediate` fields is sorted by severity alone, which tells the VP what's most dangerous but not what's most actionable. Complete effort ratings before presenting the register to leadership.
- **Quick wins compound** — closing three Medium/Low-effort risks builds program credibility, frees capacity, and often reduces the severity of higher-scoring risks. The `prioritize` mode surfaces these explicitly; don't skip them in favor of only chasing the highest scores.
- **Act Now does not mean Act Alone** — 🔥 Act Now items with High effort need resourcing, not just urgency. Escalate these to leadership with a specific resource ask, not just a flag.
