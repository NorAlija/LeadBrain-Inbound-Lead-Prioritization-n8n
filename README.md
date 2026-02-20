# 🚀 LeadBrain – AI-Powered Inbound Lead Prioritization for Agencies

## Overview

LeadBrain is a proof-of-concept system built to explore how AI and workflow automation can improve inbound lead handling for digital marketing agencies.

The system:

* Scores inbound leads using AI
* Explains the reasoning behind the score
* Logs results to Google Sheets
* Sends structured Gmail notifications
* Automatically applies Gmail labels:

  * High Lead
  * Medium Lead
  * Low Lead

This project was built as a **consulting wedge** to validate real-world agency workflows and identify automation opportunities in inbound sales processes.

---

## 🎯 Problem

Many agencies:

* Receive inbound leads via website forms or email
* Handle qualification manually
* Respond inconsistently or slowly
* Lack structured prioritization

This project explores:

> Can AI help agencies focus on high-value leads faster?

---

## 🏗 Architecture

### Frontend (Demo Interface)

* Built with **Lovable**
* Simple SaaS-style UI
* Users paste inbound lead details:

  * Name
  * Company
  * Website
  * Message
* Sends data to backend via webhook

⚠️ This is a **demo interface**, not a production SaaS frontend.

---

### Backend Automation

Built using:

* **n8n (self-hosted locally)**
* Exposed via **ngrok** for public webhook access
* OpenAI for scoring logic
* Gmail API for email routing
* Google Sheets for logging

Flow:

```
Lovable Form
  ↓
n8n Webhook
  ↓
AI Scoring (OpenAI)
  ↓
JSON Parse
  ↓
Merge Lead + AI Data
  ↓
Google Sheets Logging
  ↓
Gmail Send
  ↓
Gmail Label Assignment
  ↓
Webhook Response
```

---

## 🧠 AI Scoring Logic

The AI evaluates:

* Buying intent
* Budget signals
* Company maturity
* Clarity of request
* Fit for performance marketing agencies

Returns structured JSON:

```json
{
  "score": 75,
  "tier": "High",
  "reasoning": [...],
  "recommended_action": "..."
}
```

The reasoning is included to avoid black-box scoring.

---

## 📬 Gmail Automation

After scoring:

* A structured email summary is sent
* Gmail label is applied automatically based on score:

| Score | Label       |
| ----- | ----------- |
| ≥ 70  | High Lead   |
| 40–69 | Medium Lead |
| < 40  | Low Lead    |

Labels are applied using Gmail Label IDs via API.

---

## 📊 Google Sheets Logging

Each lead is logged with:

* Timestamp
* Name
* Company
* Message
* Score
* Tier
* Reasoning
* Recommended Action

This enables later analysis and model refinement.

---

## 🔐 Local Development Setup

### 1. n8n

Run locally:

```
n8n start
```

Default:

```
http://localhost:5678
```

### 2. ngrok

Expose webhook publicly:

```
ngrok http 5678
```

Use generated URL:

```
https://your-ngrok-url/webhook-test/lead-score
```

⚠️ ngrok free plan rotates URLs on restart.

---

### 3. Google OAuth

Configured in Google Cloud Console:

* Gmail API enabled
* OAuth Client ID created
* Redirect URI:

```
http://localhost:5678/rest/oauth2-credential/callback
```

---

## ⚠️ Important Notes

* This is a **validation project**, not a production SaaS.
* The Lovable frontend is a demo interface.
* n8n is currently hosted locally and exposed via ngrok.
* Gmail labels must exist beforehand.
* Label IDs are used (not label names).

---

## 🚀 Purpose of This Project

This project is not intended as a final product.

It was built to:

* Validate agency lead-handling workflows
* Demonstrate AI + automation capability
* Open consulting conversations
* Identify deeper operational bottlenecks

## 🛠 Tech Stack

* Lovable (Frontend Demo)
* n8n (Automation Engine)
* OpenAI API
* Gmail API
* Google Sheets API
* ngrok (Webhook exposure)

