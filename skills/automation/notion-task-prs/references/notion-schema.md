# Notion Schema

Required properties:
- `Status`: `To-do`, `Plan ready`, `Approved for implementation`, `Pending review`, `Done`, `Blocked`
- `Me/Claude`: assignee selector; process `Claude`
- `Priority`: sortable priority
- `Due Date`
- `Done date`
- `Plan`
- `PR URL`
- `Branch`
- `Failure reason`

Optional useful properties:
- `Repo`
- `Area`
- `Risk`

Status flow:
`To-do` -> `Plan ready` -> `Approved for implementation` -> `Pending review` -> `Done`

Use `Blocked` only when the agent cannot proceed without human input or unsafe assumptions.
