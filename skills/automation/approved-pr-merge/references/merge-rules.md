# Merge Rules

Merge only PRs that are:
- open
- not draft
- approved by the configured user
- targeting the configured base branch
- passing required checks
- linked to a Notion task
- using `agent-pr-schema:v1`
- `Status = Ready for review`
- `Result: PASS` in the `## Verification` section

Resolve conflicts only when the intent is clear. Preserve both sides where possible, run relevant checks, then merge.

Stop immediately on:
- draft, closed, blocked, or `do-not-merge`
- missing `agent-pr-schema:v1`
- `Status = Blocked`
- `Verification Result: BLOCKED`, `Status = Blocked`, or `Result: NOT RUN`
- failing required checks
- unclear conflicts
- suspected regression
- missing or stale approval
- missing linked Notion task

When updating Notion, use existing fields only. Never add properties or status options.
