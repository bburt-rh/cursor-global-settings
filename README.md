# AI coding assistant configuration settings

Global rules and preferences for Cursor and Claude Code, optimized for Red Hat enterprise development workflows.

**New to AI coding assistants or Cursor rules?** Start with the [FAQ](docs/faq.md) for answers to common questions like "Do I need both files?" and "How do I know the rules are working?"

## What is this?

AI coding assistants (Cursor, Claude Code) accept configuration files that shape how they generate code, make architectural decisions, and interact with you. These files are injected as system context -- the AI reads them before responding to any request.

The configuration in this repository establishes guardrails and preferences for:

- Technology choices (Podman, FastAPI, OpenShift, Red Hat UBI)
- Code quality standards (error handling, file size limits, testing)
- Documentation formatting (sentence case, no contractions, no passive voice)
- Security and compliance (FIPS awareness, secrets management)
- AI/ML tooling (vLLM-compatible embeddings, MCP servers, LangChain)
- Communication style (direct, no assumptions, explain when asked)

## Quick install

### Cursor

1. Open Settings > Cursor Settings > Rules
1. Paste the contents of [`cursor-user-rules.md`](cursor-user-rules.md) into the User Rules field
1. (Optional) Copy [`CLAUDE.md`](CLAUDE.md) to your home directory (`~/CLAUDE.md`)

### Claude Code

1. Copy [`CLAUDE.md`](CLAUDE.md) to `~/CLAUDE.md`
1. Claude Code reads this file automatically for all projects

## What is included

| File | Purpose | Used by |
|------|---------|---------|
| [`CLAUDE.md`](CLAUDE.md) | Development preferences, tech stack, architecture decisions | Claude Code (auto-loaded from ~/), Cursor (if placed at ~/) |
| [`cursor-user-rules.md`](cursor-user-rules.md) | Code generation guardrails, formatting conventions, git practices | Cursor Settings > Rules |
| [`rules/*.mdc`](rules/) | Project-level rule examples | Cursor (`.cursor/rules/` in any project) |

## Overlap between files

`CLAUDE.md` and `cursor-user-rules.md` share some content (technology preferences, error handling philosophy, testing standards). Both files are kept self-contained so you can grab the one for your tool without assembling from fragments. The overlap is intentional and harmless.

## Customizing

Fork this repo and adjust to your preferences. Sections you are most likely to change:

- **Database Choices** -- your team may use different databases
- **AI/ML Stack** -- framework preferences vary by project
- **Architecture Principles** -- gRPC, event-driven, or other patterns may suit your work better
- **Markdown documentation format** -- adjust style rules to match your team's guide
- **MCP Server Publishing Strategy** -- depends on your internal infrastructure

Sections that are generally safe to keep as-is across Red Hat:

- **Environment & Platform** (Podman, UBI, OpenShift)
- **Security & Compliance** (FIPS, secrets management)
- **Error Handling Approach** (never hide errors, never mock to work around problems)
- **Code Generation Guidelines** (clean code, no AI slop, deployment awareness)

## What is Red Hat-specific

The following assume a Red Hat / OpenShift environment:

- Podman over Docker, Containerfile over Dockerfile
- Red Hat UBI base images (`registry.redhat.io/ubi9/*`)
- OpenShift deployment targets (BuildConfig, Pipelines/Tekton, ArgoCD)
- FIPS compliance awareness
- OAuth2/OIDC via OpenShift for auth
- OpenShift AI for model deployment

Everything else (error handling, testing, code organization, git practices, documentation formatting) applies to any development context.

## Project-level rules

Beyond global rules, Cursor supports per-project rules in `.cursor/rules/*.mdc`. These apply only when working in a specific repository. See [`rules/`](rules/) for an example showing the format.

Use project rules for:

- Repository-specific conventions (naming patterns, directory structure)
- Technology constraints unique to a project
- Team agreements that differ from your global defaults

## Further reading

- [`docs/install-cursor.md`](docs/install-cursor.md) -- Detailed Cursor installation instructions
- [`docs/install-claude-code.md`](docs/install-claude-code.md) -- Detailed Claude Code installation instructions
- [`docs/customizing.md`](docs/customizing.md) -- How to fork and adapt these rules
- [`docs/whats-included.md`](docs/whats-included.md) -- Explanation of each section and why it exists
- [`docs/faq.md`](docs/faq.md) -- Frequently asked questions for beginners

## License

Apache-2.0. See [LICENSE](LICENSE).
