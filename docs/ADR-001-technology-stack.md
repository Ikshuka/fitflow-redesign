# Architecture Decision Record (ADR)

| Field | Detail |
| :--- | :--- |
| Title | ADR-001: Adopt Flutter + NestJS microservices + FastAPI AI service + PostgreSQL/MongoDB for FitFlow redesign |
| Status | Accepted |
| Context | FitFlow must serve iOS, Android and web from a single team, handle sensitive health data under compliance pressure, support AI-driven personalisation, and provide real-time social/workout features, all within a mid-sized team's delivery and operating budget. |
| Decision | Use Flutter for all client surfaces; a NestJS-based microservice backend (User, Workout, Social, Nutrition) behind a single API Gateway with Auth0 authentication; a dedicated Python/FastAPI microservice for AI/ML personalisation; PostgreSQL as the primary relational store for accounts and health-adjacent data; MongoDB for the social feed and activity logs; Redis for caching and as the real-time Pub/Sub backbone; S3 for media storage. |
| Alternatives considered | React Native + single Node monolith + Firebase (rejected: weaker web story, monolith would slow a growing team, Firestore's query limitations hurt social feed features). Kotlin Multiplatform + Swift native (rejected: two UI codebases increase cost and slow delivery). Go backend (rejected as the core backend: excellent performance but weaker native fit for AI tooling and smaller hiring pool; retained as a future option for latency-critical services). |
| Consequences | Positive: single frontend codebase, clear service boundaries, strong compliance posture, natural home for AI work in Python. Negative: operating two backend languages (TypeScript + Python) adds a small amount of cross-team coordination; microservices add operational complexity relative to a monolith, mitigated by starting with a small number of coarse-grained services rather than over-fragmenting. |
| Revisit when | User base or team size grows enough to justify splitting services further, introducing gRPC internally, or evaluating Go for a specific high-throughput service. |
