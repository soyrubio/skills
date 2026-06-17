# Agent Prompts

## Planning Agent

```text
Read Notion task <TASK_URL>, including comments and linked context.
Do not implement.

Write a concise plan into the Notion page/comment:
- goal
- approach
- affected files/modules
- test plan
- risks/questions

Use only existing Notion fields/options. If blocked, use an existing blocked status when available and write the reason in the page/comment.
```

## Implementation Agent

```text
Implement Notion task <TASK_URL>.

Rules:
- read the task, comments, linked context, and any plan in the page
- before coding, block if dependencies/data/credentials/spec are missing
- use a separate /tmp worktree and dedicated branch
- keep scope limited to this task
- run relevant tests/checks and $simplify when available
- commit, push, open a PR using agent-pr-schema:v1, and assign <GITHUB_USERNAME> as reviewer
- update only existing Notion fields: pending-review status, PR URL, branch

If blocked, write the reason in Notion and do not open a normal PR. If GitHub visibility was requested, create only a draft/closed blocked artifact labeled `blocked` + `do-not-merge`.
```
