# Color Reference

## Goal
Build a color system rooted in the product's domain and direction.

## Prerequisites
- [ ] Domain exploration complete (5+ domain colors identified)
- [ ] Design direction established

## OKLCH Color Space

Use OKLCH for perceptually uniform colors:
```
oklch(lightness% chroma hue)
```

- **Lightness:** 0-100% (0 = black, 100 = white)
- **Chroma:** 0-0.4 (0 = gray, higher = more saturated)
- **Hue:** 0-360 degrees

Benefits:
- Consistent perceived brightness across hues
- Predictable color modifications
- Better accessibility calculations

## Domain-Driven Color Selection

Before choosing colors, explore:
1. **What colors occur naturally in this domain?**
   - Healthcare: clinical blues, greens, whites
   - Finance: navy, gold, silver
   - Food: warm earth tones, appetite-inducing reds

2. **What associations do users have?**
   - Warning colors (red/yellow)
   - Success colors (green)
   - Domain-specific meanings

## Tinted Neutrals

Never use pure gray. Tint neutrals with:
- Primary hue for cohesion
- Warm undertones for approachability
- Cool undertones for professionalism

Example:
```
/* Instead of gray-500: oklch(55% 0 0) */
gray-500-tinted: oklch(55% 0.015 250) /* slight blue tint */
```

## Semantic Mappings

Define purpose, not just color:
- `--color-primary`: Main brand action
- `--color-success`: Positive outcomes
- `--color-warning`: Caution required
- `--color-error`: Problems/failures
- `--color-info`: Neutral information

## Contrast Requirements

- **AA (required):** 4.5:1 for normal text, 3:1 for large text
- **AAA (enhanced):** 7:1 for normal text, 4.5:1 for large text
- **Non-text:** 3:1 for UI components

## Validation Gates

- [ ] All text meets AA contrast (4.5:1)
- [ ] No pure gray (#808080 or oklch with 0 chroma)
- [ ] Semantic colors defined (success, warning, error)
- [ ] Colors trace to domain exploration

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Poor contrast | Colors not tested | Run contrast checker, adjust lightness |
| Generic palette | Domain not explored | Revisit domain colors |
| Muddy neutrals | Pure gray used | Add tint from primary hue |
| Inconsistent meanings | No semantic mapping | Define semantic color tokens |
