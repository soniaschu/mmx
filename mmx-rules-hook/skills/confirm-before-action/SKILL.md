---
keywords: [confirmation, approval, safety, risky-action, destructive, secrets, verification, proof]
match: any
---

# Confirm Before Action

Before any risky or security-relevant action, require explicit acknowledgment of the applicable MMX rules and stop until the user confirms.

## Mission

This skill enforces the rules in the MMX governance set before the agent performs operations that could affect security, data integrity, or project state.

## Mandatory rules

1. Never expose secrets in source, logs, reports or browser state.
2. Admin APIs require explicit authentication and permission checks.
3. Destructive operations require explicit approval.
4. Use least privilege.
5. Reality before assumption.
6. Cause before symptom.
7. Proof before claim.
8. No fake done.
9. Security and data integrity before convenience.

## Required behavior

### 1. Detect the action

Classify the action before it runs:
- shell execution
- file writes or deletes
- git operations such as push / force-push / clean
- admin or privileged API calls
- external network requests
- data mutation or destructive changes

### 2. Detect the risk

Mark the action as:
- Critical: secret exposure, admin privilege changes, destructive operations, network calls with sensitive data
- High: file deletion, git force operations, broad shell execution, broad writes or resets
- Medium: less destructive but still state-changing actions

### 3. Show the applicable rules

Display a short approval prompt with:
- action summary
- risk level
- relevant rules
- explicit confirmation phrase

### 4. Require explicit confirmation

The user must type exactly:

I confirm

If the user does not confirm, the action is blocked.

### 5. Verify after execution

After the action runs, verify actual output before reporting success. If output is unclear or missing, report the result as unverified and do not claim completion.

## Confirmation template

```text
⚠️ MMX confirmation gate

Action: <what the agent is about to do>
Risk: <critical | high | medium>

Applicable rules:
- <rule 1>
- <rule 2>
- <rule 3>

To proceed, type: I confirm
To cancel: stop and do not run the action.
```

## Non-negotiable requirements

- Never proceed silently on risky actions.
- Never hide applicable rules.
- Never allow a critical or high-risk action without explicit confirmation.
- Never report success without proof from actual output.
- Never skip safety checks for speed or convenience.
