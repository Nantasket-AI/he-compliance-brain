---
name: intel
description: Regulatory and peer intelligence feed. A curated clipping service for compliance intelligence — captures enforcement actions at peer institutions, agency press releases, Federal Register developments flagged by the VP, Congressional activity, accreditor announcements, and peer institution news. Distinct from reg-monitor (which actively scans agency websites); intel is the library where manually flagged intelligence items are filed, searched, and surfaced as pattern-based alerts. Use to file a notable enforcement action, search for peer enforcement precedents, or generate an intelligence alert on a specific topic.
argument-hint: "[mode:file|search|feed|alert|digest] [topic or agency] — e.g. 'file' or 'search OCR Title IX enforcement' or 'feed' or 'alert research-misconduct' or 'digest'"
---

# /compliance-brain:intel — Regulatory & Peer Intelligence Feed

You are building and maintaining the VP of Compliance's regulatory intelligence library. The compliance program operates in an enforcement environment — what happened at Rutgers or Michigan last month is a signal about where federal auditors will look next. This skill is the curation layer: it captures, catalogs, and surfaces the intelligence that informs proactive compliance.

**Distinction from `/compliance-brain:reg-monitor`**: The `reg-monitor` skill actively fetches content from regulatory agency websites on demand. The `intel` skill is the archive where notable items are filed over time — it stores the VP's curated intelligence, not the raw scan. Think of `reg-monitor` as the scanner and `intel` as the clipping file.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `feed` if not specified:
  - `file` — file a new intelligence item into the library
  - `search` — search the library by topic, agency, institution, or keyword
  - `feed` — display the chronological intelligence feed (most recent first)
  - `alert` — surface all intelligence matching a topic or domain as a structured alert brief
  - `digest` — produce a curated weekly intelligence digest from recent items (designed for VP briefing or board prep)

- **Topic or agency** (for `search`, `alert`): free-text topic, agency code, or institution name

---

## Intelligence Item Data Model

Each intelligence item records:

| Field | Description |
|-------|-------------|
| `item_id` | Sequential: `INTEL-NNN` |
| `type` | Item type (see taxonomy below) |
| `date` | Date of the original event/publication |
| `filed_date` | Date filed into the intel library |
| `agency` | Issuing agency or accreditor (e.g., `HHS OCR`, `FSA`, `ACGME`, `NIH`) |
| `institution` | Peer institution affected (if an enforcement action or peer development) — use formal name |
| `title` | Short descriptive title of the intelligence item |
| `source_url` | URL of the primary source (press release, Federal Register, agency website, public filing) |
| `domains` | Compliance domain codes affected (REG, RESEARCH, ACCRED, etc.) |
| `topics` | Free-text topic tags (e.g., `title-ix`, `research-misconduct`, `clery`, `fcoi`) |
| `relevance` | 🔴 High / 🟡 Medium / 🟢 Low — how directly does this affect this institution? |
| `signal` | What this item signals about enforcement priorities or regulatory direction |
| `summary` | 2-3 sentence plain-language description of what happened and why it matters |
| `institutional_implications` | Specific implications for this institution — what this means for our compliance program |
| `action_required` | Yes / No — does this item warrant an institutional response? |
| `action_items` | If yes: specific actions, owner, deadline |
| `related_risks` | Risk register IDs this item informs or updates |
| `related_counsel` | Counsel library IDs (e.g., a related resolution agreement filed in counsel/) |

---

## Intelligence Item Type Taxonomy

| Code | Type | Description |
|------|------|-------------|
| `ENFORCEMENT` | Enforcement action | OCR resolution agreement, OIG settlement, FSA program review finding, NIH debarment |
| `FINAL-RULE` | Final rule | Regulation finalized — action may be required |
| `PROPOSED-RULE` | Proposed rule | Regulation proposed — comment period may be open |
| `GUIDANCE` | Regulatory guidance | Dear Colleague Letter, FAQ update, agency policy statement |
| `PEER-ACTION` | Peer institution action | Accreditation sanction, public enforcement, headline compliance failure at a comparable institution |
| `CONGRESSIONAL` | Congressional activity | Hearing, legislation, committee inquiry relevant to compliance obligations |
| `ACCREDITOR` | Accreditor announcement | New standards, FAQ updates, policy changes from LCME, MSCHE, ACGME, TJC |
| `COURT` | Court decision | Ruling interpreting a regulation or compliance obligation |
| `OIG-ADVISORY` | OIG Advisory | OIG compliance advisory, fraud alert, special advisory bulletin |
| `SELF-DISCLOSURE` | Notable self-disclosure | A peer institution's voluntary self-disclosure that signals enforcement priorities |
| `WHISTLEBLOWER` | Whistleblower development | False Claims Act settlement, qui tam development affecting the sector |

