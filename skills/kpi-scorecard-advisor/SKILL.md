---
name: kpi-scorecard-advisor
description: "Use when an owner or department head wants to build, prune or fix a team's KPI scorecard in Torq: choosing the few numbers that matter, setting targets from past data and queuing the scorecard for approval."
---

# KPI Scorecard Advisor

Use this skill when an owner or department head wants to build, prune, or fix a team's scorecard — deciding which numbers actually prove the team won the week, and setting their targets. This is an INTERVIEW: ask, don't assume. Your job is to force the hard choice of the few that matter, not to rubber-stamp a long wish-list.

Ground first — never propose against an empty picture:
1. Read the firm's real shape before suggesting anything: use describe_dataset then query_firm_data over the eos teams/measurables datasets to list the firm's actual meeting teams and existing KPIs, and anchor the scorecard to the firm's VTO goals. Only ever reference teams and measurables that already exist (by their real ids) — a wrong-firm or invented id is rejected before it queues.
2. The KPI template packs (the Torq-authored starter library) are your STARTING proposals, not the answer. Adapt them to what this firm actually does; drop what does not fit.

The doctrine to enforce in the interview:
3. One north-star for the whole firm; one primary KPI per team. Ask "what one number proves your team won this week?" and hold them to a single primary. Supporting KPIs (≤5 per team) explain the primary; do not let them multiply into a dashboard.
4. Actionable-and-controllable test: ask "can your team actually move this number?" A vanity metric the team cannot control belongs in the diagnostic tier (off the scorecard), not as a primary/supporting KPI. Push vanity metrics down to diagnostic.
5. Leading over lagging: a team's primary+supporting band MUST include at least one leading indicator — a number the team moves this week that predicts the lagging outcome. A lagging-only band is rejected at approval, so never propose one; when the owner names only lagging outcomes, interview for the leading behaviour that drives them and add it.

Set targets from data, not vibes:
6. For each KPI with history, call suggest_kpi_target and use its average + best-quartile to propose a stretch-but-attained goal. If it returns no history, say so and ask the owner for a target — never invent one.

Confirm, then queue:
7. Summarize the proposed scorecard back to the owner in plain language and get explicit confirmation before proposing.
8. Call propose_kpi_scorecard with the full change-set (create/update ops). This QUEUES the change for admin approval — it does not apply it. Tell the owner it is pending approval. The caps and the leading-indicator gate are re-checked at approval time; if a proposal violates them it fails with a clear error, so keep the change-set within one north-star / one primary-per-team / ≤5 supporting and always include a leading indicator.

Torq tools this guide uses: `describe_dataset`, `query_firm_data`, `suggest_kpi_target`, `propose_kpi_scorecard`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
