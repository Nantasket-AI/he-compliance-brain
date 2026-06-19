---
name: substantive-change
description: Substantive change assessment for MSCHE and LCME. Determines whether a planned institutional action triggers a notification or prior approval obligation, identifies the filing requirements and timeline for each accreditor, and produces the documentation needed to initiate the filing. Use before launching new programs, campuses, modalities, partnerships, or organizational changes.
argument-hint: "<change description> [mode:assess|checklist|filing|brief] — e.g. 'new online MS program assess' or 'merger with regional hospital filing' or 'new branch campus brief'"
---

# /the-brain:substantive-change — Substantive Change Assessment

You are evaluating whether a planned institutional action constitutes a substantive change requiring notification or prior approval from MSCHE and/or LCME on behalf of the VP of Compliance. Filing late — or failing to file at all — can result in the accreditor withholding approval of the change, placing the institution on special monitoring status, or in extreme cases triggering a compliance review.

Every assessment must cite the specific MSCHE or LCME substantive change policy and must be grounded in evidence about the proposed change from the Brain.

---

## Step 1: Parse the request

From the user's input, determine:

- **Proposed change**: the action the institution is planning (provide as much detail as possible)

- **Mode**: output format — default to `assess` if not specified:
  - `assess` — evaluate whether the change triggers substantive change obligations; identify all applicable accreditors
  - `checklist` — formatted checklist of all notification/approval requirements for a confirmed substantive change
  - `filing` — produce a filing outline (narrative, supporting documents, timeline) for submitting to MSCHE and/or LCME
  - `brief` — executive summary of the substantive change obligations for institutional leadership

---

## MSCHE Substantive Change Policy Reference

MSCHE's substantive change policy requires institutions to notify or seek prior approval for changes that could significantly alter the institution's mission, goals, programs, organizational structure, geographic reach, or mode of delivery.

### MSCHE Changes Requiring Prior Approval (before implementation)

| Change Type | Policy Reference |
|-------------|-----------------|
| Establishment of an additional location (branch campus, additional location) | MSCHE Substantive Change Policy §III.A |
| Offer 50% or more of a degree or certificate program at an additional location | MSCHE Policy |
| Significant increase or decrease in enrollment (defined in policy) | MSCHE Policy |
| Merger, consolidation, or acquisition | MSCHE Policy |
| Change in ownership, governance, or control | MSCHE Policy |
| Addition of a doctorate program where none previously existed | MSCHE Policy |
| Addition of a new degree level (e.g., first baccalaureate when only graduate before) | MSCHE Policy |
| Change in mission that substantially alters the institution's purpose | MSCHE Policy |

### MSCHE Changes Requiring Notification (within specified timeframe)

| Change Type | Timeline | Notes |
|-------------|----------|-------|
| New degree or certificate programs (within existing mission) | 30 days prior to implementation | Does not require approval unless triggers another category |
| New certificate programs | 30 days prior | |
| Closure of programs, locations, or the institution | As soon as decision is made | |
| New off-campus instructional sites (< 50% of program) | 30 days prior | |
| Distance education (if institution not previously approved for distance) | Prior approval required | |
| Significant curriculum changes (>25% of a program) | Notify MSCHE | |
| Change in academic calendar (quarter to semester, etc.) | Notify | |

### MSCHE Approval Timeline
- Prior approval requests must be submitted sufficiently in advance of implementation — MSCHE recommends **6–12 months** before the change takes effect
- MSCHE's review cycle affects timing; Board of Trustees meeting schedule may affect approval dates
- Contact MSCHE liaison early — informal consultation is strongly encouraged before formal filing

---

## LCME Substantive Change Policy Reference

LCME requires notification or prior approval for changes that materially alter the MD program, its resources, its student body, or its governance.

### LCME Changes Requiring Prior Approval (Notification to LCME before implementation)

| Change Type | Notes |
|-------------|-------|
| Establishment of a regional campus or distributed campus | Any new site where students complete a significant portion of the curriculum |
| Significant change in class size (>10% increase or any decrease significantly affecting resources) | LCME must be notified |
| New integrated curriculum (major curriculum redesign, not incremental changes) | Especially if changing from systems-based to discipline-based or vice versa |
| Change in length of MD program (e.g., 3-year program) | Requires LCME approval |
| Merger, acquisition, or significant change in governance of the medical school | LCME must be notified immediately |
| Closure of the medical school or significant program suspension | LCME must be notified immediately |
| New dual-degree or combined-degree programs (MD/PhD, MD/MPH) | Notify LCME; may require approval |

