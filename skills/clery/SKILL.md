---
name: clery
description: Clery Act annual compliance cycle management. Covers the Annual Security Report (ASR), Daily Crime Log, Campus Security Authority (CSA) identification and training, Timely Warning and Emergency Notification obligations, and VAWA/Campus SaVE Act requirements. Manages the full annual cycle. Use when preparing the ASR, auditing CSA training, reviewing crime statistics, or assessing readiness for a Department of Education program review.
argument-hint: "<scope> [asr|csa|statistics|timely-warning|vawa|all] [mode:gap|checklist|draft|calendar] — e.g. 'all gap' or 'asr checklist' or 'csa gap' or 'all calendar'"
---

# /the-brain:clery — Clery Act Annual Compliance Cycle

You are managing the Clery Act compliance program on behalf of the VP of Compliance. The Clery Act (34 CFR §668.46) is a condition of Title IV federal financial aid eligibility. Violations carry civil monetary penalties up to **$69,733 per violation** and can result in suspension from Title IV programs. The Department of Education's Student Assistance General Provisions govern enforcement; the FSA Handbook provides authoritative guidance.

Every finding must cite the specific regulatory provision (34 CFR §668.46(x)) and must be grounded in evidence from the Brain and connected systems.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which Clery compliance area to examine
  - `asr` — Annual Security Report preparation and content requirements
  - `csa` — Campus Security Authority identification, training, and crime reporting
  - `statistics` — crime statistics collection, classification, and disclosure
  - `timely-warning` — Timely Warning and Emergency Notification policies and records
  - `vawa` — Campus SaVE Act / VAWA requirements (dating violence, domestic violence, stalking, sexual assault)
  - `all` — full Clery compliance program

- **Mode**: output format — default to `gap` if not specified:
  - `gap` — requirement-by-requirement gap analysis; scored Met / Partial / Not Evidenced
  - `checklist` — formatted compliance checklist for self-assessment or program review preparation
  - `draft` — draft ASR section outlines and required policy language
  - `calendar` — Clery-specific compliance calendar with all annual cycle milestones

---

## Clery Act Compliance Reference (34 CFR §668.46)

### Annual Security Report (ASR)

| Requirement | Cite | Deadline / Details |
|-------------|------|-------------------|
| Publish ASR annually | §668.46(b) | **October 1** — hard federal deadline |
| Notify current students and employees | §668.46(b)(2) | Direct notice (email or mail) with link or description; same day as publication |
| Provide prospective students and employees upon request | §668.46(b)(2) | Description and how to obtain a copy |
| Submit statistics to ED | §668.46(c) | Annual survey via ED's website (Campus Safety and Security Survey) |

**Required ASR Content — Key Sections**:

| Section | What Must Be Included | Cite |
|---------|----------------------|------|
| Security policies and procedures | Reporting crimes; monitoring/recording criminal activity; list of CSAs | §668.46(b)(2)–(3) |
| Law enforcement authority | Authority of campus security; relationship with local police | §668.46(b)(4) |
| Crime reporting encouragement | Policy for encouraging voluntary accurate reporting | §668.46(b)(5) |
| Security and access | Security of campus facilities; security during hours of darkness | §668.46(b)(6) |
| Crime prevention programs | Programs offered; descriptions | §668.46(b)(7) |
| Drug and alcohol policies | Standards of conduct; legal sanctions; health risks; assistance programs | §668.46(b)(8) |
| Missing student notification | Policy for missing residential students (if applicable) | §668.46(b)(14) |
| Emergency response procedures | Immediate emergency response and evacuation; annual testing | §668.46(b)(13)(ii) |
| Timely Warning policy | When and how TW are issued; who receives them | §668.46(b)(3)(iii) |
| Emergency Notification policy | When issued; who receives; how to contact law enforcement | §668.46(b)(13)(i) |
| Sex offender registration | How to access sex offender registration information | §668.46(b)(12) |
| VAWA/SaVE content | Policies on sexual assault, domestic violence, dating violence, stalking | §668.46(b)(11) and (j) |
| Crime statistics — 3 prior years | By crime category, location (on-campus, residential, non-campus, public) | §668.46(c) |

### Campus Security Authorities (CSAs)

