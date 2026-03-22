---
command: design-animate
argument-hint: "[component]"
description: Add or define motion specs for components or transitions
disable-model-invocation: true
---

# /design-animate [component]

Define motion specifications for a component.

## Arguments
- `$0` — Component name or interaction pattern

## Prerequisites
- Motion tokens should exist
- Read `references/domains/motion.md` for guidance

## Workflow

### Step 1 — Identify Animation Needs
For the component, determine:
- Entry/exit animations
- State transitions (hover, active, focus)
- Loading/success/error states

### Step 2 — Apply Motion Decision Framework
For each animation:
1. Should it animate? (Does motion add meaning?)
2. What's the purpose? (Feedback, transition, attention, delight)
3. Select duration and easing from tokens

### Step 3 — Define Motion Spec
Create motion specification:
```yaml
component: [name]
animations:
  - trigger: [event]
    property: [what changes]
    duration: [token-name]
    easing: [token-name]
    reducedMotion: [fallback]
```

### Step 4 — Update Component
Add motion spec to component definition.

**GATE — Do not save until:**
- [ ] All animations have clear purpose
- [ ] Durations ≤400ms for UI feedback
- [ ] prefers-reduced-motion handled

## Output

- Motion spec added to component
- motion.json updated if new patterns needed
- Documentation updated
