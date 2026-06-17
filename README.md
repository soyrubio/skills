# skills

My curated list of skills and command-style workflows.

## Catalog

- [`/simplify`](skills/coding/simplify/SKILL.md) - Simplify recently touched code while preserving behavior.
- [`simplify-loop`](skills/coding/simplify-loop/SKILL.md) - Run `/simplify` repeatedly until no new issues are found.
- [`grill-me`](skills/productivity/grill-me/SKILL.md) - Stress-test a plan or design through focused questions.
- [`security-threat-model`](skills/security/security-threat-model/SKILL.md) - Build a repo-grounded threat model with abuse paths and mitigations.
- [`notion-task-prs`](skills/automation/notion-task-prs/SKILL.md) - Plan or implement Notion tasks as isolated PRs.
- [`approved-pr-merge`](skills/automation/approved-pr-merge/SKILL.md) - Merge approved PRs sequentially and update linked Notion tasks.

## Layout

Skills live under `skills/<category>/<skill-name>/SKILL.md`.

## Automation Setup

`notion-task-prs` adapts to your existing Notion table and must not change database properties or options. For the smoothest workflow, use a task database with:

- `Status`: `To-do`, `Pending review`, `Done`, `Blocked`
- `Me/Claude`: assignee selector; assign work to `Claude`
- `Priority`
- `Due Date`
- `Done date`
- `PR URL`
- `Branch`

Blocked details, dependency notes, plans, and verification results belong in the Notion page body or comments, not extra table columns.

Agent-created PRs should use `agent-pr-schema:v1` from [`pr-template.md`](skills/automation/notion-task-prs/references/pr-template.md). Normal PRs are mergeable work. Blocked GitHub visibility may use an empty-commit draft/closed PR labeled `blocked` + `do-not-merge`; merge automation rejects those even when CI is green.

## References

- `/simplify` is adapted from Anthropic's [`code-simplifier`](https://github.com/anthropics/claude-plugins-official/blob/main/plugins/code-simplifier/agents/code-simplifier.md).
- `grill-me` is ported from Matt Pocock's [`grill-me`](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md).
- `security-threat-model` is ported from OpenAI's [`security-threat-model`](https://github.com/openai/skills/blob/main/skills/.curated/security-threat-model/SKILL.md).
