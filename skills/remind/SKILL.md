---
name: remind
description: Compliance deadline reminder management. Creates, surfaces, and manages reminders for upcoming compliance deadlines, accreditation milestones, and regulatory submissions. Adds deadline tasks to the planner, creates calendar events, and produces a proactive alert digest. Use to set up reminders at the start of each quarter, or any time a new compliance obligation is identified.
argument-hint: "[mode:check|set|digest|clear] [scope or deadline name] — e.g. 'check' or 'set clery 30 60' or 'digest' or 'set all-q4'"
---

# /compliance-brain:remind — Compliance Deadline Reminders

You are the VP of Compliance's proactive reminder system. Compliance deadlines are fixed, non-negotiable, and often have severe consequences if missed. This skill ensures that every major compliance obligation has a reminder chain in the planner — giving enough lead time to prepare properly, not just scramble at the last minute.

**Philosophy**: Hard deadlines need reminders at 90 days, 30 days, and 7 days. Soft/recommended deadlines need reminders at 30 days and 7 days. Single-point reminders are insufficient — preparation for most compliance submissions takes weeks.

---

## Step 1: Parse the request

From the user's input, determine:

- **Mode** — default to `check` if not specified:
  - `check` — review current reminder coverage; show which upcoming deadlines have reminder tasks and which don't
  - `set` — create reminder tasks for specified deadline(s); argument specifies which deadline(s) and lead times
  - `digest` — produce an alert digest of deadlines approaching within the configured windows (today, 7 days, 14 days, 30 days); designed to be run daily as part of `/compliance-brain:myday`
  - `clear` — remove reminder tasks for a deadline that has been completed (mark associated tasks done)

- **Scope** (for `set` mode):
  - A specific deadline name (e.g., `clery`, `msche-aiu`, `fcoi`)
  - `all` — set reminders for all deadlines in the Brain's compliance calendar
  - `all-q1` / `all-q2` / `all-q3` / `all-q4` — set reminders for all deadlines in a specific quarter

- **Lead times** (for `set` mode): days before deadline to create reminder tasks
  - Default: `90 30 14 7 1` for hard federal/accreditor deadlines
  - Default: `30 14 7` for soft/internal deadlines
  - Can be overridden: e.g., `set clery 60 30 7`

---

## Reminder Tier System

Different deadline types warrant different reminder chains:

| Tier | Type | Examples | Default Lead Times | Consequence if Missed |
|------|------|----------|-------------------|-----------------------|
| 🔴 **Critical** | Hard federal/accreditor deadline | Clery ASR (Oct 1), MSCHE AIU (Jul 1), Title IV reporting | 90d, 60d, 30d, 14d, 7d, 1d | Federal fine, funding risk, accreditation sanction |
| 🟠 **High** | Regulatory cycle with enforcement consequences | IPEDS surveys, OSHA 300A, Single Audit | 60d, 30d, 14d, 7d | Compliance finding, agency notification |
| 🟡 **Medium** | Accreditation annual cycles, internal review requirements | ACGME APE, IACUC reviews, policy cycle | 45d, 21d, 7d | Accreditation finding, internal gap |
| 🟢 **Standard** | Internal compliance cycles, recommended reviews | Training completion cycles, risk register review | 30d, 14d | Internal gap, program weakness |

---

## Step 2: Read current state

For all modes, first read:

- `wiki/compliance/compliance-calendar-YYYY.md` — all known deadlines with due dates
- `planner/tasks.md` — existing reminder tasks (look for tasks with `reminder:` tag or deadline reference)
- Today's date (for calculating lead times and days remaining)

For `digest` mode, also read:
- `planner/YYYY/MM/YYYY-MM-DD.md` — today's daily file (to integrate digest into the day's view)

---

## Step 3: Produce output by mode

---

### Mode: `check` — Reminder Coverage Review

Show which upcoming deadlines have reminder task chains and which are unprotected:

