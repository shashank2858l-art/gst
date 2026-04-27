# PLAN.md Template

> Copy this template when creating execution plans.

```markdown
---
phase: {N}
plan: {M}
wave: {W}
---

# Plan {N}.{M}: {Descriptive Name}

## Objective
{One paragraph — what this plan delivers and why}

## Context
Load these files for context:
- .gsd/SPEC.md
- {relevant source files — ONLY what's needed}

## Tasks

<task type="auto" effort="medium">
  <name>{Clear, specific task name}</name>
  <files>
    {exact/file/path1.ext}
    {exact/file/path2.ext}
  </files>
  <action>
    {Specific implementation instructions}

    Steps:
    1. {Step 1}
    2. {Step 2}
    3. {Step 3}

    AVOID: {common mistake} because {reason}
    USE: {preferred approach} because {reason}
  </action>
  <verify>
    {Executable command or check}
    Example: npm test -- --testNamePattern="auth"
    Example: curl -X POST localhost:3000/api/login
  </verify>
  <done>
    {Measurable acceptance criteria}
    Example: Valid credentials → 200 + Set-Cookie, invalid → 401
  </done>
</task>

<task type="auto" effort="low">
  <name>{Task 2 name}</name>
  <files>{files}</files>
  <action>{instructions}</action>
  <verify>{command}</verify>
  <done>{criteria}</done>
</task>

## Must-Haves
After all tasks complete, verify:
- [ ] {Must-have 1}
- [ ] {Must-have 2}

## Success Criteria
- [ ] All tasks verified passing
- [ ] Must-haves confirmed
- [ ] No regressions
```

## Task Types

| Type | Use For |
|------|---------|
| `auto` | Everything AI can do independently |
| `checkpoint:human-verify` | Visual/functional verification |
| `checkpoint:decision` | Implementation choices |

## Wave Assignment

| Wave | Use For |
|------|---------|
| 1 | Foundation (types, schemas, utilities) |
| 2 | Core implementations |
| 3 | Integration and validation |

Plans in the same wave can run in parallel.
Later waves depend on earlier waves.
