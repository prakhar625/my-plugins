---
command: design-audit
argument-hint: "[path]"
description: Full audit: anti-slop, consistency, accessibility (AA)
disable-model-invocation: true
---

# /design-audit [path]

Run a comprehensive design audit.

## Arguments
- `$0` — (Optional) Path to audit. Defaults to entire design system.

## Prerequisites
- Design system must exist
- Read `references/quality/audit-checklist.md`
- Read `references/quality/accessibility.md`

## Workflow

### Step 1 — Anti-Slop Check
Verify against `references/foundations/anti-patterns.md`:
- [ ] No gray text on colored backgrounds
- [ ] No pure black (#000000)
- [ ] No card nesting >2 levels
- [ ] No bounce easing
- [ ] No overused glassmorphism
- [ ] No generic gradients

### Step 2 — Accessibility Check (AA)
- [ ] Text contrast ≥4.5:1
- [ ] Large text contrast ≥3:1
- [ ] Touch targets ≥44px
- [ ] Focus states visible
- [ ] Keyboard navigation works

### Step 3 — Consistency Check
- [ ] All colors from token system
- [ ] All spacing from scale
- [ ] All typography from scale
- [ ] No orphaned values

### Step 4 — Report
Generate audit report with:
- Pass/fail for each category
- Specific issues found
- Fix recommendations

## Output

```markdown
## Audit Report: [scope]

### Anti-Slop: [PASS/FAIL]
- [Issues if any]

### Accessibility (AA): [PASS/FAIL]
- [Issues if any]

### Consistency: [PASS/FAIL]
- [Issues if any]

### Recommended Fixes
1. [Priority fix]
2. [Next fix]
```
