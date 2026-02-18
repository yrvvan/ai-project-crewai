# CrewAI Multi-Agent Test Case Generator

A FastAPI-based multi-agent system built with CrewAI to generate
structured, production-grade API test cases using LLM collaboration.

This project demonstrates how to design, orchestrate, and deploy a
CrewAI-powered quality engineering assistant capable of producing
comprehensive, structured test cases for APIs and backend systems.

------------------------------------------------------------------------

## 🚀 Overview

This system:

-   Uses CrewAI to orchestrate LLM-powered agents
-   Exposes a FastAPI REST endpoint
-   Generates structured JSON test cases
-   Enforces deterministic, machine-readable outputs
-   Is designed for extensibility and production-readiness

------------------------------------------------------------------------

## 🏗 Architecture

### Core Components

-   FastAPI -- REST interface
-   CrewAI -- Agent orchestration framework
-   Groq / LLaMA 3.3 -- Text generation engine
-   UV -- Dependency management

### High-Level Flow

1.  Client sends topic to `/analyze`
2.  CrewAI agent generates structured test cases
3.  JSON is validated and sanitized
4.  API returns structured response

------------------------------------------------------------------------

## 📦 Requirements

-   Python \>=3.10 and \<3.14
-   uv package manager

------------------------------------------------------------------------

## ⚙️ Installation

### 1️⃣ Install uv

``` bash
pip install uv
```

### 2️⃣ Install dependencies

``` bash
uv sync
```

Or:

``` bash
crewai install
```

------------------------------------------------------------------------

## 🔐 Environment Setup

Create a `.env` file in the root directory:

``` env
MODEL=groq/llama-3.3-70b-versatile
OPENAI_API_KEY=your_key_here
GROQ_API_KEY=your_key_here
```

> Never commit `.env` to version control.

------------------------------------------------------------------------

## ▶️ Running the Project

``` bash
uv run uvicorn main:app --reload
```

Or:

``` bash
uvicorn src.crew_ai.main:app --reload
```

Access Swagger UI:

    http://127.0.0.1:8000/docs

------------------------------------------------------------------------

## 📡 API Usage

### Endpoint

POST `/analyze`

### Request Body

``` json
{
  "topic": "Settle open bills API test scenarios"
}
```

### Example Response

``` json
{
  "status": "success",
  "count": 5,
  "result": [
    {
      "testCaseId": "TC001",
      "description": "Valid request with correct authorization",
      "input": {
        "request": {
          "method": "POST",
          "endpoint": "/api/admin/tasks/settle",
          "headers": {},
          "body": {}
        }
      },
      "expectedOutput": {
        "statusCode": 200,
        "response": "Successful settlement execution"
      }
    }
  ]
}
```

------------------------------------------------------------------------

## 🧠 Agent Configuration

Located at:

    src/crew_ai/config/

-   `agents.yaml` -- Agent roles and configuration
-   `tasks.yaml` -- Task definitions and expected outputs

------------------------------------------------------------------------

## 📁 Project Structure

    .
    ├── src/
    │   └── crew_ai/
    │       ├── config/
    │       │   ├── agents.yaml
    │       │   └── tasks.yaml
    │       ├── crew.py
    │       └── main.py
    ├── .env
    ├── pyproject.toml
    ├── uv.lock
    └── README.md

------------------------------------------------------------------------

## 🔒 Best Practices

-   ✅ Commit `uv.lock`
-   ❌ Do NOT commit `.venv/`
-   ❌ Do NOT commit `.env`
-   Use structured JSON instead of raw curl strings
-   Keep LLM outputs deterministic (`temperature=0`)
-   Validate all LLM responses before returning to clients

------------------------------------------------------------------------

## 🧪 Production Considerations

For real-world deployment:

-   Add retry logic for malformed LLM outputs
-   Implement schema validation with Pydantic
-   Add logging & monitoring
-   Introduce rate limiting
-   Deploy behind reverse proxy (Nginx / Cloud Load Balancer)

------------------------------------------------------------------------

## 🤝 Contributing

1.  Fork the repository
2.  Create feature branch
3.  Submit pull request
4.  Ensure linting and formatting pass