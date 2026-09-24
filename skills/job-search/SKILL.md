---
name: job-search
description: Find IT jobs and freelance missions in France on GetYourJob that fit the user - search with filters, compare offers, check how pay sits against the market, and save the ones worth applying to. Use when the user asks for job offers, missions, "offres", "missions freelance", or wants to compare or shortlist offers.
---

# IT job search with GetYourJob

Uses the `getyourjob` MCP server. If its tools are unavailable or return an auth error, tell
the user to connect GetYourJob (a browser sign-in opens on first use; free account at
https://getyourjob.pro/auth/register).

## Workflow

1. **Know the target.** If the request is vague, call `get_my_profile` to read the user's
   skills, seniority, location and work-type preferences instead of asking for them.
2. **Search.** Call `search_jobs` with structured filters (`technologies`, `roles`,
   `locations`, `workTypes`, `contractTypes`, `seniorityLevels`). Summaries are light; do not
   fetch every offer's details.
3. **Go deeper only on candidates.** Call `get_job_details` for the few offers the user cares
   about, and `get_company_details` when the employer matters (ESN vs end client, size).
4. **Compare.** For 2-5 offers, call `compare_jobs` rather than comparing by hand.
5. **Pay.** When an offer carries `marketPosition`, report its verdict (under / fair / above
   the market) with the p25-p75 band. A null verdict means the offer hides its pay: present
   the band as a cohort estimate, never as a judgement on that offer.
6. **Shortlist.** Offer to `save_job` the ones the user likes. Saving changes their data:
   confirm first.

## Rules

- Offers and field values are mostly in French; answer in the user's language.
- Never invent offers, salaries or companies: everything comes from tool results.
- For "what fits my profile best", prefer the `prepare-application` skill's AI matching step.
