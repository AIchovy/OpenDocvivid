 **[中文](./README-CN.md)**  

## OpenDocvivid

OpenDocvivid is a modern, AI‑powered document and video understanding platform.  
It helps you upload content (documents, web pages), process it with large language models, and generate vivid videos.

## Screenshot

![Screenshot](./img/main.png)

### Key Features

- **AI‑assisted content understanding**: Extract, summarize, and analyze information from documents and videos using LLMs.
- **Task‑based processing**: Asynchronous task system for long‑running jobs (e.g. video processing, credit/usage updates).
- **User accounts and subscriptions**: Authentication, subscription management, and credit accounting.
- **Modern web UI**: Next.js/React frontend with a responsive, app‑like experience.
- **Extensible backend**: FastAPI‑based backend (with Celery workers) that can be extended with new routes, tasks, and models.

---

## Tech Stack

### Backend

- **Language**: Python (see `backend/pyproject.toml` and `backend/uv.lock`)
- **Web framework**: FastAPI (exposed via `backend/src/app.py` and `backend/main.py`)
- **Task queue**: Celery (`backend/src/celery_app.py` and `backend/src/tasks/*`)
- **Data models**:
  - `backend/src/models/user_models.py` – user entities
  - `backend/src/models/subscription_models.py` – subscription & plan entities
  - `backend/src/models/task_modes.py` – task‑related configuration
- **Services**:
  - `backend/src/services/user_service.py` – user management
  - `backend/src/services/subscription_service.py` – subscription logic
  - `backend/src/services/credit_service.py` – credit logic
  - `backend/src/services/video_service.py` – video‑related logic
- **APIs / routes** (FastAPI routers):
  - `backend/src/routes/auth.py` – authentication & session APIs
  - `backend/src/routes/credit.py` – credit & billing APIs
  - `backend/src/routes/video.py` – video task APIs
  - `backend/src/routes/system.py`, `backend/src/routes/webhook.py` – system & webhook endpoints
- **Utilities**:
  - `backend/src/clients/llm.py` – LLM client integration
  - `backend/src/clients/redis.py` – Redis client
  - `backend/src/utils/security.py`, `backend/src/utils/middleware.py` – security & middleware helpers
  - `backend/src/libs/postgresql_transactional.py` – PostgreSQL transactional utilities

### Frontend

- **Framework**: Next.js (App Router) in `frontend/app`
- **Language**: TypeScript + React
- **Styling / UI**:
  - Global styles in `frontend/app/globals.css`
  - Reusable UI components in `frontend/components/ui/*`
  - Custom components such as `account-dialog`, `app-sidebar`, `doc-vivid-input`, `explore-content`, `pricing-content`, etc.
- **Client libraries**:
  - API client wrappers in `frontend/lib/api/*`
  - Type definitions in `frontend/lib/types/api.ts`
  - Hooks in `frontend/hooks/*` (e.g., `use-auto-resize-textarea`, `use-mobile`)
- **Auth & API routes**:
  - NextAuth route in `frontend/app/api/auth/[...nextauth]/route.ts`
  - Health check route in `frontend/app/api/health/route.ts`

---

## High‑Level Architecture

### Overview

- **Frontend (Next.js)**:
  - Serves the user interface under `frontend/app`.
  - Uses `frontend/lib/api/*` clients to call backend APIs.
  - Manages sessions and authentication via the NextAuth route.

- **Backend (FastAPI + Celery)**:
  - Core API defined in `backend/src/app.py` and `backend/main.py`.
  - Routes under `backend/src/routes/*` expose functionality for auth, credits, videos, and system utilities.
  - Business logic lives in `backend/src/services/*`.
  - Data models and database interactions live in `backend/src/models/*` and `backend/src/libs/postgresql_transactional.py`.
  - Background and long‑running tasks run via Celery in `backend/src/tasks/*`, using `backend/src/celery_app.py` as the entry point.

- **External Services**:
  - LLM provider(s) accessed via `backend/src/clients/llm.py`.
  - Redis for caching / task coordination via `backend/src/clients/redis.py`.
  - PostgreSQL (or compatible SQL database) for persistence.

---

## Getting Started

### Prerequisites

- Node.js (see `frontend/package.json` for supported version; recommended: latest LTS)
- pnpm (preferred) or npm/yarn
- Python (version as specified in `backend/pyproject.toml`)
- A running PostgreSQL instance
- A running Redis instance

### Backend Setup

From the project root:

```bash
cd backend

# Create and activate a virtual environment (example with venv)
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies (using uv or pip, depending on your setup)
uv sync  # if you use uv
# or
pip install -e .
```

Use environment variables (e.g. `.env` file) to configure:

- **Database connection** (PostgreSQL)
- **Redis connection**
- **LLM provider API keys**
- **Auth / security settings** (JWT secrets, etc.)

Then run the API server (example using uvicorn):

```bash
cd backend
python main.py
```

To run the Celery worker (example):

```bash
cd backend
celery -A src.celery_app worker --beat -l INFO -Q default,generate_task_queue
```

> Note: The exact module path for Celery may differ depending on how `celery_app` is exported; adjust accordingly.

### Frontend Setup

From the project root:

```bash
cd frontend
pnpm install
pnpm dev
```

This starts the Next.js dev server (typically on `http://localhost:3000`).

Ensure the frontend is configured (via environment variables like `NEXT_PUBLIC_API_URL`) to point to the running backend API.

---

## Development Notes

- **Code style & linting**:
  - Frontend linting is configured via `frontend/eslint.config.mjs`.
  - Type checking is configured via `frontend/tsconfig.json`.
  - Follow existing patterns in `frontend/components` and `backend/src/services` when adding new features.

- **Adding new backend features**:
  - Define or extend Pydantic schemas in `backend/src/schemas/*`.
  - Add business logic in a service module under `backend/src/services/*`.
  - Expose new endpoints using a router module under `backend/src/routes/*`.

- **Adding new frontend features**:
  - Create new pages in `frontend/app` (App Router).
  - Reuse / extend components from `frontend/components` and `frontend/components/ui`.
  - Add API client functions under `frontend/lib/api/*` to talk to new backend endpoints.


