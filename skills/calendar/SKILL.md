---
name: calendar
description: Compliance deadline calendar. Consolidates all regulatory reporting deadlines, accreditation milestones, certification cycles, and policy review dates into a unified calendar view. Flags what is due soon, overdue, and unowned. Use at the start of each quarter, before a board meeting, or whenever the VP of Compliance needs a complete picture of upcoming obligations.
argument-hint: "<window> [30|60|90|180|365|all] [mode:calendar|overdue|quarter|annual] — e.g. '90' or '180 calendar' or 'all annual' or 'overdue'"
---

# /the-brain:calendar — Compliance Deadline Calendar

You are building the VP of Compliance's master compliance calendar. Your role is to surface every regulatory reporting deadline, accreditation milestone, certification renewal, and policy review date that the institution must meet — and to flag what is approaching, what is overdue, and what has no assigned owner.

Missing a compliance deadline can mean fines, loss of federal funding, or accreditation sanctions. This calendar is the early-warning system.

---

## Step 1: Parse the request

From the user's input, determine:

- **Window**: how far ahead (and behind) to look — default to `90` days if not specified
  - `30` / `60` / `90` / `180` / `365` — days from today
  - `all` — every known deadline regardless of date

- **Mode**: output format — default to `calendar` if not specified:
  - `calendar` — chronological list of all deadlines in the window; color-coded by days remaining
  - `overdue` — only items past due; critical-first
  - `quarter` — organized by academic/fiscal quarter; useful for planning meetings
  - `annual` — full 12-month compliance calendar; one row per month

---

## Master Compliance Deadline Inventory

The following is the authoritative set of compliance deadlines to track. For each, search the Brain and connected systems to determine: (a) whether a Brain page or task tracks this deadline, (b) the assigned owner, and (c) the status for the current cycle.

### Federal Regulatory Reporting

| Deadline | Authority | Typical Due Date | Owner | Notes |
|----------|-----------|-----------------|-------|-------|
| IPEDS Fall Enrollment Survey | NCES | Late Oct – Nov | IR / Registrar | Keyholder must certify |
| IPEDS Winter Data Collection (Finance, Human Resources) | NCES | Jan – Feb | Finance / HR | |
| IPEDS Spring Data Collection (Completions, Grad Rates, Outcome Measures) | NCES | Feb – Apr | Registrar / IR | |
| IPEDS Student Financial Aid Survey | NCES | Mar – Apr | Financial Aid | |
| Clery Act Annual Security Report (ASR) | 34 CFR 668.46 | **October 1** | Campus Safety / Compliance | Hard federal deadline |
| Clery Act Daily Crime Log | 34 CFR 668.46 | Ongoing / 2 business days | Campus Safety | |
| Title IV Financial Responsibility Composite Score | Dept. of Education | Annual (with audited financials) | Finance / CFO | Triggers if below 1.5 |
| Gainful Employment Disclosures | Dept. of Education | Annually | Financial Aid / Registrar | |
| Cohort Default Rate (CDR) notice and appeals window | Dept. of Education | September | Financial Aid | |
| Net Price Calculator — update | HEA §132 | Annual | Financial Aid / IT | |
| Consumer Information Disclosures (all required) | HEA §485 | Annual audit | Compliance | Checklist required |
| OSHA 300A Summary posting | OSHA | **February 1 – April 30** | HR / Facilities | |
| OSHA 300 log maintenance | OSHA | Ongoing | HR / EHS | |
| EEOC EEO-1 filing | EEOC | Annual (typically May–July) | HR | For institutions with 100+ employees |

### Accreditation Milestones

