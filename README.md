# Billing & Admin SaaS Platform

A production-grade multi-tenant SaaS platform for billing and administration management.

## Tech Stack

- **Backend**: FastAPI + SQLAlchemy 2.0 + Alembic + PostgreSQL
- **Auth**: JWT (access+refresh), password hashing, email verification (mock)
- **Background Jobs**: Celery + Redis
- **Frontend**: React (Vite) + TypeScript + React Router + TanStack Query + Tailwind
- **DevOps**: Docker Compose
- **Quality**: pytest, ruff, mypy, pre-commit, GitHub Actions CI

## Project Structure

```
.
├── backend/          # FastAPI application
├── frontend/         # React application
├── infra/            # Docker Compose and infrastructure
└── README.md
```

## Quick Start

### Prerequisites

- Docker and Docker Compose
- Python 3.11+ (for local development)
- Node.js 18+ (for frontend development)

### Setup

1. **Copy environment variables**
   ```bash
   cp .env.example .env
   ```

2. **Start services with Docker Compose**
   ```bash
   docker compose -f infra/docker-compose.yml up -d
   ```

3. **Run database migrations**
   ```bash
   cd backend
   docker compose -f ../infra/docker-compose.yml exec api alembic upgrade head
   ```

4. **Access the API**
   - API: http://localhost:8000
   - API Docs: http://localhost:8000/docs
   - Health Check: http://localhost:8000/health

### Development

#### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
alembic upgrade head
uvicorn app.main:app --reload
```

#### Frontend

```bash
cd frontend
npm install
npm run dev
```

## API Endpoints

### Auth
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login and get JWT tokens
- `POST /auth/refresh` - Refresh access token
- `POST /auth/logout` - Logout (revoke refresh token)
- `GET /me` - Get current user info

## Environment Variables

See `.env.example` for required environment variables.

## Testing

```bash
# Backend tests
cd backend
pytest

# Linting
ruff check .
mypy app/
```

## License

MIT

