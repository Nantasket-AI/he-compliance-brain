---
name: reg-monitor
description: Regulatory intelligence and monitoring. Scans the regulatory horizon for new rules, proposed rules, final rules, agency guidance, enforcement actions, and peer institution news that affect the institution's compliance program. Rates the relevance and urgency of each development and produces a regulatory intelligence brief or an action-required summary. Use on a recurring basis to stay ahead of the regulatory environment, before board meetings, and whenever a new regulatory development is flagged.
argument-hint: "<scope> [all|domain:<domain>|agency:<agency>] [mode:scan|brief|action|horizon] — e.g. 'all scan' or 'domain:REG brief' or 'agency:OCR action' or 'all horizon'"
---

# /the-brain:reg-monitor — Regulatory Intelligence & Monitoring

You are performing regulatory intelligence monitoring on behalf of the VP of Compliance. Staying ahead of the regulatory environment is not optional at a federally funded research university and medical school — proposed rules become final rules, agency guidance redefines enforcement expectations, and enforcement actions at peer institutions signal where auditors are looking next. This skill systematically scans the regulatory horizon, rates what matters, and translates it into action.

Every development must be sourced — cite the specific Federal Register notice, agency guidance document, or public enforcement action. Never report regulatory developments without a source you can point to.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which regulatory environment to monitor
  - `all` — full regulatory landscape across all compliance domains
  - `domain:<domain>` — a specific compliance domain (REG, ACCRED, CLINICAL, RESEARCH, PRIVACY, HR, GOV, FINANCE)
  - `agency:<agency>` — a specific agency (OCR, FSA, OIG, NIH, OHRP, AAMC, LCME, ACGME, MSCHE, etc.)

- **Mode**: output format — default to `scan` if not specified:
  - `scan` — broad scan across the regulatory horizon; identify all recent developments by domain
  - `brief` — a formatted regulatory intelligence brief covering the most significant developments
  - `action` — filter to action-required items only: comment periods closing, compliance deadlines approaching, required policy updates
  - `horizon` — forward-looking view: what major regulatory changes are anticipated in the next 6–18 months

---

## Regulatory Sources by Domain

### REG — Regulatory (HIPAA, FERPA, Title IX, Clery, ADA)

| Source | What to Check | URL / Location |
|--------|--------------|---------------|
| HHS OCR — HIPAA | Final rules, proposed rules, enforcement actions, new guidance | hhs.gov/hipaa/for-professionals/index.html |
| Department of Education — FERPA | Regulatory updates, Dear Colleague Letters, FAQ updates | studentprivacy.ed.gov |
| Department of Education — OCR | New proposed/final rules, resolution agreements (enforcement), Dear Colleague Letters | ed.gov/ocr |
| Department of Education — FSA | Clery Act guidance, program review findings, electronic announcements | ifap.ed.gov and fsapartners.ed.gov |
| ADA — DOJ | New regulatory guidance, settlement agreements, technical assistance | ada.gov |
| Federal Register | All proposed and final rules for the above | federalregister.gov |

### ACCRED — Accreditation (LCME, MSCHE, ACGME)

| Source | What to Check |
|--------|--------------|
| LCME | Standards revisions, annotated standards updates, AFI/Condition trend data | lcme.org |
| MSCHE | Standards revisions, policy updates, annual conference announcements | msche.org |
| ACGME | CPR revisions, specialty requirement updates, CLER guidance, milestone updates | acgme.org |
| SACSCOC | Substantive change policy updates, compliance certification guidance | sacscoc.org |

### CLINICAL — Clinical / Patient Care

| Source | What to Check |
|--------|--------------|
| The Joint Commission | New and revised standards, Sentinel Event Alerts, NPSG updates | jointcommission.org |
| CMS | Conditions of Participation updates, Interpretive Guidelines changes | cms.gov |
| DEA | Controlled substance regulation updates, telemedicine rules | dea.gov/drug-information/csa |
| State licensing boards | Rule changes affecting clinical education and faculty licensure | State-specific |

### RESEARCH — Research Compliance

| Source | What to Check |
|--------|--------------|
| HHS OHRP | Common Rule guidance, FWA updates, Dear Colleague Letters | hhs.gov/ohrp |
| NIH | Grants Policy Statement updates, NOT (Notice of Opportunity) documents, new requirements | grants.nih.gov |
| FDA | IND/IDE regulations, GCP guidance updates, 21 CFR updates | fda.gov |
| ORI | Research misconduct policy updates, case summaries | ori.hhs.gov |
| BIS / DDTC | Export control updates, EAR/ITAR changes | bis.doc.gov / pmddtc.state.gov |
| OFAC | New sanctions lists and guidance | sanctionssearch.ofac.treas.gov |
| NSF | Research integrity policy updates | nsf.gov |

### PRIVACY — Privacy & Data Security

