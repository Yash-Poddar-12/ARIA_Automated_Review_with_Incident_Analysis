# Phase 1 — Fine-Tuning (LoRA / QLoRA)

## Goal

Produce a fine-tuned Reviewer-agent model (and optionally a LoRA-adapted embedding model) trained on Colab/Kaggle, then merged and quantized for local serving.

## In scope

- Source and clean a dataset of PR review comments + outcomes (a public corpus such as CodeReviewer, and/or a scraped subset from a few open-source repos via the GitHub API).
- QLoRA training notebook — base model Qwen2.5-Coder-1.5B/3B-Instruct or CodeGemma-2B, run on Colab's or Kaggle's free GPU tier.
- Merge the trained LoRA adapter into the base weights; quantize to GGUF.
- Stand up local serving via Ollama or llama.cpp.
- (Stretch) LoRA-adapt a small embedding model on incident-similarity pairs for the retrieval step — fine to slip to a later pass if time is tight.
- A before/after evaluation report: precision/recall on a held-out set for "did the model correctly flag a diff that later caused a real incident" — not text-similarity metrics like BLEU/ROUGE.

## Out of scope

- Wiring the fine-tuned model into the live LangGraph pipeline (that's a matter of replacing Phase 0's Reviewer stub, and can happen whenever this phase's model is ready).
- Production-grade serving (vLLM multi-LoRA) — documented as the production target in `README.md` §3, not built in this phase.

## Deliverables / exit criteria

- A merged, GGUF-quantized model artifact, versioned in MLflow (a minimal local MLflow instance is fine at this stage).
- Training notebook saved under `ml/training/reviewer_qlora/` and `ml/notebooks/`.
- Eval report (markdown or notebook output) showing before/after numbers.

## Dependencies

Phase 0 (repo structure, `.env.example` conventions).
