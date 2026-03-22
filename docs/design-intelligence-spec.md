# design-intelligence Plugin Specification

**Date:** 2026-03-22
**Status:** Draft
**Version:** 2026.3.22.0001

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

## SKILL.md Specification

### Frontmatter

```yaml
---
name: design-intelligence
description: >
  Use when designing UI systems, creating design tokens, establishing visual direction,
  critiquing interface designs, generating wireframes or mockups, or needing design
  guidance for dashboards, SaaS, or product interfaces. Triggers on: design system,
  design tokens, UI design, interface design, dashboard design, wireframe, mockup,
  design critique, visual direction, typography system, color palette, spacing scale.
disable-model-invocation: true
---
```

**Why `disable-model-invocation: true`:** This skill has extensive side effects:
- Creates/modifies files in `.design-intelligence/`
- Generates token JSON files
- Creates wireframe and mockup HTML files
- Modifies configuration

Users must explicitly invoke via `/design-init` or conversationally. Claude will not auto-trigger this skill.

### SKILL.md Content Structure (~400 lines)

The main SKILL.md contains:

1. **Core Philosophy** (50 lines) — the 5 principles, design partner model
2. **Workflow Overview** (30 lines) — Discover → Define → Design → Document → Audit
3. **Context Gathering Gate** (40 lines) — mandatory questions before any design work
4. **Domain Exploration Framework** (50 lines) — vocabulary, colors, signature, rejections
5. **Direction Selection** (40 lines) — preset descriptions, blending rules
6. **Anti-Slop Rules** (30 lines) — summary of rejections, strictness behavior
7. **Memory System** (30 lines) — what files exist, when to read/write
8. **Reference Loading Instructions** (50 lines) — when to load each reference doc
9. **Command Overview** (50 lines) — brief list, detail in command files
10. **Error Recovery** (30 lines) — common failure modes, fallbacks

**All detailed content goes in `references/`:**
- Laws of UX details → `references/foundations/laws-of-ux.md`
- Full anti-pattern list → `references/foundations/anti-patterns.md`
- Typography rules → `references/domains/typography.md`
- Easing curves and timing → `references/domains/motion.md`
- etc.

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
│   ├── evals/
│   │   └── evals.json                    # Trigger test cases
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

### Evals

```json
[
  {
    "name": "natural-design-request",
    "prompt": "Help me design a dashboard for tracking sales metrics",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Asks about target audience before proposing design",
      "Explores domain vocabulary",
      "Does not immediately generate code"
    ]
  },
  {
    "name": "token-system-request",
    "prompt": "I need a color palette and typography scale for my app",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Asks about brand feel or direction",
      "Proposes design direction before tokens"
    ]
  },
  {
    "name": "critique-request",
    "prompt": "Can you critique this UI design?",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Runs swap test, squint test, signature test",
      "Provides ranked issues"
    ]
  },
  {
    "name": "wireframe-request",
    "prompt": "Create a wireframe for a settings page",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Checks for existing design system",
      "Asks clarifying questions if no system exists"
    ]
  }
]
```

### Hooks

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup",
        "hooks": [
          {
            "type": "command",
            "command": "test -f .design-intelligence/system.md && echo 'Design system found' || echo 'No design system'",
            "timeout": 2,
            "statusMessage": "Checking for design system..."
          }
        ]
      }
    ]
  }
}
```

### Command File Template

Each command follows this structure:

```yaml
---
command: design-init
description: Initialize a new design system with domain exploration and direction selection
disable-model-invocation: true
---

# /design-init

Initialize a new design system for this project.

## Prerequisites

Check if `.design-intelligence/` already exists:
- If yes: warn user, confirm before overwriting
- If no: proceed with initialization

## Workflow

1. **Context Gathering**
   Read `references/foundations/design-directions.md` for exploration framework.

   Ask the user:
   - Who is the primary user? (role, context, expertise)
   - What must they accomplish? (core task, verb)
   - How should this feel? (sensory language, not "clean and modern")

2. **Domain Exploration**
   Guide user through:
   - 5+ domain vocabulary concepts
   - 5+ naturally occurring colors
   - 1 signature element unique to this product
   - 3 default choices being rejected (and why)

3. **Direction Selection**
   Present 6 presets with recommendation based on exploration.
   Allow blending or custom direction.

4. **Token Foundation**
   Invoke `token-architect` agent to generate initial tokens.
   Save to `.design-intelligence/tokens/`.

5. **Save System**
   Create `.design-intelligence/system.md` with direction and principles.
   Create `.design-intelligence/config.json` with defaults.

## Output

- `.design-intelligence/` directory structure created
- Initial tokens generated
- System documented and ready for use
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

## Marketplace Entry

Add to `.claude-plugin/marketplace.json`:

```json
{
  "name": "design-intelligence",
  "description": "Intelligent design partner for UI systems. Handles domain exploration, design direction, token generation, wireframes, mockups, and critique. Produces framework-agnostic specs and documentation.",
  "version": "2026.3.22.0001",
  "author": {
    "name": "Prakhar Bhardwaj",
    "url": "https://github.com/prakhar625"
  },
  "source": "./plugins/design-intelligence",
  "category": "design",
  "tags": [
    "design-system",
    "design-tokens",
    "ui-design",
    "wireframes",
    "mockups",
    "accessibility",
    "typography",
    "color-system",
    "spacing",
    "motion-design",
    "design-critique"
  ]
}
```

---

## External Dependencies

This plugin has **no external dependencies**. All outputs are generated through:

- **Tokens:** JSON files written directly
- **Wireframes/Mockups:** HTML files with inline CSS, viewable in any browser
- **Documentation:** Markdown files
- **Analysis:** Claude's built-in capabilities (no external APIs)

For `/design-reference` with URLs:
- Uses Claude Code's `WebFetch` tool (built-in)
- Image analysis uses Claude's vision capabilities (built-in)

---

## Out of Scope

- Visual documentation of existing codebases (use `visual-documentation` plugin)
- Marketing/landing page design (different concerns than product UI)
- Actual implementation — this plugin produces specs and tokens, not production code
- Brand identity creation (logos, brand guidelines) — product UI only

---

## Open Questions (To Resolve During Implementation)

1. **Framework detection:** How precisely should we detect React vs Vue vs Svelte? Current plan: scan `package.json` for framework dependencies. Fallback: ask user.

2. **Wireframe vs mockup distinction from visual-documentation:** This plugin's wireframes are *design artifacts* (part of the design process, informed by tokens and direction). Visual-documentation's wireframes are *documentation artifacts* (illustrating existing UI). Different purpose, similar output format.

3. **Sound module integration point:** Currently documented as optional. During implementation, decide if it needs a dedicated command or just reference doc access.
