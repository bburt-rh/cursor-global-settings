# Frequently asked questions

Common questions from people new to AI coding assistant configuration.

## Why are there two files (CLAUDE.md and cursor-user-rules.md)? Do I need both?

Cursor reads both User Rules (from Settings) and ~/CLAUDE.md (from your home directory). They arrive at the same place -- system context the AI reads before responding -- but they are different mechanisms:

- **User Rules** (cursor-user-rules.md): Stored internally by Cursor. Edited through the Settings UI. Always applied to every project. Cannot be version-controlled or shared without copy-paste. Cursor-only -- does not work in Claude Code.

- **~/CLAUDE.md**: A file on disk. Version-controllable, shareable via git. Works in both Cursor AND Claude Code. Updated with a simple file copy.

Both files are kept self-contained so you can grab one without needing the other. If you only use Cursor, pasting User Rules is sufficient. If you use both Cursor and Claude Code, ~/CLAUDE.md gives you coverage in both tools from a single file. The overlap between them is intentional -- it ensures guardrails are present regardless of which setup path someone follows.

## What happens if a rule in my global config conflicts with a project rule?

Project-level rules (.cursor/rules/*.mdc or a project-root CLAUDE.md) are applied alongside global rules. When they conflict, the AI generally follows the more specific (project-level) instruction. For example, if your global config says "use FastAPI" but a project CLAUDE.md says "this project uses Flask for historical reasons," the AI follows the project rule for that repo.

## Do these rules guarantee the AI will always follow them?

No. Rules are strong guidance, not hard constraints. The AI reads them as context and follows them in the vast majority of cases, but it can still make mistakes -- especially for complex or ambiguous requests. Think of rules as setting defaults and preventing common errors, not as enforcement mechanisms.

## I do not use OpenShift or Red Hat tooling. Can I still use these rules?

Yes. Fork the repo and remove or replace the Red Hat-specific sections (Podman, UBI images, OpenShift, FIPS). Everything else -- error handling, testing standards, code organization, git practices, documentation formatting -- applies to any development context. See [customizing.md](customizing.md) for guidance on what to change.

## How do I know the rules are working?

Start a new chat session and ask a question that the rules should influence. For example:

- "What container runtime should I use?" (should say Podman, not Docker)
- "Create a new Python project" (should use venv, FastAPI, pytest)
- "Write a Dockerfile" (should correct to Containerfile)

If the AI responds according to the rules, they are loaded correctly.

## Do I need to restart Cursor after changing User Rules?

No. Changes to User Rules take effect on the next new chat or agent session. You do not need to restart the application. However, an already-open session uses the rules that were loaded when it started.

## How often should I update these rules?

Pull from this repo when you notice the AI making decisions you disagree with repeatedly, or when your team's technology stack changes. There is no fixed cadence -- update when the rules no longer match reality.

## What is an .mdc file?

An .mdc file is a Cursor project rule. It lives in .cursor/rules/ within a repository and contains YAML frontmatter (description, glob patterns) plus markdown content. Cursor reads these files and applies them as context when you work in that project. See [rules/example-project.mdc](../rules/example-project.mdc) for the format.

## Can I use these rules with other AI coding tools (Copilot, Windsurf, etc.)?

The rules are written for Cursor and Claude Code specifically. Other tools have their own configuration mechanisms. However, the content (technology preferences, coding standards) is transferable -- you would just need to adapt it to the format your tool expects.

## Can I use the Cursor rules in another AI assistant like Claude Code?

Yes. The `CLAUDE.md` file in this repo works in both Cursor and Claude Code without modification -- copy it to `~/CLAUDE.md` and both tools read it automatically. The `cursor-user-rules.md` content is Cursor-specific in format (it goes into the Settings UI), but the underlying guidance is plain markdown. To use it in Claude Code, copy the relevant sections into your `~/CLAUDE.md` or a project-level `CLAUDE.md`. Claude Code does not have a separate "user rules" mechanism -- `~/CLAUDE.md` is its equivalent.

## How do these rules interact with skills and agent files?

Skills (SKILL.md) and agents (subagent .md files) provide task-specific instructions that the AI follows when a skill is invoked or an agent is dispatched. Global rules, project rules, and skill/agent instructions all coexist in the AI's context simultaneously. The priority order is roughly:

1. **Skill/agent instructions** -- most specific. When a skill is active, its instructions take precedence for that task.
2. **Project rules** (.cursor/rules/*.mdc, project-level CLAUDE.md) -- apply to the current repo.
3. **Global rules** (User Rules, ~/CLAUDE.md) -- broadest scope, lowest priority when they conflict with something more specific.

In practice, conflicts are rare because they operate at different levels. Your global rules say "use Podman" (technology choice), while a skill says "run this specific script to lint a file" (task instruction). They do not contradict each other -- they layer. If a skill explicitly needs to override a global rule (for example, a skill that generates Docker-specific content for upstream compatibility), the skill's instructions win for that invocation.

## My team has different conventions. Should I fork or override with project rules?

It depends on the scope of the differences:

- A few project-specific exceptions: use .cursor/rules/*.mdc in that repo.
- Broadly different technology stack: fork this repo into your team org and maintain your own baseline.
- Minor personal preferences: edit your own User Rules directly.
