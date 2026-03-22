# Sound Design Reference

## Goal
Add purposeful audio feedback when appropriate.

## Prerequisites
- [ ] Core design system complete (sound is optional layer)
- [ ] Interaction states defined (triggers for sound)
- [ ] Accessibility requirements confirmed (visual equivalents exist)

## When to Use Sound

### Appropriate Uses
- **Payment confirmations:** Success chime reinforces completion
- **Error alerts:** Audio draws attention to critical problems
- **Notifications:** Ambient sound for background updates
- **Celebrations:** Milestone achievements

### Avoid Sound For
- Decorative hovers
- Every button click
- Keyboard navigation
- Form validation
- Page transitions

## Accessibility Requirements

**Every sound must have:**
1. Visual equivalent (sound is supplementary, not primary)
2. Toggle to disable (user control)
3. prefers-reduced-motion respect (when applicable)

```css
@media (prefers-reduced-motion: reduce) {
  /* Also reduce or disable audio feedback */
}
```

## Sound Characteristics

### Duration
- UI feedback: 50-200ms
- Notifications: 200-500ms
- Celebrations: 500-1500ms

### Frequency Range
- Avoid very high frequencies (>10kHz) — fatiguing
- Avoid very low frequencies (<100Hz) — inaudible on many devices
- Pleasant range: 200Hz-4kHz

### Volume
- Default to quiet (user can increase)
- Never startle
- Test with headphones and speakers

## Sound Palette

Like colors, sounds should be cohesive:

| Type | Characteristics |
|------|-----------------|
| Success | Ascending tone, major key |
| Error | Descending tone, minor key |
| Warning | Neutral, attention-getting |
| Notification | Soft, ambient |

## Implementation Guidance

Sound is an **optional module**. Enable via:
```
/design-config soundModule enabled
```

When enabled:
1. Define sound palette in `.design-intelligence/tokens/sound.json`
2. Document triggers in component specs
3. Ensure all a11y requirements met

## Validation Gates

- [ ] Sound is supplementary (visual equivalent exists)
- [ ] User can disable sounds
- [ ] Sounds are cohesive (palette defined)
- [ ] Duration appropriate for context
- [ ] Volume is comfortable

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| No visual fallback | Sound as primary feedback | Add visual equivalent for every sound |
| Cannot disable | Missing user control | Add sound toggle in settings |
| Startling volume | Not tested on headphones | Default to quiet, test multiple devices |
| Incoherent palette | Sounds added ad-hoc | Define sound palette upfront like colors |
| Overuse | Sound on every interaction | Limit to meaningful moments (success, error, notification) |
| Accessibility failure | Ignored reduced-motion | Disable or reduce audio for prefers-reduced-motion |
