---
name: training
description: Mandatory compliance training tracker. Inventories all required compliance training programs by employee category, tracks completion status, identifies populations out of compliance, and produces the attestation documentation that auditors request. Use when auditing training compliance, preparing for an accreditation review, preparing for an audit, or running the annual training cycle.
argument-hint: "<scope> [all|domain:<domain>|role:<role>|program:<name>] [mode:status|gap|report|schedule] — e.g. 'all status' or 'domain:research gap' or 'role:faculty status' or 'program:HIPAA report'"
---

# /the-brain:training — Mandatory Compliance Training Tracker

You are auditing mandatory compliance training on behalf of the VP of Compliance. Training completion is the single most frequently requested documentation artifact in compliance audits — MSCHE, LCME, ACGME, OCR, OIG, NIH, and FSA auditors all ask for it. An institution that cannot demonstrate who was trained, on what, when, and by whom is at significant audit risk even if underlying policies are sound.

Every output must be grounded in what is actually documented in the Brain and connected systems. Never assert training was completed without documented evidence.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which training programs or populations to examine
  - `all` — the full mandatory training inventory across all domains and roles
  - `domain:<domain>` — all training required by a specific compliance domain (see taxonomy below)
  - `role:<role>` — all training required for a specific employee or student role
  - `program:<name>` — status of a specific named training program

- **Mode**: output format — default to `status` if not specified:
  - `status` — dashboard of completion rates by program and by employee category
  - `gap` — populations or individuals out of compliance; sorted by regulatory urgency
  - `report` — formatted training completion report suitable for submission to auditors or accreditors
  - `schedule` — annual training schedule with due dates by program and role

---

## Mandatory Training Inventory

The following programs represent the required compliance training portfolio for a medical school. For each, the Brain should contain evidence of: (1) the training program exists, (2) it covers the required content, (3) completion is tracked, and (4) records are retained for the required period.

### HIPAA Training

| Requirement | Regulatory Basis | Who Must Complete | Frequency | Record Retention |
|-------------|-----------------|------------------|-----------|-----------------|
| HIPAA Privacy training | 45 CFR §164.530(b) | All workforce members with access to PHI | At hire + when material changes | 6 years |
| HIPAA Security awareness | 45 CFR §164.308(a)(5) | All workforce members | Annual | 6 years |
| HIPAA breach response training | 45 CFR §164.530(b) | Privacy Officers, Security Officers, relevant staff | At hire + upon policy change | 6 years |

### Research Compliance Training

| Program | Regulatory Basis | Who | Frequency | Notes |
|---------|-----------------|-----|-----------|-------|
| Human subjects / IRB | 45 CFR §46.103(f) institutional policy | All PIs, co-investigators, study personnel | Every 3–4 years (varies by IRB); before study initiation | CITI program widely used |
| Good Clinical Practice (GCP) | FDA; ICH E6 R2 | PIs and study staff conducting FDA-regulated research | Every 3 years minimum | |
| Animal care / IACUC training | PHS Policy IV.C.1.f; AWA | All personnel working with animals | Before beginning + refreshers | |
| Responsible Conduct of Research (RCR) | NIH NOT-OD-10-019 | Graduate students, postdocs, junior faculty on NIH training grants | Per NIH requirements; at least once | Required for NIH T and F awards |
| Export controls awareness | EAR / ITAR; institutional policy | Faculty and staff in affected labs/projects | Annual or upon assignment | |
| Biosafety / IBC | NIH Guidelines | Personnel working with rDNA, biological agents | Before initiation + annual | |
| FCOI / COI training | 42 CFR §50.604(c) | All Investigators on PHS-funded research | Before beginning PHS research; every 4 years; upon policy change | See `/the-brain:coi` |

### Title IX and Civil Rights Training

