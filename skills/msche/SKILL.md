---
name: msche
description: MSCHE accreditation gap analysis. Compares Middle States Commission on Higher Education (MSCHE) Standards and Requirements of Affiliation against documentation stored in the Brain. Identifies evidential gaps, missing policies, and site-visit risk. Use when preparing for a decennial evaluation, periodic review, substantive change report, or any MSCHE compliance checkpoint.
argument-hint: "<scope> [standard:<1-7>|roa|all] [mode:gap|inventory|brief|priority] — e.g. 'Standard 5 gap' or 'all gap' or 'roa inventory' or 'Standard 3 priority'"
---

# /the-brain:msche — MSCHE Accreditation Gap Analysis

You are performing a Middle States Commission on Higher Education (MSCHE) gap analysis on behalf of the VP of Compliance. Your role is to map every applicable MSCHE requirement against evidence held in the Brain and connected systems, then surface every gap clearly so the institution can act before a site visit or periodic review.

Every finding must be traceable: cite the exact MSCHE Standard or Requirement of Affiliation element, and cite the Brain page (or absence thereof) that supports or fails to support it.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which standards or requirements to assess — default to `all` if not specified
  - `standard:<N>` — a single MSCHE Standard (1–7)
  - `roa` — the 14 Requirements of Affiliation only
  - `all` — all 7 Standards plus all 14 Requirements of Affiliation

- **Mode**: the output format — default to `gap` if not specified:
  - `gap` — full gap analysis table per standard/element; flags each element as Met / Partial / Not Evidenced
  - `inventory` — flat list of every Brain document mapped to the MSCHE element it supports
  - `brief` — executive-level compliance summary for a single standard; cite top risks
  - `priority` — gap list sorted by site-visit risk (High → Medium → Low), with recommended next actions

---

## MSCHE Standards Reference

### Requirements of Affiliation (ROA) — 14 Requirements

The ROA are threshold eligibility conditions. Any "Not Met" finding is a compliance emergency.

| # | Requirement | What must be evidenced |
|---|-------------|----------------------|
| ROA-1 | Mission statement | Published, Board-approved mission statement |
| ROA-2 | Authority to award degrees | Legal authorization in each state where operating; degree-granting authority |
| ROA-3 | Operational continuity | History of financial and operational stability |
| ROA-4 | Governance | Functioning governing board; conflict-of-interest policy |
| ROA-5 | Chief executive officer | CEO appointed by and accountable to governing board |
| ROA-6 | Financial resources | Resources sufficient to fulfill mission; audited financial statements |
| ROA-7 | Student support services | Academic and student support services for enrolled students |
| ROA-8 | Faculty | Core faculty sufficient to deliver curriculum and fulfill mission |
| ROA-9 | Curricula | Curricula that lead to stated student learning outcomes |
| ROA-10 | Student learning outcomes | Assessment of student achievement of learning outcomes |
| ROA-11 | Student records | Secure and retrievable student records |
| ROA-12 | Catalogs and publications | Accurate and current catalogs, handbooks, and public disclosures |
| ROA-13 | Articulation | Policies for acceptance of transfer credits |
| ROA-14 | MSCHE policies compliance | Compliance with all MSCHE policies, including substantive change |

### Standard 1 — Mission and Goals
Key elements to evidence:
- 1.1 Clearly defined mission statement; regularly reviewed and approved by governing board
- 1.2 Goals derived from mission; specific, measurable, achievable, and time-bound
- 1.3 Mission and goals guide institutional planning, resource allocation, and assessment
- 1.4 Mission is published and communicated to all stakeholders

### Standard 2 — Ethics and Integrity
Key elements to evidence:
- 2.1 Commitment to freedom of inquiry, intellectual honesty, and respect for persons
- 2.2 Policies that protect against bias, discrimination, and conflicts of interest
- 2.3 Fair and impartial processes for grievance, discipline, and appeal
- 2.4 Honest representation in all public disclosures, advertising, and recruiting
- 2.5 Compliance with applicable laws and regulations (Title IX, ADA, FERPA, Clery Act, etc.)
- 2.6 Regular review of ethical standards and institutional integrity commitments

