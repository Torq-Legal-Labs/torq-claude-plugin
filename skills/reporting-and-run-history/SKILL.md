---
name: reporting-and-run-history
description: "Use when the member asks about saved reports and report recipes in Torq, whether a Torq engine is running or failing, an engine's recent run history, or the record of a Brain workflow run."
---

# Reporting And Run History

Use this skill for report catalog questions, report recipes, engine health, and workflow audit lookups.

Workflow:
1. Use list_saved_reports to find the report; use get_saved_report only for the selected report spec.
2. Use get_latest_engine_run for "is it running or did it fail?" questions.
3. Use list_engine_runs for one engine over recent history.
4. Use get_engine_run_health for how an engine’s recent runs ended. Read reportsUnrunnable first: where it is true, unrunnable counts the runs that had nothing to work with, apart from completed ones; where it is false, a completed run can still have written nothing, so check the engine’s own output before calling it working. When switchedOff is set, the firm flags it lists stop the engine, so zero counts mean switched off, not broken: say so, and give lastCompletedRun’s date. lastCompletedRun and lastUnrunnableRun cover the engine’s whole history, not only the window.
5. Use list_brain_workflow_runs for approval-lifecycle or workflow-window questions, then get_brain_workflow_run for one run id.
6. Keep report specs and run payloads summarized unless the user asks for the full recipe or audit detail.

Torq tools this guide uses: `list_saved_reports`, `get_saved_report`, `list_engine_runs`, `get_latest_engine_run`, `get_engine_run_health`, `list_brain_workflow_runs`, `get_brain_workflow_run`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/ai-assistants.