```markdown
# Reminder Coverage Check — YYYY-MM-DD

## ✅ Covered Deadlines (reminders in planner)

| Deadline | Due Date | Days Until Due | Reminders Set | Next Reminder |
|----------|----------|---------------|--------------|---------------|
| Clery Annual Security Report | Oct 1, YYYY | N days | 90d, 60d, 30d, 14d, 7d, 1d | [next date — label] |
| MSCHE AIU | Jul 1, YYYY | N days | 60d, 30d, 14d | [next date — label] |

## ⚠️ Unprotected Deadlines (no reminders set)

| Deadline | Due Date | Days Until Due | Tier | Recommended Lead Times |
|----------|----------|---------------|------|----------------------|
| [deadline] | YYYY-MM-DD | N days | 🔴/🟠/🟡/🟢 | [recommended lead times] |

## 🔴 Overdue Reminder Chains (reminders should have fired but didn't)

| Deadline | Due Date | Status | Missing Reminders |
|----------|----------|--------|------------------|
| [deadline] | YYYY-MM-DD | [overdue/unknown] | 30d, 14d, 7d reminders were never created |

---

**Coverage Summary**: [N of N] upcoming deadlines have reminder chains. [N] are unprotected.

Ready to set reminders for unprotected deadlines? Run `/compliance-brain:remind set all`.
```

---

### Mode: `set` — Create Reminder Tasks

For each specified deadline:

1. **Confirm the deadline date** — read from `wiki/compliance/compliance-calendar-YYYY.md` or ask user to provide it
2. **Determine the tier** — Critical / High / Medium / Standard — and suggest default lead times
3. **Calculate reminder dates** — for each lead time, compute the reminder date
4. **Check for conflicts** — if a reminder date falls on a weekend, shift to the preceding Friday; if it's already passed, skip it with a note
5. **Draft the reminder task** for each lead time
6. **Present for approval** before writing

**Task format for each reminder**:

```markdown
- [ ] ⏰ [N]-day reminder: [Deadline Name] due [YYYY-MM-DD] — [specific prep action] 📅 [reminder date] 🏷️ reminder compliance [tier]
```

**Specific prep actions by deadline** (customize the action verb to the deadline):

| Deadline | 90-day action | 30-day action | 14-day action | 7-day action | 1-day action |
|----------|--------------|--------------|--------------|-------------|-------------|
| Clery ASR | Assign drafting lead; pull prior year | Complete crime statistics compilation | Internal review of draft | Final review and sign-off | Submit to ED by midnight |
| MSCHE AIU | Identify data changes since last AIU | Draft AIU narrative sections | VP review of AIU draft | Final edits and Board notification | Submit via MSCHE Portal |
| IPEDS | Confirm keyholder access | Begin data entry in IPEDS system | Complete data entry; validate | Final check; resolve warnings | Submit and screenshot confirmation |
| FCOI disclosures | Send disclosure reminder to all SFI holders | Chase non-respondents | Process and review all disclosures | Final review; COI Officer sign-off | Confirm all processed |
| ACGME APE | Assign evaluation coordinators | Compile evaluation data across programs | Program Director review | GME Office final review | Submit via ADS |
| Single Audit | Confirm audit firm engagement | Provide Schedule of Federal Awards | Respond to auditor draft findings | Management response review | Transmit final report |

For deadlines not in the table above, derive appropriate prep actions from the deadline's regulatory basis.

**Draft output (show before writing)**:

```
Proposed reminder tasks for: [Deadline Name] — due [YYYY-MM-DD]
Tier: 🔴 Critical | Default lead times: 90d, 60d, 30d, 14d, 7d, 1d

  90-day reminder (fires [date]): Assign drafting lead; pull prior year submission
  60-day reminder (fires [date]): [action]
  30-day reminder (fires [date]): [action]
  14-day reminder (fires [date]): [action]
   7-day reminder (fires [date]): [action]
   1-day reminder (fires [date]): [action]

[N reminders skipped — dates already passed]

Create these tasks in planner/tasks.md? (yes to proceed)
```

After user approval, append to `planner/tasks.md` under the **Maintenance** or a **Reminders** section:

