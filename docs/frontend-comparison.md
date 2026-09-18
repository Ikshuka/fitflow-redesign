# Activity 1 — Frontend Framework Evaluation

Flutter, React Native, Kotlin Multiplatform (KMP), and Swift/SwiftUI are evaluated below across the criteria specified in the lab sheet, focused on suitability for a fitness application requiring seamless iOS, Android, and web experiences with high performance.

---

## 1.1 Comparison Table

| Criterion | Flutter | React Native | Kotlin Multiplatform (KMP) | Swift / SwiftUI |
| :--- | :--- | :--- | :--- | :--- |
| **Development speed** | **Very high** — single codebase, hot reload, rich built-in widget set | **High** — single codebase, huge community, fast refresh | **Moderate** — shares business logic only; UI built per platform | **Low for cross-platform** — iOS-only UI, fastest for iOS alone |
| **Code reusability** | **~95%+** across iOS, Android, Web, Desktop | **~85–90%** across iOS & Android; Web needs RN-Web | **~40–60%** (business logic only, native UI per platform) | **0%** outside Apple platforms |
| **Performance** | **Near-native** — compiles to native ARM code, dedicated Impeller/Skia renderer | **Near-native** via bridge/JSI; can experience lag on complex animations | **Native** — compiles to native binaries per target platform | **Native** — best possible performance on Apple hardware |
| **Ecosystem maturity** | **Mature**, backed by Google, fast-growing package ecosystem (pub.dev) | **Very mature**, backed by Meta, largest JS ecosystem (npm) | **Growing**, backed by JetBrains, smaller community but improving | **Very mature** for native iOS (Apple-maintained) |
| **Learning curve** | **Moderate** — requires Dart, but features a simple, declarative widget model | **Low** for JavaScript/React developers already on the team | **Moderate-high** — requires Kotlin plus native UI frameworks (SwiftUI / Jetpack Compose) | **Moderate** — Swift is approachable, but strictly iOS/Apple-only |
| **Web compatibility** | **Strong** — first-class Flutter Web compilation target | **Weak-moderate** — separate React-DOM / RN-Web configuration needed | **Weak** — Compose Multiplatform Web remains experimental | **None** — no web target available |
| **AI/ML integration** | **Good** — TFLite, ML Kit, lightweight inference, REST/gRPC to Python services | **Good** — REST/gRPC to Python services, TensorFlow.js in-browser | **Good** — native ML Kit and Core ML access, REST to backend services | **Excellent** — native Core ML and on-device Apple ML APIs |
| **Real-time feature support** | **Strong** — WebSocket, Socket.IO, gRPC streaming, Dart isolates for background work | **Strong** — WebSocket / Socket.IO support with mature libraries | **Strong** — native platform networking (Ktor) | **Strong** — native URLSession, WebSockets, background execution modes |
| **Maintenance cost** | **Low** — one codebase, single cross-functional team | **Low-moderate** — one codebase, occasional bridge-related patch maintenance | **Moderate-high** — shared logic plus two separate native UI codebases | **High for multi-platform** — separate Android team and codebase required |
| **Security** | **Good** — Dart AOT compiled, standard TLS, certificate pinning support | **Good**, but JavaScript bridge introduces an additional attack surface if misconfigured | **Good** — native platform security models apply directly | **Excellent on iOS** — tightest OS-level integration and Keychain security |

---

## 1.2 Recommendation & Justification

### Recommended: Flutter (Single Codebase for iOS, Android, and Web)

**Flutter** is the strongest fit for the FitFlow redesign because it is the only framework offering high code reuse across **iOS, Android, AND Web** from a single codebase, directly satisfying the case study's core requirement of a *"seamless iOS/Android/web experience"*.

#### Key Architectural Justifications:
1. **High-Performance Rendering:** Its near-native rendering engine (**Impeller / Skia**) guarantees smooth, 60/120 FPS high-frame-rate animations essential for real-time workout tracking interfaces (e.g., live rep counters, interactive exercise timers, live heart-rate charts) that can stutter on bridge-reliant frameworks.
2. **AI/ML Workload Distribution:** Personalisation features are consumed via asynchronous backend API calls to a dedicated AI microservice. Flutter handles this seamlessly, while still enabling on-device inference via **TensorFlow Lite (TFLite)** for offline workout form scoring and local telemetry analysis.
3. **Pragmatic Hybrid Approach:** If FitFlow later requires deep Apple ecosystem integrations (such as **iOS Live Activities, Dynamic Island widgets, or watchOS complications**), a thin native Swift module can be embedded cleanly via Flutter **Platform Channels** without necessitating a complete rewrite.
4. **Evaluation of Alternatives:**
   - **React Native** is a viable runner-up, particularly if existing engineering staff have extensive JavaScript/React experience. However, its comparatively weaker first-party web story and reliance on community bridge libraries for complex native hardware hooks make Flutter a safer long-term choice.
   - **Kotlin Multiplatform (KMP)** and **Swift/SwiftUI** are not recommended as the primary approach: KMP still necessitates building and maintaining separate UI layers (Jetpack Compose + SwiftUI), doubling UI development effort. Swift/SwiftUI cannot deploy to Android or Web, forcing disjointed codebases and siloed development teams.
