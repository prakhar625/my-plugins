---
command: design-direction
argument-hint: "[preset-name]"
description: View or change the design direction (preset, custom, or blend)
disable-model-invocation: true
---

# /design-direction [preset-name]

View or change the design direction.

## Arguments
- `$0` — (Optional) Preset name: precision, warmth, sophistication, boldness, utility, delight

## Workflow

### Without Argument — View Current
1. Read `.design-intelligence/foundations/direction.md`
2. Display current direction with rationale
3. Show available presets for reference

### With Argument — Change Direction
1. Validate preset name or parse blend (e.g., "sophistication+warmth")
2. Confirm with user before changes
3. Update `.design-intelligence/foundations/direction.md`
4. Offer to regenerate tokens with new direction

**GATE — Do not proceed with regeneration until:**
- [ ] User confirms direction change
- [ ] User decides on token regeneration

## Presets

| Preset | Feel |
|--------|------|
| precision | Sharp, dense, efficient |
| warmth | Friendly, approachable, human |
| sophistication | Premium, trustworthy, refined |
| boldness | Confident, clear, assertive |
| utility | Functional, honest, tools-first |
| delight | Playful, expressive, memorable |

## Output

- Direction file updated
- Tokens regenerated (if requested)
- Decision logged in history
