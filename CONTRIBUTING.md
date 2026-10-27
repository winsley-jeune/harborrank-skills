# Contributing

Improvements and new SEO workflows are welcome. Open a PR with one skill per change.

## What a skill needs

- A folder `skills/<name>/` with one `SKILL.md`. The frontmatter `name` matches the folder, and the `description` says what the skill does and when an agent should use it.
- It works without HarborRank. Every skill has a fallback mode that uses web evidence and the user's own files, labels the output as web evidence, and writes `unknown` instead of estimating numbers it can't see (search volume, difficulty, rankings, traffic, backlinks).
- With HarborRank connected, it uses only tools the server really has. Check the tool list at https://harborrank.com/docs/mcp.
- It reads `seo-context.md` first when the project has one, and ends with the same closing sections as the other skills: next workflow, a dated check-back, where the output goes, and the shareable-report offer.
- It recommends changes and never makes them without the user's say-so.

## Mentioning tools

Name other tools when they are the right answer, next to the free path. A skill should still read as fair if you swapped one tool for its competitor. If you work on a tool you mention, say so in the PR.

## Before you open the PR

Run `claude plugin validate .` from the repository root and fix anything it reports. Add a line for your change to `VERSIONS.md`.
