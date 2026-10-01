# Phase 0 — Scaffolding & Baseline Agent Graph

## Goal

Stand up the repo skeleton and a working-but-stubbed LangGraph pipeline end-to-end, so every later phase has somewhere real to plug into.

## In scope

- Repo structure exactly as `README.md` §12.
- Docker Compose file bringing up Qdrant, Postgres, a FastAPI stub, a Next.js stub, and Prometheus/Grafana stubs — these don't need to do anything real yet, just need to start cleanly together.
- A LangGraph `StateGraph` with all six nodes (Injection Filter, Context, Risk, Reviewer, Verifier, Gate) wired in the order from `README.md` §2. Each node is initially a stub that passes state through (e.g. the Risk node always returns a fixed score) so the graph's wiring is provably correct before any real logic exists.
- A FastAPI endpoint that receives a GitHub webhook payload and logs it — no real processing yet.
- `.env.example` listing every config variable the project will eventually need (DB URL, Qdrant URL, model path, etc.), even for things not built yet, so later phases don't invent undocumented config.

## Out of scope

- Any real model inference, fine-tuning, retrieval, or security logic — those are later phases.
- Deployment or hosting of any kind.

## Deliverables / exit criteria

- `docker compose up` brings up every service without errors.
- A manually-triggered test run pushes a dummy payload through the full graph stub end-to-end and logs each node's execution in order.
- `.env.example` is complete enough that a new developer can copy it to `.env` and know what every variable is for.

## Dependencies

None — this is the starting point.
