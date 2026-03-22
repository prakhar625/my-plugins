# design-intelligence Plugin Specification

**Date:** 2026-03-22
**Status:** Draft
**Version:** 0.1.0

---

## Overview

An intelligent design partner plugin for Claude Code that handles the "detailed and convoluted phase of designing" — from exploration through documentation. It synthesizes knowledge from five authoritative sources into a unified, conversational agent with deep domain expertise.

### Target Audience

Product-minded users with taste who have intuitions about what they want but lack the technical vocabulary to articulate or implement them.

### Core Philosophy

1. **Explores before prescribing** — always gathers context (audience, domain, intent, feel) before recommendations
2. **Speaks the user's language** — translates vague feelings into concrete design decisions
3. **Shows its reasoning** — educational mode explains the *why* (Laws of UX, anti-patterns)
4. **Remembers and evolves** — persistent memory means decisions compound across sessions
5. **Stays strict but flexible** — anti-AI-slop by default, configurable when context demands

---

## Architecture

### Plugin Structure

```
plugins/design-intelligence/
├── .claude-plugin/
│   └── plugin.json
│
├── skills/design-intelligence/
│   ├── SKILL.md                          # Core agent (~400 lines)
│   └── references/
│       ├── foundations/
│       │   ├── laws-of-ux.md             # Fitts, Hick, Miller, Doherty + educational framing
│       │   ├── anti-patterns.md          # AI slop rules + configurable strictness
│       │   └── design-directions.md      # 6 presets + custom direction template
│       │
│       ├── domains/
│       │   ├── typography.md             # Scales, pairing, OpenType, fluid sizing
│       │   ├── color.md                  # OKLCH, domain-driven, tinted neutrals
│       │   ├── spacing.md                # Base units, scales, hierarchy
│       │   ├── motion.md                 # Decision framework, easing curves, timing, a11y
│       │   └── interaction.md            # States, feedback, component patterns
│       │
│       ├── quality/
│       │   ├── accessibility.md          # WCAG AA/AAA, keyboard, focus, semantics
│       │   ├── audit-checklist.md        # All quality gates in one checklist
│       │   └── critique-framework.md     # Swap test, squint test, signature test
│       │
│       └── optional/
│           └── sound.md                  # Audio feedback rules, when to use, a11y
│
├── commands/
│   ├── design-init.md
│   ├── design-direction.md
│   ├── design-context.md
│   ├── design-tokens.md
│   ├── design-components.md
│   ├── design-extract.md
│   ├── design-reference.md
│   ├── design-wireframe.md
│   ├── design-mockup.md
│   ├── design-refine.md
│   ├── design-animate.md
│   ├── design-audit.md
│   ├── design-audit-aaa.md
│   ├── design-critique.md
│   ├── design-polish.md
│   ├── design-document.md
│   ├── design-handoff.md
│   ├── design-history.md
│   └── design-config.md
│
├── agents/
│   ├── design-critic.md
│   ├── token-architect.md
│   └── reference-analyst.md
│
└── hooks/
    └── hooks.json                        # SessionStart: load existing system
```

### Generated Project Memory

```
.design-intelligence/
├── system.md                    # Core design system definition
├── config.json                  # User configuration
│
├── foundations/
│   ├── direction.md             # Chosen direction + rationale
│   ├── principles.md            # What we will/won't do
│   └── audience.md              # Who, what, how it should feel
│
├── tokens/
│   ├── colors.json
│   ├── typography.json
│   ├── spacing.json
│   ├── motion.json
│   ├── radii.json
│   └── shadows.json
│
├── components/                  # Component specs
├── patterns/                    # Navigation, data-display, feedback, forms
├── references/                  # Extracted from /design-reference
├── wireframes/                  # Generated wireframe files
├── mockups/                     # Generated mockup files
├── decisions/                   # Decision log with rationale
└── history/
    └── changelog.md
```

---

## Core Workflow

