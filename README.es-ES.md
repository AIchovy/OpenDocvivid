

[中文](./README-CN.md) | Español

## OpenDocvivid

OpenDocvivid es una plataforma moderna impulsada por IA que convierte documentos y páginas web en videos.  
Se centra en un flujo de trabajo de creación ágil, una interfaz web moderna y un backend extensible para flujos de video personalizados.

## Captura de pantalla

![Captura de pantalla](./img/main.png)

## ✨ Características

- **Generación de video con IA**: Genera videos a partir de documentos, archivos y URLs procesando el contenido con modelos de lenguaje grandes.
- **Procesamiento basado en tareas**: Sistema de tareas asíncrono y confiable para trabajos de larga duración, como la renderización de videos y la actualización de créditos/uso.
- **Cuentas y suscripciones**: Autenticación integrada, planes de suscripción y control de créditos.
- **Interfaz web moderna**: Frontend en Next.js/React con una experiencia responsiva y similar a una aplicación.
- **Backend extensible**: Arquitectura FastAPI + Celery que puede ampliarse con nuevas rutas, tareas y modelos.

---

## 🧱 Tecnologías

- **Backend**: Python, FastAPI, Celery, PostgreSQL, Redis, proveedores de LLM  
- **Frontend**: Next.js (App Router), TypeScript, interfaz moderna basada en componentes

---

## 🚀 Primeros pasos

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

Configura las variables de entorno (por ejemplo, mediante `.env`) para:

- Conexiones de **PostgreSQL** y **Redis**
- Claves API del **proveedor de LLM**
- Configuraciones de **autenticación/seguridad** (secretos JWT, etc.)

### Frontend

```bash
cd frontend
pnpm install
pnpm dev
```

El servidor de desarrollo de Next.js normalmente se ejecutará en `http://localhost:3000`.  
Establece `NEXT_PUBLIC_API_URL` (y las variables de entorno relacionadas) para que apunten a la API del backend en ejecución.

---

## 📄 Licencia

Este proyecto está licenciado bajo la [Licencia Apache, Versión 2.0](./LICENSE).
