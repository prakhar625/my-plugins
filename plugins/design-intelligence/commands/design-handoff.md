---
command: design-handoff
argument-hint: "[format]"
description: Prepare implementation-ready specs (format: figma, markdown, json)
disable-model-invocation: true
---

# /design-handoff [format]

Prepare design specs for implementation handoff.

## Arguments
- `$0` — Output format: markdown (default), json, figma, css

## Formats

### markdown
Human-readable documentation with code snippets.

### json
Machine-readable token exports for design tools.

### figma
Figma variables format (JSON for Figma import).

### css
CSS custom properties ready for use.

## Workflow

### Step 1 — Confirm Scope
Ask user:
- Full system or specific components?
- Any platform-specific considerations?

### Step 2 — Generate Format
Transform tokens and specs into requested format.

### Step 3 — Save and Deliver
Save to `.design-intelligence/handoff/[format]/`

**GATE — Do not finalize until:**
- [ ] User confirms scope
- [ ] Format validation passes

## Output

Handoff package ready at:
- `.design-intelligence/handoff/[format]/`
