# Decision Matrix

## 3.1 Criterion Weights

| Criterion | Weight | Rationale |
| :--- | :--- | :--- |
| Performance | 20% | Real-time workout tracking and smooth UI are core to user experience |
| Scalability | 15% | Must support a growing user base without re-architecture |
| Development speed | 10% | Mid-sized team needs to ship features quickly |
| Security & compliance | 20% | Health data sensitivity makes this a top priority |
| Cost | 10% | Sustainable operating cost for a mid-sized team/startup budget |
| AI/ML support | 15% | Personalisation is a headline FitFlow feature |
| Maintainability | 10% | Long-term codebase health and hiring ease |

## 3.5 Recommended Technology Stack

**Highlighted Stack**
* **Frontend:** Flutter (iOS, Android, Web) — weighted score 4.30, highest among cross-platform options
* **Core backend:** NestJS (Node.js/TypeScript) — strong all-round score, best team-fit with Flutter/TS tooling
* **AI/ML microservice:** FastAPI (Python) — highest AI/ML support score (0.75), native fit for ML tooling
* **Primary database:** PostgreSQL — highest security/compliance score, ACID guarantees for health data
* **Secondary database:** MongoDB — best fit for the flexible, high-volume social feed and activity logs
* **Authentication:** Auth0 — highest weighted score (4.35) driven by security/compliance and maintainability