| Source | What to Check |
|--------|--------------|
| HHS OCR — HIPAA | Breach notification guidance, cybersecurity guidance, enforcement trends | hhs.gov/hipaa |
| FTC | Data security enforcement actions relevant to education | ftc.gov |
| State AGs | State privacy law updates (many states have new or strengthened laws) | State-specific |
| CISA | Cybersecurity advisories relevant to healthcare and education | cisa.gov |

### HR — Employment

| Source | What to Check |
|--------|--------------|
| EEOC | New guidance, proposed rules, enforcement trends | eeoc.gov |
| DOL | FLSA changes, FMLA guidance, OSHA updates | dol.gov |
| NLRB | Guidance on union organizing, employee classification | nlrb.gov |

---

## Step 2: Search the Brain for prior monitoring notes

### 2a. Wiki sub-brain
- `wiki/compliance/reg-monitor/` — prior regulatory monitoring briefs (if any)
- `wiki/compliance/` — any pages documenting known regulatory changes or anticipated updates

### 2b. PM sub-brain
- `pm/notes/` — notes from past regulatory monitoring; flagged regulatory items
- `pm/projects/` — any active project responding to a regulatory change

### 2c. Planner
- `planner/tasks.md` — any open tasks triggered by prior regulatory monitoring

Note the date of the last monitoring brief and restrict the scan to developments since that date where possible.

---

## Step 3: Scan the regulatory horizon

For each domain in scope, fetch current information from the authoritative sources listed above. Use the WebFetch tool to retrieve pages from regulatory websites.

For each development found, assess:

| Field | What to Record |
|-------|---------------|
| `agency` | Issuing agency or accreditor |
| `type` | Proposed Rule / Final Rule / Guidance / Dear Colleague Letter / Enforcement Action / Accreditor Update / Peer Institution Action |
| `title` | Short title or description of the development |
| `date` | Date issued or published |
| `source_url` | URL or citation |
| `summary` | 2–3 sentence summary of the development |
| `domains_affected` | Which compliance domains this touches |
| `relevance` | 🔴 High / 🟡 Medium / 🟢 Low — how directly does this affect this institution? |
| `action_required` | Yes / No — does this require institutional response? |
| `action_type` | If yes: Policy Update / Procedure Update / Training Update / Comment Submission / Compliance Deadline / Monitoring |
| `action_deadline` | Date by which action must occur (if applicable) |

---

## Step 4: Produce output by mode

---

### Mode: `scan` — Full Regulatory Scan

```markdown
---
title: Regulatory Intelligence Scan
date: YYYY-MM-DD
period_covered: YYYY-MM-DD to YYYY-MM-DD
domains: <all|specific domains>
---

# Regulatory Intelligence Scan
## Period: <start date> to <end date>

## Executive Overview
[3–5 sentences: most significant developments, overall regulatory environment tone, top action items]

---

## Domain-by-Domain Scan

### REG — Regulatory

| # | Agency | Type | Development | Date | Relevance | Action Required |
|---|--------|------|-------------|------|-----------|----------------|
| 1 | OCR | Final Rule | [title] | YYYY-MM-DD | 🔴 High | Yes — Policy update by YYYY-MM-DD |
| 2 | FSA | Dear Colleague | [title] | YYYY-MM-DD | 🟡 Med | No |
...

### ACCRED — Accreditation
...

### RESEARCH — Research Compliance
...

[Continue for each domain]

---

## Action-Required Summary

| # | Development | Agency | Deadline | Action Type | Owner |
|---|-------------|--------|----------|-------------|-------|
| 1 | [title] | [agency] | YYYY-MM-DD | Policy Update | [role] |
...

## Developments to Monitor (No Immediate Action)
[Items in proposed rule or comment period stage that may require action when finalized]
```

---

### Mode: `brief` — Regulatory Intelligence Brief

```markdown
---
title: Regulatory Intelligence Brief
date: YYYY-MM-DD
period: <quarter/month>
audience: VP of Compliance | Board Compliance Committee
---

# Regulatory Intelligence Brief
## <Institution> — <Period>

## Overview
[2–3 sentence executive summary: what is moving in the regulatory environment and what demands attention]

---

## Significant Developments

### 1. <Development Title>
- **Agency**: [name]
- **Type**: [Final Rule / Guidance / Enforcement Action / etc.]
- **Date**: [date]
- **Source**: [citation and URL]
- **What It Says**: [plain-language 2–3 sentence description]
- **Impact on This Institution**: [what specifically changes for us — cite affected programs, policies, or populations]
- **Action Required**: [specific action, owner, deadline — or "None at this time"]
- **Risk if No Action**: [consequence of ignoring]

### 2. <Next Development>
...

---

## Pending Regulatory Developments (Watch List)

| Development | Agency | Stage | Expected | Likely Impact |
|-------------|--------|-------|----------|--------------|
| [proposed rule title] | [agency] | Proposed Rule — comment period closes YYYY-MM-DD | Final rule expected YYYY | [impact assessment] |
...

## Enforcement Environment

[2–3 sentences on enforcement trends: where agencies are focusing audits and enforcement actions, informed by public enforcement actions and Dear Colleague Letters from the period]

**Peer Institution Actions**: [any notable enforcement actions at comparable institutions that signal enforcement priorities]
```

