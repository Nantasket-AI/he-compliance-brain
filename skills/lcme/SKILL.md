---
name: lcme
description: LCME accreditation gap analysis for MD programs. Maps all 12 LCME Standards and their ~93 Elements against documentation in the Brain to identify evidential gaps, stale evidence, and site-visit risk. Use when preparing for a full accreditation review, interim report, DCI submission, or any LCME compliance checkpoint.
argument-hint: "<scope> [standard:<1-12>|all] [mode:gap|inventory|brief|priority|dci] — e.g. 'standard:6 gap' or 'all priority' or 'standard:9 brief' or 'all dci'"
---

# /the-brain:lcme — LCME Accreditation Gap Analysis

You are performing a Liaison Committee on Medical Education (LCME) gap analysis on behalf of the VP of Compliance. Your role is to map every applicable LCME Standard Element against evidence held in the Brain and connected systems, then surface every gap so the institution can act before the Data Collection Instrument (DCI) is due, an interim report is filed, or a site visit team arrives.

Every finding must be traceable: cite the exact LCME Standard and Element number, and cite the Brain page (or its absence) that supports or fails to support it.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which standards to assess — default to `all` if not specified
  - `standard:<N>` — single Standard (1–12)
  - `all` — all 12 Standards and all Elements

- **Mode**: output format — default to `gap` if not specified:
  - `gap` — element-by-element gap analysis table; each Element scored Met / Partial / Not Evidenced
  - `inventory` — flat list of every Brain document mapped to the Element(s) it supports
  - `brief` — executive summary for a single Standard with top risk flags
  - `priority` — all gaps sorted by site-visit risk (Critical → High → Medium → Low) with recommended actions
  - `dci` — DCI-oriented: for each Element, draft a summary of available evidence that could populate the DCI narrative, plus flag fields with no supporting data

---

## LCME Standards Reference (2021–2022 Standards)

### Standard 1 — Mission, Planning, Organization, and Integrity
- **1.1** Mission statement: clearly written; reviewed/approved by governing authority
- **1.2** Strategic planning process: inclusive; mission-aligned; documents goals, timelines, outcomes
- **1.3** Organizational chart: updated; clear lines of authority and accountability
- **1.4** Affiliation agreements: current, signed agreements with all clinical training sites
- **1.5** Institutional integrity: honest representation in advertising, recruiting, and public disclosures
- **1.6** LCME policies compliance: prompt reporting of substantive changes; no deceptive practices

### Standard 2 — Leadership and Administration
- **2.1** Dean: faculty member; authority commensurate with responsibility; reports to institutional CEO or Provost
- **2.2** Administrative structure: supports all functions of the medical education program
- **2.3** Faculty governance: faculty participate meaningfully in academic and curricular policy
- **2.4** Conflict of interest policies: cover faculty and administrators; enforced with disclosed management plans

### Standard 3 — Academic and Learning Environments
- **3.1** Medical education building and facilities: adequate for program delivery
- **3.2** Clinical learning environments: sufficient volume, variety, and supervisory quality
- **3.3** Educational resources: library, simulation, technology infrastructure
- **3.4** Learning climate: respectful; free from mistreatment and discrimination; monitored and enforced
- **3.5** Professionalism standards: explicitly taught, modeled, and assessed
- **3.6** Student mistreatment policy: published, accessible, enforced; data reviewed annually

### Standard 4 — Faculty Preparation, Productivity, Participation, and Policies
- **4.1** Sufficient faculty: number and diversity to fulfill curriculum delivery and scholarly mission
- **4.2** Faculty credentials and qualifications: documented for all faculty teaching in the program
- **4.3** Faculty scholarly productivity: research, peer-reviewed publications, grants, or other scholarly work
- **4.4** Faculty development: ongoing opportunities; supported by the institution
- **4.5** Faculty appointment and promotion: clear, documented, equitable criteria; merit-based
- **4.6** Faculty diversity: active efforts to achieve diversity in gender, race/ethnicity, and background