```
DISCOVER → DEFINE → DESIGN → DOCUMENT → AUDIT
```

### 1. Discover

- Who is the human? (context, not "users")
- What must they accomplish? (the verb)
- What should this feel like? (sensory language)
- Domain exploration: 5+ concepts, 5+ colors, 1 signature element, 3 rejected defaults

### 2. Define

- Choose/blend design direction (presets or custom)
- Establish tokens: color, typography, spacing, motion
- Set principles: what we will and won't do
- Configure strictness: anti-slop level, a11y tier

### 3. Design

- Component specs with rationale
- Wireframes and mockups (framework-agnostic)
- Interaction patterns and states
- Motion specs (timing, easing, triggers)

### 4. Document

- Design system documentation
- Component library specs
- Handoff-ready artifacts

### 5. Audit

- Anti-slop verification
- Accessibility compliance (AA default, AAA opt-in)
- Consistency check against established tokens
- Critique and refinement suggestions

---

## Commands (19)

### Initialization & Direction

| Command | Description |
|---------|-------------|
| `/design-init` | Start fresh: domain exploration, direction selection, token foundation |
| `/design-direction` | View/change design direction (preset, custom, or blend) |
| `/design-context` | Update audience, use cases, or brand context without full reinit |

### Token & System Management

| Command | Description |
|---------|-------------|
| `/design-tokens` | View, edit, or regenerate token system |
| `/design-components` | Define or view component specs |
| `/design-extract` | Extract design patterns from existing code into the system |
| `/design-reference` | Capture inspiration from external sources: URLs, images, products |

### Creation & Refinement

| Command | Description |
|---------|-------------|
| `/design-wireframe` | Generate lo-fi wireframe for a view/component |
| `/design-mockup` | Generate higher-fidelity mockup with tokens applied |
| `/design-refine` | Iteratively improve a specific element or view |
| `/design-animate` | Add/define motion specs for components or transitions |

### Quality & Critique

| Command | Description |
|---------|-------------|
| `/design-audit` | Full audit: anti-slop, consistency, accessibility (AA) |
| `/design-audit-aaa` | Advanced accessibility audit (WCAG AAA) |
| `/design-critique` | Get critical feedback on current design decisions |
| `/design-polish` | Final pass: micro-refinements, edge cases, delight details |

### Documentation & Handoff

| Command | Description |
|---------|-------------|
| `/design-document` | Generate/update design system documentation |
| `/design-handoff` | Prepare implementation-ready specs for developers |
| `/design-history` | View decision history and evolution |

### Configuration

| Command | Description |
|---------|-------------|
| `/design-config` | Configure strictness, a11y level, educational mode, sound module |

---

## Design Presets (6)

| Preset | Feel | Best For |
|--------|------|----------|
| **Precision** | Sharp, dense, efficient | Dev tools, admin panels, IDEs |
| **Warmth** | Friendly, approachable, human | Consumer apps, collaboration tools |
| **Sophistication** | Premium, trustworthy, refined | Finance, legal, enterprise B2B |
| **Boldness** | Confident, clear, assertive | Data-heavy apps, dashboards |
| **Utility** | Functional, honest, tools-first | GitHub-style tools, infrastructure UIs |
| **Delight** | Playful, expressive, memorable | Creative tools, consumer products |

### Preset Behavior

- Presets serve as starting points
- Domain exploration can override or blend presets
- Users can define custom directions in `.design-intelligence/foundations/custom-directions/`
- Custom directions can inherit from presets via `based_on` field

---

## Sub-Agents

### design-critic.md

- **Invoked by:** `/design-critique`
- **Purpose:** Critical, honest feedback on design decisions
- **Approach:** Swap test, squint test, signature test
- **Output:** Ranked issues (critical/major/minor), specific fixes

### token-architect.md

- **Invoked by:** `/design-tokens`, `/design-init`
- **Purpose:** Generate and refine token systems
- **Output:** JSON token files with rationale comments