| Program | Regulatory Basis | Who | Frequency | Notes |
|---------|-----------------|-----|-----------|-------|
| Title IX awareness | 34 CFR §106.8(d) | All students and employees | Annual (policy notice); depth varies by role | |
| Title IX Coordinator training | 34 CFR §106.8(d)(1) | Title IX Coordinator(s) | Ongoing / at designation | |
| Title IX investigator training | 34 CFR §106.45(b)(1)(iii) | Investigators | Before serving as investigator | Materials must be publicly posted |
| Title IX decision-maker training | 34 CFR §106.45(b)(1)(iii) | Decision-makers (hearing officers) | Before serving | Materials must be publicly posted |
| Title IX informal resolution training | 34 CFR §106.44(k) | Facilitators | Before facilitating | |

### Clery Act / Campus Safety Training

| Program | Regulatory Basis | Who | Frequency | Notes |
|---------|-----------------|-----|-----------|-------|
| Campus Security Authority (CSA) training | 34 CFR §668.46(j) | All identified CSAs | Annual or upon designation | Document date and attendees |
| VAWA/SaVE bystander intervention | 34 CFR §668.46(j)(2) | All new students; all new employees | At orientation | Document attendance |
| VAWA ongoing prevention programs | 34 CFR §668.46(j)(2) | All students and employees | Ongoing | Document program dates and participation |

### ACGME / GME Training

| Program | Regulatory Basis | Who | Frequency | Notes |
|---------|-----------------|-----|-----------|-------|
| Duty hours policy | ACGME Common Program Requirements V | All residents and fellows | Annual / at orientation | |
| Supervision policy training | ACGME CPR III | All faculty supervising residents | Annual / at onboarding | |
| Patient safety / quality improvement | ACGME CPR VI | All residents and fellows | Annual | CLER Focus Area |
| Fatigue mitigation | ACGME CPR V.C | All residents and fellows | Annual | |
| Professionalism | ACGME CPR IV | All residents, fellows, faculty | Annual | |
| Wellbeing resources | ACGME CPR V | Residents, fellows, faculty | Annual / at orientation | |

### HR / Employment Compliance Training

| Program | Regulatory Basis | Who | Frequency | Notes |
|---------|-----------------|-----|-----------|-------|
| Harassment prevention | EEOC guidance; state law | All employees | Annual (some states mandate frequency) | California, New York: specific requirements |
| ADA / accommodation process | ADA; 29 CFR §1630 | HR staff, supervisors, managers | At hire + periodic | |
| FMLA administration | 29 CFR Part 825 | HR staff, supervisors | At hire + periodic | |
| I-9 / E-Verify process | INA §274A | HR staff processing new hires | At hire + upon policy change | |
| OSHA safety training | 29 CFR Part 1910 (varies by hazard) | All employees + role-specific | Varies by standard | |

### FERPA Training

| Program | Regulatory Basis | Who | Frequency |
|---------|-----------------|-----|-----------|
| FERPA — student records | 34 CFR Part 99 | All faculty and staff who access student records | At hire + annual refresher |
| FERPA — medical school student records | 34 CFR Part 99 | Registrar, Dean of Students, Student Affairs staff | Annual |

### LCME-Required Training

| Program | LCME Standard | Who | Frequency |
|---------|--------------|-----|-----------|
| Faculty development — teaching methods | Standard 4.4 | All teaching faculty | Ongoing / at onboarding |
| Supervision of medical students | Standard 9.1 | Residents who teach/supervise students | Annual |
| Mistreatment reporting | Standard 12.5 | All faculty, residents, staff interacting with students | Annual |
| Learning environment expectations | Standard 3.5 | All faculty, staff, and residents | Annual |

---

## Step 2: Search the Brain for training records

### 2a. Wiki sub-brain
- `wiki/compliance/` — training program pages, training completion policy
- `wiki/entities/` — HR office, Compliance office, GME office, Research Compliance office, Title IX office

### 2b. PM sub-brain
- `pm/projects/` — annual training compliance projects, LMS implementation projects
- `pm/reports/` — training completion rate reports, audit-requested training summaries
- `pm/notes/` — compliance committee discussions of training gaps; HR training calendar notes

### 2c. Planner sub-brain
- `planner/tasks.md` — annual training launch tasks, completion deadline reminders

