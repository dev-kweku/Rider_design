Excellent update 💰 — switching to **Paystack** is a smart move. It’s widely supported in Ghana and integrates cleanly with Node.js + Express.

Here’s your **updated backend generation prompt**, refined to include **Paystack integration** and **payment tracking on the Admin Dashboard**, linked from **customer → rider**.

You can use this prompt in **ChatGPT (code mode)**, **Cursor IDE**, **Replit**, or **Copilot** to generate a complete TypeScript + Express backend scaffold.

---

## ⚙️ **Updated Backend Generation Prompt (TypeScript + Express + Paystack Integration)**

> **Prompt:**
>
> Build a **production-grade backend API** for **RiderLink GH**, a Ghanaian delivery rider marketplace that connects customers with verified delivery riders.
>
> Use **TypeScript**, **Node.js**, **Express.js**, and **PostgreSQL (with Prisma ORM)** following clean architecture and best practices.
>
> ---
>
> ### 🧱 **Tech Stack & Standards**
>
> * **Language:** TypeScript
> * **Framework:** Express.js
> * **Database:** PostgreSQL (via Prisma ORM)
> * **Auth:** JWT (access + refresh tokens), bcrypt password hashing
> * **Validation:** Zod or Joi
> * **Environment Variables:** dotenv
> * **Logging:** Winston + Morgan
> * **Documentation:** Swagger (OpenAPI 3.0)
> * **Testing:** Jest + Supertest
> * **Code Style:** ESLint + Prettier
> * **Deployment:** Docker + docker-compose (with PostgreSQL service)
>
> ---
>
> ### 🧩 **Core Functional Modules**
>
> #### 1. **Auth Module**
>
> * Register and login endpoints for users (riders, customers, admin).
> * JWT-based authentication with refresh tokens.
> * Role-based access control (RIDER, CUSTOMER, ADMIN).
> * Forgot/reset password endpoints.
>
> #### 2. **Rider Module**
>
> * Create, view, and update rider profile.
> * Rider verification status: *pending*, *approved*, *rejected*.
> * Availability toggle (Online/Offline).
> * Vehicle details: type, license plate, location, contact info.
> * Rider earnings summary (linked from completed Paystack payments).
>
> #### 3. **Customer Module**
>
> * Register, view, and update profile.
> * Search for nearby riders (filter by city or availability).
> * Book a rider for delivery (creates a booking record).
>
> #### 4. **Booking Module**
>
> * Create a booking (customer → rider).
> * Booking status: *requested*, *accepted*, *in-progress*, *completed*, *cancelled*.
> * Each booking should have a linked payment record.
>
> #### 5. **Payments Module (Paystack Integration)**
>
> * Integrate **Paystack API** for handling payments.
> * Endpoints:
>
>   * `POST /payments/initialize` → initialize Paystack transaction with amount, customerId, riderId, bookingId.
>   * `GET /payments/verify/:reference` → verify transaction via Paystack callback.
>   * `POST /payments/webhook` → handle Paystack webhook events (successful payment, failed, etc.).
> * Record all transactions in a **Payments table** with:
>
>   * `id`, `customerId`, `riderId`, `bookingId`, `amount`, `status`, `reference`, `transactionDate`, `channel`.
> * On successful verification, update:
>
>   * Booking status → *paid / completed*
>   * Rider earnings summary
>   * Admin dashboard metrics
>
> #### 6. **Admin Module**
>
> * Admin login with role-based permissions.
> * Dashboard overview:
>
>   * Total Riders, Active Riders, Pending Verifications
>   * Total Customers
>   * Total Bookings
>   * Total Revenue (from verified Paystack payments)
> * View all payments with full details:
>
>   * Transaction reference, amount, date, customer name, rider name.
> * Manage riders (approve/suspend) and users.
> * Export reports to CSV or PDF.
>
> ---
>
> ### 🧰 **Folder Structure Example**
>
> ```
> src/
> ├── app.ts
> ├── server.ts
> ├── config/
> │   ├── env.ts
> │   ├── db.ts
> ├── modules/
> │   ├── auth/
> │   │   ├── auth.controller.ts
> │   │   ├── auth.service.ts
> │   │   ├── auth.routes.ts
> │   │   ├── auth.schema.ts
> │   ├── riders/
> │   │   ├── rider.controller.ts
> │   │   ├── rider.service.ts
> │   │   ├── rider.routes.ts
> │   │   ├── rider.model.ts
> │   ├── customers/
> │   │   ├── customer.controller.ts
> │   │   ├── customer.service.ts
> │   │   ├── customer.routes.ts
> │   ├── bookings/
> │   │   ├── booking.controller.ts
> │   │   ├── booking.service.ts
> │   │   ├── booking.routes.ts
> │   │   ├── booking.model.ts
> │   ├── payments/
> │   │   ├── payment.controller.ts
> │   │   ├── payment.service.ts
> │   │   ├── payment.routes.ts
> │   │   ├── payment.model.ts
> │   ├── admin/
> │   │   ├── admin.controller.ts
> │   │   ├── admin.service.ts
> │   │   ├── admin.routes.ts
> ├── middleware/
> │   ├── auth.middleware.ts
> │   ├── error.middleware.ts
> ├── utils/
> │   ├── logger.ts
> │   ├── response.ts
> │   ├── paystack.ts
> ├── prisma/
> │   ├── schema.prisma
> ├── tests/
> │   ├── payments.test.ts
> │   ├── booking.test.ts
> │   ├── auth.test.ts
> └── docs/
>     ├── swagger.yaml
> ```
>
> ---
>
> ### 🧾 **Database Models (Prisma Example)**
>
> ```prisma
> model User {
>   id          String   @id @default(uuid())
>   name        String
>   email       String   @unique
>   password    String
>   role        Role
>   phone       String?
>   rider       Rider?
>   customer    Customer?
>   createdAt   DateTime @default(now())
>   updatedAt   DateTime @updatedAt
> }
>
> model Rider {
>   id          String   @id @default(uuid())
>   userId      String   @unique
>   vehicleType String
>   location    String
>   verified    Boolean  @default(false)
>   availability Boolean @default(false)
>   bookings    Booking[]
>   payments    Payment[]
>   user        User     @relation(fields: [userId], references: [id])
> }
>
> model Customer {
>   id        String   @id @default(uuid())
>   userId    String   @unique
>   bookings  Booking[]
>   payments  Payment[]
>   user      User     @relation(fields: [userId], references: [id])
> }
>
> model Booking {
>   id          String   @id @default(uuid())
>   riderId     String
>   customerId  String
>   status      String   @default("requested")
>   paymentId   String?
>   createdAt   DateTime @default(now())
>   updatedAt   DateTime @updatedAt
>   rider       Rider    @relation(fields: [riderId], references: [id])
>   customer    Customer @relation(fields: [customerId], references: [id])
>   payment     Payment? @relation(fields: [paymentId], references: [id])
> }
>
> model Payment {
>   id            String   @id @default(uuid())
>   reference     String   @unique
>   amount        Float
>   status        String
>   transactionDate DateTime @default(now())
>   customerId    String
>   riderId       String
>   bookingId     String
>   channel       String?
>   customer      Customer @relation(fields: [customerId], references: [id])
>   rider         Rider    @relation(fields: [riderId], references: [id])
>   booking       Booking  @relation(fields: [bookingId], references: [id])
> }
>
> enum Role {
>   ADMIN
>   RIDER
>   CUSTOMER
> }
> ```
>
> ---
>
> ### 📊 **Admin Dashboard API Endpoints**
>
> * `GET /admin/overview` → totals (riders, bookings, revenue).
> * `GET /admin/payments` → list all payments (join with rider & customer tables).
> * `GET /admin/riders` → all riders with verification + subscription info.
> * `GET /admin/reports/revenue` → daily/monthly revenue summary.
>
> Example response for `/admin/payments`:
>
> ```json
> [
>   {
>     "reference": "PSK-233847238",
>     "amount": 25.00,
>     "status": "success",
>     "transactionDate": "2025-10-05T12:33:00Z",
>     "customer": { "name": "Ama Boateng", "phone": "0541234567" },
>     "rider": { "name": "Kwame Mensah", "bikeNumber": "GT-1234-23" }
>   }
> ]
> ```
>
> ---
>
> ### 🧪 **Testing & CI**
>
> * Write Jest tests for Auth, Booking, and Payment modules.
> * Use Supertest for integration testing.
> * Add GitHub Actions CI workflow to run lint + tests.
>
> ---
>
> ### 🐳 **Deployment**
>
> * Include Dockerfile + docker-compose.yml (Node + Postgres).
> * Add `.env.example` with:
>
>   ```
>   PORT=4000
>   DATABASE_URL=postgresql://user:pass@localhost:5432/riderlink
>   JWT_SECRET=supersecret
>   PAYSTACK_SECRET_KEY=sk_test_xxxxxxxxx
>   PAYSTACK_PUBLIC_KEY=pk_test_xxxxxxxxx
>   NODE_ENV=development
>   ```
> * Ready to deploy on Render, Railway, or AWS Lightsail.
>
> ---
>
> **Expected Deliverables:**
>
> * Modular TypeScript backend (Express + Prisma).
> * All CRUD routes functional and documented via Swagger (`/api/docs`).
> * Paystack integration with transaction verification and webhook.
> * Admin dashboard-ready APIs showing **user ↔ rider ↔ payment linkage**.
> * Jest test coverage and Docker setup included.

---

Would you like me to now **generate the full folder structure + key backend files** (controllers, services, models, etc.) from this prompt so you can start building or deploy locally?
