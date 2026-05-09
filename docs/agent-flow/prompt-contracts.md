# Prompt Contracts

These prompt contracts are intended for OpenClaw when launching Codex.

## Shared Prompt Fields

Every prompt should include:

```text
Project: <projectName>
Repository: <owner/repo>
Local path: <repo-path>
Issue: #<issueNumber>
Session name: <projectName>-issue-<issueNumber>
Mode: <init|reinit|plan|code|merge>
Branch: issue-<issueNumber>-<short-kebab-title>
```

Also include:

```text
Read AGENTS.md and relevant local AGENTS.md files first.
Use .agents/skills/common-documentation-lookup.
Use .agents/skills/common-git-issue for issue context and status.
Use .agents/skills/common-git-pr for PR work.
Write durable details to GitHub issues/PRs.
Return a short status summary for OpenClaw.
```

## Init Prompt

```text
Mode: init

Read issue #<issueNumber> and latest comments.
Read root AGENTS.md, relevant local AGENTS.md files, and relevant docs.
Refine the issue into Goal, Scope, Acceptance Criteria, Constraints, and Context.
Update the issue body or add a concise issue comment with the refined task shape.
Do not modify implementation files.
Return only whether initialization completed, blocked, or failed.
```

## Reinit Prompt

```text
Mode: reinit

Read issue #<issueNumber> and all new comments since the last run.
Update the issue understanding based on maintainer feedback.
Revise the issue body or add a concise clarification comment when useful.
Do not modify implementation files unless the maintainer explicitly requested code in this run.
Return only whether reinitialization completed, blocked, or failed.
```

## Plan Prompt

```text
Mode: plan

Read issue #<issueNumber>, latest comments, AGENTS.md, and relevant docs.
Post an implementation plan to the issue.
The plan should include touched areas, steps, validation, risks, and open questions.
Do not modify implementation files.
Return only whether planning completed, blocked, or failed.
```

## Code Prompt

```text
Mode: code

Read issue #<issueNumber>, latest comments, AGENTS.md, and relevant docs.
Create or continue branch issue-<issueNumber>-<short-kebab-title>.
Implement the smallest change satisfying the issue.
Run relevant validation.
Commit and push the branch.
Update the issue with status, validation, assumptions, and risks.
Create or update the PR when appropriate.
Return only branch, PR link if available, validation status, and whether the run completed, blocked, or failed.
```

## Merge Prompt

```text
Mode: merge

Read issue #<issueNumber>, linked PR, review comments, and latest checks.
Only merge if maintainer approval is explicit in the triggering instruction or PR state.
If merge is not safe, report blocked with the reason.
After merge, update the issue with final status.
Return only whether merge completed, blocked, or failed.
```

