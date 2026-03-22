# Typography Reference

## Goal
Establish typographic foundations that reinforce the design direction.

## Prerequisites
- [ ] Design direction established
- [ ] Audience context gathered (expertise level affects complexity)

## Type Scales

Use harmonious ratios:
- **Minor Second (1.067):** Dense UIs, code editors
- **Major Second (1.125):** Compact, professional
- **Minor Third (1.2):** Balanced, versatile (recommended default)
- **Major Third (1.25):** Clear hierarchy, marketing
- **Perfect Fourth (1.333):** Bold, dramatic

## Font Pairing Rules

1. **Contrast without clash:** Pair serif with sans, not similar fonts
2. **Limit to 2 fonts:** Display + body is enough
3. **Match x-height:** Fonts should align visually at same size
4. **Consider weight range:** Ensure both have needed weights

## Fluid Typography

Use `clamp()` for responsive sizing:

```css
font-size: clamp(1rem, 0.5rem + 2vw, 1.5rem);
```

Guidelines:
- Minimum: readable on mobile (16px base)
- Maximum: comfortable on desktop (don't exceed 1.5x mobile)
- Growth: moderate viewport scaling

## Line Height

- **Body text:** 1.5-1.7
- **Headings:** 1.1-1.3
- **Dense UI:** 1.3-1.4
- **Large display:** 1.0-1.1

## Tracking (Letter Spacing)

- **Uppercase:** +0.05em to +0.1em
- **Small text:** +0.01em to +0.02em
- **Large display:** -0.02em to -0.05em
- **Body:** 0 (default)

## OpenType Features

Enable when available:
- `font-feature-settings: "kern"` — Kerning
- `font-feature-settings: "liga"` — Ligatures
- `font-variant-numeric: tabular-nums` — Aligned numbers in data

## Validation Gates

- [ ] Base size ≥16px for body text
- [ ] Line heights set per context
- [ ] No more than 2 font families
- [ ] Scale ratio matches direction

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Poor readability | Base size too small | Increase to 16px minimum |
| Visual monotony | Single weight used | Introduce heading/body contrast |
| Font loading issues | Too many weights | Limit to 3-4 weights total |
| Inconsistent scale | Ad-hoc sizes | Use defined scale ratio |
