---
name: case-operations
description: "Use when the member asks about a case in Torq: its status, upcoming dates and appointments, open tasks, where it sits in a pipeline, or the files attached to it."
---

# Case Operations

Use this skill for operational case-work questions: status, upcoming dates, task follow-up, pipeline position, and attached case-file metadata.

Workflow:
1. Prefer the narrowest direct lookup when the user gives an id: get_case, get_task, get_appointment, or get_pipeline.
2. For open-ended case questions, search_cases first; then call get_case only for the chosen case.
3. Use list_tasks, list_appointments, list_pipelines, or list_case_files only after the case/client context is clear.
4. Never infer missing deadlines from partial data. Say which source was checked and what was absent.
5. Mutations are separate proposed actions; this skill is read-side operating guidance.

Torq tools this guide uses: `get_case`, `list_cases`, `search_cases`, `list_tasks`, `get_task`, `list_appointments`, `get_appointment`, `list_pipelines`, `get_pipeline`, `list_case_files`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
