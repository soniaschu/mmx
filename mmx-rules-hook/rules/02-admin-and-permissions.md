# Rule: Explicit permissions for admin actions

Admin APIs require explicit authentication and permission checks.

## Why this matters

Privileged operations can create irreversible state changes and safety issues.

## Required behavior

- Verify the identity and authority before running privileged calls.
- Limit the action to the smallest necessary scope.
- Confirm the target and the effect before proceeding.
- Do not assume a token is valid or sufficient.
