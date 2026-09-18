# Backend & Infrastructure Evaluation

## 2.1 Backend Frameworks

| Criterion | Node.js / NestJS | Python / FastAPI | Go |
| :--- | :--- | :--- | :--- |
| Scalability | Good — event loop handles high I/O concurrency well; scales horizontally | Good — async support via ASGI (Uvicorn/Gunicorn); slightly lower raw throughput than Go | Excellent — goroutines give very high concurrency and low memory overhead |
| Query/runtime performance | Good for I/O-bound workloads; CPU-bound tasks need worker threads | Good; benefits from async I/O, but CPU-bound Python code is slower than compiled languages | Excellent — compiled, statically typed, very low latency |
| Health data handling | Solid with validation pipes (class-validator) and mature ORMs (TypeORM/Prisma) | Excellent — Pydantic gives strong, declarative data validation, useful for structured health records | Good but more boilerplate — no built-in validation layer, needs manual/typed structs |
| Security compliance readiness (HIPAA/GDPR) | Good — mature middleware ecosystem (helmet, rate-limiters), widely used in regulated apps | Good — same ecosystem maturity as Node for auth/encryption libraries; strong typing reduces data-shape bugs | Good — smaller ecosystem of ready-made compliance middleware, more custom work required |
| Real-time capability | Excellent — native WebSocket/Socket.IO support, same language as an eventual RN option | Good — WebSocket support via Starlette; typically paired with a separate gateway for scale | Excellent — goroutines make persistent-connection fan-out very efficient |
| AI/ML integration potential | Moderate — calls out to Python AI services over REST/gRPC; no native ML ecosystem | Excellent — same language as almost all ML tooling (PyTorch, scikit-learn, HF); can host models directly | Moderate — calls out to Python AI services; limited native ML ecosystem |
| Operational cost | Moderate — efficient for I/O workloads, large talent pool keeps hiring cost down | Moderate — efficient enough for typical CRUD/API load; ML workloads add GPU/compute cost regardless of framework | Low — very efficient per-instance, fewer servers needed at scale |
| Team maintainability (mid-sized team) | Excellent — TypeScript end-to-end with a Flutter/RN frontend team eases context-switching; NestJS's opinionated structure suits multiple contributors | Good — clean, readable, popular in universities/bootcamps so easy to hire for; separate language from frontend | Good — simple language, but smaller pool of experienced Go developers than JS/Python |

## 2.4 Backend & Infrastructure Recommendation

**Recommended: NestJS (Node.js/TypeScript) + PostgreSQL + MongoDB + Auth0**