### Standard 3 — Design and Delivery of the Student Learning Experience
Key elements to evidence:
- 3.1 Clearly articulated and published student learning outcomes (SLOs) for each program
- 3.2 Curricula designed and delivered by qualified faculty; appropriate credits and contact hours
- 3.3 Active and reflective learning; student engagement
- 3.4 Academic rigor appropriate to credential level
- 3.5 General education requirements and demonstrable integration with program requirements
- 3.6 Policies governing awarding of transfer credits, experiential learning credit, and prior learning assessment
- 3.7 Technology and distance/hybrid education delivery meets same standards as in-person
- 3.8 Academic advising

### Standard 4 — Support of the Student Experience
Key elements to evidence:
- 4.1 Recruitment and admissions consistent with mission; fair and transparent processes
- 4.2 Orientation programs
- 4.3 Financial aid policies and counseling; consumer information disclosures (Title IV)
- 4.4 Career services and preparation for post-graduation outcomes
- 4.5 Support services for diverse populations (disability services, international students, veterans, etc.)
- 4.6 Co-curricular programs consistent with mission
- 4.7 Health and wellness services
- 4.8 Safe and secure campus environment (Clery Act, Title IX protections)
- 4.9 Student complaints/grievance procedures; accessible and widely publicized

### Standard 5 — Educational Effectiveness Assessment
Key elements to evidence:
- 5.1 Documented, systematic, institution-wide assessment process for student learning
- 5.2 Defined student learning outcomes at course, program, and institutional levels
- 5.3 Assessment data collected, analyzed, and used to improve learning
- 5.4 Assessment results shared broadly with the institution
- 5.5 Assessment of general education outcomes
- 5.6 Cycle of continuous improvement driven by evidence; closing-the-loop documentation
- 5.7 Institutional research capacity to support assessment

### Standard 6 — Planning, Resources, and Institutional Improvement
Key elements to evidence:
- 6.1 Strategic and operational planning processes; documented plans aligned to mission
- 6.2 Allocation of resources in support of plans and mission
- 6.3 Audited financial statements; financial planning and sustainability
- 6.4 Physical and technology infrastructure supports mission
- 6.5 Human resources policies and sufficient staffing
- 6.6 Evidence of institutional improvement derived from planning processes
- 6.7 Ongoing assessment of planning effectiveness; closing-the-loop

### Standard 7 — Governance, Leadership, and Administration
Key elements to evidence:
- 7.1 Governing board: independent, mission-driven; policies for conflict of interest, board self-assessment
- 7.2 Board exercises fiduciary responsibility and ensures institutional integrity
- 7.3 CEO provides leadership consistent with mission; clearly defined administrative structure
- 7.4 Academic governance: faculty role in curriculum, academic policy, and standards
- 7.5 Administration policies and processes are clearly defined, consistently applied, and reviewed
- 7.6 Shared governance policies and structures; faculty, staff, and student participation

---

## Step 2: Search the Brain for accreditation evidence

Navigate the Brain systematically for MSCHE-relevant documentation. Follow the top-down tree search from CLAUDE.md.

### 2a. Wiki sub-brain — Standing knowledge
- `wiki/compliance/` — MSCHE wiki pages, accreditation notes, self-study drafts
- `wiki/concepts/` — institutional definitions (mission, SLOs, governance structures)
- `wiki/entities/` — governing board, administrative offices, academic units

### 2b. PM sub-brain — Active work and institutional memory
- `pm/projects/` — accreditation project folder(s); self-study project; any substantive change filings
- `pm/meetings/` — governance meetings (Board, Academic Senate, Curriculum Committee), assessment committee meetings, compliance committee meetings
- `pm/notes/` — any MSCHE-related briefings, preparation notes, consultant notes
- `pm/reports/` — prior self-study documents, annual MSCHE reporting, monitoring reports, last evaluation team report

### 2c. Planner sub-brain — Active tasks and deadlines
- `planner/dashboard.md` — current MSCHE-related priorities
- `planner/tasks.md` — open accreditation action items

### 2d. Raw sources
- `raw/` — any MSCHE correspondence, evaluation team reports, action letters, substantive change approvals stored as raw files

For every Brain document found:
- Record the **specific element(s)** it provides evidence for
- Note the **document type** (policy, meeting minutes, assessment report, financial audit, etc.)
- Note the **last-updated date** — flag documents older than 2 years as **Stale** for accreditation purposes
- Note documents that partially address an element vs. fully address it

---

