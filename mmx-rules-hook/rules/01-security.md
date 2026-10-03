# Rule: Never expose secrets

Never expose secrets in source, logs, reports or browser state.

## Why this matters

Secrets are high-risk and can create data leaks, credential misuse, or unauthorized access.

## Required behavior

- Do not print API keys, tokens, passwords, cookies, session IDs, or bearer values.
- Do not store them in source files or generated logs.
- Do not place them in browser state, query strings, or clipboard-copy outputs.
- Use redaction before reporting or logging.

## If a secret is exposed

1. Stop the operation.
2. Redact or revoke the secret.
3. Verify the issue and confirm the environment is clean.
