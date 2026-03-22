# Design Intelligence

**An intelligent design partner for UI systems — domain exploration, design tokens, wireframes, mockups, and critique.**

Create cohesive, accessible design systems with persistent memory. The plugin guides you through context discovery, direction selection, token generation, and quality audits. Every decision is documented and traceable.

---

## What This Does

An intelligent partner that helps you build design systems from first principles. Instead of jumping to mockups, the plugin starts with understanding your audience and their world, then grows a coherent design system that feels intentional, not generic.

**Six design presets guide the aesthetic direction:**

| Preset | Feel | Best For |
|--------|------|----------|
| **Precision** | Sharp, dense, efficient | Data products, developer tools, dashboards |
| **Warmth** | Friendly, approachable, human | Consumer apps, education, community platforms |
| **Sophistication** | Premium, trustworthy, refined | Financial services, luxury, enterprise |
| **Boldness** | Confident, clear, assertive | Media, sports, startups with strong identity |
| **Utility** | Functional, honest, tools-first | SaaS, productivity, minimalist design |
| **Delight** | Playful, expressive, memorable | Games, animation, creative tools |

You can also blend presets (e.g., "Warmth + Boldness") or define a custom direction.

---

## Installation

### Plugin (Recommended)

In Claude Code:

```
/plugin marketplace add prakhar625/my-plugins
/plugin install my-plugins@design-intelligence
```

Restart Claude Code after installing.

### Manual

```bash
git clone https://github.com/prakhar625/my-plugins.git
cp -r my-plugins/plugins/design-intelligence ~/.claude/plugins/
```

Then enable it in Claude Code with `/plugin`.

---

## Quick Start

### First Time

1. Start with `/design-init` to initialize a new design system
2. Answer three questions: **Who?** (audience) **What?** (core task) **How?** (feel)
3. Explore your domain: vocabulary, colors, and signature element
4. Pick or blend a design preset
5. Get your first set of design tokens

### Subsequent Sessions

The plugin remembers your design system at `.design-intelligence/` in your project.

- View your current direction: `/design-direction`
- Check your tokens: `/design-tokens`
- Continue designing with `/design-wireframe`, `/design-mockup`, etc.
- Audit quality: `/design-audit`

---

## Commands (19 total)

### Core System

| Command | Description |
|---------|-------------|
| `/design-init` | Initialize a new design system (context gathering, domain exploration, token generation) |
| `/design-direction [preset-name]` | View or change design direction (precision, warmth, sophistication, boldness, utility, delight) |
| `/design-context` | Update audience, use cases, or feel without full reinitialization |
| `/design-tokens [token-type]` | View, edit, or regenerate tokens (colors, typography, spacing, motion, shadows, radii) |
| `/design-config [setting]` | Configure strictness, accessibility level, educational mode, sound design |

### Design & Creation

| Command | Description |
|---------|-------------|
| `/design-components [component-name]` | Define or view component specs with states and token mappings |
| `/design-extract` | Extract design inspiration and vocabulary from reference products |
| `/design-reference` | Analyze competitor or reference designs for patterns and ideas |
| `/design-wireframe [view-name]` | Generate lo-fi wireframe using established tokens |
| `/design-mockup [view-name]` | Create high-fidelity mockup with tokens, colors, and typography |
| `/design-refine [element]` | Refine specific design decisions or components |
| `/design-animate` | Define motion specs and animation patterns |

### Quality & Documentation

| Command | Description |
|---------|-------------|
| `/design-audit [path]` | Comprehensive audit: anti-slop, consistency, accessibility (AA) |
| `/design-audit-aaa [path]` | AAA-level accessibility audit (WCAG AAA compliance) |
| `/design-critique` | Get critical feedback from the design-critic agent (swap test, squint test, signature test) |
| `/design-polish` | Final refinements before handoff (typography, spacing, micro-interactions) |
| `/design-document` | Generate comprehensive design system documentation |
| `/design-handoff [format]` | Prepare implementation-ready specs (markdown, json, figma, css) |

### System Management

| Command | Description |
|---------|-------------|
| `/design-history` | View decision history and system evolution |

---

## The Design Presets

### Precision
**Sharp, dense, efficient** — for technical and data-heavy interfaces.