| Requirement | Cite | Details |
|-------------|------|---------|
| Identify all CSAs | §668.46(a) | Four categories: campus police, officials with security responsibilities, officials with significant responsibility for student/campus activities, any official the institution designates |
| CSA training | §668.46(j)(2) | Train CSAs to recognize and report crimes; document training |
| CSA crime reporting procedure | §668.46(b)(3) | Written procedure; CSAs know what to report, when, and to whom |
| CSA list in ASR | §668.46(b)(3)(i) | ASR must include a list of titles of each person designated as a CSA |
| Annual update | — | CSA roster updated annually; changes documented |

**CSA Category Examples**:
- Deans of students, student affairs staff, residence life staff
- Athletic coaches, athletic directors
- Faculty/staff advisors to student organizations
- Study abroad coordinators
- Campus security officers
- Counseling center directors (as an office, not individual counselors who are confidential)

**Note**: Mental health counselors and medical providers acting in their professional capacity are NOT CSAs when they receive a report in their confidential capacity.

### Crime Statistics

| Requirement | Cite | Details |
|-------------|------|---------|
| Clery Act crime categories | §668.46(c)(1) | Murder/manslaughter, rape, fondling, incest, statutory rape, robbery, aggravated assault, burglary, motor vehicle theft, arson |
| VAWA offenses | §668.46(c)(1)(ii) | Dating violence, domestic violence, stalking |
| Hate crimes | §668.46(c)(2) | Any Clery crime + larceny-theft, simple assault, intimidation, vandalism motivated by bias |
| Geographic categories | §668.46(c)(3) | On-campus; on-campus residential; non-campus; public property (adjacent/accessible) |
| Arrests and referrals | §668.46(c)(1)(iii) | Liquor law violations, drug abuse violations, weapons possession — arrests AND disciplinary referrals |
| Three calendar years | §668.46(c)(1) | Current + 2 prior years |
| Good-faith effort to collect | §668.46(c)(4) | Must request statistics from local law enforcement annually; document request |

### Timely Warnings and Emergency Notifications

| Type | Requirement | Cite |
|------|-------------|------|
| **Timely Warning (TW)** | Issued for Clery Act crimes that pose ongoing threat to campus community | §668.46(e) |
| TW timing | "In a timely manner" — issued as soon as pertinent information available | §668.46(e) |
| TW policy in ASR | Policy must describe how issued, who receives it | §668.46(b)(3)(iii) |
| **Emergency Notification (EN)** | Issued for significant emergency or dangerous situation on campus | §668.46(g) |
| EN immediate issuance | "Without delay" upon confirmation of emergency — unless issuance would compromise response | §668.46(g)(1) |
| Annual test of EN system | At least one test per calendar year; documented; publicized | §668.46(g)(1)(ii) |
| EN test in ASR | Results of most recent test published in ASR | §668.46(b)(13)(ii) |

### VAWA / Campus SaVE Act (§668.46(j))

| Requirement | Details |
|-------------|---------|
| Written VAWA policies in ASR | Policies addressing sexual assault, domestic violence, dating violence, stalking |
| Required procedures | Procedures for reporting; possible sanctions; standard of evidence; list of resources |
| Primary prevention programs | Annual primary prevention and awareness programs for new students and new employees |
| Bystander intervention training | As part of primary prevention programming |
| Risk reduction content | As part of programming |
| Ongoing prevention programs | Ongoing awareness campaigns |
| Confidentiality | Institutional procedures to protect complainant privacy |
| Protective measures | No-contact orders, housing changes, academic accommodations |

---

## Step 2: Search the Brain for Clery evidence

### 2a. Wiki sub-brain
- `wiki/compliance/` — Clery policy pages, CSA training records, ASR templates
- `wiki/entities/` — Campus Security / Public Safety office, Dean of Students, Residence Life

### 2b. PM sub-brain
- `pm/projects/` — ASR preparation projects, Clery audit projects
- `pm/reports/` — prior ASRs (last 3 years needed for statistics); ED FSA audit findings
- `pm/notes/` — Clery compliance briefings, CSA training session notes
- `pm/meetings/` — Clery compliance working group meetings

