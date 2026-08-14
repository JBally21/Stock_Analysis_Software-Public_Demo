# Stock Analysis Site
A full-stack stock research and portfolio-tracking application that combines market data, saved portfolio information, and generated stock summaries.

> **Source Availability:** The implementation is maintained in a private repository. This public repository contains project documentation, architecture, demonstrations, and a view of the codebase structure without publishing source code.

## Demo

(DEMO)

## What It Does

This site is designed as a single workspace for researching and tracking stocks. Users can create an account, request a focused stock analysis, save companies to a portfolio, and return to previously tracked companies.

The analysis workflow runs asynchronously so the frontend can submit a stock request, continue polling for job status, and display the result when processing finishes.

## Key Features

- User registration and login with hashed-password storage
- Stock lookup and generated company summaries
- Background analysis jobs with status polling
- Portfolio persistence by user account
- PostgreSQL-backed application data
- Local LLM-based analysis workflow
- Retrieval-augmented context using Chroma
- News/data collection used by the analysis pipeline
- Responsive React interface built with Bootstrap

## Tech Stack

### Frontend

- React
- Vite
- React Router
- Bootstrap

### Backend

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL
- Pydantic

### AI / Data Pipeline

- Hugging Face Transformers
- Sentence Transformers
- Chroma vector database
- LangChain integrations
- Selenium

### Infrastructure

- Redis caching — frequently requested stock data and other short-lived results to reduce unnecessary repeated processing and database/API work.
- Docker — containerize the application and simplify local setup and service orchestration.

## Architecture

See [`docs/architecture.md`](docs/architecture.md) for a more detailed explanation.

## Project Structure

```text
project/
├── frontend/
│   ├── public/
│   └── src/
│       ├── assets/
│       ├── components/
│       │   ├── analysis interface
│       │   ├── navigation
│       │   ├── stock cards
│       │   └── shared UI
│       ├── pages/
│       │   ├── home
│       │   ├── dashboard
│       │   ├── portfolio
│       │   └── authentication
│       └── styles/
│
├── backend/
│   ├── database/
│   │   ├── connection / session management
│   │   ├── models
│   │   └── data-access helpers
│   ├── processes/
│   │   ├── LLM analysis
│   │   ├── retrieval pipeline
│   │   ├── news collection
│   │   └── utilities
│   └── API application
│
├── vector-store/
└── configuration/
```

This structure is intentionally descriptive rather than a one-to-one copy of the private repository.

## How the Analysis Flow Works

1. The user enters a ticker in the React frontend.
2. The frontend submits the request to FastAPI.
3. The backend creates a background analysis job and immediately returns a job identifier.
4. The frontend polls the job endpoint for completion.
5. The analysis service gathers relevant context and retrieves related information from the vector store.
6. The local language-model pipeline produces a focused summary.
7. The completed result is returned to the frontend.
8. The user can save the stock to their portfolio for later review.

## Engineering Decisions

### Asynchronous analysis requests

Stock analysis can take longer than a normal API request. The application separates job submission from result retrieval so the UI remains responsive while analysis runs.

### Separate relational and vector storage

PostgreSQL stores structured application data such as users, portfolio relationships, and stock records. Chroma is used separately for similarity-based retrieval in the analysis pipeline.

### Private implementation, public engineering documentation

The source repository remains private, while this repository documents the system design, product behavior, and engineering decisions. This makes the project reviewable without exposing implementation details that may be reused or developed further.

## Roadmap

- [ ] Improve analysis job persistence beyond in-memory job state
- [ ] Expand automated backend and frontend testing
- [ ] Add deployment and production configuration

## Screenshots

### Dashboard

_Add `media/screenshots/dashboard.png`._

### Generated Stock Analysis

_Add `media/screenshots/stock-summary.png`._

### Portfolio

_Add `media/screenshots/portfolio.png`._

## More Documentation

- [Architecture](docs/architecture.md)
- [Technical Decisions](docs/technical-decisions.md)
- [Project Structure](docs/project-structure.md)
- [Demo Capture Guide](docs/demo-guide.md)

## Repository Note

This repository is a portfolio showcase and intentionally does not include application source code, environment files, database contents, model artifacts, browser profiles, or private configuration.
