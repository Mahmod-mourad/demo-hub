# معرض المشاريع — محمود مراد (Demo Hub)

افتح `index.html` في المتصفح لعرض الصفحة الكاملة بالصور، أو راجع الملخص أدناه.

---

## 1) NexMart — متجر إلكتروني متكامل

**بيحل مشكلة إيه؟** منصة تجارة إلكترونية كاملة: تصفح وفلترة منتجات، سلة ومفضلة، إدارة طلبات، ودفع فعلي عبر Stripe — بواجهة عربي/إنجليزي (RTL/LTR) ووضع ليلي.

- **Live:** https://nexmart.vercel.app
- **Code:** https://github.com/Mahmod-mourad/e-commerce-platform-NexMart
- **Stack:** Next.js 14, TypeScript, Tailwind, Stripe, PostgreSQL, JWT (HttpOnly), i18n RTL, Docker, Vercel
- **Screenshots:** `screenshots/nexmart/` (home, products, product-detail, cart)

**How to Run:**
```bash
git clone https://github.com/Mahmod-mourad/e-commerce-platform-NexMart.git
cd e-commerce-platform-NexMart
docker compose up --build      # التطبيق: http://localhost:3000
```

---

## 2) Project Management System — إدارة مشاريع Multi-tenant

**بيحل مشكلة إيه؟** نظام SaaS لإدارة المشاريع: كل شركة (Tenant) معزولة تماماً عبر RLS Policies، مع لوحة إحصائيات حية وتحديثات Real-time (Socket.IO) وإشعارات.

- **Live:** https://pms-web-lilac.vercel.app
- **Code:** https://github.com/Mahmod-mourad/Project-management-system
- **Stack:** Next.js 14, NestJS, Supabase (PostgreSQL + Auth), RLS, Socket.IO, JWT + Bcrypt, Swagger, Jest, Vercel
- **Screenshots:** `screenshots/pms/` (login, dashboard, projects, tasks, users)

**How to Run:**
```bash
npx supabase start                                   # 1) قاعدة البيانات
psql "$DB_URL" -f scripts/01-tenants-and-plans.sql   # 2) السكيما + seed (01 → 04 بالترتيب)
psql "$DB_URL" -f scripts/02-profiles-projects-tasks.sql
psql "$DB_URL" -f scripts/03-notifications.sql
psql "$DB_URL" -f scripts/04-seed-demo-data.sql

cd backend                                           # 3) الباك اند (3001)
SUPABASE_URL=http://127.0.0.1:54321 \
SUPABASE_SERVICE_ROLE_KEY=... npm run start:dev

NEXT_PUBLIC_API_URL=http://localhost:3001/api/v1 npm run dev   # 4) الفرونت
```
**حساب تجريبي:** `admin@demo.localhost` / `DemoPassword123!` (وحساب `member@demo.localhost`).

---

## 3) Car Rental System — نظام تأجير سيارات

**بيحل مشكلة إيه؟** منصة حجز سيارات عربية بالكامل (RTL): فلترة متقدمة، بحث جغرافي قرب الفروع (PostGIS)، حجز ودفع، ولوحة أدمن لإدارة الأسطول.

- **Code:** https://github.com/Mahmod-mourad/Car-Rental-System
- **Stack:** Next.js (RTL), NestJS, PostgreSQL + PostGIS, TypeORM, JWT, Swagger, Docker Compose
- **Screenshots:** `screenshots/car-rental/` (home, cars, car-detail, swagger)

**How to Run (أمر واحد):**
```bash
git clone https://github.com/Mahmod-mourad/Car-Rental-System.git
cd Car-Rental-System
docker compose up --build
```
| الخدمة | الرابط |
|---|---|
| Web | http://localhost:3000 |
| API | http://localhost:3001 |
| Swagger | http://localhost:3001/api |

---

## ملاحظات مهمة للعرض في المقابلات

- **كل اللقطات حقيقية** — مأخوذة من التطبيقات وهي شغّالة محلياً ببيانات حقيقية من قواعد البيانات.
- **Lives منشورة:** NexMart وPMS على Vercel. Car Rental يعمل بـ Docker Compose محلياً (يعرض مهارات Docker).
- تم إصلاح باج SQL حقيقي في Car Rental (endpoint السيارات المشابهة `/vehicles/similar/:id` كان بيرجع 500 بسبب استعلام خام بأسماء جداول/parameters غلط) — قصة ممتازة تُحكى في الانترفيو.
