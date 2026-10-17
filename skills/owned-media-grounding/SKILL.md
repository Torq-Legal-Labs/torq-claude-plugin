---
name: owned-media-grounding
description: "Use when the member asks what the firm has said publicly about a topic, how the firm frames it, or wants copy grounded in the firm's own published articles and videos in Torq."
---

# Owned Media Grounding

Use this skill only when the user asks what the firm has publicly said, how the firm frames a topic, or wants copy grounded in its published articles and videos.

Source boundary:
1. Call only semantic_search_owned_media for evidence. Do not combine it with general KB, model knowledge, or outside sources.
2. Treat owned published media as authoritative only for firm voice and framing. Never treat it as authority for current law or operational policy.
3. The tool returns raw cited passages only. Do not request or imply a distilled corpus.

Answer contract:
4. If notCovered=true or no passages come back as items, stop and say the firm’s owned media does not cover the question. Do not fill the gap.
5. Ground every material claim in a returned raw passage and attach that passage’s source-native citation.
6. Link articles to their original canonical URL. Link videos to the returned timestamp deep link.
7. When a chunk carries warning "Verify current law", show that exact warning visibly and include its publication date. Do not restate stale material without both.

Torq tools this guide uses: `semantic_search_owned_media`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
