---
name: common-git-pr
description: Prepare, update, review, or merge GitHub pull requests tied to source issues. Use when Codex is creating a PR, updating a PR body, responding to review comments, or finalizing an issue branch.
---

# Common Git PR

Use this skill for pull request work.

## PR Contract

One PR should normally map to one source issue.
The source issue number is the canonical work item id.

PR title format:

`<type>(<scope>): <description> (#<issue-number>)`

Allowed default types:

- `feat`
- `fix`
- `refactor`
- `test`
- `docs`
- `chore`
- `agent`

PR body should include:

`Closes #<issue-number>`

Use `Refs #<issue-number>` instead when the PR should not close the issue.

## Before Opening Or Updating A PR

- Confirm the branch belongs to the source issue.
- Confirm the branch is pushed.
- Confirm the PR is scoped to the issue.
- Run relevant validation or explain why validation could not be run.
- Summarize assumptions and risks.
- Link back to the source issue.

## Review Comments

When responding to PR review comments:

- read the unresolved review comments and latest issue context
- address actionable comments in focused commits
- do not rewrite unrelated code
- reply with what changed and what validation was run
- leave a clear note if a comment is intentionally not addressed

## Merge Mode

Only merge when explicitly instructed by the maintainer or by a trusted OpenClaw mode that carries maintainer approval.

Before merge:

- ensure checks are passing or explicitly accepted
- ensure the PR still matches the source issue
- ensure the issue has a final status comment
- prefer squash merge unless the project docs say otherwise

