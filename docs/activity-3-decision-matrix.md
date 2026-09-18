# Activity 3 — Technology Comparison Matrix

Findings from Activities 1 and 2 are consolidated below into a rigorous weighted decision matrix. Each candidate technology is evaluated on a scale of **1 to 5** per criterion (where 5 represents the optimal fit for FitFlow), and criteria are weighted according to FitFlow's operational priorities.

$$\text{Weighted Score} = \sum (\text{Raw Score} \times \text{Weight})$$

---

## 3.1 Criterion Weights

| Criterion | Weight | Rationale |
| :--- | :---: | :--- |
| **Performance** | 20% | High-framerate real-time workout tracking and responsive UI are critical to user retention |
| **Security & Compliance** | 20% | Handling sensitive health-adjacent telemetry demands HIPAA/GDPR alignment and encryption |
| **Scalability** | 15% | Architecture must absorb anticipated user growth without necessitating structural rewrites |
| **AI/ML Support** | 15% | Dynamic personalisation is a headline differentiating feature for FitFlow |
| **Development Speed** | 10% | A mid-sized engineering team requires high velocity to ship market-ready features |
| **Cost** | 10% | Cloud operational and licensing overhead must remain sustainable for a growing startup |
| **Maintainability** | 10% | Long-term codebase cleanliness, modularity, and ease of engineering hiring |
| **Total** | **100%** | |

---

## 3.2 Frontend Decision Matrix

| Criterion (Weight) | Flutter | React Native | Kotlin Multiplatform (KMP) | Swift / SwiftUI |
| :--- | :---: | :---: | :---: | :---: |
| **Performance (20%)** | 4.5 (0.90) | 4.0 (0.80) | 4.5 (0.90) | 5.0 (1.00) |
| **Scalability (15%)** | 4.0 (0.60) | 4.0 (0.60) | 3.5 (0.53) | 3.0 (0.45) |
| **Development Speed (10%)** | 5.0 (0.50) | 4.5 (0.45) | 3.0 (0.30) | 2.0 (0.20) |
| **Security & Compliance (20%)** | 4.0 (0.80) | 3.5 (0.70) | 4.5 (0.90) | 5.0 (1.00) |
| **Cost (10%)** | 4.5 (0.45) | 4.5 (0.45) | 3.0 (0.30) | 2.0 (0.20) |
| **AI/ML Support (15%)** | 4.0 (0.60) | 4.0 (0.60) | 4.0 (0.60) | 4.5 (0.68) |
| **Maintainability (10%)** | 4.5 (0.45) | 4.0 (0.40) | 3.0 (0.30) | 2.0 (0.20) |
| **Weighted Total** | **4.30** | **4.00** | **3.83** | **3.73** |

*Winner:* **Flutter (4.30)** — Outscores alternatives by combining high development velocity with high code reusability across iOS, Android, and Web without compromising UI animation performance.

---

## 3.3 Backend Decision Matrix

| Criterion (Weight) | NestJS (Node.js) | FastAPI (Python) | Go |
| :--- | :---: | :---: | :---: |
| **Performance (20%)** | 4.0 (0.80) | 4.0 (0.80) | 5.0 (1.00) |
| **Scalability (15%)** | 4.0 (0.60) | 4.0 (0.60) | 5.0 (0.75) |
| **Development Speed (10%)** | 4.5 (0.45) | 4.5 (0.45) | 3.5 (0.35) |
| **Security & Compliance (20%)** | 4.0 (0.80) | 4.0 (0.80) | 3.5 (0.70) |
| **Cost (10%)** | 4.0 (0.40) | 4.0 (0.40) | 4.5 (0.45) |
| **AI/ML Support (15%)** | 3.0 (0.45) | 5.0 (0.75) | 3.0 (0.45) |
| **Maintainability (10%)** | 4.5 (0.45) | 4.0 (0.40) | 3.5 (0.35) |
| **Weighted Total** | **3.95** | **4.20** | **4.05** |

> **Architectural Note:** While FastAPI achieved the highest standalone score (4.20) due to its unrivaled AI/ML integration capabilities, NestJS remains the superior choice for core domain microservices and real-time WebSocket orchestration due to TypeScript end-to-end synergy and structured enterprise patterns. The architecture therefore strategically implements **both**: NestJS serves as the primary gateway and business backend, while FastAPI powers the dedicated AI personalisation microservice.

---

## 3.4 Database & Auth Decision Matrix

| Criterion (Weight) | PostgreSQL (Relational) | MongoDB (Document) | Auth0 (Identity) |
| :--- | :---: | :---: | :---: |
| **Performance (20%)** | 4.5 (0.90) | 4.0 (0.80) | 4.5 (0.90) |
| **Scalability (15%)** | 3.5 (0.53) | 4.5 (0.68) | 5.0 (0.75) |
| **Development Speed (10%)** | 4.0 (0.40) | 4.5 (0.45) | 4.5 (0.45) |
| **Security & Compliance (20%)** | 5.0 (1.00) | 3.5 (0.70) | 5.0 (1.00) |
| **Cost (10%)** | 4.0 (0.40) | 4.0 (0.40) | 3.5 (0.35) |
| **AI/ML Support (15%)** | 4.0 (0.60) | 3.5 (0.53) | 3.0 (0.45) |
| **Maintainability (10%)** | 4.0 (0.40) | 4.0 (0.40) | 4.5 (0.45) |
| **Weighted Total** | **4.23** | **3.96** | **4.35** |

---

## 3.5 Final Recommended Technology Stack

| Layer | Component | Chosen Technology | Weighted Score | Primary Rationale |
| :--- | :--- | :--- | :---: | :--- |
| **Client Frontend** | Cross-platform Application | **Flutter** (iOS, Android, Web) | **4.30** | Unified codebase, 120 FPS Impeller rendering, ~95% code reusability |
| **Core Backend** | Microservices & API Gateway | **NestJS** (TypeScript) | **3.95** | Modular DI structure, native WebSocket gateways, TypeScript type safety |
| **AI / ML Service** | Personalisation Engine | **FastAPI** (Python) | **4.20** | Direct integration with PyTorch/scikit-learn, async execution |
| **Primary Database** | System of Record | **PostgreSQL** | **4.23** | ACID compliance, robust relation modeling for sensitive health metrics |
| **Secondary Database** | Social Feed & Audit Logs | **MongoDB** | **3.96** | Flexible JSON document schema for high-velocity social events |
| **Identity & Auth** | Authentication & RBAC | **Auth0** | **4.35** | Turnkey HIPAA/GDPR compliance, enterprise MFA, social login integrations |
| **Cache & Real-Time** | Message Broker & Caching | **Redis + Socket.IO** | — | Sub-millisecond session caching and real-time WebSocket pub/sub |
| **Object Storage** | Media Assets | **Amazon S3** | — | Scalable storage for workout videos, progress images, and profile media |