### 2d. Raw sources
- `raw/` — training roster exports, CITI completion reports, LMS exports

For every training record found:
- Note the **training program name**, **date completed**, **employee category covered**, and **record source**
- Note whether records show **individual completion** vs. **aggregate completion rates**
- Note the **record retention status** (HIPAA: 6 years; most others: 3–7 years or per policy)

---

## Step 3: Search connected systems

- **SharePoint**: training rosters by program; CITI training exports; LMS (learning management system) completion reports; harassment prevention certificates; CSA training sign-in sheets; GME orientation training documentation
- **Outlook/Teams**: training launch announcements; completion reminder emails; HR training notifications
- **Jira**: training compliance tracking tickets

---

## Step 4: Produce output by mode

---

### Mode: `status` — Training Compliance Dashboard

```markdown
---
title: Mandatory Training Compliance Dashboard
date: YYYY-MM-DD
---

# Mandatory Training Compliance Dashboard

## Overall Summary
- Training Programs Tracked: N
- Programs with Full Compliance: N (🟢)
- Programs with Partial Completion: N (🟡)
- Programs with No Records / Not Evidenced: N (🔴)

---

## Program-by-Program Status

| Program | Domain | Required Populations | Records Found | Completion Rate | Due Date | Status |
|---------|--------|---------------------|--------------|----------------|----------|--------|
| HIPAA Privacy | PRIVACY | All workforce | [Y/N — source] | N% or Unknown | Annual | 🟢/🟡/🔴 |
| HIPAA Security | PRIVACY | All workforce | | | Annual | |
| IRB / Human Subjects | RESEARCH | Investigators | | | Per FWA | |
| CSA Training | SAFETY | All CSAs | | | Annual | |
| Title IX Investigator | TITLE9 | Investigators | | | Before serving | |
| ACGME Duty Hours | GME | Residents/Fellows | | | Annual | |
| Harassment Prevention | HR | All employees | | | Annual | |
| FERPA | STUDENT | Faculty/Staff | | | Annual | |
...

---

## Status by Employee Category

| Role | # Training Programs Required | Fully Compliant | At Risk | Records Missing |
|------|----------------------------|----------------|---------|----------------|
| Faculty | N | N | N | N |
| Residents/Fellows | N | N | N | N |
| Staff (clinical) | N | N | N | N |
| Staff (admin) | N | N | N | N |
| Students (medical) | N | N | N | N |
```

---

### Mode: `gap` — Populations Out of Compliance

```markdown
---
title: Training Compliance Gaps
date: YYYY-MM-DD
---

# Training Compliance Gaps

Sorted by regulatory urgency.

## 🔴 Critical — Regulatory Non-Compliance

| Program | Population | Gap Description | Regulatory Consequence | Recommended Action |
|---------|-----------|-----------------|----------------------|-------------------|
| FCOI Training | Investigators on PHS awards | No completion records found for N investigators | Cannot expend PHS funds without training; 42 CFR §50.604(c) | Launch training immediately; hold award expenditures |
| IRB Training | Study team members | N protocols have team members with expired CITI | Research may not continue; OHRP reportable | Suspend protocols until training complete |
...

## 🟠 High — Accreditation or Audit Risk

| Program | Population | Gap | Risk | Action |
...

## 🟡 Medium — Completion Rate Below Target

| Program | Completion Rate | Target | Due Date | Action |
...

## Programs with No Records at All

| Program | Required By | Who | Recommended Action |
|---------|-----------|-----|-------------------|
```

---

### Mode: `report` — Auditor-Ready Training Report

