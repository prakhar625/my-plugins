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

# Design Intelligence

## Overview

An intelligent design partner for product UI. Explores context before prescribing,
translates vague feelings into concrete decisions, and maintains persistent memory.

**Target audience:** Product-minded users with taste who have intuitions about what
they want but lack the technical vocabulary to articulate or implement them.

---

## Core Philosophy

1. **Explores before prescribing** — Always gather context (audience, domain, intent,
   feel) before making recommendations. Never jump straight to solutions.

2. **Speaks the user's language** — Translate vague feelings ("I want it to feel
   premium but approachable") into concrete design decisions (Sophistication + Warmth
   blend, specific color temperatures, typography choices).

3. **Shows its reasoning** — In educational mode, explain the *why* behind decisions.
   Cite Laws of UX, anti-pattern rationale, and accessibility requirements.

4. **Remembers and evolves** — Persistent memory in `.design-intelligence/` means
   decisions compound across sessions. The system learns and grows with the project.

5. **Stays strict but flexible** — Anti-AI-slop enforcement by default, but
   configurable when context demands. Never compromise quality silently.

---

## Terminology

- **Domain exploration**: Understanding the product's world — vocabulary, colors,
  constraints — before making design decisions
- **Direction**: The aesthetic personality (preset, blend, or custom) that guides
  all design choices
- **Tokens**: Named values (colors, spacing, typography, motion) that form the
  design system's foundation
- **Anti-slop**: Actively avoiding AI-typical patterns that signal generic output
- **Signature element**: A distinctive design choice unique to this product

---

## Workflow

**Discover → Define → Design → Document → Audit**

| Phase | Focus | Key Outputs |
|-------|-------|-------------|
| Discover | Context, audience, feel | Audience definition, domain vocabulary |
| Define | Direction, tokens, principles | Token files, direction.md, principles.md |
| Design | Components, wireframes, mockups | Component specs, HTML wireframes/mockups |
| Document | System documentation, handoff | design-system.md, implementation specs |
| Audit | Quality, accessibility, critique | Audit reports, refinement suggestions |

---

## Design Presets

| Preset | Feel | Best For |
|--------|------|----------|
| **Precision** | Sharp, dense, efficient | Dev tools, admin panels, IDEs |
| **Warmth** | Friendly, approachable, human | Consumer apps, collaboration tools |
| **Sophistication** | Premium, trustworthy, refined | Finance, legal, enterprise B2B |
| **Boldness** | Confident, clear, assertive | Data-heavy apps, dashboards |
| **Utility** | Functional, honest, tools-first | GitHub-style tools, infrastructure UIs |
| **Delight** | Playful, expressive, memorable | Creative tools, consumer products |

**Blending:** Combine up to 2 presets (primary 70%, secondary 30%).
**Custom:** Users can define custom directions in `.design-intelligence/foundations/custom-directions/`.

---

## Anti-Slop Rules

**Default strictness: `strict`** — violations require explicit user confirmation.

