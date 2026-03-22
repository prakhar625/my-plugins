# Interaction Reference

## Goal
Define consistent component states and feedback patterns.

## Prerequisites
- [ ] Color tokens established (for state variations)
- [ ] Motion tokens established (for transitions)

## Component States

Every interactive element needs these states:

### Visual States
- **Default:** Resting state
- **Hover:** Mouse over (desktop)
- **Active:** Being pressed
- **Focus:** Keyboard navigation (visible ring)
- **Disabled:** Not interactive

### Data States
- **Loading:** Awaiting data
- **Empty:** No data to display
- **Error:** Something went wrong
- **Success:** Action completed

## State Styling Guidelines

### Hover
- Subtle background change (5-10% opacity shift)
- Slight scale (1.01-1.02) for cards
- Color tint toward primary

### Active
- Darker than hover
- Slight scale down (0.97-0.99) for buttons
- Immediate response (no delay)

### Focus
- Visible focus ring (2-3px)
- High contrast against background
- Never remove focus styles

### Disabled
- Reduced opacity (50-60%)
- Cursor: not-allowed
- Remove hover effects

## Feedback Patterns

### Immediate Feedback (0-100ms)
- Button color change
- Checkbox toggle
- Input focus

### Progress Feedback (100ms-2s)
- Loading spinners
- Progress bars
- Skeleton screens

### Completion Feedback
- Success checkmarks
- Confirmation messages
- Subtle animations

## Touch Targets

- **Minimum:** 44×44px (Apple HIG)
- **Recommended:** 48×48px
- **Spacing:** 8px between targets

## Form Patterns

### Input States
- Default: subtle border
- Focus: primary color border + ring
- Error: error color border + message
- Success: success indicator (optional)

### Validation Timing
- Validate on blur (not on every keystroke)
- Show errors after first interaction
- Clear errors when user starts fixing

## Validation Gates

- [ ] All interactive elements have all 5 states
- [ ] Focus states are visible and high-contrast
- [ ] Loading states for async operations
- [ ] Touch targets ≥44px

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Missing focus styles | Removed for aesthetics | Add visible focus ring |
| Incomplete states | Rush to ship | Define all 5 states before polish |
| Tiny tap targets | Desktop-first thinking | Increase to 44px minimum |
| No loading feedback | Async not considered | Add skeleton/spinner for >200ms |
