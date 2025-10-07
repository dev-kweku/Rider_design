Excellent 🔥 — you’re thinking like a *founder-engineer*.
Here’s a **backend generation prompt** you can use with AI code tools (like ChatGPT’s code interpreter, GitHub Copilot, Replit, or Cursor IDE) to automatically scaffold a **production-grade backend** for your delivery rider platform — **RiderLink GH**.

It’s written to enforce **industry standards**, **scalable architecture**, and **TypeScript + Express.js best practices**.

---

## ⚙️ **AI Backend Build Prompt (TypeScript + Express + Node.js)**

> **Prompt:**
>
> Build a **modular, production-ready backend** for a project called **“RiderLink GH”**, a delivery rider marketplace platform for Ghana.
>
> The backend should be built using **TypeScript**, **Node.js**, and **Express.js**, following **clean architecture** and **industry-standard conventions**.
>
> ---
>
> ### 🧱 **Tech Stack & Standards**
>
> * **Language:** TypeScript
> * **Framework:** Express.js
> * **Database:** PostgreSQL (with Prisma ORM)
> * **Auth:** JWT (Access + Refresh tokens) with bcrypt password hashing
> * **Validation:** Zod or Joi
> * **Environment management:** dotenv
> * **Logging:** Winston + Morgan
> * **API Documentation:** Swagger (OpenAPI 3.0)
> * **Testing:** Jest + Supertest
> * **Code Style:** ESLint + Prettier
> * **Version control:** Git
> * **Folder structure:** Use clean modular architecture with feature-based modules.
> * **Deployment ready:** Include Dockerfile and docker-compose.yml
>
> ---
>
> ### 🧩 **Core Modules / Features**
>
> #### 1. **Auth Module**
>
> * Register user (rider or customer)
> * Login / Logout
> * Refresh token endpoint
> * Password reset
> * Role-based access (user, rider, admin)
> * Middleware for authentication & authorization
>
> #### 2. **Rider Module**
>
> * CRUD endpoints for rider profile
> * Upload ID (image URL field only; actual upload handled by Cloudinary)
> * Availability toggle (Online/Offline)
> * Rider verification status (pending, approved, rejected)
> * Rider ratings (average rating, total reviews count)
> * Subscription status (free, premium)
>
> #### 3. **Customer Module**
>
> * CRUD endpoints for customer profile
> * View nearby riders by location (use simple geo query or external API)
>
> #### 4. **Booking Module**
>
> * Create booking (customer → rider)
> * Update booking status (requested, accepted, in-progress, completed, cancelled)
> * Rider and customer relationship through foreign keys
> * Optional payment reference (for MoMo or Paystack integration)
>
> #### 5. **Payments Module**
>
> * Integration-ready structure for **MTN MoMo API** or **Paystack API**
> * Record transactions with fields: userId, amount, type, status, reference, date
> * Webhook endpoint for payment confirmation
>
> #### 6. **Admin Module**
>
> * Dashboard summary endpoints (total users, active riders, revenue, bookings)
> * Manage riders (approve, suspend, delete)
> * Manage users and payments
>
> ---
>
> ### 🧩 **Folder Structure Example**
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
> │   ├── bookings/
> │   │   ├── booking.controller.ts
> │   │   ├── booking.service.ts
> │   │   ├── booking.routes.ts
> │   │   ├── booking.model.ts
> │   └── payments/
> │       ├── payment.controller.ts
> │       ├── payment.service.ts
> │       ├── payment.routes.ts
> │       ├── payment.model.ts
> ├── middleware/
> │   ├── auth.middleware.ts
> │   ├── error.middleware.ts
> ├── utils/
> │   ├── logger.ts
> │   ├── response.ts
> ├── prisma/
> │   ├── schema.prisma
> ├── tests/
> │   ├── auth.test.ts
> │   ├── rider.test.ts
> └── docs/
>     ├── swagger.yaml
> ```
>
> ---
>
> ### 🧰 **Features to Include**
>
> * Centralized error handling with custom `ApiError` class.
> * Response helper for consistent API responses.
> * Automatic Swagger documentation generation.
> * `.env` file with keys:
>
>   ```
>   PORT=4000
>   DATABASE_URL=postgresql://user:pass@localhost:5432/riderlink
>   JWT_SECRET=supersecret
>   REFRESH_TOKEN_SECRET=supersecretrefresh
>   NODE_ENV=development
>   ```
> * Use dependency injection where necessary (services, repositories).
> * Include seed script to create default Admin account.
>
> ---
>
> ### 🧪 **Testing & CI**
>
> * Write Jest unit tests for Auth, Rider, and Booking modules.
> * Use Supertest for API endpoint tests.
> * Add GitHub Actions CI workflow for lint + test.
>
> ---
>
> ### 🐳 **Deployment**
>
> * Include Dockerfile for containerized deployment.
> * Docker-compose with PostgreSQL service.
> * Ready to deploy on Render, Railway, or AWS Lightsail.
>
> ---
>
> ### ✅ **Expected Output**
>
> * A ready-to-run backend with clean TypeScript architecture.
> * All routes and models structured properly.
> * Swagger docs at `/api/docs`.
> * Authentication, rider management, bookings, and payments endpoints functional.
> * Fully testable using Postman or Swagger UI.
>
> ---
>
> **Deliverables:**
>
> * `/src` folder with modular code.
> * Prisma schema + migrations.
> * Swagger documentation.
> * Example `.env.example` file.
> * README.md with setup instructions and API overview.
> * 5–10 Jest test cases for core modules.

---

### 🧠 Bonus Add-On (Optional)

Add a **WebSocket / Socket.io module** for real-time job status updates — e.g.,

* “Rider accepted job”
* “Delivery in progress”
* “Delivery completed.”

---

Would you like me to generate a **ready-to-run backend boilerplate (TypeScript + Express + Prisma)** using this structure next, so you can start coding immediately?
I can output the full folder structure and key files here.
