---
command: design-tokens
argument-hint: "[token-type]"
description: View, edit, or regenerate token system (colors, typography, spacing, motion)
disable-model-invocation: true
---

# /design-tokens [token-type]

Manage the design token system.

## Arguments
- `$0` — (Optional) Token type: colors, typography, spacing, motion, shadows, radii

## Prerequisites
- `.design-intelligence/tokens/` must exist
- If not, suggest running `/design-init` first

## Workflow

### Without Argument — Overview
1. List all token files with summary stats
2. Show last modified dates
3. Highlight any validation issues

### With Argument — Token Type
1. Display full token file contents
2. Explain key decisions
3. Offer options: edit, regenerate, validate

## Edit Mode
Allow user to:
- Modify individual token values
- Add new tokens
- Remove deprecated tokens

**GATE — Do not save until:**
- [ ] Changes validated for accessibility
- [ ] User confirms changes

## Regenerate Mode
1. Invoke `token-architect` agent
2. Regenerate specified token type
3. Preserve custom additions if requested

## Output

- Token files updated or displayed
- Validation results shown
- Changes logged in history
