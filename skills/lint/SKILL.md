---
name: lint
description: Health check the entire Brain. Finds schema drift in CLAUDE.md, orphan pages, stale content, missing index entries, unresolved action items, broken heading anchors, raw/ governance violations, and cross-brain reference gaps. Use periodically to maintain Brain integrity.
---

# /the-brain:lint — Brain Health Check

You are performing a comprehensive health check of the Brain. Scan all three sub-brains systematically.

## Checks to perform

### 0. Schema integrity (CLAUDE.md vs. the bootstrap copy)

The Brain's `CLAUDE.md` was installed at bootstrap from the plugin's canonical copy and then customized. When the plugin updates, the Brain's copy can silently fall behind. Compare the two and report discrepancies.

**Canonical copy**: `${CLAUDE_PLUGIN_ROOT}/skills/newbrain/assets/CLAUDE.md` — read it alongside the Brain root's `CLAUDE.md`. If the canonical copy can't be read (skill run outside the plugin), skip this check and say so in the report.

**Customized sections** — these three are personalized by `/the-brain:newbrain` and are **expected to differ**. Never flag content differences in them, and never overwrite them:

- Available Connectors
- Timezone Convention
- External Reference Conventions

For these, check only that (a) the section still exists in the Brain's copy, and (b) no bootstrap placeholders survive — `<!-- CUSTOMIZE` comments or angle-bracket-wrapped uppercase placeholders (`<YOUR_BRAIN_PATH>`, etc.). Leftover placeholders mean bootstrap never finished — flag as a **Warning**.

**All other sections** — compare heading-by-heading (ignore whitespace-only differences):

- Section in the canonical copy but missing from the Brain's → **Warning** (schema drift: plugin added it, or it was deleted locally)
- Section whose content materially differs from the canonical copy → **Warning** (schema outdated, or edited locally)
- Section in the Brain's copy but not the canonical one → **Suggestion** (local extension; legitimate, but note it so the user knows it won't survive a future re-bootstrap)
- `CLAUDE.md` missing from the Brain root entirely → **Error** (the Brain has no schema; recommend re-running `/the-brain:newbrain` in a fresh folder and migrating, or restoring from the canonical copy)

**Auto-fix offer**: for drifted non-customized sections, offer to update the Brain's `CLAUDE.md` from the canonical copy — replacing only the drifted sections and leaving the three customized sections untouched. Show the user which sections will change before writing. If a drifted section appears to contain deliberate local edits (not just an older plugin version), say so and let the user decide per section.

Apply the same comparison to `templates.md` (also installed from `${CLAUDE_PLUGIN_ROOT}/skills/newbrain/assets/templates.md` at bootstrap). It has no customized sections, so any material difference is a **Warning** with the same auto-fix offer.

### 1. Index integrity

For each sub-brain (wiki/, pm/, planner/):
- List all `.md` files in the sub-brain directories
  - For planner: scan `planner/YYYY/MM/` directories for daily files (YYYY-MM-DD.md) and weekly files (week-WW.md)
  - For pm: include `pm/prep/` in the scan scope alongside `pm/projects/`, `pm/meetings/`, `pm/notes/`
- Read the sub-brain's `index.md`
- Flag any pages that exist on disk but are missing from the index
- Flag any index entries that reference pages that don't exist
- Auto-fix: add missing pages to the index with a `[NEEDS REVIEW]` tag

### 2. Orphan pages

- For each page, grep across all sub-brains for inbound `[[wikilinks]]` to that page
- Flag pages with zero inbound links (other than from their index)
- These are candidates for better cross-referencing or deletion

### 3. Broken heading anchors

- Find all `[[page#heading]]` links across the Brain
- For each, verify the target page exists AND the heading exists in that page
- Flag broken anchors — these are high-priority fixes

### 4. Source traceability

- For each page with a `raw_source` frontmatter field, verify the raw file exists. **`.ref.md` connector-reference stubs are valid `raw_source` targets** — a path like `raw/2026-06-11-meeting.ref.md` is compliant even though it contains no verbatim content.
- For each page derived from a source, verify it has both `raw_source:` in frontmatter AND an inline `Source: [[raw/...]]` wikilink
- Flag pages missing traceability

