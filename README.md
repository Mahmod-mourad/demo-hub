# Mahmoud Mourad — Project Demos

Open `index.html` for the full page with screenshots, or read the summary below.

Live at: https://mahmod-mourad.github.io/demo-hub/

---

## 1) NexMart — E-Commerce Platform

**What it solves:** a complete shop — catalogue with search, filters and pagination, cart and wishlist, Stripe checkout, order history and an admin dashboard. Payments settle through a server-side webhook; stock is reserved inside the order transaction to stop overselling. Arabic/English UI with RTL and a dark mode.

- Live: https://nexmart.vercel.app
- Code: https://github.com/Mahmod-mourad/e-commerce-platform-NexMart
- Stack: Next.js 14, TypeScript, Tailwind, Stripe, PostgreSQL/Prisma, JWT (HttpOnly), i18n RTL, Docker
- Screenshots: `screenshots/nexmart/` (home, products, product-detail, cart)

**How to Run:**
```bash
git clone https://github.com/Mahmod-mourad/e-commerce-platform-NexMart.git
cd e-commerce-platform-NexMart
docker compose up --build      # App: http://localhost:3000
```

---

## 2) Project Management System — Multi-tenant SaaS

**What it solves:** a task tracker for small teams where tenant isolation is enforced at the database level with Postgres row-level security. Task board, per-project statistics, real-time updates over Socket.IO, and 151 unit/integration/e2e tests.

- Live: https://pms-web-lilac.vercel.app
- Code: https://github.com/Mahmod-mourad/Project-management-system
- Stack: Next.js 14, NestJS, Supabase/PostgreSQL + RLS, Socket.IO, JWT + bcrypt, Swagger, Jest
- Screenshots: `screenshots/pms/` (login, dashboard, projects, tasks, users)

**How to Run:**
```bash
npx supabase start                                   # 1) Local database
psql "$DB_URL" -f scripts/01-tenants-and-plans.sql   # 2) Schema + seed (01 → 04 in order)
psql "$DB_URL" -f scripts/02-profiles-projects-tasks.sql
psql "$DB_URL" -f scripts/03-notifications.sql
psql "$DB_URL" -f scripts/04-seed-demo-data.sql

cd backend                                           # 3) Backend on 3001
SUPABASE_URL=http://127.0.0.1:54321 \
SUPABASE_SERVICE_ROLE_KEY=... npm run start:dev

NEXT_PUBLIC_API_URL=http://localhost:3001/api/v1 npm run dev   # 4) Frontend
```
**Demo login:** `admin@demo.localhost` / `DemoPassword123!` (member account: `member@demo.localhost`, same password).

---

## 3) Car Rental System

**What it solves:** an Arabic RTL car booking platform. Filters on transmission, fuel, seats and price; radius search around branches with PostGIS; bookings with payments and refunds; reviews with owner replies; admin fleet dashboard. One docker compose command runs the whole stack.

- Code: https://github.com/Mahmod-mourad/Car-Rental-System
- Stack: Next.js (RTL), NestJS, PostgreSQL + PostGIS, TypeORM, JWT, Swagger, Docker Compose
- Screenshots: `screenshots/car-rental/` (home, cars, car-detail, swagger)

**How to Run:**
```bash
git clone https://github.com/Mahmod-mourad/Car-Rental-System.git
cd Car-Rental-System
docker compose up --build
```
| Service | URL |
|---|---|
| Web | http://localhost:3000 |
| API | http://localhost:3001 |
| Swagger | http://localhost:3001/api |

---

## Notes for interviews

- **Every screenshot is real** — taken from the running apps with real data.
- **Live deployments:** NexMart and PMS are on Vercel. Car Rental runs locally with Docker (a good Docker story to tell).
- A story worth telling: in Car Rental I fixed a genuine bug where the similar-cars endpoint `/vehicles/similar/:id` returned 500 because of a raw SQL query with the wrong table name and unbound parameters. It's a real debugging story, not a rehearsed one.