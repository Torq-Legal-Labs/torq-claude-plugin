---
name: intake-coaching
description: "Use when a manager asks about intake performance in Torq: what good intake looks like, the team's weakest skills, practice scenarios, or assigning scenarios to reps."
---

# Intake Coaching

Use this skill for coaching, practice planning, and intake quality questions.

Workflow:
1. Start with get_intake_criteria when the user asks what good performance means.
2. Use get_team_weakest_skills for team-level coaching priorities.
3. Use list_scenarios to find practice options, then summarize_scenario for the selected scenario only.
4. assign_scenarios is a proposed action. Explain that it queues for approval and use it only when the user asks to assign practice.
5. Separate score facts from coaching recommendations in the final answer.

Torq tools this guide uses: `get_intake_criteria`, `get_team_weakest_skills`, `list_scenarios`, `summarize_scenario`, `assign_scenarios`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
