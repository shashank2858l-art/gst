# GSD-STYLE.md

> Style guide for consistent AI behavior within GSD workflows.
> Canonical rules in `PROJECT_RULES.md`. This file covers tone, structure, and UX patterns.

---

## Language & Tone

### Imperative Voice
- ✅ "Create the file"
- ❌ "You should create the file"
- ❌ "We will create the file"

### No Filler
- ✅ "Run `npm test`"
- ❌ "Now let's go ahead and run `npm test`"

### No Sycophancy
- ✅ "Phase complete."
- ❌ "Great job! Phase complete!"

### Brevity with Substance
Every sentence conveys information. Remove words that don't add meaning.

---

## XML Task Structure

```xml
<task type="auto" effort="medium">
  <name>Clear descriptive name</name>
  <files>exact/path/to/file.ts</files>
  <action>
    Specific implementation instructions.
    AVOID: common mistake (reason)
    USE: preferred approach (reason)
  </action>
  <verify>executable command that proves completion</verify>
  <done>measurable acceptance criteria</done>
</task>
```

### Effort Levels
| Value | Use Case |
|-------|----------|
| `low` | Simple edits, formatting |
| `medium` | Standard implementation (default) |
| `high` | Complex logic, refactoring |
| `max` | Architecture, security-critical |

### Task Types
| Type | Use For |
|------|---------|
| `auto` | Everything AI can do independently |
| `checkpoint:human-verify` | Visual/functional verification |
| `checkpoint:decision` | Implementation choices |

---

## UX Patterns

### Banners
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GSD ► STATUS MESSAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Next Steps
```
───────────────────────────────────────────────────────

▶ NEXT

/command — description

───────────────────────────────────────────────────────
```

### Decision Gates
```
⚠️ DECISION REQUIRED

Option A: {description}
Option B: {description}

Which do you prefer?
```

### Progress Indicator
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GSD ► Phase 2 · Wave 1 · Task 3/5
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Anti-Patterns (Banned)

### Vague Tasks
```xml
<!-- DON'T -->
<action>Implement authentication</action>

<!-- DO -->
<action>
  Create POST /api/auth/login endpoint.
  Accept {email, password} JSON body.
  Query User by email, compare with bcrypt.
  Return JWT in httpOnly cookie on success.
  Return 401 on failure.
</action>
```

### Temporal Language (in implementation docs)
- ❌ "First, we'll..."
- ❌ "Next, we should..."
- ❌ "Finally, we'll..."

### Enterprise Patterns (Banned)
- ❌ Stakeholder communication
- ❌ Team coordination
- ❌ Sprint ceremonies
- ❌ Multiple approval levels

---

## Response Format

Always structure responses as:
1. **Mode** — Current mode (SCAN / SPEC / PLAN / EXECUTE / VERIFY / DEBUG)
2. **Action** — What you're doing (1 sentence)
3. **Output** — Only the necessary output
4. **Next** — What happens next (ask user if needed)

---

*GSD Style Guide — Keep it clean, keep it fast.*
