---
name: policy
description: Policy registry and review cycle management. Inventories all institutional policies, maps them to regulatory and accreditation requirements, flags overdue reviews and ownership gaps, and identifies standards that lack a corresponding policy. Use when auditing policy currency, preparing for an accreditation review, onboarding a new policy owner, or identifying policy gaps.
argument-hint: "<scope> [all|domain:<domain>|owner:<name>|standard:<ref>] [mode:inventory|gaps|overdue|map|new] — e.g. 'all overdue' or 'domain:research gaps' or 'standard:LCME-3.6 map' or 'new HIPAA minimum necessary'"
---

# /the-brain:policy — Policy Registry & Review Cycle Management

You are managing the institutional policy registry on behalf of the VP of Compliance. Policies are the primary evidence artifact in virtually every compliance audit and accreditation review. Your job is to know what policies exist, whether they are current, who owns them, what requirements they satisfy, and — critically — what is missing.

Every output must be grounded in what is actually documented in the Brain and connected systems. Never assume a policy exists; confirm it.

---

## Step 1: Parse the request

From the user's input, determine:

- **Scope**: which policies to examine
  - `all` — the full institutional policy inventory
  - `domain:<domain>` — policies within a specific compliance domain (see taxonomy below)
  - `owner:<name or role>` — all policies assigned to a specific owner
  - `standard:<ref>` — policies that map (or should map) to a specific standard (e.g., `LCME-3.6`, `MSCHE-Standard-2`, `HIPAA`)

