# 🤖 Automated Job Application System

> Built with n8n + Google Gemini AI — finds jobs, researches companies, writes tailored resumes and cold emails, sends applications with your approval, follows up automatically, and delivers weekly reports.

![n8n](https://img.shields.io/badge/n8n-workflow-orange?style=flat-square)
![Gemini](https://img.shields.io/badge/Google-Gemini_AI-blue?style=flat-square)
![Gmail](https://img.shields.io/badge/Gmail-automated-red?style=flat-square)
![Telegram](https://img.shields.io/badge/Telegram-approval_bot-blue?style=flat-square)
![Cost](https://img.shields.io/badge/cost-$0_free_tier-green?style=flat-square)

---

## 📌 What This Does

Instead of manually searching job boards, writing cover letters, and sending cold emails every day — this system does it all automatically while keeping you in control via Telegram.

```
Daily 9am  → Finds jobs from 5 sources → AI filters relevant ones → Saves to Sheets
Daily 10am → Researches each company → Finds HR email → Checks for portal
Daily 11am → Tailors your resume → Writes cover letter → Saves as Google Docs
Daily 12pm → Writes cold email → Sends YOU a Telegram preview → You reply YES/NO
Daily 2pm  → Checks for no-reply after 5 days → Sends follow-up on your approval
Every Mon  → Sends weekly stats report to Telegram
```

---

## 🔄 Full Workflow

### Step 1 — Job Discovery
- Pulls listings from **Adzuna**, **Remotive**, **Indeed RSS**, **Internshala RSS**, **LinkedIn RSS**
- Google Gemini filters jobs matching your title, skills, and location
- Skips duplicate companies
- Saves matched jobs to Google Sheets with status `Matched`

### Step 2 — Company Research
- Scrapes company website and careers page
- Finds HR/founder email via **Hunter.io**
- Gemini writes a 3-line company summary
- Checks if a direct application portal exists
- Updates Sheets with all research data

### Step 3 — Application Prep
- Gemini tailors your resume to match each job description
- Gemini writes a custom cover letter under 250 words
- Both saved as **Google Docs**
- Doc links saved to Sheets

### Step 4 — Outreach + Approval
Two paths based on portal availability:

**Portal found →**
Gemini writes application message → Telegram preview sent to you → Reply YES/NO → Status updated

**No portal →**
Gemini writes cold email to HR → Telegram preview sent to you → Reply YES → Gmail sends automatically → Logged as Applied

### Step 5 — Follow-up
- Runs daily, checks applications older than 5 days with no reply
- Gemini writes a short 3-sentence follow-up
- Telegram approval before sending
- Updates status to `Follow-up Sent`

### Step 6 — Weekly Report
Every Monday 8am, sends this to Telegram:
```
📊 Weekly Job Search Report
📧 Cold emails sent: X
🌐 Portal applications: X
🔁 Follow-ups sent: X
💬 Replied: X
🎯 Interviews: X
❌ Rejected: X
Reply rate: X%
```

### Bonus — Gmail Response Tracker
- Monitors inbox for replies from HR emails
- Auto-updates status to `Replied` in Sheets

---

## 🛠️ Tech Stack

| Tool | Purpose | Cost |
|------|---------|------|
| n8n Cloud | Workflow automation engine | Free |
| Google Gemini AI | Filtering, writing, research | Free |
| Adzuna API | Job listings | Free |
| Remotive API | Remote jobs | Free |
| Indeed / Internshala / LinkedIn | RSS job feeds | Free |
| Hunter.io | Find HR emails | Free |
| Gmail | Send emails | Free |
| Google Sheets | Application tracker | Free |
| Google Docs | Resume + cover letter storage | Free |
| Telegram Bot | Approval system + reports | Free |

**Total monthly cost: $0**

---

## 📊 Google Sheets Structure

```
Company | Job Title | Type | Job URL | HR Email | Company Summary |
Has Portal | Portal URL | Status | Applied Date | Follow-up Sent |
Original Email | Resume Doc URL | Cover Letter URL | Notes
```

**Status flow:**
```
Matched → Researched → Prep Done → Applied / Portal Applied
→ Follow-up Sent → Replied → Interview → Rejected / Skipped
```

---

## ⚙️ Setup

### 1. API Keys Required
```
Adzuna        → adzuna.com/api
Hunter.io     → hunter.io
Google Gemini → aistudio.google.com
```

### 2. n8n Credentials to Connect
```
✅ Google Sheets OAuth2
✅ Google Docs OAuth2
✅ Gmail OAuth2
✅ Google Gemini(PaLM) API
✅ Telegram Bot API
```

### 3. Telegram Bot Setup
```
1. Open Telegram → search @BotFather
2. Send /newbot → follow steps → copy bot token
3. Get your Chat ID from @userinfobot
4. Add both to n8n credentials
```

### 4. Personalise the Prompts
In the Gemini nodes, replace:
```
[PASTE YOUR FULL RESUME HERE AS PLAIN TEXT]
[YOUR BACKGROUND HERE]
```

### 5. Import & Run
```
1. Import the JSON file into n8n
2. Connect all credentials
3. Add your API keys to HTTP Request nodes
4. Publish the workflow
5. Test each step manually in order
```

---

## 🧪 Testing Order

```
1. Run "Daily 9am - Job Discovery"      → check Sheets for new rows
2. Run "Daily 10am - Company Research"  → check HR email + summary
3. Run "Daily 11am - Application Prep"  → check Google Docs created
4. Run "Daily 12pm - Send Applications" → check Telegram for preview
5. Reply YES on Telegram                → check Gmail + Sheets updated
6. Run "Weekly Monday 8am - Summary"    → check Telegram report
```

---

## 💡 Key Features

- ✅ **Human-in-the-loop** — you approve every email before it sends
- ✅ **Duplicate prevention** — never applies to the same company twice
- ✅ **Portal detection** — finds direct apply links automatically
- ✅ **Auto follow-up** — never miss a follow-up again
- ✅ **Full tracking** — every application status logged in Sheets
- ✅ **Weekly insights** — reply rate and stats every Monday
- ✅ **Zero cost** — runs entirely on free tiers
- ✅ **Retry logic** — Gemini nodes retry automatically on failure

---

## 📁 Files

```
├── README.md
└── Automated_Job_Application_Discovery_and_Preparation_System.json
```

---

## 🎯 Why I Built This

This project was built as part of my automation engineering portfolio to demonstrate:
- Multi-source data aggregation and merging
- AI-powered content generation and filtering
- Human-in-the-loop design patterns
- End-to-end workflow automation
- Real-world problem solving with no-code/low-code tools

---

## 👤 Author

**Rachit Tibrewal**
Automation Engineer | n8n | AI Tools | Python

---

> ⭐ If you found this useful, give it a star!
