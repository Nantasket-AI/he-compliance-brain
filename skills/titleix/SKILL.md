---
name: titleix
description: Title IX compliance audit and management. Covers the 2022 Title IX regulations (34 CFR Part 106), coordinator obligations, required policies and grievance procedures, training documentation, supportive measures, and annual certification. Use when auditing Title IX program compliance, reviewing grievance procedures, preparing for a Department of Education review, or responding to a complaint.
argument-hint: "<scope> [coordinator|policies|procedures|training|all] [mode:gap|brief|checklist|response] — e.g. 'all gap' or 'policies checklist' or 'training brief' or 'procedures response'"
---

# /the-brain:titleix — Title IX Compliance Audit & Management

You are performing a Title IX compliance review on behalf of the VP of Compliance. Title IX compliance is a mandatory condition of receiving federal financial assistance. The 2022 regulations (effective August 1, 2024) impose specific procedural, policy, and staffing requirements that are regularly audited by the Department of Education Office for Civil Rights (OCR).

Every finding must cite the specific regulatory provision (34 CFR §106.xx) and must be grounded in evidence from the Brain and connected systems.

**Regulatory note**: Title IX regulations have changed significantly in recent years. The 2020 regulations (effective August 14, 2020) were substantially revised by the 2022 regulations (effective August 1, 2024). Confirm which version applies to any document you find; evidence under the 2020 rules may not satisfy the 2024 requirements.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which Title IX compliance area to examine
  - `coordinator` — Title IX Coordinator designation, authority, and duties
  - `policies` — required written policies and annual notice
  - `procedures` — grievance procedures for complaints of sex discrimination
  - `training` — required training for coordinators, investigators, decision-makers, advisors
  - `all` — all areas

- **Mode**: output format — default to `gap` if not specified:
  - `gap` — element-by-element gap analysis; each requirement scored Met / Partial / Not Evidenced
  - `brief` — executive summary with top risk flags
  - `checklist` — formatted compliance checklist for self-assessment
  - `response` — structured response to a specific OCR complaint or Resolution Agreement obligation

---

## Title IX Regulatory Reference (34 CFR Part 106 — 2022 Regulations, Effective August 1, 2024)

### Coordinator Requirements (§106.8)

| Requirement | Cite | What It Requires |
|-------------|------|-----------------|
| Coordinator designation | §106.8(a) | At least one Title IX Coordinator; may have multiple |
| Coordinator qualifications | §106.8(a) | Must have training; must be free from conflicts of interest |
| Coordinator contact published | §106.8(b) | Name or title, office address, phone number, and email address — in catalog, on website, and in all notices |
| Coordinator duties | §106.8(c) | Coordinates compliance; receives complaints; ensures training; maintains records |
| Notice of Coordinator | §106.8(b) | Notice provided to all students, employees, parents/guardians, and applicants; must include how to contact coordinator |

### Required Policies (§106.8(c) and §106.45)

| Requirement | Cite | What It Requires |
|-------------|------|-----------------|
| Nondiscrimination policy | §106.8(c)(1) | Written statement that institution does not discriminate on basis of sex |
| Policy distributed annually | §106.8(c)(2) | Annual notice to all students, employees, parents/guardians |
| Grievance procedures posted | §106.45(b)(1)(i) | Written grievance procedures posted on website and distributed upon request |
| Supportive measures policy | §106.44(f)(1) | Written policy for offering supportive measures; must notify complainants and respondents |
| Prohibition on sex-based harassment | §106.2 | Policy prohibiting all forms of sex-based harassment including sexual violence |

### Grievance Procedures (§106.45 and §106.46)

| Requirement | Cite | What It Requires |
|-------------|------|-----------------|
| Written grievance procedures | §106.45(b)(1)(i) | Published, detailed procedures for resolving complaints |
| Objective evaluation | §106.45(b)(1)(ii) | Objective evaluation of all relevant evidence; no presumption of responsibility |
| Conflict of interest — investigators | §106.45(b)(1)(iii) | Investigators and decision-makers must be free from conflicts and bias; training documented |
| Written notice of allegations | §106.45(b)(2) | Notice to both parties upon initiation of grievance process |
| Opportunity to respond | §106.45(b)(3) | Both parties have equal opportunity to present information and evidence |
| Investigative report | §106.45(b)(7) | Written investigative report prior to determination; both parties can review and respond |
| Written determination | §106.45(b)(9) | Written determination of responsibility; simultaneously provided to both parties |
| Appeals | §106.45(b)(10) | Appeals process; same bases available to both parties |
| Reasonable timeframes | §106.45(b)(1)(v) | Reasonably prompt timeframes; extensions allowed for good cause |
| Informal resolution | §106.44(k) | Voluntary informal resolution option for certain complaints |
| Recordkeeping | §106.45(b)(10)(i) | Maintain records for minimum 7 years |

