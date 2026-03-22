# Critique Framework Reference

## Goal
Evaluate design effectiveness through structured tests.

## The Three Tests

### 1. Swap Test

**Question:** If you swapped the typeface, would anyone notice?

**Process:**
1. Replace display font with generic alternative
2. Does the design lose character?
3. If indistinguishable → type choice not contributing

**What it reveals:**
- Whether typography is intentional
- If font choices support the direction
- Opportunity for more distinctive type

### 2. Squint Test

**Question:** When you squint, does hierarchy persist?

**Process:**
1. Blur your vision (or blur the design)
2. Can you still identify primary, secondary, tertiary elements?
3. Is the eye drawn to the right place?

**What it reveals:**
- Visual hierarchy effectiveness
- Contrast and weight distribution
- Layout clarity at a glance

### 3. Signature Test

**Question:** Can you locate 5+ distinctive elements?

**Process:**
1. List elements that are unique to this design
2. Would these elements identify this product blindfolded?
3. If you can't find 5 → too generic

**Examples of signature elements:**
- Unique color combination
- Distinctive component shape
- Characteristic spacing rhythm
- Custom iconography style
- Specific animation signature

## Critique Output Format

```markdown
## Critique: [Component/View Name]

### Swap Test
- **Result:** Pass / Fail
- **Finding:** [What was learned]
- **Recommendation:** [If fail, what to change]

### Squint Test
- **Result:** Pass / Fail
- **Finding:** [What was learned]
- **Recommendation:** [If fail, what to change]

### Signature Test
- **Result:** Pass / Fail
- **Distinctive Elements Found:**
  1. [Element 1]
  2. [Element 2]
  ...
- **Recommendation:** [If <5, what to add]

### Overall Assessment
[Summary paragraph]

### Priority Fixes
1. [Highest impact fix]
2. [Second priority]
3. [Third priority]
```

## When to Critique

- After initial wireframes (quick pass)
- Before mockup refinement (full pass)
- Before handoff (final verification)
- When something feels "off" but unclear why

## Validation Gates

- [ ] All three tests conducted
- [ ] Issues documented with specifics
- [ ] Recommendations are actionable
- [ ] Priority clearly assigned
