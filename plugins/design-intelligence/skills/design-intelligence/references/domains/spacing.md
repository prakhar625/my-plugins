# Spacing Reference

## Goal
Create consistent spatial rhythm through a systematic scale.

## Base Unit

Choose one:
- **4px:** Dense UIs, data-heavy applications
- **8px:** Standard choice, most applications

All spacing derives from the base unit.

## Spacing Scale

Standard scale (8px base):
```
--space-0: 0px
--space-1: 4px    (0.5x)
--space-2: 8px    (1x)
--space-3: 12px   (1.5x)
--space-4: 16px   (2x)
--space-5: 24px   (3x)
--space-6: 32px   (4x)
--space-7: 48px   (6x)
--space-8: 64px   (8x)
--space-9: 96px   (12x)
```

## Spacing Contexts

### Micro (within components)
- Icon to label: 4-8px
- Input padding: 8-12px
- Button padding: 8-16px

### Component (between elements)
- Form field gap: 16-24px
- Card padding: 16-24px
- Section gap: 24-32px

### Section (layout level)
- Page margins: 24-64px
- Section padding: 48-96px
- Container max-width gutters: 5-10%

## Vertical Rhythm

Maintain consistent line-height multiples:
- Base line-height: 24px (1.5 × 16px)
- Margins as multiples: 24px, 48px, 72px

## Validation Gates

- [ ] All spacing values from the scale
- [ ] No arbitrary pixel values
- [ ] Consistent rhythm across components
- [ ] Touch targets ≥44px (mobile)
