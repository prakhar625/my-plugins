---
command: design-extract
argument-hint: "[path]"
description: Extract design patterns from existing code into the design system
disable-model-invocation: true
---

# /design-extract [path]

Extract design patterns from existing code.

## Arguments
- `$0` — Path to analyze (file, directory, or glob pattern)

## Prerequisites
- Design system should be initialized (will create if not)

## Workflow

### Step 1 — Analyze Code
1. Read files at specified path
2. Extract color values, spacing, typography, motion patterns
3. Identify component patterns

### Step 2 — Map to Tokens
1. Match extracted values to existing tokens
2. Identify orphaned values (not in system)
3. Suggest new tokens for common orphaned values

### Step 3 — Present Findings
```markdown
## Extraction Report

### Matched Values
- [value] → [token-name] (N occurrences)

### Orphaned Values
- [value] (N occurrences) — suggest: [token-name]

### Component Patterns
- [pattern-name]: [description]
```

**GATE — Do not modify tokens until:**
- [ ] User reviews findings
- [ ] User approves suggested additions

## Output

- Extraction report displayed
- Suggested tokens added (if approved)
- Refactoring suggestions provided
