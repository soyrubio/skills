---
name: notion-task-prs
description: Plan or implement batches of Notion tasks as isolated GitHub pull requests. Use when the user asks Codex or Claude to read a Notion task list, prepare implementation plans, create per-task worktrees/branches, spawn one agent per task, open standardized PRs, or update Notion task statuses.
---

# Notion Task PRs

Use this for Notion -> implementation -> PR automation. Adapt to the existing Notion database; never change its properties, names, or options.

## Inputs

- Notion task list/page URL
- mode: `plan` or `implement`
- repo path or GitHub repo
- task limit, default `20`
- reviewer GitHub username

## References

- `references/notion-schema.md` - field mapping rules
- `references/agent-prompts.md` - sub-agent prompts
- `references/pr-template.md` - required PR schema

## Workflow

1. Read the Notion task list via MCP.
2. Map existing fields when present: status, assignee, priority, due date, PR URL, branch, done date. Do not add or edit fields/options.
3. Select open/to-do tasks assigned to Claude/agent when an assignee field exists.
4. Sort by due date, then priority, when available. Apply the task limit.
5. For each task, read the page/comments first and decide whether it is actionable.

Plan mode:
- Write a concise plan into the Notion page/comment.
- If blocked, use an existing blocked status when available and write the reason in the page/comment.

Implement mode:
- For each actionable task, create one `/tmp` worktree and branch.
- Spawn one implementation agent per task when sub-agent tools are available.
- Require the agent to implement, test, run `$simplify` when available, commit, push, open a PR using `agent-pr-schema:v1`, and request reviewer approval.
- Update existing Notion fields only: pending-review status, PR URL, branch.
- For blocked tasks, write the reason in the page/comment and, by default, create an empty-commit draft notification PR.
- After all agents finish, verify PR links, delete worktrees, and report PRs/failures/cleanup.

## Guardrails

- Never change Notion table schema, property names, or select/status options.
- If a useful Notion field is missing, write the information in the page/comment.
- Do not create normal PRs for blocked or unclear tasks.
- Blocked GitHub artifacts are notifications only: create branch `blocked/<task-slug>`, commit with `git commit --allow-empty`, open a draft PR, use the blocked schema, label `blocked` and `do-not-merge`, and leave it open for the user to close.
- Blocked notification PRs must link the Notion task, explain the blocker, and must never be merged.
- Keep each task on its own branch/worktree.
