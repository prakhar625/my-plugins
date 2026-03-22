---
command: design-config
argument-hint: "[setting]"
description: Configure strictness, accessibility level, educational mode, sound module
disable-model-invocation: true
---

# /design-config [setting]

Configure plugin settings.

## Arguments
- `$0` — (Optional) Setting to modify

## Available Settings

| Setting | Values | Default | Description |
|---------|--------|---------|-------------|
| `strictness` | strict, moderate, relaxed | strict | Anti-slop enforcement level |
| `accessibility` | AA, AAA | AA | WCAG compliance tier |
| `educationalMode` | true, false | true | Explain the "why" behind decisions |
| `soundModule` | true, false | false | Enable sound design features |
| `autoSaveDecisions` | true, false | true | Log decisions automatically |
| `confirmDestructive` | true, false | true | Confirm before overwriting |

## Workflow

### Without Argument — View All
Display current configuration from `.design-intelligence/config.json`

### With Argument — Modify Setting
```
/design-config strictness moderate
/design-config accessibility AAA
/design-config educationalMode false
```

## Configuration File

`.design-intelligence/config.json`:
```json
{
  "strictness": "strict",
  "accessibility": "AA",
  "educationalMode": true,
  "soundModule": false,
  "autoSaveDecisions": true,
  "confirmDestructive": true,
  "customDirections": [],
  "ignoredAntiPatterns": []
}
```

## Strictness Levels

### strict (default)
- Actively rejects AI-typical patterns
- Requires user confirmation to override
- Best for: Final output quality

### moderate
- Warns about anti-patterns but allows
- Explains why patterns are problematic
- Best for: Learning and exploration

### relaxed
- Guidance only, no blocking
- Educational notes in output
- Best for: Rapid prototyping

## Output

- Current or updated configuration displayed
- Changes saved to config.json
- Effect explanation provided
