# FastAPI Learning Roadmap for LLMOps / DevOps

## 📌 Overview

This repository documents a practical, day-by-day FastAPI learning journey designed for **LLMOps and DevOps engineers**.

The goal is to learn how to build, test, deploy, and monitor AI-powered APIs using FastAPI while practising Python simultaneously. The roadmap focuses on production-oriented skills rather than advanced backend development.

Through hands-on exercises and a final capstone project, this repository covers the complete journey from developing a simple API to deploying an observable LLM-powered service on Kubernetes.

## 🎯 Learning Objectives

- Understand FastAPI fundamentals, HTTP methods, and REST APIs.
- Build API endpoints using Pydantic models and request validation.
- Manage configuration and secrets securely.
- Write automated API tests using `pytest` and FastAPI `TestClient`.
- Integrate external LLM APIs and handle failures, timeouts, and retries.
- Containerize applications using Docker.
- Deploy FastAPI applications to Kubernetes and AWS EKS.
- Monitor application health, latency, and errors using Prometheus and Grafana.
- Automate testing, image building, scanning, and deployment through CI/CD.
- Develop a production-oriented AI service suitable for LLMOps workflows.

## 🛠️ Technology Stack

| Category | Technologies |
| -------- | -------------|
| Programming language | Python |
| API framework | FastAPI |
| ASGI server | Uvicorn |
| Data validation | Pydantic |
| Automated testing | pytest, FastAPI TestClient, HTTPX |
| LLM integration | LLM APIs, SDKs, HTTP clients |
| Containerization | Docker |
| Orchestration | Kubernetes, AWS EKS |
| CI/CD | Jenkins, GitLab CI/CD |
| Container registry | Docker Hub, Amazon ECR |
| Observability | Prometheus, Grafana, application logging |
| Version control | Git, GitHub |

## 🗓️ 20-Day Learning Roadmap

### Week 1 — FastAPI Foundations

**Goal:** Understand API fundamentals and build your first FastAPI application.

| Day | Topic | Practical Outcome |
| --- | ----- | ------------------|
| 01 | Introduction to FastAPI | Understand APIs, HTTP, ASGI, and FastAPI vs Flask |
| 02 | Project Setup | Create a virtual environment and install dependencies |
| 03 | First FastAPI Application | Build and run your first API using Uvicorn |
| 04 | Swagger UI and OpenAPI | Explore interactive API documentation |
| 05 | HTTP Methods | Implement basic GET and POST endpoints |

### Week 2 — API Fundamentals and Automated Testing

**Goal:** Build reliable APIs with input validation, error handling, and automated tests.

| Day | Topic | Practical Outcome |
|---- | ----- | ------------------|
| 06 | Path and Query Parameters | Accept IDs, filters, and optional parameters |
| 07 | Pydantic Models | Validate request and response data |
| 08 | Status Codes and Error Handling | Handle HTTP errors and invalid requests |
| 09 | Environment Variables and Secrets | Externalize configuration and protect credentials |
| 10 | Automated API Testing | Test endpoints using pytest and FastAPI TestClient |

**Mandatory milestone:** Automated testing must be established before containerization.

### Week 3 — Production Basics and LLM Integration

**Goal:** Connect FastAPI to an LLM provider and handle real-world API failures.

| Day | Topic | Practical Outcome |
|---- | ----- | ------------------|
| 11 | Health Checks and Logging | Implement `/health` and useful application logs |
| 12 | LLM API Integration | Build an `/ask` endpoint that calls an LLM |
| 13 | Timeouts, Retries, and Failures | Handle provider errors, rate limits, and timeouts |
| 14 | Async and Await | Understand asynchronous endpoints and I/O-bound workloads |
| 15 | Mocking and LLM API Testing | Test model interactions without real API calls |

### Week 4 — DevOps, Deployment, and Observability

**Goal:** Deploy, monitor, and automate the lifecycle of an AI service.

| Day | Topic | Practical Outcome |
|---- | ----- | ------------------|
| 16 | Docker Containerization | Build and run a FastAPI Docker image |
| 17 | Kubernetes / AWS EKS | Deploy the application with Services and health probes |
| 18 | Prometheus and Grafana | Monitor API metrics, latency, and errors |
| 19 | CI/CD Pipeline | Automate tests, image building, scanning, and deployment |
| 20 | Production Readiness | Review security, reliability, and the complete workflow |

## 🧪 Automated Testing Strategy

Automated testing is a mandatory quality gate in this learning roadmap.

### Tools

- **pytest:** Test runner and assertion framework.
- **FastAPI TestClient:** Test API endpoints without starting a separate web server.
- **HTTPX:** HTTP client dependency used by FastAPI TestClient.
- **Mocking:** Simulate LLM provider responses and failures without making real API calls.

### Test Coverage Goals

- Verify successful responses from `/health`.
- Validate correct and incorrect request payloads.
- Check expected HTTP status codes.
- Test error-handling behaviour.
- Mock LLM API responses and provider failures.
- Run regression tests after application changes.

### Example Test

```python
from fastapi import FastAPI
from fastapi.testclient import TestClient

app = FastAPI()


@app.get("/health")
def health_check():
    return {"status": "healthy"}


client = TestClient(app)


def test_health_check():
    response = client.get("/health")

    assert response.status_code == 200
    assert response.json() == {"status": "healthy"}
```

Run the test with:

```bash
pytest -v
```

## 🔄 CI/CD Workflow

