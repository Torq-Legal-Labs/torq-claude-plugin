---
name: firm-data-querying
description: "Use when the member asks a question about the firm's Torq data that no specific Torq tool answers, such as counts, totals, trends or rankings across leads, cases, opportunities or other firm datasets."
---

# Firm Data Querying

Use this skill when no curated Brain tool directly answers the question or the user asks for aggregation over raw firm datasets.

Workflow:
1. Call describe_dataset for the target dataset before composing a query.
2. Push filtering, grouping, and aggregation into query_firm_data; do not fetch broad rows and aggregate in model context.
3. Select only fields needed for the answer. Keep limits tight unless the user explicitly needs a sample.
4. Prefer aggregate rows for trends, counts, sums, averages, and rankings.
5. total counts every row the query matches. When nextCursor is set, pass it back as cursor with the same arguments for the next page, or issue a narrower query; never treat one page as the complete result.
6. The synced datasets lag Salesforce by up to ~15 minutes. ONLY when a lead/case/client/opportunity was created or changed in the last few minutes and the synced row is missing or stale, use sf_live_lookup for a live read. Treat verified=false (no items) as "could not confirm" — not as "no such record".

Torq tools this guide uses: `describe_dataset`, `query_firm_data`, `sf_live_lookup`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
