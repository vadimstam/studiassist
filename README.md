# 📚 AI Study Assistant

**Project Title:** AI Study Assistant for University Students  
**Objective:** Help students get instant, subject-specific answers to academic questions using AI, with RAG over their own lecture slides, quizzes, and a performance dashboard.  
**Tools:** Python, Streamlit (frontend), FastAPI (backend)  
**AI Model:** OpenAI / Google Gemini / Anthropic Claude — selectable at runtime via the `AI_PROVIDER` env var.

---

## 🗂️ Project Structure

```
ai_study_assistant/
├── app.py            # Streamlit frontend
├── backend.py        # FastAPI backend
├── requirements.txt  # Dependencies
└── README.md
```

---

## ⚙️ Setup & Running Instructions

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/ai-study-assistant.git
cd ai-study-assistant
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure your AI provider and API key

The backend reads `AI_PROVIDER` at startup and will refuse to boot without it. Pick one of `openai`, `gemini`, or `anthropic` and provide the matching key.

**Easiest: create a `.env` file** in the project root (loaded automatically via `python-dotenv`):
```bash
cp .env.example .env
# then edit .env and set AI_PROVIDER + the matching key
```

Or export them in your shell:

```bash
# macOS / Linux
export AI_PROVIDER=gemini
export GEMINI_API_KEY=your_key_here

# Windows (PowerShell)
$env:AI_PROVIDER="gemini"
$env:GEMINI_API_KEY="your_key_here"

# Windows (Command Prompt)
set AI_PROVIDER=gemini
set GEMINI_API_KEY=your_key_here
```

Get a free Gemini API key at: https://aistudio.google.com/apikey
(Use `OPENAI_API_KEY` or `ANTHROPIC_API_KEY` instead if you pick those providers.)

### 4. Start the FastAPI backend
```bash
uvicorn backend:app --reload
# Runs at http://localhost:8000
# API docs at http://localhost:8000/docs
```

### 5. Start the Streamlit frontend (new terminal)
```bash
streamlit run app.py
# Opens at http://localhost:8501
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/`          | Health check (returns active AI provider) |
| GET  | `/subjects`  | List available subjects |
| POST | `/ask`       | Submit a question (streams answer) |
| POST | `/upload`    | Upload a `.pdf` or `.pptx` lecture for RAG |
| POST | `/summarize` | Summarize the uploaded lecture |
| POST | `/quiz`      | Generate a multiple-choice quiz |

**POST `/ask` body:**
```json
{
  "subject": "Computer Science",
  "question": "What is recursion?",
  "level": "Undergraduate",
  "session_id": ""
}
```
Pass a `session_id` returned by `/upload` to get answers grounded in your slides.

---

## ✨ Features
- Select subject + academic level, then ask any academic question
- Streaming AI answers with a clean, structured format
- Upload a **PDF or PPTX** lecture; the backend chunks + embeds it and answers using RAG
- One-click **lecture summarization** (main topics, key concepts, takeaways)
- **Quiz mode** — generate multiple-choice quizzes from your slides or any subject, with scoring, XP, and badges
- **Dashboard** — average / best score, per-subject breakdown, session log, score history chart
- Question history persisted within the session
- Multi-provider AI (OpenAI / Gemini / Anthropic) selected via env var

---

## 👥 Team Members
<!-- TODO: replace with real names + roles before submission -->
- _Name_ — _Role_
- _Name_ — _Role_
- _Name_ — _Role_
