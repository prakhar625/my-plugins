# Audit Checklist Reference

## Goal
Systematic quality verification for design outputs.

## Anti-Slop Checklist

- [ ] No gray text on colored backgrounds
- [ ] No pure black (#000000)
- [ ] No card nesting beyond 2 levels
- [ ] No bounce easing curves
- [ ] No overused glassmorphism
- [ ] No generic gradient backgrounds
- [ ] No stock icon syndrome
- [ ] Would fail "AI image generator" test

## Accessibility Checklist (AA)

- [ ] Text contrast ≥4.5:1
- [ ] Large text contrast ≥3:1
- [ ] UI component contrast ≥3:1
- [ ] Touch targets ≥44px
- [ ] Focus states visible
- [ ] Keyboard navigation works
- [ ] Labels on all form inputs
- [ ] Error messages present

## Consistency Checklist

- [ ] All colors from token system
- [ ] All spacing from scale
- [ ] All typography from scale
- [ ] All motion from defined curves
- [ ] No arbitrary values
- [ ] Components use established patterns

## Completeness Checklist

- [ ] All 5 component states defined (default, hover, active, focus, disabled)
- [ ] Loading states for async operations
- [ ] Empty states for data views
- [ ] Error states with recovery guidance
- [ ] Mobile considerations addressed

## Performance Checklist

- [ ] Motion durations ≤400ms
- [ ] No unnecessary animations
- [ ] prefers-reduced-motion handled
- [ ] Image optimization considered
- [ ] Font loading strategy defined

## Audit Process

1. **Run each checklist in order**
2. **Document failures with specifics**
3. **Prioritize fixes:** Critical (blocks ship) > Important (should fix) > Minor (nice to fix)
4. **Re-audit after fixes**

## Common Failure Patterns

| Pattern | Usually Causes | Fix |
|---------|---------------|-----|
| "It looks fine to me" | Skipped contrast check | Run actual contrast checker |
| Orphaned values | New feature bypassed tokens | Add to token system |
| Missing states | Rush to ship | Add states before polish |
| Keyboard broken | Only tested with mouse | Tab through entire flow |
