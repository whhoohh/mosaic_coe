# MosaicX Platform

A unified, AI-native platform for MSMEs, academia, and grassroots businesses — democratizing AI scaling through an open-source Compute Center of Excellence (CoE) and low-code/no-code AI environment.

---

## 🚀 Project Overview

MosaicX is a modular, extensible platform designed to onboard users of all backgrounds (from hobby learners to professional B2B teams and farmers) into the world of AI, automation, and data-driven workflows. It features persona-driven onboarding, dynamic dashboard routing, and a Build Studio that aggregates and manages AI credits and integrations.

---

## 🧩 Key Features

- **Persona-Based Onboarding**
  - On first login, users are guided through a modal onboarding flow.
  - Persona detection (Hobby Learner, Developer, Project Manager, Farmer, Admin) via a short survey.
  - User profile and persona stored in Supabase/Postgres.
  - Backend FastAPI endpoint `/api/onboarding/analyze-persona` determines persona and dashboard routing.

- **Persona Routing**
  - Users are redirected to dashboards tailored to their persona:
    - Hobby Learner → Build Studio
    - Developer/Professional → StudioX Dashboard
    - Project Manager → StudioX Dashboard
    - Farmer → My Farm
    - Admin → Admin Panel

- **Build Studio with AI Credits Aggregation**
  - "My AI Credits" dashboard section displays status of all connected AI/infra providers:
    - Supabase, Lovable, Cursor, LangChain, Gemini AI Studio, ElevenLabs, MinIO, Docker
  - Connect, activate, and redeem credits via unified UI and API.
  - Backend endpoints under `/api/credits/` manage provider connections and credit usage.

- **No-Code & Pro User Flows**
  - No-code drag/drop, prompt-based, and API-first interaction styles supported.
  - Local AI Cluster or solo compute onboarding options.

- **Extensible Architecture**
  - Modular monorepo: React frontend, FastAPI backend, Supabase/Postgres, Docker, LangChain, Redis, MinIO, and more.
  - SDK for credits management and integration.

---

## 🛠 Tech Stack

- **Frontend:** React (Vite), TypeScript, TailwindCSS
- **Backend:** FastAPI (Python)
- **Database:** Supabase/Postgres
- **AI/Infra:** LangChain, MinIO, Redis, Docker, Gemini AI Studio, ElevenLabs, Cursor, Lovable
- **DevOps:** Docker Compose
- **SDK:** TypeScript client for credits and persona APIs

---

## 🧑‍💻 Getting Started

### Prerequisites

- Docker & Docker Compose
- Node.js (v18+ recommended)
- Python 3.9+
- Supabase/Postgres (auto-provisioned via Docker)

### Quick Start

```bash
# Clone the repo
git clone https://github.com/whhoohh/MosaicX-platform.git
cd MosaicX-platform

# Start full stack (API, DB, Frontend, etc.)
docker compose up --build
```

- Frontend: http://localhost:3000
- API: http://localhost:8000
- Supabase: http://localhost:54321 (default)
- Open the app in your browser to trigger onboarding.

### Development

- Frontend (React):  
  ```bash
  cd mosaicx/apps/web
  npm install
  npm run dev
  ```
- Backend (FastAPI):  
  ```bash
  cd mosaicx/apps/api
  pip install -r requirements.txt
  uvicorn app.main:app --reload
  ```

---

## 📝 Persona Onboarding Flow

- On first login, `OnboardingModal` is shown (see `src/pages/OnboardingModal.tsx`).
- User answers 4–6 questions about their background, goals, and preferences.
- Answers are stored in `user_profiles` table (see `infra/migrations.sql`).
- Backend endpoint `/api/onboarding/analyze-persona` returns persona and redirect URL.

**Sample cURL:**
```bash
curl -X POST localhost:8000/api/onboarding/analyze-persona \
  -H "Content-Type: application/json" \
  -d '{"answers":["Hobby Learner","I want to explore AI","No-code","Need credits"]}'
```

**Sample Response:**
```json
{ "persona": "b2c_hobby", "redirect": "/build-studio" }
```

---

## 🏗️ Build Studio & Credits Integration

- Build Studio dashboard (`/build-studio`) shows "My AI Credits" grid.
- Each card displays the status of a provider (Connected, Activate Trial, Linked, etc.).
- Connect or redeem credits via `/api/credits/connect/<provider>` and `/api/credits/redeem/<provider>`.
- Status endpoint: `/api/credits/status`

**Sample cURL:**
```bash
curl localhost:8000/api/credits/status
```

---

## 🗂️ API Endpoints

### Onboarding

- `POST /api/onboarding/analyze-persona`  
  - Body: `{ "answers": [...] }`
  - Returns: `{ "persona": "...", "redirect": "..." }`

### Credits

- `GET /api/credits/status`
- `POST /api/credits/connect/{provider}`
- `POST /api/credits/redeem/{provider}`

See `/apps/api/app/routes/onboarding.py` and `/apps/api/app/routes/credits.py` for implementation.

---

## 🗄️ Database Schema

See `infra/migrations.sql` for all tables.

Key tables:
- `user_profiles` (id, user_id, persona, answers, created_at)
- `credits` (id, user_id, provider, status, credits_used, created_at)

Seed demo data:  
```bash
python mosaicx/infra/scripts/seed_dev_data.py
```

---

## 🧪 Testing

- Run all services:  
  `docker compose up --build`
- Backend tests:  
  `pytest mosaicx/apps/api/tests`
- Frontend:  
  `npm run dev` (in `mosaicx/apps/web`)
- API test (example):  
  See cURL examples above.

---

## 🤝 Contributing

Pull requests welcome! Please open issues for bugs or feature requests.

---

## 📄 License

[MIT](LICENSE) (or specify your license here)

---

## 🌐 Links

- [OpenAPI Docs](http://localhost:8000/api/docs)
- [Supabase](https://supabase.com/)
- [LangChain](https://langchain.com/)
- [Gemini AI Studio](https://aistudio.google.com/)
- [ElevenLabs](https://elevenlabs.io/)

---

## 👥 Maintainers

- Ravi RS Nadimpalli
# mosaic_coe
Mini Open-Source AI Clusters empowering MSMEs, students &amp; innovators to build, deploy &amp; scale GenAI solutions through low-code tools &amp; shared compute.
