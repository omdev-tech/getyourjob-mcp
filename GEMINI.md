# GetYourJob

The `getyourjob` MCP server gives access to IT job and freelance mission offers in France
and to the signed-in candidate's GetYourJob space.

- Start with `search_jobs` for offer searches; call `get_job_details` only for offers the user cares about.
- `run_ai_matching`, `generate_cover_letter` and `generate_action_plan` consume the user's plan quota:
  check `get_matching_quota` first and don't call them speculatively.
- Tools that change data (save, update, delete) must be confirmed with the user first.
- Answer in the user's language; offers and field values are mostly in French.