```markdown
---
title: Training Compliance Report — <Program or Domain>
prepared_for: [Audit name / Accreditor / Internal review]
date: YYYY-MM-DD
period_covered: YYYY-MM-DD to YYYY-MM-DD
---

# Training Compliance Report

## Program: <Training Program Name>

**Regulatory Basis**: [citation]
**Required Population**: [description]
**Required Frequency**: [schedule]
**Content**: [summary of what the training covers]

## Completion Data

| Completion Period | # Required | # Completed | Completion Rate | Records Location |
|-----------------|-----------|------------|----------------|-----------------|
| [period] | N | N | N% | [source] |

## Documentation of Training Content
[Summary of what the training covers; how it addresses the regulatory requirement; trainer qualifications if applicable]

## Record Retention Compliance
**Retention Policy**: [years]
**Oldest Records Available**: YYYY-MM-DD
**Retention Method**: [LMS / SharePoint / paper files]

## Gaps and Remediation
[Any completion gaps and what was done about them]

## Certification
[Space for VP of Compliance signature and date]
```

---

### Mode: `schedule` — Annual Training Calendar

```markdown
---
title: Annual Compliance Training Schedule — AY YYYY–YYYY
date: YYYY-MM-DD
---

# Annual Compliance Training Schedule

## By Month

| Month | Training Program | Target Population | Delivery Method | Owner |
|-------|-----------------|------------------|----------------|-------|
| July–August | New employee HIPAA privacy | All new hires | LMS / in-person | HR |
| August | CSA training | All new and returning CSAs | In-person | Compliance |
| August | VAWA/SaVE orientation | All new students, new employees | Orientation session | Dean of Students / HR |
| October | HIPAA security refresher | All workforce | LMS | IT / Compliance |
| November | FCOI annual disclosure reminder | All investigators | Email + LMS | Research Compliance |
| December | Harassment prevention | All employees | LMS | HR |
| January | Duty hours — residents/fellows | All GME trainees | Orientation + annual | GME Office |
| Ongoing | IRB CITI renewals | Investigators per expiration | CITI platform | IRB |
| Ongoing | CSA crime report reminders | All CSAs | Email | Compliance |

## By Employee Category

| Role | Training Programs Required | Completion Cycle |
|------|--------------------------|-----------------|
| All employees | HIPAA Privacy, HIPAA Security, Harassment Prevention, FERPA (if applicable) | Annual |
| Faculty | Above + IRB (if research), LCME mistreatment, Title IX awareness | Annual + at onboarding |
| Residents/Fellows | HIPAA, ACGME suite (duty hours, supervision, wellbeing, professionalism, QI/patient safety) | Annual + at orientation |
| Research staff | IRB CITI, FCOI, Export Controls (if applicable), GCP (if applicable), RCR (if applicable) | Per regulatory cycle |
| Clinical staff | HIPAA, Joint Commission (if applicable), OSHA safety | Annual |
| Students (medical) | HIPAA, FERPA, VAWA/SaVE, mistreatment/learning environment | At orientation + annual |
```

---

## Step 5: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write status report to `wiki/compliance/training-status-YYYY-MM-DD.md`
2. **Create tasks** — add overdue and near-term training programs as tasks in `planner/tasks.md`
3. **Calendar integration** — push annual training schedule to `/the-brain:calendar`
4. **Audit package** — if an audit is approaching, run `report` mode for each program the auditor has requested
5. **Gap follow-up** — for FCOI training gaps, escalate via `/the-brain:coi`; for IRB training gaps, escalate via `/the-brain:research`

---

## Quality Rules

- **"Training was conducted" without records is not evidence** — if completion records cannot be produced, treat it as 🔴 Not Evidenced for audit purposes.
- **Individual completion records vs. aggregate rates**: auditors typically want to see individual names, dates, and training titles for high-risk programs (FCOI, IRB, Title IX investigator); aggregate rates alone are insufficient for those programs.
- **Training materials must be retained**: for Title IX, training materials must be publicly posted; for HIPAA, materials must be retainable for 6 years; for IRB, completion certificates must survive for the life of the award plus the retention period.
- **Role changes matter**: when an employee changes roles (e.g., a faculty member becomes a study PI, or a staff member is designated as a CSA), new training obligations may be triggered — flag role-based training gaps for new designees.
- **Completion rate targets**: MSCHE and LCME evaluators often look for 100% completion for legally required training (HIPAA, FERPA); anything below 90% for regulatory training is a finding risk; anything below 80% warrants immediate remediation.
