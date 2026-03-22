# Anti-Patterns Reference

## Goal
Avoid AI-typical patterns that signal generic, low-effort output.

## Prerequisites
- [ ] Design direction established
- [ ] Strictness level configured (default: strict)

## The AI Slop Test

Before shipping any design, ask: "Could this have been the first result from an AI image generator?"
If yes, it needs work.

## Explicit Rejections

### Gray Text on Colored Backgrounds
**What:** Gray (#666, #888) text on colored surfaces
**Why rejected:** Looks desaturated and lifeless
**Alternative:** Use tinted neutrals that harmonize with the background color

### Pure Black (#000000)
**What:** Using pure black for text or backgrounds
**Why rejected:** Too harsh, creates excessive contrast
**Alternative:** Use near-black with slight warmth (oklch 12-15% lightness, 0.01-0.02 chroma)

### Card Nesting (>2 levels)
**What:** Cards inside cards inside cards
**Why rejected:** Creates visual noise and unclear hierarchy
**Alternative:** Use whitespace and subtle dividers, flatten hierarchy

### Bounce Easing
**What:** cubic-bezier curves that overshoot
**Why rejected:** Looks playful/cheap, often inappropriate
**Alternative:** Use smooth ease-out curves for professional feel

### Glassmorphism (overused)
**What:** Blurred transparent backgrounds everywhere
**Why rejected:** Often illegible, poor accessibility, overused
**Alternative:** Use solid backgrounds with subtle shadows for depth

### Generic Gradient Backgrounds
**What:** Blue-to-purple or orange-to-pink gradients
**Why rejected:** AI-image-generator aesthetic
**Alternative:** Single colors or purposeful, subtle gradients

### Stock Icon Syndrome
**What:** Generic, mismatched icons from free packs
**Why rejected:** Inconsistent style, no personality
**Alternative:** Curated icon set with consistent weight and style

## Strictness Levels

| Level | Behavior |
|-------|----------|
| `strict` (default) | Reject all patterns above, require user confirmation to override |
| `moderate` | Warn but allow with acknowledgment |
| `relaxed` | Flag for awareness only |

Configure via `/design-config strictness [level]`

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Design feels generic | Too many defaults accepted | Revisit domain exploration, find signature elements |
| Looks "AI-generated" | Multiple anti-patterns present | Audit against list above, fix each |
| User frustrated by rejections | Strictness too high for context | Adjust via /design-config |
