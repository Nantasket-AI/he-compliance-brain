---
name: acgme
description: ACGME GME compliance gap analysis. Covers the Sponsoring Institution requirements, Common Program Requirements, specialty-specific requirements, CLER visit readiness, and the Annual Program Evaluation cycle. Maps evidence across the full GME portfolio or a specific program. Use when preparing for a CLER visit, responding to a program citation, conducting an Annual Institutional Review (AIR), or auditing GME compliance across the institution.
argument-hint: "<scope> [institution|program:<specialty>|all] [mode:gap|cler|air|citation|priority] — e.g. 'institution gap' or 'program:internal-medicine cler' or 'all priority' or 'program:surgery citation'"
---

# /the-brain:acgme — ACGME GME Compliance Gap Analysis

You are performing an ACGME accreditation compliance analysis on behalf of the VP of Compliance. GME compliance operates at two levels: the **Sponsoring Institution** (institutional requirements applying to all programs) and individual **Accredited Programs** (Common Program Requirements plus specialty-specific requirements). Both must be evidenced and both are assessed by ACGME and during CLER visits.

Every finding must cite the exact ACGME requirement source (Institutional Requirements, Common Program Requirements section, or specialty-specific) and the Brain page or connected-system document that supports or fails to support it.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**:
  - `institution` — Sponsoring Institution requirements only (GMEC, DIO, institutional policies)
  - `program:<specialty>` — Common Program Requirements + specialty-specific for one program
  - `all` — institutional requirements plus all programs tracked in the Brain

- **Mode**: output format — default to `gap` if not specified:
  - `gap` — requirement-by-requirement gap analysis; scored Met / Partial / Not Evidenced
  - `cler` — CLER visit readiness: maps evidence to the 6 CLER Focus Areas
  - `air` — Annual Institutional Review: produces an AIR-structured summary of program compliance and institutional performance
  - `citation` — structured response to a specific ACGME citation or "Areas for Improvement"
  - `priority` — all gaps sorted by accreditation risk with recommended actions

---

## ACGME Requirements Reference

### Sponsoring Institution Requirements (SI)

| Area | Key Requirements |
|------|-----------------|
| **SI-1: GMEC** | Graduate Medical Education Committee functioning; DIO with authority; program director oversight |
| **SI-2: DIO** | Designated Institutional Official appointed; sufficient authority; reports to CEO/Provost |
| **SI-3: Program Director oversight** | GMEC reviews and approves all program directors; monitors performance |
| **SI-4: Resident/Fellow complement** | Total and per-program complement approved by GMEC; within ACGME-approved limits |
| **SI-5: Resources** | Institutional resources (financial, faculty, facilities) support all programs |
| **SI-6: Policies** | Written policies: duty hours, supervision, professionalism, grievance, leave, moonlighting, fatigue mitigation |
| **SI-7: Annual Institutional Review (AIR)** | GMEC conducts annual review of all programs; documents findings; drives improvement |
| **SI-8: Accreditation status** | GMEC monitors all program accreditation statuses; responsive to citations |
| **SI-9: Resident/fellow wellbeing** | Institutional commitment to wellbeing; resources available; culture monitored |
| **SI-10: Diversity, equity, inclusion** | Institutional efforts to recruit/retain diverse residents and faculty |

### Common Program Requirements (CPR) — Key Sections

| Section | Title | Key Requirements |
|---------|-------|-----------------|
| **CPR I** | Oversight | Program director qualifications; program leadership team; faculty |
| **CPR II** | Resident/Fellow Appointments | Selection criteria; contracts; due process for dismissal |
| **CPR III** | Fellow/Resident Supervision | Supervision framework; levels of supervision; oversight of progressive independence |
| **CPR IV** | Professionalism | Professional conduct policies; duty to report; safety culture |
| **CPR V** | Wellbeing | Wellbeing resources; duty hours; fatigue mitigation; access to mental health |
| **CPR VI** | The Learning and Working Environment | Patient safety reporting; quality improvement participation; handoffs |
| **CPR VII** | Educational Program | Goals and objectives mapped to milestones; didactics; simulation |
| **CPR VIII** | Evaluation | Resident/fellow evaluation using milestones; faculty evaluation; program evaluation |

