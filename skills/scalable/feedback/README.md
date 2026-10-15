# Retrieval and workflow feedback cases

Add one JSON object to `cases-v1.json` for each reviewed test prompt. Keep prompts synthetic and free of customer data. Record the expected skill-selection result and, when relevant, whether the workflow completed truthfully. Do not add new feedback categories: `failure_kind` must be one of `auth`, `input`, `tool_error`, `missing_capability`, `unclear_result`, or `other`, matching the MCP feedback tool. A submitted report also requires `user_consented: true`; optional fields are `tool`, `error_code`, and `attempt` (1–100). The retrieval fixtures are not feedback submissions.

The empty template is versioned as `cases-v1.json`; add a new file for an incompatible future case format rather than silently changing existing case meaning.
