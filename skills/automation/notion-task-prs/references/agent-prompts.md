# Agent Prompts

## Planning Agent

```text
Read Notion task <TASK_URL>, including comments and linked context.

Do not implement.

Inspect relevant repo context and write a concise plan back to Notion:
- goal
- approach
- affected files/modules
- test plan
- risks/questions

Set Status = "Plan ready".
If unclear or unsafe, set Status = "Blocked" and write the reason.
```

## Implementation Agent

```text
Implement Notion task <TASK_URL>.

Rules:
- read the task, comments, and approved plan
- use a separate /tmp worktree and dedicated branch
- keep scope limited to this task
- run relevant tests/checks
- run $simplify when available
- commit with a clear technical summary
- push branch and open a PR using the standard template
- assign <GITHUB_USERNAME> as reviewer

Update Notion:
- Status = "Pending review"
- PR URL = created PR URL
- Branch = branch name

If blocked, do not open a weak PR. Set Status = "Blocked" and write the reason.
```
