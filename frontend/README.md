# FitFlow — Frontend (Flutter)

> Cross-platform client application for iOS, Android, and Web built with Flutter & Dart.

---

## Overview

The FitFlow frontend is a single Flutter codebase that delivers a consistent, high-performance user experience across iOS, Android, and the web. It communicates with the NestJS backend via REST APIs and Socket.IO for real-time features.

---

## Tech Stack

| Technology | Purpose |
| :--- | :--- |
| Flutter 3.x | UI framework (iOS, Android, Web) |
| Dart | Programming language |
| Riverpod / Bloc | State management |
| GoRouter | Navigation & deep linking |
| Dio | HTTP client for REST API calls |
| Socket.IO Client | Real-time workout & social features |
| Flutter Secure Storage | Secure token storage (Auth0 JWT) |
| Google Fonts | Typography (Inter / Outfit) |

---

## Planned Features

- **Authentication** — Login, registration, and social sign-in via Auth0
- **Workout Tracking** — Real-time exercise logging with live progress updates
- **AI Personalisation** — Personalised workout and nutrition plans from the AI service
- **Social Feed** — Activity feed, friend challenges, and leaderboards
- **Nutrition Logging** — Meal tracking with macro/calorie breakdowns
- **Profile & Settings** — User profile management and app preferences
- **Push Notifications** — Workout reminders and social activity alerts

---

## Folder Structure (Planned)

```
frontend/
├── lib/
│   ├── main.dart              # App entry point
│   ├── config/                # Environment & theme configuration
│   ├── models/                # Data models / DTOs
│   ├── providers/             # State management (Riverpod/Bloc)
│   ├── screens/               # Screen-level widgets
│   │   ├── auth/
│   │   ├── home/
│   │   ├── workout/
│   │   ├── social/
│   │   └── nutrition/
│   ├── services/              # API clients & Socket.IO service
│   ├── utils/                 # Helpers & constants
│   └── widgets/               # Shared reusable widgets
├── assets/                    # Images, fonts, animations
├── test/                      # Unit & widget tests
├── pubspec.yaml               # Dependencies
└── README.md
```

---

## Getting Started

```bash
# Install dependencies
flutter pub get

# Run on a connected device or emulator
flutter run

# Run on web
flutter run -d chrome

# Run tests
flutter test
```

---

## Environment Variables

Create a `.env` file in the project root:

```env
API_BASE_URL=http://localhost:3000/api
AUTH0_DOMAIN=your-auth0-domain.auth0.com
AUTH0_CLIENT_ID=your-client-id
```
