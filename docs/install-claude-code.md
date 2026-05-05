# Installing in Claude Code

Claude Code reads a `CLAUDE.md` file from your home directory automatically. No configuration UI is needed.

## Installation

```bash
# Clone this repo (if you have not already)
git clone git@github.com:bburt-rh/cursor-global-settings.git

# Copy CLAUDE.md to your home directory
cp cursor-global-settings/CLAUDE.md ~/CLAUDE.md
```

Claude Code reads `~/CLAUDE.md` at the start of every session. Changes to the file take effect on the next session.

## How Claude Code uses CLAUDE.md

Claude Code loads `~/CLAUDE.md` as part of its system context. The content informs:

- Technology choices and architecture decisions
- Code generation style and preferences
- Error handling philosophy
- Testing standards
- Deployment targets and container preferences

Claude Code also reads any `CLAUDE.md` file in the current project root. If both exist, both are used (global + project-specific).

## Project-level CLAUDE.md

For project-specific instructions, create a `CLAUDE.md` in the repository root:

```bash
cd my-project
cat > CLAUDE.md << 'EOF'
# Project-specific instructions

Follow the conventions in this project:
- Use the existing database schema (do not propose migrations without asking)
- This project uses Flask (not FastAPI) for historical reasons
- See ARCHITECTURE.md for the service boundaries
EOF
```

Project-level CLAUDE.md supplements (does not replace) the global `~/CLAUDE.md`.

## Verifying

1. Start a new Claude Code session.
1. Ask: "What base images should I use for containers?"
1. Claude should respond with Red Hat UBI images, confirming `~/CLAUDE.md` is loaded.

## Updating

```bash
cd cursor-global-settings
git pull
cp CLAUDE.md ~/CLAUDE.md
```
