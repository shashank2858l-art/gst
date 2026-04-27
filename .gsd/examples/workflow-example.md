# GSD Workflow Examples

> Real-world walkthroughs showing how GSD handles each scenario.

---

## Example 1: Frontend Exists → Add Backend

**Scenario:** User has a React frontend with login, dashboard, and product pages.

### Step 1: Start
```
User: gst/start
GSD: Shows options 1-5
User: 1
GSD: "Provide the absolute path to your frontend folder."
User: D:\projects\my-store-frontend
```

### Step 2: Smart Scan
```
GSD scans (credit-efficient):
  list_dir D:\projects\my-store-frontend        → finds src/, public/, package.json
  grep "react" package.json                      → React confirmed
  grep "fetch(\|axios" src/ --recursive          → finds 8 API calls
  grep "Route\|path:" src/ --recursive           → finds 6 routes
  reads package.json (lines 1-30)                → gets dependencies
  reads src/App.tsx (lines 1-40)                 → gets router structure

Total file reads: 2 (within budget)
```

### Step 3: Scan Report Generated
```markdown
Type: Frontend (React + TypeScript)
API Calls Found:
  POST /api/auth/login       → src/pages/Login.tsx:34
  POST /api/auth/register    → src/pages/Register.tsx:28
  GET  /api/products         → src/pages/Products.tsx:15
  GET  /api/products/:id     → src/pages/ProductDetail.tsx:12
  POST /api/cart/add          → src/components/AddToCart.tsx:8
  GET  /api/cart              → src/pages/Cart.tsx:10
  POST /api/orders            → src/pages/Checkout.tsx:45
  GET  /api/orders            → src/pages/Orders.tsx:18
```

### Step 4: Backend Spec
```
GSD generates SPEC.md with:
  - 8 API endpoints to create
  - User + Product + Cart + Order models
  - JWT auth (detected from frontend localStorage usage)
  - Express + MongoDB recommended
  
User reviews and FINALIZES.
```

### Step 5: Plan → Execute → Verify
```
Phase 1: Database + Auth (Wave 1)
Phase 2: Product + Cart endpoints (Wave 2)
Phase 3: Order endpoints + integration test (Wave 3)
```

---

## Example 2: Both Exist → Integrate

**Scenario:** User has a Vue frontend and a FastAPI backend built separately.

### Step 1: Start
```
User: gst/start
GSD: Shows options 1-5
User: 3
GSD: "Provide the absolute path to your frontend folder."
User: D:\projects\shop-frontend
GSD: "Provide the absolute path to your backend folder."
User: D:\projects\shop-api
```

### Step 2: Scan Both
```
Frontend scan: Vue 3, 12 API calls found
Backend scan: FastAPI, 15 endpoints found
```

### Step 3: Integration Analysis
```markdown
✅ Matched (10):
  POST /api/auth/login     ↔  @app.post("/auth/login")
  GET  /api/products       ↔  @app.get("/products")
  ...

⚠️ Missing Backend (2):
  GET /api/wishlist         →  No backend route
  POST /api/reviews         →  No backend route

ℹ️ Unused Backend (3):
  GET /api/admin/stats      →  No frontend caller (admin)
  DELETE /api/admin/user    →  No frontend caller (admin)
  GET /api/health           →  Health check (OK)

Config Issues:
  Frontend: VITE_API_URL=http://localhost:8000
  Backend: --port 8001  ← MISMATCH!
```

### Step 4: Fix Integration
```
GSD proposes:
  1. Fix port mismatch (backend → 8000)
  2. Create GET /api/wishlist endpoint
  3. Create POST /api/reviews endpoint
  4. Add CORS middleware for Vue dev server
  5. Align auth token format

User approves → EXECUTE
```

---

## Example 3: New Project from Scratch

### Step 1: Start
```
User: gst/start
User: 4
```

### Step 2: Discovery (ONE message)
```
GSD asks ALL questions at once:
  - What are you building?
  - Reference app?
  - Target users?
  - Top 5 features?
  - Tech preferences?
  - Constraints?

User answers in one response.
```

### Step 3: SPEC.md Generated
```
Status: DRAFT
Vision: A food delivery platform...
Features: Menu browsing, Cart, Orders, Driver tracking, Admin panel
Tech: Next.js + Express + PostgreSQL + JWT
```

### Step 4: User Reviews → FINALIZES → Plan → Execute

---

## Credit Cost Comparison

| Approach | File Reads | Estimated Tokens |
|----------|------------|------------------|
| Read everything | 50+ files | ~40,000 |
| GSD Smart Scan | 5-10 files | ~4,000 |
| **Savings** | **~80-90%** | **~36,000 tokens** |
