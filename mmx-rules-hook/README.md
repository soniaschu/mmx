# MMX Rules Guard Plugin

This plugin enforces MMX's operating rules before the agent runs a risky action.

## What this plugin does

It blocks risky actions until the user explicitly confirms the action and the applicable safety rules.

Risky actions include:
- shell operations
- writes and deletes in the workspace
- git push / force-push / reset / clean operations
- admin or privilege-changing calls
- calls that may expose secrets or sensitive data
- external requests with data or credentials

## Required rules enforced

1. Never expose secrets in source, logs, reports or browser state.
2. Admin APIs require explicit authentication and permission checks.
3. Destructive operations require explicit approval.
4. Use least privilege.
5. Reality before assumption.
6. Cause before symptom.
7. Proof before claim.
8. No fake done.
9. Security and data integrity before convenience.

## Local marketplace installation

This repository includes a local marketplace layout so it can be used as a direct plugin source for MiniMax:

```text
marketplace/
  mmx-rules-hook/
    .minimax-plugin/
    hooks/
    skills/
    rules/
```

To install from the local marketplace, copy the plugin folder into the active local plugin directory used by your MiniMax profile:

```bash
cp -r marketplace/mmx-rules-hook ~/.minimax/plugins/
# or for a named profile:
# cp -r marketplace/mmx-rules-hook ~/.minimax-<profile>/plugins/
```

Then enable it in the TUI:

```bash
mcode plugin list --available --marketplace local
mcode plugin enable mmx-rules-hook@local
```

## Manual install

```bash
cp -r mmx-rules-hook ~/.minimax/plugins/
mcode plugin enable mmx-rules-hook@local
```

## Confirm flow

When a risky command is about to run, the plugin shows a prompt like:

```text
⚠️ MMX confirmation gate

Action: Delete temp logs
Risk: high

Applicable rules:
- Destructive operations require explicit approval.
- Proof before claim.
- Security and data integrity before convenience.

To proceed, type: I confirm
```

If the user does not type exactly `I confirm`, the action stops.

## Rule files

The rule set is split into dedicated files so each rule is explicit and reviewable:
- `rules/01-security.md`
- `rules/02-admin-and-permissions.md`
- `rules/03-destructive-operations.md`
- `rules/04-least-privilege.md`
- `rules/05-reality-before-assumption.md`
- `rules/06-proof-before-claim.md`
- `rules/07-no-fake-done.md`
- `rules/08-safety-before-convenience.md`

## Alignment with MMX repo rules

This plugin is built from the governing principles in your MMX repository:
- `00-core.mdc`
- `00-mody-contract.md`
- `01-autonomous-development.md`
- `02-no-fake-done.mdc`
- `05-security.mdc`
