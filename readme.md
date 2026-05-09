# Python Web Course Assignment: Docker Basics with FastAPI

## Assignment Overview

This project is an academic assignment from the Python Web course.
The goal is to containerize a simple FastAPI application and connect it to PostgreSQL using Docker Compose.

## Learning Objectives

- Build and run a Python web app in Docker.
- Configure a PostgreSQL service in a separate container.
- Connect FastAPI to PostgreSQL using SQLAlchemy.
- Verify service health with an API endpoint.

## Tech Stack

- Python 3.10+
- FastAPI
- Uvicorn
- SQLAlchemy
- PostgreSQL 15 (Alpine)
- Docker & Docker Compose

## Project Structure

```text
.
├── main.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── conf/
│   └── db.py
├── static/
└── templates/
```

## API Endpoints

- `GET /` — renders HTML template.
- `GET /healthchecker` — checks database connectivity (`SELECT 1`).

## Run Locally (without Docker)

1. Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Make sure PostgreSQL is running and available at:

```text
postgresql+psycopg2://postgres:567234@localhost:5432/hw02
```

Or set your own URL:

```bash
export DATABASE_URL="postgresql+psycopg2://<user>:<password>@<host>:<port>/<db_name>"
```

4. Start the app:

```bash
python main.py
```

5. Open:

- `http://localhost:8000/`
- `http://localhost:8000/healthchecker`

## Run with Docker Compose

Build and start services:

```bash
docker compose up -d --build
```

Check status:

```bash
docker compose ps
```

Check DB health endpoint:

```bash
curl -i http://localhost:8000/healthchecker
```

Stop services:

```bash
docker compose down
```

## Notes

- Database URL is read from `DATABASE_URL` in `conf/db.py`.
- If `DATABASE_URL` is not provided, local fallback is used:
	`postgresql+psycopg2://postgres:567234@localhost:5432/hw02`.
- Inside Docker Compose, the DB host must be the service name: `db_postgres`.

## Course Context

This repository demonstrates practical skills for the Docker topic in a Python Web lesson:
containerizing a backend service, connecting multi-container services, and validating runtime connectivity.

