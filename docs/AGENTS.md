# AGENTS.md

This file is canonical coordination guidance for any AI coding agent (Claude Code, Antigravity, Codex, or any other tool) working on this repository. Read this in full before making any changes.

## Project

ARIA — see `README.md` for full architecture, tech stack, and rationale. This file does not repeat that content; it governs how agents behave while building it.

## Before starting any work

1. Read `README.md` in full.
2. Read `TASKS.md` and check which tasks are already claimed or in-progress by another agent or by the humans on the team.
3. Claim a task in `TASKS.md` (mark it in-progress, note which agent/tool claimed it) before writing any code for it.
4. Work phase by phase, in the order laid out in `docs/phases/` — don't jump ahead to a later phase's tasks unless explicitly instructed to.

## While working

- Follow the repo structure in `README.md` §12. Don't introduce a new top-level layout.
- Keep all configuration (API URLs, DB connection strings, model paths, secrets) in environment variables, never hardcoded — this project will be deployed later and config needs to stay portable.
- Preserve the decision/advisory separation described in `README.md` §4.3: any code path that makes the actual merge/gate decision must be fed only by the Risk Agent's numeric score, never by raw LLM text output. Do not simplify this away for convenience, even temporarily.
- Write tests alongside the code you add, not as a separate later pass.
- Update `TASKS.md` as you complete work — mark tasks done, note anything you deferred or left as a stretch goal.
- If you hit a design decision not covered by `README.md` or the relevant phase file, leave a clearly marked `TODO(agent):` comment in the code and log it under "Open questions / decisions needed" in `TASKS.md` rather than deciding silently.

## Rules

- **Never add yourself (the AI agent/tool) as a contributor, co-author, or author anywhere in the project.** This includes commit metadata, `README.md`, package manifests, code comments, and any contributors/credits file. Authorship belongs to the humans on the team only.
- Don't rewrite or delete another agent's in-progress work noted in `TASKS.md` without flagging it first.
- Don't introduce new third-party services or paid tiers not already named in `README.md` without flagging it in `TASKS.md`.
- Don't touch deployment/hosting configuration — that decision is explicitly deferred (see `README.md` §9 and `docs/phases/phase-7-deployment.md`). Just keep everything Dockerized and config-driven so the decision can be made later without rework.

## Multi-agent coordination

More than one AI coding tool may work on this repo at different times (e.g. one tool for core feature work, another reserved for CI/CD-specific phases). `TASKS.md` is the single source of truth for who is doing what — always check it before starting, and update it before stopping, so two agents never collide on the same file at the same time.
