---
name: finance-and-vendor-spend
description: "Use when an owner or billing member asks about the firm's finances in Torq: the current financial snapshot, trends over time, vendor spend and the largest vendor, Brain usage cost, or signed-case revenue by case type."
---

# Finance And Vendor Spend

Use this skill for finance and spend questions that require firm-owner or billing visibility.

Workflow:
1. Use get_financials_snapshot for current P&L-style state.
2. Use list_financials_history for trend windows and compare periods in the returned data.
3. Use get_vendor_spend_summary before list_vendor_spend unless the user asks for raw vendor rows.
4. Use get_top_vendor for a quick largest-vendor answer.
5. Use list_brain_costs for Brain usage-cost analysis, not for law-firm operating spend.
6. Use get_opportunity_revenue_by_case_type for signed-case revenue, revenue-by-category, or matter-revenue questions (e.g. Traffic vs DUI); it groups opportunity revenue by the firm CRM case category and defaults to signed (paid / Closed Won). Use list_opportunities for the underlying matter rows.
7. Keep raw financial payloads out of client-rendered prose unless the user asked for the underlying figures.

Torq tools this guide uses: `get_financials_snapshot`, `list_financials_history`, `list_brain_costs`, `get_vendor_spend_summary`, `list_vendor_spend`, `get_top_vendor`, `list_opportunities`, `get_opportunity_revenue_by_case_type`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
