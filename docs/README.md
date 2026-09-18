# FitFlow Redesign — Documentation

This directory contains the complete technical deliverables, evaluations, and architecture designs for the **FitFlow Redesign** project.

---

## Deliverables Index

| # | Document | Description |
| :---: | :--- | :--- |
| **Activity 1** | [Frontend Framework Evaluation](frontend-comparison.md) | Comprehensive 10-criterion comparison of Flutter, React Native, Kotlin Multiplatform, and Swift/SwiftUI with recommendation. |
| **Activity 2** | [Backend, Database & Auth Evaluation](backend-comparison.md) | In-depth evaluation of backend frameworks (NestJS, FastAPI, Go), polyglot databases (PostgreSQL, MongoDB, Firestore, DynamoDB), and authentication options (Auth0, Cognito, Firebase, Supabase). |
| **Activity 3** | [Technology Comparison Matrix](decision-matrix.md) | Consolidated weighted scoring matrix evaluating all candidate technologies across 7 weighted criteria with mathematical justification. |
| **Activity 4** | [High-Level System Architecture](architecture.md) | System architecture diagram (Mermaid), core feature data flows (workouts, social, nutrition), security (HIPAA/GDPR), scalability, and integration. |
| **Activity 4** | [ADR-001: Technology Stack](ADR-001-technology-stack.md) | Formal Architecture Decision Record capturing the context, decision, alternatives evaluated, and architectural consequences. |

---

## Recommended Technology Stack Summary

* **Frontend:** Flutter (Single codebase for iOS, Android, and Web)
* **API Gateway & Core Backend:** NestJS (Node.js / TypeScript microservices)
* **AI/ML Personalisation:** Python / FastAPI (PyTorch, scikit-learn)
* **Primary Database (System of Record):** PostgreSQL (ACID compliant, encrypted health metrics)
* **Secondary Database (Social & Feeds):** MongoDB (Document store for social streams)
* **Authentication & Authorization:** Auth0 (HIPAA/GDPR-compliant, OAuth2/OIDC)
* **Caching & Real-Time Broker:** Redis + Socket.IO
* **Object Storage:** Amazon S3 (Direct uploads via presigned URLs)
