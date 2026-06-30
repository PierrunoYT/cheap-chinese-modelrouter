# router.py review

## Strengths
- Clean structure: dataclasses, clear separation of classify -> route -> chat -> call.
- Fallback chain across models with early-exit on auth errors and exponential backoff.
- Task classification is pragmatic (regex heuristics + token estimate for long-context).
- `--dry-run` is great for testing routing without spending tokens.
- Modes (auto/cheap/balanced/quality) give useful knobs.

## Weaknesses (all addressed)
1. ~~**Token estimate is naive**~~ -- FIXED: CJK-aware `estimate_tokens` (2 tokens/CJK char, 4 chars/token Latin).
2. ~~**No streaming**~~ -- FIXED: `--stream` flag + `StreamResult` iterator with fallback before first chunk.
3. ~~**No message history support**~~ -- FIXED: `chat(history=...)` and `--history file.json` wire prior turns through.
4. ~~**Classification is keyword-only**~~ -- IMPROVED: creative/translation intent checked before generic coding keywords; "write a story about bugs" -> creative.
5. ~~**Hardcoded model slugs**~~ -- FIXED: `--validate-models` checks slugs against OpenRouter's live `/models` catalog.
6. ~~**No retry on 429/5xx**~~ -- FIXED: `_is_retryable`/`_is_auth_error` split, `Retry-After`-aware backoff, non-retryable errors skip to next model.
7. ~~**Cost/quality scores subjective**~~ -- DOCUMENTED: comment clarifies they are heuristics for ordering only, not pricing/benchmarks.
8. ~~**No tests**~~ -- FIXED: `tests/test_router.py` (24 unittest cases, no network).
9. ~~**`reasoning` extra_body sent blindly**~~ -- FIXED: `_create` retries once without `extra_body` on a 400.

## Verdict
Heuristics remain heuristics (classification is still keyword-based and scores are
hand-tuned), but the structural gaps are closed: CJK-aware budgeting, streaming,
multi-turn, smarter retries, slug validation, and a test suite. Reasonable for
personal/CLI use; for production you'd still want a real tokenizer and benchmark-driven scores.
