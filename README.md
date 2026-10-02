# TriageAI 🚀

> An AI-Powered Support Ticket Triage Engine built with Python, FastAPI, and Structured LLM Outputs.

TriageAI automatically ingests, categorizes, prioritizes, and summarizes incoming support tickets in real-time, routing them to the correct teams while maintaining a human-in-the-loop admin feedback loop for continuous model evaluation.

## ✨ Features

* **Automated AI Triage:** Classifies tickets into categories (*Technical, Billing, Account, General*) and assigns priority levels (*Low, Medium, High, Urgent*).

* **Intelligent Routing:** Automatically assigns incoming requests to dedicated teams (*Tier 1, DevOps, Finance, Customer Success*).

* **Executive Summarization:** Generates concise 1–2 sentence context summaries for quick agent comprehension.

* **Admin Feedback Loop:** Allows support leads to override AI decisions, logging human ground-truth data for evaluation and fine-tuning.

* **High-Performance API:** Built on FastAPI with asynchronous endpoint execution and auto-generated OpenAPI documentation.

## 🛠 Tech Stack

* **Language:** Python 3.10+

* **Framework:** FastAPI

* **Data Validation:** Pydantic v2

* **AI / LLM Integration:** OpenAI API (`gpt-4o-mini` with Structured Outputs)

* **Database:** SQLAlchemy 2.0 / SQLite (or PostgreSQL)

## 📁 Repository Structure

```
triage-ai/
├── app/
│   ├── __init__.py
│   ├── main.py          # FastAPI application & endpoints
│   ├── triage.py        # LLM parsing engine & structured prompts
│   ├── models.py        # Database schemas & Pydantic models
│   └── database.py      # DB connection setup
├── .env.example         # Environment variables template
├── requirements.txt     # Dependency list
└── README.md

```

## 🚀 Getting Started

### 1. Prerequisites

* Python 3.10 or higher

* An OpenAI API Key

### 2. Installation

1. Clone the repository:

   ```
   git clone https://github.com/your-username/triage-ai.git
   cd triage-ai
   
   ```

2. Create and activate a virtual environment:

   ```
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   
   ```

3. Install dependencies:

   ```
   pip install -r requirements.txt
   
   ```

4. Set up environment variables:

   ```
   cp .env.example .env
   
   ```

   Add your OpenAI key inside `.env`:

   ```
   OPENAI_API_KEY=your_openai_api_key_here
   
   ```

## 🏃 Running the Application

Start the development server with Uvicorn:

```
uvicorn app.main:app --reload

```

Once running, access the interactive API documentation at:

* **Swagger UI:** `http://127.0.0.1:8000/docs`

* **ReDoc:** `http://127.0.0.1:8000/redoc`

## 📡 API Endpoints

| **Method** | **Endpoint** | **Description** | 
| `POST` | `/tickets` | Submit a new ticket for instant AI triage and routing | 
| `GET` | `/tickets` | List all triaged tickets for the dashboard | 
| `PATCH` | `/tickets/{id}/feedback` | Admin override endpoint to submit ground-truth corrections | 

## 📝 Example Request

```
POST /tickets
Content-Type: application/json

{
  "customer_id": "CUST-9021",
  "subject": "Production Database Connection Timeout",
  "body": "Our primary database on Azure went down 10 minutes ago. All customer requests are returning 500 errors. We need immediate assistance."
}

```

### Response

```
{
  "id": 1,
  "customer_id": "CUST-9021",
  "subject": "Production Database Connection Timeout",
  "body": "Our primary database on Azure went down 10 minutes ago...",
  "category": "Technical",
  "priority": "Urgent",
  "assigned_team": "DevOps/Tech",
  "summary": "Primary Azure database outage causing site-wide 500 errors; requires urgent infrastructure intervention.",
  "status": "Triaged",
  "created_at": "2026-10-02T14:51:00Z"
}

```
