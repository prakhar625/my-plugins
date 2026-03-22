---
command: design-refine
argument-hint: "[element]"
description: Iteratively improve a specific element or view
disable-model-invocation: true
---

# /design-refine [element]

Iteratively refine a design element based on feedback.

## Arguments
- `$0` — Element to refine (component name, view name, or specific aspect)

## Prerequisites
- Element must exist (wireframe, mockup, or component)

## Workflow

### Step 1 — Load Current State
Read the current element from:
- `.design-intelligence/wireframes/`
- `.design-intelligence/mockups/`
- `.design-intelligence/components/`

### Step 2 — Gather Feedback
Ask user:
- What's not working?
- What feeling are you trying to achieve?
- Any specific references?

### Step 3 — Propose Refinements
Offer 2-3 refinement options:
- Option A: [specific changes]
- Option B: [alternative approach]
- Option C: [different direction]

### Step 4 — Apply and Iterate
Apply chosen refinement, update files.

**GATE — Do not proceed until:**
- [ ] User selects refinement direction
- [ ] Changes maintain token consistency

## Output

- Element updated
- Before/after documented in explorations/
- Ready for further refinement or approval