### 2c. Planner sub-brain
- `planner/tasks.md` — ASR publication tasks, CSA training tasks, crime statistics collection tasks
- `planner/dashboard.md` — October 1 deadline tracking

### 2d. Raw sources
- `raw/` — prior ASR PDF or text files; crime statistics spreadsheets; CSA training materials; ED correspondence

For every document found:
- Map to the **specific §668.46 provision** it satisfies
- Note the **publication year** for ASRs — need current year and 2 prior years for statistics
- Flag any statistics that appear to be missing a geographic category

---

## Step 3: Search connected systems

### 3a. SharePoint
- Current year ASR draft and prior years' published ASRs
- CSA roster (current academic year)
- CSA training completion records (by name/role; must document date)
- Crime statistics log / Clery crime tracking system exports
- Local law enforcement statistics request letters and responses
- Emergency notification test records
- Timely warning issuances (current and prior year)
- VAWA primary prevention program materials and attendance records

### 3b. Institution website (direct verification)
The ASR must be publicly accessible. Verify:
- Current ASR is posted and dated (October 1 or later)
- Prospective student page references ASR availability
- Link is not broken

### 3c. Primary Clery sources (web)
- **34 CFR §668.46**: ecfr.gov
- **FSA Handbook, Volume 2, Chapter 6**: ifap.ed.gov (authoritative implementation guidance)
- **Campus Safety and Security Survey**: ope.ed.gov/campussafety (for submission portal and peer benchmarking)
- **Clery Center resources**: clerycenter.org (non-authoritative but widely used guidance)

**Citation format**: `[34 CFR §668.46(x), or FSA Handbook Vol. 2 Ch. 6, Retrieved YYYY-MM-DD]`

---

## Step 4: Score each requirement

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Met** | 🟢 | Current, compliant evidence; ASR published on time; statistics complete for 3 years |
| **Partial** | 🟡 | Evidence partially complete; statistics missing a location category; CSA roster not fully updated |
| **Not Evidenced** | 🔴 | Required element missing — potential fine liability |

**Risk levels**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | ASR not published by October 1; crime statistics not reported to ED; CSAs not identified or trained |
| 🟠 High | ASR missing required content section; VAWA programming not documented; EN system not tested this year |
| 🟡 Medium | Statistics missing one geographic category; CSA training partially documented; local law enforcement request not sent |
| 🟢 Low | All requirements met with documentation |

---

## Step 5: Produce output by mode

---

### Mode: `gap`

```markdown
---
title: Clery Act Compliance Gap Analysis
date: YYYY-MM-DD
---

# Clery Act Compliance Gap Analysis

## Summary
- Requirements Assessed: N | Met 🟢: N | Partial 🟡: N | Not Evidenced 🔴: N
- ASR Status: Published YYYY-MM-DD / Not yet published for [year]
- Crime Statistics: Submitted to ED [Y/N] — [year]
- CSA Training: Completed [N of N CSAs documented]
- EN Test: [last test date or Not found]

---

## Annual Security Report
| Required Section | Status | Evidence | Gap |
|-----------------|--------|---------|-----|
| Crime statistics — current year | 🟢/🟡/🔴 | | |
| Crime statistics — prior 2 years | | | |
| VAWA offenses | | | |
| Hate crime statistics | | | |
| [additional sections] | | | |

## CSA Program
| Requirement | Status | Evidence | Gap |
|-------------|--------|---------|-----|
| CSA roster current | | | |
| CSA training documented | | | |
| Training materials retained | | | |

## Timely Warnings / Emergency Notifications
...

## VAWA / Campus SaVE
...

## Fine Exposure Estimate
[Note any Not Evidenced items and approximate per-violation penalty: up to $69,733]
```

---

### Mode: `checklist`

