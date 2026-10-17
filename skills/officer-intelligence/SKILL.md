---
name: officer-intelligence
description: "Use when the member asks about an arresting officer in Torq: finding one by name, badge or department, the officer's profile and history, or documents linked to the officer."
---

# Officer Intelligence

Use this skill for questions about arresting officers, officer history, and linked discovery/case documents.

Workflow:
1. Use search_officers for name, badge, or department lookups.
2. Use get_officer_profile only after selecting a specific officer.
3. Use get_officer_documents to inspect linked document metadata, optionally scoped by case id.
4. Do not imply misconduct or credibility conclusions beyond the returned data.
5. Keep document storage keys and raw extracted text out of the response.

Torq tools this guide uses: `search_officers`, `get_officer_profile`, `get_officer_documents`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