---

## Step 2: Read current state

- `intel/index.md` — master intelligence library index (all items, newest first)
- `intel/overview.md` — current intelligence landscape narrative
- `intel/enforcement/` — enforcement actions at peer institutions
- `intel/regulatory/` — regulatory developments (rules, guidance, Dear Colleague Letters)
- `intel/peer/` — peer institution news and compliance failures

---

## Step 3: Produce output by mode

---

### Mode: `file` — File a New Intelligence Item

1. **Gather information** from the user (or from a URL/pasted content):
   - What happened? (brief description)
   - What type of item is it?
   - Who was affected? (institution or agency)
   - When did it happen?
   - Source URL
   - What does this signal?
   - Any immediate action required for our institution?

2. **If a URL is provided**: use WebFetch to retrieve the primary source and extract:
   - The date and formal title
   - The specific regulatory provisions involved
   - The findings or actions taken
   - Any monetary penalty, corrective action, or required policy changes
   - Deadlines or timelines

3. **Assess relevance** for this institution:
   - Is the regulation involved one we're subject to?
   - Is the institution type comparable (medical school, research university, GME sponsor)?
   - Does the finding relate to a control we have (or lack)?
   - Could this trigger a self-audit or policy review?

4. **Assign INTEL-NNN** and draft the item for approval

5. **Write to the appropriate sub-directory** (`intel/enforcement/`, `intel/regulatory/`, `intel/peer/`)

6. **Update `intel/index.md`**

7. If relevance is 🔴 High and action_required is Yes: offer to add action items to `planner/tasks.md` and update the risk register

**Example enforcement action entry**:

```markdown
---
item_id: INTEL-047
type: ENFORCEMENT
date: 2026-05-15
filed_date: 2026-06-01
agency: HHS OCR
institution: Midwestern Medical School (hypothetical)
title: OCR Resolution Agreement — HIPAA Security Rule Violation — Ransomware Incident
source_url: https://www.hhs.gov/ocr/enforcement/...
domains: [PRIVACY]
topics: [hipaa, cybersecurity, ransomware, security-risk-analysis]
relevance: 🔴 High
action_required: true
related_risks: [RISK-008]
---

# INTEL-047 — OCR Resolution Agreement: Midwestern Medical School

**Type**: Enforcement Action | **Agency**: HHS OCR | **Date**: 2026-05-15
**Source**: [HHS OCR Press Release](https://www.hhs.gov/ocr/enforcement/...)

## What Happened

OCR reached a $1.2M resolution agreement with Midwestern Medical School following a ransomware attack that compromised 45,000 patients' PHI. OCR investigation found the institution had not conducted a comprehensive HIPAA Security Risk Analysis in 4 years and lacked a risk management plan.

## Signal

This is the fifth OCR action in 12 months involving a ransomware incident at a health system. OCR is actively investigating all reported ransomware incidents and using them as probes into the underlying HIPAA Security Rule compliance program. Institutions with outdated risk analyses or lacking documented risk management plans are at high risk.

## Institutional Implications

Our last HIPAA Security Risk Analysis was completed [date from Brain or risk register]. OCR's enforcement posture requires: (1) annual SRA or upon significant environmental change, (2) documented risk management plan with specific remediation timelines, (3) workforce training with completion records.

## Action Items

- [ ] Confirm date of last HIPAA Security Risk Analysis — if > 12 months, schedule immediately
- [ ] Review risk management plan for currency and completeness
- [ ] Pull training completion records for HIPAA security training
```

---

### Mode: `search` — Search the Intelligence Library

Use Grep across `intel/` to find items by topic, agency, institution, or keyword:

```markdown
# Intelligence Library Search — "[query]"
## [N] results | [N] High relevance, [N] Medium, [N] Low

| Item ID | Type | Title | Date | Agency/Institution | Relevance |
|---------|------|-------|------|--------------------|-----------|
| INTEL-NNN | [type] | [title] | YYYY-MM-DD | [source] | 🔴/🟡/🟢 |
...

## Top Results

### INTEL-NNN — [Title]
**Signal**: [signal field]
**Summary**: [summary]
**Implications**: [institutional_implications]
```

---

### Mode: `feed` — Chronological Intelligence Feed

