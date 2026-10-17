---
name: case-strategy
description: "Use when an attorney wants defense strategy, tactics or investigative questions for a specific matter, grounded in and cited to the firm's vetted reference-library manuals in Torq."
---

# Case Strategy

Use this skill when an attorney wants recommended defense strategy, tactics, or investigative questions for a specific matter, grounded in the firm’s vetted reference-library manuals rather than general model knowledge.

This is a closed-corpus, no-guessing surface (same contract as library-qa): every recommendation must be traceable to a specific manual passage. Never fill a gap with outside/model knowledge, even if you are confident it is correct in general.

Note: the dedicated Case Strategy engine (POST /cases/:caseId/strategy) runs this end-to-end and lands a cited case_strategy_review card in the Action Inbox. Use THIS skill for interactive, in-chat strategy questions about a matter; prefer the engine route when the attorney wants the persisted, inbox-tracked analysis.

Workflow:
1. If the attorney named a case id, call get_case to load the matter facts (charge, court, jurisdiction, statutes, priors). Otherwise use the facts the attorney supplied verbatim — never invent facts.
2. Identify the distinct legal issues the facts raise, then call semantic_search_docs (one query per issue) to retrieve candidate manual passages. Never pass reference_library_only=false or scope on this surface. When the thread is pinned to the reference library the server forces the closed corpus and ignores those arguments, so a widened search is not available — never describe one to the user.
3. STOP for an issue when the result reports notCovered=true, or when the top hit’s score < 0.615 (the calibrated not-covered similarity threshold): say that issue is not covered in the reference library and name the space(s) searched (spacesSearched) — do not synthesize ungrounded guidance.
4. Otherwise, synthesize strategy / tactics / questions using ONLY the retrieved passage text. Attach a citation to every recommendation: manual title + section path + page number, drawn from each passage’s citation object.
5. Use kb_get_page_content for the same page_id when a recommendation needs more surrounding context than the chunk carries — never widen scope to a different page or manual to fill a gap.
6. Present strategy, tactics, and questions as separate groups, and never present a covered recommendation without its citation attached.

Torq tools this guide uses: `get_case`, `semantic_search_docs`, `kb_get_page_content`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/ai-assistants.
