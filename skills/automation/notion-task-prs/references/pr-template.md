# PR Schema

Every agent-created PR body must use this schema. Keep sections short and complete.

````markdown
<!-- agent-pr-schema:v1 -->

## Status
Ready for review

## Notion
- Task: <TASK_URL>
- Notion status: Pending review

## Summary
- <what changed>

## Changes
- <files/modules/behavior changed>

## Verification
- Result: PASS | NOT RUN
- Commands:

```bash
<commands>
```

## Manual QA
- [ ]

## Risk
Low | Medium | High

## Human Follow-up
None
````

Rules:
- `Status` is `Ready for review` only for mergeable PRs.
- Use `Result: PASS` when checks ran and passed.
- Use `Result: NOT RUN` only with a short reason under `Human Follow-up`.
- Do not put blocked work in a normal PR.

If GitHub visibility is required for blocked work, create an empty-commit notification PR:
- branch: `blocked/<task-slug>`
- commit: `git commit --allow-empty -m "<blocked summary>"`
- PR state: draft, or closed immediately if only history is needed
- labels: `blocked`, `do-not-merge`

````markdown
<!-- agent-pr-schema:v1 -->

## Status
Blocked

## Notion
- Task: <TASK_URL>
- Notion status: Blocked

## Blocker
- <why work cannot proceed>

## Required Human Action
- <specific next action>
````

Blocked notification PRs must link the Notion task, explain the blocker, and must never be merged.
