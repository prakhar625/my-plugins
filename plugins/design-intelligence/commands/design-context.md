---
command: design-context
description: Update audience, use cases, or brand context without full reinitialization
disable-model-invocation: true
---

# /design-context

Update design context without full reinitialization.

## Workflow

### Step 1 — Show Current Context
Read and display:
- `.design-intelligence/foundations/audience.md`
- `.design-intelligence/foundations/principles.md`

### Step 2 — Identify Changes
Ask user what they want to update:
- Audience definition
- Core use cases
- Feel/sensory language
- Principles

### Step 3 — Update Context
Modify relevant files in `.design-intelligence/foundations/`.

**GATE — Do not proceed until:**
- [ ] Changes confirmed by user

### Step 4 — Cascade Check
Determine if changes affect tokens:
- Minor clarifications → no token changes
- Significant audience shift → suggest direction review
- Feel change → suggest token regeneration

## Output

- Context files updated
- Cascade actions suggested if needed
- Changes logged in history
