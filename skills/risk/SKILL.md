---
name: risk
description: Compliance risk register management. Builds and maintains the institution's compliance risk register — identifies risks from domain-specific gap analyses, rates each risk by likelihood and impact, assesses current controls, assigns risk owners, and tracks treatment plans. Produces a scored risk register, executive heat map narrative, and board-level risk summary. Use when building a new risk register, updating after an audit cycle, preparing a board risk report, or conducting an annual compliance risk assessment.
argument-hint: "<scope> [all|domain:<domain>|risk:<id>] [mode:register|update|rate|treat|report|heat-map] — e.g. 'all register' or 'domain:RESEARCH rate' or 'risk:RISK-014 treat' or 'all heat-map'"
---

# /the-brain:risk — Compliance Risk Register

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
  - `rate` — score risks by likelihood × impact; produce the rated register with priority order
  - `treat` — develop or update treatment plans for specific risks
  - `report` — produce a compliance risk summary formatted for executive or board reporting
  - `heat-map` — produce a narrative risk heat map (textual table grid, not graphical) grouped by severity

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

## Risk Identification Sources

Pull risks from the following sources in the Brain:

### Domain skill outputs
Run each domain skill in `gap` mode and extract findings rated 🔴 or 🟠 as candidate risk register entries:
- `/the-brain:compliance` — general regulatory risk
- `/the-brain:titleix` — Title IX compliance risks
- `/the-brain:clery` — Clery Act risks
- `/the-brain:coi` — FCOI/COI risks
- `/the-brain:research` — research compliance risks
- `/the-brain:acgme` — GME/ACGME risks
- `/the-brain:lcme` — LCME risks
- `/the-brain:msche` — MSCHE risks
- `/the-brain:training` — training compliance risks
- `/the-brain:policy` — policy gaps as governance risks

### Brain PM sub-brain
- `pm/reports/` — prior audit findings; each unresolved finding is a candidate risk
- `pm/projects/` — active compliance projects often map to open risks
- `pm/notes/` — compliance officer observations

### External signals
- `/the-brain:reg-monitor` output — new regulatory requirements = new or changed risks
- `/the-brain:audit` escalation outputs — audit responses reveal risk exposure

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

| ID | Domain | Risk Title | L | I | Score | Level | Controls | Residual | Owner | Status |
|----|--------|-----------|---|---|-------|-------|---------|---------|-------|--------|
| RISK-001 | REG | [title] | 3 | 4 | 12 | 🟠 High | Adequate | 🟡 Med | VP Compliance | In Progress |
...

## Risks Requiring Immediate Attention

| ID | Risk | Score | Treatment Due | Days Overdue |
|----|------|-------|--------------|-------------|
```

Flag:
- Risks with no treatment plan and score ≥ 12 (🔴 or 🟠)
- Risks not reviewed in > 6 months
- Risks with treatment past due date
- Risks where treatment_status is "Not Started" and score ≥ 12

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
3. Present the scored register sorted by risk_score descending
4. Flag any risk where the score changed significantly since last rating
5. Ask: "Do any of these ratings look off to you?"
6. Write updated ratings back to the register

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

## Step 4: Offer follow-up actions

After producing output, offer:
1. **Save register** — write/update `wiki/compliance/risk-register.md`
2. **Create treatment tasks** — add all High/Critical treatment actions to `planner/tasks.md` with due dates and owners
3. **Board report** — run `/the-brain:board-report` to package this risk summary into a board compliance report
4. **Domain drill-down** — for any domain with multiple High/Critical risks, offer to run the domain skill in `gap` mode for a deeper look
5. **Calendar** — schedule the next quarterly risk review in `/the-brain:calendar`

---

## Quality Rules

- **The risk register is a living document** — it must be updated after every domain skill gap analysis, every audit finding, and every regulatory change. A static risk register is worse than none.
- **Risk score without a treatment plan is just a list of problems** — every risk at 🟠 High or above must have a treatment plan with an owner and due date.
- **Never conflate inherent risk with residual risk** — always record both: what the risk is before controls, and what it is after current controls are applied.
- **"Accepted" is a legitimate treatment status** — for Low and some Medium risks, formal acceptance with documentation is appropriate and more honest than a treatment plan no one will implement.
- **Risk owners must be roles, not individuals** — people change roles; the risk register must survive those transitions.
- **Regulatory changes automatically reopen risks** — when `/the-brain:reg-monitor` identifies a new or changed requirement, check whether it creates or modifies any existing risk register entries.