Best for dashboards, developer tools, analytics platforms, and productivity software. High information density, clear hierarchy, minimal decoration.

**Characteristics:** Monospace typography, tight spacing, muted accent colors, system UI patterns

---

### Warmth
**Friendly, approachable, human** — for consumer-facing experiences.

Best for education, community, consumer apps, and wellness. Conversational tone, generous spacing, warm color palettes, hand-drawn or organic elements.

**Characteristics:** Rounded corners, natural colors, generous whitespace, expressive illustrations

---

### Sophistication
**Premium, trustworthy, refined** — for enterprise and high-end brands.

Best for financial services, luxury products, healthcare, and B2B enterprise. Classic proportions, restrained color use, premium typography, subtle animations.

**Characteristics:** Serif typography, high contrast, elegant spacing, minimal ornamentation

---

### Boldness
**Confident, clear, assertive** — for brands with strong identity.

Best for media, sports, startups, and creative industries. High contrast, vibrant colors, strong typography, dynamic layouts.

**Characteristics:** All-caps headings, saturated colors, bold weight typography, dramatic spacing

---

### Utility
**Functional, honest, tools-first** — for minimalist, no-nonsense design.

Best for SaaS, productivity software, and developer tools. Clear visual hierarchy, limited color palette, efficient layouts, no decoration without purpose.

**Characteristics:** Grid-based layouts, limited colors (3-4 main), functional typography, consistent iconography

---

### Delight
**Playful, expressive, memorable** — for experiences that engage emotions.

Best for games, creative tools, entertainment, and animation-forward products. Colorful palettes, playful animations, expressive typography, personality-driven design.

**Characteristics:** Variable fonts, bright colors, smooth animations, unique illustrations

---

## Memory System: `.design-intelligence/`

All design decisions live here, organized for discovery and reuse:

```
.design-intelligence/
├── system.md                          # Core definition: direction, principles, audience
├── config.json                        # Settings: strictness, accessibility, sound module
│
├── foundations/
│   ├── audience.md                    # Who uses this? What are they doing?
│   ├── principles.md                  # Design principles guiding all decisions
│   ├── direction.md                   # Selected preset(s) and rationale
│   └── domain.md                      # Domain vocabulary, colors, signature element
│
├── tokens/
│   ├── colors.json                    # Color tokens (hues, shades, semantic meanings)
│   ├── typography.json                # Type scale, font families, weights
│   ├── spacing.json                   # Spacing scale (4px base)
│   ├── motion.json                    # Animation timings, easing functions
│   ├── shadows.json                   # Shadow depths and blur radii
│   └── radii.json                     # Border radius scale
│
├── components/
│   ├── button.md                      # Component spec: states, token mappings, variants
│   ├── input.md
│   ├── card.md
│   └── [component-name].md            # One file per component
│
├── wireframes/
│   └── [view-name].html               # Lo-fi wireframes (structure only)
│
├── mockups/
│   └── [view-name].html               # High-fidelity mockups (with tokens applied)
│
├── documentation/
│   ├── design-system.md               # Full system documentation
│   └── [custom-docs].md               # Additional reference docs
│
├── handoff/
│   ├── markdown/                      # Human-readable specs
│   ├── json/                          # Machine-readable tokens
│   ├── figma/                         # Figma variable import format
│   └── css/                           # CSS custom properties
│
└── history/
    └── decisions.log                  # Timestamped decision log
```

**Key files:**
- `system.md` — Your design system's identity. Start here to understand everything.
- `tokens/` — The single source of truth. Every color, spacing, and motion value should trace back to a token.
- `components/` — Component specifications with all visual states (default, hover, active, focus, disabled) and data states (loading, empty, error).
- `documentation/` — Ready-to-share design system documentation.

---

## Configuration Options

### Strictness (Anti-Slop Enforcement)

| Level | Behavior | Best For |
|-------|----------|----------|
| **strict** (default) | Actively rejects AI-typical patterns. Requires user confirmation to override. | Production quality, final output |
| **moderate** | Warns about patterns but allows them. Explains why they're problematic. | Learning and exploration |
| **relaxed** | Guidance only, no blocking. Educational notes in output. | Rapid prototyping |

Configure with: `/design-config strictness moderate`

