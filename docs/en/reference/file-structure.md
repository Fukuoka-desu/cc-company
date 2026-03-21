# File Structure

## Plugin Structure

```
cc-company/
├── .claude-plugin/
│   └── marketplace.json        ← Marketplace registration info
├── .github/
│   └── workflows/
│       └── deploy-docs.yml     ← Auto-deploy documentation
├── plugins/
│   └── company/
│       ├── .claude-plugin/
│       │   └── plugin.json     ← Plugin metadata
│       └── skills/
│           └── company/
│               ├── SKILL.md    ← Skill definition (entire workflow)
│               └── references/
│                   ├── departments.md         ← Department templates
│                   ├── claude-md-template.md  ← CLAUDE.md generation template
│                   └── state-template.json    ← state.json template
├── docs/                       ← This documentation (VitePress)
├── package.json
├── README.md
└── LICENSE
```

## Generated Organization Structure

The `.company/` folder created after running `/company`.

### Initial State

```
.company/
├── CLAUDE.md              ← Organization rules & owner info
├── state.json             ← Departments, proposal state, routing hints
└── secretary/
    ├── CLAUDE.md           ← Secretary behavior rules
    ├── inbox/              ← Quick capture
    ├── todos/              ← Daily task management
    │   └── YYYY-MM-DD.md
    └── notes/              ← Brainstorming & consultation notes
```

### After Adding Departments

```
.company/
├── CLAUDE.md
├── secretary/
│   ├── CLAUDE.md
│   ├── inbox/
│   ├── todos/
│   └── notes/
├── research/              ← Added department
│   ├── CLAUDE.md
│   └── topics/
└── pm/                    ← Added department
    ├── CLAUDE.md
    ├── projects/
    └── tickets/
```

## File Naming Rules

| Pattern | Format | Example |
|---------|--------|---------|
| Daily files | `YYYY-MM-DD.md` | `2026-03-19.md` |
| Topic files | `kebab-case.md` | `competitor-analysis.md` |
| Decision logs | `YYYY-MM-DD-decisions.md` | `2026-03-19-decisions.md` |
| Templates | `_template.md` | `_template.md` |

## TODO Format

```markdown
- [ ] Task description | Priority: High/Normal/Low | Due: YYYY-MM-DD
- [x] Completed task | Done: YYYY-MM-DD
```

## state.json

```json
{
  "version": 3,
  "departments": ["secretary"],
  "routing_hints": {
    "pm": 0,
    "research": 0,
    "marketing": 0,
    "engineering": 0,
    "finance": 0,
    "sales": 0,
    "creative": 0,
    "hr": 0
  },
  "last_active_date": "YYYY-MM-DD",
  "pending_proposals": []
}
```

- `departments`: currently active departments
- `routing_hints`: how many repeated requests each area has seen
- `pending_proposals`: departments or follow-ups waiting for a decision

## Operational Rules

- **One file per day**: Daily files for todos, inbox, decisions, and learnings append by date
- **One file per topic**: Notes and department files append to the existing topic file when possible
- **Date check**: Always verify today's date before file operations
- **No overwriting**: Existing files are append-only
- **When in doubt, inbox**: If unsure where to categorize, put it in `secretary/inbox/`
