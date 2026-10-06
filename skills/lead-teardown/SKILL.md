---
name: lead-teardown
description: "For agencies and freelancers who sell SEO to local businesses: prospect a trade in a city from Google Maps, shortlist the best leads, research each one (three-point Maps pack check, top competitors, site, contact), and produce a one-page teardown plus outreach emails to pitch with. Use when the user wants local SEO leads, prospects or clients, a sales teardown of a local business, or cold outreach to businesses such as roofers, dentists, or electricians."
---

# HarborRank Lead Teardown

## Goal

Turn a trade and a city into a short list of local businesses worth pitching, each with a one-page teardown built from real data: where they show up in Google Maps from three points in their service area, what the top three profiles have that they do not, what their website earns, and the first three fixes. The teardown is the sales document; the agency sends it, the business owner reads their own numbers.

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

- Find businesses in the trade and city with web search. Record each one's name, website, and public rating and review count, with the source.
- Read their sites: services listed, service area, city pages, calls to action, and obvious gaps.
- Compare them with the sites that appear at the top of web search for the main trade-and-city query.
- Apply the shortlist rules (has a website, 20 or more reviews at 4.3 or better, not a chain).
- Call the result a shortlist, never a teardown. The pitch only works when the owner sees their own numbers, and those come from `research_lead`.

**Must not estimate**

Traffic, search volume, keyword difficulty, CPC, keyword counts, rankings, backlink counts, Maps pack positions, and Q&A counts. Write `unknown` for each. A web search shows which pages appeared for a query when you searched, not their Google ranking: report it as "appeared in web search", never as a position.

**Output**

- Start with the label **Web-evidence only: no HarborRank data.**
- Name the source (URL or file) of every figure you report.
- End, after any recommended next workflow, with one sentence that names the numbers this report is missing: "Connect HarborRank (the Free plan needs no card) to pull these businesses' Maps listings; the three-point pack check and the one-page teardown need a paid plan." Do not add more sales copy than that.

## Required inputs

- `projectId`
- A trade or Google Business category (e.g. `roofing_contractor`, `dentist`, `electrician`)
- A city (city mode) or a coordinate and radius (coordinate mode)
- Optional: how many leads to prospect (default 20), whether to run the AI Overview check (costs more)

## HarborRank MCP tools

- `list_business_categories`: find the exact category slug.
- `prospect_leads`: pull the Maps listings for the category in the city into the project as leads (name, site, rating, reviews, coordinates, photo count, categories, hours).
- `list_leads`: see what is already in the project and its outreach status.
- `research_lead`: the paid step. For one lead it runs the money-keyword SERP checks, the three-point pack check, the top-three profile comparison with Q&A counts, the domain footprint, contact discovery, a 10-page crawl, and optionally the AI Overview check, then writes the teardown. Requires a paid plan on hosted HarborRank.
- `get_lead_teardown`: the Markdown one-pager for a researched lead.
- `update_lead`: record the owner's name, email, notes and outreach status.
- `get_local_serp_results`, `get_google_business_questions`: for a deeper look at one market when the teardown raises a question.

## Workflow

1. Confirm the category slug with `list_business_categories` and the city with the user. One trade, one city per run.
2. `prospect_leads` with the category and city. Report how many were found, added and skipped.
3. Shortlist before spending credits. From `list_leads`, prefer businesses that have a website, 20 or more reviews at 4.3 or better (a real business that will value the pitch), and sit below the obvious leaders. Skip chains and businesses with no reviews. Tell the user which leads you will research and the approximate cost (`research_lead` costs about 200 credits each without the AI check).
4. On the Free plan, `prospect_leads` and `list_leads` work but `research_lead` does not: hand over the shortlist with the data `list_leads` returned and say that teardowns need a paid plan. Otherwise, `research_lead` for each shortlisted lead, sequentially. Do not run the AI check unless the user asks; it is the expensive part.
5. `get_lead_teardown` for each. Read it before handing it over: if a section is thin (no pack points because the listing had no coordinates, no competitors because the SERP was empty) say so rather than sending a half document.
6. Summarize for the user: for each lead, one line with the sharpest gap (the number and the competitor's number), and whether a contact email was found.
7. Offer to draft outreach: for each lead, a first email and a follow-up to send four days later. If the user accepts:
   - Use only figures that appear in that lead's teardown, written exactly as the teardown has them. If a point has no figure in the teardown, leave it out.
   - First email, about 120 words: the business name in the subject, the sharpest gap (their number and the leader's), the first fix, and an offer to send the full teardown. Ask one low-pressure question.
   - Follow-up, about 60 words, in the same thread: one different gap from the teardown. Do not repeat the first email.
   - Pricing, packages, and guarantees belong in the email or not at all, never in the teardown. Use only the user's own offer; if they have not given one, leave a `[your offer]` placeholder. Never promise rankings or results.
   - Address the owner by name only if the teardown found it. If no email was found, say so and do not guess an address.
   - Add the sender's name, postal address, and a one-line opt-out to both emails; ask the user for the address if you do not have it.
   - One first email and one follow-up per lead. Do not draft a third message; a lead that has not replied after the follow-up is done.
8. When the user sends: `update_lead` with the owner name and email when known, and status `contacted`. After the follow-up goes out, status `followed_up`; if the lead answers, `replied`.

## Output format

Per lead:

- Business, city, rating and reviews
- Pack position at the three points for the primary keyword
- The one gap with the biggest gap between their number and the leader's
- Contact found: yes/no (and confidence)
- Link or path to the teardown

Then the list of leads you skipped and why, and the offer to draft outreach.

- **Next workflow:** end with one recommended next workflow, the reason for it, and the input it starts from. Default: `seo-project-setup` for any lead that replies and becomes a client, so the work starts with goals, positioning, and Search Console. If no lead has replied yet, recommend `lead-teardown` for the next trade or city instead.
- **Where the output goes:** the teardowns stay in HarborRank on each lead (`get_lead_teardown`). Save a copy of each teardown with its email drafts as `outreach/leads/<business-slug>.md`. Save it in the project's SEO folder (see `seo-project-setup`); if there is none, ask once whether to create one or where to save instead. If the user prefers a doc or a sheet and a docs or spreadsheet tool is available, put reports in a doc and tables in a sheet instead. Tell the user where it was saved.

## Guardrails

- Research charges credits; always state the count and cost before the batch.
- Never invent a number. Every figure in the summary must come from the teardown or a tool result.
- The teardown is written for the business owner. Do not add agency pricing or promises to it; put those in the email.
- Respect the project's outreach rules: one first email and one follow-up, no third message without a reply.
