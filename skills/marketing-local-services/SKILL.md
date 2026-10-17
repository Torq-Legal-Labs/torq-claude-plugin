---
name: marketing-local-services
description: "Use when the member asks about the firm's Google Local Services Ads in Torq: the LSA scorecard, leads that are candidates for a rating such as spam, the LSA action queue, or proposing a rating."
---

# Marketing Local Services

Use this skill for Local Services Ads quality, spam-rating, and LSA action queue questions.

Workflow:
1. Use get_lsa_scorecard for current LSA health and benchmark context.
2. Use list_lsa_rating_candidates for possible spam/rating actions; apply date filters for recent windows.
3. Use list_lsa_action_queue to inspect pending or historical action work.
4. propose_lsa_rating only queues an approval-backed proposal. Never describe it as an immediate Google write.
5. If a lead is not a current candidate, report that eligibility failed instead of forcing an action.

Torq tools this guide uses: `get_lsa_scorecard`, `list_lsa_rating_candidates`, `list_lsa_action_queue`, `propose_lsa_rating`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/ai-assistants.
