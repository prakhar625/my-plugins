---
command: design-init
description: Initialize a new design system with domain exploration and direction selection
disable-model-invocation: true
---

# /design-init

Initialize a new design system for this project.

## Prerequisites

Check if `.design-intelligence/` already exists:
- If yes: warn user, confirm before overwriting
- If no: proceed with initialization

## Workflow

### Step 1 — Context Gathering

Read `references/foundations/design-directions.md` for exploration framework.

Ask the user:
- Who is the primary user? (role, context, expertise)
- What must they accomplish? (core task, verb)
- How should this feel? (sensory language, not "clean and modern")

**GATE — Do not proceed until:**
- [ ] All three questions answered with specifics
- [ ] "Clean and modern" rejected if offered

### Step 2 — Domain Exploration

Guide user through:
- 5+ domain vocabulary concepts
- 5+ naturally occurring colors
- 1 signature element unique to this product
- 3 default choices being rejected (and why)

**GATE — Do not proceed until:**
- [ ] Domain vocabulary captured (minimum 5)
- [ ] Color world established (minimum 5)
- [ ] Signature element articulated
- [ ] Rejected defaults documented

### Step 3 — Direction Selection

Present 6 presets with recommendation based on exploration.
Allow blending or custom direction.

**GATE — Do not proceed until:**
- [ ] Direction confirmed by user

### Step 4 — Token Foundation

Invoke `token-architect` agent to generate initial tokens.
Save to `.design-intelligence/tokens/`.

**GATE — Do not proceed until:**
- [ ] All token files generated (colors, typography, spacing, motion, shadows, radii)
- [ ] Tokens validated for accessibility (contrast ratios)

### Step 5 — Save System

Create `.design-intelligence/system.md` with direction and principles.
Create `.design-intelligence/config.json` with defaults.

## Output

- `.design-intelligence/` directory structure created
- Initial tokens generated and validated
- System documented and ready for use
