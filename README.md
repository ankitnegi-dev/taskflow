# TaskFlow API

A production-ready full-stack task management application built with **Node.js, Express, TypeScript, PostgreSQL, Prisma, Redis, and Next.js**.

---

# Tech Stack

| Layer      | Technology                           |
| ---------- | ------------------------------------ |
| Backend    | Node.js + Express + TypeScript       |
| Database   | PostgreSQL + Prisma ORM              |
| Auth       | JWT (Access Tokens) + bcrypt         |
| API Docs   | Swagger / OpenAPI 3.0                |
| Frontend   | Next.js 14 (App Router) + TypeScript |
| Styling    | Tailwind CSS                         |
| State      | Zustand                              |
| Validation | Zod (frontend + backend)             |
| Cache      | Redis (optional)                     |
| DevOps     | Docker + Docker Compose              |

---

# Quick Start

## Prerequisites

* Node.js ≥ 18
* Docker & Docker Compose
* npm or yarn

---

# 1. Clone Repository

```bash
git clone https://github.com/your-org/taskflow.git
cd taskflow
```

---

# 2. Start Database (Docker)

⚠️ IMPORTANT: Ensure ports 5432 and 6379 are not already in use.

```bash
docker compose up -d postgres redis
```

If ports are occupied, update `docker-compose.yml`:

* PostgreSQL → `55432:5432`
* Redis → `6380:6379`

---

# 3. Backend Setup

```bash
cd backend
npm install
cp .env.example .env
```

## Configure `.env`

```env
DATABASE_URL="postgresql://postgres:password@localhost:55432/taskflow?schema=public"
JWT_SECRET=your_super_secret_jwt_key_at_least_32_chars
JWT_EXPIRES_IN=7d
JWT_REFRESH_SECRET=your_refresh_secret
PORT=5000
```

---

## Database Setup

```bash
npx prisma migrate dev --name init
npx prisma generate
```

(Optional)

```bash
npm run prisma:seed
```

---

## Start Backend

```bash
npm run dev
```

Backend runs at:

* API: [http://localhost:5000/api/v1](http://localhost:5000/api/v1)
* Swagger: [http://localhost:5000/api-docs](http://localhost:5000/api-docs)
* Health: [http://localhost:5000/api/v1/health](http://localhost:5000/api/v1/health)

---

# 4. Frontend Setup

```bash
cd ../frontend
npm install
cp .env.example .env.local
```

## Configure

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api/v1
```

## Run Frontend

```bash
npm run dev
```

Frontend runs at:

* [http://localhost:3000](http://localhost:3000)

---

# Authentication Flow

## 1. Register User

POST `/api/v1/auth/register`

```json
{
  "name": "Admin User",
  "email": "admin@taskflow.io",
  "password": "Admin@123456"
}
```

---

## 2. Login User

POST `/api/v1/auth/login`

Response:

```json
{
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIs..."
  }
}
```

---

## 3. Using Token (IMPORTANT)

All protected routes require:

```
Authorization: Bearer <token>
```

⚠️ Do NOT send:

```
Bearer Bearer <token>
```

---

# API Endpoints

## Auth

| Method | Endpoint       | Auth   | Description        |
| ------ | -------------- | ------ | ------------------ |
| POST   | /auth/register | Public | Register user      |
| POST   | /auth/login    | Public | Login user         |
| GET    | /auth/profile  | JWT    | Get logged-in user |

---

## Tasks

| Method | Endpoint   | Auth | Description   |
| ------ | ---------- | ---- | ------------- |
| GET    | /tasks     | JWT  | Get all tasks |
| GET    | /tasks/:id | JWT  | Get task      |
| POST   | /tasks     | JWT  | Create task   |
| PUT    | /tasks/:id | JWT  | Update task   |
| DELETE | /tasks/:id | JWT  | Delete task   |

---

## Query Parameters (Tasks)

```
?page=1&limit=10&status=TODO&priority=HIGH&search=api&sortBy=createdAt&sortOrder=desc
```

---

# Swagger API

[http://localhost:5000/api-docs](http://localhost:5000/api-docs)

Steps:

1. Click Authorize
2. Paste:

   ```
   Bearer <token>
   ```
3. Test endpoints

---

# Seed Credentials (if enabled)

| Role  | Email                                         | Password     |
| ----- | --------------------------------------------- | ------------ |
| ADMIN | [admin@taskflow.io](mailto:admin@taskflow.io) | Admin@123456 |
| USER  | [john@taskflow.io](mailto:john@taskflow.io)   | User@123456  |

---

# Docker Deployment

```bash
docker compose up --build
```

Stop:

```bash
docker compose down
```

---

# Folder Structure

```
taskflow/
├── backend/
│   ├── prisma/
│   └── src/
│       ├── modules/
│       ├── middleware/
│       ├── utils/
│       ├── config/
│       ├── routes/
│       ├── docs/
│       ├── types/
│       ├── app.ts
│       └── server.ts
├── frontend/
│   ├── app/
│   ├── components/
│   ├── store/
│   ├── lib/
│   └── types/
├── docker-compose.yml
└── README.md
```

---

# Common Issues

## 1. Port already in use

Stop conflicting services or change Docker ports.

## 2. Prisma authentication error

Ensure `DATABASE_URL` matches credentials defined in `docker-compose.yml`.

## 3. Swagger Unauthorized

Use correct format:

```
Authorization: Bearer <token>
```

## 4. Login fails after registration

Check correct email/password and user existence.

---

# Project Highlights

This project demonstrates:

* JWT authentication system
* Role-based access control (ADMIN / USER)
* Full CRUD task management system
* Prisma ORM with PostgreSQL
* RESTful API design using Express
* Swagger API documentation
* Dockerized development environment
* Full-stack integration with Next.js frontend

---