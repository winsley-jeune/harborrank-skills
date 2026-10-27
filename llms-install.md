# Installing HarborRank MCP (for AI agents such as Cline)

HarborRank is a hosted (remote) MCP server. There is nothing to clone, build or run locally, and no API key to paste.

1. Add this server to the MCP settings file (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "harborrank": {
      "type": "streamableHttp",
      "url": "https://app.harborrank.com/mcp",
      "timeout": 120
    }
  }
}
```

2. The server answers with `401` until the user signs in. That is expected. Tell the user to click **Authenticate** next to `harborrank` in the MCP servers panel. Their browser opens the HarborRank sign-in page; after they sign in and approve access, the client reconnects on its own. New accounts start with a 7-day free trial.

3. Confirm the connection by calling the `whoami` tool. It returns the signed-in user and workspace. Do not test with a research tool.

4. Most tools take a `projectId`. Call `list_projects` first and use the `id` it returns. If there are no projects, call `create_project` with the user's site.

Some research calls take 20 to 60 seconds, so keep the timeout at 120 seconds or more.

Optional: the `skills/` folder in this repository holds eighteen SEO workflows (keyword research, competitor analysis, site audit and more) as `SKILL.md` files that any agent can follow.

Docs: https://harborrank.com/docs/mcp · Support: support@harborrank.com
