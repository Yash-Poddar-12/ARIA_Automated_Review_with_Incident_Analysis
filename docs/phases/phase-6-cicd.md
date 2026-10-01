# Phase 6 — CI/CD Integration

## Goal

Make the whole system trigger itself the way it's meant to in production: a real GitHub webhook kicking off a real graph run, gated by the security and prompt regression suites.

## In scope

- A GitHub Actions workflow (or the FastAPI webhook handler, depending on final design) that runs the full LangGraph pipeline on PR open/update events against a real or test repo.
- CI gate: the red-team security suite (Phase 2) and the golden-set prompt regression suite (Phase 3) must both pass before any change to `main` is allowed to merge — eat your own dog food.
- Wire Prefect's scheduled retraining trigger (Phase 4) into this CI/CD layer if not already done.

## Out of scope

- Deployment itself (`README.md` §9).

## Deliverables / exit criteria

- Opening a real test PR against the demo repo triggers a real end-to-end run, visible in the dashboard (Phase 5) and logged in LangSmith.
- A deliberately-broken prompt or a deliberately injection-vulnerable change gets caught and blocked by CI before merge.

## Dependencies

All prior phases.
