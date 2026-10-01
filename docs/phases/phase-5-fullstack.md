# Phase 5 — Full-Stack Dashboard

## Goal

Turn the backend into something a recruiter can actually click through.

## In scope

- FastAPI endpoints serving dashboard data: PR history, risk scores over time, per-module/per-contributor trends, and a per-PR agent-trace view (what each node decided and why).
- Postgres schema for the above.
- Next.js dashboard consuming those endpoints: a repo-health trend view, a PR history list, and a detail view showing the full agent trace for a given PR. This detail view is the single most important screen for demos — make it good.

## Out of scope

- Any deployment or hosting (`README.md` §9, deferred).

## Deliverables / exit criteria

- A working local demo: open the dashboard, pick a PR, see the full agent trace (Injection Filter → Context → Risk → Reviewer → Verifier → Gate) with real data from a real run.

## Dependencies

Phases 0–4 (there needs to be real data flowing through the graph for the dashboard to show anything meaningful).