### LCME Notification Timeline
- LCME requests **notification as early as possible** — at minimum 6 months before implementation for most changes
- LCME will indicate if the change triggers a formal review or site visit
- LCME may also address the change in a scheduled accreditation survey

### LCME vs. MSCHE Interaction
- A change that triggers LCME notification often also triggers MSCHE notification (and vice versa)
- When evaluating a change, assess both accreditors simultaneously
- Coordinate submission timelines so both filings are consistent with each other

---

## Other Accreditors and Regulators to Consider

Depending on the nature of the change, other bodies may also have substantive change obligations:

| Body | Triggered By | Notes |
|------|-------------|-------|
| ACGME (DIO/GMEC) | New GME programs, closure of programs, changes in program complement | Report via ADS; program-specific |
| State authorization | New state where students receive education (including online) | Varies dramatically by state; see NC-SARA and state-specific rules |
| HLC, SACSCOC, or other regional accreditor | If institution is dually accredited | Follow their separate substantive change policies |
| Dept. of Education | 90/10 Rule, changes in ownership, change in control | May trigger recertification for Title IV |

---

## Step 2: Search the Brain for context on the proposed change

### 2a. PM sub-brain
- `pm/projects/` — any existing project for the proposed change (strategic planning, new program development, real estate, partnerships)
- `pm/meetings/` — Board meetings, Dean's leadership team, academic affairs discussions where the change was discussed or approved
- `pm/notes/` — planning documents, feasibility studies, business cases for the change
- `pm/reports/` — prior substantive change filings (to understand what was filed before and what the process looked like)

### 2b. Wiki sub-brain
- `wiki/compliance/` — any substantive change policy pages or prior filing summaries
- `wiki/entities/` — MSCHE liaison, LCME accreditation office, General Counsel

### 2c. Planner sub-brain
- `planner/tasks.md` — any existing tasks related to the change or the notification filing

---

## Step 3: Search connected systems

- **SharePoint**: program proposals, feasibility studies, Board resolution approving the change, partnership agreements, real estate or lease documents for new locations
- **Outlook/Teams**: communications with MSCHE or LCME about the proposed change (prior consultation is very valuable)
- **Web**: verify current MSCHE and LCME substantive change policies — these are periodically updated:
  - MSCHE: msche.org/standards-and-practices/substantive-change/
  - LCME: lcme.org/accreditation/functions-and-structure/policies/

---

## Step 4: Assessment criteria

For each proposed change, evaluate against the following questions:

| Question | MSCHE Trigger | LCME Trigger |
|----------|-------------|-------------|
| Does it add a new location where students will receive instruction? | Prior approval likely required | Notification required |
| Does it add a new degree level? | Prior approval required | N/A for LCME (MD only) |
| Does it significantly change class size? | May require notification | Notification required |
| Does it change the mission? | Prior approval required | Notify LCME |
| Does it involve a merger or change in control? | Prior approval required | Notify LCME immediately |
| Does it add distance education where none existed? | Prior approval required | Notify LCME if >25% of curriculum |
| Does it add a new degree or certificate program? | Notification required | Varies |
| Does it change the curriculum by more than 25%? | Notify MSCHE | Notify LCME |
| Does it add a dual-degree program? | Notify MSCHE | Notify LCME |
| Does it close a program or location? | Notify MSCHE immediately | Notify LCME immediately |

---

## Step 5: Produce output by mode

---

### Mode: `assess` — Substantive Change Assessment

```markdown
---
title: Substantive Change Assessment — <Change Description>
date: YYYY-MM-DD
proposed_change: <one-sentence description>
implementation_target: <YYYY-MM-DD or "TBD">
---

# Substantive Change Assessment

## Proposed Change
[Detailed description of the planned action, based on Brain documents and user input]

## MSCHE Assessment

| Criterion | Applies? | Finding |
|-----------|---------|---------|
| New location / branch campus | Y/N | [analysis] |
| New degree level | Y/N | |
| Class size change | Y/N | |
| Mission change | Y/N | |
| Merger / change in control | Y/N | |
| Distance education (new) | Y/N | |
| New program notification | Y/N | |

**MSCHE Obligation**: Prior Approval Required / Notification Required / Not Required
**Filing Deadline**: [date based on implementation target]
**MSCHE Contact**: [liaison or MSCHE office, if known from Brain]

---

## LCME Assessment

| Criterion | Applies? | Finding |
|-----------|---------|---------|
| New regional/distributed campus | Y/N | |
| Class size change (>10%) | Y/N | |
| Major curriculum redesign | Y/N | |
| Change in program length | Y/N | |
| Merger / governance change | Y/N | |

**LCME Obligation**: Prior Approval / Notification / Not Required
**Filing Deadline**: [date]

---

## Other Bodies to Notify

| Body | Obligation | Deadline |
|------|-----------|---------|
| ACGME | [if applicable] | |
| State authorization | [states affected] | |
| Dept. of Education | [if ownership/control change] | |

---

## Overall Risk Assessment
[Narrative: what happens if the institution proceeds without filing; what monitoring/approval risk exists]

## Recommended Immediate Actions
1. [action] — Owner: [role] — Due: [date]
```

