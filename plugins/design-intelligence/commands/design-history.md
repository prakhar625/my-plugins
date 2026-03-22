---
command: design-history
description: View decision history and design evolution
disable-model-invocation: true
---

# /design-history

View the history of design decisions and evolution.

## Prerequisites
- Design system must exist
- Decisions logged in `.design-intelligence/decisions/`

## Workflow

### Step 1 — Load History
Read from:
- `.design-intelligence/decisions/` (individual decisions)
- `.design-intelligence/history/changelog.md` (evolution log)
- `.design-intelligence/explorations/` (past explorations)

### Step 2 — Present Timeline
Show chronological view:

```markdown
## Design History

### [Date] — [Decision Title]
**Context:** [Why this decision was needed]
**Options Considered:** [A, B, C]
**Decision:** [What was chosen]
**Rationale:** [Why]

### [Earlier Date] — [Earlier Decision]
...
```

### Step 3 — Offer Actions
- View specific decision details
- Compare before/after states
- Revisit past explorations

## Output

- Chronological decision history
- Context and rationale preserved
- Exploration artifacts accessible
