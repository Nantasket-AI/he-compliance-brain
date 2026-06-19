---
name: compliance
description: Deep research on compliance topics within a medical school. Covers regulatory (HIPAA, FERPA, Title IX, Clery Act), accreditation (LCME, ACGME), clinical (Joint Commission, CMS, state licensure), and research compliance (IRB, NIH, FDA, COI). Produces structured briefs, gap analyses, remediation plans, or permanent wiki pages. Use when researching any compliance requirement, audit finding, or policy question.
argument-hint: "<topic> [brief|gap|remediate|wiki] — e.g. 'HIPAA minimum necessary standard brief' or 'LCME accreditation gap analysis' or 'IRB continuing review remediate'"
---

# /the-brain:compliance — Medical School Compliance Research

You are performing deep compliance research for a medical school. Your output must be accurate, well-cited, and actionable. Every factual claim about a regulatory or accreditation requirement must be traceable to a primary source.

---

## Step 1: Parse the request

From the user's input, determine:

- **Topic**: the specific compliance area, requirement, standard, or policy question
- **Domain**: which compliance domain(s) apply (see taxonomy below) — infer if not stated
- **Mode**: the output format requested — default to `brief` if not specified:
  - `brief` — structured compliance summary with citations and risk flags
  - `gap` — gap analysis comparing current Brain knowledge or stated practice against the standard
  - `remediate` — step-by-step remediation/action plan for a specific finding or deficiency
  - `wiki` — research and file a permanent compliance wiki page to `wiki/compliance/`

**Compliance Domain Taxonomy**:

| Code | Domain | Key Authorities |
|------|--------|-----------------|
| `REG` | Regulatory | HIPAA/HITECH, FERPA, Title IX, Title VI, Clery Act, ADA/Section 504, OSHA |
| `ACCRED` | Accreditation | LCME (MD), ACGME (GME/residency), ABA (basic science), COCA (DO), CODA (dental), SACSCOC (institutional) |
| `CLINICAL` | Clinical / Patient Care | The Joint Commission (TJC), CMS Conditions of Participation, DEA, state medical board & health dept |
| `RESEARCH` | Research | IRB (45 CFR 46 / Common Rule), NIH grants policy, FDA 21 CFR, COI/financial disclosure, IACUC |
| `PRIVACY` | Privacy & Data | HIPAA Privacy/Security Rules, state breach notification laws, GDPR (if applicable) |
| `HR` | Employment & HR | FLSA, I-9/E-Verify, EEOC, NLRA, state employment law |

If the topic spans multiple domains, note all that apply and research each.

---

## Step 2: Search the Brain

Navigate the Brain's existing compliance knowledge before going external. Follow the top-down tree search from CLAUDE.md.

1. Check `wiki/compliance/` — read `wiki/compliance/index.md` (if it exists) for existing compliance pages on this topic
2. Check `wiki/concepts/` — any concept pages with compliance implications
3. Check `pm/projects/` — active compliance projects, audit remediation work, or accreditation projects
4. Check `pm/reports/` — prior compliance reports, audit findings, or self-study documents
5. Check `planner/tasks.md` — open compliance action items

For each Brain page found:
- Note the **specific claim**, source section, and last-updated date
- Flag any **stale entries** (over 12 months old for regulatory content; over 6 months for accreditation cycles)
- Note **gaps**: what the Brain does NOT yet know that is needed to answer the question

---

## Step 3: Gather live source data

Supplement Brain knowledge with live sources. Query in this order:

### 3a. Internal policy documents (SharePoint)
Search SharePoint for the institution's own policies related to the topic:
- Policy manuals, standard operating procedures (SOPs)
- Audit reports, corrective action plans
- Accreditation self-study documents
- Committee meeting minutes (Compliance Committee, IRB, IACUC, etc.)

