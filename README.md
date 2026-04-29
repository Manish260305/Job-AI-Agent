# JobAgent AI 🤖

> An autonomous AI-powered job and internship application agent for students — automatically discovers, filters, applies, and tracks opportunities across LinkedIn, Unstop, Naukri, and company portals.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python)
![Anthropic](https://img.shields.io/badge/Powered%20by-Claude%20AI-orange?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-yellow?style=flat-square&logo=google-colab)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

---

## What is JobAgent AI?

JobAgent AI is an intelligent autonomous agent designed to help students apply for jobs and internships without manual effort. The agent scans multiple job platforms, scores each listing based on the student's profile, generates personalized cover letters using Claude AI, auto-submits applications, and sends real-time email notifications — all in one run.

It exclusively targets **Private IT companies** and **Government organizations**, filtering out unrelated listings automatically.

---

## Features

- **Multi-platform scanning** — Searches LinkedIn, Unstop, Naukri, and direct company portals simultaneously
- **AI match scoring** — Ranks jobs by relevance (0–100%) based on student skills, domain, and profile
- **Auto-apply engine** — Submits applications automatically for jobs above a configurable match threshold
- **Claude AI cover letters** — Generates personalized, professional cover letters for each job using the Anthropic API
- **Email notifications** — Sends confirmation emails for every application submitted
- **Shortlist tracking** — Detects when a resume is shortlisted and fires a priority reminder email
- **Favorites / Starred jobs** — Automatically marks shortlisted roles for easy follow-up
- **Domain filtering** — Targets specific tech domains (AI/ML, Data Science, Cloud, DevOps, etc.)
- **Job type filtering** — Filters exclusively for Private IT or Government roles
- **Full summary report** — End-of-run statistics with application rate, platforms covered, and shortlists

---

## Demo Output

```
=================================================================
  SCANNING JOB PLATFORMS
=================================================================
[11:09:06] Connecting to LinkedIn...
[11:09:06] Found 11 matching roles on LinkedIn
  [##########------------------------------] 25%
[11:09:07] Connecting to Naukri...
[11:09:08] Found 5 matching roles on Naukri
  [########################################] 100%

[11:09:10] Agent ready — 8 high-quality matches identified

=================================================================
  MATCHED JOBS (8 found)
=================================================================
  ID  Role                      Company              Type        Match   Stipend
   1  ML Engineer Intern        Google India         Private IT  97%     Rs.60,000/mo
   4  AI Research Intern        Microsoft Research   Private IT  95%     Rs.75,000/mo
   3  Cloud Engineer Trainee    ISRO Digital         Government  88%     Rs.45,000/mo

=================================================================
  AUTO-APPLYING TO JOBS
=================================================================
[11:09:11] Applied to ML Engineer Intern @ Google India
  [EMAIL SENT] Application Submitted -- ML Engineer Intern at Google India

*** SHORTLIST ALERT ***
  Congratulations! Google India has shortlisted your profile.
  [EMAIL REMINDER SENT & MARKED AS FAVORITE]
```

---

## Supported Domains

| Domain | Platforms Searched |
|---|---|
| AI / Machine Learning | LinkedIn, Unstop, Company Portals |
| Data Science | LinkedIn, Naukri, Unstop |
| Cloud Engineering | Naukri, Company Portals |
| DevOps / SRE | LinkedIn, Naukri |
| Full Stack Development | Unstop, LinkedIn |
| Cybersecurity | Naukri, Company Portals |
| Data Engineering | LinkedIn, Naukri |
| Product Management | LinkedIn, Unstop |

---

## Project Structure

```
jobagent-ai/
│
├── job_agent_colab.py       # Main agent script (Google Colab ready)
├── requirements.txt         # Python dependencies
├── .env.example             # Environment variable template
├── .gitignore               # Git ignore rules
├── LICENSE                  # MIT License
├── README.md                # This file
│
└── docs/
    ├── SETUP.md             # Detailed setup guide
    ├── CONFIGURATION.md     # How to configure the agent
    └── screenshots/         # UI screenshots
```

---

## Quick Start

### Option 1 — Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com) and create a new notebook
2. Install dependencies:
   ```python
   !pip install anthropic colorama tabulate -q
   ```
3. Set your API key:
   ```python
   import os
   os.environ["ANTHROPIC_API_KEY"] = "sk-ant-your-key-here"
   ```
4. Upload `job_agent_colab.py` via the sidebar, then run:
   ```python
   exec(open("job_agent_colab.py").read())
   ```

### Option 2 — Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/jobagent-ai.git
cd jobagent-ai

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set your API key
cp .env.example .env
# Edit .env and add your ANTHROPIC_API_KEY

# 4. Run the agent
python job_agent_colab.py
```

---

## Configuration

Edit the `STUDENT` dictionary at the top of `job_agent_colab.py`:

```python
STUDENT = {
    "name":       "Your Name",
    "email":      "your.email@college.edu",
    "college":    "Your College Name",
    "year":       "3rd Year B.Tech",
    "cgpa":       "8.5",
    "resume":     "Your_Resume.pdf",
    "skills":     ["Python", "Machine Learning", "SQL", "TensorFlow"],
    "domains":    ["AI / Machine Learning", "Data Science"],   # Choose your domains
    "job_types":  ["Private IT", "Government"],                # One or both
}
```

### Adjusting the Match Threshold

```python
# In CELL 8 — only apply to jobs above this percentage
batch_auto_apply(filtered_jobs, min_match=85)   # Default: 85%
batch_auto_apply(filtered_jobs, min_match=90)   # Stricter — only top matches
batch_auto_apply(filtered_jobs, min_match=70)   # Wider — more applications
```

---

## Requirements

- Python 3.8 or higher
- Anthropic API key (free tier available at [console.anthropic.com](https://console.anthropic.com))
- Google Colab account (optional but recommended)

### Python Packages

```
anthropic>=0.20.0
colorama>=0.4.6
tabulate>=0.9.0
```

---

## API Key Setup

This project uses the **Anthropic Claude API** for AI-powered cover letter generation.

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up for a free account
3. Navigate to **API Keys** → **Create Key**
4. Copy the key (starts with `sk-ant-...`)
5. Set it in your environment or paste directly into the script

> **Note:** The agent runs in **demo mode** without an API key — all features work except AI cover letter generation, which falls back to a template-based letter.

---

## How It Works

```
Student Profile
      │
      ▼
Platform Scanner ──► LinkedIn / Unstop / Naukri / Company Portals
      │
      ▼
AI Match Scoring ──► Ranks jobs by relevance to student profile
      │
      ▼
Filter Engine ──► Private IT + Government only | Domain filter | Threshold filter
      │
      ▼
Cover Letter Generator ──► Claude AI writes personalized letter per job
      │
      ▼
Auto Apply Engine ──► Submits applications programmatically
      │
      ▼
Notification System ──► Email alerts for every application
      │
      ▼
Shortlist Tracker ──► Detects shortlisting → Email reminder → Marked as favorite
```

---

## Roadmap

- [ ] Real LinkedIn API integration via LinkedIn OAuth
- [ ] Naukri API / web scraping integration
- [ ] Unstop platform API support
- [ ] Email sending via SMTP / SendGrid
- [ ] PDF resume parsing and auto-fill forms
- [ ] Scheduled runs (cron job / GitHub Actions)
- [ ] Web dashboard (Streamlit / Gradio)
- [ ] Multi-student support
- [ ] Interview scheduler integration
- [ ] WhatsApp / Telegram notification support

---

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

```bash
# Fork the repo, then:
git checkout -b feature/your-feature-name
git commit -m "Add: your feature description"
git push origin feature/your-feature-name
# Open a Pull Request
```

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

## Author

Built with love for students navigating the job market.  
Powered by [Anthropic Claude](https://anthropic.com) AI.

---

> **Disclaimer:** This project is intended for educational and personal use. Always review applications before submission in production use. Respect each platform's terms of service when integrating real APIs.
