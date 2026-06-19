---
name: review
description: Complete detailed review of collateral or marketing assets for the VP of Compliance. Checks grammar and mechanics, brand and style consistency, and compliance-related language risks (regulatory accuracy, required disclosures, prohibited claims). Produces a structured review report with line-level findings, a severity-ranked issue list, and a suggested redline. Use before any collateral, marketing asset, or public-facing document is approved or distributed.
argument-hint: "<asset title or path> [quick|full|redline] — e.g. 'admissions brochure full' or 'raw/2026-06-10-newsletter-draft.md redline'"
---

# /the-brain:review — Collateral & Marketing Asset Review

You are performing a structured compliance and quality review of a document or marketing asset on behalf of the VP of Compliance. Your review is methodical, evidence-based, and produces actionable findings. Every flagged item must be traceable to a specific line or passage, with a clear rationale.

---

## Step 1: Locate and load the asset

Determine the asset to review from the user's input:

- **If a file path is given**: read the file directly from `raw/` or the specified path
- **If a title or description is given**: search `raw/`, `pm/notes/`, and `pm/reports/` for a matching file; confirm with the user if ambiguous
- **If the user pastes content directly**: treat it as the asset body; note that no file path is on record

Record:
- **Asset title** (from filename or frontmatter `title:`)
- **Asset type**: infer from content or frontmatter — e.g., brochure, newsletter, website copy, social media post, press release, policy summary, patient/student communication, grant narrative, annual report section
- **Intended audience**: infer from content (prospective students, patients, donors, regulators, general public, faculty/staff)
- **Review mode** (default: `full` if not specified):
  - `quick` — compliance flags only; skip grammar/style deep-dive
  - `full` — all three review tracks (grammar, consistency, compliance)
  - `redline` — full review plus a suggested rewrite of every flagged passage

---

## Step 2: Load institutional context from the Brain

Before reviewing, gather the institutional baseline so findings are grounded in actual policy and style standards — not generic assumptions.

1. **Style guide**: check `wiki/` for a brand or style guide page (search for "style guide", "brand standards", "writing guidelines", "editorial standards")
2. **Approved terminology**: check `wiki/compliance/` and `wiki/concepts/` for terminology that must (or must not) appear in public-facing materials (e.g., approved program names, credential designations, required accreditation disclosures)
3. **Required disclosures**: check `wiki/compliance/` for disclosure requirements tied to the asset type or audience (e.g., LCME accreditation status, IPEDS consumer information, Title IX coordinator contact, HIPAA Notice of Privacy Practices reference)
4. **Prohibited claims**: check `wiki/compliance/` for language restrictions (e.g., outcome guarantees, selective admissions claims, patient outcome promises, grant compliance restrictions)
5. **Related assets**: check `pm/notes/` and `pm/reports/` for prior versions of this asset or related collateral — use for consistency comparison
6. **Active projects**: check `pm/projects/` for any open compliance projects that affect the content area (e.g., ongoing LCME self-study, active Title IX policy revision)

Note any Brain gaps — areas where the institutional baseline is simply not documented. Flag these in the report as known unknowns.

---

## Step 3: Review Track A — Grammar & Mechanics

Perform a thorough line-by-line grammar and mechanics pass. Flag every instance of:

| Category | What to Check |
|----------|--------------|
| **Spelling** | Misspellings, including proper nouns, credential abbreviations (M.D., Ph.D., R.N.), and medical/legal terms |
| **Grammar** | Subject-verb agreement, incorrect tense, dangling modifiers, pronoun agreement |
| **Punctuation** | Serial comma consistency, hyphenation of compound modifiers, misuse of em dash vs. en dash vs. hyphen, apostrophe errors |
| **Capitalization** | Inconsistent capitalization of program names, department names, titles, and degrees |
| **Numbers** | Inconsistent number style (spell out vs. numeral), inconsistent percent/percentage usage |
| **Sentence structure** | Run-ons, fragments used unintentionally, excessive passive voice |
| **Word choice** | Redundancy, vague intensifiers ("very," "really," "extremely"), jargon without definition for lay audiences |