| Deadline | Authority | Cycle / Due Date | Owner | Notes |
|----------|-----------|-----------------|-------|-------|
| MSCHE Annual Institutional Update (AIU) | MSCHE | **July 1** | Provost / Compliance | Submitted via MSCHE Portal |
| MSCHE Periodic Review Report (PRR) | MSCHE | Year 7 or 8 of cycle | Provost / Compliance | Requires self-study process |
| MSCHE Substantive Change notifications | MSCHE | 6–12 months prior to change | Compliance / Provost | Prior approval may be required |
| LCME Annual Medical Education Report (AMER) | LCME | Annual — check LCME portal for date | Dean / Compliance | |
| LCME DCI submission | LCME | 12–18 months before site visit | Dean / Compliance | Full self-study document |
| LCME Interim Report | LCME | Per action letter | Dean / Compliance | Specific to each institution's letter |
| ACGME Sponsoring Institution Annual Report | ACGME | Annual via ADS | DIO / GME Office | |
| ACGME Annual Program Evaluations (APE) | ACGME | Annual — each program | Program Directors | Reviewed by GMEC |
| ACGME Annual Institutional Review (AIR) | ACGME | Annual — GMEC conducted | DIO / GMEC | Must be documented in GMEC minutes |
| ACGME WebADS updates (faculty, complement) | ACGME | Ongoing / annual certification | Program Coordinators | |
| CLER Visit (if scheduled) | ACGME | Per ACGME notification | DIO / Compliance | Typically 2–4 week notice |
| Joint Commission Survey (if applicable) | TJC | Rolling / 18–36 month cycle | Clinical Compliance | Unannounced after first survey |
| State Medical Board institutional reporting | State | Annual or per state requirement | Legal / Compliance | Varies by state |
| State authorization renewals | State(s) of operation | Per state cycle | Compliance / Legal | Must cover all states where students receive instruction |

### Research Compliance Cycles

| Deadline | Authority | Cycle | Owner | Notes |
|----------|-----------|-------|-------|-------|
| IRB continuing reviews (active protocols) | 45 CFR 46 | Per protocol approval period | Research Compliance / PIs | PI responsibility; tracked by IRB |
| FCOI annual disclosures | 42 CFR Part 50 Subpart F | Annual (typically pre-fiscal year) | Research Compliance / COI Officer | All significant financial interest holders |
| FCOI retrospective review (new SFI identified mid-project) | 42 CFR §50.605 | Within 60 days of identification | Research Compliance | |
| NIH Other Support / Foreign Component updates | NIH GPS | Per grant cycle | PI / Sponsored Programs | RPPR submissions |
| Research Progress Reports (RPPRs) | NIH / Sponsor | Annual + closeout | Sponsored Programs / PIs | 120 days before budget period ends |
| IACUC continuing reviews / 3-year de novo reviews | PHS Policy / AWA | Per protocol | IACUC / Research Compliance | |
| IBC annual reviews | NIH Guidelines | Annual | IBC / Research Compliance | |
| Export Control training renewals | EAR / ITAR | Annual (institutional policy) | Research Compliance / Legal | |

### Title IX and Civil Rights

| Deadline | Authority | Cycle | Owner | Notes |
|----------|-----------|-------|-------|-------|
| Title IX training — staff, faculty, investigators, advisors | 34 CFR §106.45(b)(1)(iii) | Annual | Title IX Coordinator | Training content must be publicly posted |
| Title IX policy annual review and publication | 34 CFR §106.8 | Annual | Title IX Coordinator | Must be distributed to all students and employees |
| Title IX Coordinator designation — publish name, title, contact | 34 CFR §106.8(a) | Ongoing / review annually | Title IX Coordinator | Catalog, website, all student communications |
| Clery Act/VAWA SAVE Act training | 34 CFR §668.46(j)(2) | Annual | Campus Safety / Title IX | All new students and employees |

### Financial and Audit Cycles

| Deadline | Authority | Cycle | Owner | Notes |
|----------|-----------|-------|-------|-------|
| Audited financial statements | Board / Lenders / MSCHE | Annual — typically 90–120 days after FY close | CFO / Finance | Submitted to MSCHE if requested |
| Single Audit (if >$750K federal expenditures) | 2 CFR Part 200 | Annual — 9 months after FY close | Finance / External Auditors | A-133 threshold |
| Board of Trustees meeting cycle | Bylaws | Per institutional calendar | Board Secretary / President | Governance evidence for MSCHE / LCME |
| Policy review cycle (overdue policies) | Institutional | Per policy review schedule | Compliance / Policy Owners | See `/the-brain:policy` |

---

## Step 2: Search the Brain for deadline tracking

### 2a. Planner sub-brain
- `planner/tasks.md` — any compliance deadlines already tracked as tasks
- `planner/dashboard.md` — current priorities mentioning compliance dates
- `planner/YYYY/MM/` — daily files mentioning deadline submissions or completions

### 2b. PM sub-brain
- `pm/projects/` — any projects with deadline milestones (LCME DCI, MSCHE AIU, IPEDS, etc.)
- `pm/reports/` — prior year submissions that anchor the current year's due dates

### 2c. Wiki sub-brain
- `wiki/compliance/` — any compliance calendar pages, deadline trackers, or cycle documentation

### 2d. Raw sources
- `raw/` — MSCHE correspondence with due dates, LCME action letters with reporting deadlines, ACGME annual report notifications

