# 🤖 AI-Powered Email Assistant & Lead Routing Pipeline

An automated, human-in-the-loop email triage and response pipeline built with **n8n** and **Google Gemini AI**. The system intercepts incoming client inquiries in real-time, categorizes them by topic and priority, generates contextual draft responses, and routes them to a review queue with a single-click `Reply-To` dispatch mechanism.

---

## 🚀 Key Features

- **Real-Time IMAP Ingestion:** Monitors inbox for new incoming client inquiries automatically.
- **LLM-Powered Classification & Drafting:** Uses **Google Gemini** to analyze raw body text, summarize content, categorize inquiries (*Sales, Support, Billing, Partnerships, Jobs, Others*), assign priority (*High, Medium, Low*), and generate tailored response drafts.
- **Data Normalization:** Custom JavaScript Code node parses raw LLM JSON outputs, cleans code fences, handles fallbacks, and standardizes client metadata (`client_email`, `client_name`).
- **Dynamic `Reply-To` Routing:** Overrides outgoing review headers so hitting **Reply** in Gmail automatically populates the client's original email address.
- **Infinite Loop Safeguards:** Implements strict architectural separation and pre-processing logic (filtering bot sender addresses and notification subject flags) to prevent recursive automation loops.
- **Structured HTML Email Templates:** Clean formatting with inline CSS (`white-space: pre-wrap;`) to render line breaks, callout boxes, and formatted metadata blocks cleanly.

---

## 🛠️ Tech Stack & Tools

- **Workflow Automation:** [n8n](https://n8n.io/)
- **Large Language Model:** Google Gemini AI API (`Basic LLM Chain`)
- **Scripting & Parsing:** JavaScript (Node.js runtime inside n8n)
- **Protocols & Services:** IMAP, SMTP, Custom Domain Email (`Zoho Mail / Resend API`)

---

## 📐 Workflow Architecture