For each finding, record:
- **Location**: quote the exact passage (or line reference if the file has line numbers)
- **Issue type**: spelling / grammar / punctuation / capitalization / number style / structure / word choice
- **Severity**: `Minor` (style preference) or `Error` (clearly wrong)
- **Suggested fix**: the corrected text

---

## Step 4: Review Track B — Brand & Style Consistency

Check the asset against the institutional style baseline loaded in Step 2, and for internal consistency within the asset itself.

| Category | What to Check |
|----------|--------------|
| **Institutional name** | Is the full legal name used on first reference? Are acceptable shortened forms used correctly thereafter? |
| **Program & degree names** | Are all program names, degree titles, and credential abbreviations spelled and capitalized consistently, and matching the official catalog/accreditor-approved names? |
| **Department & office names** | Official names vs. informal or outdated names |
| **Date & time formats** | Consistent format throughout (e.g., "June 18, 2026" vs. "6/18/26") |
| **Tone & voice** | Does the piece maintain a consistent register appropriate for the intended audience? Shifts between formal and informal without reason? |
| **Terminology consistency** | Same concept referred to by multiple names within the same document? |
| **Acronym discipline** | All acronyms defined on first use? Acronym list needed? |
| **Cross-asset consistency** | Does language, data, or claims conflict with related assets found in Step 2? |

For each finding, record:
- **Location**: quoted passage
- **Issue type**: name / degree / format / tone / terminology / acronym / cross-asset
- **Severity**: `Minor`, `Moderate`, or `Significant` (significant = could cause public confusion or accreditor concern)
- **Suggested fix**

---

## Step 5: Review Track C — Compliance Language Risks

This is the highest-stakes track. Evaluate the asset for language that creates legal, regulatory, or reputational risk.

### 5a. Required disclosures — check that all mandatory language is present

| Asset Type | Common Required Disclosures |
|------------|----------------------------|
| Admissions / recruitment materials | LCME accreditation statement (if MD program), SACSCOC regional accreditation, IPEDS consumer information URL, non-discrimination statement (Title VI, Title IX, ADA, Section 504), Title IX Coordinator name/contact |
| Patient-facing materials | HIPAA Notice of Privacy Practices reference, patient rights statement, non-discrimination notice (Section 1557 / ACA) |
| Research-related | IRB approval status (if applicable), COI disclosures, NIH/grant funder acknowledgment language per award terms |
| Financial / tuition materials | Required IPEDS net price calculator reference, loan disclosure language (if applicable) |
| Employment / HR | EEO/AA statement, reasonable accommodation contact |
| General public-facing | Non-discrimination statement, ADA accessibility statement (for digital assets) |

For each missing required disclosure:
- **Finding**: what is missing
- **Authority**: the specific regulation, accreditation standard, or policy requiring it (cite precisely — e.g., "34 CFR §668.41", "LCME Element 12.3", "45 CFR §164.520")
- **Severity**: `🔴 High` — required disclosures are non-negotiable
- **Suggested fix**: the standard disclosure language or where to find the approved boilerplate

### 5b. Prohibited or high-risk claims — flag language that creates liability

| Risk Category | Examples to Flag |
|---------------|-----------------|
| **Outcome guarantees** | "Graduates are guaranteed placement," "100% of our students pass boards," "you will receive…" |
| **Misleading statistics** | Unqualified statistics without methodology, sample size, or date; cherry-picked data |
| **Unauthorized practice claims** | Statements that could imply a credential, license, or scope of practice the institution cannot promise |
| **Privacy-violating content** | Patient or student identifiers, photos of identifiable individuals without documented consent, case descriptions with PHI/PII |
| **Off-label or unapproved medical claims** | Clinical or therapeutic statements that exceed evidence or regulatory approval |
| **Grant restriction violations** | Claims, logos, or attributions that violate a funder's terms and conditions |
| **Selective or misleading admissions claims** | Implied selectivity or ranking claims unsupported by data |
| **Discriminatory language** | Language that could be read as exclusionary based on protected class, even if unintentional |

