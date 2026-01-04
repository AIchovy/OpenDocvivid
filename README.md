[中文](./README-CN.md) | English

## OpenDocvivid

OpenDocvivid is a modern, AI-powered platform that turns documents and web pages into videos.  
It focuses on a smooth authoring workflow, a modern web UI, and an extensible backend for custom video pipelines.

## Screenshot

![Screenshot](./img/main.png)

## ✨ Features

- **AI video generation**: Generate videos from documents, files, and URLs by processing content with large language models.
- **Task-based processing**: Asynchronous, reliable task system for long-running jobs such as video rendering and credit/usage updates.
- **Accounts & subscriptions**: Built-in authentication, subscription plans, and credit accounting.
- **Modern web UI**: Next.js/React frontend with a responsive, app-like experience.
- **Extensible backend**: FastAPI + Celery architecture that can be extended with new routes, tasks, and models.

---

## 🧱 Tech Stack

- **Backend**: Python, FastAPI, Celery, PostgreSQL, Redis, LLM providers  
- **Frontend**: Next.js (App Router), TypeScript, modern component-based UI

---

## 🚀 Getting Started

### Backend

```bash
cd backend

# Create and activate a virtual environment (example with venv)
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
uv sync  # or: pip install -e .

# Run API server
python main.py
```

Configure environment variables (e.g. via `.env`) for:

- **PostgreSQL** and **Redis** connections
- **LLM provider** API keys
- **Auth/security** settings (JWT secrets, etc.)

### Frontend

```bash
cd frontend
pnpm install
pnpm dev
```

The Next.js dev server will typically run on `http://localhost:3000`.  
Set `NEXT_PUBLIC_API_URL` (and related env vars) to point to the running backend API.

---

## 📄 License

This project is Licensed under [Apache License, Version 2.0](./LICENSE).