Markdown
# Hybrid E-Commerce & AI - Backend Core

High-performance, decoupled REST API built with **FastAPI** and **Supabase (PostgreSQL)**. This service powers a hybrid e-commerce engine, managing catalog operations with dynamic JSONB technical specifications, specialized service bookings, strict payload validation, and an AI-driven shopping assistant interface.

---

## 🏗 Architecture & Design Decisions

- **Decoupled Architecture (Polyrepo):** Completely separated from the frontend client (`hybrid-ecommerce-ai-web`) to enable independent deployment cycles, isolated CI/CD pipelines, and clean domain boundaries.
- **ASGI Web Server (Uvicorn):** Utilizes Uvicorn as an asynchronous server to handle concurrent network connections and route non-blocking I/O operations directly to FastAPI.
- **Strict Data Validation (Pydantic v2):** Every incoming payload and outgoing response is validated against strict Data Transfer Objects (DTOs) to eliminate malformed data at the API boundary.
- **Dynamic Database Layer (Supabase / PostgreSQL):** Leverages PostgreSQL `JSONB` data types to handle heterogeneous product attributes (e.g., audio IEM specifications vs. smartphone replacement parts) within a single unified catalog schema.
- **Quality Assurance & Testing (Pytest):** Built-in automated testing suite covering unit validation logic and integration HTTP contracts.

---

## 🛠 Tech Stack

| Technology | Role / Purpose |
| :--- | :--- |
| **Python 3.10+** | Core programming language |
| **FastAPI** | Modern asynchronous Web framework for API routing |
| **Uvicorn** | High-performance ASGI server implementation |
| **Supabase (Python SDK)** | Database interaction (PostgreSQL) and Row Level Security (RLS) |
| **Pydantic / Pydantic-Settings** | Data validation, serialization, and typed environment management |
| **Pytest & HTTPX** | Unit testing, integration testing, and async HTTP clients |

---

## 📂 Project Directory Structure

```text
hybrid-ecommerce-ai-api/
├── app/
│   ├── api/
│   │   └── v1/
│   │       ├── endpoints/
│   │       │   ├── products.py      # Catalog & stock management endpoints
│   │       │   ├── services.py      # Technical repair & service endpoints
│   │       │   └── ai_agent.py      # AI assistant processing & prompt boundaries
│   │       └── router.py            # API v1 central router
│   ├── core/
│   │   ├── config.py                # Environment settings via Pydantic
│   │   └── database.py              # Supabase client instantiation
│   ├── middlewares/
│   │   ├── cors.py                  # Cross-Origin Resource Sharing policy for Angular
│   │   └── exceptions.py            # Global HTTP exception handlers & JSON formatting
│   ├── schemas/
│   │   └── payloads.py              # Pydantic DTOs for request/response contracts
│   ├── services/
│   │   ├── ai_service.py            # AI business logic & hallucination prevention
│   │   └── db_service.py            # Database queries to Supabase
│   └── main.py                      # FastAPI app initialization & middleware mounting
├── tests/
│   ├── unit/                        # Pydantic schema and service logic tests
│   └── integration/                 # API endpoint integration tests
├── .env.example                     # Environment variables template
├── .gitignore                       # Python-specific ignore rules
├── Dockerfile                       # Containerized production deployment
├── requirements.txt                 # Frozen dependency tree
└── README.md                        # Technical documentation

🚀 Getting Started

Prerequisites
Python 3.10 or higher installed.

Git configured.

Local Setup & Execution
Clone the repository:

Bash
git clone [https://github.com/s-rengifo-dev/hybrid-ecommerce-ai-api.git](https://github.com/s-rengifo-dev/hybrid-ecommerce-ai-api.git)
cd hybrid-ecommerce-ai-api
Create and activate a virtual environment:

Bash
# Linux / macOS
python3 -m venv venv
source venv/bin/activate

# Windows (PowerShell)
python -m venv venv
.\venv\Scripts\Activate.ps1
Install dependencies:

Bash
pip install -r requirements.txt
Environment Variables Configuration:
Create a .env file in the root directory following the .env.example template:

Fragmento de código
SUPABASE_URL=[https://your-supabase-project.supabase.co](https://your-supabase-project.supabase.co)
SUPABASE_KEY=your-supabase-anon-key
ALLOWED_ORIGINS=http://localhost:4200
Start the Development Server:

Bash
uvicorn app.main:app --reload
The API will be accessible at http://127.0.0.1:8000.

🧪 Quality Assurance & Test Execution
Run the full automated test suite using Pytest:

Bash
# Run all tests with verbose output
pytest -v

# Run unit tests only
pytest tests/unit/ -v

# Run integration tests only
pytest tests/integration/ -v
📖 API Documentation
FastAPI automatically generates interactive OpenAPI documentation. Once the application is running, access:

Swagger UI: http://127.0.0.1:8000/docs

ReDoc: http://127.0.0.1:8000/redoc


---

### Siguiente Paso Obligatorio

1. Guarda este archivo como `README.md`.
2. Asegúrate de tener creados los archivos `.gitignore` y `requirements.txt` en la raíz.
3. Ejecuta los comandos de inicialización de Git para tu primer commit formal:

```bash
git init
git add .
git commit -m "chore(core): initialize backend architecture and project structure"
git branch -M main
git remote add origin https://github.com/s-rengifo-dev/hybrid-ecommerce-ai-api.git
git push -u origin main