## Step 3: Search connected systems for additional evidence

Supplement Brain knowledge with live sources before concluding gaps exist.

### 3a. SharePoint
Search SharePoint for accreditation-critical documents:
- Board of Trustees meeting minutes (governance evidence for Standards 2 and 7)
- Strategic plan and planning documents (Standard 6)
- Audited financial statements (Standard 6, ROA-6)
- Student handbook, academic catalog (Standards 3, 4, ROA-12)
- Program assessment reports and SLO documentation (Standards 3, 5)
- Accreditation self-study draft or prior self-study
- MSCHE correspondence and action letters
- Substantive change notifications and approvals (ROA-14)
- Faculty credentialing records summary (Standard 3, ROA-8)
- Conflict of interest disclosures and policies (Standards 2, 7)

### 3b. Connectors
- **Outlook**: search for recent MSCHE correspondence, evaluator communications, liaison updates
- **Teams**: compliance committee or accreditation task force channel discussions
- **Jira/project management**: open accreditation preparation tickets
- **Confluence**: any living accreditation runbooks or preparation wikis

### 3c. Primary MSCHE sources (web)
Where Brain and SharePoint evidence is absent or ambiguous, consult MSCHE primary sources:
- **Accreditation Standards**: msche.org/standards-and-practices/standards-for-accreditation/ — cite specific Standard and element number
- **Requirements of Affiliation**: msche.org/standards-and-practices/requirements-of-affiliation/
- **MSCHE Policies and Procedures**: msche.org/standards-and-practices/policies-and-procedures/
- **Substantive Change Policy**: msche.org/standards-and-practices/substantive-change/
- **Annual Institutional Update guidance**: msche.org/accreditation/maintaining-accreditation/

**Citation format**: `[MSCHE, Standard/ROA reference, Retrieved YYYY-MM-DD]`

---

## Step 4: Score each element

For every MSCHE element assessed, assign one of three evidence statuses:

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Met** | 🟢 | Clear, current (≤2 years), and accessible evidence exists in the Brain or connected systems |
| **Partial** | 🟡 | Evidence exists but is incomplete, stale (>2 years), not formally approved, or not publicly accessible |
| **Not Evidenced** | 🔴 | No evidence found in Brain or connected systems; gap confirmed |

Assign a **site-visit risk level** based on the status and the criticality of the element:

| Risk | When to assign |
|------|---------------|
| 🔴 **Critical** | Any ROA element Not Evidenced; any Standard element that evaluators are known to probe heavily, Not Evidenced |
| 🟠 **High** | Standard element Not Evidenced; any ROA element Partial |
| 🟡 **Medium** | Standard element Partial; Met evidence that is stale or relies on a single document |
| 🟢 **Low** | Met with current, multi-source evidence |

---

## Step 5: Produce output by mode

---

### Mode: `gap` — Full Gap Analysis

```markdown
---
title: MSCHE Gap Analysis — <Scope>
scope: <standard number(s) or ROA or all>
date: YYYY-MM-DD
analyst: VP of Compliance / AI-assisted
---

# MSCHE Gap Analysis: <Scope>

## Summary
- **Elements Assessed**: N
- **Met (🟢)**: N
- **Partial (🟡)**: N
- **Not Evidenced (🔴)**: N
- **Critical / High Risk Items**: N
- **Next Review Date Recommended**: YYYY-MM-DD

---

## Requirements of Affiliation  *(include if scope = roa or all)*

| # | Requirement | Evidence Found | Status | Risk |
|---|-------------|---------------|--------|------|
| ROA-1 | Mission statement | [[wiki/compliance/mission-statement]] | 🟢 Met | 🟢 Low |
| ROA-2 | Degree-granting authority | *Not found in Brain* | 🔴 Not Evidenced | 🔴 Critical |
...

---

## Standard N — <Name>  *(one section per standard in scope)*

| Element | Requirement Summary | Evidence Found | Status | Risk |
|---------|---------------------|---------------|--------|------|
| N.1 | [plain-language summary] | [Brain page or "Not found"] | 🟢/🟡/🔴 | 🟢/🟡/🟠/🔴 |
...

**Standard N Risk Summary**: Overall risk — Critical / High / Medium / Low
**Key Gaps in Standard N**:
1. [gap description] — [recommended action]
2. ...

---

## Sources
1. [MSCHE, Standard/ROA reference, Retrieved YYYY-MM-DD]
2. [Brain page citation]
```

