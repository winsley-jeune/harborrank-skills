# HarborRank Agent Skills

SEO workflows for Claude Code, Codex, and other agents that support `SKILL.md` files. Each skill is one slash command. The skills pull live data through the [HarborRank MCP server](https://harborrank.com/docs/mcp): keyword metrics, SERPs, ranked keywords, backlinks, rank tracking, and Google Search Console.

## Install

```bash
npx skills add winsley-jeune/harborrank-skills
```

Install everything for Claude Code only:

```bash
npx skills add winsley-jeune/harborrank-skills --skill '*' --agent claude-code
```

Or copy the folders into `~/.claude/skills/` (Claude Code) or `~/.codex/skills/` (Codex).

Connect HarborRank MCP first. The skill files are instructions, not data: without the MCP connection your agent only has what it can see on its own.

## Skills

| Command | What it does |
| --- | --- |
| `/seo-project-setup` | Create a local workspace with goals, competitors, exports, and preferences that later sessions reuse. |
| `/seo-coach` | Pick the next workflow when you are new to SEO or unsure what to run first. |
| `/keyword-research` | Turn seed topics into a prioritized keyword shortlist with volume, difficulty, intent, and SERP caveats. |
| `/keyword-clustering` | Group a keyword list by intent, map clusters to pages, and flag cannibalization. |
| `/competitive-landscape` | Map who wins a market, why, and where the openings are. |
| `/competitor-analysis` | Study one competitor's keywords, pages, and backlinks and turn it into takeaways. |
| `/link-prospecting` | Find qualified link prospects and the angle that makes each one relevant. |

Docs for every skill: https://harborrank.com/docs/skills

## License

MIT. These skills started from the open-source [OpenSEO](https://github.com/bensenescu/open-seo) project's skills and keep its license.
