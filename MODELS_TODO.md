# Candidate models to add later

Chinese-origin LLM families available on OpenRouter (catalog snapshot 2026-06-30,
337 total models) that the router does **not** currently cover. Verify slugs with
`py router.py --validate-models` after adding any of these — slugs drift.

> Note: `cost_score` / `quality_score` in `router.py` are subjective heuristics,
> not benchmarked. Assign them deliberately when adding a family.

## New families (not in the table at all)

| Family | Slug(s) | Status / notes |
|---|---|---|
| **StepFun** | `stepfun/step-3.7-flash`, `stepfun/step-3.5-flash` | Cheap/fast general models. Best near-term candidate. |
| **Tencent Hunyuan** | `tencent/hy3-preview`, `tencent/hunyuan-a13b-instruct` | `hy3-preview` is newest but a preview build. |
| **Baidu ERNIE** | `baidu/ernie-4.5-vl-424b-a47b` | Only a vision (VL) variant exposed right now; wait for a standard chat build. |
| **ByteDance** | `bytedance/ui-tars-1.5-7b` | Niche GUI-agent vision model, not general chat. Skip unless needed. |

## Recommendation when revisiting

1. Add **StepFun** (`step-3.7-flash`) first — real general-purpose cheap model, fills the low-cost tier.
2. Consider **Hunyuan** (`hy3-preview`) once it leaves preview.
3. Hold **ERNIE** until a non-VL chat model ships.
4. Skip **ByteDance UI-TARS** unless a GUI-agent use case appears.

## Also noted (within existing families, not yet added)

- Qwen coding-specialized: `qwen/qwen3-coder-plus`, `qwen/qwen3-coder-next` — could strengthen the `coding` route.
- Qwen mid-tier: `qwen/qwen3.6-plus` / `qwen/qwen3.7-plus` — a balanced tier between flash and max.
- GLM cheap/fast: `z-ai/glm-4.7-flash`; GLM vision: `z-ai/glm-5v-turbo`.