```markdown
# Intelligence Feed — As of YYYY-MM-DD

## 🔴 High Relevance

### [Month YYYY]

**INTEL-NNN** — [Title]
*[Type] | [Agency/Institution] | [Date]*
[Summary]
[Signal]

**INTEL-NNN** — [Title]
...

## 🟡 Medium Relevance

### [Month YYYY]
...

## 🟢 Low Relevance / Monitor

[Abbreviated list]
```

---

### Mode: `alert` — Intelligence Alert on a Topic

Pull all intelligence items matching the specified topic and synthesize into an alert brief:

```markdown
---
title: Intelligence Alert — [Topic]
date: YYYY-MM-DD
prepared_for: VP of Compliance
---

# Intelligence Alert — [Topic]

## Alert Summary

[2-3 sentences: what the pattern shows, how many relevant items, overall signal strength]

**Pattern signal**: 🔴 Active enforcement priority / 🟡 Emerging trend / 🟢 Monitor

---

## Recent Enforcement Actions

| Item | Institution | Date | Penalty | Finding |
|------|------------|------|---------|---------|
| [INTEL-NNN] | [institution] | YYYY-MM-DD | [$amount or sanction] | [core finding] |
...

**Pattern**: [What these enforcement actions have in common — the common failure modes]

---

## Regulatory Developments

[List relevant final rules, proposed rules, guidance — what's changing]

---

## Peer Institution Developments

[Notable compliance failures, self-disclosures, accreditor actions in this area]

---

## Institutional Self-Assessment

Based on this intelligence, the following questions are worth asking:

1. [Specific self-assessment question based on enforcement patterns]
2. [Specific question]
3. [Specific question]

**Recommended actions**:
- [Action with owner and suggested deadline]
- [Action]
```

---

### Mode: `digest` — Weekly Intelligence Digest

Compile a curated weekly digest from items filed in the last 7–14 days:

```markdown
---
title: Compliance Intelligence Digest
date: YYYY-MM-DD
period: [start date] to [end date]
---

# Compliance Intelligence Digest — Week of [Date]

## This Week's Highlights

[3-5 sentence narrative: what dominated the regulatory and enforcement landscape this week]

---

## New Items Filed — [N] this week

### 🔴 Requires Attention

| Item | Title | Signal | Action |
|------|-------|--------|--------|
| INTEL-NNN | [title] | [signal] | [recommended action or "Monitor"] |

### 🟡 Notable / Monitor

| Item | Title | Signal |
|------|-------|--------|
| INTEL-NNN | [title] | [signal] |

### 🟢 Background Intelligence

[Brief list — one line per item]

---

## Running Pattern Tracker

[Domains or topics where multiple items have filed recently — signals emerging enforcement priority]

| Pattern | Items in Last 30 Days | Signal Strength |
|---------|----------------------|-----------------|
| [Topic] | N items | 🔴/🟡/🟢 |
```

---

## Step 4: Offer follow-up actions

After any mode, offer:
1. **Risk register update** — High-relevance enforcement actions often warrant a risk register update; offer to run `/compliance-brain:risk update`
2. **Regulatory scan** — for a new final rule or guidance, offer to run `/compliance-brain:reg-monitor` for a full agency scan
3. **Counsel library** — for enforcement actions at peer institutions, offer to file the resolution agreement in `/compliance-brain:counsel`
4. **Policy response** — if the intel reveals a policy gap, offer to track via `/compliance-brain:policy`
5. **Board report** — High-relevance items often belong in the next board report; offer to flag them via `/compliance-brain:board-report`

---

## Quality Rules

- **Source everything** — every intelligence item must have a `source_url` pointing to a primary source: the HHS OCR press release, the Federal Register notice, the ACGME announcement page. Intelligence without a primary source is rumor.
- **Signal is more valuable than summary** — the VP doesn't just want to know what happened; they want to know what it means for this institution. The `signal` and `institutional_implications` fields are the most important part of each entry.
- **Enforcement actions at comparable institutions are high priority** — a research university and medical school that received an OCR enforcement action is far more informative than one at a community college. Filter for comparability and weight accordingly.
- **The pattern tracker is the real product** — a single enforcement action is interesting. Five enforcement actions in the same domain over 12 months is a signal that should change compliance priorities. The `alert` mode exists to surface these patterns.
- **Proposed rules are not yet compliance obligations** — always distinguish proposed from final. A proposed rule means: (1) read it, (2) decide whether to submit comments, (3) monitor for finalization. It does not yet require policy changes.
- **Congressional activity is early warning** — a Congressional hearing on FCOI or a GAO study on GME oversight often precedes regulatory action by 12–24 months. File it and track it. Early warning is the intelligence dividend.