### CLER Focus Areas (Clinical Learning Environment Review)

| Focus Area | What CLER Evaluates |
|-----------|---------------------|
| **1. Patient Safety** | Resident/fellow participation in safety event reporting; just culture; near-miss reporting |
| **2. Health Care Quality** | Resident/fellow engagement in QI projects; data-driven improvement |
| **3. Care Transitions** | Handoff policies; training; compliance monitoring |
| **4. Supervision** | Faculty supervision practices; progressive independence documentation |
| **5. Professionalism** | Institutional culture; reporting concerns without fear of retaliation |
| **6. Wellbeing** | Prevalence of burnout; institutional support; access to help without stigma |

---

## Step 2: Search the Brain for ACGME evidence

### 2a. Wiki sub-brain
- `wiki/compliance/` — ACGME wiki pages, institutional GME compliance notes
- `wiki/entities/` — GMEC structure, DIO office, program director roster, affiliated hospitals
- `wiki/concepts/` — milestone frameworks, supervision levels, duty hour rules

### 2b. PM sub-brain
- `pm/projects/` — ACGME self-study projects, CLER preparation, program citation responses
- `pm/meetings/` — GMEC meeting minutes (critical: must document AIR and program reviews), DIO briefings
- `pm/notes/` — ACGME correspondence, WebADS data notes, program director reports
- `pm/reports/` — prior AIR reports, CLER summaries, program accreditation letters, Annual Program Evaluation (APE) reports

### 2c. Planner sub-brain
- `planner/tasks.md` — open GME compliance action items
- `planner/dashboard.md` — CLER or AIR deadlines

### 2d. Raw sources
- `raw/` — ACGME action letters, CLER summary reports, WebADS milestone data exports

For every document found:
- Map to the specific **SI requirement or CPR section** it addresses
- Note if it provides **policy evidence** (the rule exists) vs. **performance evidence** (it is being followed)
- Flag anything **older than 12 months** as potentially stale for GME purposes (annual cycles are the standard)

---

## Step 3: Search connected systems

### 3a. SharePoint
- GMEC meeting minutes (all months — must show quorum, AIR conduct, program director approvals)
- All program letters of agreement (PLAs) with affiliated sites
- Duty hour logs or attestation records
- Supervision policies and program-specific supervision tables
- Moonlighting policies and individual moonlighting attestations
- Resident/fellow contracts and due process policies
- Wellbeing program documentation and utilization data
- Faculty development records
- Residency/fellowship handbooks

### 3b. Connectors
- **Outlook**: ACGME correspondence, WebADS notifications, CLER scheduling communications
- **Teams**: GMEC working channels, DIO communications
- **Jira**: open citation response tickets or program improvement action items

### 3c. Primary ACGME sources (web)
- **Sponsoring Institution Requirements**: acgme.org/globalassets/pfassets/publicationsbooks/sponsoring-institutions_acgme-institutional-requirements.pdf
- **Common Program Requirements**: acgme.org/what-we-do/accreditation/common-program-requirements/
- **Specialty-specific requirements**: acgme.org/what-we-do/accreditation/specialty/
- **CLER Pathways to Excellence**: acgme.org/what-we-do/initiatives/cler/
- **Milestones by specialty**: acgme.org/what-we-do/milestones/

**Citation format**: `[ACGME, SI/CPR/CLER reference, Retrieved YYYY-MM-DD]`

---

## Step 4: Score each requirement

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Met** | 🟢 | Current (≤12 months), accessible evidence for both policy and performance |
| **Partial** | 🟡 | Incomplete, stale, or policy-only evidence |
| **Not Evidenced** | 🔴 | No evidence in Brain or connected systems |

**Accreditation risk**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | Not Evidenced for a CLER Focus Area or SI requirement; existing citation not yet resolved |
| 🟠 High | Not Evidenced for a CPR section; CLER Focus Area partially evidenced |
| 🟡 Medium | Partial evidence; policy without performance data; stale by more than 12 months |
| 🟢 Low | Met with current, multi-source evidence |

