# Motion Reference

## Goal
Add purposeful motion that enhances rather than distracts.

## Prerequisites
- [ ] Design direction established (affects motion character)
- [ ] Accessibility requirements confirmed (reduced motion support)

## Motion Decision Framework

1. **Should it animate?**
   - Does motion communicate something?
   - Would static be equally clear?
   - If unsure, don't animate

2. **What's the purpose?**
   - Feedback (button press)
   - Transition (page change)
   - Attention (notification)
   - Delight (celebration)

3. **How should it move?**
   - Easing curve
   - Duration
   - Property changes

## Durations

```json
{
  "instant": "0ms",
  "fast": "150ms",
  "normal": "250ms",
  "slow": "400ms",
  "deliberate": "600ms"
}
```

Guidelines:
- UI feedback: fast (150ms)
- Transitions: normal (250ms)
- Emphasis: slow (400ms)
- Never exceed 600ms for UI

## Easing Curves

```json
{
  "default": "cubic-bezier(0.23, 1, 0.32, 1)",
  "enter": "cubic-bezier(0.21, 1.02, 0.73, 1)",
  "exit": "cubic-bezier(0.06, 0.71, 0.55, 1)",
  "inOut": "cubic-bezier(0.77, 0, 0.175, 1)"
}
```

**Avoid:** Bounce easing unless direction explicitly calls for playfulness.

## Reduced Motion

**Always respect `prefers-reduced-motion`:**

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

Fallback: opacity-only transitions

## Common Patterns

| Element | Duration | Easing | Transform |
|---------|----------|--------|-----------|
| Button press | fast | default | scale(0.97) |
| Popover enter | normal | enter | scale(0.95)→1 |
| Modal enter | normal | enter | opacity, translateY |
| Toast slide | normal | enter | translateY |
| Menu expand | fast | default | opacity, height |

## Validation Gates

- [ ] All motion has clear purpose
- [ ] Durations ≤400ms for UI
- [ ] prefers-reduced-motion handled
- [ ] No bounce easing (unless direction allows)

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Motion feels slow | Durations too long | Keep UI feedback under 250ms |
| Accessibility issues | No reduced-motion support | Add prefers-reduced-motion media query |
| Feels cheap | Bounce/spring easing overused | Use professional ease-out curves |
| Distracting | Motion without purpose | Remove or simplify |
