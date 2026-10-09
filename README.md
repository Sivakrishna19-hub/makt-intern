# 🎬 SIVACINE AI — Generative Storytelling & Cinematic Video Studio

A full-stack, enterprise-grade Generative AI Storytelling & Video Production platform. SIVACINE AI converts natural language story prompts into structured cinematic scenes, character dialogues, multi-voice synthesized narrations, and exports compliant scene packages for **LTX-2.5 AI Video Generators**.

---

## 🌟 Key Features

- **🎨 Cinematic Studio Frontend**: High-performance dark-mode UI with glassmorphism, responsive scene cards, real-time waveform audio preview, and duration balancing.
- **🤖 Structured Story Synthesis**: Gemini 2.5 Flash integration orchestrating cinematic narratives with structured scene breakdowns, visual director prompts, and character dialogues.
- **🎙️ Multi-Engine TTS Pipeline**: Synthesizes character voices and narrations with Edge-TTS, Kokoro TTS, and offline fallbacks.
- **🎥 LTX-2.5 Handoff Schema**: Generates clean, zero-dependency JSON handoff contracts with synchronized audio paths for video rendering pipelines.
- **🔐 Multi-Provider Authentication**:
  - **FastAPI Backend (`backend_py/`)**: JWT tokens, Argon2id password hashing, PostgreSQL / SQLite with SQLAlchemy & Alembic.
  - **Node.js Backend (`backend/`)**: Google & GitHub OAuth 2.0 with CSRF state protection and MySQL persistence.

---

## 📁 Repository Structure

```
.
├── index.html                   # SIVACINE AI Studio Web Interface
├── style.css                    # Dark-mode cinematic design system
├── app.js                       # Frontend studio engine & API client
├── serve-client.js              # Lightweight frontend server (Port 3000)
├── init_postgres.sql            # PostgreSQL database initialization script
├── .gitignore                   # Repository ignore rules (secrets & builds)
├── backend_py/                  # Python FastAPI Backend (Port 8000)
│   ├── app/
│   │   ├── config.py            # Pydantic settings (DB, Gemini, TTS, Output Root)
│   │   ├── database.py          # SQLAlchemy engine & session management
│   │   ├── main.py              # FastAPI application entrypoint & CORS
│   │   ├── security.py          # Argon2id hashing & JWT token handling
│   │   ├── models/              # SQLAlchemy models (User, Project, Story, Scene, Job)
│   │   ├── schemas/             # Pydantic request/response schemas
│   │   ├── routes/              # API endpoints (Auth, Health, Projects, Jobs)
│   │   └── services/            # Gemini story synthesis & TTS pipeline
│   ├── alembic/                 # Database migrations
│   ├── alembic.ini              # Alembic configuration
│   ├── requirements.txt         # Python dependencies
│   ├── .env.example             # Python environment template
│   ├── README.md                # Python backend documentation
│   ├── test_api_auth.py         # Authentication verification suite
│   └── test_story_tts_suite.py  # Story generation & TTS verification suite
└── backend/                     # Node.js Express OAuth Backend (Port 5000)
    ├── server.js                # Express OAuth 2.0 server (Google & GitHub)
    ├── database.js              # MySQL connection pool & user management
    ├── package.json             # Node.js dependencies
    ├── .env.example             # Node.js environment template
    ├── README.md                # Node.js OAuth backend documentation
    └── test-oauth.js            # OAuth test suite
```

---

## 🚀 Quick Start Guide

### 1. Prerequisites

- **Python**: 3.10+
- **Node.js**: 18+
- **PostgreSQL** or **SQLite** (for Python FastAPI backend)
- **MySQL** (optional, for Node.js OAuth backend)

---

### 2. Frontend Setup

Run the lightweight client server on port `3000`:

```bash
node serve-client.js
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

### 3. Python FastAPI Storytelling Backend Setup

```bash
# Navigate to python backend
cd backend_py

# Create & activate virtual environment
python -m venv .venv
# On Windows:
.venv\Scripts\activate
# On Linux/macOS:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Edit .env and supply GEMINI_API_KEY and DATABASE_URL

# Run database migrations
alembic upgrade head

# Start FastAPI server (Port 8000)
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

---

### 4. Node.js OAuth & MySQL Backend Setup (Optional)

```bash
# Navigate to Node.js backend
cd backend

# Install dependencies
npm install

# Configure environment variables
cp .env.example .env
# Add GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET, etc.

# Start Express server (Port 5000)
node server.js
```

---

## 🧪 Running Test Suites

### Python Backend Tests:
```bash
cd backend_py
python test_story_tts_suite.py
python test_api_auth.py
```

### Node.js Backend Tests:
```bash
cd backend
node test-oauth.js
```

---

## 📡 API Contract & LTX-2.5 Video Handoff

When a story is generated and narrated, the system generates an exportable JSON payload adhering to the **LTX-2.5 Video Generation Handoff Schema**:

```json
{
  "schema_version": "1.0.0",
  "project_id": "6e168fd4-e981-41cb-92f6-5c2a367b6c69",
  "story_id": "5efb7187-f805-4f4c-b02e-2c7cdb6485b0",
  "title": "The Mars Transmission",
  "language": "en",
  "genre": "science_fiction",
  "target_duration_seconds": 60,
  "visual_style": "cinematic realism",
  "scenes": [
    {
      "scene_id": "1f4912a9-725f-4acb-a695-9b4e6fa40ae9",
      "scene_number": 1,
      "duration_seconds": 15,
      "visual_prompt": "Cinematic wide 8k drone shot of a solitary astronaut in an illuminated EVA suit walking across desolate red sand dunes on Mars...",
      "narration": "Commander Arun had spent eighty sols searching the Martian craters in complete isolation.",
      "dialogue": [
        {
          "character": "Arun",
          "text": "Base, telemetry sensors are picking up harmonic frequencies from sector 4.",
          "voice_id": "arun"
        }
      ],
      "visual_style": "cinematic realism",
      "status": "audio_generated",
      "audio_path": "outputs/6e168fd4-e981-41cb-92f6-5c2a367b6c69/5efb7187-f805-4f4c-b02e-2c7cdb6485b0/audio/1f4912a9-725f-4acb-a695-9b4e6fa40ae9.wav"
    }
  ]
}
```

---

## 🛡️ Security & Quality

- **Argon2id & JWT Authentication** with token expiry and role checks.
- **CSRF Protection** via cryptographically random state tokens for OAuth flows.
- **Parameterized SQL Queries** preventing SQL injection attacks.
- **Environment Isolation**: `.env` files are strictly excluded from version control.

---

## 📄 License

MIT License. Designed & Developed for the AI Video Generation & Storytelling Studio.
