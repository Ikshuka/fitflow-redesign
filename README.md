# FitFlow Redesign — Lab Exercise 05

> **Module:** IT3060 — Human Computer Interaction (Semester 2, 2026)  
> **Degree:** B.Sc. (Hons) in Information Technology — Year 3, SLIIT  
> **Student:** Ikshuka Malhengoda  
> **Email:** iumadawa4@gmail.com  
> **Topic:** Technology Evaluation, Decision Framework & System Architecture  

---

## Assignment Overview

This repository contains the complete deliverables for **Lab Exercise 05** for the **FitFlow** fitness application redesign. The exercise encompasses evaluating contemporary mobile and cross-platform frontend frameworks, comparing cloud backend architectures, databases, and authentication mechanisms, formulating a weighted decision matrix to mathematically justify technology selections, designing a robust high-level system architecture, and formalizing choices through an Architecture Decision Record (ADR).

---

## Objectives & Activity Breakdown

- **Activity 1:** Comprehensive comparative analysis of mobile/cross-platform frontend technologies (Flutter, React Native, Kotlin Multiplatform, and Swift/SwiftUI).
- **Activity 2:** Detailed evaluation of backend frameworks (NestJS, FastAPI, Go), polyglot persistence layers (PostgreSQL, MongoDB, Firestore, DynamoDB), and identity/auth providers (Auth0, AWS Cognito, Firebase, Supabase).
- **Activity 3:** Formulation of a weighted decision matrix scoring all candidate technologies against 7 weighted operational criteria.
- **Activity 4:** High-level system architecture design (including a Mermaid diagram, core feature data flows, HIPAA/GDPR security, and scalability) accompanied by **ADR-001**.
- **Activity 5:** Structured GitHub repository setup with standard conventions, full documentation, modular placeholders, and continuous integration workflows.

---

## Recommended Technology Stack

| Layer | Component | Chosen Technology | Primary Rationale |
| :--- | :--- | :--- | :--- |
| **Frontend** | Cross-Platform Client | **Flutter** (iOS, Android, Web) | ~95% code reuse, single codebase, 120 FPS Impeller rendering, seamless multi-platform UX |
| **Core Backend** | Microservices & API Gateway | **NestJS** (Node.js / TypeScript) | Modular DI architecture, first-class WebSocket gateways, TypeScript consistency |
| **AI / ML Service** | Personalisation Engine | **Python / FastAPI** | Native home for PyTorch, scikit-learn, asynchronous inference execution |
| **Primary Database** | System of Record | **PostgreSQL** | ACID transactions, strict schema integrity, column-level encryption for health metrics |
| **Secondary Database**| Social Feed & Activity | **MongoDB** | High-velocity flexible JSON document storage for community feeds and audit streams |
| **Cache & Real-Time** | Real-Time Broker & Cache | **Redis + Socket.IO** | Low-latency pub/sub event fan-out and distributed session caching |
| **Authentication** | Identity Provider & RBAC | **Auth0** | Out-of-the-box HIPAA/GDPR compliance, enterprise MFA, social login integrations |
| **Storage** | Object / Media Store | **Amazon S3** | Scalable, secure storage for progress photos and media via presigned URLs |

---

## Repository Structure

```
fitflow-redesign/
├── .github/
│   └── workflows/
│       └── ci.yml                 # CI workflow (docs & lint validation)
├── frontend/                      # Flutter client application scaffold & README
├── backend/                       # NestJS microservices scaffold & README
├── ai-service/                    # FastAPI AI/ML microservice scaffold & README
├── docs/                          # Comprehensive assignment documentation
│   ├── README.md                  # Documentation index & summary
│   ├── frontend-comparison.md     # Activity 1: Frontend evaluation (10 criteria)
│   ├── backend-comparison.md      # Activity 2: Backend, DB & Auth evaluation
│   ├── decision-matrix.md         # Activity 3: Weighted scoring decision matrix
│   ├── architecture.md            # Activity 4: High-level architecture & data flows
│   └── ADR-001-technology-stack.md# Activity 4: Architecture Decision Record
├── .gitignore                     # Git exclusion rules
└── README.md                      # Repository root overview
```

---

## Documentation Index

| Document | Description |
| :--- | :--- |
| [Frontend Comparison](docs/frontend-comparison.md) | 10-criterion comparative evaluation of Flutter, React Native, Kotlin Multiplatform, and Swift/SwiftUI |
| [Backend, DB & Auth Evaluation](docs/backend-comparison.md) | Comprehensive evaluation of backend engines, relational/NoSQL datastores, and authentication options |
| [Decision Matrix](docs/decision-matrix.md) | Mathematical weighted decision matrix across 7 operational criteria justifying the chosen stack |
| [High-Level Architecture](docs/architecture.md) | Visual system architecture diagram (Mermaid), 3 feature data flows, and security/scalability analysis |
| [ADR-001: Technology Stack](docs/ADR-001-technology-stack.md) | Formal Architecture Decision Record documenting context, decisions, alternatives, and consequences |
