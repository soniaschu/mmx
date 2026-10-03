# Rule: Never expose secrets

Never expose secrets in source, logs, reports or browser state.

## Required behavior

- Do not print credentials or tokens.
- Do not write them to logs or source files.
- Redact them before reporting.
