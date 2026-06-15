---
name: notion-task-prs
description: Plan or implement batches of Notion tasks as isolated GitHub pull requests. Use when the user asks Codex or Claude to read a Notion task list, prepare implementation plans, create per-task worktrees/branches, spawn one agent per task, open standardized PRs, or update Notion task statuses.
---

# Notion Task PRs

Use this skill for the Notion -> plan -> implementation PR workflow. Keep prompts short; put repeated structure in references.

## Inputs

Collect only missing blockers:
- Notion task list/page URL
- mode: `plan` or `implement`
- repo path or GitHub repo
- task limit
- reviewer GitHub username

Default task limit: `20`.

## References

- Notion fields: `references/notion-schema.md`
- Agent prompts: `references/agent-prompts.md`
- PR template: `references/pr-template.md`

Load only the references needed for the current mode.

## Plan Mode

1. Read the Notion task list via MCP.
2. Select tasks:
   - `Status = To-do`
   - `Me/Claude = Claude`
3. Sort by Due Date ascending, empty dates last, then Priority descending.
4. Limit to the requested task count.
5. For each task:
   - read the task, comments, and linked context
   - inspect relevant repo context
   - write a concise plan to Notion
   - set `Status = Plan ready`
6. If a task is unclear or unsafe, set `Status = Blocked` and write the blocker reason.

## Implement Mode

1. Read the Notion task list via MCP.
2. Select tasks:
   - `Status = Approved for implementation`
   - `Me/Claude = Claude`
3. Sort by Due Date ascending, empty dates last, then Priority descending.
4. Limit to the requested task count.
5. For each task, create one isolated `/tmp` worktree and branch.
6. Spawn exactly one implementation agent per task when sub-agent tools are available.
7. Require each agent to:
   - follow the approved plan
   - keep scope limited to one task
   - run relevant tests/checks
   - run `$simplify` when available
   - commit, push, and open a PR using `references/pr-template.md`
   - request review from the configured reviewer
   - update Notion with `Pending review`, PR URL, and branch
8. After agents finish:
   - verify each successful task has a reachable PR
   - update failed tasks with a short reason
   - delete created local worktrees
   - report PRs, failures, and cleanup status

## Guardrails

- Do not implement tasks that are only `Plan ready`; wait for approval.
- Do not create weak PRs for blocked or unclear tasks.
- Keep each task on its own branch and worktree.
- Leave remaining tasks unchanged for the next run.
