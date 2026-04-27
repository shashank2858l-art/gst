# Scanning Guide

> How the GSD Smart Scanner identifies tech stacks, routes, and APIs without reading full files.

---

## Philosophy

**Never read what you can search. Never search what you can infer from structure.**

A well-structured project tells you 80% of what you need from:
1. Folder names alone
2. `package.json` / `requirements.txt` dependencies
3. Grep patterns on key terms

---

## Scan Pipeline

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐
│  Structure  │ →   │  Tech Stack  │ →   │   Routes     │
│  (list_dir) │     │ (grep deps)  │     │ (grep paths) │
│  FREE       │     │  CHEAP       │     │  CHEAP       │
└─────────────┘     └──────────────┘     └──────────────┘
                          ↓                      ↓
                    ┌──────────────┐     ┌──────────────┐
                    │  API Calls   │     │  DB & Auth   │
                    │ (grep fetch) │     │ (grep models)│
                    │  CHEAP       │     │  CHEAP       │
                    └──────────────┘     └──────────────┘
                                ↓
                    ┌──────────────────────┐
                    │  Targeted File Reads │
                    │  (≤10 files, ≤50 ln) │
                    │  EXPENSIVE           │
                    └──────────────────────┘
```

---

## Step 1: Structure Detection

Run `list_dir` on the project root and key subdirectories.

### Folder Name → Purpose Mapping

| Folder | Implies |
|--------|---------|
| `src/` | Source code root |
| `pages/` or `app/` | Next.js/Nuxt routing |
| `components/` | UI components (frontend) |
| `routes/` or `controllers/` | Backend routing |
| `models/` | Database models |
| `middleware/` | Backend middleware |
| `hooks/` | React custom hooks |
| `stores/` or `store/` | State management |
| `services/` or `api/` | API client layer |
| `utils/` or `lib/` | Utility functions |
| `public/` or `static/` | Static assets |
| `tests/` or `__tests__/` | Test files |
| `prisma/` | Prisma ORM |
| `migrations/` | Database migrations |

### Project Type Inference

| Structure | Type |
|-----------|------|
| Has `components/` + no `models/` | Frontend |
| Has `routes/` + `models/` + no `components/` | Backend |
| Has both `components/` and `routes/` | Full-stack |
| Has `pages/` + `api/` subfolder | Next.js full-stack |

---

## Step 2: Tech Stack Detection

### Package Managers

| File | Manager |
|------|---------|
| `package.json` + `package-lock.json` | npm |
| `package.json` + `yarn.lock` | Yarn |
| `package.json` + `pnpm-lock.yaml` | pnpm |
| `requirements.txt` | pip |
| `pyproject.toml` | Python (poetry/uv) |
| `go.mod` | Go |
| `Cargo.toml` | Rust |

### Grep Patterns for Dependencies

```bash
# Read only dependencies section of package.json
grep -A 50 '"dependencies"' package.json

# Frontend frameworks
grep '"react"\|"vue"\|"svelte"\|"@angular"\|"next"\|"nuxt"' package.json

# Backend frameworks
grep '"express"\|"fastify"\|"koa"\|"hapi"\|"nestjs"' package.json

# Databases
grep '"mongoose"\|"prisma"\|"sequelize"\|"typeorm"\|"pg"\|"mysql2"\|"better-sqlite3"' package.json

# Auth
grep '"jsonwebtoken"\|"bcrypt"\|"passport"\|"next-auth"\|"@auth/"' package.json
```

---

## Step 3: Route Discovery

### Frontend Route Patterns

```bash
# React Router
grep -rn 'path=\|<Route\|createBrowserRouter\|useNavigate' src/

# Next.js (file-based)
list_dir pages/  or  list_dir app/

# Vue Router
grep -rn 'path:\|component:\|createRouter' src/router/
```

### Backend Route Patterns

```bash
# Express
grep -rn 'app\.get(\|app\.post(\|app\.put(\|app\.delete(\|router\.' src/

# FastAPI
grep -rn '@app\.get(\|@app\.post(\|@app\.put(\|@app\.delete(' .

# NestJS
grep -rn '@Get(\|@Post(\|@Put(\|@Delete(\|@Controller(' src/

# Django
grep -rn 'path(\|url(\|urlpatterns' */urls.py
```

---

## Step 4: API Call Detection

```bash
# fetch calls
grep -rn "fetch(" src/ --include="*.ts" --include="*.tsx" --include="*.js" --include="*.jsx"

# axios calls
grep -rn "axios\.\|axiosInstance\." src/

# Custom API client
grep -rn "apiClient\.\|httpClient\.\|api\." src/services/ src/api/

# Base URL config
grep -rn "baseURL\|NEXT_PUBLIC_API\|VITE_API\|REACT_APP_API" .env* src/
```

---

## Step 5: Database & Auth Detection

```bash
# Database models
grep -rn "Schema(\|model(\|@Entity(\|Model\.init(" src/

# Auth middleware
grep -rn "jwt\|bcrypt\|passport\|isAuthenticated\|requireAuth" src/

# Environment secrets
grep -rn "DATABASE_URL\|MONGO_URI\|JWT_SECRET\|SESSION_SECRET" .env*
```

---

## Step 6: Targeted Reads

**Only after all grep steps**, read these files (first 50 lines max):

| Priority | File | Why |
|----------|------|-----|
| 1 | Main entry point (`index.ts`, `app.ts`, `server.ts`) | Understand app bootstrap |
| 2 | Router config | Understand URL structure |
| 3 | Database config | Understand connection |
| 4 | Auth middleware | Understand auth flow |
| 5 | API client (frontend) | Understand how calls are made |

**Hard limit: ≤10 file reads. ≤50 lines per read.**

---

## Output: SCAN_REPORT.md

Use the template in `.gsd/templates/SCAN_REPORT.md` to format results.

---

*Smart scanning is the foundation of credit-efficient development.*
