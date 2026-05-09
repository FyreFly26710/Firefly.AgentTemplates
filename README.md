# Firefly Agent Templates

This repository is a starter template for projects that use GitHub issues, OpenClaw, and Codex together.

## Intent

- Keep project-specific guidance close to the code.
- Keep reusable agent workflow skills in `.agents/skills`.
- Use GitHub issues as the source of truth for task scope.
- Let OpenClaw coordinate notifications and Codex session continuity.
- Let Codex implement focused issue branches and prepare pull requests.

## Structure

- `AGENTS.md` contains generic repository guidance.
- `.agents/skills/` contains reusable workflow skills.
- `.github/` contains issue and pull request templates.
- `src/client/web/AGENTS.md` is the placeholder for web-specific guidance.
- `src/server/AGENTS.md` is the placeholder for backend-specific guidance.
- `docs/agent-flow/` documents the issue-to-session workflow contract.

## Project Setup

After creating a new project from this template:

1. Replace placeholder project names and repository URLs.
2. Fill in `src/client/web/AGENTS.md` with the chosen frontend stack.
3. Fill in `src/server/AGENTS.md` with the chosen backend stack.
4. Add product docs and architecture docs under `docs/`.
5. Configure OpenClaw with the repository path, GitHub repo, and Codex session mapping store.

