# 🚀 GSD — Get Shit Done

> A **meta-prompting system** that transforms AI coding assistants into structured, credit-efficient full-stack development engines.

**Works with:** Antigravity (Gemini) · Claude Code · Any AI that reads project-level markdown instructions.

---

## ⚡ What Is GSD?

GSD solves **context rot** — the quality degradation AI assistants experience during long coding sessions. Instead of one messy conversation, GSD breaks projects into:

- **Atomic tasks** with clear acceptance criteria
- **Smart scanning** that reads only what's needed (saves ~97% tokens)
- **Structured phases** (SPEC → PLAN → EXECUTE → VERIFY → COMMIT)
- **Frontend ↔ Backend integration** with ~99% endpoint matching accuracy

---

## 📦 What's Inside

```
gst/
├── GEMINI.md                  # System prompt for Antigravity (auto-loaded)
├── CLAUDE.md                  # System prompt for Claude Code (auto-loaded)
├── PROJECT_RULES.md           # Canonical GSD rules
├── GSD-STYLE.md               # Style guide (tone, XML structure, UX patterns)
├── .gsd/
│   ├── templates/
│   │   ├── SPEC.md            # Project specification template
│   │   ├── PLAN.md            # Execution plan template (XML-structured tasks)
│   │   ├── SCAN_REPORT.md     # Smart folder scan report
│   │   ├── INTEGRATION.md     # Frontend ↔ Backend integration map
│   │   ├── VERIFICATION.md    # Pass/fail verification report
│   │   └── DEBUG.md           # Hypothesis-driven debug tracker
│   └── examples/
│       ├── quick-reference.md # Command cheat sheet
│       └── workflow-example.md# End-to-end walkthroughs
└── docs/
    ├── token-optimization.md  # Credit-saving strategies
    └── scanning-guide.md      # How smart scanning works
```

---

## 🏁 Quick Start

### Step 1: Clone into your project

```bash
git clone https://github.com/shashank2858l-art/gst.git
```

Or copy `GEMINI.md` / `CLAUDE.md` into your project root.

### Step 2: Open with your AI

- **Antigravity**: Open the folder → `GEMINI.md` auto-loads
- **Claude Code**: Open the folder → `CLAUDE.md` auto-loads

### Step 3: Type the magic command

```
gst/start
```

You'll see:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GSD ► WELCOME — Let's Get Shit Done
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What's your situation?

  1 → I have a FRONTEND — need to add a backend
  2 → I have a BACKEND — need to add a frontend
  3 → I have BOTH (separate) — link frontend ↔ backend
  4 → Build a NEW PROJECT from scratch
  5 → I have an EXISTING project — extend or improve it

───────────────────────────────────────────────────────
Reply with a number (1-5)
───────────────────────────────────────────────────────
```

Pick your option and GSD handles the rest.

---

## 🎯 The 5 Workflows

### 1️⃣ Frontend → Add Backend
You built the UI. GSD scans your frontend, detects every `fetch()` and `axios` call, and generates a complete backend spec with matching API endpoints, database models, and auth.

### 2️⃣ Backend → Add Frontend
You built the API. GSD scans your endpoints, models, and auth patterns, then helps you build a matching frontend.

### 3️⃣ Both → Integrate
You have separate frontend and backend. GSD scans both, maps every API call to its handler, identifies mismatches, and generates a connection plan:

```
✅ MATCH:   POST /api/auth/login  →  router.post('/auth/login')
⚠️ MISSING: GET /api/dashboard    →  No backend route found
ℹ️ UNUSED:  DELETE /api/admin/*   →  No frontend caller
```

### 4️⃣ New → Build from Scratch
GSD asks all discovery questions in ONE message (saves credits), generates a full SPEC, and guides you through phased implementation.

### 5️⃣ Existing → Extend
GSD scans your project, understands what exists, and creates a scoped spec for just the changes you want.

---

## 💰 Credit Optimization

GSD is designed to **minimize token/credit usage**:

| Traditional AI | GSD |
|---|---|
| Reads all files "to understand" | Searches first, reads only needed lines |
| ~40,000 tokens per scan | ~1,200 tokens per scan |
| Re-reads files it already understood | References summaries |
| Outputs entire files for small changes | Outputs only changed sections |
| Long explanations | 3-sentence max unless asked |

### The Search-First Rule

```
Step 1: grep for the pattern you need     → ~10 tokens
Step 2: Evaluate if full read is needed   → usually NO
Step 3: Read only the specific lines      → ~140 tokens

vs. Reading the full 400-line file        → ~1,600 tokens
Savings: ~90% per file access
```

---

## 📋 GSD Protocol

```
SPEC → PLAN → EXECUTE → VERIFY → COMMIT
```

| Phase | What Happens |
|-------|-------------|
| **SPEC** | Requirements defined in `.gsd/SPEC.md`. Must be FINALIZED before any code. |
| **PLAN** | Decomposed into atomic phases (1, 2, 3) and sub-phases (1.1, 1.2) with dedicated folders in `.gsd/phases/`. |
| **EXECUTE** | Sub-phases are executed in strict sequence. Verify EACH sub-phase before moving to the next. |
| **VERIFY** | Empirical proof required (logs, screenshots) stored in `.gsd/phases/{N}/VERIFICATION.md`. |
| **COMMIT** | One sub-phase = atomic commits. Format: `type(phase-X.Y): description`. |

---

## ⚡ All Commands

| Command | Purpose |
|---------|---------|
| `gst/start` | Launch GSD — choose workflow |
| `gst/scan [path]` | Scan a project folder |
| `gst/plan` | Create execution plans |
| `gst/execute` | Run current plans |
| `gst/verify` | Validate work |
| `gst/debug [issue]` | Systematic debugging |
| `gst/status` | Show current progress |
| `gst/pause` | Save state, end session |
| `gst/resume` | Load state, continue |

---

## 🔍 Smart Scanner

GSD never reads your entire codebase. It uses a 7-step pipeline:

1. **Structure Map** — `list_dir` on root and src/ (FREE)
2. **Tech Detection** — grep for package.json dependencies (CHEAP)
3. **Route Discovery** — grep for route patterns (CHEAP)
4. **API Call Detection** — grep for fetch/axios patterns (CHEAP)
5. **Database & Auth** — grep for mongoose/prisma/jwt/bcrypt (CHEAP)
6. **Targeted Reads** — only entry points and configs, ≤10 files, ≤50 lines each (MODERATE)
7. **Report** — generates `.gsd/SCAN_REPORT.md`

**Total cost: ~1,200 tokens** vs ~40,000 for reading everything.

---

## 🛡️ Safety Rules

- ❌ Never assumes requirements — asks when unclear
- ❌ Never auto-debugs without permission
- ❌ Never overwrites user code blindly — shows diff first
- ❌ Never generates entire project at once — small chunks only
- ✅ Always asks for folder paths
- ✅ Always presents plan before executing
- ✅ 3-strike debug rule — after 3 failures, dumps state and recommends fresh session

---

## 🤝 Supported AI Assistants

| AI | Instruction File | How It Loads |
|---|---|---|
| **Antigravity** (Gemini) | `GEMINI.md` | Auto-loaded from project root |
| **Claude Code** | `CLAUDE.md` | Auto-loaded from project root |
| **Cursor / Windsurf** | Copy contents into `.cursorrules` or system prompt | Manual |
| **Any other AI** | Copy contents into system prompt | Manual |

---

## 📄 License

MIT — Use it, fork it, make it yours.

---

**Built with 🔥 by [shashank2858l-art](https://github.com/shashank2858l-art)**