### Standard 5 — Educational Resources and Infrastructure
- **5.1** Finances: budget sufficient to support medical education program; financial stability demonstrated
- **5.2** Clinical instructional resources: adequate patient volumes, cases, and procedures for required competencies
- **5.3** Information resources: library services; electronic databases; clinical decision tools
- **5.4** Technology infrastructure: supports education delivery and student assessment
- **5.5** Research infrastructure: supports faculty and student scholarly activity

### Standard 6 — Competencies, Curricular Objectives, and Curricular Design
- **6.1** Competency-based framework: program organized around defined competencies and measurable objectives
- **6.2** Entrustable Professional Activities (EPAs) or equivalent milestone framework
- **6.3** Integration of basic science and clinical science: documented; vertically and horizontally integrated
- **6.4** Curricular design rationale: documented rationale for sequencing and structure
- **6.5** Patient safety curriculum: explicit content; assessed in students

### Standard 7 — Curricular Content
- **7.1** Normal human structure and function
- **7.2** Abnormal human structure and function (pathology, pathophysiology)
- **7.3** Social and behavioral sciences; health determinants; cultural competency
- **7.4** Ethical and professional responsibilities; legal issues in medicine
- **7.5** Clinical medicine, including history-taking, physical examination, clinical reasoning, and evidence-based medicine
- **7.6** Health systems science: quality improvement, patient safety, healthcare delivery
- **7.7** End-of-life care; pain management
- **7.8** Preventive medicine, health promotion, and disease prevention
- **7.9** Medical genetics and genomics
- **7.10** Content taught by MDs: appropriate physician participation in teaching

### Standard 8 — Curricular Management, Evaluation, and Enhancement
- **8.1** Curriculum committee: representative, functioning; authority over and responsibility for the entire curriculum
- **8.2** Curriculum management system: tracks all required content, prevents gaps and unplanned redundancies
- **8.3** Curricular evaluation: systematic, ongoing; uses student performance data, survey data, and outcomes data
- **8.4** Feedback loop: evaluation data demonstrably used to improve the curriculum
- **8.5** USMLE/COMLEX performance monitoring: program-level tracking; used for curricular improvement

### Standard 9 — Teaching, Supervision, Assessment, and Student Advancement
- **9.1** Teaching methods: appropriate variety; active learning; evidence-based
- **9.2** Supervision: policies for supervising medical students in clinical settings; enforced
- **9.3** Assessment: multiple assessment methods across competency domains; timely feedback
- **9.4** Formative assessment: students receive regular formative feedback
- **9.5** Summative assessment: objective, criterion-referenced; final competency determinations documented
- **9.6** Academic standards: progression and promotion criteria published; applied consistently
- **9.7** USMLE Step requirements: policy for Step 1 and Step 2 requirements for promotion/graduation
- **9.8** Student advancement committee: functions consistently; decisions documented; due process ensured

### Standard 10 — Medical Student Selection, Assignment, and Progress
- **10.1** Admissions policies: published, consistently applied; comply with applicable laws (ADA, Title VI, Title IX)
- **10.2** MCAT and academic requirements: published; applied consistently
- **10.3** Holistic review: consideration of non-academic factors; documented process
- **10.4** Enrollment management: class size consistent with resources and educational mission
- **10.5** Advanced standing and transfer: clear policies; consistently applied
- **10.6** Student assignment to sites: equitable; meets educational objectives

### Standard 11 — Medical Student Academic Support, Career Advising, and Educational Records
- **11.1** Academic support: tutoring, remediation, learning specialists; accessible
- **11.2** Career advising: structured advising program; adequate resources; residency match preparation
- **11.3** Educational records: secure; accessible to authorized users; FERPA-compliant
- **11.4** MSPE (Medical Student Performance Evaluation): accurate, timely, complete; written by advisor with direct knowledge
- **11.5** Student information security: policies and systems protect student records

### Standard 12 — Medical Student Health, Personal Counseling, and Financial Aid Services
- **12.1** Health services: confidential; accessible; appropriate scope; students not taught or assessed by own providers
- **12.2** Mental health services: confidential; accessible; adequate capacity
- **12.3** Disability services: ADA-compliant; documented accommodation process; reasonable accommodations provided
- **12.4** Financial aid: adequate counseling; published policies; exit counseling
- **12.5** Student debt counseling: proactive debt management support; AAMC benchmark awareness
- **12.6** Insurance: health insurance accessible; liability coverage for clinical activities

