---
name: agent-openclaw-codex-flow
description: Coordinate OpenClaw-triggered Codex work by project, issue, mode, session id, branch, and GitHub status. Use when Codex is launched by OpenClaw or when documenting the OpenClaw automation contract.
---

# Agent OpenClaw Codex Flow

Use this skill when Codex is running as part of the OpenClaw workflow.

## Roles

- Dev is the lead and final reviewer.
- OpenClaw is the coordinator, notification center, and session mapping owner.
- Codex is the coding agent.
- GitHub issues and PRs are the durable task log.

## OpenClaw Must Provide

- project name
- GitHub repository
- local repository path or worktree path
- issue number
- workflow mode: `init`, `reinit`, `plan`, `code`, or `merge`
- known Codex session id, if one exists
- branch name, if one exists
- latest user instruction from Discord or another control channel

## Session Mapping

OpenClaw owns the durable mapping:

`projectName-issue-<number> -> codex_session_id`

Store at least:

- project name
- repository full name
- issue number
- Codex session id
- session display name
- local repo path
- worktree path
- branch name
- last mode
- last run status
- last run timestamp

Codex session names are useful for humans, but the Codex session UUID is the reliable resume key.

## Command Contract

For a new session, OpenClaw should run a non-interactive command:

```bash
codex exec -C <repo-path> --json "<mode-specific prompt>"
```

For an existing session, OpenClaw should resume by UUID:

```bash
codex exec resume <codex-session-id> --json "<mode-specific prompt>"
```

Do not use `codex resume --all` for automation.
That command is a human TUI picker.

## Codex Responsibilities

- Read root and local `AGENTS.md`.
- Use `common-documentation-lookup`.
- Use `common-git-issue` for issue context and status.
- Use `common-git-pr` for PR creation, updates, review responses, and merge work.
- Keep durable progress in GitHub issue or PR comments.
- Keep responses to OpenClaw short: success, blocked, failed, and links or ids.

## Mode Behavior

`init`:

- read issue and latest comments
- read relevant docs
- refine goal, scope, acceptance criteria, constraints
- update issue body or add an issue comment
- do not code

`reinit`:

- read latest comments
- update issue understanding
- revise issue body or add clarification comment
- do not code unless explicitly instructed

`plan`:

- read issue and docs
- post an implementation plan to the issue
- identify risks, validation, and likely touched areas
- do not code

`code`:

- create or continue the issue branch
- create a worktree if the project workflow expects one
- implement the smallest change satisfying the issue
- run relevant checks
- push the branch
- update the issue with status and validation

`merge`:

- ensure PR exists and matches the issue
- update PR body if needed
- check merge readiness
- merge only with explicit maintainer approval
- update the issue with final status

