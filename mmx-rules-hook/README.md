# MMX Rules Guard Plugin

A MiniMax plugin that enforces mandatory safety rules before risky agent actions.

## What It Does

Before the agent executes any risky action (file delete, shell command, git force-push, admin API call, etc.), this plugin:

1. **Identifies** the action and classifies its risk level
2. **Shows** the applicable safety rules (from your MMX rules repo)
3. **Requires** explicit user confirmation with "I confirm"
4. **Blocks** the action if not confirmed
5. **Verifies** the result after execution

## Installation

### Option 1: From Local Directory (Development)

```bash
# Copy the plugin to your local plugin directory
cp -r mmx-rules-hook ~/.minimax/plugins/mmx-rules-hook

# OR if using a profile:
cp -r mmx-rules-hook ~/.minimax-<profile>/plugins/mmx-rules-hook

# Then in mcode TUI:
mcode plugin marketplace list  # shows local plugin directory
# Enable the plugin:
mcode plugin enable mmx-rules-hook@local
```

### Option 2: From This Repository

```bash
# Clone or download this repo
git clone https://github.com/soniaschu/mmx.git
cd mmx/mmx-rules-hook

# Copy to your local plugins:
cp -r . ~/.minimax/plugins/mmx-rules-hook

# Enable in mcode:
mcode plugin enable mmx-rules-hook@local
```

## Mandatory Rules Enforced

✅ Never expose secrets in source, logs, reports or browser state  
✅ Admin APIs require explicit authentication and permission checks  
✅ Destructive operations require explicit approval  
✅ Use least privilege  
✅ Reality before assumption  
✅ Cause before symptom  
✅ Proof before claim  
✅ No fake done  
✅ Security and data integrity before convenience  

## How to Use

### In mcode TUI

1. Open `/plugins` in mcode
2. Search for "mmx-rules-hook"
3. Enable it with `Space`
4. When you ask the agent to do something risky:
   - The plugin will show the applicable rules
   - You'll see a confirmation prompt
   - Type "I confirm" to proceed
   - Type anything else or timeout to cancel

### Via CLI

```bash
# List available plugins
mcode plugin list --available --marketplace local

# Enable the plugin
mcode plugin enable mmx-rules-hook@local

# Disable the plugin
mcode plugin disable mmx-rules-hook@local

# Remove the plugin
mcode plugin remove mmx-rules-hook@local
```

## Covered Actions

- 🔴 **Shell execution** (npm, bash, python, etc.)
- 🔴 **File operations** (create, write, delete)
- 🔴 **Git operations** (push, force-push, rebase)
- 🔴 **Admin API calls** (permissions, config changes)
- 🔴 **External requests** (API calls to external services)
- 🔴 **Destructive operations** (delete, overwrite)

## Example Workflow

```
You: "Delete all .log files in the temp directory"

[mcode agent analyzes the action]

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

You type: `I confirm`

```
✅ Confirmed. Deleting files...
[actual deletion happens]
✅ Verification: Deleted 12 files, freed 50.2MB
```

## Project Alignment

This plugin enforces rules from your MMX governance rules:

- `00-core.mdc` - Work from actual project state
- `00-mody-contract.md` - Reality before assumption, proof before claim
- `01-autonomous-development.md` - Self-sufficient loops with verification
- `05-security.mdc` - Never expose secrets, require approval
- `02-no-fake-done.mdc` - No completion without verification

## License

MIT (or your chosen license)

## Author

soniaschu
