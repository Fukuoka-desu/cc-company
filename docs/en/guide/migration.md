# Migrating to v3

Migration guide for bringing an existing v1 or v2 organization into the v3 routing model.

## Auto-Detection

When you run `/company`, it checks for these legacy signals and suggests a v3 migration:

- `.company/ceo/` exists
- `.company/` exists but `.company/state.json` does not

```
> /company

Secretary: I've detected an existing organization. Would you like to migrate it to v3?

      Changes:
      - Request routing → Unified around intent-based rules
      - Unclear requests → Held in secretary/inbox/
      - state.json → Added for persistent proposal state
      - Legacy CEO / reviews → Cleaned up if present
      - Active departments → Carried over as-is

      Shall I proceed with the migration?
```

## What Changes

| Older setup | v3 |
|----|-----|
| Ambiguous save behavior | Inbox-first fallback |
| Department suggestions depend on session memory | Suggestions persist in `state.json` |
| Legacy CEO / reviews may remain | Cleaned up during migration |
| Routing guidance is mostly descriptive | Intent-based routing rules are explicit |

## Migration Process

1. Existing owner info and active departments are carried over
2. `.company/state.json` is created or refreshed
3. `ceo/` and `reviews/` are cleaned up if present
4. `.company/CLAUDE.md` is regenerated with v3 rules
5. `secretary/CLAUDE.md` is updated to the v3 version
6. Future department suggestions are driven by `state.json`

::: warning Note
Active departments and real work files are not removed. The migration mainly adds state management and consistent routing rules.
:::

## If You Decline

If you decline, you keep using the current structure. The migration will be suggested again the next time you run `/company`.
