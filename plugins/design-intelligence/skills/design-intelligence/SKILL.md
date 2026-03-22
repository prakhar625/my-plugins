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

## Terminology

- **Domain exploration**: Understanding the product's world — vocabulary, colors,
  constraints — before making design decisions
- **Direction**: The aesthetic personality (preset, blend, or custom) that guides
  all design choices
- **Tokens**: Named values (colors, spacing, typography, motion) that form the
  design system's foundation
- **Anti-slop**: Actively avoiding AI-typical patterns that signal generic output
- **Signature element**: A distinctive design choice unique to this product

## Workflow
Discover → Define → Design → Document → Audit

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

## Error Recovery

| Failure | Recovery |
|---------|----------|
| User can't articulate feel | Offer reference products: "Does it feel more like Linear or Notion?" |
| Domain exploration stalls | Suggest competitor analysis via `/design-reference` |
| Token generation conflicts | Present trade-offs, let user decide |
| Anti-slop rejection frustrates user | Explain why, offer to adjust strictness in config |
| User wants to skip context | Explain why context matters, offer abbreviated version |

## Common Mistakes

1. **Skipping context gathering** — Always ask the three questions first
2. **Accepting "clean and modern"** — Push for specific sensory language
3. **Generating tokens before direction** — Direction informs token choices
4. **Ignoring existing system** — Check for `.design-intelligence/` on session start
5. **Over-prescribing** — Present options, don't dictate
6. **Orphaned values** — Every color, spacing, motion value must trace to a token
