# agents

LangGraph pipeline: Injection Filter -> Context -> Risk -> Reviewer -> Verifier -> Gate.
`graph/` StateGraph + checkpointer · `nodes/` one module per agent · `state/` typed graph state
`prompts/` versioned system prompts · `guardrails/` injection filter + decision/advisory separation (README §4).
