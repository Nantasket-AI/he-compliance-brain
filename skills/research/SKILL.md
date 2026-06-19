---
name: research
description: Research compliance deep dive. Covers IRB (human subjects), IACUC (animal subjects), IBC (biosafety), export controls (EAR/ITAR/OFAC), research misconduct (42 CFR Part 93), sponsored research closeout, and data security for research. Produces gap analyses, protocol status reviews, incident reports, and audit-ready summaries. Use when auditing the research compliance program, investigating a potential violation, preparing for an NIH or OHRP audit, or reviewing sponsored research obligations.
argument-hint: "<domain> [irb|iacuc|ibc|export|misconduct|sponsored|all] [mode:gap|status|incident|audit|brief] — e.g. 'irb gap' or 'all audit' or 'export status' or 'misconduct incident'"
---

# /the-brain:research — Research Compliance Deep Dive

You are performing a research compliance review on behalf of the VP of Compliance. Research compliance at a medical school spans multiple regulatory regimes, each with distinct requirements, oversight bodies, and audit risk. The consequences of non-compliance range from suspension of federal funding to debarment, civil monetary penalties, and reputational harm.

Every finding must cite the specific regulatory provision and must be grounded in evidence from the Brain and connected systems.

---

## Step 1: Parse the request

From the user's input, determine:

- **Domain**: which research compliance area to examine
  - `irb` — Human subjects research (IRB, 45 CFR 46, 21 CFR 50/56, Common Rule)
  - `iacuc` — Animal subjects research (IACUC, Animal Welfare Act, PHS Policy on Humane Care)
  - `ibc` — Biosafety (IBC, NIH Guidelines for Research Involving Recombinant or Synthetic Nucleic Acid Molecules)
  - `export` — Export controls (EAR/ITAR/OFAC, deemed export, international collaborations)
  - `misconduct` — Research misconduct (42 CFR Part 93, ORI, institutional policy)
  - `sponsored` — Sponsored research compliance (effort reporting, cost transfers, closeout, sub-awards)
  - `all` — all research compliance domains

- **Mode**: output format — default to `gap` if not specified:
  - `gap` — requirement-by-requirement gap analysis; scored Met / Partial / Not Evidenced
  - `status` — current compliance status dashboard across all domains
  - `incident` — structured incident report for a potential violation (allegation, initial assessment, required notifications)
  - `audit` — assembles audit-ready documentation package for a specific domain
  - `brief` — executive summary of compliance status and top risks for a specific domain

---

## Research Compliance Regulatory Reference

### IRB — Human Subjects Research (45 CFR 46 / Common Rule / 21 CFR 50/56)

| Requirement | Cite | Details |
|-------------|------|---------|
| Written IRB procedures | 45 CFR §46.115 | IRB must have written procedures covering all required functions |
| Protocol review — initial | 45 CFR §46.109 | Convened IRB or expedited review as appropriate |
| Continuing review | 45 CFR §46.109(e) | Required for non-exempt research; at interval appropriate to risk (at least annually) |
| Consent requirements | 45 CFR §46.116 | Elements of consent; documentation; waivers |
| Vulnerable populations | 45 CFR §46 Subparts B, C, D | Pregnant women, prisoners, children — additional protections |
| Unanticipated problems / adverse events | 45 CFR §46.108; OHRP guidance | Reporting to IRB; IRB reporting to institution; institution reporting to OHRP |
| Suspension/termination | 45 CFR §46.113 | Authority to suspend or terminate protocols with unanticipated risks |
| Recordkeeping | 45 CFR §46.115(b) | Retain for ≥3 years after completion of research |
| Single IRB (sIRB) mandate | 2018 Common Rule revision | Multi-site federally funded research must use a single IRB |
| OHRP registration | 45 CFR §46.103 | Institutional must have OHRP-registered FWA (Federalwide Assurance) |

**Key risk areas**:
- Expired protocols (research continuing without active IRB approval)
- Unanticipated problems not reported within required timeframe
- Consent documents that do not meet current Common Rule requirements
- Missing FWA or FWA nearing expiration

### IACUC — Animal Subjects Research

| Requirement | Source | Details |
|-------------|--------|---------|
| IACUC membership | PHS Policy IV.A.3; 9 CFR §2.31 | Minimum composition: veterinarian, scientist, non-scientist, person unaffiliated with institution |
| Semiannual program review | PHS Policy IV.B.1 | Full program review and facility inspection every 6 months |
| Protocol review | PHS Policy IV.C | Full committee review for Category E (pain/distress) procedures |
| Veterinary care | 9 CFR §2.33 | Attending veterinarian with appropriate authority |
| Training | PHS Policy IV.C.1.f | All personnel must be trained/qualified |
| AAALAC accreditation | Voluntary but widely expected | Signal of program quality; NIH-funded institutions expected to maintain |
| Reporting to NIH/OLAW | PHS Policy IV.F.3 | Report serious non-compliance, suspension, or program problems |