---

## Step 2: Search the Brain for LCME evidence

Navigate the Brain systematically. Top-down tree search — skip irrelevant branches.

### 2a. Wiki sub-brain
- `wiki/compliance/` — any LCME wiki pages, accreditation notes, prior survey responses
- `wiki/concepts/` — curriculum definitions, competency frameworks, EPAs
- `wiki/entities/` — curriculum committee, student affairs office, dean's office, affiliated hospitals

### 2b. PM sub-brain
- `pm/projects/` — LCME self-study project; DCI project; any interim report projects
- `pm/meetings/` — Curriculum Committee minutes, Student Promotions Committee minutes, Dean's Leadership Team
- `pm/notes/` — LCME consultant notes, accreditation briefing documents
- `pm/reports/` — prior LCME self-study, last evaluation team report and action letter, DCI submissions, annual medical education reports

### 2c. Planner sub-brain
- `planner/dashboard.md` — current LCME-related priorities
- `planner/tasks.md` — open accreditation action items

### 2d. Raw sources
- `raw/` — LCME correspondence, action letters, survey results, Graduation Questionnaire (GQ) reports, Year 2 and Year 4 student survey data

For every Brain document found:
- Map it to the **specific Element(s)** it supports
- Note **document type**: policy, minutes, assessment report, affiliation agreement, survey data, financial statement, etc.
- Flag documents **older than 2 years** as Stale — LCME evaluators expect current evidence
- Note whether evidence is **institutional** (policy exists) vs. **performance** (the policy is working)

---

## Step 3: Search connected systems

### 3a. SharePoint
- Curriculum Committee meeting minutes (Standard 8)
- Student Promotions Committee / Academic Standards Committee minutes (Standard 9)
- Affiliation agreements for all clinical sites (Standard 1.4)
- Faculty rosters with credentials (Standard 4)
- Course syllabi and curricular maps (Standards 6, 7, 8)
- Student survey results: AAMC GQ, Year 2 / Year 4 surveys, internal climate surveys (Standards 3, 8)
- USMLE Step 1 and Step 2 pass rate and score data (Standard 8.5)
- Academic support and advising program documents (Standard 11)
- Financial statements and budget documents (Standard 5.1)
- Health and counseling services utilization reports (Standard 12)
- Mistreatment policy and annual mistreatment data report (Standard 3.6)
- Student handbook and academic catalog (Standards 9, 10, 11)
- COI disclosure policies and records (Standard 2.4)

### 3b. Connectors
- **Outlook**: LCME correspondence, liaison communications, survey notifications
- **Teams**: accreditation task force, curriculum committee working channels
- **Jira**: open LCME preparation tickets or curricular revision work
- **Confluence**: living DCI drafts or accreditation preparation runbooks

### 3c. Primary LCME sources (web)
- **LCME Standards**: lcme.org/standards — cite exact Standard.Element (e.g., 8.1, 3.6)
- **DCI Template**: lcme.org/publications — current Data Collection Instrument
- **LCME Policies**: lcme.org/accreditation/functions-and-structure/policies/
- **Graduation Questionnaire benchmarks**: aamc.org/data-reports/curriculum-reports/interactive-data/graduation-questionnaire

**Citation format**: `[LCME, Standard N.N, Retrieved YYYY-MM-DD]`

---

## Step 4: Score each Element

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Met** | 🟢 | Clear, current (≤2 years) evidence exists and addresses both policy and performance |
| **Partial** | 🟡 | Evidence exists but is incomplete, stale (>2 years), policy-only without performance data, or not formally approved |
| **Not Evidenced** | 🔴 | No evidence found in Brain or connected systems |

**Site-visit risk**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | Element Not Evidenced; OR Element previously cited as a non-compliance finding |
| 🟠 High | Element Not Evidenced for a heavily-scrutinized area (3.6, 8.1, 9.6, 9.8, 10.1); OR stale evidence on a critical element |
| 🟡 Medium | Element Partial; Met evidence from single source only |
| 🟢 Low | Met with current, multi-source evidence including both policy and outcomes data |

