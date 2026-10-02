---
keywords: [confirmation, approval, safety, verification, rule, guard]
match: any
---

# Confirm Before Action

Before any risky action, require explicit confirmation of the relevant MMX safety rules.

## Rules to apply

- Never expose secrets in source, logs, reports or browser state.
- Admin APIs require explicit authentication and permission checks.
- Destructive operations require explicit approval.
- Use least privilege.
- Reality before assumption.
- Cause before symptom.
- Proof before claim.
- No fake done.
- Security and data integrity before convenience.

## Mandatory flow

1. Detect the action and classify the risk.
2. Show the applicable rules.
3. Wait for the exact phrase `I confirm`.
4. Continue only if confirmed.
5. Verify actual output before reporting success.