---

### Mode: `action` — Action-Required Items Only

```markdown
---
title: Regulatory Action Items
date: YYYY-MM-DD
---

# Compliance Action Items — Regulatory Developments

Items requiring institutional response, sorted by deadline.

## 🔴 Immediate — Due Within 30 Days

| Development | Source | Deadline | Required Action | Owner | Status |
|-------------|--------|----------|----------------|-------|--------|
| [title] | [agency + URL] | YYYY-MM-DD | [specific action] | [role] | Not Started |
...

## 🟠 Due Within 90 Days

| Development | Source | Deadline | Required Action | Owner |
...

## 🟡 Due Within 6 Months

| Development | Source | Deadline | Required Action | Owner |
...

## Comment Periods Open

| Proposed Rule | Agency | Comment Deadline | Recommendation |
|--------------|--------|-----------------|---------------|
| [title] | [agency] | YYYY-MM-DD | Submit comment / Monitor / No action |
[Note: If submitting a comment is recommended, flag for General Counsel and leadership; formal comments on proposed rules typically require institutional review and approval]
```

---

### Mode: `horizon` — Forward-Looking (6–18 Months)

```markdown
---
title: Regulatory Horizon — 6–18 Month Outlook
date: YYYY-MM-DD
---

# Regulatory Horizon

Anticipated regulatory developments in the next 6–18 months. Based on: current proposed rules, administration priorities, enforcement trends, and accreditor scheduled review cycles.

## High Confidence — Expected Developments

| Development | Agency | Expected | Likely Impact | Prepare Now By |
|-------------|--------|----------|--------------|----------------|
| [pending final rule title] | [agency] | Finalization: YYYY-QN | [impact] | [what to do now] |
...

## Accreditor Cycles — Known Dates

| Accreditor | Event | Expected Date | Prep Lead Time Needed |
|-----------|-------|-------------|----------------------|
| LCME | [interim report / site visit] | YYYY-MM | 12 months minimum |
| MSCHE | [decennial review / monitoring] | YYYY-MM | 18 months minimum |
| ACGME | [CLER visit] | YYYY-MM | 6 months minimum |

## Watch List — Uncertain Timing

| Development | Agency | Status | Notes |
|-------------|--------|--------|-------|
| [proposed rule or anticipated guidance] | [agency] | [Proposed / Expected / Rumored] | [context] |

## Recommended Proactive Steps
1. [action to take now to prepare for an anticipated regulatory change]
2. ...
```

---

## Step 5: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write the brief to `wiki/compliance/reg-monitor/YYYY-MM-DD-brief.md`
2. **Update risk register** — for any High-relevance development, offer to add or update a risk entry via `/the-brain:risk update`
3. **Create action tasks** — for any action-required items, add to `planner/tasks.md` with deadlines and owners
4. **Policy impact** — for any development that requires a policy update, offer to run `/the-brain:policy` to draft the update
5. **Board brief** — if preparing for a board meeting, roll this into the board compliance report via `/the-brain:board-report`
6. **Comment submission** — if a comment period is open for a significant proposed rule, flag for General Counsel review

---

## Step 6: Update the monitoring log

After completing a scan, append to `log.md`:

```
## [YYYY-MM-DD] reg-monitor | <mode> | <domains>
Period: <start> to <end>. Developments found: N total (<N High, N Medium, N Low relevance). Action items: N. Filed: [[wiki/compliance/reg-monitor/YYYY-MM-DD-brief]].
```

---

## Quality Rules

- **Source everything** — a regulatory development that cannot be linked to a primary source (Federal Register notice, agency website, public enforcement letter) should not be reported. No paraphrasing from memory.
- **Distinguish proposed from final** — a proposed rule does not yet require policy changes; a final rule does. Always label the status clearly and note the effective date for final rules.
- **Enforcement actions at peer institutions are intelligence** — a public enforcement action at a comparable institution tells you what auditors are looking for right now; treat High-priority peer actions as pre-audit signals.
- **Comment periods are time-sensitive** — if the institution intends to submit comments on a proposed rule, the comment period closes on a specific date; flag with at least 30 days' lead time.
- **Accreditor guidance supplements regulations** — accreditor Dear Colleague Letters and FAQ updates often reinterpret existing standards; treat these with the same weight as new standards.
- **The regulatory environment changes fast** — this skill should be run at minimum quarterly; monthly is better for high-change domains (HIPAA privacy reform, Title IX, ACGME CPR revisions are all in active flux as of 2025–2026).
