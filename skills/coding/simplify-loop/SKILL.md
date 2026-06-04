---
name: simplify-loop
description: Repeatedly run the /simplify workflow until no new actionable simplification issues are found. Use when the user invokes /simplify-loop or asks to keep simplifying until clean.
---

# /simplify-loop

Run the `/simplify` workflow repeatedly on the same scope until a pass finds no new actionable simplification issues.

Workflow:

1. Establish the scope from recently modified files or the user's requested paths.
2. Run one `/simplify` pass.
3. Apply only behavior-preserving improvements.
4. Verify with existing tests, type checks, linters, or focused checks when practical.
5. Run `/simplify` again on the updated scope.
6. Stop only when the next pass finds no new actionable issues.

Stop early if:

- A proposed change risks behavior.
- A pass only finds cosmetic churn.
- Five passes have completed and issues are still appearing; report the remaining pattern instead of looping indefinitely.

Report the iteration count, files changed, verification run, and any remaining tradeoffs.
