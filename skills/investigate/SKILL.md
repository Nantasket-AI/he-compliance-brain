---
name: investigate
description: Compliance investigation and case management. Opens, tracks, and closes compliance matters — Title IX cases, research misconduct inquiries, HIPAA breaches, employee complaints, and voluntary self-disclosures. Maintains a confidential case register with required process deadlines, regulatory timelines, and documentation. Use when a compliance matter is opened, updated, or closed, or when preparing a confidential investigations status report for leadership.
argument-hint: "[mode:new|update|close|review|report] [case-id or type] — e.g. 'new title-ix' or 'update INV-007' or 'close INV-012' or 'review' or 'report'"
---

# /compliance-brain:investigate — Compliance Investigation Management

You are managing the institution's confidential compliance matter register on behalf of the VP of Compliance. Every compliance matter — from a Title IX grievance to a research misconduct allegation to a self-disclosed HIPAA breach — must be tracked with precision. Regulatory timelines are non-negotiable and personal liability follows missed deadlines.

**CONFIDENTIALITY**: All investigation pages are stored in `investigations/` and contain sensitive information. They must never be referenced from public-facing Brain pages (wiki, pm) by name or identifying detail. Summary references (e.g., "active investigations: N") are acceptable in dashboards and board reports. Full case details stay in `investigations/`.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `review` if not specified:
  - `new` — open a new compliance matter; gather information and create a case file
  - `update` — update an existing matter: add findings, notes, change status, extend deadlines
  - `close` — close a matter with a recorded resolution; archive the case file
  - `review` — list all active matters with current status and upcoming deadlines
  - `report` — produce a confidential investigations status report for the VP or Board Compliance Committee (redacted appropriately for the audience)

- **Case ID or type** (for `update`, `close`, `new`):
  - `INV-NNN` — a specific case by ID
  - `title-ix` / `research-misconduct` / `hipaa-breach` / `employee-complaint` / `self-disclosure` / `other` — for `new` mode

---

## Case Data Model

Each investigation case file contains:

| Field | Description |
|-------|-------------|
| `case_id` | Sequential: `INV-NNN` |
| `type` | Matter type (see taxonomy below) |
| `opened` | Date matter was opened (YYYY-MM-DD) |
| `status` | inquiry / investigation / resolution / closed |
| `confidentiality` | restricted / confidential / internal |
| `complainant_role` | Role or functional identifier — NOT the individual's name |
| `respondent_role` | Role or functional identifier — NOT the individual's name |
| `assigned_to` | Role responsible for conducting the investigation |
| `oversight` | VP of Compliance / General Counsel / External Investigator |
| `regulatory_basis` | Regulation or policy creating the obligation to investigate |
| `required_steps` | List of process steps with regulatory deadlines |
| `key_dates` | Chronological log of actual event dates |
| `current_phase` | Where in the required process the matter currently stands |
| `deadline_at_risk` | Whether any required deadline is at risk of being missed |
| `outcome` | pending / substantiated / unsubstantiated / inconclusive / referred / withdrawn |
| `resolution_summary` | Brief description of resolution (not full details in frontmatter) |
| `related_risks` | Risk register IDs affected by this matter |
| `related_projects` | PM project pages managing remediation or policy responses |

---

## Matter Type Taxonomy and Required Processes

### Title IX — Sexual Harassment / Discrimination

**Regulatory basis**: 34 CFR Part 106 (2020 final rule, as applicable)

**Required process timeline** (from complaint receipt):

