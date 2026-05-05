# Installing in Cursor

Cursor reads user rules from its Settings interface and project rules from `.cursor/rules/` in your repository.

## User rules (global)

User rules apply to every project you open in Cursor.

1. Open Cursor.
1. Go to **Settings** > **Cursor Settings** > **Rules**.
1. In the **User Rules** text area, paste the full contents of [`cursor-user-rules.md`](../cursor-user-rules.md).
1. Close settings. The rules take effect immediately for all new agent interactions.

To update later, replace the text with the latest version from this repo.

## CLAUDE.md (optional, recommended)

Cursor also reads a `CLAUDE.md` file placed in your home directory. This provides additional context that supplements the User Rules.

```bash
cp CLAUDE.md ~/CLAUDE.md
```

If both User Rules and `~/CLAUDE.md` exist, Cursor uses both. They complement each other -- User Rules focus on code generation guardrails and formatting, while CLAUDE.md covers broader architecture and technology stack decisions.

## Project-level rules (per-repo)

For rules that apply only to a specific repository, create `.cursor/rules/` in that repo and add `.mdc` files. See the [`rules/`](../rules/) directory for an example.

```bash
mkdir -p .cursor/rules
cp /path/to/cursor-global-settings/rules/example-project.mdc .cursor/rules/my-project.mdc
```

Edit the `.mdc` file to match your project's conventions. These rules are version-controlled with the repo and shared with anyone who clones it.

## Verifying the rules are active

After setting up:

1. Start a new chat or agent session in Cursor.
1. Ask: "What container runtime should I use?"
1. The agent should respond with Podman (not Docker), confirming the rules are loaded.

## Updating

Pull the latest from this repo and re-paste into Settings. There is no automatic sync mechanism -- user rules are stored in Cursor's internal config, not as a file you can symlink.
