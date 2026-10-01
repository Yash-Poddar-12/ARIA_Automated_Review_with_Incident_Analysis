# TASKS.md

Living task tracker. Claim a task (mark in-progress + which agent/person) before starting; mark done when finished, with a one-line note on what was actually delivered. This file exists specifically to prevent two agents from colliding on the same work — check it before you start anything, and update it before you stop.

## Status legend

- `[ ]` not started
- `[~]` in progress — claimed by: _(agent/person)_
- `[x]` done — delivered: _(short note)_

## Phase 0 — Scaffolding & Baseline Agent Graph

- [x] Repo structure per README §12 — delivered: scaffold with folders, module READMEs, .gitignore, .env.example
- [ ] Docker Compose skeleton (Qdrant, Postgres, FastAPI, Next.js, Grafana/Prometheus stubs)
- [ ] LangGraph StateGraph skeleton with stubbed Injection Filter / Context / Risk / Reviewer / Verifier / Gate nodes
- [ ] GitHub webhook receiver (stub) in FastAPI
- [ ] `.env.example` covering every config variable the project will eventually need

## Phase 1 — Fine-Tuning

- [ ] Dataset sourcing + cleaning
- [ ] QLoRA training notebook (Colab/Kaggle)
- [ ] Adapter merge + GGUF quantization
- [ ] Local serving via Ollama/llama.cpp
- [ ] Before/after eval report
- [ ] (Stretch) LoRA-adapted embedding model for retrieval

## Phase 2 — Security Hardening

- [ ] Injection-detection pre-filter (regex + small classifier)
- [ ] Decision/advisory separation structurally enforced in Gate Node
- [ ] Red-team test PR suite
- [ ] CI job running the red-team suite

## Phase 3 — Prompt Engineering & Verifier

- [ ] Per-agent versioned system prompts
- [ ] Structured JSON output + schema validation (Reviewer)
- [ ] Dynamic few-shot from Context Agent retrieval
- [ ] Verifier agent (citation sanity-check)
- [ ] Golden-set prompt regression tests

## Phase 4 — MLOps & Observability

- [ ] MLflow registry (adapters + risk classifier versions)
- [ ] Prefect flow(s) for scheduled retraining/reindexing
- [ ] RAGAS/DeepEval retrieval-quality harness
- [ ] Prometheus metrics + Grafana dashboards

## Phase 5 — Full-Stack Dashboard

- [ ] FastAPI endpoints for dashboard data
- [ ] Postgres schema (PR history, risk scores, review outcomes)
- [ ] Next.js dashboard (repo-health trends, PR history, agent trace view)

## Phase 6 — CI/CD Integration

- [ ] GitHub Actions workflow: webhook → full graph run on PR events
- [ ] CI gating: security suite + prompt regression suite must pass before merge to main
- [ ] Automated retrain trigger wiring (Prefect ↔ CI)

## Phase 7 — Deployment (deferred — see README §9)

- [ ] Confirm current hosting terms before committing to a platform
- [ ] Confirm everything is containerized + env-var configured (should already be true from Phase 0)
- [ ] Deploy decision + execution — intentionally left open until closer to completion

## Open questions / decisions needed

_(agents: log anything ambiguous here instead of deciding silently)_