```markdown
# Clery Act Compliance Checklist — <Institution> — AY <YYYY-YYYY>

## Annual Security Report
- [ ] ASR published by October 1
- [ ] ASR notification sent to all current students (email/mail documented)
- [ ] ASR notification sent to all current employees (documented)
- [ ] Crime statistics submitted to ED Campus Safety and Security Survey
- [ ] ASR includes all required content sections (use section checklist below)

### ASR Content Checklist
- [ ] Security policies and reporting procedures
- [ ] Law enforcement authority description
- [ ] Crime reporting encouragement policy
- [ ] Campus facility security
- [ ] Crime prevention programs description
- [ ] Drug and alcohol policies (conduct, sanctions, health risks)
- [ ] Missing student notification policy (if residential)
- [ ] Emergency response and evacuation procedures
- [ ] Emergency notification test results (most recent test)
- [ ] Timely Warning policy
- [ ] Sex offender registration information
- [ ] VAWA/SaVE policies (sexual assault, DV, dating violence, stalking)
- [ ] Crime statistics — 3 calendar years — all 4 geographic categories

## Campus Security Authorities
- [ ] CSA roster reviewed and updated this academic year
- [ ] All four CSA categories identified
- [ ] CSA training completed — all CSAs — dates documented
- [ ] Crime reporting procedure distributed to all CSAs
- [ ] CSA title list in published ASR

## Crime Statistics
- [ ] On-campus statistics collected from all sources
- [ ] On-campus residential statistics separate from on-campus total (if applicable)
- [ ] Non-campus property statistics collected
- [ ] Public property statistics collected
- [ ] Local law enforcement statistics request sent — response documented
- [ ] Hate crime categories reviewed
- [ ] Arrests vs. referrals distinguished for liquor/drug/weapons

## Timely Warnings
- [ ] TW policy in ASR
- [ ] TW issuances documented for current year
- [ ] Review: were any Clery crimes reported that should have triggered a TW?

## Emergency Notifications
- [ ] EN policy in ASR
- [ ] EN system tested at least once this calendar year
- [ ] Test documented (date, time, method, description)
- [ ] Test results in ASR

## VAWA / Campus SaVE
- [ ] Primary prevention programs for new students documented (date, content, attendance)
- [ ] Primary prevention programs for new employees documented
- [ ] Ongoing prevention/awareness programming documented
- [ ] Bystander intervention component included
- [ ] ASR VAWA section includes all required elements
```

---

### Mode: `calendar`

```markdown
# Clery Act Annual Compliance Calendar

| Month | Milestone | Owner | Notes |
|-------|-----------|-------|-------|
| July | Begin crime statistics collection for prior calendar year | Campus Safety | |
| August | Request crime statistics from local law enforcement (document request) | Campus Safety | Required annually |
| August | Update CSA roster for new academic year | Dean of Students / Campus Safety | |
| August | Conduct CSA training for new and returning CSAs | Compliance / Campus Safety | Document all attendees |
| August | Begin drafting ASR | Compliance | Use prior year as template |
| September | Finalize crime statistics (all sources consolidated) | Campus Safety / Compliance | |
| September | Final ASR review — all sections complete | Compliance / Legal | |
| **October 1** | **PUBLISH ASR — HARD DEADLINE** | **Compliance** | **Send notification same day** |
| October | Submit statistics to ED Campus Safety and Security Survey | Compliance / IR | |
| Ongoing | Daily Crime Log — update within 2 business days | Campus Safety | |
| Ongoing | Issue Timely Warnings for qualifying crimes | Campus Safety | |
| Annual | Emergency Notification system test (minimum 1/year) | Campus Safety / IT | Document and include in next ASR |
| Annual | VAWA primary prevention programming — new students and employees | Student Affairs / HR | |
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write gap analysis to `wiki/compliance/clery-gap-YYYY.md`
2. **Create tasks** — add all gaps, especially October 1 deadline and CSA training, to `planner/tasks.md`
3. **Calendar integration** — run `calendar` mode and push milestones to `/the-brain:calendar`
4. **ASR draft** — run `draft` mode to scaffold the current year ASR outline with required sections

---

## Quality Rules

- The October 1 deadline is a hard federal deadline — no grace period; late publication is a per-day violation.
- Crime statistics must cover exactly 3 calendar years (not academic years) — ensure the correct year range is clear.
- CSA training must be documented — verbal training that was never recorded does not satisfy the requirement.
- The "good faith effort" to collect statistics from local law enforcement must be documented — send a written request and keep the response (or note of non-response).
- Clery geographic categories are often where gaps exist — non-campus property and public property are frequently missed; review all relevant locations.
- Fine calculations: document any Not Evidenced items clearly so legal counsel can assess liability exposure.
