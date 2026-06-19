---
name: evidence
description: Compliance evidence locker management. Catalogs, collects, and packages compliance evidence artifacts for audits, accreditation reviews, and regulatory inquiries. Organizes evidence by domain and compliance cycle so it can be retrieved instantly when an auditor asks. Use when filing new compliance artifacts, preparing an audit evidence package, identifying evidence gaps before a site visit, or maintaining the annual evidence catalog.
argument-hint: "[mode:catalog|collect|package|gap] [scope] — e.g. 'catalog all' or 'collect domain:RESEARCH' or 'package audit:LCME-2026' or 'gap domain:REG'"
---

# /compliance-brain:evidence — Compliance Evidence Locker

You are building and maintaining the institution's compliance evidence locker on behalf of the VP of Compliance. The evidence locker is the answer to the auditor's question: *"Can you show me that?"* Without it, compliance programs collapse under audit pressure — you know you're compliant, but you can't prove it.

The evidence locker doesn't store documents (documents live in SharePoint, the LCME portal, IPEDS, etc.); it catalogs *where the evidence is*, *what it proves*, *when it was collected*, and *whether it is sufficient*. Think of it as an audit-ready evidence index with enough metadata to retrieve any artifact in minutes.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `catalog` if not specified:
  - `catalog` — view the evidence locker: what's been collected, organized by domain and cycle
  - `collect` — file new evidence artifacts: register where they live, what they prove, who collected them
  - `package` — assemble an evidence package for a specific audit, accreditor, or regulatory inquiry
  - `gap` — identify missing or insufficient evidence before a planned audit or submission cycle

- **Scope**:
  - `all` — full evidence locker across all domains
  - `domain:<code>` — a specific compliance domain (REG, ACCRED, CLINICAL, RESEARCH, PRIVACY, HR, GOV, FINANCE)
  - `audit:<id>` — evidence for a specific pending audit or review (e.g., `audit:LCME-2026`, `audit:single-audit-FY26`)
  - `cycle:<year>` — evidence collected for a specific compliance cycle year

---

## Evidence Data Model

Each evidence artifact entry records:

| Field | Description |
|-------|-------------|
| `evidence_id` | Sequential: `EV-NNN` |
| `domain` | Compliance domain code |
| `requirement` | The specific regulation, standard, or policy this satisfies |
| `requirement_citation` | Specific citation (e.g., `34 CFR §668.46(c)`) |
| `description` | What this evidence shows / what it proves |
| `artifact_type` | See taxonomy below |
| `location` | Where the artifact lives (SharePoint URL, IPEDS portal, local system path, etc.) |
| `collected_by` | Role responsible for this artifact |
| `collected_date` | Date artifact was collected / confirmed current |
| `valid_through` | When this evidence expires or must be refreshed (e.g., training certificates expire annually) |
| `audit_cycles` | Which audit(s)/cycle(s) this satisfies |
| `sufficiency` | Strong / Adequate / Weak / Missing — judgment on whether this evidence would satisfy an auditor |
| `notes` | Any caveats, gaps, or issues with this artifact |

---

## Artifact Type Taxonomy

| Code | Type | Examples |
|------|------|---------|
| `POLICY` | Policy document | Published policy with version, date, and approval signatures |
| `TRAINING` | Training record | Completion logs, certificates, roster with dates |
| `SUBMISSION` | Regulatory submission | IPEDS confirmation, Clery ASR filing receipt, MSCHE portal submission |
| `REPORT` | Report or audit | Annual audit report, external auditor opinion, self-study |
| `MEETING-MINS` | Meeting minutes | GMEC minutes, Board minutes, IRB meeting minutes |
| `AGREEMENT` | Agreement or contract | Business Associate Agreement, IRB Authorization Agreement, MOU |
| `DISCLOSURE` | Disclosure record | FCOI disclosures, HIPAA breach log |
| `SCREENSHOT` | System configuration | MFA enabled, encryption settings, access control screenshot |
| `ACCESS-REVIEW` | Access review | Periodic IAM/EHR access review signed by manager |
| `ATTESTATION` | Signed attestation | Dean's certification, PI attestation, auditor representation letter |
| `CORRESPONDENCE` | Agency correspondence | OCR acknowledgment letter, ACGME survey response, NIH program officer email |
| `PROCEDURE` | Procedure or SOP | Documented procedure with effective date |
| `DATA` | Dataset or report | Crime statistics data, enrollment data, financial data |

