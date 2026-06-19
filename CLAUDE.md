# HE Compliance Brain

A second brain and personal knowledge system for a VP of Compliance, implemented as Claude Code Skills (`.claude/commands/`) with Python utilities.

## Project Purpose

Two interlocking skill sets:
1. **Second Brain / PKM** — capture, organize, retrieve, and synthesize personal knowledge and working notes
2. **Compliance Brain** — help a VP of Compliance manage regulatory tracking, gap analysis, risk registers, audit prep, policy drafting, and regulatory change monitoring

## Project Structure

```
he-compliance-brain/
├── .claude/
│   └── commands/         # Claude Code skill files (.md)
├── src/                  # Python utilities called by skills
├── docs/                 # Reference docs, templates, schema definitions
└── CLAUDE.md             # This file
```

## Skill Naming Convention

Skills live in `.claude/commands/` as markdown files. Name them with a prefix that groups them:

- `brain-*`      — second brain / PKM skills (capture, organize, retrieve)
- `compliance-*` — compliance workflow skills (track, analyze, draft, audit)
- `reg-*`        — regulatory intelligence skills (monitor, parse, map)

## Python Utilities (`src/`)

Any Python scripts invoked by skills go here. Keep them thin CLI wrappers — accept JSON or plain text on stdin, return structured output on stdout.

## Development Notes

- Skills are markdown prompt files; they are invoked via `/skill-name` in Claude Code
- Use `$ARGUMENTS` in skill files to accept user input
- Skills can shell out to `src/` Python scripts for data-heavy operations
- The primary user is a VP of Compliance — assume regulatory expertise, prefer concise outputs, structured templates over prose