---

### Mode: `checklist` — Filing Checklist

```markdown
# Substantive Change Filing Checklist — <Change> — <Date>

## MSCHE Prior Approval / Notification

### Required Documentation
- [ ] Cover letter signed by President/CEO
- [ ] Description of the proposed change (narrative)
- [ ] Rationale and relationship to institutional mission
- [ ] Timeline for implementation
- [ ] Evidence of Board of Trustees approval
- [ ] Financial impact analysis
- [ ] Organizational chart reflecting the change (if governance/structure change)
- [ ] Student impact statement (enrollment, services, outcomes)
- [ ] Faculty and staffing plan
- [ ] Teach-out plan (if applicable — program closures)

### MSCHE Process
- [ ] Informal consultation with MSCHE liaison initiated
- [ ] MSCHE online substantive change form submitted (msche.org portal)
- [ ] Filing fee paid (if applicable)
- [ ] Confirmation of receipt from MSCHE
- [ ] MSCHE approval letter received (if prior approval required)

## LCME Notification

### Required Documentation
- [ ] Letter to LCME Secretary notifying of the change
- [ ] Description of the change and rationale
- [ ] Timeline
- [ ] Impact analysis on LCME Standards (specifically affected Standards noted)
- [ ] Board approval documentation
- [ ] Class size data (if enrollment change)
- [ ] Affiliation agreements for new sites (Standard 3.2)

### LCME Process
- [ ] LCME Liaison or accreditation office informed
- [ ] Formal notification letter submitted
- [ ] LCME confirmation of receipt
- [ ] LCME determination letter received

## Internal Prerequisites
- [ ] Board of Trustees approval documented in minutes
- [ ] Dean's approval documented
- [ ] Legal review completed
- [ ] State authorization review completed (all affected states)
```

---

### Mode: `filing` — Filing Outline

Produce a complete filing outline with section-by-section guidance:

```markdown
---
title: Substantive Change Filing Outline — MSCHE — <Change>
date: YYYY-MM-DD
---

# MSCHE Substantive Change Filing Outline

## Section 1: Institutional Overview
[Guidance: brief institutional mission, accreditation history, current status]

## Section 2: Description of the Proposed Change
[Guidance: what is changing, when, and how]

## Section 3: Rationale and Mission Alignment
[Guidance: why the institution is making this change; how it advances the mission]

## Section 4: Resource Assessment
[Guidance: financial, physical, faculty, and staff resources to support the change]

## Section 5: Impact on Students
[Guidance: how current and prospective students are affected; teach-out plan if programs are ending]

## Section 6: Governance Approval
[Guidance: document Board approval; provide resolution if available]

## Section 7: Effect on Other Standards
[Guidance: identify which MSCHE Standards are most affected by the change and how compliance is maintained]

## Supporting Documents Required
[Checklist of exhibits to attach]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save to Brain** — write assessment to `wiki/compliance/substantive-change-YYYY-MM-DD.md`
2. **Create project** — scaffold a substantive change filing project in `pm/projects/substantive-change-<name>/`
3. **Create tasks** — add filing deadline tasks to `planner/tasks.md`
4. **Calendar integration** — add filing deadline to `/the-brain:calendar`
5. **Cross-check policy** — if the change creates new programs, offer `/the-brain:policy` to ensure required policies will be in place before implementation

---

## Quality Rules

- **When in doubt, file.** The risk of filing an unnecessary notification is administrative inconvenience. The risk of failing to file a required notification is loss of accreditation or Title IV eligibility.
- **Always check both MSCHE and LCME** — a change to the MD program almost always affects both accreditors.
- **State authorization is frequently overlooked** — even a new online program that serves students in a different state can trigger state authorization requirements in that state; flag this explicitly.
- **Document all accreditor consultations** — informal conversations with MSCHE or LCME liaisons about a proposed change should be documented in the Brain.
- **Teach-out plans are required for closures** — if any program is being closed, a teach-out plan must be filed with MSCHE and may need to be filed with the state; flag immediately.
- **Timing is critical** — prior approval must be obtained before implementation, not after. "We'll file it when we're ready to launch" is non-compliant.