### reference-analyst.md

- **Invoked by:** `/design-reference`
- **Purpose:** Analyze external references (URLs, images, products)
- **Output:** Structured analysis in `.design-intelligence/references/`

---

## Configuration

### config.json

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

### Strictness Levels

| Level | Behavior |
|-------|----------|
| **strict** | Actively rejects AI-typical patterns, requires confirmation to override |
| **moderate** | Warns but doesn't block |
| **relaxed** | Guidance only in educational mode |

### Accessibility Tiers

| Tier | Scope |
|------|-------|
| **AA** (default) | WCAG 2.1 AA — baked into all decisions |
| **AAA** (opt-in) | WCAG 2.1 AAA — stricter contrast, enhanced targets |

### Educational Mode

When enabled, explains the *why* behind decisions:
- Laws of UX citations
- Anti-pattern reasoning
- Technical rationale for token choices

---

## Source Synthesis

The plugin synthesizes knowledge from five authoritative sources:

| Domain | Primary Sources | Synthesis Approach |
|--------|-----------------|-------------------|
| Laws of UX | Source A | Thresholds: 32px, 300ms, 5-9 chunks, 400ms |
| Anti-patterns | Source B | AI slop test, explicit rejections |
| Design directions | Source C | 6 presets + domain exploration |
| Typography | Source B + A | Scales + OpenType features |
| Color | Source B + C | OKLCH + domain-driven approach |
| Spacing | Source B + C | Grid systems + token architecture |
| Motion | Source D + A | Decision framework + timing rules |
| Interaction | Source D + C | Component patterns + states |
| Accessibility | Source E + A | Deep a11y + Laws of UX integration |
| Sound | Source A | Audio rules (optional module) |

### Synthesis Rules

- **Take the more specific** — exact values over general guidance
- **Take the stricter** — anti-patterns over permissive defaults
- **Preserve unique insights** — domain exploration, sound guidance
- **Unify vocabulary** — one term per concept, defined in SKILL.md
- **Document conflicts** — when sources disagree, explain both and let config decide

---

## Output Formats

### Design Phase (Framework-Agnostic)

- **Tokens:** JSON files with semantic naming
- **Wireframes:** HTML/SVG lo-fi representations
- **Mockups:** HTML with inline styles or CSS variables
- **Specs:** Markdown documentation
- **Decisions:** Markdown with rationale

### Implementation Phase (Framework-Detected)

- Detect framework from codebase (React, Vue, Svelte, vanilla)
- Generate implementation using established tokens
- Respect existing patterns and conventions

---

## Key Behaviors

### Memory

- Auto-loads `system.md` and `config.json` on session start
- Prompts to save after significant decisions
- Never overwrites silently — confirms destructive changes
- Works with partial systems (not all files required)

### Commands

- All commands are shortcuts — conversational paths work too
- Commands respect established memory
- Commands confirm destructive changes
- Commands support arguments (e.g., `/design-audit src/components/`)

### Anti-Slop

- Strict by default
- Configurable via `/design-config` or `config.json`
- Contextual overrides with human confirmation
- Specific patterns can be allowlisted in `ignoredAntiPatterns`

---

## Success Criteria

1. **Activation:** Skill loads for natural prompts ("help me design", "I need a dashboard", "make this look better")
2. **Exploration:** Never prescribes without first gathering context
3. **Memory:** Decisions persist and compound across sessions
4. **Quality:** Output passes anti-slop test — doesn't look AI-generated
5. **Accessibility:** AA compliance baked in, AAA available
6. **Handoff:** Produces implementation-ready specs and tokens
7. **Education:** Users learn design vocabulary through use

---

## Out of Scope

- Visual documentation of existing codebases (use `visual-documentation` plugin)
- Marketing/landing page design (different concerns than product UI)
- Actual implementation — this plugin produces specs, not code
- Brand identity creation (logos, brand guidelines) — product UI only
