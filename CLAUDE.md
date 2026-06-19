# HE Compliance Brain

A set of Claude Code skills for a second brain / PKM system and compliance work. Drop the `.claude/commands/` folder into any Claude Code project to install.

## What This Is

A plugin — no Python, no dependencies, no server. Just markdown skill files that tell Claude how to use its built-in tools (Read, Write, Grep, Glob, WebFetch) to run structured workflows.

## How Skills Work

Each `.md` file in `.claude/commands/` becomes a `/skill-name` slash command in Claude Code. The file is an instruction set Claude follows when the command is invoked. `$ARGUMENTS` captures anything the user types after the command name.

## Skill Sets

### Second Brain — Capture
- `/brain-capture` — universal router
- `/brain-capture-meeting` — structured meeting notes with action items
- `/brain-capture-reading` — reading notes and takeaways
- `/brain-capture-decision` — decision log with rationale and alternatives
- `/brain-capture-person` — notes on a person or contact

### Second Brain — Ingest from M365
- `/brain-ingest-email` — capture an Outlook email or thread
- `/brain-ingest-teams` — capture a Teams chat or meeting transcript
- `/brain-ingest-sharepoint` — fetch and capture a SharePoint doc or page
- `/brain-ingest-calendar` — capture a calendar event and build a pre-meeting brief

### Second Brain — Retrieve & Synthesize
- `/brain-retrieve` — search notes by topic or keyword using Grep
- `/brain-synthesize` — synthesize all notes on a topic into a document
- `/brain-daily` — daily review: recent captures, open action items

### Compliance Workflows *(coming next)*
- `/compliance-gap`
- `/compliance-risk`
- `/compliance-audit-prep`
- `/compliance-policy`
- `/reg-monitor`
- `/reg-map`

## Brain Storage

Notes are written as markdown files to the brain root:

```
~/brain/
  meetings/    YYYY-MM-DD-<slug>.md
  readings/    YYYY-MM-DD-<slug>.md
  decisions/   YYYY-MM-DD-<slug>.md
  people/      <person-name-slug>.md
```

Override the root by setting `BRAIN_PATH` in your environment.

## Skill File Convention

- One file per skill, named to match the slash command
- Instructions written for Claude to follow step-by-step
- Use `$ARGUMENTS` for user input
- Reference built-in tools by name: Write, Read, Grep, Glob, WebFetch
