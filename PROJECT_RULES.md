# PROJECT_RULES.md — GSD Canonical Rules

> **Single Source of Truth** for the Get Shit Done methodology.
> Optimized for Antigravity. Credit-conscious. Model-agnostic.

---

## Core Protocol

**SPEC → PLAN → EXECUTE → VERIFY → COMMIT**

1. **SPEC**: Define requirements in `.gsd/SPEC.md` until status is `FINALIZED`
2. **PLAN**: Decompose into phases (1, 2, 3) and sub-phases (1.1, 1.2) with folders in `.gsd/phases/`
3. **EXECUTE**: Implement sub-phase by sub-phase. NEVER skip or combine sub-phases.
4. **VERIFY**: Prove completion of each sub-phase with empirical evidence in phase folders.
5. **COMMIT**: One sub-phase = atomic commits, format: `type(phase-X.Y): description`

**Planning Lock**: No implementation code until SPEC.md contains "Status: FINALIZED".

---

## Search-First Discipline

**Before reading any file completely:**

1. **Search first** — Use grep/ripgrep to find relevant snippets
2. **Evaluate snippets** — Determine if full read is justified
3. **Targeted reads** — Only read specific line ranges when needed

**Anti-pattern**: Reading entire files "to understand the context" without searching first.

---

## Snapshot Discipline — Scan Once, Never Again

**The most important credit-saving rule in GSD.**

### The Rule:
```
Before ANY work on a project:
  1. Check: Does .gsd/PROJECT_SNAPSHOT.md exist?
  2. YES → Read ONLY that file. You know everything. Skip scanning.
  3. NO  → Run the SCAN workflow. Generate PROJECT_SNAPSHOT.md. Then proceed.
```

### What is PROJECT_SNAPSHOT.md?
A single file that contains EVERYTHING about the project:
- Type, framework, language, database, auth
- Directory structure
- All routes (frontend + backend)
- All API calls (frontend → backend)
- All database models
- All environment variables
- Key file index
- Changes log (updated incrementally)

### When to create:
- First scan of any project (automatic)
- When user runs `gst/scan` (explicit re-scan)

### When to read (instead of scanning):
- **Every. Single. Prompt.** after the first scan
- Before planning, executing, debugging, or any other work

### When to update (WITHOUT re-scanning):
- After each EXECUTE wave — append new files/routes/endpoints to Changes Log
- After integration changes

### When to re-generate (full re-scan):
- **ONLY** when user explicitly runs `gst/scan`
- **NEVER** automatically

**Template:** `.gsd/templates/PROJECT_SNAPSHOT.md`

---

## Smart Scanning Rules

When scanning a user's project folder:

### Detection Priority (cheapest first)
1. `list_dir` — folder structure (FREE, always do first)
2. `grep` for package.json/requirements.txt — tech stack (CHEAP)
3. `grep` for route patterns — URL structure (CHEAP)
4. `grep` for API call patterns — integration points (CHEAP)
5. `grep` for DB/auth patterns — infrastructure (CHEAP)
6. Targeted file reads — only entry points and configs (EXPENSIVE, limit to 10)

### Pattern Libraries

**Frontend Detection:**
```
React:     "react", "jsx", "useState", "useEffect", "createRoot"
Next.js:   "next", "getServerSideProps", "pages/", "app/"
Vue:       "vue", "createApp", "<template>", ".vue"
Angular:   "@angular", "NgModule", "@Component"
Svelte:    "svelte", ".svelte"
```

**Backend Detection:**
```
Express:   "express()", "app.listen", "router."
FastAPI:   "FastAPI()", "@app.get", "uvicorn"
Django:    "django", "urlpatterns", "views.py"
NestJS:    "@Controller", "@Injectable", "NestFactory"
Go:        "http.HandleFunc", "gin.", "chi."
```

