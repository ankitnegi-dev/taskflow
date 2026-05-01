# 🚀 TaskFlow – Backend Developer Intern Assignment Submission

A production-ready full-stack **Task Management System** built with **Node.js, Express, TypeScript, PostgreSQL, Prisma, Redis, and Next.js**.

This project demonstrates **secure authentication, role-based access control, scalable backend architecture, and full frontend integration**.

---

# 📌 Live Features Overview

## 🔐 Authentication System

* User Registration & Login
* Secure password hashing (bcrypt)
* JWT-based authentication
* Role-based access control (USER / ADMIN)

## 📋 Task Management (CRUD)

* Create tasks
* View all / single task
* Update tasks
* Delete tasks
* Status tracking (TODO / IN_PROGRESS / DONE)
* Priority levels (LOW / MEDIUM / HIGH)

## 🧠 System Design Features

* Modular backend architecture
* RESTful API design
* Centralized error handling
* Input validation (Zod)
* API versioning (`/api/v1`)
* Swagger documentation
* Rate limiting middleware

## 💻 Frontend (Next.js)

* Authentication pages (Login/Register)
* Protected dashboard
* Task management UI
* API integration layer
* Zustand state management
* Responsive UI with Tailwind CSS

## ⚙️ DevOps & Scalability

* Dockerized backend + database
* PostgreSQL via Prisma ORM
* Redis integration (optional caching layer)
* Scalable folder/module structure

---

# 🧱 Tech Stack

| Layer      | Technology                      |
| ---------- | ------------------------------- |
| Backend    | Node.js, Express.js, TypeScript |
| Database   | PostgreSQL                      |
| ORM        | Prisma                          |
| Auth       | JWT + bcrypt                    |
| Frontend   | Next.js (App Router)            |
| State      | Zustand                         |
| Validation | Zod                             |
| Cache      | Redis (optional)                |
| DevOps     | Docker                          |

---

# 🚀 Getting Started

## 1. Clone Repository

```bash
git clone https://github.com/ankitnegi-dev/taskflow.git
cd taskflow
```

---

## 2. Start Database (Docker)

```bash
docker compose up -d postgres redis
```

---

## 3. Backend Setup

```bash
cd backend
npm install
cp .env.example .env
```

### Configure `.env`

```env
DATABASE_URL="postgresql://postgres:password@localhost:55432/taskflow?schema=public"
JWT_SECRET=your_super_secret_key
JWT_EXPIRES_IN=7d
PORT=5000
```

### Run migrations

```bash
npx prisma migrate dev --name init
npx prisma generate
```

### Start backend

```bash
npm run dev
```

---

## 4. Frontend Setup

```bash
cd ../frontend
npm install
cp .env.example .env.local
```

### Configure

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api/v1
```

### Start frontend

```bash
npm run dev
```

---

# 🌐 Application URLs

| Service      | URL                                                                        |
| ------------ | -------------------------------------------------------------------------- |
| Frontend     | [http://localhost:3000](http://localhost:3000)                             |
| Backend API  | [http://localhost:5000/api/v1](http://localhost:5000/api/v1)               |
| Swagger Docs | [http://localhost:5000/api-docs](http://localhost:5000/api-docs)           |
| Health Check | [http://localhost:5000/api/v1/health](http://localhost:5000/api/v1/health) |

---

# 🔐 Authentication Flow

## Register

```http
POST /api/v1/auth/register
```

## Login

```http
POST /api/v1/auth/login
```

### Response

```json
{
  "data": {
    "token": "JWT_TOKEN"
  }
}
```

---

## Using Token

```
Authorization: Bearer <token>
```

⚠️ Do NOT use:

```
Bearer Bearer <token>
```

---

# 📋 API Endpoints

## Auth

| Method | Endpoint       | Description      |
| ------ | -------------- | ---------------- |
| POST   | /auth/register | Register user    |
| POST   | /auth/login    | Login user       |
| GET    | /auth/profile  | Get current user |

## Tasks

| Method | Endpoint   | Description   |
| ------ | ---------- | ------------- |
| GET    | /tasks     | Get all tasks |
| GET    | /tasks/:id | Get task      |
| POST   | /tasks     | Create task   |
| PUT    | /tasks/:id | Update task   |
| DELETE | /tasks/:id | Delete task   |

---

# 🧪 Sample Credentials

## Admin

```
Email: admin@taskflow.io
Password: Admin@123456
```

## User

```
Email: john@taskflow.io
Password: User@123456
```

---

# 🧠 Scalability Highlights

* Modular architecture (feature-based modules)
* Stateless authentication (JWT)
* Database abstraction using Prisma ORM
* Middleware-based request pipeline
* Docker-ready deployment
* Redis ready for caching layer expansion
* Clean separation of concerns (controller/service/repository pattern)

---

# ⚠️ Common Issues

## 1. Port already in use

Change ports in docker-compose or kill process

## 2. Prisma auth error

Ensure DATABASE_URL matches Docker credentials

## 3. Swagger unauthorized

Use correct format:

```
Bearer <token>
```

## 4. Login issues

Ensure correct seeded credentials

---

# 📌 Submission Summary

This project demonstrates:

* JWT Authentication system
* Role-based access control (RBAC)
* Full CRUD task management system
* Scalable backend architecture
* Prisma ORM database modeling
* RESTful API design
* Swagger API documentation
* Dockerized environment
* Full-stack integration (Next.js frontend)

---

# 🏁 Final Note

This system is designed to be **scalable, secure, and production-ready**, following real-world backend engineering practices including modular architecture, authentication flows, and deployment readiness.
