# Telegram Job Apply Assistant

A Telegram-based AI job application assistant that stores your CV, analyses job postings against your profile, scores your fit, and helps automate the application process — all through a simple chat interface.

## What It Does

Send job postings to the bot and it will:

1. **Store your CV** — upload once, used for all future analyses
2. **Analyse any job posting** — paste a job description and get an instant fit analysis
3. **Score your match** — AI compares the job requirements against your CV
4. **Highlight gaps** — tells you exactly what's missing and what to emphasise
5. **Guide your application** — recommends what to highlight for each specific role
6. **Track applications** — logs every job you apply to in a database
7. **Automate submission** — can submit applications automatically for approved roles

## Commands

| Command | Action |
|---------|--------|
| `/start` | Welcome message and instructions |
| `/upload_cv` | Upload your CV file for analysis |
| `/apply [job description]` | Analyse a job and get fit score |
| `/skip` | Skip current application |
| `/cancel` | Cancel current action |
| `/status` | Check application status |

## Architecture

```
Telegram Bot → Parse Command → Route Command
    ├── /upload_cv → Download CV → Store CV & Profile → Confirm
    ├── /apply → Extract Job Details → Analyse Requirements (OpenAI)
    │               → Get Stored CV → Compare Job with CV
    │               → Fit Analysis → Send Results
    │               ├── Approve → Log Application → Submit → Confirm
    │               └── Skip → Confirm Skipped
    └── /start → Send Welcome Message
```

## Tech Stack

- **n8n** — workflow orchestration
- **OpenAI GPT** — job requirement extraction and CV-to-job fit analysis
- **Telegram Bot** — conversational interface
- **Supabase / PostgreSQL** — CV storage and application tracking

## Key Features

- **One-time CV upload** — store your CV once and reuse it for every job analysis
- **AI-powered fit scoring** — detailed analysis of how well you match each role
- **Gap identification** — specific feedback on what skills or experience are missing
- **Application logging** — full history of every role you've applied to
- **Smart routing** — command parser handles multiple workflows from a single bot

## Example Interaction

```
You: /apply [paste job description here]

Bot: 📊 Fit Analysis for: Senior Automation Engineer at Hostinger

Match Score: 75%

✅ Strong matches:
- n8n automation experience
- Node.js backend development
- Docker deployment
- Non-technical stakeholder collaboration

⚠️ Gaps to address:
- TypeScript (you have JS — mention this)
- Vue.js frontend

💡 What to highlight:
Lead with your n8n production experience.
Mention your ERP-style internal tools.
Your Kaunas location is a big advantage.

Ready to apply? [Apply] [Skip]
```

---

Built by [Shehroz Khan](https://www.linkedin.com/in/shehroz-khan-b91716197/) · Fullstack Automation Engineer
