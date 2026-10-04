# DATASETS.md

Data sources for ARIA, by purpose and phase. Nothing here is needed for Phase 0.

**Rules for agents and humans**
- Never commit raw or processed data to git (`ml/data/` is git-ignored). Store download/prep scripts in `ml/training/<model>/` or `scripts/`, not the data itself.
- Before using any dataset, check that it still exists and read its license. Hugging Face dataset names and Zenodo links change; treat the identifiers below as starting points to verify, not guaranteed paths.
- Record the exact source, version/commit, license, and date downloaded in `ml/data/SOURCES.md`.
- Large downloads and all training happen on Colab/Kaggle, not the local 4GB-VRAM laptop.

## 1. Reviewer model (QLoRA fine-tuning) — Phase 1

| Dataset | Use | Notes |
|---|---|---|
| **CodeReviewer** (Microsoft, Li et al. 2022) | Core data: diff hunk -> human review comment, plus quality estimation and code refinement splits | Primary dataset. Distributed via the paper's GitHub repo / Zenodo. |
| **Mined PR review comments** (GitHub API) | Supplement with data from 5-10 well-reviewed open-source repos (permissive licenses) | Pull merged PRs, review comments, and the diff each comment is attached to. Respect API rate limits; use a token. |

Training format: instruction-style pairs (system prompt + diff + retrieved context -> structured JSON review). Hold out whole repositories, not random rows, to avoid leakage.

## 2. Risk classifier (defect risk of a diff) — Phase 1

| Dataset | Use | Notes |
|---|---|---|
| **ApacheJIT** | Just-in-time (commit-level) defect labels across Apache projects | Closest match to "does this change introduce a bug." |
| **Defectors** | Python-focused commit-level defect dataset | Useful if you want language coverage beyond Java. |
| **SZZ-labelled commits (self-built)** | Label bug-introducing commits in repos you mine yourself (SZZ algorithm, e.g. PyDriller-based) | Gives you labels tied to your own retrieval corpus. |
| Devign / BigVul / CVEfixes / DiverseVul | Optional: security-vulnerability labels as an extra "security risk" signal | Function-level, so a different task from commit-level defects; use as an auxiliary feature, not the main label. |

Split by time (train on older commits, test on newer) to mimic real deployment.

## 3. Incident memory corpus (what the Context Agent retrieves) — Phase 1 / 4

ARIA's differentiator needs a corpus of "past incidents." You have no private incident history, so build one from public sources:

- **Public postmortem collections** (e.g. the community-curated `danluu/post-mortems` list) — scrape/summarize the linked postmortems into short incident records.
- **Bug-fix commits and linked issues** from the same repos used above: each fix commit + issue discussion becomes an incident ("what broke, what fixed it, which files").
- **Style guides / contributing docs / past review comments** from those repos.

Each record needs: id, title, summary, affected files/modules, root cause, source URL. The Reviewer's citations must point at these ids.

## 4. Prompt-injection classifier and red-team suite — Phase 2

| Dataset | Use | Notes |
|---|---|---|
| **deepset/prompt-injections** (HF) | Labelled injection vs benign text; quick baseline | Small. |
| **Lakera Gandalf datasets** (HF) | Injection attempts from a public game | Check current names/licenses. |
| **BIPIA** (indirect prompt injection benchmark) | Indirect injection through retrieved/ingested content, which matches ARIA's threat model | Most relevant to ARIA. |
| **Jailbreak / safe-guard prompt-injection sets on HF** | Extra positives and negatives | Verify quality before training on them. |
| **Self-written code-specific attacks** | Injections hidden in diff comments, docstrings, PR descriptions, commit messages, linked issue text | Essential: public sets are chat-oriented, not code-review-oriented. These become `evals/red_team/`. |

## 5. Embedding adaptation (stretch) — Phase 1

- Positive pairs from your own corpus: (diff, past incident it resembles / the fix that followed).
- **CodeSearchNet** as general code-text pairs if you need more volume.

## 6. Evaluation sets

- `evals/golden_set/`: 30-50 hand-picked PRs with known-good expected outcomes (write these yourselves from the mined data).
- `evals/retrieval/`: question/relevant-incident pairs for RAGAS/DeepEval.
- Held-out repositories never seen in training, for the final before/after report.

## 7. Base models (not datasets, but downloaded in Phase 1)

- Reviewer: Qwen2.5-Coder 1.5B or 3B Instruct (or CodeGemma 2B).
- Embeddings: a small open code/text embedding model (e.g. a BGE-small class model).
- Verify current availability and license on Hugging Face before starting.