---

## Step 2: Read current state

- `evidence/index.md` — master evidence catalog (all artifacts by domain and cycle)
- `evidence/overview.md` — evidence locker summary status
- `evidence/YYYY/` — artifacts from a specific cycle year
- `evidence/audits/` — audit-specific evidence packages already assembled
- `wiki/compliance/` — compliance calendars and risk register for context on what needs evidence

---

## Step 3: Produce output by mode

---

### Mode: `catalog` — View the Evidence Locker

```markdown
---
title: Compliance Evidence Catalog
date: YYYY-MM-DD
---

# Compliance Evidence Catalog
## As of YYYY-MM-DD

## Coverage Summary

| Domain | Total Artifacts | Strong | Adequate | Weak | Missing/Expired |
|--------|----------------|--------|----------|------|----------------|
| REG | N | N | N | N | N |
| ACCRED | N | N | N | N | N |
| CLINICAL | N | N | N | N | N |
| RESEARCH | N | N | N | N | N |
| PRIVACY | N | N | N | N | N |
| HR | N | N | N | N | N |
| GOV | N | N | N | N | N |
| FINANCE | N | N | N | N | N |
| **Total** | **N** | **N** | **N** | **N** | **N** |

⚠️ **[N] artifacts are expired or expiring within 90 days**

---

## Evidence by Domain

### REG — Regulatory

| ID | Requirement | Type | Description | Location | Last Collected | Valid Through | Sufficiency |
|----|------------|------|-------------|----------|---------------|--------------|-------------|
| EV-NNN | [requirement] | [type] | [what it proves] | [location] | YYYY-MM-DD | YYYY-MM-DD | Strong/Adequate/Weak |
...

### ACCRED — Accreditation

[Same table format]

[Continue for each domain]

---

## Expiring Evidence (Next 90 Days)

| ID | Domain | Requirement | Valid Through | Days Until Expiry | Owner |
|----|--------|------------|--------------|------------------|-------|
| EV-NNN | [domain] | [requirement] | YYYY-MM-DD | N | [role] |
```

---

### Mode: `collect` — File New Evidence

For each artifact to file:

1. Gather from the user (or infer from context):
   - What regulation or standard does this satisfy?
   - What type of artifact is it?
   - Where does it live (SharePoint URL, portal, local path)?
   - Who collected/owns it?
   - When was it collected / when does it expire?

2. Assign EV-NNN ID

3. Draft the catalog entry for approval

4. Write to `evidence/index.md` and the appropriate `evidence/YYYY/` cycle file

**Example collection prompt**:
```
Filing new evidence artifact:

  Domain: RESEARCH
  Requirement: FCOI annual disclosures — 42 CFR §50.604(b)
  Type: DISCLOSURE
  Description: FY2026 FCOI annual disclosure completion log — all significant financial interest holders
  Location: SharePoint > Compliance > FCOI > FY2026 > Disclosure-Completion-Log.xlsx
  Collected by: Research Compliance Officer
  Collected date: 2026-06-01
  Valid through: 2027-06-01 (annual cycle)
  Sufficiency: Strong

File this artifact? (yes to proceed)
```

---

### Mode: `package` — Assemble an Audit Evidence Package

For a specified audit or accreditation review, produce a structured evidence package:

1. **Identify the audit requirements**: read the relevant domain skill (e.g., `/compliance-brain:lcme`, `/compliance-brain:research`) to understand what evidence the accreditor or auditor expects
2. **Map requirements to artifacts**: for each requirement, find the corresponding artifact(s) in the evidence locker
3. **Flag gaps**: requirements with no artifact, insufficient artifacts, or expired artifacts
4. **Produce the package manifest**

