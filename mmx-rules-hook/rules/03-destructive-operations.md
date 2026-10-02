# Rule: Destructive operations need approval

Destructive operations require explicit approval.

## Why this matters

Deletes, resets, force-pushes, and destructive changes are often irreversible.

## Required behavior

- Show the target and the impact before execution.
- Require explicit confirmation.
- Prefer backups, snapshots, or narrowly scoped change sets.
- Never delete or reset broadly without confirmation.
