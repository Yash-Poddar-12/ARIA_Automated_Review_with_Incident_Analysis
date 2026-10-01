# Phase 2 — Security Hardening (Prompt Injection Defense)

## Goal

Make the Injection Filter real, and make the decision/advisory separation (`README.md` §4.3) an enforced architectural property rather than just a design intent.

## In scope

- Injection-detection pre-filter: regex heuristics for known injection patterns plus a small classifier (can reuse Phase 1's fine-tuning skills at a smaller scale) that flags suspicious PR text, diff content, and comments before it reaches any agent's context window.
- Logging for flagged content — never silently drop it; always record what was caught and why.
- Enforce in code, not just by convention, that the Gate Node only ever reads the Risk Agent's numeric score field from the graph state — it should be structurally impossible for the Reviewer or Verifier's text output to influence the Gate Node's decision. Consider a type-level or schema-level guarantee (e.g. the Gate Node's input type simply doesn't include the LLM text fields).
- Red-team test suite: a folder of crafted adversarial PRs attempting various injection strategies, each with an expected "safe" outcome defined.
- Hook point for CI (the suite itself is built here; wiring it into the pipeline happens in Phase 6).

## Out of scope

- Prompt-level engineering beyond what's needed for the filter itself — the full prompt engineering work is Phase 3.

## Deliverables / exit criteria

- Red-team suite passes on 100% of currently-known attack patterns.
- A short writeup (can live under `docs/`) explaining the threat model and each defense layer — useful both as documentation and as interview prep material.

## Dependencies

Phase 0 (graph skeleton to harden).
