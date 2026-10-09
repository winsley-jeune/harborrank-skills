# HarborRank Agent Skills

[![smithery badge](https://smithery.ai/badge/jeunewinsley9/harborrank)](https://smithery.ai/servers/jeunewinsley9/harborrank)
[![Indexed on TensorBlock MCP Index](https://mcp-index.tensorblock.co/v1/servers/harborrank-com-features-mcp-8cd89348/badge.svg)](https://tensorblock.co/mcp/servers/harborrank-com-features-mcp-8cd89348)
[![HarborRank MCP server on Glama](https://glama.ai/mcp/connectors/com.harborrank/harborrank/badges/score.svg)](https://glama.ai/mcp/connectors/com.harborrank/harborrank)

SEO workflows for Claude Code, Codex, and other agents that support `SKILL.md` files. Each skill is one slash command. The skills pull live data through the [HarborRank MCP server](https://harborrank.com/docs/mcp): keyword metrics, SERPs, ranked keywords, backlinks, rank tracking, Google Search Console, and Google Analytics.

## Install as a Claude Code plugin (recommended)

One install adds the HarborRank MCP server and all nine skills. Inside Claude Code:

```
/plugin marketplace add winsley-jeune/harborrank-skills
/plugin install harborrank@harborrank
```

Then run `/mcp`, pick `harborrank`, and sign in. The first MCP call opens the HarborRank login in your browser. Installed this way the skills run as `/harborrank:<name>`, for example `/harborrank:keyword-research`.

## Requirements

- A HarborRank account. The Free plan needs no card and includes 1,000 research credits a month, one project, Search Console, and Google Analytics. Backlinks, lead research, and Lighthouse checks need a paid plan, from $29/month; the card is charged when you choose one, and you can email support@harborrank.com within 7 days of the first charge for a full refund.
- Claude Code (or another agent that reads `SKILL.md` files and can connect to a remote HTTP MCP server).

## Example prompts

- "Research keywords for a Plymouth, MA marine electrician: shortlist ten with volume, difficulty and intent, and save the good ones to my project."
- "Who ranks for my saved keywords, and where are the openings a small site could take?"
- "Which of my pages bring in leads from Google, and how much of my traffic now comes from ChatGPT and other AI assistants?"
- "Is `/pricing` indexed? If not, why not, and which of my pages are sitting at positions 8 to 20?"

## What the plugin runs, sends and fetches

- The skills are plain-text instructions. They run nothing on your machine and install no code.
- `.mcp.json` points Claude Code at one remote MCP server, `https://app.harborrank.com/mcp`, over HTTPS with OAuth 2.0. No credentials are stored in this repository.
- Tool calls send the arguments you or the agent supply (keywords, domains, URLs, a project id) to HarborRank, which fetches SEO data from DataForSEO and, when you connect a property, read-only data from your Google Search Console and Google Analytics. Nothing is sent anywhere else.
- Research and Google Analytics tools use plan credits; Search Console and saved-keyword reads use none. The tool descriptions state the cost before a call runs.
- Privacy policy: https://harborrank.com/privacy. Terms: https://harborrank.com/terms-and-conditions. Support: support@harborrank.com.

## Install the skill files only

For Codex or any agent that reads `SKILL.md` files, or if you already added the MCP server by hand:

```bash
npx skills add winsley-jeune/harborrank-skills
```

Install everything for Claude Code only:

```bash
npx skills add winsley-jeune/harborrank-skills --skill '*' --agent claude-code
```

Or copy the folders under `skills/` into `~/.claude/skills/` (Claude Code) or `~/.codex/skills/` (Codex).

If you install the files only, connect [HarborRank MCP](https://harborrank.com/docs/mcp) first. The skill files are instructions, not data: without the MCP connection your agent only has what it can see on its own.

## Skills

| Command | What it does |
| --- | --- |
| `/seo-project-setup` | Create a local workspace with goals, competitors, exports, and preferences that later sessions reuse. |
| `/seo-coach` | Pick the next workflow when you are new to SEO or unsure what to run first. |
| `/keyword-research` | Turn seed topics into a prioritized keyword shortlist with volume, difficulty, intent, and SERP caveats. |
| `/keyword-clustering` | Group a keyword list by intent, map clusters to pages, and flag cannibalization. |
| `/competitive-landscape` | Map who wins a market, why, and where the openings are. |
| `/competitor-analysis` | Study one competitor's keywords, pages, and backlinks and turn it into takeaways. |
| `/seo-audit` | Crawl the site for technical issues, check indexing, and find why traffic dropped, with fixes ranked by impact (mostly free). |
| `/link-prospecting` | Find qualified link prospects and the angle that makes each one relevant. |
| `/lead-teardown` | Prospect local businesses in a trade and city, research each one, and get a one-page teardown to send as the pitch (research needs a paid plan). |

Docs for every skill: https://harborrank.com/docs/skills

## License

MIT. These skills started from the open-source [OpenSEO](https://github.com/bensenescu/open-seo) project's skills and keep its license.