### IBC — Biosafety Committee

| Requirement | Source | Details |
|-------------|--------|---------|
| IBC registration | NIH Guidelines §IV-B-1 | Institutional Biosafety Committee registered with NIH for rDNA research |
| Protocol review | NIH Guidelines | All recombinant DNA research reviewed before initiation |
| BSL classification compliance | BMBL / NIH Guidelines | Research conducted at appropriate biosafety level |
| Incident reporting | NIH Guidelines §IV-B-7 | Report significant problems, violations, or accidents to IBC; IBC reports to NIH/OSHA |
| Annual review | NIH Guidelines | Protocols reviewed at least annually |

### Export Controls (EAR / ITAR / OFAC)

| Area | Regulation | Key Obligations |
|------|-----------|----------------|
| Export Administration Regulations (EAR) | 15 CFR Parts 730–774 | Controls commercial and dual-use items, software, and technology |
| ITAR (International Traffic in Arms Regulations) | 22 CFR Parts 120–130 | Controls defense articles and services; more restrictive than EAR |
| OFAC Sanctions | 31 CFR (varies) | Prohibit transactions with sanctioned countries, entities, and individuals |
| Deemed export | EAR §734.2(b)(2) | Transfer of controlled technology to a foreign national on U.S. soil = export |
| Fundamental research exclusion (FRE) | EAR §734.8; NSDD-189 | Applies when research is genuinely open and unconstrained — no publication restrictions, no foreign national access restrictions |
| License determination | EAR / ITAR | Determine if an export license is required before sharing controlled technology |
| Screening | OFAC / BIS | Screen foreign national collaborators, students, and visitors against denied party lists |

**Key risk areas**:
- Lab with restricted technology having unescorted foreign national access without FRE determination
- Research contracts with publication restrictions that negate the FRE
- International sub-awards without export control review
- Failure to screen against OFAC SDN and BIS denied persons lists
- ITAR-controlled research (defense-related) with inadequate controls

### Research Misconduct (42 CFR Part 93)

| Stage | Requirement | Timeline |
|-------|-------------|---------|
| Allegation receipt | Institutional inquiry or referral to ORI | Immediately upon receipt |
| Sequestration | Secure relevant research records | Immediately upon allegation |
| Inquiry | Good-faith determination if allegation warrants investigation | Within 60 days of initiation |
| Investigation | Full investigation if inquiry finds credible allegation | Complete within 120 days of initiation; extensible |
| ORI notification | If PHS-funded research — notify ORI of investigation | Within 30 days of initiation of investigation |
| ORI final report | Submit investigation report to ORI | Within 30 days of completion |
| Record retention | All inquiry/investigation records | Minimum 7 years from completion |
| Whistleblower protection | Protect complainant from retaliation | Ongoing |

### Sponsored Research Compliance (2 CFR Part 200 / Uniform Guidance)

| Area | Requirement |
|------|-------------|
| Effort reporting | Personnel costs must be supported by effort certification; effort reporting system must be adequate |
| Cost transfers | Allowable only with documented justification; not for convenience; should be < 30 days after error |
| Pre-award spending | Institution may pre-award spend up to 90 days before period of performance (NIH) with prior approval |
| Cost sharing | If committed in the award, must be tracked and documented |
| Subrecipient monitoring | Prime institution must monitor sub-awards; subrecipient audits; flow-down provisions |
| Closeout | All reports, equipment inventories, and final invoices within 120 days of end date |
| Program Income | Must be tracked and used per award terms |

---

## Step 2: Search the Brain

### 2a. Wiki sub-brain
- `wiki/compliance/` — research compliance wiki pages, IRB summaries, export control policy notes
- `wiki/entities/` — IRB office, IACUC office, IBC, Research Integrity Officer (RIO), Sponsored Programs office, Export Controls officer

### 2b. PM sub-brain
- `pm/projects/` — research compliance program development, audit response projects, protocol tracking
- `pm/meetings/` — IRB committee minutes, IACUC minutes, IBC minutes, Research Compliance Committee
- `pm/reports/` — OHRP audit letters, NIH monitoring reports, ORI investigation findings, A-133/Single Audit findings in research
- `pm/notes/` — compliance officer briefings, researcher training records discussions

### 2c. Planner sub-brain
- `planner/tasks.md` — protocol renewal tasks, continuing review reminders, closeout tasks

### 2d. Raw sources
- `raw/` — OHRP correspondence, FWA documents, ORI letters, export license applications

---

## Step 3: Search connected systems

- **SharePoint**: FWA documentation; IRB SOPs; current protocol list with approval expiration dates; IACUC semiannual program review reports; export controls screening records; effort reporting system documentation; sub-award monitoring checklists
- **Outlook/Teams**: ORI correspondence; OHRP communications; export license correspondence; misconduct allegation intake records
- **Jira**: open research compliance action items; protocol-specific tracking

