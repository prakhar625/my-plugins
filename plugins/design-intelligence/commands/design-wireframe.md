---
command: design-wireframe
argument-hint: "[view-name]"
description: Generate lo-fi wireframe for a view or component
disable-model-invocation: true
---

# /design-wireframe [view-name]

Generate a lo-fi wireframe using established tokens.

## Arguments
- `$0` — View or component name (e.g., "settings-page", "user-profile")

## Prerequisites
- Design system must be initialized
- If no system exists, offer to run `/design-init` first

## Workflow

### Step 1 — Gather Requirements
Ask user:
- What is this view's primary purpose?
- What key elements must be present?
- Any reference views in the system?

### Step 2 — Generate Wireframe
Create lo-fi HTML wireframe:
- Use spacing tokens for layout
- Use typography tokens for text hierarchy
- Use neutral colors (structure, not style)
- Include placeholder content

### Step 3 — Save and Preview
Save to `.design-intelligence/wireframes/[view-name].html`
Provide preview instructions.

**GATE — Do not proceed until:**
- [ ] User approves wireframe direction
- [ ] All elements use tokens (no arbitrary values)

## Output

- Wireframe HTML saved
- Preview link provided
- Ready for refinement or mockup conversion
