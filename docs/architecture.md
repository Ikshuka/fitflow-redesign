# Activity 4 — High-Level System Architecture

This document describes the high-level system architecture for the FitFlow redesign, detailing client interfaces, edge routing, microservice layers, persistent datastores, core feature data flows, and non-functional requirements (security, scalability, and integration).

---

## 4.1 System Architecture Diagram

```mermaid
graph TD
    %% Client Layer
    subgraph CLIENT_LAYER ["Client Layer (Flutter Unified Codebase)"]
        iOS["Flutter iOS App\n(Native Companion/HealthKit)"]
        Android["Flutter Android App\n(Health Connect)"]
        Web["Flutter Web\n(PWA / Responsive CanvasKit)"]
        Watch["Wearable Companion\n(HealthKit / Health Connect)"]
    end

    %% Edge / Ingress Layer
    subgraph EDGE_LAYER ["Edge & Ingress Layer"]
        Gateway["API Gateway (NestJS)\nRate Limiting | CORS | Routing"]
        Auth0["Auth0 (OIDC / OAuth2)\nJWT Issuance | MFA | Social Login"]
    end

    %% Application Microservices Layer
    subgraph APP_LAYER ["Application Services Layer (NestJS / TypeScript)"]
        UserService["User & Profile Service\nAccount Settings, Privacy"]
        WorkoutService["Workout Service\nExercise Logs, Plans, Sessions"]
        SocialService["Social Service\nFeeds, Friends, Challenges"]
        NutritionService["Nutrition Service\nMeal Logs, Macro Tracking"]
    end

    %% Real-Time & AI Microservice Layer
    subgraph AI_RT_LAYER ["AI & Real-Time Layer"]
        AIService["AI/ML Microservice (Python / FastAPI)\nPersonalisation Engine | PyTorch | Scikit-Learn"]
        RTGateway["Real-Time Gateway (Socket.IO / WebSockets)\nLive Workout Sync | Push Events"]
    end

    %% Data Layer
    subgraph DATA_LAYER ["Data Persistence & Storage Layer"]
        Postgres[(PostgreSQL Primary)\nAccounts, Encrypted Health Telemetry]
        Mongo[(MongoDB Secondary)\nSocial Feeds, Activity Stream]
        Redis[(Redis Cache & Broker)\nSessions, Pub/Sub Leaderboards]
        S3[(Amazon S3 Storage)\nProgress Photos, Workout Media]
    end

    %% Connections
    iOS --> Gateway
    Android --> Gateway
    Web --> Gateway
    Watch --> Gateway
    
    Gateway -. Auth Validation .-> Auth0
    
    Gateway --> UserService
    Gateway --> WorkoutService
    Gateway --> SocialService
    Gateway --> NutritionService
    Gateway <--> RTGateway

    WorkoutService <--> AIService
    NutritionService <--> AIService

    UserService --> Postgres
    WorkoutService --> Postgres
    NutritionService --> Postgres
    
    SocialService --> Mongo
    SocialService --> S3
    
    RTGateway <--> Redis
    SocialService --> Redis
    WorkoutService --> Redis
```

---

## 4.2 Key Architectural Components

1. **Client Tier (Flutter):** Single codebase compiled to native ARM binaries for iOS/Android and CanvasKit for Web. Utilizes platform channels for native hardware sensors (Apple HealthKit / Android Health Connect).
2. **Edge / API Gateway (NestJS):** Acts as the single entry point for all client requests. Enforces rate limiting, terminates TLS, authenticates bearer tokens against Auth0 public keys, and reverse-proxies requests to internal domain microservices.
3. **Application Services (NestJS):** Domain-driven microservices designed with loose coupling:
   - **User Service:** Manages user credentials, privacy profiles, and GDPR consent states.
   - **Workout Service:** Orchestrates live workout routines, set/rep validation, and workout plan lifecycle.
   - **Social Service:** Handles social feeds, user follows, community challenges, and leaderboard generation.
   - **Nutrition Service:** Tracks caloric intake, macro breakdowns, and barcode database lookups.
