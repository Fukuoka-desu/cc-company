# Adding Departments

This is a core feature of cc-company. In v3, department suggestions are grounded in `.company/state.json` instead of pure conversation memory.

## Suggestions from the Secretary

When specialized work in the same area repeats, the secretary suggests a new department.

```
> Research competitors for me
Secretary: I'll organize this as a research request in inbox first.
  → Saved to secretary/inbox/2026-03-21.md

(After a similar request happens again...)

> I'd also like to know about overseas trends
Secretary: Research requests are piling up.
           `.company/state.json` has reached the proposal threshold,
           so a Research department would let us organize this in topics/.
           Shall I create it?

You: Yes, create it

→ research/ is automatically generated
```

::: tip Note
If a department does not exist yet, the secretary first stores the request summary in `secretary/inbox/`. v3 avoids forcing work into the wrong place just to look smart.
:::

## Direct Requests

Of course, you can also request directly.

```
> Create a PM department
Secretary: Creating a PM department now!

→ pm/ is automatically generated
```

If you explicitly ask to create a department, the secretary does not wait for the proposal counter.

## What Gets Created

When a department is added, the following are auto-generated:

- **Department folder** — `.company/[department]/`
- **Department CLAUDE.md** — Rules and behavior for that department
- **Subfolders** — For file management
- **Templates** — For creating new files
- **state.json update** — Department list and proposal state

For example, adding a Research department:

```
.company/
├── CLAUDE.md              ← Department list gets updated
├── secretary/
└── research/              ← Newly added
    ├── CLAUDE.md           ← Research rules
    └── topics/             ← Research topic management
```

## Available Departments

| Department | Area |
|-----------|------|
| PM | Project progress, ticket management |
| Research | Market research, competitive analysis, tech research |
| Marketing | Content planning, SNS, campaigns |
| Engineering | Technical docs, design, debugging |
| Finance | Invoices, expenses, revenue management |
| Sales | Client management, proposals |
| Creative | Design briefs, brand management |
| HR | Recruitment, team management |

See the [Departments Reference](/en/reference/departments) for details.
