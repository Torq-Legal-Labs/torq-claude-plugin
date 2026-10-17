---
name: memory-and-provenance
description: "Use when the member asks what the firm's past Torq Brain conversations said about something, where a remembered fact came from, or why an earlier answer cited past context."
---

# Memory And Provenance

Use this skill when the user asks what the Brain previously knew, where a remembered fact came from, or why an answer cited past context.

Workflow:
1. Use memory_search with a precise phrase; broad queries return noisy excerpts.
2. Expand promising hits with get_thread_context before relying on them.
3. Use get_memory_source_anchor when the user asks for provenance of a derived memory key.
4. Treat missing memory as absence from recall, not proof that something never happened.
5. Do not expose raw transcript excerpts beyond what is needed to answer the question.

Torq tools this guide uses: `memory_search`, `get_thread_context`, `get_memory_source_anchor`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/ai-assistants.