### 5. Raw governance check (Outlook/Teams retention policy)

Outlook emails, Teams chats, and Teams meeting transcripts must **never** be stored verbatim in `raw/`. They are represented by connector-reference stubs (`.ref.md` files with `type: connector-reference` frontmatter). Synthesized downstream pages (meeting pages, notes, analysis) are exempt — only verbatim copies violate policy.

**Step 1 — Scan `raw/` for violations.**

For every file in `raw/`:
- **Skip immediately** if the file has a `.ref.md` suffix OR its frontmatter contains `type: connector-reference`. These are compliant by definition.
- **Skip** synthesized pages (meeting pages, notes) — they may quote a line or two without being verbatim copies.
- **Read the file content** before flagging. The heuristics below are triggers to read; confirmation requires judgment.

Heuristics that indicate a verbatim Outlook/Teams copy:

| Category | Heuristics |
|----------|-----------|
| **Outlook email copy** | Header block containing `From:` / `To:` / `Subject:` / `Sent:` followed by a message body; filename containing `email` |
| **Teams meeting transcript** | Repeated speaker-labeled lines (`Name: text` or `Name (HH:MM): text` patterns); VTT/timestamp artifacts; `"transcript"` in the filename with a substantial body (>20 lines); metadata header stating "Teams auto-generated transcript" |
| **Teams chat log** | Sequences of timestamped sender→message lines; markers like "Teams chat" or "chat export" in the file; `teams.microsoft.com` deep links combined with quoted message bodies |

**Step 2 — For each confirmed violation, report:**
- File path
- Which heuristic pattern triggered the flag (be specific)
- File size (line count or byte count)
- All inbound `[[raw/filename]]` references found across the Brain (grep all sub-brains)

**Step 3 — Offer exactly two resolutions. Never act without the user choosing.**

**(a) Delete** — Before offering this option, verify that derived pages exist (a meeting page, notes, or analysis page) that capture the knowledge from the file. If no derived pages exist, do **not** offer deletion as the primary option — lead with option (b) and warn that choosing deletion will permanently lose the knowledge.

**(b) Summarize & catalog** — Run the /the-brain:ingest pipeline on the file's content: extract knowledge into proper Brain pages (meeting page, notes, etc.), then replace the raw file with a `.ref.md` connector-reference stub containing only metadata and retrieval instructions, and update all inbound `[[raw/...]]` links in the Brain to point at the new stub.

**This check never auto-deletes or auto-replaces files.** Report findings and wait for the user to choose (a) or (b) for each violation.

Include governance violations in the final report under **Errors** (verbatim copies present) — these are policy violations, not just quality issues.

### 6. Stale content

- For project pages: check `updated` date. If older than 2 weeks and project is active, flag as potentially stale
- For meeting action items: check if any are past due date and still `status: open`
- Cross-reference with `planner/tasks.md` — tasks there should match action items in meeting pages

### 7. Cross-brain reference gaps

- Meeting pages should link to project pages and entity pages
- Project pages should link to concept pages where relevant
- Entity pages mentioned in meetings should exist in `wiki/entities/`
- Flag significant entities/concepts mentioned in text but lacking their own page

### 8. Archive candidates

- Projects with `status: completed` still in active index sections
- Daily logs (in `planner/YYYY/MM/YYYY-MM-DD.md`) older than 2 weeks without a weekly reflection covering them
- Completed tasks still in `planner/tasks.md` (should have been pruned by `/the-brain:reflect`)

### 9. Overview freshness

- Read each `overview.md` and compare with current index
- Flag if the overview doesn't reflect the Brain's current state

## Output

Produce a report organized by severity:
- **Errors** (broken links, missing files, broken anchors) — these break navigation
- **Warnings** (stale content, missing cross-refs, archive candidates) — these degrade quality
- **Suggestions** (missing pages for mentioned concepts, better cross-refs) — these improve the Brain

For simple fixes (missing index entries, obvious missing links), offer to auto-fix.
For complex issues, create tasks in `planner/tasks.md`.

Append to `log.md`:
```
## [YYYY-MM-DD] lint | /the-brain:lint Brain health check
Errors: N, Warnings: N, Suggestions: N. Auto-fixed: [list]. Tasks created: [list].
```