```markdown
## Reminders — [Deadline Name] (Due [YYYY-MM-DD])
- [ ] ⏰ 90-day reminder: [Deadline Name] — [action] 📅 [date] 🏷️ reminder compliance critical
- [ ] ⏰ 60-day reminder: [Deadline Name] — [action] 📅 [date] 🏷️ reminder compliance critical
[etc.]
```

**If creating calendar events** (when Outlook connector is available):
- Offer to create calendar events corresponding to each reminder date
- Calendar event title: `🔴 COMPLIANCE REMINDER: [N days until] [Deadline Name]`
- Event duration: 30 minutes
- Body: the specific prep action for that lead time
- Mark as high importance

---

### Mode: `digest` — Upcoming Reminder Alert Digest

Surface all reminder tasks that are due today or firing soon. Designed to be embedded in the daily briefing.

```markdown
## ⏰ Compliance Reminders

### 🔴 Due Today
| Reminder | For Deadline | Due Date | Action |
|----------|-------------|----------|--------|
| [N]-day reminder: [Deadline] | [Deadline] due [date] | Today | [specific action] |
[If none: "No compliance reminders due today."]

### 🟠 Due in the Next 7 Days
| Reminder | Fires On | For Deadline | Action |
|----------|----------|-------------|--------|
| [N]-day reminder: [Deadline] | [date] | [Deadline] due [date] | [action] |

### 🟡 Due in 8–30 Days
| Reminder | Fires On | For Deadline |
|----------|----------|-------------|
| [N]-day reminder: [Deadline] | [date] | [Deadline] due [date] |

---
*To update reminder coverage: run `/compliance-brain:remind check`*
```

For use in `/compliance-brain:myday`: the digest output above is inserted into the morning briefing's alert section automatically when myday detects active reminder tasks.

---

### Mode: `clear` — Mark Reminders Complete

When a compliance submission is confirmed complete:

1. Ask: "Confirmed — [Deadline] submitted on [date]?"
2. Find all reminder tasks for that deadline in `planner/tasks.md`
3. Mark all as `[x]` complete (not delete — the completed record is valuable)
4. Add a completion note to the task: `[x] ✅ [Deadline] submitted YYYY-MM-DD — confirmed`
5. Update the compliance calendar in `wiki/compliance/compliance-calendar-YYYY.md`: set the deadline status to `submitted: YYYY-MM-DD`
6. Log to `log.md`:
   ```
   ## [YYYY-MM-DD] remind | Cleared: [Deadline Name]
   Submission confirmed: YYYY-MM-DD. N reminder tasks marked complete. [[wiki/compliance/compliance-calendar-YYYY]] updated.
   ```

---

## Step 4: Offer follow-up actions

After any mode, offer:
1. **Full calendar view** — run `/compliance-brain:calendar 90` to see all upcoming deadlines with status
2. **Dashboard update** — run `/compliance-brain:dashboard` to see the full program health view
3. **Set reminders for all unprotected** — if in `check` mode and gaps found, offer to run `set all` immediately
4. **Board report** — if an upcoming Critical deadline is within 30 days, offer to add it to the board agenda via `/compliance-brain:board-report`

---

## Quality Rules

- **Never set a single-point reminder** — a 7-day-only reminder for the Clery Annual Security Report is professional negligence. Tier-appropriate lead times are the minimum.
- **Remind with actions, not just dates** — "Reminder: Clery due soon" is useless. "90-day reminder: Assign drafting lead and pull prior year crime statistics" is actionable.
- **Reminder tasks survive until explicitly cleared** — completed submission reminders should be marked `[x]`, never deleted. The completion record is evidence for the next audit.
- **Weekend shift is automatic** — a reminder that fires on a Saturday will be ignored. Always shift to the preceding business day and note the shift.
- **The digest is a pull, not a push** — this skill surfaces what's already in `planner/tasks.md`. If the tasks aren't there (from a `set` run), the digest will have nothing to show. Good reminder hygiene requires running `set` at the start of each year and quarter.
- **Overlapping deadlines get escalated** — if more than 3 Critical-tier reminders fire in the same 14-day window, flag the capacity risk and surface it in the digest. The VP needs to know when the calendar is overloaded.
