---
name: library-qa
description: "Use when an attorney asks a question that should be answered only from the firm's vetted reference-library manuals in Torq, such as a statute, a playbook or a procedure guide, with a citation for every claim."
---

# Ask The Library

Use this skill when an attorney asks a question that should be answered strictly from the firm’s vetted reference-library manuals (statutes, playbooks, procedure guides) rather than general model knowledge.

This is a closed-corpus, no-guessing surface. Never fill a gap with outside/model knowledge, even if you are confident the answer is correct in general — the value of this skill is that every answer is traceable to a specific manual.

Workflow:
1. Call semantic_search_docs (add space_ids only if the user named a specific manual/space) to retrieve candidate chunks. Never pass reference_library_only=false or scope on this surface. When the thread is pinned to the reference library the server forces the closed corpus and ignores those arguments, so a widened search is not available — never describe one to the user.
2. STOP with "not covered in the reference library" when the result reports notCovered=true, or when the top hit’s score < 0.615 (the calibrated not-covered similarity threshold). On a STOP, name the space(s) searched (spacesSearched) and do not proceed to step 3 — never answer from a below-threshold chunk.
3. Otherwise (covered=true), compose the answer using ONLY the retrieved chunk text. Attach a citation to every claim: manual title + section path + page number, drawn from each chunk’s citation object.
4. If a citation needs more surrounding context than the chunk carries, use kb_get_page_content (full page) or kb_get_page_version (a specific pinned revision) for the same page_id before finalizing the answer — never widen scope to a different page or manual to fill a gap.
5. If retrieved chunks conflict or only partially cover the question, say precisely which part is covered and which part is not, rather than blending in an assumption.
6. Never present a "not covered" answer as if it were a considered legal opinion, and never present a covered answer without its citations attached.

Torq tools this guide uses: `semantic_search_docs`, `kb_get_page_content`, `kb_get_page_version`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/ai-assistants.