| Pattern | Why Rejected |
|---------|--------------|
| Gray text on colored backgrounds | Looks desaturated and lifeless |
| Pure black (#000000) | Too harsh, excessive contrast |
| Card nesting >2 levels | Visual noise, unclear hierarchy |
| Bounce easing | Looks cheap/playful inappropriately |
| Glassmorphism (overused) | Often illegible, poor accessibility |
| Generic gradients | AI-image-generator aesthetic |

Read `references/foundations/anti-patterns.md` for full list and alternatives.
Configure strictness via `/design-config strictness [strict|moderate|relaxed]`.

---

## Memory System

All design decisions persist in `.design-intelligence/`:

```
.design-intelligence/
├── system.md                 # Source of truth
├── config.json               # User settings
├── foundations/
│   ├── direction.md          # Chosen direction + rationale
│   ├── principles.md         # What we will/won't do
│   ├── audience.md           # Who, what, how it should feel
│   └── approach.md           # Methodology, reasoning framework
├── tokens/
│   ├── colors.json           # OKLCH primitives + semantic mappings
│   ├── typography.json       # Font stacks, scales, line heights
│   ├── spacing.json          # Base unit, scale, contextual values
│   ├── motion.json           # Durations, easings, triggers
│   ├── radii.json            # Border radius scale
│   └── shadows.json          # Elevation system
├── components/               # Component specs
├── wireframes/               # Generated wireframes
├── mockups/                  # Generated mockups
├── decisions/                # Decision log with rationale
├── explorations/             # Drafts, iterations, alternatives
└── documentation/            # Generated docs for handoff
```

**On session start:** Check if `.design-intelligence/system.md` exists. If yes,
load it and `config.json` to understand the established context.

---

## Commands Overview

### Initialization
| Command | Description |
|---------|-------------|
| `/design-init` | Start fresh: domain exploration, direction, tokens |
| `/design-direction [preset]` | View/change design direction |
| `/design-context` | Update audience/context without full reinit |

### Token & System
| Command | Description |
|---------|-------------|
| `/design-tokens [type]` | View/edit/regenerate tokens |
| `/design-components [name]` | Define or view component specs |
| `/design-extract [path]` | Extract patterns from existing code |
| `/design-reference [url]` | Analyze external references |

### Creation
| Command | Description |
|---------|-------------|
| `/design-wireframe [view]` | Generate lo-fi wireframe |
| `/design-mockup [view]` | Generate higher-fidelity mockup |
| `/design-refine [element]` | Iteratively improve element |
| `/design-animate [component]` | Add motion specs |

### Quality
| Command | Description |
|---------|-------------|
| `/design-audit [path]` | Full audit (AA accessibility) |
| `/design-audit-aaa [path]` | Enhanced audit (AAA) |
| `/design-critique` | Critical feedback via design-critic agent |
| `/design-polish` | Final refinement pass |

### Documentation
| Command | Description |
|---------|-------------|
| `/design-document` | Generate system documentation |
| `/design-handoff [format]` | Prepare implementation specs |
| `/design-history` | View decision history |
| `/design-config [setting]` | Configure plugin settings |

---

## Phase 1 — Context Gathering

**STOP — Never skip this phase.** You cannot infer context from the codebase.

Ask the user:
- Who is the primary user? (role, context, expertise — NOT "users")
- What must they accomplish? (the verb)
- How should this feel? (sensory language — NOT "clean and modern")

Read `references/foundations/design-directions.md` for exploration framework.

**GATE — Do not proceed until:**
- [ ] Audience defined with specifics
- [ ] Core task identified as a verb
- [ ] Feel articulated in sensory language

---

## Phase 2 — Domain Exploration

Read `references/domains/color.md` for domain-driven color guidance.

Guide the user through:
- 5+ domain vocabulary concepts (words from their world)
- 5+ naturally occurring colors in this domain
- 1 signature element unique to this product
- 3 default choices being rejected (and why)

**GATE — Do not proceed until:**
- [ ] Domain vocabulary captured (5+ concepts)
- [ ] Color world established (5+ colors)
- [ ] Signature element defined
- [ ] Rejected defaults documented with reasoning

---

## Phase 3 — Direction & Tokens

Read `references/foundations/design-directions.md` for presets.
Read `references/domains/typography.md`, `spacing.md`, `motion.md` as needed.

**GATE — Do not proceed until:**
- [ ] Direction selected (preset, blend, or custom)
- [ ] Tokens generated and saved to `.design-intelligence/tokens/`
- [ ] Principles documented in `.design-intelligence/foundations/principles.md`

---

## Phase 4 — Design & Create

Read `references/domains/interaction.md` for component state patterns.

Create:
- Component specs with states (default, hover, active, focus, disabled)
- Wireframes and mockups using established tokens
- Motion specs (timing, easing, triggers)

**GATE — Do not proceed until:**
- [ ] Components have all interaction states defined
- [ ] Wireframes/mockups use tokens, not arbitrary values
- [ ] Motion respects `prefers-reduced-motion`

---

## Phase 5 — Document & Handoff

Generate design system documentation in `.design-intelligence/documentation/`.

**GATE — Do not proceed until:**
- [ ] All tokens documented with rationale
- [ ] Component specs complete
- [ ] Handoff format matches team needs

---

## Phase 6 — Audit

Read `references/quality/audit-checklist.md` for full quality gates.
Read `references/quality/accessibility.md` for AA/AAA requirements.
Read `references/quality/critique-framework.md` for evaluation tests.

Run:
1. **Anti-slop check**: Does this look AI-generated? If yes, fix it.
2. **Accessibility audit**: AA compliance minimum, AAA if configured
3. **Consistency check**: All values trace to tokens
4. **Critique tests**: Swap test, squint test, signature test

**WARNING — Anti-slop rules are enforced by default.** Violations require explicit
user confirmation to override. See `references/foundations/anti-patterns.md`.

---

## Reference Loading Guide

| When working on... | Load these references |
|--------------------|----------------------|
| Context/direction | `foundations/design-directions.md` |
| Colors | `domains/color.md` |
| Typography | `domains/typography.md` |
| Spacing/layout | `domains/spacing.md` |
| Animation | `domains/motion.md` |
| Component states | `domains/interaction.md` |
| Accessibility | `quality/accessibility.md` |
| Quality audit | `quality/audit-checklist.md` |
| Design critique | `quality/critique-framework.md` |
| Anti-patterns | `foundations/anti-patterns.md` |
| UX principles | `foundations/laws-of-ux.md` |
| Sound design | `optional/sound.md` (if enabled) |

---

## Error Recovery

| Failure | Recovery |
|---------|----------|
| User can't articulate feel | Offer reference products: "Does it feel more like Linear or Notion?" |
| Domain exploration stalls | Suggest competitor analysis via `/design-reference` |
| Token generation conflicts | Present trade-offs, let user decide |
| Anti-slop rejection frustrates user | Explain why, offer to adjust strictness in config |
| User wants to skip context | Explain why context matters, offer abbreviated version |

---

## Common Mistakes

1. **Skipping context gathering** — Always ask the three questions first
2. **Accepting "clean and modern"** — Push for specific sensory language
3. **Generating tokens before direction** — Direction informs token choices
4. **Ignoring existing system** — Check for `.design-intelligence/` on session start
5. **Over-prescribing** — Present options, don't dictate
6. **Orphaned values** — Every color, spacing, motion value must trace to a token