**Historically scrutinized areas** (flag these explicitly):
- Duty hours: attestation completeness and actual compliance
- Supervision: documentation of progressive independence decisions
- Wellbeing: evidence that resources exist AND residents/fellows actually access them without stigma
- GMEC minutes: must reflect active oversight, not rubber-stamp meetings
- Milestone assessments: completeness and faculty calibration

---

## Step 5: Produce output by mode

---

### Mode: `gap`

```markdown
---
title: ACGME Gap Analysis — <Scope>
scope: <institution|program|all>
date: YYYY-MM-DD
---

# ACGME Gap Analysis: <Scope>

## Summary
- Requirements Assessed: N | Met 🟢: N | Partial 🟡: N | Not Evidenced 🔴: N
- Programs Tracked in Brain: N
- Programs with Open Citations: [list]
- Next CLER Visit (if known): YYYY-MM-DD
- Next AIR Due: YYYY-MM-DD

---

## Sponsoring Institution Requirements

| Requirement | Evidence Found | Status | Risk |
|-------------|---------------|--------|------|
| SI-1: GMEC | [[pm/meetings/gmec-...]] | 🟢 Met | 🟢 Low |
...

---

## Common Program Requirements — <Program Name>

| CPR Section | Requirement Summary | Evidence | Status | Risk |
|-------------|---------------------|---------|--------|------|
| CPR I | Program director qualifications | [evidence] | 🟡 | 🟡 |
...
```

---

### Mode: `cler`

```markdown
---
title: CLER Visit Readiness — <Institution>
date: YYYY-MM-DD
---

# CLER Visit Readiness Assessment

## CLER Focus Area Scores
| Focus Area | Evidence on Hand | Status | Risk |
|-----------|-----------------|--------|------|
| 1. Patient Safety | [evidence] | 🟢/🟡/🔴 | |
| 2. Health Care Quality | [evidence] | | |
| 3. Care Transitions | [evidence] | | |
| 4. Supervision | [evidence] | | |
| 5. Professionalism | [evidence] | | |
| 6. Wellbeing | [evidence] | | |

## What CLER Site Visitors Will Ask
[For each Focus Area: the 2–3 questions/scenarios CLER visitors typically probe, and how available evidence addresses them]

## Gaps to Address Before CLER Visit
[Priority-sorted list]
```

---

### Mode: `citation`

```markdown
---
title: ACGME Citation Response — <Program> — <Citation Reference>
citation: [CPR section or SI requirement cited]
date: YYYY-MM-DD
---

# Citation Response: <Citation Text>

## Citation Summary
[Verbatim or paraphrased citation language]

## Root Cause Analysis
[What gap in policy, performance, or documentation led to this finding]

## Current State
[What evidence is now available / what has changed since the citation]

## Corrective Action Plan

| Action | Owner | Due Date | Evidence of Completion |
|--------|-------|----------|----------------------|
| 1. [action] | [role] | YYYY-MM-DD | [artifact] |
...

## Monitoring Plan
[How the institution will monitor and sustain compliance going forward]

## Sources
[Citations]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write to `wiki/compliance/acgme-gap-YYYY-MM-DD.md`
2. **Create GME project** — scaffold `pm/projects/acgme-compliance/` with gaps as issues
3. **Push tasks** — add Critical/High items to `planner/tasks.md`
4. **CLER prep** — offer to run `cler` mode if a CLER visit is approaching

---

## Quality Rules

- GME compliance evidence must be current within **12 months** — annual cycles are the ACGME standard.
- GMEC minutes are the single most important evidence artifact for institutional requirements — flag if any months are missing.
- Never conflate "policy exists" with "policy is followed" — ACGME citations routinely stem from unenforced policies.
- For any program with an existing citation, always elevate its gaps to 🔴 Critical regardless of evidence status.
- Duty hour violations carry serious reputational and accreditation risk — any gap here is at least 🟠 High.
