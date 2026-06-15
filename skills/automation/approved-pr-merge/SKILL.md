---
name: approved-pr-merge
description: Merge human-approved GitHub pull requests sequentially and update linked Notion tasks. Use when the user asks to process approved PRs, merge PRs reviewed by a specific GitHub user, resolve merge conflicts conservatively, or mark Notion tasks done after successful merges.
---

# Approved PR Merge

Use this skill for the approval -> merge -> Notion done workflow.

## Inputs

Collect only missing blockers:
- GitHub repo
- approver GitHub username
- base branch, default `main`
- Notion access, if task updates are required

## Reference

Load `references/merge-rules.md` before merging.

## Workflow

1. Find open PRs that:
   - target the base branch
   - are approved by the configured user
   - have passing required checks
   - are linked to a Notion task
2. Sort by PR number ascending.
3. Process one PR at a time.
4. For each PR:
   - reread the PR, changed files, CI result, and linked Notion task
   - verify it is mergeable without an obvious regression
   - resolve only merge conflicts if needed
   - run relevant checks after conflict resolution
   - merge into the base branch
   - update Notion: `Status = Done`, `Done date = today`
5. Stop on failing checks, unclear conflicts, missing approval, or suspected regression.

## Guardrails

- Never batch-merge blindly.
- Never continue if the base branch may be unstable.
- Do not introduce new behavior while resolving conflicts.
- Report merged PRs, stopped PR, blocker reason, and Notion update status.
