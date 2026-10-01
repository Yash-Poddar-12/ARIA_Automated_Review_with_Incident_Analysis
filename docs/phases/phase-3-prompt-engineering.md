# Phase 3 — Prompt Engineering & Verifier

## Goal

Replace stubbed prompts with real, versioned, schema-enforced prompts, and add the Verifier agent.

## In scope

- Per-agent system prompts, stored as versioned files (not inline strings scattered through code), with a clear naming/versioning convention.
- Structured JSON output from the Reviewer Agent (risk score, cited incident IDs, comment text), validated against a Pydantic schema, with retry logic on schema violation.
- Dynamic few-shot examples pulled from the Context Agent's retrieved incidents at request time, rather than static examples baked into the prompt.
- Verifier agent: a second LLM pass (can reuse the same fine-tuned model with a different system prompt) that checks whether the Reviewer's cited incidents are real and relevant, and flags or downgrades confidence if not.
- A golden-set of PRs with known-good expected review outcomes, used for prompt regression testing.

## Out of scope

- CI wiring of the regression tests (that's Phase 6), though the test suite itself is built here.

## Deliverables / exit criteria

- Reviewer output reliably validates against its schema (track the retry rate — it should be low in steady state).
- A golden-set regression suite exists and passes against the current prompt set.

## Dependencies

Phase 1 (needs the fine-tuned model to prompt against), Phase 2 (prompts must respect the trust-boundary rules for untrusted content).