4. **AI/ML Personalisation Microservice (Python / FastAPI):** Standalone machine learning service executing recommendations asynchronously using PyTorch and scikit-learn models.
5. **Real-Time Gateway (Socket.IO + Redis):** Manages persistent WebSocket connections for live workout sessions, group challenges, and immediate notification fan-outs.
6. **Persistence Layer (Polyglot):**
   - **PostgreSQL:** ACID transactional store for relational, regulated health metrics.
   - **MongoDB:** High-throughput document store for social timeline posts and comment threads.
   - **Redis:** In-memory caching for active workout states, rate-limiter buckets, and pub/sub message brokering.
   - **Amazon S3:** Direct-to-bucket media uploads via presigned URLs.

---

## 4.3 Data Flows for Core Features

### 1. Personalised Workout Plan Generation
1. **Client Request:** User triggers a request for a custom training program via the mobile client.
2. **Gateway Routing:** The API Gateway validates the Auth0 JWT and forwards the request to the `Workout Service`.
3. **Context Assembly:** The `Workout Service` fetches user fitness goals, past performance history, and recovery metrics from `PostgreSQL`.
4. **AI Inference Delegation:** The `Workout Service` invokes the `AI/ML Microservice` over internal REST/gRPC with pseudonymised telemetry.
5. **Model Evaluation:** The FastAPI service runs the recommendation algorithm (evaluating muscle fatigue balance and target progression) and returns a structured multi-week plan.
6. **Persistence & Notification:** The `Workout Service` commits the generated plan to `PostgreSQL` and dispatches a WebSocket event via the `Real-Time Gateway` to inform the user that their plan is ready.

### 2. Social Sharing & Live Feed Fan-Out
1. **Media Upload:** When a user shares a workout milestone with an image, the client requests a presigned S3 upload URL from the `Social Service`.
2. **Direct Storage:** The client uploads the image binary directly to Amazon S3, bypassing application servers.
3. **Post Creation:** The client submits post metadata (text, workout summary metrics, S3 image URL) to the `Social Service`.
4. **Document Insertion:** The `Social Service` writes the post document to `MongoDB`.
5. **Real-Time Distribution:** The `Social Service` publishes an event to `Redis Pub/Sub`.
6. **WebSocket Fan-Out:** The `Real-Time Gateway` intercepts the Redis event and fans it out via active WebSockets to online followers' devices.

### 3. Nutrition & Macro Tracking
1. **Meal Logging:** User logs meal items (manually or via barcode scan) on the client app.
2. **Validation & Storage:** The `Nutrition Service` validates caloric and macronutrient values against standard food tables and writes the entry to `PostgreSQL`.
3. **AI Macro Analysis (Optional / Asynchronous):** The `Nutrition Service` calls the `AI Microservice` to compute macro variance against daily targets.
4. **Insights Delivery:** Nutritional suggestions or balance warnings are pushed back to the client interface.

---

## 4.4 Security, Scalability & Integration Considerations

### Security & Compliance (HIPAA / GDPR)
- **Zero-Trust Network Traffic:** All communications (client-to-gateway and service-to-service) enforce TLS 1.3 encryption in transit.
- **Identity & Token Scoping:** Auth0-issued RS256 JWTs are verified at the API Gateway. Claims are mapped to internal role-based access control (RBAC) permissions.
- **Data Encryption at Rest:** Database volumes use AES-256 encryption. Sensitive biometric and health-adjacent database columns in PostgreSQL are protected with application-level envelope encryption.
- **Data Minimisation:** The internal AI microservice receives pseudonymised, synthetic IDs to perform inference, ensuring raw personal identifiable information (PII) is isolated from ML logs.

### Scalability Strategy
- **Independent Horizontal Autoscaling:** Each NestJS microservice and the FastAPI ML service run inside containerized Kubernetes pods with Horizontal Pod Autoscalers (HPA) governed by CPU and request throughput metrics.
- **Decoupled Real-Time Layer:** Redis Pub/Sub decouples WebSocket connection handling from application logic, allowing the real-time gateway to scale to tens of thousands of concurrent client connections without locking database resources.
- **Stateless Services:** All application services remain strictly stateless, storing transient state in Redis.

### Integration Strategy
- **Unified Client Contract:** The API Gateway presents a consolidated OpenAPI / Swagger REST specification to the Flutter team.
- **Internal Communication:** Standard synchronous inter-service requests utilize lightweight HTTP/REST, with high-frequency ML inference pipelines architected to transition to gRPC for microsecond serialization efficiency.
