# Setup Guide

## Phase 1: Foundation Setup

### Prerequisites
- Docker and Docker Compose installed
- Python 3.11+ (for local development)
- Git

### Step 1: Environment Configuration

Create a `.env` file in the project root with the following content:

```env
# Database
DATABASE_URL=postgresql://postgres:postgres@postgres:5432/saas_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=saas_db

# Redis
REDIS_URL=redis://redis:6379/0

# JWT
JWT_SECRET_KEY=your-secret-key-change-in-production-min-32-chars
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=15
REFRESH_TOKEN_EXPIRE_DAYS=7

# Email (Mock)
EMAIL_FROM=noreply@example.com
EMAIL_BACKEND=mock

# Billing Webhook Secret (for fake Stripe)
BILLING_WEBHOOK_SECRET=whsec_fake_webhook_secret_for_dev

# CORS
CORS_ORIGINS=http://localhost:5173,http://localhost:3000

# Environment
ENVIRONMENT=development
```

### Step 2: Start Docker Services

```bash
docker compose -f infra/docker-compose.yml up -d
```

This will start:
- PostgreSQL database
- Redis
- FastAPI backend (with hot reload)
- Celery worker
- Celery beat

### Step 3: Run Database Migrations

```bash
cd backend
docker compose -f ../infra/docker-compose.yml exec api alembic upgrade head
```

Or if running locally:

```bash
cd backend
alembic upgrade head
```

### Step 4: Verify Setup

1. Check health endpoint: http://localhost:8000/health
2. View API docs: http://localhost:8000/docs

### Step 5: Test Registration

```bash
curl -X POST "http://localhost:8000/api/v1/auth/register" \
  -H "Content-Type: application/json" \
  -d '{"email": "test@example.com", "password": "testpassword123"}'
```

### Step 6: Test Login

```bash
curl -X POST "http://localhost:8000/api/v1/auth/login" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=test@example.com&password=testpassword123"
```

## Local Development (Without Docker)

### Backend Setup

```bash
cd backend
python -m venv venv
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

pip install -r requirements.txt
alembic upgrade head
uvicorn app.main:app --reload
```

## Troubleshooting

- **Database connection errors**: Ensure PostgreSQL container is running and healthy
- **Port conflicts**: Change ports in `docker-compose.yml` if 8000, 5432, or 6379 are in use
- **Migration errors**: Make sure database is running before running migrations


