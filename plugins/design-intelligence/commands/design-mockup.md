---
command: design-mockup
argument-hint: "[view-name]"
description: Generate higher-fidelity mockup with full tokens applied
disable-model-invocation: true
---

# /design-mockup [view-name]

Generate a higher-fidelity mockup with full design system applied.

## Arguments
- `$0` — View name (can reference existing wireframe)

## Prerequisites
- Design system must be initialized
- Ideally, wireframe exists (but not required)

## Workflow

### Step 1 — Load Context
1. Read design direction and tokens
2. Load wireframe if exists
3. Load relevant component specs

### Step 2 — Generate Mockup
Create styled HTML mockup:
- Apply color tokens fully
- Use typography at correct scales
- Include spacing and motion tokens
- Add interaction states (via CSS)

### Step 3 — Validate
Run quick audit:
- Anti-slop check
- Accessibility check (contrast)
- Token consistency check

### Step 4 — Save and Preview
Save to `.design-intelligence/mockups/[view-name].html`

**GATE — Do not finalize until:**
- [ ] Passes anti-slop check
- [ ] Meets accessibility requirements
- [ ] All values trace to tokens

## Output

- Mockup HTML saved
- Validation report included
- Ready for refinement or handoff
