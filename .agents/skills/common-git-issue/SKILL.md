---
name: common-git-issue
description: Handle GitHub issue-driven work. Use when Codex must read, refine, update, label, comment on, or execute against a GitHub issue as the source of truth.
---

# Common Git Issue

Use this skill as the entry point for GitHub issue work.

## Source Of Truth

The GitHub issue is the canonical task definition.
Read the issue body and latest comments before acting.

Extract:

- issue number
- issue title
- goal
- scope
- acceptance criteria
- constraints
- latest maintainer comments
- linked PRs or related issues

## Modes

OpenClaw may trigger Codex with one of these modes.

- `init`: read the issue, inspect relevant docs, and refine the issue. Do not code.
- `reinit`: read new comments and update the issue understanding. Do not code unless explicitly asked.
- `plan`: write or update an implementation plan in the issue. Do not code.
- `code`: implement the issue on the issue branch, validate, push, and prepare review.
- `merge`: create or update the PR and merge only when the workflow and maintainer instruction allow it.

If the mode is missing, infer conservatively from the prompt and issue state.
When unsure, do `init` or `plan`, not `code`.

## Status Comments

Keep GitHub visible as the durable work log.

Use concise comments for:

- `in progress`: Codex has picked up the issue and states the branch/session context.
- `blocked`: Codex cannot continue without clarification, access, failing dependency, or a decision.
- `ready for review`: implementation and validation are complete enough for maintainer review.

Do not send large implementation details only to OpenClaw.
Write durable status to GitHub so the maintainer can review remotely.

## Labels

When labels are available, keep these aligned:

- always keep `codex` on Codex-assisted issues
- keep `co-op` for human-led collaborative work
- use exactly one current state label: `in-progress`, `blocked`, or `ready-for-review`

If label operations fail, continue and mention the failure in the issue status comment or final summary.

## Branch Rules

For implementation work, use:

`issue-<number>-<short-kebab-title>`

Do not use PR numbers as work item ids.
The issue number remains the canonical id.

## Blocking Rules

Block instead of guessing when:

- the goal is unclear
- acceptance criteria are missing for a risky change
- the requested scope conflicts with repository rules
- credentials, APIs, or external systems are unavailable
- implementation would require broad unrelated refactoring

