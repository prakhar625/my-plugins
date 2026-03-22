---
command: design-document
description: Generate or update design system documentation
disable-model-invocation: true
---

# /design-document

Generate comprehensive design system documentation.

## Prerequisites
- Design system must be initialized
- Tokens and components should exist

## Workflow

### Step 1 — Gather All Artifacts
Read from `.design-intelligence/`:
- system.md (core definition)
- foundations/ (direction, principles, audience)
- tokens/ (all token files)
- components/ (all component specs)

### Step 2 — Generate Documentation
Create `.design-intelligence/documentation/design-system.md`:

```markdown
# [Project] Design System

## Overview
[Direction, principles, audience summary]

## Design Tokens

### Colors
[Color tokens with usage notes]

### Typography
[Type scale with examples]

### Spacing
[Spacing scale with guidelines]

### Motion
[Animation patterns with timing]

## Components
[Component specs with states]

## Usage Guidelines
[How to apply the system]
```

### Step 3 — Save and Confirm
Save to `.design-intelligence/documentation/`

## Output

- Full documentation generated
- Ready for team sharing
- Can export to other formats via `/design-handoff`
