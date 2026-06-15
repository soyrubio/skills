# Merge Rules

Merge only PRs that are:
- open
- approved by the configured user
- targeting the configured base branch
- passing required checks
- linked to a Notion task

Resolve conflicts only when the intent is clear. Preserve both sides where possible, run relevant checks, then merge.

Stop immediately on:
- failing required checks
- unclear conflicts
- suspected regression
- missing or stale approval
- missing linked Notion task