### Training Requirements (§106.45(b)(1)(iii) and §106.8(d))

| Who Must Be Trained | On What | Cite |
|--------------------|---------|------|
| Title IX Coordinator(s) | Title IX; §106 regulations; scope of institution's obligations; how to handle complaints | §106.8(d)(1) |
| Investigators | How to conduct investigations; evidence gathering; trauma-informed approach | §106.45(b)(1)(iii) |
| Decision-makers (hearing officers, panels) | How to serve impartially; evidentiary standards; technology issues | §106.45(b)(1)(iii) |
| Facilitators of informal resolution | Informal resolution process | §106.44(k) |
| **Training materials public posting** | All training materials must be posted on institution's website | §106.45(b)(1)(iii) |

### Supportive Measures (§106.44)

| Requirement | Cite | What It Requires |
|-------------|------|-----------------|
| Offer supportive measures | §106.44(f)(1) | Offered to complainant upon receiving a complaint; non-disciplinary, non-punitive |
| Offer to respondent | §106.44(f)(1) | Supportive measures offered to respondent as well |
| Confidentiality | §106.44(f)(1)(ii) | Supportive measures kept confidential to the extent possible |
| No unreasonable burden | §106.44(f)(1)(iii) | Measures not unreasonably burdensome to the other party |

### Mandatory Reporting vs. Confidential Employees

| Category | Requirement | Cite |
|----------|-------------|------|
| Employees with authority | Must report sex discrimination to Title IX Coordinator | §106.44(c) |
| Confidential employees | May provide confidential support without mandatory reporting duty | §106.44(j) |
| Institution must publish | Which employees are mandatory reporters vs. confidential | §106.8(c) |

---

## Step 2: Search the Brain for Title IX evidence

### 2a. Wiki sub-brain
- `wiki/compliance/` — Title IX policy pages, coordinator designation records, training logs
- `wiki/entities/` — Title IX Coordinator office, Deputy Coordinators, Student Affairs, HR

### 2b. PM sub-brain
- `pm/projects/` — Title IX policy revision projects, OCR investigation responses
- `pm/meetings/` — Title IX team meetings, compliance committee discussions of Title IX
- `pm/reports/` — OCR correspondence, Resolution Agreements, Title IX annual reports
- `pm/notes/` — policy revision notes, training curriculum notes

### 2c. Planner sub-brain
- `planner/tasks.md` — annual policy review tasks, training completion deadlines

### 2d. Raw sources
- `raw/` — OCR correspondence, resolution agreements, training materials, policy documents

For every document found:
- Map to the **specific §106 provision** it satisfies
- Note the **regulation version** it reflects (2020 or 2022/2024 rules)
- Flag any document reflecting the 2020 rules that has **not been updated** for 2024 — this is the most common Title IX compliance gap right now

---

## Step 3: Search connected systems

### 3a. SharePoint
- Title IX policy (most recent approved version — confirm reflects 2024 rules)
- Grievance procedures document (same)
- Title IX Coordinator contact page or designation memo
- Training completion certificates and sign-in sheets
- Training materials (must be publicly posted — note URL if web-posted)
- Supportive measures checklist or standard offering documentation
- Recordkeeping logs (complaint intake, investigation timelines, determinations)
- Annual notice distribution records (email, catalog, website update)

### 3b. Institution website (direct verification)
Title IX requires specific information be publicly posted. Verify the following are findable on the institution's public website:
- Title IX Coordinator name/title/contact information
- Nondiscrimination policy
- Grievance procedures
- Training materials
- How to file a complaint

### 3c. Primary regulatory sources (web)
- **34 CFR Part 106 (2022 Final Rule)**: ecfr.gov
- **DOE OCR Title IX Resource Guide**: ed.gov/ocr/title9.html
- **OCR Complaint and Compliance Review processes**: ed.gov/ocr/complaints.html

**Citation format**: `[34 CFR §106.xx, Title IX 2022 Final Rule, Retrieved YYYY-MM-DD]`

---

## Step 4: Score each requirement

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Met** | 🟢 | Current, compliant evidence under 2024 rules; publicly posted where required |
| **Partial** | 🟡 | Evidence exists but reflects 2020 rules not yet updated; not publicly posted; incomplete |
| **Not Evidenced** | 🔴 | Required element missing |

**OCR complaint risk**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | Required element missing; or element reflects superseded 2020 rules; or training materials not publicly posted |
| 🟠 High | Coordinator contact information not published in all required locations; annual notice not distributed this cycle |
| 🟡 Medium | Documentation stale but compliant version exists somewhere; recordkeeping gaps |
| 🟢 Low | All documentation current, compliant, and publicly accessible |

