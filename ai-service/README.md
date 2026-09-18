# FitFlow — AI Service (FastAPI)

> Python/FastAPI microservice for AI-driven workout and nutrition personalisation.

---

## Overview

The AI Service is a standalone Python microservice that provides personalised workout plans, nutrition recommendations, and fitness insights using machine learning models. It is called by the NestJS backend via internal REST/gRPC endpoints and is deployed independently for flexible scaling (including GPU instances when needed).

---

## Tech Stack

| Technology | Purpose |
| :--- | :--- |
| Python 3.11+ | Programming language |
| FastAPI | Async web framework |
| Uvicorn | ASGI server |
| scikit-learn | Classical ML models (clustering, regression) |
| PyTorch | Deep learning models (recommendation engine) |
| Pandas / NumPy | Data processing & feature engineering |
| SQLAlchemy | Database access (read from PostgreSQL) |
| Redis (aioredis) | Caching predictions & model outputs |
| Pydantic | Request/response validation |
| Pytest | Testing framework |

---

## Planned Features

- **Workout Personalisation** — Generate tailored workout plans based on user goals, fitness level, and history
- **Nutrition Recommendations** — Suggest meals and macros based on dietary preferences and calorie targets
- **Progress Prediction** — Forecast fitness milestones using historical workout data
- **Activity Clustering** — Group users by behaviour patterns for community features
- **Anomaly Detection** — Flag unusual activity patterns (e.g., overtraining alerts)

---

## Folder Structure (Planned)

```
ai-service/
├── app/
│   ├── main.py                # FastAPI entry point
│   ├── config.py              # Environment & settings
│   ├── api/
│   │   ├── routes/            # API route handlers
│   │   │   ├── workouts.py
│   │   │   ├── nutrition.py
│   │   │   └── predictions.py
│   │   └── dependencies.py    # Shared dependencies (DB, Redis)
│   ├── models/                # ML model loading & inference
│   │   ├── workout_model.py
│   │   ├── nutrition_model.py
│   │   └── clustering.py
│   ├── schemas/               # Pydantic request/response schemas
│   ├── services/              # Business logic layer
│   └── utils/                 # Helpers & data preprocessing
├── ml/
│   ├── notebooks/             # Jupyter notebooks for experimentation
│   ├── training/              # Model training scripts
│   └── saved_models/          # Serialised model files (.pkl, .pt)
├── tests/                     # Unit & integration tests
├── requirements.txt           # Python dependencies
├── Dockerfile                 # Container build
└── README.md
```

---

## Getting Started

```bash
# Create a virtual environment
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Start the development server
uvicorn app.main:app --reload --port 8000

# Run tests
pytest
```

---

## Environment Variables

Create a `.env` file in the project root:

```env
# Server
PORT=8000
ENV=development

# PostgreSQL (read-only access to main DB)
DATABASE_URL=postgresql://fitflow_readonly:password@localhost:5432/fitflow

# Redis
REDIS_URL=redis://localhost:6379/1

# Model Configuration
MODEL_PATH=./ml/saved_models/
MODEL_VERSION=v1.0
```

---

## API Endpoints (Planned)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| POST | `/api/v1/personalise/workout` | Generate a personalised workout plan |
| POST | `/api/v1/personalise/nutrition` | Generate nutrition recommendations |
| GET | `/api/v1/predictions/{user_id}` | Get progress predictions for a user |
| GET | `/api/v1/health` | Service health check |

API docs will be available at `http://localhost:8000/docs` (Swagger UI).
