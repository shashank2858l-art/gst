# DEBUG.md Template

> Template for `.gsd/debug/[slug].md` — active debug session tracking.

```markdown
---
status: gathering | investigating | fixing | verifying | resolved
trigger: "[verbatim user input]"
created: [ISO timestamp]
updated: [ISO timestamp]
attempts: 0
---

## Current Focus
<!-- OVERWRITE on each update - always reflects NOW -->

hypothesis: [current theory being tested]
test: [how testing it]
expecting: [what result means if true/false]
next_action: [immediate next step]

## Symptoms
<!-- Written during gathering, then immutable -->

expected: [what should happen]
actual: [what actually happens]
errors: [error messages if any]
reproduction: [how to trigger]

## Eliminated
<!-- APPEND only - prevents re-investigating -->

- hypothesis: [theory that was wrong]
  evidence: [what disproved it]
  timestamp: [when eliminated]

## Evidence
<!-- APPEND only - facts discovered -->

- timestamp: [when found]
  checked: [what was examined]
  found: [what was observed]
  implication: [what this means]

## Resolution
<!-- OVERWRITE as understanding evolves -->

root_cause: [empty until found]
fix: [empty until applied]
verification: [empty until verified]
files_changed: []
```

## 3-Strike Rule

After `attempts: 3`:
1. **STOP** — No more fixes in this session
2. **Document** everything in the debug file
3. **State dump** to STATE.md
4. **Fresh session** recommended

## Resume Behavior

When AI reads this file after session reset:
1. Parse frontmatter → know status and attempt count
2. Read Current Focus → know exactly what was happening
3. Read Eliminated → know what NOT to retry
4. Read Evidence → know what's been learned
5. Continue from next_action
