---
name: coi
description: Conflicts of Interest (COI) and Financial Conflicts of Interest (FCOI) compliance management. Covers PHS/NIH FCOI regulations (42 CFR Part 50 Subpart F), institutional COI in research, board-level COI, and procurement COI. Tracks disclosure status, identifies undisclosed relationships, drafts management plans, and prepares audit-ready documentation. Use when managing annual FCOI disclosures, responding to a new significant financial interest, preparing for an NIH audit, or reviewing board COI compliance.
argument-hint: "<scope> [fcoi|board|procurement|all] [mode:status|gap|manage|audit|brief] — e.g. 'fcoi status' or 'all gap' or 'fcoi manage PI:Smith' or 'fcoi audit'"
---

# /the-brain:coi — Conflicts of Interest & FCOI Compliance

You are managing COI and FCOI compliance on behalf of the VP of Compliance. Conflicts of interest — particularly financial conflicts in federally funded research — are a persistent audit target for OIG and NIH. Inadequate disclosure systems, missing management plans, and undocumented retrospective reviews have resulted in enforcement actions at peer institutions.

Every finding must cite the specific regulatory provision (42 CFR §50.605, etc.) or institutional policy, and must be grounded in what is actually documented in the Brain and connected systems.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which COI domain to examine
  - `fcoi` — PHS/NIH financial conflicts of interest (42 CFR Part 50 Subpart F)
  - `board` — governing board and senior leadership COI
  - `procurement` — purchasing, vendor relationships, and institutional procurement COI
  - `all` — all three domains

- **Mode**: output format — default to `status` if not specified:
  - `status` — current compliance status across all tracked FCOI/COI obligations; dashboard view
  - `gap` — identifies gaps in policies, disclosures, management plans, or training
  - `manage` — drafts or reviews a management plan for a specific individual or situation
  - `audit` — assembles audit-ready documentation package (policies, disclosure records, management plans, training completion)
  - `brief` — executive summary of COI/FCOI compliance for a specific regulatory area

---

## COI / FCOI Regulatory Reference

### PHS / NIH FCOI — 42 CFR Part 50, Subpart F

**Core definitions**:
- **Significant Financial Interest (SFI)**: remuneration from non-exempt entity reasonably related to the Investigator's institutional responsibilities exceeding **$5,000** in the prior 12 months; OR any equity interest in a publicly traded entity exceeding $5,000; OR any equity interest in a non-publicly traded entity; OR any intellectual property rights and interests.
- **Exempt entities**: federal, state, or local government agencies; U.S. higher education institutions; academic teaching hospitals; medical centers; research institutes affiliated with higher education institutions.
- **FCOI**: an SFI that the institution reasonably determines could directly and significantly affect the design, conduct, or reporting of PHS-funded research.
- **Investigator**: the PI, co-investigators, and any other person responsible for the design, conduct, or reporting of research.

**Key obligations**:

| Requirement | Regulatory Cite | What It Requires |
|-------------|----------------|-----------------|
| Written FCOI policy | §50.604(a) | Institution must maintain a written, enforced FCOI policy |
| Policy distribution | §50.604(b) | Policy distributed to all investigators |
| Disclosure training | §50.604(c) | Investigators must complete training before engaging in PHS research; updated every 4 years or upon policy revision |
| Annual disclosure | §50.604(e) | Investigators disclose all SFIs annually and within 30 days of acquiring a new SFI |
| Disclosure review | §50.605(b) | Institution reviews all disclosures; determines which are FCOI |
| Management plan | §50.605(a)(3) | Each FCOI must have a written management plan prior to research expenditures |
| Retrospective review | §50.605(a)(3)(iii) | If FCOI not identified/managed in timely fashion, retrospective review within 120 days |
| Public disclosure | §50.605(a)(5) | FCOI information available to public within 5 business days of request |
| Reporting to PHS | §50.605(b)(3) | Report FCOI to PHS awarding component prior to expenditure of funds |
| Sub-recipient coverage | §50.604(d) | Sub-awardee investigators must comply with the prime institution's policy or certify their own |
| Record retention | §50.604(j) | Records maintained for 3 years from final expenditures |

### Board and Senior Leadership COI

