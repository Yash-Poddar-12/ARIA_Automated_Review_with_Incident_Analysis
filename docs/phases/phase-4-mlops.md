# Phase 4 — MLOps & Observability

## Goal

Make the project's model/adapter lifecycle and retrieval quality trackable over time, not just "it worked once."

## In scope

- MLflow registry: each LoRA adapter and each version of the risk classifier tracked as a model version, with its eval metrics attached.
- Prefect flow(s) for recurring jobs (e.g. periodic reindexing of retrieval data, a scheduled retraining trigger once enough new labeled outcomes accumulate).
- RAGAS/DeepEval harness run against the Context Agent's retrieval, tracked over time.
- Prometheus metrics exported from the FastAPI backend (request latency, per-node graph execution time, injection-filter flag rate); Grafana dashboards built on top.

## Out of scope

- Airflow — intentionally using Prefect instead given the local hardware constraints (`README.md` §8). Revisit only if a specific target role calls for Airflow by name.

## Deliverables / exit criteria

- MLflow UI shows a real history of adapter/classifier versions with metrics attached.
- Grafana dashboard shows at least: request latency, injection-filter flag rate, and retrieval-quality score over time.

## Dependencies

Phase 1 (models to track), Phase 2 (injection-filter metric to surface).
