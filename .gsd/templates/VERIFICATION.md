# VERIFICATION.md Template

> Copy this template when creating verification reports.

```markdown
---
phase: {N}
verified_at: {YYYY-MM-DD HH:MM}
verdict: PASS | FAIL | PARTIAL
pass_count: {X}
total_count: {Y}
---

# Phase {N} Verification Report

## Summary

**{X}/{Y}** must-haves verified
**Verdict:** {PASS | FAIL | PARTIAL}

## Must-Haves

### ✅ 1. {Must-have description}
**Status:** PASS
**Method:** {How this was verified}
**Evidence:**
```
{Actual command output or screenshot reference}
```

### ❌ 2. {Must-have description}
**Status:** FAIL
**Method:** {How this was verified}
**Expected:** {What should happen}
**Actual:** {What actually happened}
**Evidence:**
```
{Actual command output}
```
**Gap:** {What needs to be fixed}

### ⏭️ 3. {Must-have description}
**Status:** SKIPPED
**Reason:** {Why this couldn't be verified}

## Gap Closure Required

1. **{Gap 1}:** {Description + how to fix}
2. **{Gap 2}:** {Description + how to fix}

## Next Steps

- If PASS: Proceed to next phase
- If FAIL: Fix gaps then re-verify
- If PARTIAL: Address gaps then re-verify
```

## Evidence Types

| Verification | Evidence Required |
|--------------|-------------------|
| API endpoint | curl command + response |
| UI behavior | Screenshot |
| Test suite | Test output |
| File exists | `ls` or `dir` output |
| Build passes | Build command output |
| Integration | End-to-end trace |
