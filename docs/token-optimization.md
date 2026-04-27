# Token Optimization Guide

> Practical strategies for minimizing credit usage while maintaining quality.

---

## Why This Matters

| Issue | Impact |
|-------|--------|
| Excessive file loading | Higher costs, slower responses |
| Context accumulation | Quality degradation after 50% |
| Re-reading files | Wasted credits on understood content |
| Full files when snippets suffice | 10x credit usage |

**Goal:** Maximum quality per credit spent.

---

## The 3-Step Read Protocol

Every file access MUST follow this:

```
Step 1: SEARCH — grep for the specific pattern
  → If found, note file:line
  → Cost: ~10 tokens

Step 2: EVALUATE — is a full read justified?
  → Usually NO. Snippet is enough.
  → Cost: 0 tokens

Step 3: TARGETED READ — read only needed lines
  → e.g., lines 45-80 instead of full 400-line file
  → Cost: ~140 tokens vs ~1600 tokens
  → Savings: ~90%
```

---

## File Size Strategy

| File Lines | Strategy |
|------------|----------|
| <50 | Read freely |
| 50-200 | Search + outline first |
| 200-500 | Search + snippets only |
| 500+ | NEVER read fully |

---

## Scan Budget

When scanning a user's project:

| Step | Method | Credit Cost |
|------|--------|-------------|
| Folder structure | `list_dir` | FREE |
| Tech detection | `grep` for package.json patterns | CHEAP (~20 tokens) |
| Route discovery | `grep` for route patterns | CHEAP (~20 tokens) |
| API call detection | `grep` for fetch/axios | CHEAP (~20 tokens) |
| DB/Auth patterns | `grep` for mongoose/jwt/etc | CHEAP (~20 tokens) |
| Entry point read | `view_file` lines 1-50 | MODERATE (~200 tokens) |
| Config read | `view_file` specific sections | MODERATE (~100 tokens) |
| **Total scan** | | **~400-800 tokens** |
| **vs reading everything** | | **~20,000-40,000 tokens** |

---

## Summarize After Understanding

After reading any file, create a mental summary:

```
auth.ts: Exports login(), logout(), validateToken(). Uses bcrypt + JWT. Express middleware.
```

Next time you need info about auth.ts → reference summary, don't reload.

---

## Output Optimization

| Rule | Savings |
|------|---------|
| Don't regenerate unchanged code | ~50% per task |
| Output only new/modified files | ~30% per task |
| Keep explanations under 3 sentences | ~20% per response |
| Never repeat context user knows | ~10% per response |
| Use code comments over prose | ~15% per response |

---

## Session Budget Thresholds

| Context Usage | Quality | Action |
|---------------|---------|--------|
| 0-30% | PEAK | Full quality work |
| 30-50% | GOOD | Normal operations |
| 50-70% | DEGRADING | Compress, use outlines |
| 70%+ | POOR | State dump → fresh session |

---

## Anti-Patterns

### ❌ The Context Dump
```
BAD:  "Let me read all files in src/"  → 50 files × 200 lines = 40,000 tokens
GOOD: "Search for 'router' in src/"   → 2 results, ~500 tokens
```

### ❌ The Just-In-Case Load
```
BAD:  "Loading utils.ts in case I need it"  → probably won't, wasted
GOOD: "Noting utils.ts exists, will load if needed"  → 0 tokens
```

### ❌ The Re-Read
```
BAD:  "Reading config.ts again to check the port"  → already read it
GOOD: "From earlier: port is 3001 in config.ts:15"  → 0 tokens
```

### ❌ The Full Rewrite
```
BAD:  "Here's the complete updated file"  → 200 lines output for 5-line change
GOOD: "Replace lines 45-49 with:"        → 5 lines output
```

---

*Every token saved is a credit preserved for the work that matters.*
