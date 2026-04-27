# SPEC.md Template

> Copy this template to `.gsd/SPEC.md` when starting a new project.

```markdown
---
status: DRAFT | FINALIZED
created: {YYYY-MM-DD}
updated: {YYYY-MM-DD}
---

# Project Specification

## Vision
{One paragraph describing what this project does and why it exists}

## Target Users
- {User type 1}: {what they need}
- {User type 2}: {what they need}

## Core Features
1. {Feature 1} — {brief description}
2. {Feature 2} — {brief description}
3. {Feature 3} — {brief description}
4. {Feature 4} — {brief description}
5. {Feature 5} — {brief description}

## User Roles & Permissions
| Role | Access Level | Can Do |
|------|-------------|--------|
| {role} | {level} | {permissions} |

## Functional Requirements

### {Feature 1}
- [ ] {Requirement 1.1}
- [ ] {Requirement 1.2}
- [ ] {Requirement 1.3}

### {Feature 2}
- [ ] {Requirement 2.1}
- [ ] {Requirement 2.2}

## Non-Functional Requirements
- **Performance**: {response time, throughput}
- **Security**: {auth method, data protection}
- **Scalability**: {expected load}
- **Accessibility**: {WCAG level, if applicable}

## Tech Stack

### Frontend
- Framework: {React/Next.js/Vue/etc.}
- Styling: {Tailwind/CSS Modules/etc.}
- State: {Redux/Zustand/Context/etc.}

### Backend
- Runtime: {Node.js/Python/Go/etc.}
- Framework: {Express/FastAPI/etc.}
- Database: {PostgreSQL/MongoDB/etc.}
- Auth: {JWT/Session/OAuth/etc.}

### Infrastructure
- Hosting: {Vercel/AWS/Railway/etc.}
- CI/CD: {GitHub Actions/etc.}

## API Design (High-Level)

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | /api/auth/login | User login |
| POST | /api/auth/register | User registration |
| GET | /api/{resource} | List resources |
| POST | /api/{resource} | Create resource |
| PUT | /api/{resource}/:id | Update resource |
| DELETE | /api/{resource}/:id | Delete resource |

## Database Schema (High-Level)

### {Collection/Table 1}
| Field | Type | Required | Notes |
|-------|------|----------|-------|
| {field} | {type} | {yes/no} | {notes} |

## Success Criteria
- [ ] {Criterion 1 — measurable}
- [ ] {Criterion 2 — measurable}
- [ ] {Criterion 3 — measurable}

## Constraints
- {Constraint 1}
- {Constraint 2}

## Out of Scope
- {What this project does NOT include}
```

## Status Flow

```
DRAFT → User reviews → FINALIZED → Planning can begin
```

**Planning Lock**: No implementation until status is FINALIZED.
