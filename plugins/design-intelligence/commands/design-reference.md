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

## Examples
- `/design-reference https://linear.app`
- `/design-reference ./inspiration/competitor.png`
- `/design-reference "Stripe dashboard"`

## Workflow

### Step 1 — Fetch/Analyze
Invoke `reference-analyst` agent with the provided reference.

### Step 2 — Save Analysis
Save to `.design-intelligence/references/[source-name].md`

### Step 3 — Summarize
Present key insights to user:
- Overall vibe
- Color observations
- Typography patterns
- Spacing/density
- Motion character
- Signature elements

### Step 4 — Incorporate
Offer to apply insights to current direction:
- Adjust color palette
- Modify typography scale
- Update motion patterns
- Add to rejected defaults

**GATE — Do not modify system until:**
- [ ] User selects which insights to incorporate

## Output

- Analysis saved to references/
- Insights summarized
- System updated (if requested)