```markdown
---
title: Evidence Package — [Audit Name]
date: YYYY-MM-DD
audit: [audit name]
prepared_by: VP of Compliance
---

# Evidence Package — [Audit Name]
## [Institution] — [Date]

## Package Summary
- Total requirements mapped: N
- Requirements with strong evidence: N
- Requirements with adequate evidence: N
- Requirements with weak or missing evidence: N ← **Priority gap list**

---

## Evidence Map

### Section 1: [Requirement Category]

| # | Requirement | Citation | Evidence ID | Artifact | Location | Sufficiency |
|---|------------|---------|-------------|---------|---------|-------------|
| 1 | [requirement] | [citation] | EV-NNN | [description] | [location] | Strong ✅ |
| 2 | [requirement] | [citation] | — | [no artifact found] | — | Missing 🔴 |

### Section 2: [Next Category]
...

---

## 🔴 Evidence Gaps — Immediate Action Required

| Requirement | Citation | Gap | Recommended Action | Owner | Deadline |
|------------|---------|-----|-------------------|-------|----------|
| [requirement] | [citation] | No artifact | [collect X from Y] | [role] | [date] |

---

## Package Contents (for transmittal)

[Numbered list of all artifacts to be transmitted, with location and description]
```

---

### Mode: `gap` — Evidence Gap Analysis

For the specified domain or audit:

1. Pull the comprehensive list of requirements from the relevant skill (or the compliance calendar / risk register)
2. For each requirement, check the evidence locker for a covering artifact
3. Flag: missing, expired, weak, or untested artifacts
4. Produce a prioritized gap list

```markdown
# Evidence Gap Analysis — [Domain/Audit] — YYYY-MM-DD

## Gap Summary
- Requirements assessed: N
- Fully covered (Strong): N
- Partially covered (Adequate/Weak): N
- Not covered (Missing): N ← **Critical**

## Critical Gaps (No Evidence)

| Requirement | Regulatory Basis | Gap Type | Consequence | Collect From | Owner | Target Date |
|------------|-----------------|----------|-------------|-------------|-------|------------|
| [requirement] | [citation] | Missing | [audit finding / penalty risk] | [where to get it] | [role] | [date] |

## Weak Evidence (Should Strengthen Before Audit)

| Requirement | Regulatory Basis | Current Evidence | Weakness | How to Strengthen |
|------------|-----------------|-----------------|----------|------------------|
| EV-NNN | [requirement] | [citation] | [current artifact] | [issue] | [action] |

## Evidence Approaching Expiry

| EV-ID | Requirement | Expires | Days Left | Refresh Action |
|-------|------------|---------|-----------|---------------|
| EV-NNN | [requirement] | YYYY-MM-DD | N | [what to collect] |
```

---

## Step 4: Offer follow-up actions

After any mode, offer:
1. **Create collection tasks** — add gap-filling actions to `planner/tasks.md` with owners and deadlines
2. **Audit prep** — if a site visit is approaching, run `/compliance-brain:timeline` to see timing context
3. **Risk register update** — evidence gaps often reflect risk register exposures; offer to update via `/compliance-brain:risk update`
4. **Board report** — if packaging evidence for an accreditor visit, roll up into board report via `/compliance-brain:board-report`

---

## Quality Rules

- **The locker catalogs; it doesn't store.** Documents live in SharePoint, accreditor portals, or secure institutional systems. The evidence locker holds the index, not the files. Every artifact entry must have a `location` that a human can retrieve without the Brain.
- **Sufficiency is a judgment call, not a checkbox.** An auditor who is unsatisfied with your evidence can reject it regardless of whether it technically exists. Rate artifacts honestly: if a training log exists but shows only 60% completion, that's `Weak`, not `Strong`.
- **Expiry dates are real deadlines.** Training certificates, IRB approvals, BAAs — these expire. An expired artifact is worse than none because it signals to an auditor that the control lapsed.
- **Every control in the risk register needs evidence.** When a control is listed as `Strong` or `Adequate` in the risk register, there must be evidence to back that claim. Evidence gaps in High or Critical risks are priority findings.
- **Collect evidence continuously, not in a panic.** The worst time to look for a training certificate is two weeks before an accreditation site visit. The evidence locker should be updated quarterly at minimum.