### 3b. Connector data
- **Outlook/Teams**: recent communications from the Compliance Office, General Counsel, or relevant committee chairs
- **Jira**: open compliance remediation tickets or audit tracking items
- **Confluence**: compliance runbooks or living procedure documents

### 3c. Primary regulatory & accreditation sources (web)
Consult primary sources directly. Use exact citations:

| Domain | Primary Sources |
|--------|----------------|
| HIPAA | HHS OCR: hhs.gov/hipaa — cite specific rule sections (45 CFR §164.xxx) |
| FERPA | Dept. of Education: studentprivacy.ed.gov — cite 34 CFR Part 99 |
| Title IX | Dept. of Education OCR: ed.gov/ocr — cite 34 CFR Part 106 |
| Clery Act | Dept. of Education FSA: studentaid.gov/clery — cite 34 CFR Part 668.46 |
| LCME | lcme.org — cite specific Element (e.g., LCME Element 1.1) |
| ACGME | acgme.org — cite Common Program Requirements section |
| TJC | jointcommission.org — cite specific standard (e.g., EC.02.06.01) |
| CMS | cms.gov — cite Conditions of Participation (42 CFR Part 482) |
| Common Rule | hhs.gov/ohrp — cite 45 CFR 46 subpart and section |
| NIH | grants.nih.gov — cite Grants Policy Statement section |
| FDA | fda.gov — cite 21 CFR part and section |

**Citation format**: `[Source Name, §Reference, Date Retrieved]`

---

## Step 4: Synthesize findings

Organize the research by mode:

---

### Mode: `brief` — Compliance Brief

Structure the brief using this template:

```markdown
---
title: Compliance Brief — <Topic>
domain: <REG|ACCRED|CLINICAL|RESEARCH|PRIVACY|HR>
standard: <specific regulation, element, or standard cited>
date: YYYY-MM-DD
status: current | stale | unverified
---

# Compliance Brief: <Topic>

## Requirement Summary
<!-- What the law/standard actually requires. Plain-language statement first, then precise regulatory language. -->

## Applicable Authority
<!-- Name of the regulatory body, exact rule/standard citation, and effective date. -->
- **Authority**: [name]
- **Citation**: [CFR/Element/Standard reference]
- **Effective Date**: [date]
- **Enforcement Body**: [HHS OCR / Dept of Ed / TJC / LCME / etc.]

## Current Institutional Practice
<!-- What the Brain (and live connectors) reveal about current practice. Cite specific Brain pages or SharePoint documents. If unknown, state explicitly. -->

## Risk Flags
<!-- Items where current practice is unclear, potentially deficient, or not evidenced in the Brain. -->
- 🔴 **High**: [description]
- 🟡 **Medium**: [description]
- 🟢 **Low / Informational**: [description]

## Key Deadlines & Reporting Cycles
<!-- Recurring submission deadlines, reporting periods, or audit cycles. -->

## Sources
<!-- Full citations for all claims. -->
1. [Source, §Ref, Retrieved YYYY-MM-DD]
```

---

### Mode: `gap` — Gap Analysis

Structure the gap analysis using this template:

```markdown
---
title: Gap Analysis — <Topic> vs. <Standard/Requirement>
domain: <domain code>
standard: <citation>
date: YYYY-MM-DD
---

# Gap Analysis: <Topic>

## Standard Being Assessed
[Full citation and plain-language description of the requirement]

## Assessment Method
[What sources were reviewed: Brain pages, SharePoint docs, connector data, primary sources]

## Findings

| # | Requirement Element | Current State | Gap | Severity |
|---|---------------------|--------------|-----|----------|
| 1 | [element] | [what evidence shows] | [what is missing or unclear] | 🔴 High / 🟡 Medium / 🟢 Low |

## Summary
- **Total Elements Assessed**: N
- **Met / Evidenced**: N
- **Partial / Unclear**: N
- **Not Met / Missing**: N
- **Overall Risk Level**: High / Medium / Low

## Recommended Next Steps
[Top 3–5 priority actions based on severity]

## Sources
[Citations]
```

