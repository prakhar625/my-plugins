---
command: design-audit-aaa
argument-hint: "[path]"
description: Advanced accessibility audit (WCAG AAA requirements)
disable-model-invocation: true
---

# /design-audit-aaa [path]

Run enhanced accessibility audit with WCAG AAA requirements.

## Arguments
- `$0` — (Optional) Path to audit. Defaults to entire design system.

## Prerequisites
- Design system must exist
- Read `references/quality/accessibility.md`

## WCAG AAA Requirements

### Contrast
- [ ] Text contrast ≥7:1 (vs 4.5:1 for AA)
- [ ] Large text contrast ≥4.5:1 (vs 3:1 for AA)

### Targets
- [ ] Touch targets ≥48px (vs 44px for AA)
- [ ] 8px spacing between targets

### Content
- [ ] Reading level appropriate
- [ ] No timing-dependent content
- [ ] Multiple ways to locate content

### Focus
- [ ] Enhanced focus visibility
- [ ] Context-sensitive help available

## Workflow

1. Run standard AA audit first
2. Apply additional AAA requirements
3. Document gaps between AA and AAA
4. Provide upgrade recommendations

## Output

```markdown
## AAA Accessibility Report

### Current Level: [AA/AAA]

### AAA Gaps
- [Gap 1]: [Current] → [AAA requirement]
- [Gap 2]: [Current] → [AAA requirement]

### Upgrade Path
1. [Highest impact upgrade]
2. [Next upgrade]
```
