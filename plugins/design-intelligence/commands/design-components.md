---
command: design-components
argument-hint: "[component-name]"
description: Define or view component specs with states and token mappings
disable-model-invocation: true
---

# /design-components [component-name]

Manage component specifications.

## Arguments
- `$0` — (Optional) Component name: button, input, card, modal, etc.

## Prerequisites
- Design system must be initialized
- Tokens should exist

## Workflow

### Without Argument — List Components
1. Show all defined components in `.design-intelligence/components/`
2. Display completion status (states defined, tokens mapped)

### With Argument — Component Detail
1. If exists: show full spec
2. If new: guide through definition

## Component Definition

Guide user through:
- Visual states: default, hover, active, focus, disabled
- Data states: loading, empty, error (if applicable)
- Token mappings: which tokens apply to which properties
- Variants: sizes, themes, modes

**GATE — Do not save until:**
- [ ] All 5 visual states defined
- [ ] All properties mapped to tokens (no arbitrary values)

## Output

- Component spec saved to `.design-intelligence/components/[name].md`
- Includes full state definitions and token mappings
