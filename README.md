# Claude SEO skills and SEO MCP server (HarborRank)

[![smithery badge](https://smithery.ai/badge/jeunewinsley9/harborrank)](https://smithery.ai/servers/jeunewinsley9/harborrank)
[![Indexed on TensorBlock MCP Index](https://mcp-index.tensorblock.co/v1/servers/harborrank-com-features-mcp-8cd89348/badge.svg)](https://tensorblock.co/mcp/servers/harborrank-com-features-mcp-8cd89348)
[![HarborRank MCP server on Glama](https://glama.ai/mcp/connectors/com.harborrank/harborrank/badges/score.svg)](https://glama.ai/mcp/connectors/com.harborrank/harborrank)

Eighteen free, MIT-licensed Claude SEO skills, plus the [HarborRank](https://harborrank.com/?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) SEO MCP server that gives them live keyword, SERP, backlink and Google Search Console data. The MCP server works in Claude, ChatGPT, Cursor, Codex and Gemini CLI, and the skills work in any agent that reads `SKILL.md` files. Every skill works on its own from web evidence and your files, and gets live numbers when HarborRank is connected.

**Contributions welcome.** Found a way to improve a skill or have a new SEO workflow to add? See [CONTRIBUTING.md](CONTRIBUTING.md) and open a PR.

Each skill is one slash command. With HarborRank connected, the skills pull live data through the [HarborRank MCP server](https://harborrank.com/docs/mcp?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills): keyword metrics, SERPs, ranked keywords, backlinks, rank tracking, Google Search Console, and Google Analytics.

## Install in Claude (web, desktop, Cowork)

1. Install **HarborRank SEO** from the plugin directory, or add the **HarborRank** connector (Customize, then Connectors).
2. Choose Connect and sign in to HarborRank with Google or email to start your 7-day free trial.
3. Back in Claude, ask for something real, for example "Find 20 low-difficulty keywords for mysite.com and save the best ones to my project" or "Which of my pages sit at positions 8 to 20 in Search Console?"

If you ask before connecting, Claude says HarborRank isn't connected, gives these steps, and picks the task back up once you say "connected".

## Install as a Claude Code plugin

One install adds the HarborRank MCP server and all eighteen skills. Inside Claude Code:

```
/plugin marketplace add harborrank/harborrank-skills
/plugin install harborrank@harborrank
```

Then run `/mcp`, pick `harborrank`, and sign in ([setup guide](https://harborrank.com/docs/skills/setup?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills)). The first MCP call opens the HarborRank login in your browser. Installed this way the skills run as `/harborrank:<name>`, for example `/harborrank:keyword-research`.

## Install in Cursor

Add the MCP server in `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "harborrank": { "url": "https://app.harborrank.com/mcp" } } }
```

Cursor opens the HarborRank login the first time it connects. This repository is also a Cursor plugin (`.cursor-plugin/`) that adds the server and the eighteen skills in one install.

## Install in ChatGPT

Add [HarborRank from ChatGPT's plugin directory](https://chatgpt.com/plugins/plugin_asdk_app_6ac8ca2f7924819194a7f81d93adda2f) and sign in when ChatGPT asks. It connects the same MCP server; the skills in this repository are for agents that read `SKILL.md` files.

## Install as a Gemini CLI extension

```
gemini extensions install https://github.com/harborrank/harborrank-skills
```

Then run `/mcp auth harborrank` in Gemini CLI to sign in. The extension adds the MCP server and the eighteen skills.

## Requirements

- A HarborRank account. Start free: new accounts get a 7-day free trial with 1,000 research credits, one project, Search Console, and Google Analytics. You add a card at signup; Basic ($29/month, 15,000 credits a month) starts when the trial ends unless you cancel from Billing first. Backlinks, lead research, and Lighthouse checks need a paid plan, and you can email support@harborrank.com within 7 days of the first charge for a full refund.
- Claude Code, Cursor or Gemini CLI (or another agent that reads `SKILL.md` files and can connect to a remote HTTP MCP server).

## What the MCP server can do

One remote server, `https://app.harborrank.com/mcp` (Streamable HTTP, OAuth 2.0 with dynamic client registration), with 41 tools:

| Area | Tools |
| --- | --- |
| Your own data (read-only) | `get_search_console_performance`, `inspect_urls`, `get_analytics_report`, `get_landing_page_performance`, `get_ai_referral_traffic` |
| Keyword research | `research_keywords`, `get_keyword_metrics`, `get_domain_keyword_suggestions`, `save_keywords`, `list_saved_keywords` |
| Live Google results | `get_serp_results`, `find_serp_competitors`, `get_local_serp_results`, `search_local_businesses`, `get_google_business_questions` |
| Competitors and links | `get_domain_overview`, `get_ranked_keywords`, `get_backlinks_overview`, `get_backlinks_profile` |
| Site audits | `run_site_audit`, `get_audit_status`, `get_audit_issues`, `get_audit_pages` |
| Rank tracking and reports | `get_rank_tracker`, `create_share_report`, `list_share_reports`, `delete_share_report` |
| Local leads for agencies | `list_business_categories`, `prospect_leads`, `research_lead`, `get_lead_teardown`, `list_leads`, `update_lead`, `set_lead_competitors`, `set_lead_serp_checks`, `set_lead_top_issues` |
| Account and projects | `whoami`, `list_projects`, `create_project`, `delete_project`, `get_upgrade_link` |

## Check that it works

After connecting, ask your agent:

1. "Which HarborRank account am I connected to?" It calls `whoami` and answers with the account and the credits left.
2. "List my HarborRank projects." It calls `list_projects`.
3. "Show the live Google results for 'best running shoes'." It calls `get_serp_results` and returns the top results.

If a call answers that the account needs a plan or more credits, the text of the reply says what to do next.

## Example prompts

- "Research keywords for a Plymouth, MA marine electrician: shortlist ten with volume, difficulty and intent, and save the good ones to my project."
- "Who ranks for my saved keywords, and where are the openings a small site could take?"
- "Which of my pages bring in leads from Google, and how much of my traffic now comes from ChatGPT and other AI assistants?"
- "Is `/pricing` indexed? If not, why not, and which of my pages are sitting at positions 8 to 20?"

## What the plugin runs, sends and fetches

- The skills are plain-text instructions. They run nothing on your machine and install no code.
- `.mcp.json` (Claude Code), `mcp.json` (Cursor) and `gemini-extension.json` (Gemini CLI) all point at one remote MCP server, `https://app.harborrank.com/mcp`, over HTTPS with OAuth 2.0. No credentials are stored in this repository.
- Tool calls send the arguments you or the agent supply (keywords, domains, URLs, a project id) to HarborRank, which fetches search data from licensed third-party providers and, when you connect a property, read-only data from your Google Search Console and Google Analytics. Nothing is sent anywhere else.
- Research and Google Analytics tools use plan credits; Search Console and saved-keyword reads use none.
- Privacy policy: https://harborrank.com/privacy?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills Terms: https://harborrank.com/terms-and-conditions?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills Support: support@harborrank.com.

## Install the skill files only

For Codex or any agent that reads `SKILL.md` files, or if you already added the MCP server by hand:

```bash
npx skills add harborrank/harborrank-skills
```

Install everything for Claude Code only:

```bash
npx skills add harborrank/harborrank-skills --skill '*' --agent claude-code
```

Or copy the folders under `skills/` into `~/.claude/skills/` (Claude Code) or `~/.codex/skills/` (Codex).

If you install the files only, connect [HarborRank MCP](https://harborrank.com/docs/mcp?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) first. The skill files are instructions, not data: without the MCP connection your agent only has what it can see on its own.

## Skills

| Command | What it does |
| --- | --- |
| [`/seo-project-setup`](https://harborrank.com/docs/skills/seo-project-setup?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Create a local workspace with goals, competitors, exports, and preferences that later sessions reuse. |
| [`/seo-context`](https://harborrank.com/docs/skills/seo-context?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Write the one-page context file (site, market, audience, competitors, goals) that every other skill reads first. |
| [`/seo-coach`](https://harborrank.com/docs/skills/seo-coach?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Pick the next workflow when you are new to SEO or unsure what to run first. |
| [`/keyword-research`](https://harborrank.com/docs/skills/keyword-research?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Turn seed topics into a prioritized keyword shortlist with volume, difficulty, intent, and SERP caveats. |
| [`/keyword-clustering`](https://harborrank.com/docs/skills/keyword-clustering?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Group a keyword list by intent, map clusters to pages, and flag cannibalization. |
| [`/competitive-landscape`](https://harborrank.com/docs/skills/competitive-landscape?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Map who wins a market, why, and where the openings are. |
| [`/competitor-analysis`](https://harborrank.com/docs/skills/competitor-analysis?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Study one competitor's keywords, pages, and backlinks and turn it into takeaways. |
| [`/seo-audit`](https://harborrank.com/docs/skills/seo-audit?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Crawl the site for technical issues, check indexing, and find why traffic dropped, with fixes ranked by impact (the crawl and Search Console checks use no credits). |
| [`/content-brief`](https://harborrank.com/docs/skills/content-brief?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Turn one target keyword into a brief built from the live SERP: questions to answer, what to add that page one lacks, outline, links, schema and title. |
| [`/local-seo`](https://harborrank.com/docs/skills/local-seo?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Check where a local business ranks in Google Maps across its service area, compare it with the businesses above it, and get a local action plan. |
| [`/client-seo-report`](https://harborrank.com/docs/skills/client-seo-report?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Write a monthly SEO report for a client or boss from Search Console, Analytics and rank tracking, and publish it as a shareable link. |
| [`/keyword-cannibalization`](https://harborrank.com/docs/skills/keyword-cannibalization?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Find queries where two of your pages compete in Search Console, fix only the splits that cost traffic, and check Google's chosen canonical. |
| [`/google-business-profile`](https://harborrank.com/docs/skills/google-business-profile?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Audit a Google Business Profile against the Maps leaders: categories, services, description, reviews, Q&A, NAP and landing page, with ready-to-paste text. |
| [`/schema-markup`](https://harborrank.com/docs/skills/schema-markup?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Find the structured data each page type has, write JSON-LD that matches the visible content, and validate it. |
| [`/ai-search-visibility`](https://harborrank.com/docs/skills/ai-search-visibility?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | See how often AI assistants send visits and cite the site, which sources they cite instead, and what to change to get cited. |
| [`/seo-proposal`](https://harborrank.com/docs/skills/seo-proposal?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Turn a prospect's teardown into an SEO proposal: current state with numbers, opportunity ranges, a 90-day plan, and a cover email. |
| [`/link-prospecting`](https://harborrank.com/docs/skills/link-prospecting?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Find qualified link prospects and the angle that makes each one relevant. |
| [`/lead-teardown`](https://harborrank.com/docs/skills/lead-teardown?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills) | Prospect local businesses in a trade and city, research each one, and get a one-page teardown to send as the pitch (research needs a paid plan). |

Docs for every skill: [harborrank.com/docs/skills](https://harborrank.com/docs/skills?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills). What the skills are for and how they compare: [Claude SEO skills built on live search data](https://harborrank.com/claude-seo-skills?utm_source=github&utm_medium=readme&utm_campaign=harborrank-skills).

## License

MIT. See [LICENSE](LICENSE) for the copyright holders.
