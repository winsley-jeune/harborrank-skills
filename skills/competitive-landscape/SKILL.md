---
name: competitive-landscape
description: Map SEO market leaders, winning content themes, keyword coverage, backlinks, and strategic gaps.
---

# HarborRank Competitive Landscape

## Goal

Answer: "Who is winning this SEO market, what content is working for them, and where are the openings?"

Use this when the user wants a market-level view across several competitors. For a deep dive on one domain, use `competitor-analysis`.

## Step 0: Check connection

Before any other step, confirm the HarborRank MCP tools are loaded. Look for `get_domain_overview` or `list_leads` among your tools, including deferred tools you can load (the name may carry a prefix such as `mcp__harborrank__`). If they are there, call `whoami`: it uses no credits, confirms the user is signed in, and returns `creditsRemaining` for budgeting the run. Do not call a research tool to test the connection.

If neither tool is available, or `whoami` fails because the user is not signed in, tell the user plainly: "HarborRank isn't connected, so I can't pull live HarborRank data yet." Then tell them how to connect it:

- Claude Code with the HarborRank plugin: run `/mcp`, choose `harborrank`, and sign in.
- Claude Code without the plugin: run `claude mcp add --transport http --scope user harborrank https://app.harborrank.com/mcp`, then `/mcp` to sign in.
- Other clients: add `https://app.harborrank.com/mcp` as a remote MCP server. Setup for each client is at https://harborrank.com/docs/mcp.

Do not stop there. Continue in fallback mode (below). If the user connects HarborRank mid-task, run Step 0 again and switch to the full workflow.

### Plan limits

On hosted HarborRank, research tools spend credits. The Free plan has 1,000 credits a month and one project; paid plans start at $29/month with 15,000 credits. Search Console, saved keywords, rank tracker reads, and site crawls use no credits. A keyword search costs about 50 credits and a domain overview about 80. Backlinks, lead research (`research_lead`), and Lighthouse checks need a paid plan.

- If `creditsRemaining` will not cover the planned calls, give the user the estimate and ask before spending. Use the free tools first.
- If a tool replies that a feature "is included in paid plans", tell the user once which feature needs a paid plan, skip that tool for the rest of the run, and finish with the other evidence. Do not retry it.
- If a tool fails for insufficient credits, stop making paid calls, tell the user, and finish with free tools and the data you already have.
- When `whoami` returns `mode: "self-hosted"`, there are no plan gates.

### Fallback mode (no HarborRank connection)

Use this mode only when Step 0 finds no connection. It works from web search, page reading, and files the user provides.

**Can still do**

- Run the market query set through web search and note which domains keep appearing.
- Group those domains by type: direct competitors, publishers, directories, communities, resources.
- Read the leaders' sites to identify the content formats, themes, and positioning that are working.
- Call the result directional.

**Must not estimate**

Traffic, search volume, keyword difficulty, CPC, keyword counts, rankings, backlink counts, Maps pack positions, and Q&A counts. Write `unknown` for each. A web search shows which pages appeared for a query when you searched, not their Google ranking: report it as "appeared in web search", never as a position.

**Output**

- Start with the label **Web-evidence only: no HarborRank data.**
- Name the source (URL or file) of every figure you report.
- End with one sentence that names the numbers this report is missing: "Connect HarborRank (the Free plan needs no card) to add each leader's organic footprint, traffic, and backlink strength." Do not add more sales copy than that.

## Required inputs

- `projectId`
- Topic, seed keywords, market/category, or user's domain
- Optional known competitors
- Optional location/language

## HarborRank MCP tools

- `research_keywords`: discover representative market queries.
- `get_keyword_metrics`: validate known query sets with volume, difficulty, intent, and trends.
- `get_serp_results`: identify recurring ranking domains across target queries.
- `find_serp_competitors`: compare domains competing across supplied keywords; use this before manual SERP counting when a keyword set is available.
- `get_domain_overview`: size organic footprint for candidate leaders.
- `get_search_console_performance`: when the user's own domain is in the comparison and Search Console is connected, anchor their position with first-party clicks/impressions/CTR rather than third-party estimates.
- `get_ranked_keywords`: find exact ranking keywords, URLs, ranks, intents, and SERP result types for leaders.
- `get_backlinks_overview`: compare backlink/referring-domain strength where relevant.
- `search_local_businesses`, `get_local_serp_results`, and `get_google_business_questions`: use for local SEO markets where proximity, Maps rankings, business categories, reviews, or Google Q&A affect who is winning.

## Workflow

1. Define the market query set:
   - Use provided keywords, or call `research_keywords` to build 5-10 representative queries.
   - Include mixed intent: informational, commercial, comparison, and tool/software terms when applicable.
   - For local SEO, include neighborhood/city/service-area queries and identify the priority locations or coordinates.
2. If the query set is already known, use `get_keyword_metrics` to validate relative demand and difficulty and `find_serp_competitors` to identify recurring domains at scale.
3. For local SEO, call `search_local_businesses` and `get_local_serp_results` for the highest-priority location(s) before synthesizing winners. Use `get_serp_results` as a complement for organic pages, not as the only local evidence.
4. Call `get_serp_results` for representative queries when live SERP composition, ranking URLs, or SERP features need inspection. Send at most 10 queries per call.
5. Identify recurring domains and group them by type:
   - Direct product competitors
   - Publishers/media
   - Marketplaces/directories
   - Communities/forums
   - Documentation/resources
6. For the strongest recurring domains, call `get_domain_overview`; default to the top 3-5 domains before expanding.
7. For direct competitors and relevant publishers, call `get_ranked_keywords`.
8. Use `get_backlinks_overview` when backlink authority appears important or the user asks why a domain is winning. Backlinks need a paid plan; on Free, skip this and continue with SERP and domain evidence.
9. Synthesize patterns: content types, themes, SERP formats, local-pack signals, authority advantages, and underserved angles.

## Output format

Start with the market read:

- Market leaders
- Most winnable opportunity area
- Biggest barrier to ranking

Then include:

| Domain | Type | Why they matter | Organic footprint | Winning themes | Weakness/gap |
| ------ | ---- | --------------- | ----------------- | -------------- | ------------ |

Add:

- Query set used
- Content formats that are working
- Keyword/theme gaps
- Backlink or authority observations
- Recommended next workflows: competitor analysis, keyword clustering, or content brief

## Guardrails

- Distinguish SEO competitors from business competitors.
- Do not overstate exact traffic when HarborRank returns estimates.
- If using a small query set, call the result directional.
- Do not assume a publisher is a product competitor; label domain types clearly.
- For local markets, distinguish organic-page winners from Maps/local-pack winners.
