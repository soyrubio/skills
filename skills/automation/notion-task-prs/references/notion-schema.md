# Notion Field Mapping

Never change the Notion database schema, property names, or select/status options.

Map the existing database fields when present:
- status: open/to-do, pending review, done, blocked
- assignee/owner: Claude/agent/user
- priority
- due date
- done date
- PR URL
- branch
- repo/area/risk

If a useful field is missing, do not create it. Put the information in the task page/comment instead.

Selection rule:
Process tasks whose existing status means open/to-do and whose assignee field, if present, points to Claude/agent. Each agent must assess readiness after reading the page/comments. If not actionable, mark an existing blocked status when available and write the reason in the page/comment.
