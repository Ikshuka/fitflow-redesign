# FitFlow — Backend (NestJS)

> Microservice-based backend built with NestJS (Node.js / TypeScript), PostgreSQL, MongoDB, Redis, and Auth0.

---

## Overview

The FitFlow backend is a collection of NestJS microservices behind a single API Gateway. It handles user management, workout tracking, social features, and nutrition logging. Auth0 provides authentication, PostgreSQL stores structured health data, MongoDB powers the social feed, and Redis handles caching and real-time pub/sub.

---

## Tech Stack

| Technology | Purpose |
| :--- | :--- |
| NestJS 10.x | Backend framework (TypeScript) |
| TypeORM / Prisma | ORM for PostgreSQL |
| Mongoose | ODM for MongoDB |
| PostgreSQL | Primary relational database (users, workouts, nutrition) |
| MongoDB | Social feed & activity logs |
| Redis | Caching, sessions, and pub/sub |
| Socket.IO | Real-time communication (live workouts, notifications) |
| Auth0 | Authentication & authorisation (JWT) |
| Amazon S3 | Media/file storage (profile pictures, workout images) |
| Jest | Unit & integration testing |

---

## Microservices

| Service | Responsibility |
| :--- | :--- |
| API Gateway | Request routing, rate limiting, Auth0 JWT validation |
| User Service | User profiles, preferences, account management |
| Workout Service | Exercise logging, workout plans, progress tracking |
| Social Service | Activity feed, friends, challenges, leaderboards |
| Nutrition Service | Meal logging, calorie/macro tracking |

---

## Folder Structure (Planned)

```
backend/
├── src/
│   ├── main.ts                    # App entry point
│   ├── app.module.ts              # Root module
│   ├── config/                    # Environment & database configuration
│   ├── common/                    # Shared guards, decorators, pipes, filters
│   ├── modules/
│   │   ├── auth/                  # Auth0 integration & JWT guards
│   │   ├── users/                 # User CRUD & profile management
│   │   ├── workouts/              # Workout tracking & plans
│   │   ├── social/                # Feed, friends, challenges
│   │   └── nutrition/             # Meal logging & macros
│   └── shared/                    # Shared DTOs, interfaces, utilities
├── test/                          # E2E tests
├── docker-compose.yml             # PostgreSQL, MongoDB, Redis containers
├── package.json
├── tsconfig.json
└── README.md
```

---

## Getting Started

```bash
# Install dependencies
npm install

# Set up environment variables (see below)
cp .env.example .env

# Start databases (Docker)
docker-compose up -d

# Run database migrations
npm run migration:run

# Start development server
npm run start:dev

# Run tests
npm run test
```

---

## Environment Variables

Create a `.env` file in the project root:

```env
# Server
PORT=3000
NODE_ENV=development

# PostgreSQL
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_USER=fitflow
POSTGRES_PASSWORD=your-password
POSTGRES_DB=fitflow

# MongoDB
MONGODB_URI=mongodb://localhost:27017/fitflow-social

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# Auth0
AUTH0_DOMAIN=your-auth0-domain.auth0.com
AUTH0_AUDIENCE=https://api.fitflow.com
AUTH0_CLIENT_ID=your-client-id
AUTH0_CLIENT_SECRET=your-client-secret

# AWS S3
AWS_S3_BUCKET=fitflow-media
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_REGION=ap-southeast-1
```

---

## API Documentation

API documentation will be auto-generated using **Swagger/OpenAPI** via `@nestjs/swagger` and available at:

```
http://localhost:3000/api/docs
```
