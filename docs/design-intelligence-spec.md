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

### SKILL.md Body Structure

```markdown
# Design Intelligence

## Overview
An intelligent design partner for product UI. Explores context before prescribing,
translates vague feelings into concrete decisions, and maintains persistent memory.

## Workflow
Discover → Define → Design → Document → Audit

## Phase 1 — Context Gathering

**GATE — Do not proceed until:**
- [ ] Audience defined (who is this human, not "users")
- [ ] Core task identified (the verb)
- [ ] Feel articulated (sensory language, not "clean and modern")

Read `references/foundations/design-directions.md` for exploration framework.

## Phase 2 — Domain Exploration

Guide through:
- 5+ domain vocabulary concepts
- 5+ naturally occurring colors
- 1 signature element unique to this product
- 3 default choices being rejected (and why)

**GATE — Do not proceed until:**
- [ ] Domain vocabulary captured
- [ ] Color world established
- [ ] Signature element defined
- [ ] Rejected defaults documented with reasoning

## Phase 3 — Direction & Tokens

Read `references/foundations/design-directions.md` for presets.
Read `references/domains/color.md`, `typography.md`, `spacing.md`, `motion.md` as needed.

**GATE — Do not proceed until:**
- [ ] Direction selected (preset, blend, or custom)
- [ ] Tokens generated and saved to `.design-intelligence/tokens/`
- [ ] Principles documented in `.design-intelligence/foundations/principles.md`

[... remaining phases ...]

## Error Recovery

| Failure | Recovery |
|---------|----------|
| User can't articulate feel | Offer reference products: "Does it feel more like Linear or Notion?" |
| Domain exploration stalls | Suggest competitor analysis via `/design-reference` |
| Token generation conflicts | Present trade-offs, let user decide |
| Anti-slop rejection frustrates user | Explain why, offer to adjust strictness in config |

## Common Mistakes

1. **Skipping context gathering** — Always ask the three questions first
2. **Accepting "clean and modern"** — Push for specific sensory language
3. **Generating tokens before direction** — Direction informs token choices
4. **Ignoring existing system** — Check for `.design-intelligence/` on session start
5. **Over-prescribing** — Present options, don't dictate
```

### Reference File Structure

Each reference document follows this structure:

```markdown
# [Topic] Reference

## Goal
One sentence: what this reference helps accomplish.

## Prerequisites
- [ ] Design direction established
- [ ] Relevant context gathered

## Content

### [Subsection 1]
Detailed guidance with examples.

### [Subsection 2]
More guidance...

## Validation Gates

**Before applying [topic]:**
- [ ] Check 1
- [ ] Check 2

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| ... | ... | ... |
```

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
      "Does not immediately generate code",
      "Offers design direction options"
    ]
  },
  {
    "name": "token-system-request",
    "prompt": "I need a color palette and typography scale for my app",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Asks about brand feel or direction",
      "Proposes design direction before tokens",
      "Uses OKLCH for color definitions",
      "Generates semantic mappings, not just primitives"
    ]
  },
  {
    "name": "critique-request",
    "prompt": "Can you critique this UI design?",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Runs swap test, squint test, signature test",
      "Provides ranked issues (critical/major/minor)",
      "Offers specific fixes for each issue",
      "Acknowledges strengths, not just problems"
    ]
  },
  {
    "name": "wireframe-request",
    "prompt": "Create a wireframe for a settings page",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Checks for existing design system",
      "Asks clarifying questions if no system exists",
      "Applies established tokens if system exists"
    ]
  },
  {
    "name": "vague-feel-request",
    "prompt": "I want something that feels premium but approachable",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Translates vague language into concrete direction",
      "Suggests Sophistication + Warmth blend",
      "Asks follow-up questions to refine"
    ]
  },
  {
    "name": "reference-capture-request",
    "prompt": "I really like how Linear looks, can we use that as inspiration?",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Offers to analyze Linear via /design-reference",
      "Extracts principles, not direct copies",
      "Connects insights to user's domain"
    ]
  },
  {
    "name": "anti-slop-enforcement",
    "prompt": "Add some glassmorphism and a gradient background",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Warns about anti-slop patterns",
      "Explains why these patterns are problematic",
      "Offers to adjust strictness if user insists",
      "Requires explicit confirmation to override"
    ]
  },
  {
    "name": "existing-system-continuation",
    "prompt": "Let's add a new component to our design system",
    "expected_trigger": "design-intelligence",
    "expected_behaviors": [
      "Checks for .design-intelligence/ directory",
      "Loads existing system.md and tokens",
      "Ensures new component follows established patterns"
    ]
  },
  {
    "name": "negative-test-unrelated",
    "prompt": "Refactor the database connection pool",
    "expected_trigger": null,
    "expected_behaviors": [
      "Does NOT load design-intelligence skill",
      "Handles as normal coding task"
    ]
  },
  {
    "name": "negative-test-visual-docs",
    "prompt": "Create an architecture diagram of our codebase",
    "expected_trigger": null,
    "expected_behaviors": [
      "Does NOT load design-intelligence skill",
      "Should trigger visual-documentation instead"
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
├── system.md                    # Core design system definition (source of truth)
├── config.json                  # User configuration
│
├── foundations/
│   ├── direction.md             # Chosen direction + rationale
│   ├── principles.md            # What we will/won't do
│   ├── audience.md              # Who, what, how it should feel
│   ├── approach.md              # Thought process, methodology, reasoning approach
│   └── custom-directions/       # User-defined direction presets
│       └── [name].yaml
│
├── tokens/
│   ├── colors.json              # Primitives + semantic mappings
│   ├── typography.json          # Font stacks, scales, line heights, tracking
│   ├── spacing.json             # Base unit, scale, contextual values
│   ├── motion.json              # Durations, easings (cubic-bezier), triggers, a11y
│   ├── radii.json               # Border radius scale
│   └── shadows.json             # Elevation system, layered shadows
│
├── components/                  # Component specs (buttons, inputs, cards, etc.)
├── patterns/                    # Navigation, data-display, feedback, forms
│
├── references/                  # Extracted from /design-reference
│   └── [source-name].md         # Analysis of external references
│
├── explorations/                # Intermediates: drafts, iterations, alternatives
│   └── [date]-[topic].md        # Exploration before final decision
│
├── wireframes/                  # Generated wireframe HTML/SVG files
├── mockups/                     # Generated mockup HTML files
│
├── decisions/                   # Decision log with rationale
│   └── [date]-[topic].md        # Why we chose X over Y
│
├── documentation/               # Generated design system docs
│   └── design-system.md         # Full documentation for handoff
│
└── history/
    └── changelog.md             # Evolution over time, version history
```

### Explorations (Intermediates)

`explorations/` captures drafts, alternatives, and iterations before final decisions:

```markdown
# explorations/2026-03-22-color-direction.md

## Context
Exploring color direction for healthcare analytics dashboard.

## Options Explored

### Option A: Clinical Blue
- Primary: oklch(55% 0.15 250)
- Pros: Trustworthy, professional, healthcare-associated
- Cons: Cold, sterile, overused in healthcare

### Option B: Warm Teal
- Primary: oklch(62% 0.12 195)
- Pros: Trust + warmth, distinctive, calming
- Cons: Less conventional for healthcare

### Option C: Sage Green
- Primary: oklch(58% 0.08 150)
- Pros: Natural, calming, growth-oriented
- Cons: May feel too casual for analytics

## Decision
Chose Option B (Warm Teal). See `decisions/2026-03-22-color-direction.md` for rationale.

## Artifacts
- [color-exploration-a.html](../wireframes/explorations/color-a.html)
- [color-exploration-b.html](../wireframes/explorations/color-b.html)
```

### Approach Document

`foundations/approach.md` captures the thought process and methodology:

```markdown
# Design Approach

## Methodology
How we approach design decisions for this project.

## Reasoning Framework
- Primary consideration: [e.g., "User efficiency over visual polish"]
- Secondary consideration: [e.g., "Accessibility always, delight when possible"]
- Tie-breaker: [e.g., "When in doubt, choose clarity"]

## Influences
- Domain: [e.g., "Healthcare analytics — trust and precision matter"]
- References: [e.g., "Linear's density, Stripe's clarity, Notion's warmth"]
- Constraints: [e.g., "Must work on low-bandwidth connections"]

## Evolution Notes
- 2026-03-22: Started with Sophistication preset, added Utility influences
- 2026-03-25: Shifted from blue to teal after domain exploration revealed...
```

### Motion Tokens Detail

`motion.json` captures:

```json
{
  "durations": {
    "instant": "0ms",
    "fast": "150ms",
    "normal": "250ms",
    "slow": "400ms",
    "deliberate": "600ms"
  },
  "easings": {
    "default": "cubic-bezier(0.23, 1, 0.32, 1)",
    "enter": "cubic-bezier(0.21, 1.02, 0.73, 1)",
    "exit": "cubic-bezier(0.06, 0.71, 0.55, 1)",
    "inOut": "cubic-bezier(0.77, 0, 0.175, 1)",
    "spring": "cubic-bezier(0.175, 0.885, 0.32, 1.275)"
  },
  "reducedMotion": {
    "respectPreference": true,
    "fallback": "opacity-only"
  },
  "patterns": {
    "buttonPress": { "duration": "fast", "easing": "default", "transform": "scale(0.97)" },
    "popoverEnter": { "duration": "normal", "easing": "enter", "transform": "scale(0.95) → scale(1)" },
    "toastSlide": { "duration": "normal", "easing": "enter", "transform": "translateY(100%) → translateY(0)" }
  }
}
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

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-init` | — | Start fresh: domain exploration, direction selection, token foundation |
| `/design-direction` | `[preset-name]` | View/change design direction (preset, custom, or blend) |
| `/design-context` | — | Update audience, use cases, or brand context without full reinit |

### Token & System Management

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-tokens` | `[token-type]` | View, edit, or regenerate token system (colors, typography, spacing, motion) |
| `/design-components` | `[component-name]` | Define or view component specs |
| `/design-extract` | `[path]` | Extract design patterns from existing code into the system |
| `/design-reference` | `[url-or-path]` | Capture inspiration from external sources: URLs, images, products |

### Creation & Refinement

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-wireframe` | `[view-name]` | Generate lo-fi wireframe for a view/component |
| `/design-mockup` | `[view-name]` | Generate higher-fidelity mockup with tokens applied |
| `/design-refine` | `[element]` | Iteratively improve a specific element or view |
| `/design-animate` | `[component]` | Add/define motion specs for components or transitions |

### Quality & Critique

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-audit` | `[path]` | Full audit: anti-slop, consistency, accessibility (AA) |
| `/design-audit-aaa` | `[path]` | Advanced accessibility audit (WCAG AAA) |
| `/design-critique` | — | Get critical feedback on current design decisions |
| `/design-polish` | — | Final pass: micro-refinements, edge cases, delight details |

### Documentation & Handoff

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-document` | — | Generate/update design system documentation |
| `/design-handoff` | `[format]` | Prepare implementation-ready specs (format: figma, markdown, json) |
| `/design-history` | — | View decision history and evolution |

### Configuration

| Command | Argument Hint | Description |
|---------|---------------|-------------|
| `/design-config` | `[setting]` | Configure strictness, a11y level, educational mode, sound module |

### Command File Template (with argument-hint)

```yaml
---
command: design-reference
argument-hint: "[url-or-path]"
description: Capture inspiration from external sources: URLs, images, products
disable-model-invocation: true
---

# /design-reference [url-or-path]

Analyze an external reference and extract design patterns.

## Arguments
- `$0` — URL to a website, path to an image, or product name

## Workflow
1. Invoke `reference-analyst` agent with the provided URL/path
2. Save analysis to `.design-intelligence/references/[source-name].md`
3. Summarize key insights to user
4. Offer to incorporate insights into direction

## Examples
- `/design-reference https://linear.app`
- `/design-reference ./inspiration/competitor.png`
- `/design-reference "Stripe dashboard"`
```

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
- Users can define custom directions in `.design-intelligence/foundations/custom-directions/[name].yaml`
- Custom directions can inherit from presets via `based_on` field
- Custom directions can be referenced by name in `/design-direction` or conversationally

### Custom Direction Template

```yaml
# .design-intelligence/foundations/custom-directions/my-brand.yaml
name: my-brand-direction
tagline: "Clinical precision meets human warmth"
based_on: [precision, warmth]  # Optional: inherit from presets

overrides:
  color:
    temperature: neutral
    primary: "oklch(65% 0.15 220)"
  typography:
    display: "Söhne"
    body: "Inter"
  motion:
    speed: fast
    easing: "cubic-bezier(0.23, 1, 0.32, 1)"

principles:
  - "Data density without overwhelm"
  - "Warmth in copy, precision in layout"
  - "Motion only on user-initiated actions"

anti-patterns:
  - "Decorative illustrations"
  - "Rounded buttons"
  - "Bounce easing"
```

---

## Sub-Agents

### Agent File Structure

Each agent follows this structure:

```markdown
---
name: agent-name
description: Brief description of agent purpose
---

# Agent Name

## Role
You are a [role description]. Your purpose is [specific purpose].

## Inputs
- **Required:** [what the agent receives]
- **Optional:** [additional context]

## Process
1. [Step 1]
2. [Step 2]
3. [Step 3]

## Output Format
[Specific format the agent returns]

## Guidelines
- [Guideline 1]
- [Guideline 2]
```

### design-critic.md

```markdown
---
name: design-critic
description: Provides critical design feedback using swap, squint, and signature tests
---

# Design Critic

## Role
You are a demanding design critic. Your purpose is to identify weaknesses
in design decisions before they ship. Be direct, specific, and constructive.

## Inputs
- **Required:** Design artifacts to critique (system.md, tokens, components, mockups)
- **Optional:** Specific areas of concern

## Process
1. **Swap Test:** Would swapping the typeface or layout template affect perception?
2. **Squint Test:** Does hierarchy persist when blurred?
3. **Signature Test:** Can you locate 5+ elements carrying the design's signature?

## Output Format
### Critical Issues (must fix)
- [Issue]: [Why it matters] → [Specific fix]

### Major Issues (should fix)
- [Issue]: [Why it matters] → [Specific fix]

### Minor Issues (nice to fix)
- [Issue]: [Why it matters] → [Specific fix]

### Strengths
- [What's working well]

## Guidelines
- Never say "looks good" without evidence
- Every issue must have a specific fix
- Acknowledge what's working, not just problems
- Rank by impact on user experience
```

### token-architect.md

```markdown
---
name: token-architect
description: Generates and refines design token systems from direction and domain
---

# Token Architect

## Role
You are a systematic design token architect. Your purpose is to derive
coherent token systems from design direction and domain exploration.

## Inputs
- **Required:** Design direction (from `.design-intelligence/foundations/direction.md`)
- **Optional:** Domain exploration, reference analysis, existing tokens

## Process
1. Read direction and understand the feel
2. Derive color primitives using OKLCH
3. Build semantic color mappings
4. Establish typography scale
5. Define spacing system from base unit
6. Create motion tokens (durations, easings)
7. Add shadows and radii

## Output Format
JSON files with inline comments explaining choices:
- `colors.json`
- `typography.json`
- `spacing.json`
- `motion.json`
- `shadows.json`
- `radii.json`

## Guidelines
- Every token must trace back to a primitive
- Explain WHY in comments, not just WHAT
- Check accessibility (contrast ratios) during color generation
- Use OKLCH for perceptual uniformity
```

### reference-analyst.md

```markdown
---
name: reference-analyst
description: Analyzes external references (URLs, images, products) for design patterns
---

# Reference Analyst

## Role
You are a design pattern analyst. Your purpose is to extract actionable
insights from external references without copying directly.

## Inputs
- **Required:** URL, image path, or product name
- **Optional:** Specific aspects to focus on

## Process
1. Fetch/analyze the reference
2. Identify color palette and usage patterns
3. Note typography choices (faces, scales, weights)
4. Analyze spacing rhythm and density
5. Observe motion/interaction patterns
6. Capture overall vibe and differentiators

## Output Format
Save to `.design-intelligence/references/[source-name].md`:

### [Source Name] Analysis

**Overall Vibe:** [1-2 sentence impression]

**Color Palette:**
- Primary: [color + usage]
- Secondary: [color + usage]
- Neutrals: [approach]

**Typography:**
- Display: [face, usage]
- Body: [face, usage]
- Scale: [observations]

**Spacing:**
- Density: [loose/medium/tight]
- Rhythm: [observations]

**Motion:**
- Speed: [fast/medium/deliberate]
- Character: [observations]

**Signature Elements:**
- [Unique element 1]
- [Unique element 2]

**Applicable Insights:**
- [How this applies to current project]

## Guidelines
- Extract principles, don't copy specifics
- Note what makes the reference distinctive
- Connect insights to the current project's domain
```

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