**API Endpoint Patterns:**
```
REST:      app.get(, app.post(, app.put(, app.delete(, router.
GraphQL:   "typeDefs", "resolvers", "gql`"
tRPC:      "t.router", "t.procedure"
```

**Database Patterns:**
```
Mongoose:  "mongoose.model(", "new Schema("
Prisma:    "prisma.", "@prisma/client"
Sequelize: "sequelize.define(", "Model.init("
TypeORM:   "@Entity(", "@Column("
SQL raw:   "CREATE TABLE", "SELECT ", "INSERT INTO"
```

---

## Integration Matching Rules

When connecting frontend ↔ backend:

### Matching Algorithm
1. Extract all frontend fetch/axios URLs
2. Extract all backend registered routes
3. Normalize both (strip prefixes like `/api/v1/` → `/`)
4. Match by: URL path + HTTP method
5. Confidence levels:
   - **EXACT** (99%): URL + method match perfectly
   - **HIGH** (90%): URL matches, method inferred
   - **MEDIUM** (75%): Partial URL match (e.g., `/users` ↔ `/user`)
   - **LOW** (50%): Semantic match only (e.g., "login" keyword in both)

### Config Alignment
Check and align:
- `baseURL` / `NEXT_PUBLIC_API_URL` / `VITE_API_URL` → backend listen address
- CORS settings on backend match frontend origin
- Auth token format matches between frontend storage and backend validation

---

## Proof Requirements

Every change requires verification evidence:

| Change Type | Required Proof |
|-------------|----------------|
| API endpoint | curl/HTTP response |
| UI change | Screenshot or browser test |
| Build/compile | Command output |
| Test | Test runner output |
| Config | Verification command |
| Integration | End-to-end request trace |

**Never accept**: "It looks correct", "This should work"
**Always require**: Captured output, screenshot, or test result

---

## Wave Execution

Plans are grouped into **waves** based on dependencies:

| Wave | Characteristic | Execution |
|------|----------------|-----------|
| 1 | Foundation tasks, no dependencies | Can be parallel |
| 2 | Depends on Wave 1 | Wait for Wave 1 |
| 3 | Depends on Wave 2 | Wait for Wave 2 |

**Wave Completion Protocol:**
1. All tasks in wave verified
2. State snapshot created
3. Update STATE.md with position

---

## Credit Budget System

### Loading Rules
| Action | Rule |
|--------|------|
| Before reading file | Search first (grep) |
| File >200 lines | Use outline, not full file |
| File already understood | Reference summary, don't reload |
| >5 files needed at once | Stop, reconsider approach |

### Output Rules
| Action | Rule |
|--------|------|
| Unchanged code | NEVER regenerate |
| Explanations | Keep under 3 sentences unless asked |
| Context repeating | NEVER — user already knows |
| Full project generation | BANNED — small chunks only |

### Budget Thresholds
| Usage | Action Required |
|-------|-----------------|
| 0-50% | Proceed normally |
| 50-70% | Compress context, outline mode |
| 70%+ | State dump → recommend fresh session |

---

## Context Management

**Quality Thresholds:**
| Usage | Quality |
|-------|---------|
| 0-30% | **PEAK** — Comprehensive, thorough |
| 30-50% | **GOOD** — Solid, confident |
| 50-70% | **DEGRADING** — Efficiency mode |
| 70%+ | **POOR** — Rushed, incomplete |

**Hygiene Rules:**
- Keep plans under 50% context usage
- Fresh context for each plan execution
- After 3 debugging failures → state dump → fresh session
- STATE.md = memory across sessions

---

## Commit Conventions

**Format:** `type(scope): description`

| Type | Usage |
|------|-------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code restructure |
| `test` | Adding/updating tests |
| `chore` | Maintenance |

**Rules:** One task = one commit. Verify before commit.

---

## Quick Reference

```
Before coding     → SPEC.md must be FINALIZED
Before file read  → Search first, then targeted read
After each task   → Update STATE.md
After each wave   → State snapshot
After 3 failures  → State dump + fresh session
Before "Done"     → Empirical proof captured
```

---

*GSD Methodology — Optimized for Antigravity*