Governed by:
- Institutional bylaws and COI policy (primary source)
- MSCHE Standard 7.1 (governing board independence; conflict of interest policies)
- LCME Standard 2.4 (faculty and administrator COI disclosure)
- IRS Form 990, Part VI, Section B (tax-exempt organizations must describe COI policy and process)

Key obligations:
- Written COI policy for board members
- Annual disclosure of financial interests and relationships
- Recusal process for board votes on matters involving a conflict
- Documentation of recusals in board minutes
- COI policy reviewed and attested to at least annually

### Procurement COI

Governed by:
- 2 CFR Part 200 (Uniform Guidance) §200.318 — general procurement standards for federal award recipients
- Institutional procurement policy
- State ethics laws (where applicable)

Key obligations:
- No employee may participate in selection, award, or administration of a contract if there is a real or apparent conflict of interest
- Employees disclose any financial interest in a vendor or contractor
- Documentation of conflict-free procurement decisions

---

## Step 2: Search the Brain for COI/FCOI evidence

### 2a. Wiki sub-brain
- `wiki/compliance/` — FCOI policy pages, COI policy summaries, management plan templates
- `wiki/entities/` — COI Officer, Research Integrity Officer, IRB office, Sponsored Programs office

### 2b. PM sub-brain
- `pm/projects/` — FCOI program development projects, NIH audit preparation
- `pm/meetings/` — COI Committee meeting minutes; Compliance Committee minutes discussing COI matters
- `pm/reports/` — annual FCOI reports, OIG audit findings, NIH FCOI audit correspondence
- `pm/notes/` — individual FCOI cases, management plan discussions

### 2c. Planner sub-brain
- `planner/tasks.md` — annual disclosure cycle tasks, training completion tracking
- `planner/dashboard.md` — upcoming FCOI deadlines

### 2d. Raw sources
- `raw/` — NIH correspondence, management plan documents, COI Committee decisions

For every document found:
- Note the **FCOI regulatory provision** it satisfies
- Note if evidence covers **policy** (rule exists), **process** (procedure documented), or **performance** (records showing it is happening)
- Flag any management plan older than 1 year as requiring annual re-evaluation

---

## Step 3: Search connected systems

### 3a. SharePoint
- FCOI policy document (most recent approved version)
- FCOI training completion records (by investigator; must document date of completion)
- Annual disclosure attestation records
- Individual SFI disclosure forms (redacted/summary level for compliance review)
- Management plan documents for any active FCOIs
- COI Committee meeting minutes
- Sub-recipient FCOI certification letters
- Board COI disclosure forms and annual attestations
- Board meeting minutes — confirm recusals are documented

### 3b. Connectors
- **Outlook**: NIH FCOI correspondence, COI Committee notifications, disclosure reminder emails
- **Jira**: FCOI tracking tickets, management plan implementation action items

### 3c. Primary sources (web — verify current requirements)
- **42 CFR Part 50, Subpart F**: ecfr.gov — most current regulatory text
- **NIH FCOI Policy**: grants.nih.gov/grants/policy/coi/
- **PHS FCOI Guidance**: hhs.gov/ohrp/regulations-and-policy/
- **IRS Form 990 Part VI guidance**: irs.gov (for board COI policy disclosure requirements)
- **2 CFR 200.318**: ecfr.gov (procurement COI)

**Citation format**: `[42 CFR §50.xxx, or NIH Grants Policy Statement §x.x, Retrieved YYYY-MM-DD]`

---

## Step 4: Score compliance for each obligation

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Compliant** | 🟢 | Policy, process, and performance records all current and documented |
| **Partial** | 🟡 | Policy/process exists but performance records incomplete, stale, or not confirmable |
| **Non-Compliant** | 🔴 | Required element missing — regulatory risk |

**Risk levels**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | Missing FCOI policy; undocumented FCOIs on active PHS awards; missing management plans; NIH audit in progress |
| 🟠 High | Annual disclosures overdue; training not completed prior to research engagement; sub-recipient certifications missing |
| 🟡 Medium | Management plans in place but not recently re-evaluated; training completed but approaching 4-year renewal |
| 🟢 Low | All documentation current; annual cycle on schedule |

---

## Step 5: Produce output by mode

---

### Mode: `status` — FCOI/COI Dashboard

