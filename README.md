# Cyber Reasoning System (CRS) Platform

A modular, containerized research-grade **Cyber Reasoning System (CRS)** combining network attack simulation, software vulnerability discovery, AI reasoning, automated verification, patch validation, and SOC monitoring dashboard.

---

## 🏗️ System Architecture Overview

```
                ┌───────────────────────────────┐
                │        DATA SOURCES           │
                ├───────────────────────────────┤
                │ Network Attack Dataset        │
                │ CRSBench Vulnerabilities      │
                │ Cybersecurity Reasoning Data  │
                │ Kimi Cyber Reasoning Data     │
                └──────────────┬────────────────┘
                               │
                               ▼
                ┌───────────────────────────────┐
                │       INGESTION LAYER         │
                │ PCAP / CSV / JSON / Binary    │
                └──────────────┬────────────────┘
                               │
             ┌─────────────────┴─────────────────┐
             ▼                                   ▼
   ┌────────────────────┐              ┌────────────────────┐
   │ NETWORK ANALYSIS   │              │ SOFTWARE ANALYSIS  │
   │ Traffic Analysis   │              │ Fuzzing & Static   │
   └─────────┬──────────┘              └─────────┬──────────┘
             │                                   │
             └─────────────────┬─────────────────┘
                               ▼
                ┌───────────────────────────────┐
                │       REASONING ENGINE        │
                │ LLM Triage & Hypothesis       │
                └──────────────┬────────────────┘
                               │
                               ▼
                ┌───────────────────────────────┐
                │       VERIFICATION LAYER      │
                │ Sandboxed PoV & Patch Test    │
                └──────────────┬────────────────┘
                               │
                               ▼
                ┌───────────────────────────────┐
                │        WEB DASHBOARD          │
                └───────────────────────────────┘
```

---

## 🚀 Quickstart & Installation

### Option 1: Run via Docker Compose (Recommended)

1. **Clone & Configure**:
   ```bash
   cp .env.example .env
   ```

2. **Launch Container Pipeline**:
   ```bash
   docker compose up --build
   ```

3. **Access Services**:
   - **Frontend SOC Dashboard**: [http://localhost:3000](http://localhost:3000)
   - **Backend REST API**: [http://localhost:8000](http://localhost:8000)
   - **Interactive API Documentation (Swagger)**: [http://localhost:8000/docs](http://localhost:8000/docs)

---

### Option 2: Local Development Setup

#### Backend (FastAPI)
```bash
cd backend
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# Install requirements:
pip install -r requirements.txt
# Run local dev server:
uvicorn app.main:app --reload --port 8000
```

#### Frontend (React + Vite + Tailwind)
```bash
cd frontend
npm install
npm run dev
```

---

## 🧪 Testing

Run automated unit and integration tests across the backend pipeline:

```bash
cd backend
python -m pytest tests/
```

---

## 🔒 Safety & Isolation Directive
This system is strictly designed for **authorized research, controlled simulation, and defensive cyber analysis**. All network simulation, PoV validation, and patch testing operate exclusively within sandboxed local Docker container environments.
