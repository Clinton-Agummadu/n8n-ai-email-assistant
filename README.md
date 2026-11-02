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
## 🛠️ Setup & Installation

### 1. Requirements
- Self-hosted or Cloud **n8n** instance.
- **Google Gemini API Key**.
- Active IMAP & SMTP credentials (or App Passwords).

### 2. Import Workflow
1. Download `ai_email_assistant.json` from this repository.
2. In your n8n workspace, click **Workflows** $\rightarrow$ **Import from File**.
3. Select `ai_email_assistant.json`.

### 3. Credential Configuration
- Configure your **IMAP Account** credential on the `Email Trigger (IMAP)` node.
- Add your **Google Gemini API Key** under the `Google Gemini Chat Model` node.
- Configure your **SMTP Account** credential on the `Send an Email` node.

---

## 💡 Architectural Insights & Trade-offs

During development, two key operational challenges were addressed:

1. **Recursive Feedback Loops:** When an IMAP trigger watches an inbox that also receives automated review notifications, the system risks infinite execution loops. This was resolved by routing review drafts to a dedicated review destination and implementing an `IF` guardrail node filtering out `[AI DRAFT REVIEW]` subjects and bot sender headers.
2. **Native Drafts vs. SMTP Workaround:** While the native Gmail API `Create Draft` endpoint is ideal for single-inbox setups, using SMTP with dynamic `Reply-To` headers serves as a robust cross-platform alternative when operating under strict API/OAuth scopes.

---

## 👤 Author

**Clinton Agummadu (Odogwu)**
* AI Automation Specialist & Workflow Engineer
* **LinkedIn:** [Clinton Agummadu](www.linkedin.com/in/clinton-agummadu-602389288)
