# Versions

## 1.12.1
- `ai-search-visibility` uses the new AI visibility tools: `get_ai_brand_visibility` for mentions and share of voice, `ask_ai_models` to sample ChatGPT, Claude, Gemini and Perplexity, and `get_ai_brand_tracking` for the trend. `get_serp_results` now returns the AI Overview text and the pages it cites. Asking the assistants by hand stays as the fallback without a paid plan.

## 1.12.0
- `local-seo` scans a grid of points with `run_local_grid` (saved as a heatmap in the project) and re-runs the same grid at check-back; sampling points by hand stays as the fallback.
- `lead-teardown` can add a grid scan for the leads the user pitches first.
- `competitor-analysis` offers to keep watching the competitor in the user's rank tracker with `add_rank_tracker_competitors`.
- These skills say which extras need Pro or Agency (7x7 grids, more than 3 tracked competitors), pass on the Pro link once and carry on with the smaller option.

## 1.11.1
- When a tool says the free trial hasn't started or credits ran out, every skill passes the link on exactly as written and waits.
- Upgrades are paid by card.

## 1.11.0
- New skills: `keyword-cannibalization`, `google-business-profile`, `schema-markup`, `ai-search-visibility` and `seo-proposal`.

## 1.10.0
- New skills: `seo-context` (the one-page context file every workflow reads first), `local-seo`, `content-brief` and `client-seo-report`.
- Every workflow reads `seo-context.md` first when the project has one.
- README: contributions welcome, tracked links.

## 1.9.0
- Every workflow ends with one dated follow-up, saved to the project README; `seo-coach` opens with any follow-up that is due.
- Workflows offer a weekly scheduled check where scheduled tasks are available.

## 1.8.1
- The connect step leads with the 7-day free trial.