```markdown
---
title: COI / FCOI Compliance Status
date: YYYY-MM-DD
---

# COI / FCOI Compliance Dashboard

## PHS / NIH FCOI (42 CFR Part 50)
| Obligation | Status | Last Completed | Next Due | Owner |
|-----------|--------|---------------|----------|-------|
| Written FCOI policy | 🟢/🟡/🔴 | YYYY-MM-DD | YYYY-MM-DD | COI Officer |
| Annual disclosure cycle | | | | |
| Investigator training | | | | |
| Active management plans | N plans | | | |
| Sub-recipient certifications | N of N received | | | |
| Public disclosure readiness | | | | |

## Board COI
| Obligation | Status | Last Completed | Owner |
...

## Procurement COI
| Obligation | Status | Owner |
...

## Open Issues
[List any active FCOIs with management plans — no names, describe by status only]
```

---

### Mode: `manage` — Management Plan

```markdown
---
title: FCOI Management Plan — [PI Name/Redacted] — [Project/Award #]
date: YYYY-MM-DD
review_date: YYYY-MM-DD (1 year from today)
status: Draft
---

# FCOI Management Plan

## Identification
- **Investigator**: [name or identifier]
- **Award**: [PHS award number and title]
- **SFI Identified**: [company/entity name; type of interest; approximate value range per 42 CFR §50.605]
- **Relationship to Research**: [how the SFI relates to the design, conduct, or reporting of the research]

## FCOI Determination
- **Determination**: This SFI constitutes / does not constitute a FCOI [select one]
- **Basis**: [reasoning for determination]

## Management Conditions
[Select and customize applicable conditions:]
- [ ] Public disclosure of the FCOI in all publications and presentations arising from the research
- [ ] Appointment of an independent monitor with authority to oversee research
- [ ] Modification of research plan to eliminate conflict
- [ ] Disqualification from participation in portions of research related to the SFI
- [ ] Divestiture of the SFI
- [ ] Severance of relationships that create actual or potential conflict
- [ ] Other: [describe]

## Monitoring and Reporting
- **Monitor** (if applicable): [name/role]
- **Reporting frequency**: [quarterly/annual/milestone-based]
- **Annual re-evaluation date**: YYYY-MM-DD

## Institutional Reporting to PHS
- **Reported to**: [PHS awarding component]
- **Reported on**: YYYY-MM-DD
- **Confirmation**: [reference/confirmation number]

## Signatures
- COI Officer: ____________ Date: ________
- Investigator: ____________ Date: ________
- Department Chair/Dean: ____________ Date: ________
```

---

### Mode: `audit` — Audit-Ready Documentation Package

```markdown
---
title: FCOI Audit Documentation Package
date: YYYY-MM-DD
---

# FCOI Audit Documentation Package

## Documents Assembled
| Document | Location | Last Updated | Status |
|----------|----------|-------------|--------|
| FCOI Policy | [[wiki/compliance/fcoi-policy]] or [SharePoint path] | YYYY-MM-DD | 🟢/🟡/🔴 |
| Training completion records | [location] | YYYY-MM-DD | |
| Annual disclosure records (current cycle) | [location] | YYYY-MM-DD | |
| Active management plans | [count] plans — [location] | | |
| Sub-recipient certifications | [count] received of [count] required | | |
| COI Committee meeting minutes | [date range] | | |

## Gaps (Missing Before Audit)
[Any required document not found — with severity and recommended action]

## Audit Narrative Summary
[2–3 paragraph summary of the FCOI program suitable for an auditor briefing or written response]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write status report to `wiki/compliance/coi-status-YYYY-MM-DD.md`
2. **Management plan** — run `manage` mode for any investigator with an active SFI requiring a plan
3. **Calendar integration** — flag annual disclosure deadline and training renewal dates in `planner/tasks.md`
4. **Policy** — if FCOI policy is missing or stale, offer to run `/the-brain:policy new FCOI`

---

## Quality Rules

- Never record or store individual SFI disclosure details verbatim — reference document locations only; these are sensitive records.
- The $5,000 threshold is the PHS regulatory threshold; the institution's policy may be lower — use whichever is stricter.
- A management plan must exist **before** expenditures begin on a PHS award when an FCOI is identified — timing is a common audit finding.
- Retrospective review must be completed within **120 days** of discovering a late-identified FCOI — flag if this window is approaching or past.
- Training must be completed before the investigator begins PHS-funded research — training completed *after* the fact is a finding.
