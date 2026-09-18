# FitFlow Redesign — Lab Assignment

> **Course:** Mobile & Cloud Application Development  
> **Assignment:** Technology Evaluation, Architecture Design & Repository Setup  
> **Student:** Ikshuka Malhengoda  
> **Email:** iumadawa4@gmail.com  

---

## Assignment Overview

This repository contains the complete deliverables for the FitFlow redesign lab assignment. The task involved evaluating modern technology options for a cross-platform fitness application, producing a weighted decision matrix to justify the chosen stack, designing a high-level system architecture, and documenting the decisions in a formal Architecture Decision Record (ADR).

---

## Objectives

- Evaluate and compare frontend frameworks (Flutter, React Native, Kotlin Multiplatform, Swift/SwiftUI)
- Evaluate and compare backend frameworks, databases, and authentication solutions
- Produce a weighted decision matrix to justify technology choices
- Design a high-level system architecture based on the recommended stack
- Document all decisions in an Architecture Decision Record (ADR)
- Set up a structured GitHub repository as per lab requirements

---

## Recommended Technology Stack

| Layer | Technology | Reason |
| :--- | :--- | :--- |
| Frontend | Flutter (iOS, Android, Web) | Highest code reuse (~95%), single codebase, first-class web support |
| Core Backend | NestJS (Node.js / TypeScript) | Strong scalability, real-time support, TypeScript consistency |
| AI/ML Service | Python / FastAPI | Native ML ecosystem (PyTorch, scikit-learn), fastest AI integration |
| Primary Database | PostgreSQL | ACID compliance, best fit for sensitive health data |
| Secondary Database | MongoDB | Flexible schema for social feeds and activity logs |
| Cache / Real-time | Redis + Socket.IO | Low-latency pub/sub and session caching |
| Authentication | Auth0 | Managed auth, HIPAA/GDPR ready, fast integration |
| Media Storage | Amazon S3 | Scalable, cost-effective object storage |

---

## Repository Structure

```
fitflow-redesign/
├── frontend/          # Flutter client application (iOS, Android, Web)
├── backend/           # NestJS microservices (User, Workout, Social, Nutrition)
├── ai-service/        # FastAPI AI/ML personalisation microservice
└── docs/              # All assignment documentation
    ├── frontend-comparison.md
    ├── backend-comparison.md
    ├── decision-matrix.md
    └── ADR-001-technology-stack.md
```

---

## Documentation

| Document | Description |
| :--- | :--- |
| [Frontend Comparison](docs/frontend-comparison.md) | 10-criterion evaluation of Flutter, React Native, Kotlin Multiplatform, Swift/SwiftUI |
| [Backend Comparison](docs/backend-comparison.md) | 8-criterion evaluation of NestJS, FastAPI, and Go |
| [Decision Matrix](docs/decision-matrix.md) | Weighted scoring matrix with final technology recommendations |
| [ADR-001](docs/ADR-001-technology-stack.md) | Architecture Decision Record documenting the chosen stack and rationale |

