# Design Directions Reference

## Goal
Guide aesthetic decisions through coherent design presets.

## Prerequisites
- [ ] Context gathering complete (audience, task, feel)
- [ ] Domain exploration started (vocabulary, colors)

## The 6 Presets

### Precision
**Feel:** Sharp, dense, efficient
**Best for:** Dev tools, admin panels, IDEs
**Defaults:**
- Typography: Monospace-influenced, tight tracking
- Colors: High contrast, cool neutrals
- Spacing: Dense, minimal padding
- Motion: Fast, functional (150ms)

### Warmth
**Feel:** Friendly, approachable, human
**Best for:** Consumer apps, collaboration tools
**Defaults:**
- Typography: Rounded sans-serif, generous line height
- Colors: Warm neutrals, soft primaries
- Spacing: Generous padding, breathing room
- Motion: Smooth, natural (250ms)

### Sophistication
**Feel:** Premium, trustworthy, refined
**Best for:** Finance, legal, enterprise B2B
**Defaults:**
- Typography: Classic serif accents, balanced sans
- Colors: Muted, desaturated palettes
- Spacing: Balanced, intentional whitespace
- Motion: Subtle, deliberate (300ms)

### Boldness
**Feel:** Confident, clear, assertive
**Best for:** Data-heavy apps, dashboards
**Defaults:**
- Typography: Strong weights, clear hierarchy
- Colors: Saturated primaries, strong contrast
- Spacing: Clear sections, bold dividers
- Motion: Purposeful, decisive (200ms)

### Utility
**Feel:** Functional, honest, tools-first
**Best for:** GitHub-style tools, infrastructure UIs
**Defaults:**
- Typography: System fonts, practical sizing
- Colors: Minimal palette, functional accents
- Spacing: Compact but clear
- Motion: Minimal, functional only

### Delight
**Feel:** Playful, expressive, memorable
**Best for:** Creative tools, consumer products
**Defaults:**
- Typography: Personality fonts, varied weights
- Colors: Vibrant, unexpected combinations
- Spacing: Dynamic, playful rhythm
- Motion: Expressive, characterful (300-400ms)

## Blending Presets

Combine up to 2 presets with weighted influence:
- Primary (70%): Core feel and defaults
- Secondary (30%): Accent behaviors

Example: `Sophistication + Warmth` = Premium but approachable

## Domain Exploration Framework

Before selecting a direction, explore:

1. **Domain vocabulary** (5+ concepts)
   - What words does this world use?
   - What concepts are familiar to users?

2. **Domain colors** (5+ colors)
   - What colors naturally occur in this domain?
   - What associations do users have?

3. **Signature element** (1 unique choice)
   - What makes this product distinctive?
   - What should be memorable?

4. **Rejected defaults** (3+ with reasons)
   - What obvious choices are we avoiding?
   - Why are we different?

## Custom Direction Template

```yaml
# .design-intelligence/foundations/custom-directions/[name].yaml
name: my-direction
tagline: "Brief description of feel"
based_on: [preset1, preset2]  # Optional

overrides:
  color:
    temperature: warm|cool|neutral
    primary: "oklch(...)"
  typography:
    display: "Font Name"
    body: "Font Name"
  motion:
    speed: fast|normal|slow
    easing: "cubic-bezier(...)"

principles:
  - "Principle 1"
  - "Principle 2"

anti-patterns:
  - "Pattern to avoid"
```

## Validation Gates

**Before finalizing direction:**
- [ ] Direction matches audience expectations
- [ ] Feel articulated in sensory terms
- [ ] Domain exploration informs choice
- [ ] User confirms direction

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Direction feels generic | Skipped domain exploration | Revisit vocabulary, colors, signature |
| Mismatch with audience | Assumed without asking | Confirm with context questions |
| Preset too rigid | Forced single preset | Consider blending or custom |
| Vague direction | "Clean and modern" accepted | Push for specific sensory language |
