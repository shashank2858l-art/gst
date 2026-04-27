# PROJECT_SNAPSHOT.md Template

> **THE BRAIN FILE.** Generated once after first scan. Read THIS instead of re-scanning.
> Only regenerated when user runs `gst/scan` explicitly.

```markdown
---
generated: {YYYY-MM-DD HH:MM}
project_path: {absolute/path/to/project}
type: frontend | backend | fullstack
last_scanned: {YYYY-MM-DD HH:MM}
scan_version: 1
---

# Project Snapshot: {Project Name}

## Quick Identity
- **Type**: {frontend / backend / fullstack}
- **Framework**: {React / Express / Next.js / etc.}
- **Language**: {TypeScript / JavaScript / Python}
- **Database**: {MongoDB / PostgreSQL / none}
- **Auth**: {JWT / session / OAuth / none}
- **Package Manager**: {npm / yarn / pnpm / pip}
- **Entry Point**: {src/index.ts / app.js / main.py}

## Directory Map
```
{project-root}/
├── {dir1}/          # {purpose}
├── {dir2}/          # {purpose}
│   ├── {subdir}/    # {purpose}
│   └── {subdir}/    # {purpose}
└── {entry-point}    # {purpose}
```

## All Routes

### Frontend Pages
| Path | Component | File |
|------|-----------|------|
| / | Home | src/pages/Home.tsx |
| /login | Login | src/pages/Login.tsx |
| /dashboard | Dashboard | src/pages/Dashboard.tsx |

### Backend Endpoints
| Method | Path | Handler | Auth | File:Line |
|--------|------|---------|------|-----------|
| POST | /api/auth/login | loginHandler | no | routes/auth.js:12 |
| GET | /api/users | getUsers | yes | routes/users.js:8 |

## API Calls (Frontend → Backend)
| From File:Line | Method | URL |
|----------------|--------|-----|
| src/pages/Login.tsx:34 | POST | /api/auth/login |
| src/pages/Dashboard.tsx:15 | GET | /api/dashboard |
| src/components/Cart.tsx:22 | POST | /api/cart/add |

## Database Models
| Model | Key Fields | File |
|-------|-----------|------|
| User | id, email, password, role | models/User.js |
| Product | id, name, price, category | models/Product.js |

## Auth Summary
| Aspect | Value |
|--------|-------|
| Strategy | JWT |
| Storage | httpOnly cookie |
| Middleware | middleware/auth.js |
| Protected Routes | /api/users, /api/orders, /api/admin/* |

## Key Dependencies
| Package | Purpose |
|---------|---------|
| express | Web framework |
| mongoose | MongoDB ODM |
| jsonwebtoken | Auth tokens |
| bcrypt | Password hashing |

## Environment Variables
| Variable | Purpose | Example |
|----------|---------|---------|
| DATABASE_URL | DB connection | mongodb://localhost:27017/myapp |
| JWT_SECRET | Token signing | random-secret-key |
| PORT | Server port | 3001 |
| VITE_API_URL | Frontend API base | http://localhost:3001/api |

## File Index (Key Files Only)
| Purpose | File Path | Lines |
|---------|-----------|-------|
| Server entry | server.js | 45 |
| Router config | routes/index.js | 30 |
| Auth middleware | middleware/auth.js | 25 |
| DB connection | config/db.js | 18 |
| API client | src/api/client.ts | 22 |
| App entry | src/App.tsx | 35 |

## Notes
- {Any warnings, anomalies, or important observations}
- {Integration points that need attention}
```

## Rules

### When to CREATE this file:
- First time user runs `gst/start` with an existing project (options 1, 2, 3, 5)
- When user explicitly runs `gst/scan`

### When to READ this file (instead of re-scanning):
- **EVERY subsequent prompt** — read `.gsd/PROJECT_SNAPSHOT.md` instead of scanning folders
- Before planning any changes
- Before executing any task
- Before debugging any issue

### When to UPDATE this file:
- After creating new files/routes/endpoints during EXECUTE phase
- After integration changes
- When user runs `gst/scan` to force a re-scan

### When to RE-GENERATE (full re-scan):
- ONLY when user explicitly runs `gst/scan`
- NEVER automatically on subsequent prompts

## Update Protocol

After each EXECUTE wave, append changes:
```markdown
## Changes Log
| Date | Change | Files |
|------|--------|-------|
| 2024-01-15 | Added /api/orders endpoint | routes/orders.js |
| 2024-01-15 | Added Order model | models/Order.js |
```

This keeps the snapshot current without re-scanning.