---

### Mode: `remediate` — Remediation Plan

Structure the remediation plan using this template:

```markdown
---
title: Remediation Plan — <Finding or Deficiency>
domain: <domain code>
standard: <citation>
finding_date: YYYY-MM-DD
date: YYYY-MM-DD
---

# Remediation Plan: <Finding>

## Finding Description
[Precise statement of the deficiency or non-conformance, with citation to the standard]

## Root Cause
[Why this gap exists — based on Brain context and connector data]

## Remediation Actions

| # | Action | Owner | Due Date | Evidence of Completion |
|---|--------|-------|----------|------------------------|
| 1 | [action] | [role/person] | YYYY-MM-DD | [what artifact proves done] |

## Monitoring & Sustainability
[How will the institution confirm this stays remediated — policy update, recurring audit, training cadence, etc.]

## Escalation Path
[Who is notified if actions are not completed on time — Compliance Officer, General Counsel, Board, accreditor]

## Sources
[Citations to standard, prior findings, Brain pages]
```

---

### Mode: `wiki` — File a Permanent Compliance Wiki Page

Create or update a page in `wiki/compliance/` using this template:

```markdown
---
title: <Topic> — Compliance Reference
type: compliance-reference
domain: <domain code>
standard: <citation>
last_reviewed: YYYY-MM-DD
review_cycle: annual | biennial | accreditation-cycle
status: current
raw_source: [[raw/YYYY-MM-DD-slug]] (if applicable)
---

# <Topic>

## Overview
[Plain-language description of the compliance requirement and why it matters to the institution]

## Applicable Authority
- **Regulation/Standard**: [full citation]
- **Enforcement Body**: [name]
- **Effective Date / Last Amended**: [date]

## Institutional Requirements
[What the institution must specifically do to comply — derived from both the standard and institutional policy]

## Key Contacts
[Compliance Officer, department heads, or committees responsible]

## Reporting & Deadlines
[Submission calendar, reporting cycles, self-study schedules]

## Related Brain Pages
- [[wiki/compliance/...]] — related standards
- [[pm/projects/...]] — active compliance projects
- [[pm/reports/...]] — audit findings or self-study docs

## Sources
1. [Citation, Retrieved YYYY-MM-DD]
```

After writing the wiki page:
- Update (or create) `wiki/compliance/index.md` — add an entry for the new page under the appropriate domain section
- If `wiki/compliance/index.md` does not exist, create it with a domain-grouped index structure

---

## Step 5: Surface contradictions and knowledge gaps

Before finalizing output, check for:

- **Contradictions**: Does the Brain contradict the primary source? If yes, note using `> [!conflict]` callout and explain the discrepancy.
- **Stale Brain content**: Flag any Brain pages that appear outdated relative to the current regulatory version.
- **Missing institutional evidence**: Note where the institution's compliance posture is simply unknown — the Brain has no record and SharePoint surfaced nothing. These are the highest-priority research gaps.

---

## Step 6: Present output

Present the full output in the appropriate template format from Step 4.

**For `brief`, `gap`, and `remediate` modes**: display inline in the conversation. Offer to file the output to `wiki/compliance/` as a permanent page at the end.

**For `wiki` mode**: write the file to `wiki/compliance/<slug>.md` and update `wiki/compliance/index.md`. Confirm the path and a one-sentence summary of what was filed.

---

## Step 7: Log

Append to `log.md`:

```
## [YYYY-MM-DD] compliance | <mode> | <domain code>
Topic: <topic>. Mode: <mode>. Domains: <codes>. Sources consulted: Brain (<N pages>), SharePoint (<N docs>), web (<N primary sources>). Filed: [[wiki/compliance/<slug>]] (if wiki mode). Risk flags: <High N / Medium N / Low N> (if applicable).
```
