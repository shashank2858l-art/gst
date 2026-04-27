# GSD Quick Reference Card

## Entry Point

```
gst/start  →  Choose your workflow (1-5)
```

## Workflow Lifecycle

```
┌───────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ gst/start │ →  │ gst/scan │ →  │ gst/plan │ →  │gst/execute│ → │gst/verify│
│           │    │          │    │          │    │          │    │          │
│  Choose   │    │  Analyze │    │  Create  │    │   Run    │    │  Check   │
│  workflow │    │ codebase │    │  phases  │    │  tasks   │    │  work    │
└───────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
                                                      ↑              │
                                                      └──────────────┘
                                                      (if gaps found)
```

## All Commands

| Command | Purpose |
|---------|---------|
| `gst/start` | Launch GSD — choose workflow |
| `gst/scan [path]` | Analyze a project folder |
| `gst/plan` | Create execution plans for current phase |
| `gst/execute` | Run plans with wave execution |
| `gst/verify` | Validate with empirical proof |
| `gst/debug [issue]` | Systematic debugging |
| `gst/status` | Show current progress |
| `gst/pause` | Save state, end session |
| `gst/resume` | Load state, continue work |

## Start Options

| # | Situation | What Happens |
|---|-----------|-------------|
| 1 | Have frontend, need backend | Scan frontend → generate backend spec |
| 2 | Have backend, need frontend | Scan backend → generate frontend spec |
| 3 | Have both separate | Scan both → create integration map |
| 4 | New project | Discovery questions → full spec |
| 5 | Existing project | Scan → extend/improve spec |

## Core Rules

| Rule | Enforcement |
|------|-------------|
| 🔒 Planning Lock | No code until SPEC finalized |
| 🔍 Search-First | Grep before reading files |
| 💰 Credit Budget | <10 file reads per scan |
| ✅ Proof Required | Evidence for every "done" |
| 🔄 3-Strike Debug | 3 failures → fresh session |

## Key Files

| File | Purpose |
|------|---------|
| `.gsd/SPEC.md` | Requirements (finalize first!) |
| `.gsd/ROADMAP.md` | Phase definitions |
| `.gsd/STATE.md` | Session memory |
| `.gsd/SCAN_REPORT.md` | Codebase analysis |
| `.gsd/INTEGRATION.md` | API mapping |

## Credit-Saving Tips

```
✅ Search, then read targeted lines
✅ Summarize after understanding
✅ Reference summaries, don't re-read
❌ Reading files "just in case"
❌ Regenerating unchanged code
❌ Long explanations
```
