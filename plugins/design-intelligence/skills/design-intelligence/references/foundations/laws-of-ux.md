# Laws of UX Reference

## Goal
Apply proven UX principles to design decisions.

## Prerequisites
- [ ] Context gathering complete (audience, task, feel)
- [ ] Design direction established

## Laws

### Fitts's Law
**Principle:** Time to reach a target depends on distance and size.
**Application:**
- Interactive elements minimum 32px (mobile: 44px)
- Primary actions should be larger and closer to likely cursor position
- Danger actions should be smaller and farther

### Hick's Law
**Principle:** Decision time increases logarithmically with choices.
**Application:**
- Limit primary options to 5-9 (Miller's Law)
- Use progressive disclosure for complex actions
- Group related options to reduce cognitive load

### Miller's Law
**Principle:** Working memory holds 5-9 chunks.
**Application:**
- Navigation items: 5-7 max
- Form sections: chunk into 3-5 fields
- Dashboard widgets: group into digestible sections

### Doherty Threshold
**Principle:** Productivity increases when response < 400ms.
**Application:**
- UI feedback must appear within 100ms
- Operations >400ms need progress indicators
- Optimistic updates for perceived speed

### Jakob's Law
**Principle:** Users expect your site to work like others they know.
**Application:**
- Follow platform conventions (close button top-right, etc.)
- Match mental models from competitor products
- Deviate only with clear benefit

### Law of Proximity
**Principle:** Objects near each other appear related.
**Application:**
- Group related form fields
- Use whitespace to separate sections
- Align labels with their inputs

## Validation Gates

**Before finalizing layouts:**
- [ ] Touch targets ≥32px (44px mobile)
- [ ] Primary navigation ≤7 items
- [ ] Loading states for operations >400ms
- [ ] Related elements visually grouped

## Common Failure Modes

| Failure | Cause | Fix |
|---------|-------|-----|
| Tiny tap targets | Mobile not considered | Increase to 44px minimum |
| Overwhelming navigation | Too many top-level options | Group into 5-7 categories |
| Perceived slowness | No loading feedback | Add progress indicators for >100ms |
| Confusing layout | Related items separated | Use proximity and grouping |
