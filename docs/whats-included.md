# What is included

A section-by-section explanation of the rules and why they exist.

## CLAUDE.md sections

### Environment and platform standards

Forces the AI to use Podman, Containerfile, Red Hat UBI base images, and target OpenShift. Without this, AI assistants default to Docker and generic base images that are not compliant with Red Hat infrastructure requirements.

### Python development standards

Enforces venv usage, prevents global package installs, and sets FastAPI as the preferred framework. Prevents the common AI mistake of suggesting `pip install` without a virtual environment or using outdated package versions from training data.

### Architecture principles

Establishes loose coupling via APIs, MCP servers for AI capabilities, and SSE/streamable-http for real-time communication. Prevents the AI from suggesting monolithic architectures or gRPC without being asked.

### AI/ML technology stack

Sets LangChain/LangGraph, vLLM-compatible embeddings, and Docling as the preferred tools. Prevents the AI from suggesting incompatible embedding models or deprecated frameworks.

### Database technology choices

Provides a decision matrix so the AI does not suggest a database type without context. Each use case (relational, document, graph, vector, cache) has a specific recommendation.

### Standard project structure

Defines a consistent directory layout so new projects all follow the same pattern. The AI uses this when scaffolding new projects.

### Prompt management standards

Establishes YAML as the format for prompt templates and defines the expected structure. Keeps prompts editable and outside of application code.

### Testing standards

Sets pytest as the framework, 80% coverage target, and TDD/BDD practices. Prevents the AI from generating code without tests or using inappropriate testing patterns.

### Deployment standards

Establishes GitOps (ArgoCD), OpenShift Pipelines (Tekton), and built-in monitoring as the deployment target. Prevents the AI from suggesting non-OpenShift deployment patterns.

### MCP server publishing strategy

Defines a multi-layered distribution approach (Python package, container, OpenShift manifests). Provides the AI with context for how MCP servers should be packaged and deployed.

### Code generation guidelines

The most behavioral section. Controls:

- **Architecture awareness** -- respect ARCHITECTURE.md files, edit in place (do not create new versions)
- **File organization** -- 512-line target, break into utilities when needed
- **Git operations** -- never commit on behalf of the user
- **Error handling** -- never mock to hide errors

## cursor-user-rules.md sections

### Code generation guidelines

Prevents common AI coding mistakes: generated slop, binary bloat, hardcoded paths, overwhelming CLI output. These are the most frequently triggered guardrails.

### Architecture

Respect existing architecture, edit files in place, ask about backward compatibility before making breaking changes.

### Agreeableness

Controls the AI's interpretation of questions. Prevents the AI from assuming a question implies disagreement or from being overly deferential.

### File size

The 512-line guideline reduces context saturation -- when files are too large, the AI loses track of earlier content and makes inconsistent edits.

### Environment and platform

Same as CLAUDE.md -- Podman, UBI, OpenShift. Duplicated here because Cursor User Rules and CLAUDE.md are consumed independently.

### Markdown documentation format

Enforces Red Hat documentation style: sentence case headings, no contractions, no passive voice, no emojis, spelled-out abbreviations. Prevents the AI from generating documentation that fails style reviews.

### Issue creation and commit messages

Establishes conventions for git workflow artifacts. Prevents verbose, redundant commit messages and ensures issues have sufficient context.
