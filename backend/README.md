# backend

FastAPI service: GitHub webhook intake, review/dashboard REST API, Postgres persistence, Prometheus metrics.
Calls the LangGraph pipeline from `agents/` — it does not contain agent logic itself.
Layout: `src/aria_api/{api,core,db,schemas,services,observability}`, Alembic `migrations/`, `tests/`.
