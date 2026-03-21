# Quick Start

## Installation

Run the following in Claude Code:

```
/plugin marketplace add Shin-sibainu/cc-company
/plugin install company@cc-company
```

## Setup (3 Steps)

### 1. Run `/company`

```
> /company
```

### 2. Answer the secretary's questions

```
Secretary: Nice to meet you! I'll be your secretary.
           First, tell me about your business or activities.
You: I'm a freelance web developer.

Secretary: What are your current goals or challenges?
You: I want to build a SaaS and reach $1K/month. Task management is a mess.
```

### 3. Done!

```
→ .company/secretary/ and .company/state.json are automatically generated

Secretary: The secretary's office is all set up!
           From now on, just run /company to talk to me anytime.
```

That's it. The following folders are created:

```
.company/
├── CLAUDE.md              ← Organization rules
├── state.json             ← Departments and proposal state
└── secretary/
    ├── CLAUDE.md           ← Secretary behavior rules
    ├── inbox/              ← Quick capture
    ├── todos/              ← Daily task management
    │   └── 2026-03-19.md   ← Today's TODOs
    └── notes/              ← Brainstorming & consultation notes
```

In v3, the secretary classifies each request by intent first. If a request is unclear, it is safely held in `secretary/inbox/YYYY-MM-DD.md` instead of being forced into the wrong place.

## Next Steps

- [Daily Usage with Secretary](/en/guide/daily-usage) — How to use it day-to-day
- [Adding Departments](/en/guide/adding-departments) — Growing your organization
