# Accessibility Reference

## Goal
Ensure designs meet WCAG accessibility standards.

## WCAG 2.1 Levels

### Level AA (Required Default)

**Visual:**
- Text contrast: 4.5:1 minimum (3:1 for large text ≥24px)
- UI component contrast: 3:1 against background
- No information conveyed by color alone
- Text resizable to 200% without loss of content

**Interactive:**
- Touch targets: 44×44px minimum
- Focus visible on all interactive elements
- Keyboard operable for all functionality
- No keyboard traps

**Content:**
- Labels on form inputs
- Error identification with suggestions
- Consistent navigation
- Page titles describe topic

### Level AAA (Enhanced Opt-in)

**Visual:**
- Text contrast: 7:1 minimum (4.5:1 for large text)
- No timing-dependent content
- No flashing content

**Interactive:**
- Touch targets: 48×48px recommended
- Multiple ways to locate content
- Context-sensitive help available

**Content:**
- Reading level appropriate for audience
- Abbreviations expanded
- Pronunciation guidance for unusual words

## Keyboard Navigation

### Focus Order
- Logical tab order (follows visual flow)
- Skip links for repeated content
- Focus trapped in modals until closed

### Focus Styles
```css
:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 2px;
}
```

Never remove focus styles. Make them visible and high-contrast.

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Semantic HTML

Use appropriate elements:
- `<button>` for actions, not `<div onclick>`
- `<a>` for navigation
- `<h1>`-`<h6>` in order, no skipping
- `<nav>`, `<main>`, `<aside>` for landmarks

## Validation Gates

- [ ] All text meets contrast requirements
- [ ] All interactive elements keyboard accessible
- [ ] Focus states visible
- [ ] Form inputs have labels
- [ ] Touch targets ≥44px
- [ ] prefers-reduced-motion respected
