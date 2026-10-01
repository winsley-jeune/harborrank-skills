---
name: lead-teardown
description: Find local businesses with search gaps, research each one, and produce a one-page teardown an agency can send as its pitch.
---

# HarborRank Lead Teardown

## Goal

Turn a trade and a city into a short list of local businesses worth pitching, each with a one-page teardown built from real data: where they show up in Google Maps from three points in their service area, what the top three profiles have that they do not, what their website earns, and the first three fixes. The teardown is the sales document; the agency sends it, the business owner reads their own numbers.

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
4. `research_lead` for each shortlisted lead, sequentially. Do not run the AI check unless the user asks; it is the expensive part.
5. `get_lead_teardown` for each. Read it before handing it over: if a section is thin (no pack points because the listing had no coordinates, no competitors because the SERP was empty) say so rather than sending a half document.
6. Summarize for the user: for each lead, one line with the sharpest gap (the number and the competitor's number), and whether a contact email was found.
7. If the user wants to send: `update_lead` with the owner name and email when known, and move status to `contacted` once the email goes out. The follow-up is due in four days.

## Output format

Per lead:

- Business, city, rating and reviews
- Pack position at the three points for the primary keyword
- The one gap with the biggest gap between their number and the leader's
- Contact found: yes/no (and confidence)
- Link or path to the teardown

Then the list of leads you skipped and why.

## Guardrails

- Research charges credits; always state the count and cost before the batch.
- Never invent a number. Every figure in the summary must come from the teardown or a tool result.
- The teardown is written for the business owner. Do not add agency pricing or promises to it; put those in the email.
- Respect the project's outreach rules: one first email and one follow-up, no third message without a reply.
