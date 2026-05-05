# Customizing these rules

Fork this repository and adjust the rules to match your team's preferences, technology stack, and workflow.

## How to fork and maintain

1. Fork this repo on GitHub.
1. Edit the files to match your preferences.
1. Periodically pull upstream changes and merge what applies.

```bash
# Add upstream remote
git remote add upstream git@github.com:bburt-rh/cursor-global-settings.git

# Pull latest changes
git fetch upstream
git merge upstream/main
```

## What to customize

### Technology stack

The defaults assume a Red Hat OpenShift environment. If your team uses different infrastructure, update these sections:

- **Database Choices** -- swap PostgreSQL/MongoDB/Neo4j for your stack
- **Container Runtime** -- if your team uses Docker, remove the Podman preference
- **Deployment** -- replace OpenShift/ArgoCD/Tekton with your CI/CD
- **AI/ML Stack** -- adjust frameworks and model deployment targets

### Code style preferences

- **File size limit** -- 512 lines is a guideline, not a hard rule. Adjust if your team has a different convention.
- **Markdown format** -- the documentation rules (sentence case, no contractions, no passive voice) follow the Red Hat Supplementary Style Guide. Adjust for your style guide.
- **Commit messages** -- the conventional commit format may differ from your team's convention.

### Interaction style

The "Agreeableness" section controls how the AI interprets your questions. Adjust if you prefer a different communication style.

## What NOT to customize (recommendations)

These sections encode universally good practices. Changing them typically leads to worse outcomes:

- **Error Handling Approach** -- hiding errors always causes problems downstream
- **No Binary Bloat** -- large binaries in git cause permanent repo bloat
- **Clean Commit History** -- always valuable regardless of project
- **Deployment Awareness** -- hardcoded paths break in production

## Creating team variants

If your team has shared conventions that differ from this baseline:

1. Fork this repo into your team's org/group.
1. Make team-specific edits.
1. Document changes in a CHANGELOG at the top of each file.
1. Team members clone the team fork (not this upstream repo).

This approach gives you a stable baseline to pull updates from while maintaining team-specific overrides.
