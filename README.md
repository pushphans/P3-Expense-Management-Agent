# P3 Expense Management Agent

A professional AI-powered expense management assistant built with Python, FastAPI, LangChain, LangGraph, and Supabase. This project enables users to interact with their finances through natural language by saving expenses, retrieving expense history, and receiving financial insights through an API-driven workflow.

## Overview

P3 Expense Management Agent is designed to simplify expense tracking by combining conversational AI with structured finance operations. It accepts user requests in plain English, understands the intent, extracts relevant expense details, and stores or retrieves data from a Supabase-backed backend.

## Key Features

- Natural language expense entry and retrieval
- AI-powered intent understanding using OpenAI models
- LangGraph-based workflow orchestration
- FastAPI REST API for chat and expense management
- Supabase integration for chat history and expense persistence
- Health check and structured API responses

## Tech Stack

- Python 3.10+
- FastAPI
- LangChain
- LangGraph
- OpenAI GPT-4o-mini
- Pydantic
- Supabase
- Uvicorn

## Project Structure

```text
.
├── app/
│   ├── agent/
│   │   └── finance_agent_graph.py
│   ├── api/
│   │   └── router.py
│   ├── core/
│   │   ├── config.py
│   │   ├── db.py
│   │   └── llm.py
│   └── main.py
├── main.py
├── requirement.txt
├── .env.example
└── README.md
```

## Prerequisites

Before running the project, ensure you have:

- Python 3.10 or higher
- pip installed
- Access to an OpenAI API key
- A Supabase project with the required tables

## Installation

1. Clone the repository
   ```bash
   git clone https://github.com/pushphans/P3-Expense-Management-Agent.git
   cd P3-Expense-Management-Agent
   ```

2. Create and activate a virtual environment
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # On Windows: .venv\Scripts\activate
   ```

3. Install dependencies
   ```bash
   pip install -r requirement.txt
   ```

4. Configure environment variables
   ```bash
   cp .env.example .env
   ```

   Update `.env` with your actual values:

   ```env
   OPENAI_API_KEY=your_openai_api_key
   SUPABASE_URL=your_supabase_url
   SUPABASE_KEY=your_supabase_service_role_key
   ```

## Running the Application

Start the FastAPI server locally:

```bash
uvicorn app.main:app --reload
```

The API will be available at:

- `http://127.0.0.1:8000/health`
- `http://127.0.0.1:8000/api/v1/chat`
- `http://127.0.0.1:8000/api/v1/expenses`

## API Endpoints

### Health Check

- `GET /health`

### Chat

- `POST /api/v1/chat`

Request body example:

```json
{
  "user_id": "user_123",
  "session_id": "session_456",
  "user_message": "Save an expense of 25 for lunch in Food"
}
```

### Expenses

- `GET /api/v1/expenses`

Query parameters:

- `user_id` (required)
- `start_date`
- `end_date`
- `category`
- `limit`

## Database Notes

This application expects a Supabase backend with at least the following data structures:

- `finance_agent_chat_history`
- `finance_agent_expense`

These tables are used by the API layer to store conversation history and expense records.

## Development Notes

The AI agent workflow is defined in `app/agent/finance_agent_graph.py`, while the API interface is implemented in `app/api/router.py`. The core service layer handles configuration, LLM initialization, and database access.

## Contributing

Contributions are welcome. Feel free to open an issue or submit a pull request with improvements, bug fixes, or new features.
