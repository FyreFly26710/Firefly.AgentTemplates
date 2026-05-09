# AGENTS.md

## Repository Role

This repository is designed for issue-driven agent collaboration.
GitHub issues define the requested work, OpenClaw coordinates task triggers and session continuity, and Codex performs focused implementation work.

## Core Principles

- Treat the GitHub issue as the source of truth for issue-driven work.
- Keep one issue mapped to one focused branch and one reviewable pull request.
- Prefer small, explicit changes over broad refactors.
- Follow local `AGENTS.md` files before introducing new conventions.
- Do not rename files, folders, APIs, or public contracts unless the issue requires it.
- Do not add dependencies unless the need is clear and documented.
- Keep assumptions visible in issue comments, PR summaries, or docs.
- Update docs when architecture, workflow, or delivery behavior changes materially.

## Repository Structure

- `.agents/skills/` contains reusable agent skills for issue handling, documentation lookup, PR work, planning, frontend work, and backend work.
- `.github/` contains issue and pull request templates for Codex-assisted work.
- `src/client/web/` contains the web client area and its local `AGENTS.md`.
- `src/server/` contains the backend/server area and its local `AGENTS.md`.
- `docs/` contains project, architecture, and agent workflow documentation.

## Skill Naming Convention

Skills live under `.agents/skills/<scope>-<skill-desc>/SKILL.md`.

Use stable scope prefixes:

- `common-` for workflow and repository-wide skills.
- `frontend-` for general frontend work.
- `web-` for web-client architecture and implementation.
- `backend-` for server-side work.
- `agent-` for OpenClaw/Codex coordination.

Examples:

- `common-documentation-lookup`
- `common-git-issue`
- `common-git-pr`
- `frontend-ui-design`
- `web-architecture`
- `backend-tdd`
- `agent-openclaw-codex-flow`

## Issue-Driven Workflow

For GitHub issue work:

1. Read the issue and latest comments.
2. Read this file, relevant local `AGENTS.md` files, and relevant docs.
3. If the issue is unclear, update the issue with a refinement comment or revised issue body before coding.
4. When implementation is requested, create or continue the issue branch.
5. Keep progress visible in GitHub issue or PR comments.
6. Run relevant checks before handing work back.
7. Prepare a focused PR tied to the source issue.

OpenClaw should track the durable mapping between:

- project name
- GitHub repository
- issue number
- Codex session id
- branch name
- worktree or checkout path
- current workflow mode

Codex should not rely on the interactive session picker for automation.

## Branch And PR Rules

- Branch names should be `issue-<number>-<short-kebab-title>`.
- PR titles should be `<type>(<scope>): <description> (#<issue-number>)`.
- PR bodies should include `Closes #<issue-number>` when the PR should close the issue.
- Use the source GitHub issue number as the canonical work item id.
- Do not use the PR number as a substitute for the issue number.

## Local Guidance

Child folders may define their own `AGENTS.md`.
When guidance conflicts, prefer the most specific `AGENTS.md` that applies to the files being changed, unless the root guidance defines a workflow rule.