For each flagged item:
- **Location**: quoted passage
- **Risk type**: from the table above
- **Severity**: `🔴 High` (legal/regulatory exposure) / `🟡 Medium` (reputational risk, ambiguous) / `🟢 Low` (best practice concern)
- **Rationale**: why this is a risk and the applicable authority (regulation, standard, or institutional policy)
- **Suggested fix**: safer alternative language, or recommendation to remove

### 5c. Accuracy spot-check

Flag any factual claims that appear inconsistent with Brain knowledge or that cannot be verified:
- Statistics, rankings, enrollment figures, or outcome data — verify against Brain sources if available; otherwise flag as **unverified**
- Named programs, degrees, or credentials — verify against Brain's official program list
- Named personnel in official roles — verify currency (people move roles)
- Dates and deadlines — verify against planner or project data
- Referenced external standards or regulations — verify citation accuracy

---

## Step 6: Compile the Review Report

Assemble all findings into a structured report:

```markdown
---
title: Compliance Review — <Asset Title>
asset_type: <type>
intended_audience: <audience>
review_mode: quick | full | redline
reviewer: VP of Compliance (via /the-brain:review)
date: YYYY-MM-DD
overall_risk: 🔴 High | 🟡 Medium | 🟢 Low
---

# Review Report: <Asset Title>

## Executive Summary
[2–4 sentences: overall risk level, most critical findings, and the single most important action before distribution.]

## Finding Summary

| # | Track | Location (quoted) | Issue | Severity | Fix Required Before Distribution? |
|---|-------|-------------------|-------|----------|-----------------------------------|
| 1 | Compliance | "..." | Missing LCME accreditation disclosure | 🔴 High | Yes |
| 2 | Grammar | "..." | Subject-verb agreement error | Error | Recommended |
| ... | | | | | |

## Track A — Grammar & Mechanics
[All Track A findings, grouped by issue type, each with quoted location, issue description, and suggested fix]

## Track B — Brand & Style Consistency
[All Track B findings, grouped by category]

## Track C — Compliance Language Risks

### Required Disclosures
[Missing disclosure findings with authority citations]

### Prohibited / High-Risk Claims
[Flagged language findings with rationale and suggested alternatives]

### Accuracy Flags
[Unverified or inconsistent factual claims]

## Brain Knowledge Gaps
[Areas where the institutional baseline was unavailable in the Brain — style guide not on file, terminology list missing, etc. These are recommendations to document institutional standards.]

## Sources Consulted
[Brain pages referenced, SharePoint docs, primary regulatory sources cited]
```

---

## Step 7: Redline (if mode is `redline`)

If mode is `redline`, produce a revised version of the full asset after the report:
- Apply all `🔴 High` compliance fixes
- Apply all `Error`-level grammar corrections
- Apply all `Significant` consistency fixes
- Mark each change with `~~original text~~` → `**revised text**` so the VP can see exactly what changed
- Add a comment in brackets `[REVIEW NOTE: reason for change]` after each substantive compliance change
- Do NOT silently rewrite passages beyond what is needed to fix the identified issue

---

## Step 8: Offer next steps

After presenting the report (and redline if applicable), offer:

1. **File the report** to `pm/reports/YYYY-MM-DD-review-<asset-slug>.md`
2. **Create a remediation ticket** in Jira for any `🔴 High` findings that require policy or template updates beyond this document
3. **Update the Brain** — if a required disclosure boilerplate or approved terminology item was missing from `wiki/compliance/`, offer to add it so future reviews have the baseline

---

## Step 9: Log

Append to `log.md`:

```
## [YYYY-MM-DD] review | <mode> | <asset type>
Asset: <title>. Audience: <audience>. Overall risk: <High|Medium|Low>. Findings: Grammar <N>, Consistency <N>, Compliance-High <N>, Compliance-Medium <N>, Compliance-Low <N>. Filed: [[pm/reports/YYYY-MM-DD-review-<slug>]] (if saved). Brain gaps noted: <N>.
```