**Anti-slop rules enforced (all levels):**
- No pure black (#000000) — use dark neutrals
- No gray text on colored backgrounds — insufficient contrast
- No card nesting >2 levels — visual hierarchy collapse
- No bounce easing — overused, unprofessional
- No overused glassmorphism — generic pattern
- No generic gradients without purpose

---

### Accessibility

| Level | Standard | Use Case |
|-------|----------|----------|
| **AA** (default) | WCAG AA — 4.5:1 text contrast | Most products |
| **AAA** | WCAG AAA — 7:1 text contrast | Healthcare, government, accessibility-first |

Configure with: `/design-config accessibility AAA`

The plugin validates:
- Text contrast ratios (colors tokens)
- Touch target sizes (spacing tokens)
- Focus states (motion tokens)
- Keyboard navigation (component specs)
- Motion for `prefers-reduced-motion`

---

### Other Settings

```
/design-config educationalMode true         # Explain the "why" behind decisions
/design-config soundModule true             # Enable sound design features
/design-config autoSaveDecisions true       # Log decisions automatically
/design-config confirmDestructive true      # Confirm before overwriting
```

---

## Usage Examples

### Example 1: Building a Design System from Scratch

```bash
# Start fresh
/design-init

# Answer three questions in the chat
# → Audience: "Researchers analyzing genomic data"
# → Task: "Filter, compare, and export sequences"
# → Feel: "Laboratory precision with quiet confidence"

# Explore your domain
# → Vocabulary: locus, allele, mutation, phenotype, diploid
# → Colors: lab whites, equipment grays, sample blues
# → Signature: Nested hierarchical tree for variant relationships

# Pick a direction
# → "Precision" preset recommended

# Get initial tokens
# → Colors, typography, spacing, motion generated

# Check your system
/design-tokens
/design-direction
```

### Example 2: Adding a New Component

```bash
# View existing components
/design-components

# Define a new component
/design-components "sequence-viewer"

# Answer guided questions about states:
# → Visual states (default, hover, active, focus, disabled)
# → Data states (loading, empty, error, no-results)
# → Token mappings (use tokens for all values)

# Component spec saved automatically
```

### Example 3: Creating Wireframes & Mockups

```bash
# Lo-fi wireframe (structure, layout, spacing only)
/design-wireframe "analysis-dashboard"

# High-fidelity mockup (with colors, typography, tokens)
/design-mockup "analysis-dashboard"

# Both use your tokens — no arbitrary values
```

### Example 4: Quality Assurance

```bash
# Full audit
/design-audit

# Get critical feedback from design-critic agent
/design-critique

# AAA accessibility audit
/design-audit-aaa

# Final refinements
/design-polish
```

### Example 5: Handoff

```bash
# Generate implementation-ready specs
/design-handoff markdown    # For documentation
/design-handoff css         # For developers
/design-handoff figma       # For design tools
/design-handoff json        # For code generation
```

---

## Workflow: The Six Phases

The plugin guides you through a structured design process:

### Phase 1: Context Gathering
- Who is the primary user? (role, context, expertise)
- What must they accomplish? (the core task/verb)
- How should this feel? (sensory language — NOT "clean and modern")

### Phase 2: Domain Exploration
- 5+ domain vocabulary concepts (words from their world)
- 5+ naturally occurring colors in this domain
- 1 signature element unique to this product
- 3 default choices being rejected (and why)

### Phase 3: Direction & Tokens
- Direction selected (preset, blend, or custom)
- Tokens generated and saved
- Design principles documented

### Phase 4: Design & Create
- Component specs with all interaction states
- Wireframes and mockups using tokens
- Motion specs with accessibility considerations

### Phase 5: Document & Handoff
- Design system documentation generated
- Implementation-ready specs prepared
- Handoff format ready for team

### Phase 6: Audit
- Anti-slop check (no generic patterns)
- Accessibility audit (AA or AAA)
- Consistency check (all values trace to tokens)
- Critique tests (swap, squint, signature)

---

## Requirements & Dependencies

No external API keys or dependencies required. All work is local, file-based, and framework-agnostic.

**Outputs:**
- Token files: JSON
- Wireframes & Mockups: HTML (no frameworks)
- Component specs: Markdown
- Handoff formats: Markdown, JSON, CSS, Figma variables

All HTML output is standalone — no CDN dependencies, no JavaScript frameworks.

---

## What's Inside

```
plugins/design-intelligence/
├── .claude-plugin/
│   └── plugin.json                    # Plugin metadata
│
├── commands/                          # 19 slash commands
│   ├── design-init.md
│   ├── design-direction.md
│   ├── design-context.md
│   ├── design-tokens.md
│   ├── design-config.md
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
│   └── design-history.md
│
├── agents/                            # Specialized agents
│   ├── design-critic.md               # Critical feedback using swap/squint/signature tests
│   ├── token-architect.md             # Token generation and validation
│   └── reference-analyst.md           # Competitor/reference analysis
│
├── skills/
│   └── design-intelligence/
│       ├── SKILL.md                   # Main skill (triggers on design-related prompts)
│       └── references/
│           ├── foundations/
│           │   ├── design-directions.md           # Preset explanations and exploration framework
│           │   └── anti-patterns.md               # AI-typical patterns to avoid
│           ├── domains/
│           │   ├── typography.md                  # Type scale guidance
│           │   ├── color.md                       # Color system design
│           │   ├── spacing.md                     # Spacing scale design
│           │   ├── motion.md                      # Animation patterns
│           │   └── interaction.md                 # Component state patterns
│           ├── quality/
│           │   ├── accessibility.md               # WCAG AA/AAA requirements
│           │   ├── audit-checklist.md             # Quality gates
│           │   └── critique-framework.md          # Evaluation tests
│           └── optional/
│               └── sound.md                       # Sound design integration
│
└── hooks/
    └── hooks.json                     # SessionStart hook (checks for existing .design-intelligence/)
```

---

## Tips & Gotchas

### Common Mistakes to Avoid

1. **Skipping context gathering** — Always ask the three questions first. You cannot infer context from the codebase.
2. **Accepting vague language** — "Clean and modern" → Ask for sensory language. "Approachable" → How? Warm colors? Rounded corners?
3. **Generating tokens before direction** — Direction informs token choices. Get it right first.
4. **Ignoring existing system** — The plugin checks for `.design-intelligence/` on session start. Don't delete it!
5. **Orphaned values** — Every color, spacing, motion value must trace to a token. Use `/design-audit` to find orphans.
6. **Over-prescribing** — Present options; don't dictate. Let users make informed decisions.

### When the Plugin Rejects Your Design

The plugin enforces anti-slop rules by default. If it rejects something:

1. **Read the explanation** — It will tell you why
2. **Consider the feedback** — It's usually right
3. **Adjust strictness if needed** — `/design-config strictness moderate` for exploration
4. **Or fix the design** — That's often better

If you find yourself frequently overriding anti-slop checks, it might be time to reconsider the direction or token choices.

### Design Presets Are Starting Points

Mix and match presets to create custom directions:

```
/design-direction warmth+boldness      # Friendly and confident
/design-direction sophistication        # Pure preset
/design-direction custom               # Define your own
```

### Tokens Trace Everything

Every visual decision should trace back to a token:

```
❌ "The button uses color #0066FF"
✓ "The button uses primary-action (token: colors.primary-action = #0066FF)"
```

Use `/design-audit` to find violations.

---

## Error Recovery

| Problem | Solution |
|---------|----------|
| User can't articulate "feel" | Offer reference products: "Does it feel more like Linear or Notion?" |
| Domain exploration stalls | Use `/design-reference` to analyze competitor designs |
| Token generation conflicts | Present trade-offs; let user decide which values to keep |
| Anti-slop rejection frustrates | Explain why; adjust strictness if in exploration phase |
| User wants to skip context | Explain why context matters; offer abbreviated version |
| Design system lost | Check `.design-intelligence/` — it should still exist. Copy from backup if needed. |

---

## Exporting & Sharing Your Design System

Once your design system is mature, use `/design-handoff` to prepare it for teams:

```bash
# Generate all formats
/design-handoff markdown              # Share with non-designers
/design-handoff json                  # For code generation tools
/design-handoff css                   # For frontend developers
/design-handoff figma                 # For design tools
```

All output is framework-agnostic, so your tokens work with React, Vue, Svelte, native iOS, Android, or anywhere else.

---

## License

MIT — See [LICENSE](../LICENSE)
