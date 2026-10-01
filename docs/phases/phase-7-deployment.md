# Phase 7 — Deployment (deferred)

## Goal

Get the finished project live, once it's actually finished enough to be worth deploying.

## Status

**Intentionally deferred.** Don't start this phase until the rest of the system works end-to-end locally. Hosting terms for the free-tier platforms under consideration (frontend, backend, model serving, database, vector store) move quickly — reconfirm current terms before committing to any of them. See `README.md` §9 for the direction under consideration as of now.

## What should already be true by the time this phase starts

- Everything is Dockerized.
- All config (API URLs, DB connection strings, model paths, secrets) comes from environment variables — nothing hardcoded.
- The app works fully from `docker compose up` locally with no manual steps.

If those three things hold, the actual deployment decision and execution should be a short phase, not a rework.

## Dependencies

All prior phases.
