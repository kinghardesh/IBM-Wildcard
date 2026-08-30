# Nova Health

A healthcare navigation assistant that helps people understand their symptoms, find care options, and navigate insurance — powered by IBM watsonx.ai (Granite) and Google Gemini.

---

## What it does

Nova is a five-tab web app built for people who are uninsured, underinsured, or simply confused by the US healthcare system.

| Tab | What it does |
|---|---|
| **Home** | Chat with Nova (IBM Granite via watsonx.ai) — describe your symptoms and get plain-language guidance on what level of care to seek |
| **Insurance lens** | Browse providers filtered by specialty, language, and accessibility |
| **No insurance** | Find free/low-cost clinics (HRSA), Medicaid eligibility, 211 social services, and financial aid resources by ZIP code and state |
| **Urgent** | Upload a photo of a wound or symptom for an objective visual description (Google Gemini), and use voice-to-text to build an emergency summary to share with paramedics |
| **Manage costs** | Understand care cost estimates, see what your plan covers, and manage your payment plan |
| **Learn** | Quick how-to guides on first aid, prevention, nutrition, mental health, and when to see a doctor |

Additional features:
- Light, dark, and colorblind-friendly themes
- Voice dictation for the chat (Web Speech API)
- One-click copy for AI-generated summaries
- Home tab nav cards linking to all sections

---

## Tech stack

| Layer | Tech |
|---|---|
| Frontend | React 19, Vite, Lucide icons |
| Backend | Node.js, Express |
| AI (chat) | IBM watsonx.ai — Granite models |
| AI (photo analysis) | Google Gemini Vision |
| Clinic finder | HRSA Find a Health Center, 211.org, healthcare.gov |

---

## Project structure

```
IBM-Wildcard/
├── src/
│   ├── NovaHealth.jsx        # All frontend tabs and UI
│   └── ManageCareCosts.jsx   # Manage costs tab component
├── backend/
│   ├── server.js             # Express API — watsonx.ai chat + Gemini photo analysis
│   ├── package.json
│   └── .env                  # API keys (not committed)
├── public/
├── index.html
├── vite.config.js
└── package.json
```

---

## Running locally

You need **two terminals**.

### 1. Backend

```bash
cd backend
npm install
npm run dev
```

Runs on `http://localhost:5001`.

### 2. Frontend

```bash
npm install
npm run dev
```

Runs on `http://localhost:5173`.

---

## Environment variables

Create `backend/.env` with the following:

```
WATSONX_API_KEY=your_ibm_api_key
WATSONX_PROJECT_ID=your_project_id
WATSONX_SPACE_ID=your_space_id
WATSONX_URL=https://us-south.ml.cloud.ibm.com
WATSONX_MODEL_ID=ibm/granite-4-h-small
GEMINI_API_KEY=your_gemini_api_key
PORT=5001
```

**Never commit `.env` to git** — it is already listed in `backend/.gitignore`.

### Where to get the keys

| Key | Where |
|---|---|
| `WATSONX_API_KEY` | [IBM Cloud](https://cloud.ibm.com) → Manage → Access (IAM) → API Keys |
| `WATSONX_PROJECT_ID` / `WATSONX_SPACE_ID` | [watsonx.ai](https://dataplatform.cloud.ibm.com) → Deployment space → Manage tab |
| `WATSONX_MODEL_ID` | The model deployed in your watsonx.ai space |
| `GEMINI_API_KEY` | [Google AI Studio](https://aistudio.google.com) → Get API key |

---

## Deploying

| Service | Purpose |
|---|---|
| [Vercel](https://vercel.com) | Frontend — import repo, set root to `.`, Vite is auto-detected |
| [Railway](https://railway.app) | Backend — import repo, set root to `backend`, add env variables in Settings |

After deploying the backend to Railway, update the fetch URLs in [`src/NovaHealth.jsx`](src/NovaHealth.jsx) from `http://localhost:5001` to your Railway domain.

---

## Disclaimer

Nova provides general health information and navigation only. It does not diagnose medical conditions, prescribe medication, or guarantee insurance coverage. In an emergency, call 911.