- **Mode**: output format — default to `inventory` if not specified:
  - `inventory` — complete registry: every policy found, mapped to domains and standards, with status
  - `gaps` — policies that SHOULD exist (based on regulatory/accreditation requirements) but are NOT documented in the Brain or connected systems
  - `overdue` — policies past their review date or with no review date assigned
  - `map` — maps a specific standard to the policies that satisfy it (and flags what's missing)
  - `new` — research and draft a policy stub for a new policy topic

---

## Policy Domain Taxonomy

| Code | Domain | Key Requirements Driving Policy |
|------|--------|--------------------------------|
| `GOV` | Governance & Administration | MSCHE Standard 7, LCME Standards 1–2 |
| `ACAD` | Academic Affairs & Curriculum | MSCHE Standard 3, LCME Standards 6–9 |
| `STUDENT` | Student Affairs | MSCHE Standard 4, LCME Standards 10–12, FERPA |
| `ASSESS` | Educational Assessment | MSCHE Standard 5, LCME Standard 8 |
| `RESEARCH` | Research Compliance | IRB (45 CFR 46), NIH, FDA, IACUC, IBC, Export Controls |
| `PRIVACY` | Privacy & Data Security | HIPAA (45 CFR 164), FERPA (34 CFR 99), state law |
| `HR` | Human Resources | FLSA, EEOC, NLRA, ADA, FMLA, OSHA |
| `CLINICAL` | Clinical Operations | TJC, CMS CoPs, DEA, state licensure |
| `GME` | Graduate Medical Education | ACGME SI and CPR requirements |
| `FINANCE` | Financial & Fiscal | MSCHE Standard 6, OMB Circulars, Title IV |
| `SAFETY` | Campus Safety & Security | Clery Act (34 CFR 668.46), OSHA, Title IX |
| `TITLE9` | Title IX & Civil Rights | Title IX (34 CFR 106), Title VI, Section 504, ADA |
| `COI` | Conflicts of Interest | 42 CFR Part 50 (PHS FCOI), institutional COI |

---

## Policy Registry Data Model

Each policy in the registry should have the following attributes. When scanning the Brain and SharePoint, extract as many as are available; flag missing attributes as registry gaps.

| Field | Description |
|-------|-------------|
| `title` | Official policy title |
| `policy_number` | Institutional policy number (if assigned) |
| `domain` | Domain code(s) from taxonomy above |
| `owner` | Office or role responsible for policy maintenance |
| `approving_authority` | Who approved it (Board, President, Dean, etc.) |
| `effective_date` | Date currently effective version was approved |
| `next_review_date` | Scheduled review date |
| `review_frequency` | Annual / Biennial / Triennial / Other |
| `standard_map` | Accreditation/regulatory standards this policy satisfies |
| `brain_location` | `[[wiki/compliance/...]]` or SharePoint path |
| `status` | Current / Stale / Under Revision / Missing |

---

## Step 2: Search the Brain for policies

### 2a. Wiki sub-brain
- `wiki/compliance/` — primary location for compliance-related policy wiki pages
- Search for pages with titles or frontmatter indicating policy content: "policy", "procedure", "standard", "guideline", "code of conduct"
- Check for a policy index or policy registry page at `wiki/compliance/policy-index.md`

### 2b. PM sub-brain
- `pm/projects/` — any policy revision or development projects
- `pm/reports/` — policy audit reports, prior policy gap analyses

### 2c. Raw sources
- `raw/` — any exported policy documents from SharePoint stored as raw files

For every policy found:
- Extract all available registry fields (see data model above)
- Calculate **days since last review** and **days until next review** (use current date)
- Flag if `next_review_date` is missing — policies without scheduled reviews are a common audit finding
- Flag if `owner` is missing — unowned policies are a governance risk

---

## Step 3: Search connected systems

### 3a. SharePoint
This is the primary source for the institutional policy library. Search for:
- Policy manual folders or policy libraries
- Policies by domain (HR policies, research policies, student affairs policies, clinical policies)
- Board-approved policy documents
- Policy acknowledgment records

For each policy found in SharePoint but NOT in the Brain: note it as a Brain sync gap (Brain is missing this policy page).

### 3b. Connectors
- **Outlook/Teams**: policy revision communications, committee approvals, policy review notifications
- **Jira**: open policy revision or development tickets

### 3c. Requirement-driven policy checklist (web verification)
For `gaps` mode, cross-reference the following authoritative requirement lists against the policy inventory to identify missing policies:

**MSCHE-required policies**: msche.org/standards-and-practices/standards-for-accreditation/
**LCME-required policies**: lcme.org/standards — note Elements with explicit "written policy" language
**ACGME-required policies**: acgme.org/what-we-do/accreditation/common-program-requirements/
**HIPAA minimum required policies**: hhs.gov/hipaa/for-professionals/privacy/guidance/
**Title IX required policies**: 34 CFR §106.45 (grievance procedures), §106.8 (coordinator), §106.44 (response)
**Clery Act required policies**: 34 CFR §668.46

---

## Step 4: Produce output by mode

---

### Mode: `inventory` — Full Policy Registry

```markdown
---
title: Institutional Policy Registry
date: YYYY-MM-DD
scope: <all|domain|owner|standard>
---

# Policy Registry: <Scope>

## Registry Summary
- **Total Policies Identified**: N
- **Current**: N (🟢)
- **Stale / Overdue for Review**: N (🟡)
- **Missing Required Policies**: N (🔴)
- **Missing Owner**: N
- **Missing Review Date**: N

---

## Policy Inventory

| Policy Title | # | Domain | Owner | Effective | Next Review | Standards | Status |
|-------------|---|--------|-------|-----------|-------------|-----------|--------|
| [title] | [#] | [domain] | [owner] | YYYY-MM-DD | YYYY-MM-DD | [refs] | 🟢/🟡/🔴 |
...

## Brain Sync Gaps
Policies found in SharePoint but not yet in the Brain:
1. [policy title] — [SharePoint location]
```

---

### Mode: `gaps` — Missing Policies

```markdown
---
title: Policy Gap Analysis
date: YYYY-MM-DD
---

# Policy Gap Analysis

Policies required by applicable standards that are NOT documented in the Brain or SharePoint.

| # | Required By | Standard Reference | Policy Description | Risk | Recommended Owner |
|---|-------------|-------------------|-------------------|------|------------------|
| 1 | LCME | Standard 3.6 | Student mistreatment reporting and response | 🔴 Critical | Dean of Students |
| 2 | Title IX | 34 CFR §106.45 | Grievance procedures for sex discrimination | 🔴 Critical | Title IX Coordinator |
...

## Summary by Domain
| Domain | Required Policies | Found | Missing |
|--------|-----------------|-------|---------|
| TITLE9 | N | N | N |
...
```

---

### Mode: `overdue` — Review Cycle Violations

```markdown
---
title: Overdue Policy Reviews
date: YYYY-MM-DD
---

# Overdue Policy Reviews

## Past Due — Immediate Action Required

| Policy | Owner | Last Reviewed | Overdue By | Standard(s) Affected |
|--------|-------|--------------|-----------|---------------------|
| [title] | [owner] | YYYY-MM-DD | N days | [refs] |
...

## Due Within 90 Days — Schedule Now

| Policy | Owner | Due Date | Days Remaining |
|--------|-------|----------|---------------|
...

## No Review Date Assigned — Governance Gap

| Policy | Owner | Last Known Review |
|--------|-------|------------------|
...
```

---

### Mode: `map` — Standard-to-Policy Mapping

```markdown
---
title: Policy Map — <Standard Reference>
standard: <ref>
date: YYYY-MM-DD
---

# Policy Map: <Standard Reference>

## Standard Requirements
[Summary of what the standard requires re: policies]

## Policies Satisfying This Standard

| Policy | Status | Owner | Last Review | Gaps |
|--------|--------|-------|------------|------|
| [title] | 🟢/🟡/🔴 | [owner] | YYYY-MM-DD | [what's missing] |
...

## Unsatisfied Requirements
[Elements of the standard that no policy addresses]
```

---

### Mode: `new` — Policy Stub Draft

When drafting a new policy, produce:

```markdown
---
title: DRAFT — <Policy Title>
domain: <domain code>
owner: <recommended owner>
approving_authority: <recommended approver>
effective_date: [PENDING]
next_review_date: [PENDING — set to 1 year from effective date]
review_frequency: Annual
standard_map: [applicable standards]
status: Draft
---

# <Policy Title>

## Purpose
[1–2 sentences: why this policy exists and what it is designed to achieve]

## Scope
[Who is covered: employees, students, faculty, affiliates, vendors]

## Policy Statement
[The core rule(s). Numbered if multiple. Plain language.]

## Procedures
[Step-by-step implementation, if applicable]

## Roles and Responsibilities
| Role | Responsibility |
|------|---------------|
| [Office/Title] | [What they must do] |

## Definitions
[Key terms used in the policy]

## Related Policies
[Cross-references to related institutional policies]

## Regulatory Authority
[Statute, regulation, or accreditation standard that requires or informs this policy]
- [Citation 1]
- [Citation 2]

## Revision History
| Date | Version | Description | Approved By |
|------|---------|-------------|------------|
| YYYY-MM-DD | 1.0 | Initial draft | [pending] |
```

---

## Step 5: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write registry or gap analysis to `wiki/compliance/policy-registry-YYYY-MM-DD.md`
2. **Create tasks** — add overdue reviews or missing policies as tasks in `planner/tasks.md` with due dates
3. **Drill down** — run `map` mode for any standard where policy coverage is incomplete
4. **New policy** — run `new` mode for any identified missing policy

---

## Quality Rules

- Never assume a policy exists because it is required — confirm via Brain or SharePoint.
- A policy found in SharePoint but absent from the Brain is a documentation gap, not a compliance gap — but note both.
- A policy with no review date is ungoverned — flag it regardless of how recently it was last reviewed.
- Policies that have not been reviewed within their stated cycle are stale for accreditation purposes — LCME and MSCHE evaluators will ask when policies were last reviewed and who approved them.
- "Policy" means a Board- or Dean-approved institutional policy, not a departmental procedure — distinguish between the two in the inventory.