**High-scrutiny areas** (OCR probes these in virtually every review):
- Currency: Does the institution's policy reflect the 2024 regulations, not the 2020 regulations?
- Training materials: Are they publicly posted? Are they free from material that would cause a reasonable person to believe investigators are prejudging?
- Recordkeeping: Are complaint records maintained for 7 years?
- Coordinator designation: Is there a named, trained coordinator with published contact information?

---

## Step 5: Produce output by mode

---

### Mode: `gap`

```markdown
---
title: Title IX Compliance Gap Analysis
date: YYYY-MM-DD
regulation: 34 CFR Part 106 (2022 Final Rule, effective August 1, 2024)
---

# Title IX Compliance Gap Analysis

## Summary
- Requirements Assessed: N | Met 🟢: N | Partial 🟡: N | Not Evidenced 🔴: N
- Regulation Version in Current Policies: [2020 rules / 2024 rules / mixed — flag mixed as critical]
- OCR Complaints Active: [Y/N — if known]

---

## Coordinator Requirements (§106.8)
| Requirement | Evidence | Status | Risk |
|-------------|---------|--------|------|
| Coordinator designated | | 🟢/🟡/🔴 | |
| Contact published — catalog | | | |
| Contact published — website | | | |
| Contact published — annual notice | | | |
...

## Required Policies
...

## Grievance Procedures (§106.45 / §106.46)
...

## Training (§106.45(b)(1)(iii))
| Who | Training Topic | Completion Evidence | Materials Posted | Status |
|-----|---------------|---------------------|-----------------|--------|
| Coordinator | | | | |
| Investigators | | | | |
| Decision-makers | | | | |
...

## Supportive Measures (§106.44)
...

## Top Gaps
1. [gap] — [regulatory cite] — [recommended action]
```

---

### Mode: `checklist`

```markdown
# Title IX Compliance Checklist — <Institution> — <Date>

## Coordinator
- [ ] Coordinator designated in writing
- [ ] Coordinator's name/title/address/phone/email published in catalog
- [ ] Coordinator's contact on institution website (findable within 2 clicks from homepage)
- [ ] Annual notice includes Coordinator contact — sent to all students and employees this cycle
- [ ] Coordinator has completed required training (documented)

## Policies
- [ ] Nondiscrimination policy reflects 2024 regulations
- [ ] Policy distributed to all students, employees, parents/guardians, applicants this cycle
- [ ] Grievance procedures posted on website
- [ ] Grievance procedures reflect 2024 regulations (not 2020)
- [ ] Supportive measures policy in place and distributed

## Grievance Procedures
- [ ] Written procedures address all required elements (§106.45)
- [ ] Objective evaluation language included
- [ ] Conflict of interest provisions for investigators and decision-makers
- [ ] Written notice of allegations process
- [ ] Appeals available to both parties on equal terms
- [ ] Recordkeeping — 7-year retention policy in place

## Training
- [ ] All training materials publicly posted on website
- [ ] Coordinator training completed — date documented
- [ ] Investigator training completed — dates documented for each
- [ ] Decision-maker training completed — dates documented for each
- [ ] Informal resolution facilitator training (if informal resolution offered)

## Supportive Measures
- [ ] Documented process for offering supportive measures to complainants
- [ ] Documented process for offering supportive measures to respondents
- [ ] Confidentiality protections documented

## Recordkeeping
- [ ] Complaint intake records maintained
- [ ] Investigation records maintained
- [ ] Determination records maintained
- [ ] 7-year retention being followed
- [ ] Training records maintained
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write analysis to `wiki/compliance/titleix-gap-YYYY-MM-DD.md`
2. **Policy review** — if policies reflect 2020 rules, offer to note the required updates and trigger `/the-brain:policy` for the Title IX policy
3. **Create tasks** — add gaps to `planner/tasks.md` with owners and due dates
4. **Calendar integration** — add annual notice distribution and training renewal deadlines to `/the-brain:calendar`

---

## Quality Rules

- Always verify which regulatory version (2020 or 2024) is reflected in the institution's current policies — the 2024 rules are substantially different and this is the most common finding right now.
- Training materials must be publicly posted; "available upon request" is not compliant.
- The 7-year recordkeeping requirement applies from the date of final determination or action — confirm the records system supports this retention period.
- Never characterize a specific complaint's facts or outcomes — restrict analysis to programmatic/systemic compliance.
- OCR investigations can be triggered by a single complaint — one gap in procedure can become an institution-wide compliance review.
