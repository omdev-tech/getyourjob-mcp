---
name: prepare-application
description: Prepare a strong application to an IT job on GetYourJob - run AI matching on the user's profile, explain the fit and the missing skills, then produce a tailored action plan and cover letter, and track the application status. Use when the user asks which offers match them, how to apply, for a "lettre de motivation", a "plan d'action", or to update where an application stands.
---

# Prepare an application with GetYourJob

Uses the `getyourjob` MCP server. If its tools are unavailable or return an auth error, tell
the user to connect GetYourJob first.

## Workflow

1. **Quota first.** `run_ai_matching`, `generate_action_plan` and `generate_cover_letter`
   consume the user's plan quota on free plans. Call `get_matching_quota` before matching,
   and never call these tools speculatively or twice for the same thing.
2. **Match.** `run_ai_matching` returns the best-fitting active offers with a score
   breakdown. Explain the top results in plain words: why they fit, which skills are missing.
3. **Plan.** For the offer the user picks, `generate_action_plan` gives 3-5 concrete steps.
   To keep a plan just shown, call `save_action_plan` - never regenerate to save.
   `get_my_action_plan` reads saved plans for free; `complete_action_plan_step` ticks steps.
4. **Letter.** `generate_cover_letter` for that offer. Show it, and offer edits in the chat.
5. **Track.** After the user applies, `update_application_status` records it;
   `get_my_pipeline` shows every application in progress.

## Rules

- Tools that change data (save, update, delete) need the user's confirmation first.
- The connector never sends an application to a recruiter: the user applies themselves.
- If `get_my_cv_analysis` has a stored report, use its findings to sharpen the letter; respect
  its caveats (`partial`, `roleScoped`, `marketAvailable`) and never estimate a score yourself.