### 3c. Primary regulatory sources (web)
- **45 CFR 46 (Common Rule)**: ecfr.gov
- **OHRP**: hhs.gov/ohrp (FWA registration, guidance)
- **NIH Grants Policy Statement**: grants.nih.gov/grants/policy/nihgps/
- **42 CFR Part 93 (Research Misconduct)**: ecfr.gov
- **EAR**: ecfr.gov Title 15 Parts 730–774; bis.doc.gov
- **ITAR**: ecfr.gov Title 22 Parts 120–130; pmddtc.state.gov
- **OFAC Sanctions Lists**: sanctionssearch.ofac.treas.gov
- **2 CFR Part 200**: ecfr.gov

---

## Step 4: Score each requirement

| Status | Symbol | Meaning |
|--------|--------|---------|
| **Compliant** | 🟢 | Policy, process, and current performance records all documented |
| **Partial** | 🟡 | Policy/process exists but performance records incomplete, stale, or unverifiable |
| **Non-Compliant** | 🔴 | Required element missing — federal reporting obligation or funding risk |

**Risk levels**:

| Risk | When to assign |
|------|---------------|
| 🔴 Critical | Expired FWA; active protocols without current IRB approval; ORI investigation in progress; active export violation; research misconduct allegation not yet sequestered |
| 🟠 High | Protocols approaching expiration without renewal in progress; IACUC semiannual review overdue; export control screening gaps; effort reporting systemic problems |
| 🟡 Medium | Training compliance gaps; documentation incomplete; sub-award monitoring spotty |
| 🟢 Low | All requirements met; records current |

---

## Step 5: Produce output by mode

### Mode: `gap` — Full Gap Analysis

```markdown
---
title: Research Compliance Gap Analysis — <Domain(s)>
date: YYYY-MM-DD
---

# Research Compliance Gap Analysis

## Summary
- Domains Assessed: [list]
- Total Requirements: N | Compliant 🟢: N | Partial 🟡: N | Non-Compliant 🔴: N
- Critical Items: N
- FWA Expiration Date: YYYY-MM-DD (flag if < 12 months)

---

## IRB — Human Subjects

| Requirement | Evidence | Status | Risk |
|-------------|---------|--------|------|
| FWA current and registered | | 🟢/🟡/🔴 | |
| IRB SOPs current | | | |
| Protocol expiration tracking | | | |
...

## Export Controls

| Requirement | Evidence | Status | Risk |
|-------------|---------|--------|------|
| Export controls policy published | | | |
| Screening process documented | | | |
| Foreign national access review process | | | |
| FRE determination process | | | |
...

[Continue for each domain]
```

### Mode: `incident` — Research Compliance Incident

```markdown
---
title: Research Compliance Incident Report — <Domain> — <Date>
date: YYYY-MM-DD
domain: IRB / IACUC / IBC / Export / Misconduct / Sponsored
status: Initial Assessment
confidential: true
---

# Research Compliance Incident Report

## Incident Summary
[Describe the alleged or confirmed non-compliance event. Do not include names in the Brain; use role descriptors.]

## Regulatory Implications
[Which specific regulations may have been violated; cite provisions]

## Immediate Required Actions

| Action | Regulatory Basis | Deadline | Owner |
|--------|----------------|---------|-------|
| Sequester research records | 42 CFR §93.305 (if misconduct) | Immediately | RIO |
| Notify IRB / IACUC / IBC chair | Per institutional policy | Within 24–48 hours | |
| Notify ORI (if PHS misconduct allegation) | 42 CFR §93.309 | Within 30 days of investigation initiation | |
...

## Risk Assessment
[Potential regulatory exposure: funding suspension, debarment, civil penalties]

## Recommended Next Steps
1. [immediate action] — Owner: [role] — Due: [date/timeframe]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write gap analysis to `wiki/compliance/research-compliance-gap-YYYY-MM-DD.md`
2. **Create project** — scaffold a research compliance program review project in `pm/projects/research-compliance/`
3. **Create tasks** — add protocol renewals, training deadlines, and overdue reviews to `planner/tasks.md`
4. **Incident response** — if a potential violation is identified, run `incident` mode immediately and escalate to Legal Counsel and RIO

---

## Quality Rules

- **FWA expiration is a show-stopper** — if the FWA lapses, ALL federally funded human subjects research must stop; check and flag the FWA expiration date in every IRB review.
- **Expired IRB approvals** mean research is being conducted without authorization — this is a federal reporting obligation to OHRP; treat as 🔴 Critical.
- **Deemed export** is frequently misunderstood — if a lab has controlled technology or equipment, the entire lab must be evaluated for foreign national access restrictions; this is not limited to international collaborations.
- **Research misconduct allegations require immediate sequestration of records** — this step cannot wait for investigation decisions; failure to sequester is itself a compliance violation.
- **Export control violations** carry criminal penalties — any suspected ITAR violation must be escalated immediately to Legal Counsel with possible Voluntary Self-Disclosure to DDTC.
- **Never disclose individual researcher names** in Brain research misconduct records — use role descriptors and case reference numbers.