The CI/CD pipeline will enforce automated testing before allowing containerization or deployment.

```text
Developer Push
      |
      v
Checkout Source Code
      |
      v
Install Dependencies
      |
      v
Run pytest
      |
      +------ Tests Failed ------> Stop Pipeline
      |
      v
Tests Passed
      |
      v
Build Docker Image
      |
      v
Scan Image
      |
      v
Push to Container Registry
      |
      v
Deploy to Kubernetes / AWS EKS
      |
      v
Verify Deployment Health
      |
      v
Monitor with Prometheus and Grafana
```

**Quality gate:** If pytest returns a non-zero exit code, the pipeline must fail. Docker image building, publishing, and deployment must not proceed.

## 📂 Repository Structure

```text
FastAPI_Learning_Roadmap_for_LLMOps_DevOps/
│
├── README.md
├── .gitignore
├── requirements.txt
├── .env.example
│
├── Week_01_FastAPI_Foundations/
│   ├── Day_01_Introduction/
│   ├── Day_02_Project_Setup/
│   ├── Day_03_First_API/
│   ├── Day_04_Swagger_OpenAPI/
│   └── Day_05_HTTP_Methods/
│
├── Week_02_API_Fundamentals_Testing/
│   ├── Day_06_Path_Query_Parameters/
│   ├── Day_07_Pydantic_Models/
│   ├── Day_08_Status_Codes_Errors/
│   ├── Day_09_Environment_Variables/
│   └── Day_10_Automated_Testing/
│
├── Week_03_Production_LLM_Integration/
│   ├── Day_11_Health_Logging/
│   ├── Day_12_LLM_API_Integration/
│   ├── Day_13_Timeouts_Retries/
│   ├── Day_14_Async_Await/
│   └── Day_15_Mocking_LLM_Tests/
│
├── Week_04_DevOps_Deployment/
│   ├── Day_16_Docker/
│   ├── Day_17_Kubernetes_EKS/
│   ├── Day_18_Prometheus_Grafana/
│   ├── Day_19_CICD_Pipeline/
│   └── Day_20_Production_Readiness/
│
└── capstone-llm-api/
    ├── app/
    ├── tests/
    ├── k8s/
    ├── Dockerfile
    ├── .dockerignore
    ├── requirements.txt
    └── README.md
```

Each daily folder will contain notes, practical exercises, code samples, and commands where appropriate. Files will be added progressively as each topic is completed.

## 🚀 Getting Started

### Prerequisites

- Python and pip
- Git and GitHub
- Basic Python programming knowledge
- Docker
- Basic Kubernetes knowledge
- Access to an LLM API when beginning LLM integration

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/FastAPI_Learning_Roadmap_for_LLMOps_DevOps.git

cd FastAPI_Learning_Roadmap_for_LLMOps_DevOps
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Create a Virtual Environment

**Windows PowerShell:**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux / macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Start Learning

Begin with `Week_01_FastAPI_Foundations/Day_01_Introduction/` and proceed sequentially through the roadmap.

## 🏆 Capstone Project — LLM API Service

The final project will combine the skills learned throughout the roadmap into a production-oriented AI service.

### Planned Features

- FastAPI endpoints for health checks and AI question answering.
- Pydantic validation for incoming requests.
- External LLM API integration with configurable model settings.
- Secure configuration using environment variables and secrets.
- Automated unit and API tests using pytest.
- Mocked LLM tests for reliable CI execution.
- Docker image with appropriate runtime configuration.
- Kubernetes Deployment, Service, health probes, and resource limits.
- Prometheus metrics and Grafana dashboards.
- CI/CD automation with a mandatory test gate.

### Expected Outcome

A tested, containerized, deployable, and observable AI API that demonstrates the integration of Python, FastAPI, LLM APIs, and DevOps practices.

## 📈 Learning Progress Tracker

- [ ] Week 1 — FastAPI Foundations
- [ ] Week 2 — API Fundamentals and Automated Testing
- [ ] Week 3 — Production Basics and LLM Integration
- [ ] Week 4 — DevOps, Deployment, and Observability
- [ ] Capstone — LLM API Service

Update this checklist as you complete each milestone.

## 🔐 Security Best Practices

- Never commit API keys, tokens, passwords, or production credentials.
- Keep `.env` files out of version control.
- Use `.env.example` to document required configuration.
- Use Kubernetes Secrets or an appropriate secrets manager for deployments.
- Validate external input and handle provider errors safely.
- Use non-root containers where practical.
- Scan container images and dependencies in CI/CD.

## 🔮 Future Enhancements

After completing the roadmap, potential next steps include:

- Retrieval-Augmented Generation (RAG) endpoints.
- Streaming LLM responses.
- LLM observability and token-usage tracking.
- Rate limiting and API authentication.
- Structured logging and distributed tracing.
- Helm-based Kubernetes deployments.
- GitOps-based delivery with Argo CD.
- Advanced LLM evaluation and production monitoring.

## 👨‍💻 Learning Approach

This repository follows a hands-on learning approach:

**Learn → Practise → Test → Commit → Deploy → Monitor**

Python will be practised alongside FastAPI, with each concept reinforced through small exercises and progressively integrated into the capstone application.

The objective is not just to learn a framework, but to understand how to build and operate AI services reliably in real-world LLMOps and DevOps environments.

---

⭐ If you find this roadmap useful, feel free to star the repository and follow the learning journey.