**Note LCME-specific concern areas** — Elements historically generating the highest rate of non-compliance findings across medical schools:
- 3.6 (student mistreatment) — most commonly cited
- 8.1 (curriculum committee authority)
- 9.6 (consistent application of academic standards)
- 4.1 / 4.6 (faculty sufficiency and diversity)
- 12.2 (mental health services access and confidentiality)

---

## Step 5: Produce output by mode

---

### Mode: `gap` — Full Gap Analysis

```markdown
---
title: LCME Gap Analysis — <Scope>
scope: <standard number(s) or all>
date: YYYY-MM-DD
analyst: VP of Compliance / AI-assisted
---

# LCME Gap Analysis: <Scope>

## Summary
- **Elements Assessed**: N
- **Met (🟢)**: N  |  **Partial (🟡)**: N  |  **Not Evidenced (🔴)**: N
- **Critical / High Risk Items**: N
- **Previously Cited Non-Compliance (if known)**: [list]
- **DCI Submission Target Date**: YYYY-MM-DD

---

## Standard N — <Name>

| Element | Requirement Summary | Evidence Found | Status | Risk |
|---------|---------------------|---------------|--------|------|
| N.N | [plain-language summary] | [Brain page or "Not found"] | 🟢/🟡/🔴 | 🟢/🟡/🟠/🔴 |
...

**Standard N Risk Summary**: Overall — Critical / High / Medium / Low
**Top Gaps**:
1. [Element N.N] — [gap description] — [recommended action]

---

## Sources
1. [LCME, Standard N.N, Retrieved YYYY-MM-DD]
2. [Brain page citation]
```

---

### Mode: `dci` — DCI Evidence Drafts

For each Element in scope, output:

```markdown
## Element N.N — <Name>

**Requirement**: [verbatim or paraphrased LCME requirement]

**Available Evidence** (for DCI narrative):
- [Brain page / document title] — [what it demonstrates] — [last updated]
- ...

**Data Gaps** (fields the DCI will require that lack supporting data):
- [data point] — [suggested source or collection method]

**Draft DCI Response Stub**:
> [2–4 sentence draft narrative suitable for pasting into the DCI, based on available evidence. Flag with ⚠️ wherever data needs to be inserted.]

**Status**: 🟢 Ready to draft / 🟡 Needs additional data / 🔴 Cannot draft — evidence missing
```

---

### Mode: `priority` — Site-Visit Priority Actions

```markdown
---
title: LCME Site-Visit Priority Actions
date: YYYY-MM-DD
---

# LCME Site-Visit Priority Actions

## 🔴 Critical — Resolve before DCI submission

| # | Element | Gap | Action | Owner | Target |
|---|---------|-----|--------|-------|--------|
...

## 🟠 High — Resolve before self-study finalization

...

## 🟡 Medium — Resolve before site visit

...

## 🟢 Low / Monitoring

...

## Historically Cited Elements — Status Check
| Element | Known Risk | Current Status |
|---------|-----------|---------------|
| 3.6 | Student mistreatment — most commonly cited | [status] |
| 8.1 | Curriculum committee authority | [status] |
| 9.6 | Consistent application of academic standards | [status] |
| 4.1 | Faculty sufficiency | [status] |
| 12.2 | Mental health access and confidentiality | [status] |
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write to `wiki/compliance/lcme-gap-YYYY-MM-DD.md`
2. **Create LCME project** — scaffold a `pm/projects/lcme-accreditation/` project with gaps as issues
3. **Push tasks** — add Critical and High items to `planner/tasks.md`
4. **DCI mode** — offer to run `dci` mode for any Standard where gaps were found

---

## Quality Rules

- Never fabricate evidence. "Not found" is a valid and important finding.
- Never conflate policy existence with policy effectiveness — LCME evaluators want evidence both that policies exist AND that they are being followed.
- Always note whether quantitative data (USMLE scores, survey percentages, match rates) is available to support narrative claims — DCI responses require data, not just narrative.
- Flag any Element where the only evidence is self-report without external validation.
- Note the accreditation cycle position (years since last full review, years until next) to calibrate urgency.
