---
keywords: [confirmation, rules, safety, approval, risky-action, destructive, secrets, admin]
match: any
---

# Confirm Before Action

Enforce mandatory safety rules before risky agent actions. Require explicit acknowledgment and confirmation.

## Mission

Before any action that could affect security, data integrity, or project state, identify the risk and show the applicable rules. Only proceed after explicit user confirmation.

## Mandatory Rules

These rules apply to all risky actions:

1. **Never expose secrets** in source, logs, reports or browser state.
   - Applies to: file writes, external requests, shell commands, git operations
   - If the action would output secrets or store them unencrypted → block and warn

2. **Admin APIs require explicit authentication and permission checks.**
   - Applies to: admin API calls, privileged operations
   - Verify credentials and scope before proceeding

3. **Destructive operations require explicit approval.**
   - Applies to: file deletes, git force-push, SQL drops, cache clears, state mutations
   - Show what will be deleted/changed and why
   - Require confirmation phrase: "I confirm"

4. **Use least privilege.**
   - Applies to: admin calls, shell execution, file operations
   - Use minimal permissions and scope necessary
   - Avoid overly broad patterns or wildcards

5. **Reality before assumption.**
   - Applies to: file writes, shell execution
   - Check actual state before making changes
   - Do not invent files, tests, results, or success
   - Verify the project exists in the actual state

6. **Cause before symptom.**
   - Applies to: all actions
   - Understand root cause, not just surface symptoms
   - Make targeted fixes, not blanket changes

7. **Proof before claim.**
   - Applies to: shell execution, tests, build, git operations
   - Verify results with actual output
   - Do not assume success; run verification

8. **No fake done.**
   - Applies to: all actions
   - Completion without sufficient verification is not a real result
   - Incomplete work or unverified changes are not acceptable

9. **Security and data integrity before convenience.**
   - Applies to: file deletes, force-push, admin calls, external requests
   - Never skip safety checks for speed
   - Do not allow "move fast and break things" approach

## Behavior

### Before Action Execution

1. **Identify** the intended action (shell command, file operation, git command, API call, etc.).
2. **Classify** the risk level:
   - **Critical**: secrets exposure, destructive without backups, admin operations, external calls with sensitive data
   - **High**: file deletes, force-push, unverified shell, permission changes
   - **Medium**: file writes, git operations, local builds
3. **Map** applicable rules from the mandatory list above.
4. **Display** the confirmation prompt:
   ```
   ⚠️  Risky Action Requires Confirmation
   
   Action: [description of what will happen]
   Risk Level: [critical|high|medium]
   
   Applicable Rules:
   - [Rule 1]
   - [Rule 2]
   - [Rule N]
   
   To proceed, type: I confirm
   To cancel: (Ctrl+C or no response)
   ```
5. **Wait** for explicit user confirmation with phrase "I confirm".
6. **If confirmed**: proceed with the action once.
7. **If denied or timeout**: stop immediately, do not execute.

### After Action Execution

1. **Verify** the actual result with real output.
2. **Compare** claimed result with actual result.
3. **Document** what was changed and proof (logs, file diffs, test output).
4. **Report** completion only if verification passed.

## Examples

### Example 1: File Delete (Destructive)

```
⚠️  Risky Action Requires Confirmation

Action: Delete files matching 'temp/**/*.log' (12 files, ~50MB)
Risk Level: HIGH

Applicable Rules:
- Destructive operations require explicit approval.
- Use least privilege.
- Proof before claim.

Files to delete:
  temp/logs/app.2026-10-01.log (15MB)
  temp/logs/app.2026-10-02.log (18MB)
  temp/logs/system.log (17MB)
  [9 more files]

To proceed, type: I confirm
```

### Example 2: Shell Command (Unverified)

```
⚠️  Risky Action Requires Confirmation

Action: Execute shell: npm run build && npm test
Risk Level: HIGH

Applicable Rules:
- Reality before assumption.
- Proof before claim.
- No fake done.

This command will:
1. Build the project (output will be verified)
2. Run all tests (results must pass)

To proceed, type: I confirm
```

### Example 3: Admin API Call

```
⚠️  Risky Action Requires Confirmation

Action: Update user permissions via admin API (grant admin role to user_id=42)
Risk Level: CRITICAL

Applicable Rules:
- Admin APIs require explicit authentication and permission checks.
- Use least privilege.
- Security and data integrity before convenience.

Verify:
- Your authentication token has admin scope: ✓
- User ID 42 is correct: [you must verify]
- You intend to grant admin role: [confirm]

To proceed, type: I confirm
```

### Example 4: Secrets in Output (Blocked)

```
⚠️  Risky Action BLOCKED

Action: Upload log to external service
Reason: Log contains secrets (API keys, tokens)

Applicable Rule:
- Never expose secrets in source, logs, reports or browser state.

This action has been BLOCKED to prevent secret exposure.
To proceed safely:
1. Redact secrets from the log
2. Use a secure, authenticated channel
3. Verify encryption in transit and at rest
```

## Integration Points

### Hook Events

- `before_tool_call`: Intercept shell, file_write, file_delete, git_push, admin_api_call, external_request
- `after_tool_call`: Verify result against stated intent

### User Confirmation

- Phrase: "I confirm"
- Must be explicit and intentional
- Timeout: 5 minutes
- No auto-retry or workarounds

### Logging

- Log all risky actions and confirmations
- Include user response, timestamp, action details
- Keep audit trail for compliance

## Non-Negotiable

- **Never** proceed without explicit confirmation for critical/high-risk actions.
- **Never** hide rules or make them optional.
- **Never** allow "proceed anyway" without user typing the exact phrase.
- **Never** assume verification passed; check actual output.
- **Never** skip safety checks for convenience or speed.
