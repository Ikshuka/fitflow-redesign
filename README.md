# FitFlow Redesign

Technology redesign of the FitFlow fitness app, covering frontend/backend
technology evaluation, a weighted decision matrix, system architecture and
an Architecture Decision Record (ADR).

## Tech Stack Summary
- Frontend: Flutter (iOS, Android, Web)
- Backend: NestJS (Node.js/TypeScript) microservices behind an API Gateway
- AI/ML: Python/FastAPI microservice for personalisation
- Databases: PostgreSQL (primary), MongoDB (social/activity)
- Cache/Real-time: Redis + Socket.IO
- Auth: Auth0
- Storage: Amazon S3

## Repository Structure
- frontend/    Flutter client application
- backend/     NestJS microservices (User, Workout, Social, Nutrition)
- ai-service/  FastAPI AI/ML personalisation service
- docs/        Technology comparisons, decision matrix, architecture, ADR

## Documentation
See the docs/ folder for the full frontend and backend comparison
matrices, the weighted decision matrix, the architecture diagram and
ADR-001.