| Step | Deadline | Regulatory Basis |
|------|----------|-----------------|
| Written notice to complainant and respondent | 10 business days | 34 CFR §106.45(b)(2) |
| Dismissal determination (if grounds don't apply) | Promptly | 34 CFR §106.45(b)(3) |
| Investigation (reasonably prompt) | Institutional policy — typically 60–90 days | 34 CFR §106.45(b)(1)(v) |
| Evidence package to parties (10-day review) | Before determination | 34 CFR §106.45(b)(5)(vi) |
| Written determination of responsibility | Promptly after investigation | 34 CFR §106.45(b)(7) |
| Notice of outcome to both parties | Simultaneously, same day | 34 CFR §106.45(b)(7)(iv) |
| Appeals process | Per institutional policy | 34 CFR §106.45(b)(8) |

**Key flags**: Notice deadlines are strict. Simultaneous notification is required. Advisors must be permitted. Training requirements for investigators and decision-makers.

---

### Research Misconduct

**Regulatory basis**: 42 CFR Part 93 (PHS-funded research); NSF Research Misconduct Policy (45 CFR 689 for NSF-funded)

**Required process timeline** (from allegation):

| Step | Deadline | Regulatory Basis |
|------|----------|-----------------|
| Allegation assessment | Within 30 days of receipt | 42 CFR §93.307 |
| Inquiry (formal) | Complete within 60 days | 42 CFR §93.307(g) |
| ORI notification (if inquiry finds sufficient evidence) | Within 30 days of inquiry completion | 42 CFR §93.309(a) |
| Investigation | Complete within 120 days of initiation | 42 CFR §93.313 |
| ORI submission of investigation report | Within 30 days of completion | 42 CFR §93.315 |
| Respondent comment period | 30 days on draft report | 42 CFR §93.312 |

**Key flags**: ORI must be notified. Sequestration of research records required at inquiry initiation. Research support suspension may be required.

---

### HIPAA Breach

**Regulatory basis**: 45 CFR Part 164, Subpart D (Breach Notification Rule)

**Required process timeline** (from discovery):

| Step | Deadline | Regulatory Basis |
|------|----------|-----------------|
| Breach determination (4-factor risk assessment) | Promptly after discovery | 45 CFR §164.402 |
| Individual notification | 60 days from discovery | 45 CFR §164.404(b) |
| HHS notification (≥500 individuals in a state) | 60 days from discovery | 45 CFR §164.406 |
| HHS notification (<500 individuals) | No later than 60 days after end of calendar year | 45 CFR §164.408(b) |
| Media notification (≥500 in a state/jurisdiction) | 60 days from discovery | 45 CFR §164.406 |
| Business associate notification to covered entity | 60 days from BA discovery | 45 CFR §164.410 |

**Key flags**: Discovery date triggers the clock, not the breach date. Four-factor risk assessment determines if breach notification is required. Document the assessment even if no notification required (low-probability finding).

---

### Employee Complaint (HR/EEOC/Labor)

**Regulatory basis**: Title VII, ADA, FMLA, ADEA, NLRA — varies by allegation

**Required process** (institutional; no single federal timeline):
- Receipt and acknowledgment: within 5 business days
- Initial assessment and routing: within 10 business days
- Investigation: institutional policy typically 30–60 days
- Outcome notification: per institutional policy
- External agency response (if EEOC charge filed): per EEOC timeline (typically 180 days)

---

### Voluntary Self-Disclosure

**Regulatory basis**: Varies by federal program; NIH, FSA, OIG each have disclosure policies

**Process**: Self-disclosures to federal agencies have specific submission requirements that vary by agency and program. Always involve General Counsel and the relevant program officer. Document the disclosure, the agency's acknowledgment, and any resulting audit or review.

---

### Other Compliance Matter

For matters that don't fit the above categories — use this type and define the regulatory basis and required process manually.

---

## Step 2: Read current state

Read the following:
- `investigations/index.md` — case register with all active and closed cases
- `investigations/overview.md` — current investigations summary
- If updating/closing a specific case: read `investigations/active/INV-NNN.md`

---

## Step 3: Produce output by mode

---

### Mode: `new` — Open a New Matter

1. **Gather matter information**:
   - Date of allegation/complaint/discovery
   - Matter type (see taxonomy)
   - Brief description (not identifying details in writing unless necessary)
   - Who is handling: Title IX Coordinator? Research Integrity Officer? HR? External counsel?
   - Is General Counsel notified? Is the VP of Compliance notified?
   - Is there an immediate sequestration, preservation, or notification obligation?

2. **Assign case ID**: read current highest INV-NNN in the index and increment.

3. **Calculate required deadlines**: based on matter type and date of receipt, calculate all required process step deadlines. Flag any already at risk.

4. **Draft the case file**:

```markdown
---
case_id: INV-NNN
type: [matter type]
opened: YYYY-MM-DD
status: inquiry
confidentiality: restricted
complainant_role: [role — no name]
respondent_role: [role — no name]
assigned_to: [role]
oversight: VP of Compliance
regulatory_basis: [regulation]
deadline_at_risk: false
outcome: pending
related_risks: []
related_projects: []
---

# INV-NNN — [Brief Matter Title]

**Type**: [matter type] | **Opened**: YYYY-MM-DD | **Status**: Inquiry | **Confidentiality**: Restricted

## Required Process Steps and Deadlines

| # | Step | Deadline | Status | Completed |
|---|------|----------|--------|-----------|
| 1 | [step] | YYYY-MM-DD | ⏳ Pending | — |
| 2 | [step] | YYYY-MM-DD | ⏳ Pending | — |
...

## 🔴 Immediate Obligations

[List any steps due within 10 business days — these need immediate action]

## Key Dates

| Date | Event |
|------|-------|
| YYYY-MM-DD | Allegation/complaint/discovery date |
| YYYY-MM-DD | Matter opened; INV-NNN assigned |

## Matter Description

[Brief non-identifying description of the matter]

## Assigned Personnel

- **Investigator/Handler**: [role]
- **Decision-Maker**: [role — separate from investigator for Title IX]
- **General Counsel notified**: Yes/No — [date if yes]
- **External counsel engaged**: Yes/No

## Evidence and Documentation

[Links to secure file locations or SharePoint document library — not verbatim documents here]

## Notes

[Chronological notes on developments]
```

5. **Write to `investigations/active/INV-NNN.md`**

6. **Update `investigations/index.md`** — add the new case

7. **Update `planner/tasks.md`** — add deadline reminder tasks for all process steps due in the next 30 days

8. **Log to `log.md`**:
   ```
   ## [YYYY-MM-DD] investigate | Opened INV-NNN
   Type: [matter type]. Assigned to: [role]. Immediate deadlines: [N within 10 days].
   ```

---

### Mode: `update` — Update a Case

Read the existing case file. Apply updates:
- Change status (inquiry → investigation → resolution)
- Add to Key Dates log
- Update process step completion status
- Add notes
- Update risk or project cross-references

Show the proposed changes before writing. Write updated file and update index.

---

### Mode: `close` — Close a Matter

Record:
- Resolution date
- Outcome: substantiated / unsubstantiated / inconclusive / referred / withdrawn
- Resolution summary (brief, non-identifying)
- Any resulting policy changes, training requirements, or remediation tasks

Move file from `investigations/active/` to `investigations/closed/YYYY/INV-NNN.md`. Update index.

Add to `planner/tasks.md` if any remediation actions result from the closure.

---

### Mode: `review` — Active Case Register

```markdown
# Active Compliance Matters — YYYY-MM-DD

## Summary
- Active matters: N
- Matters with deadlines in the next 14 days: N
- Matters at risk of missing a deadline: N

## Active Case Register

| Case ID | Type | Opened | Status | Current Phase | Next Deadline | Days Left | Risk |
|---------|------|--------|--------|--------------|--------------|-----------|------|
| INV-NNN | [type] | YYYY-MM-DD | Investigation | [phase] | YYYY-MM-DD | N | 🔴/🟠/🟡/🟢 |
...

## 🔴 Deadline Alerts (Next 14 Days)

| Case | Step Due | Deadline | Days Remaining |
|------|----------|----------|---------------|
...

## 🟡 Pending Outcome / Resolution

| Case | Status | Opened | Days Open |
|------|--------|--------|----------|
...
```

---

### Mode: `report` — Investigations Status Report

Audience-calibrated output:

**For VP of Compliance** (internal, full detail):
- Full case register with status and deadlines
- Deadline risk assessment
- Staffing and resource needs
- Patterns across matter types

**For Board Compliance Committee** (redacted, high-level):
- Number of active matters by type (no identifying details)
- Any matters with regulatory notification requirements
- Status of matters open > 90 days
- Outcomes closed this quarter

```markdown
---
title: Compliance Investigations Status Report
prepared_for: [VP of Compliance | Board Compliance Committee]
date: YYYY-MM-DD
confidentiality: RESTRICTED — Attorney-Client Privilege May Apply
---

# Compliance Investigations Status Report
## [Date] — CONFIDENTIAL

## Active Matters Summary

| Type | Active | Closed This Quarter | Avg Days Open |
|------|--------|--------------------|----|
| Title IX | N | N | N |
| Research Misconduct | N | N | N |
| HIPAA Breach | N | N | N |
| Employee Complaint | N | N | N |
| Self-Disclosure | N | N | N |
| Other | N | N | N |
| **Total** | **N** | **N** | **N** |

[For VP: full case detail below]
[For Board: aggregate only — individual matter details not included]

## Matters Requiring Leadership Attention

[Cases with regulatory notification obligations, missed deadlines, or escalation risk]

## Closed Matters — This Quarter

[Summary of outcomes without identifying details]
```

---

## Step 4: Offer follow-up actions

After any mode, offer:
1. **Risk register update** — if this matter reveals a risk gap, add to `wiki/compliance/risk-register.md` via `/compliance-brain:risk update`
2. **Policy response** — if the matter reveals a policy gap, offer to track a policy update via `/compliance-brain:policy`
3. **Board report** — if any matter requires board notification, offer to prepare via `/compliance-brain:board-report`
4. **Evidence filing** — offer to link to the evidence sub-brain for documentation management

---

## Quality Rules

- **No individual names in case files** — use roles and functional identifiers only. This protects both the respondent and the institution.
- **Every required step gets a deadline** — if the regulatory deadline is not defined, the investigation SOP defines it. No step is undated.
- **Deadline misses must escalate immediately** — a deadline missed in a Title IX or research misconduct case is a federal compliance failure. Flag missed deadlines as errors, not warnings.
- **Confidentiality is structural** — investigations pages are never linked from wiki or pm pages by case detail. Dashboard references to "N active matters" are permissible.
- **Attorney-client privilege requires care** — if General Counsel is directing the investigation, tag it appropriately. Do not file privileged communications as ordinary Brain pages.
- **Self-disclosures reduce penalties** — when a self-disclosure is the matter type, document the disclosure date and agency acknowledgment carefully. This record protects the institution.
