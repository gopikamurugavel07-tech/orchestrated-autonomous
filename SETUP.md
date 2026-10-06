# Cyber Reasoning System (CRS) Platform Setup Guide

## System Overview

The **Cyber Reasoning System (CRS)** is an autonomous defense and vulnerability analysis platform that integrates:
- File & Artifact Ingestion (PDF, DOCX, C/C++, Python, Java, PCAP, Logs, ZIP, etc.)
- Target Security URL Analysis
- Multi-Agent Orchestration Engine (Task DAG Execution)
- Static Security Analysis & AST Verification
- Network Telemetry & Attack Detection (DoS, MitM, Brute-Force)
- Evidence-Linked AI Triage & Reasoning
- Sandboxed PoV & Patch Verification
- Executive & Technical Incident Reporting

---

## 1. Requirements

- **Python**: Version 3.10+ (Tested on Python 3.13)
- **Node.js**: Version 18+ & npm/pnpm
- **Operating System**: Windows, Linux, or macOS
- **Optional**: Docker & Docker Compose (for containerized sandboxing)

---

## 2. Environment Configuration

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

### Key Environment Variables

| Variable | Description | Default |
|---|---|---|
| `PROJECT_NAME` | Platform Title | Cyber Reasoning System (CRS) |
| `ENVIRONMENT` | Deployment Environment | development |
| `MOCK_MODE` | Standalone local research mode | `true` |
| `DATABASE_URL` | PostgreSQL or SQLite URL | `sqlite+aiosqlite:///:memory:` |
| `LLM_PROVIDER` | LLM Provider (`mock`, `openai`, `ollama`) | `mock` |
| `OPENAI_API_KEY` | OpenAI API Key (optional) | `""` |
| `OLLAMA_URL` | Ollama Server URL | `http://localhost:11434` |

---

## 3. Quick Start (Local Development)

### Backend Setup (FastAPI)

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Activate Virtual Environment:
   - **Windows (PowerShell)**:
     ```powershell
     .\venv\Scripts\Activate.ps1
     ```
   - **Linux / macOS**:
     ```bash
     source venv/bin/activate
     ```
3. Install Dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Start Backend Server:
   ```bash
   uvicorn app.main:app --reload --port 8000
   ```

- **Backend API Base**: [http://localhost:8000](http://localhost:8000)
- **Interactive Swagger Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Unified Web Dashboard**: [http://localhost:8000/dashboard](http://localhost:8000/dashboard)

### Frontend Setup (React + Vite + Tailwind)

1. Open a second terminal and navigate to the frontend directory:
   ```bash
   cd frontend
   ```
2. Install Node dependencies:
   ```bash
   npm install
   ```
3. Start Vite Development Server:
   ```bash
   npm run dev
   ```

- **Frontend SOC Dashboard**: [http://localhost:3000](http://localhost:3000)

---

## 4. Running via Docker Compose

```bash
docker compose up --build
```

Access services:
- Frontend: [http://localhost:3000](http://localhost:3000)
- Backend API: [http://localhost:8000](http://localhost:8000)

---

## 5. Running Automated Tests

```bash
cd backend
python -m pytest tests/
```

Expected output:
```
tests/test_artifacts.py PASSED
tests/test_health.py PASSED
tests/test_multi_agent.py PASSED
```

---

## 6. API Endpoint Reference

- `GET /api/v1/health` - Health check & active engine telemetry
- `POST /api/v1/artifacts/upload` - File artifact ingestion & pipeline execution
- `POST /api/v1/artifacts/url` - Target URL security assessment
- `GET /api/v1/artifacts` - List ingested artifacts
- `GET /api/v1/analyses/{artifact_id}` - Retrieve complete analysis & findings
- `GET /api/v1/analyses/{artifact_id}/report` - Export security incident report
- `GET /api/v1/orchestration/{analysis_id}/tasks` - Inspect multi-agent task DAG
- `WS /api/v1/ws/orchestration/{analysis_id}` - Real-time task progress WebSocket
