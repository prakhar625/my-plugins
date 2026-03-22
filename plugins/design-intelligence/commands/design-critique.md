---
command: design-critique
description: Get critical feedback on current design decisions
disable-model-invocation: true
---

# /design-critique

Get critical feedback on the design system.

## Prerequisites
- Design system must exist
- Read `references/quality/critique-framework.md`

## Workflow

### Step 1 — Gather Context
Load current design artifacts:
- system.md
- Token files
- Component specs
- Mockups (if any)

### Step 2 — Invoke Critic
Dispatch `design-critic` agent with:
- All design artifacts
- Direction and principles
- Any specific concerns from user

### Step 3 — Present Findings
Display critique with:
- Swap test results
- Squint test results
- Signature test results
- Ranked issues with fixes
- Acknowledged strengths

## Output

The `design-critic` agent returns:

### Critical Issues (must fix)
- [Issue]: [Why] → [Fix]

### Major Issues (should fix)
- [Issue]: [Why] → [Fix]

### Minor Issues (nice to fix)
- [Issue]: [Why] → [Fix]

### Strengths
- [What's working well]