---

### Mode: `inventory` — Evidence Inventory

```markdown
---
title: MSCHE Evidence Inventory
date: YYYY-MM-DD
---

# MSCHE Evidence Inventory

| Document | Location | Type | Last Updated | MSCHE Elements Supported | Status |
|----------|----------|------|-------------|--------------------------|--------|
| [doc title] | [[Brain page or SharePoint path]] | [Policy/Minutes/Report/etc.] | YYYY-MM-DD | [Standard N.N, ROA-N] | 🟢/🟡/🔴 |
...

## Coverage Summary

| Standard / ROA | # Elements | # Evidenced | # Partial | # Gaps |
|----------------|-----------|------------|-----------|--------|
| ROA | 14 | N | N | N |
| Standard 1 | 4 | N | N | N |
...

## Documents Needed (not yet in Brain or SharePoint)
1. [document description] — covers [elements] — [recommended source or owner]
```

---

### Mode: `brief` — Executive Summary (single standard)

```markdown
---
title: MSCHE Executive Brief — Standard <N>: <Name>
standard: <N>
date: YYYY-MM-DD
---

# MSCHE Executive Brief: Standard <N>

## Standard Overview
[Plain-language description of what this standard requires and why it matters for site visits]

## Overall Status: <Met / Partial / At Risk>

## Evidence on Hand
[Bulleted list of documents in the Brain or connected systems that support this standard, with status]

## Critical Gaps
[Numbered list of elements with no evidence — most critical first]

## Risk Flags
- 🔴 **Critical**: [description and implication for site visit]
- 🟠 **High**: [description]
- 🟡 **Medium**: [description]

## Recommended Immediate Actions
1. [action] — Owner: [role] — Due: [timeframe]
2. ...

## Sources
[Citations]
```

---

### Mode: `priority` — Site-Visit Priority Action List

```markdown
---
title: MSCHE Site-Visit Priority Actions
scope: <scope>
date: YYYY-MM-DD
---

# MSCHE Site-Visit Priority Actions

Sorted by site-visit risk. Address Critical items before any evaluator contact.

## 🔴 Critical — Must resolve before site visit

| # | Element | Gap Description | Recommended Action | Suggested Owner | Target Date |
|---|---------|-----------------|-------------------|-----------------|------------|
| 1 | [ROA or Standard element] | [what is missing] | [specific action] | [role/office] | [date] |
...

## 🟠 High — Resolve before self-study submission

| # | Element | Gap | Action | Owner | Target |
...

## 🟡 Medium — Resolve before desk review

| # | Element | Gap | Action | Owner | Target |
...

## 🟢 Low — Address in normal cycle

| # | Element | Note | Action |
...

## Summary Counts
- 🔴 Critical: N items
- 🟠 High: N items
- 🟡 Medium: N items
- 🟢 Low: N items

## Suggested Next Steps
1. [immediate next step for VP of Compliance]
2. ...
```

---

## Step 6: Offer to save findings

After producing any output, offer these follow-up actions:

1. **Save to Brain** — write the gap analysis or inventory to `wiki/compliance/msche-gap-YYYY-MM-DD.md` and index it under `wiki/compliance/index.md`
2. **Create a project** — if no active MSCHE accreditation project exists in `pm/projects/`, offer to scaffold one with the gap findings as the initial issue list
3. **Create tasks** — offer to add each Critical and High item as an open task in `planner/tasks.md` with a suggested due date
4. **Drill down** — offer to run a `brief` for any Standard where gaps were found

---

## Quality Rules

- **Never fabricate evidence.** If a document was not found, record "Not found in Brain or connected systems" — do not assume it exists.
- **Never assume compliance.** Absence of evidence in the Brain is not evidence of absence in the institution — but it IS a gap for site-visit purposes, because evaluators can only review what is accessible and documented.
- **Always cite the exact MSCHE element** (e.g., Standard 5.3, ROA-10) alongside every finding.
- **Always date the analysis** — accreditation evidence has a shelf life; flag anything that will be stale at the projected evaluation date.
- **Flag substantive change triggers** — if the Brain reveals any new programs, locations, modalities, or organizational changes, note them as potential substantive change obligations under MSCHE policy.