---

## Step 3: Search connected systems

- **Outlook**: calendar events or emails containing compliance deadlines, submission confirmations, renewal notices
- **SharePoint**: prior year submissions (use to infer current year due dates); IPEDS keyholder portal access records; accreditation portal submissions

---

## Step 4: Calculate deadline status

For each deadline, calculate:
- **Days until due** = due date − today
- **Status**:

| Status | Symbol | Condition |
|--------|--------|-----------|
| **Overdue** | 🔴 | Past due; not confirmed complete |
| **Due within 30 days** | 🟠 | 1–30 days remaining |
| **Due within 90 days** | 🟡 | 31–90 days remaining |
| **Due within 180 days** | 🟢 | 91–180 days remaining |
| **Future / Confirmed Complete** | ⚪ | >180 days out, or confirmed submitted this cycle |

Flag as **Unowned** (⚠️) if no assigned owner is found in the Brain or connected systems.

---

## Step 5: Produce output by mode

---

### Mode: `calendar` — Chronological Deadline View

```markdown
---
title: Compliance Calendar — <Window>-Day Lookout
date: YYYY-MM-DD
window: <N> days
---

# Compliance Calendar: Next <N> Days

## 🔴 Overdue — Immediate Action Required

| Deadline | Authority | Was Due | Owner | Status |
|----------|-----------|---------|-------|--------|
| [deadline] | [authority] | YYYY-MM-DD | [owner or ⚠️ Unowned] | [action needed] |

## 🟠 Due Within 30 Days

| Deadline | Authority | Due Date | Days Left | Owner | Brain/Task Link |
|----------|-----------|----------|-----------|-------|----------------|
...

## 🟡 Due Within 90 Days

| Deadline | Due Date | Days Left | Owner | Notes |
...

## 🟢 Due 91–180 Days Out

| Deadline | Due Date | Owner | Notes |
...

## ⚠️ Unowned Deadlines (any window)

| Deadline | Due Date | Suggested Owner |
...
```

---

### Mode: `annual` — Full 12-Month Calendar

```markdown
---
title: Annual Compliance Calendar — AY YYYY–YYYY
date: YYYY-MM-DD
---

# Annual Compliance Calendar

## July
| Date | Deadline | Authority | Owner | Status |
|------|----------|-----------|-------|--------|
| Jul 1 | MSCHE Annual Institutional Update | MSCHE | Provost | ⚪/🟢/🟡/🟠/🔴 |
...

## August
...

## September
...

## October
| Oct 1 | **Clery Act Annual Security Report** | 34 CFR 668.46 | Campus Safety | — |
...

[Continue through June]

## Recurring / Ongoing Obligations
| Obligation | Frequency | Owner | Next Due |
|-----------|-----------|-------|----------|
| IRB continuing reviews | Per protocol | Research Compliance / PIs | Varies |
| Clery Daily Crime Log | Within 2 business days of incident | Campus Safety | Ongoing |
...
```

---

### Mode: `overdue` — Past-Due Items Only

```markdown
---
title: Overdue Compliance Deadlines
date: YYYY-MM-DD
---

# Overdue Compliance Deadlines

| # | Deadline | Was Due | Days Overdue | Owner | Authority | Recommended Action |
|---|----------|---------|-------------|-------|-----------|-------------------|
| 1 | [deadline] | YYYY-MM-DD | N | [owner] | [authority] | [action] |
...

## Escalation Recommendations
[Any overdue items that carry fine risk, funding risk, or accreditation risk — escalate immediately]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write calendar to `wiki/compliance/compliance-calendar-YYYY.md`
2. **Create tasks** — add all overdue and near-term deadlines to `planner/tasks.md` with due dates and owners
3. **Set up project** — scaffold an IPEDS, Clery, or accreditation project in `pm/projects/` if work tracking is needed
4. **Policy review integration** — run `/the-brain:policy overdue` to integrate policy review deadlines

---

## Quality Rules

- Today's date is known at runtime — always calculate `days until due` from the actual current date.
- When a prior year submission is found in the Brain, use it to confirm the current year deadline (most annual deadlines are fixed dates or follow a predictable cycle).
- If a deadline's status cannot be confirmed (submitted or not), mark it as **status unknown** — never assume completion.
- Flag any deadline with no Brain record, no task, and no SharePoint evidence — these are the most dangerous invisible obligations.
- Clery Act October 1 deadline and MSCHE July 1 AIU are hard federal/accreditor deadlines — always elevate these in visibility regardless of days remaining.
